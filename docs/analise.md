Nesta seção de análises de dados incluirei alguns exemplos de análises com dados reais. </br>

### **Análise exploratória de dados (PNAD)**

**Analisando a relação entre escolaridade e rendimentos**

O exemplo a seguir é de uma análise utilizando dados da Pesquisa Nacional por Amostra de Domicílios (PNAD). Esta análise foi feita para o primeiro artigo da minha dissertação de mestrado (que está disponível no link na página inicial deste site).

Importando os pacotes:
```python
In [1]: %matplotlib inline
        import pandas as pd
        import matplotlib.pyplot as plt
        import seaborn as sns
        from openpyxl import load_workbook
        sns.set(style='whitegrid', palette='muted')
```

```python

In [2]: pnad3 = (pd.read_csv('dados/pnad.csv')
                       .query('idade > 17')  # incluir apenas quem já poderia ter concluído o ensino médio
                       .query('freq_esc == 2')) # apenas quem não frequenta mais a escola

        pnad3['sexo'] = pnad3.sexo.astype('category') # transformando em categórica
        pnad3.sexo = pnad3.sexo.cat.rename_categories(['masculino', 'feminino'])

In [3]: pnad3.nivel_instrucao.value_counts()
Out[3]: 2.0    129671
        5.0    106461
        7.0     44608
        1.0     43232
        3.0     32718
        4.0     19527
        6.0      6754

In [4]: pnad3.nivel_instrucao = pnad3.nivel_instrucao.replace([4, 6], [3, 5])
        pnad3['nivel_instrucao'] = pnad3.nivel_instrucao.astype('category')
        pnad3.nivel_instrucao.cat.rename_categories(['sem instrução', 'fundamental inc.',
        'fundamental', 'médio', 'superior'], inplace=True)
        pnad3.nivel_instrucao.cat.as_ordered(inplace=True)

In [5]: pnad3.nivel_instrucao.value_counts()
Out[5]: fundamental inc.    129671
        médio               113215
        fundamental          52245
        superior             44608
        sem instrução        43232

In [6]: pnad4 = pnad3.query('nivel_instrucao == ["fundamental", "médio"]')
        # apenas quem possui ensino fundamental ou médio completo
        pnad4.nivel_instrucao.cat.remove_unused_categories(inplace=True)

In [7]: pnad4.nivel_instrucao.value_counts()
Out[7]: médio          113215
        fundamental     52245

In [8]: nivel = (pnad3.nivel_instrucao.value_counts(normalize=True)*100).round(1)
        nivel = pd.DataFrame(nivel).reset_index().iloc[[4, 0, 2, 1, 3]]
        nivel.columns = ['nível de instrução', '%']
        nivel
Out[8]:  	nível de instrução 	    %
        4 	     sem instrução 	 11.3
        0 	  fundamental inc.	 33.9
        2          fundamental 	 13.6
        1 	             médio 	 29.6
        3 	          superior   11.6
```

**Ocupações mais comuns (maiores de 17 que não frequentam a escola)**

```python
In [9]: temp = (pnad4.query('nivel_instrucao == "médio"').ocup_cod
                .value_counts(normalize=True)*100).round(1)
        temp = pd.DataFrame(temp).reset_index()
        temp.columns = ['ocup_desc', 'médio']

        temp = (pnad4.query('nivel_instrucao == "médio"').ocup_desc
        .value_counts(normalize=True)*100).round(1)
        temp = pd.DataFrame(temp).reset_index()
        temp.columns = ['ocup_desc', 'médio']

        temp2 = (pnad4.query('nivel_instrucao == "fundamental"').ocup_desc
        .value_counts(normalize=True)*100).round(1)
        temp2 = pd.DataFrame(temp2).reset_index()
        temp2.columns = ['ocup_desc', 'fundamental']

        temp3 = temp.merge(temp2)
        temp3['diferença'] = temp3.fundamental - temp3.médio
In [10]: ocup_fund = temp3.sort_values('fundamental', ascending=False).head(10)
         ocup_fund
Out[10]:                            ocup_desc 	  médio   fundamental 	diferença
        3 	                 trab_serv_domest 	  3.5 	          7.4 	      3.9
        5 	                       agricultor 	  2.3             4.8 	      2.5
        10 	                        pedreiros 	  1.9         	  4.7 	      2.8
        4 	trab_limp_interior_edif_esc_hotel 	  2.6         	  4.0 	      1.4
        0 	                   balc_vend_loja 	  6.8         	  3.8      	 -3.0
        2 	                 comerciante_loja 	  3.7         	  3.6        -0.1
        14 	                     criador_gado 	  1.5         	  3.2 	      1.7
        8 	             cond_caminhão_pesado 	  2.0 	          3.2         1.2
        20 	            trab_element_agricult 	  1.2 	          3.1 	      1.9
        25 	         trab_element_constr_edif 	  0.9 	          2.4 	      1.5

In [11]: ocup_med = temp3.sort_values('médio', ascending=False).head(10)
         ocup_med
Out[11]:  	                        ocup_desc 	médio 	fundamental 	diferença
        0 	                   balc_vend_loja 	  6.8         	3.8 	     -3.0
        1                  escriturario_geral 	  3.9 	        1.0 	     -2.9
        2 	                 comerciante_loja 	  3.7 	        3.6 	     -0.1
        3 	                 trab_serv_domest 	  3.5 	        7.4 	      3.9
        4 	trab_limp_interior_edif_esc_hotel 	  2.6 	        4.0 	      1.4
        5 	                       agricultor 	  2.3 	        4.8 	      2.5
        6 	                       guarda_seg 	  2.2 	        1.8 	     -0.4
        7 	      cond_carro_taxi_caminhonete 	  2.2 	        1.9 	     -0.3
        9 	              caixa_exped_bilhete 	  2.0 	        0.8 	     -1.2
        8 	             cond_caminhão_pesado 	  2.0 	        3.2 	      1.2
```

**Rendimento médio de acordo com o nível de instrução** </br>
(maiores de 17 que não frequentam a escola)

```python
In [12]: pnad3.groupby('nivel_instrucao').rendimento.mean().plot.barh(color='gray',
         figsize=(7, 7))
         plt.ylabel('')
         plt.xlabel('rendimento médio', labelpad = 20)
         plt.savefig('figuras/rendimento.png', bbox_inches='tight');
Out[13]:
```

![analise-1](img/analise/analise-1.png)

```python
In [13]: pnad3.groupby('nivel_instrucao').rendimento.mean().round(0)
Out[13]: nivel_instrucao
         sem instrução        806.0
         fundamental inc.    1141.0
         fundamental         1357.0
         médio               1655.0
         superior            4251.0

```

**Rendimentos de acordo com o sexo e o nível de instrução** </br>
(maiores de 17 que não frequentam a escola e rendimentos menores do que 7 mil)

```python
In [14]: plt.figure(figsize=(11, 10))
         sns.boxplot('rendimento', 'nivel_instrucao', hue='sexo', color = 'gray',
                     data=pnad3.query('rendimento < 7000'))
         plt.xlabel('rendimento médio', labelpad = 20)
         plt.legend(bbox_to_anchor=(1,1))
         plt.ylabel('')
         plt.savefig('figuras/sexo.png', bbox_inches='tight');
Out[14]:
```
![analise-2](img/analise/analise-2.png)

```python
In [15]: pnad3.query('rendimento < 7000').groupby(['nivel_instrucao', 'sexo']).rendimento.median()
Out[15]: nivel_instrucao        sexo     
         sem instrução     masculino     700.0
                            feminino     500.0
         fundamental inc.  masculino    1000.0
                            feminino     930.0
         fundamental       masculino    1200.0
                            feminino     937.0
         médio             masculino    1500.0
                            feminino    1000.0
         superior          masculino    3000.0
                            feminino    2000.0
```

### **Análise exploratória e análise de regressão**

As análises a seguir se referem aos mesmos dados da análise apresentada anteriormente. A diferença é que agora, além de uma análise exploratória, é feita uma análise a partir de um modelo estatístico (modelo de regressão linear múltipla, nesse caso). </br>
Esta é uma técnica muito conhecida de machine learning.

```python

In [1]: %matplotlib inline
        import pandas as pd
        import numpy as np
        import scipy.stats as stats
        import statsmodels.formula.api as smf
        import statsmodels.api as sms
        from statsmodels.iolib.summary2 import summary_col
        from statsmodels.stats.outliers_influence import variance_inflation_factor
        import matplotlib.pyplot as plt
        import seaborn as sns
        pd.set_option('mode.chained_assignment', None)
        sns.set(style='whitegrid')

In [2]: pnad1 = pd.read_csv('dados/pnad.csv') # pnadc 2tri 2017
        pnad2 = pnad1.query('idade > 17') # apenas quem já poderia ter concluído o ensino médio
        pnad3 = pnad2.query('freq_esc == 2')
        pnad4 = pnad3.query('nivel_instrucao == [3, 5]')
        linha_vazia = pd.DataFrame([np.nan]).T
        pnad_zero = pnad4
        pnad_zero.rendimento = pnad_zero.rendimento.fillna(0)
        # trab. familiares aux., quem recebe em espécie, desocupados, donas de casa, nem nem
        pnad = pnad4.query('rendimento > 0')
        pnad = pnad.assign(rendimento_log=np.log(pnad.rendimento))
In [2]: print(' início: ', pnad1.shape[0], '\n',
        'idade > 17: ', pnad2.shape[0], '\n',
        'não freqenta a escola: ', pnad3.shape[0], '\n',
        'fundamental ou médio: ', pnad4.shape[0], '\n',
        'rendimento > 0: ', pnad.shape[0])
Out[2]:  início:  568313 
         idade > 17:  417664 
         não freqenta a escola:  382971 
         fundamental ou médio:  139179 
         rendimento > 0:  85122

In [3]: df = pnad1.query('idade > 25').nivel_instrucao.value_counts() / pnad1
        .query('idade > 25').shape[0]
In [4]: df[[1, 2, 3, 4]].sum()
Out[4]: 0.5989869557558413

In [5]: pnad.groupby('nivel_instrucao').rendimento.describe(percentiles=[.9, .95, .99])
Out[5]:        
                   count 	     mean 	       std 	 min 	 50% 	 90% 	 95% 	 99% 	   max
nivel_instrucao 									
            3.0  18459.0  1389.439135  1832.573276 	10.0  1100.0  2500.0  3000.0  6000.0  166666.0
            5.0  66663.0  1595.003810  1657.389486 	 4.0  1200.0  3000.0  4000.0  7000.0  100000.0

```

Para facilitar a visualização, foram retiradas as observações com valores mais altos (1% do ensino médio).

```python
In [6]: ocup_forca = pd.crosstab(pnad_zero.ocup_forca, pnad_zero.nivel_instrucao,
        normalize='columns').round(2) * 100
        ocup_forca.index = ['sim', 'não']
        ocup_forca = pd.concat([linha_vazia, ocup_forca])

        rendimento = (pnad_zero.groupby('nivel_instrucao').rendimento.describe(percentiles=[.5])
        .astype(int).T.iloc[1:, :])
        rendimento.index = ['média', 'desvio padrão', 'mínimo', 'mediana', 'máximo']

        idade = pnad_zero.groupby('nivel_instrucao').idade.describe(percentiles=[.5]).round(1)
        .T.iloc[1:, :]
        idade.index = ['média', 'desvio padrão', 'mínimo', 'mediana', 'máximo']
        idade = pd.concat([linha_vazia, idade])

        sexo = pd.crosstab(pnad_zero.sexo, pnad_zero.nivel_instrucao, normalize='columns')
        .round(2) * 100
        sexo.index = ['masculino', 'feminino']
        sexo = pd.concat([linha_vazia, sexo])

        ocup_pos2 = pd.crosstab(pnad_zero.ocup_pos2, pnad_zero.nivel_instrucao,
                    normalize='columns').round(4) * 100
        ocup_pos2.index = ['empregado s. priv. c/ cart.', 'empregado s. priv. s/ cart.',
                           'trabalhador domest. c/ cart.', 'trabalhadores domest. s/ cart.',
                           'empregado s. pub. c/ cart.', 'empregado s. pub. s/ cart.',
                           'militar e servidor estatutário', 'empregador', 
                           'trabalhador por conta própria', 'trabalhador familiar auxiliar']
        ocup_pos2 = pd.concat([linha_vazia, ocup_pos2])

        resumo1 = (pd.concat([sexo, ocup_forca, ocup_pos2, idade, rendimento], 
                    keys=['Sexo', 'Força de trabalho', 'Posição na ocupação', 'Idade',
                          'Rendimento'])
                   .drop(0, axis=1))
        resumo1.columns = ['Ensino fundamental', 'Ensino médio']
        resumo1
Out[6]:  		                                                Ensino fundamental   Ensino médio
                                                            0                  NaN 	          NaN
                       Sexo   	                    masculino                50.00 	        47.00
                                                     feminino 	             50.00 	        53.00
        	                                                0                  NaN 	          NaN
          Força de trabalho                               sim                66.00 	        75.00
                                                          não 	             34.00 	        25.00
                                                            0 	               NaN     	      NaN
        Posição na ocupação        empregado s. priv. c/ cart.               32.41          42.77
                                   empregado s. priv. s/ cart.               12.55          10.08
                                  trabalhador domest. c/ cart.                3.38           1.58
                                trabalhadores domest. s/ cart.                6.58           3.51
                                    empregado s. pub. c/ cart.                0.48           1.20
                                    empregado s. pub. s/ cart.                1.52           2.79
                                militar e servidor estatutário                3.03           8.22
                                                    empregador                4.21     	     4.31
                                 trabalhador por conta própria               32.10          22.91
                                 trabalhador familiar auxiliar                3.72     	     2.62
                                                             0 	               NaN     	      NaN
                      Idade                              média 	             43.00 	        37.60
                                                 desvio padrão 	             15.50 	        14.30
                                                        mínimo 	             18.00   	    18.00
                                                       mediana 	             42.00 	        35.00
                                                        máximo 	             99.00 	       107.00
                  Rendimento                             média 	            783.00 	       998.00
                                                 desvio padrão 	           1539.00 	      1521.00
                                                        mínimo 	              0.00 	         0.00
                                                       mediana 	            450.00 	       937.00
                                                        máximo 	         166666.00      100000.00
```

```python
In [7]: rendimento = (pnad.groupby('nivel_instrucao').rendimento.describe(percentiles=[.5])
                      .astype(int).T.iloc[1:, :])
        rendimento.index = ['média', 'desvio padrão', 'mínimo', 'mediana', 'máximo']
        
        idade = pnad.groupby('nivel_instrucao').idade.describe(percentiles=[.5]).round(1)
        .T.iloc[1:, :]
        idade.index = ['média', 'desvio padrão', 'mínimo', 'mediana', 'máximo']
        idade = pd.concat([linha_vazia, idade])
        
        sexo = pd.crosstab(pnad.sexo, pnad.nivel_instrucao, normalize='columns')
        .round(2)*100
        sexo.index = ['masculino', 'feminino']
        sexo = pd.concat([linha_vazia, sexo])
        
        ocup_pos2 = pd.crosstab(pnad.ocup_pos2, pnad.nivel_instrucao, normalize='columns')
        .round(2)*100
        ocup_pos2.index = ['empregado s. priv. c/ cart.', 'empregado s. priv. s/ cart.',
                           'trabalhador domest. c/ cart.', 'trabalhadores domest. s/ cart.',
                           'empregado s. pub. c/ cart.', 'empregado s. pub. s/ cart.',
                           'militar e servidor estatutário', 'empregador', 
                           'trabalhador por conta própria']
        ocup_pos2 = pd.concat([linha_vazia, ocup_pos2])
        
        resumo2 = (pd.concat([sexo, ocup_pos2, idade, rendimento], 
                            keys=['Sexo', 'Posição na ocupação', 'Idade', 'Rendimento'])
                           .drop(0, axis=1))
        resumo2.columns = ['Ensino fundamental', 'Ensino médio']
        resumo2

Out[7]:  	                                                    Ensino fundamental    Ensino médio
	                                                        0 	               NaN 	           NaN
                       Sexo                         masculino                 64.0 	          56.0
                                                     feminino 	              36.0 	          44.0
                                                            0 	               NaN 	           NaN
        Posição na ocupação 	  empregado s. priv. c/ cart.                 34.0 	          44.0
                                  empregado s. priv. s/ cart. 	              13.0 	          10.0
                                 trabalhador domest. c/ cart. 	               4.0 	           2.0
                               trabalhadores domest. s/ cart. 	               7.0 	           4.0
                                   empregado s. pub. c/ cart. 	               1.0 	           1.0
                                   empregado s. pub. s/ cart. 	               2.0 	           3.0
                               militar e servidor estatutário 	               3.0 	           8.0
                                                   empregador 	               4.0 	           4.0
                                trabalhador por conta própria 	              33.0 	          24.0
        	                                                0 	               NaN 	           NaN
                      Idade                             média 	              40.7            36.8
                                                desvio padrão 	              12.6	          11.9
                                                       mínimo 	              18.0 	          18.0
                                                      mediana 	              40.0 	          35.0
                                                       máximo 	              88.0 	         107.0
                 Rendimento                             média 	            1389.0 	        1595.0
                                                desvio padrão 	            1832.0 	        1657.0
                                                       mínimo 	              10.0             4.0
                                                      mediana               1100.0 	        1200.0
                                                       máximo 	          166666.0 	      100000.0
        
```

**Modelos de regressão**

```python
In [8]: modelo1 = smf.ols('rendimento ~ C(nivel_instrucao)', data=pnad).fit(cov_type='HC0')

        modelo2 = smf.ols('rendimento ~ C(nivel_instrucao) + C(sexo)', data=pnad)
        .fit(cov_type='HC0')
        modelo3 = smf.ols('rendimento ~ C(nivel_instrucao) + C(sexo) + idade', data=pnad)
        .fit(cov_type='HC0')
        modelo4 = smf.ols('rendimento ~ C(nivel_instrucao) + C(sexo) + idade + C(tipo_area)
                           + C(uf)', data=pnad).fit(cov_type='HC0')
        modelo5 = smf.ols('rendimento ~ C(nivel_instrucao) + C(sexo) + idade + C(tipo_area)
                           + C(uf)', data=pnad.query('rendimento < 7000'))
                           .fit(cov_type='HC0')
        modelo6 = smf.ols('rendimento ~ C(nivel_instrucao) + C(sexo) + idade + C(tipo_area)
                          + C(uf)', data=pnad_zero.query('rendimento < 7000'))
                          .fit(cov_type='HC0')
        
        lista = [modelo1, modelo2, modelo3, modelo4, modelo5, modelo6]
        strings = ['modelo1', 'modelo2', 'modelo3', 'modelo4', 'modelo5', 'modelo6']
        
        info_dict={'R-squared' : lambda x: "{:.2f}".format(x.rsquared),
                   'No. observations' : lambda x: "{0:d}".format(int(x.nobs))}
        
        tabela = summary_col(results=[modelo1, modelo2, modelo3, modelo4, modelo5, modelo6],
                                      float_format='%0.2f',
                                      model_names=['Modelo 1', 'Modelo 2', 'Modelo 3',
                                      'Modelo 4', 'Modelo 5', 'Modelo 6'],
                                      info_dict=info_dict,
                                      regressor_order=['Intercept', 'C(nivel_instrucao)[T.5.0]',
                                      'C(sexo)[T.2]', 'idade'])
        
        tabela.add_title('Resultados das regressões')
        
        print(tabela)
   
Out[8]:
                           Resultados das regressões
===============================================================================
                          Modelo 1 Modelo 2 Modelo 3 Modelo 4 Modelo 5 Modelo 6
-------------------------------------------------------------------------------
Intercept                 1389.44  1608.27   421.48   593.12   791.65   1022.69 
                          (13.49)  (15.03)  (22.80)  (51.66)  (27.11)   (23.13) 
C(nivel_instrucao)[T.5.0]  205.56   255.81   370.55   390.54   313.08    247.93  
                          (14.94)  (14.73)  (14.89)  (14.84)   (6.96)    (5.75)  
C(sexo)[T.2]                       -605.43  -622.28  -621.16  -491.00   -624.34 
                                   (10.51)  (10.43)  (10.27)   (5.77)    (5.25)  
idade                                         29.31    27.95    19.61      2.91    
                                             (0.56)   (0.56)   (0.28)    (0.19)  
C(tipo_area)[T.2]                                    -119.62   -74.47    -63.21  
                                                     (15.92)   (9.78)    (8.64)  
C(tipo_area)[T.3]                                    -126.08  -113.95    -50.25  
                                                     (46.09)  (29.41)   (25.59) 
C(tipo_area)[T.4]                                    -155.51  -149.21   -113.51 
                                                     (12.81)   (7.57)    (6.56)  
C(uf)[T.12]                                          -232.92  -240.07   -227.61 
                                                     (68.37)  (33.18)   (27.86) 
C(uf)[T.13]                                          -365.92  -383.51   -339.03 
                                                     (76.23)  (29.66)   (24.72) 
C(uf)[T.14]                                          -133.83  -113.02    -90.93  
                                                     (63.89)  (39.65)   (33.37) 
C(uf)[T.15]                                          -295.12  -282.39   -215.17 
                                                     (61.73)  (28.92)   (24.34) 
C(uf)[T.16]                                           163.45   -80.64   -160.69 
                                                    (198.67)  (46.53)   (36.78) 
C(uf)[T.17]                                           -61.94   -98.43   -107.63 
                                                     (69.34)  (34.76)   (29.82) 
C(uf)[T.21]                                          -409.75  -374.65   -339.82 
                                                     (52.39)  (26.70)   (22.64) 
C(uf)[T.22]                                          -344.83  -318.06   -250.81 
                                                     (58.60)  (32.78)   (26.82) 
C(uf)[T.23]                                          -449.65  -386.95   -315.40 
                                                     (50.89)  (27.03)   (22.94) 
C(uf)[T.24]                                          -370.28  -293.35   -256.09 
                                                     (54.58)  (31.85)   (26.62) 
C(uf)[T.25]                                          -383.93  -325.72   -262.32 
                                                     (54.69)  (31.24)   (25.93) 
C(uf)[T.26]                                          -330.66  -307.42   -299.42 
                                                     (54.70)  (28.54)   (23.95) 
C(uf)[T.27]                                          -338.04  -278.53   -304.69 
                                                     (53.66)  (29.07)   (24.28) 
C(uf)[T.28]                                          -212.63  -190.34   -191.11 
                                                     (61.08)  (34.94)   (28.68) 
C(uf)[T.29]                                          -383.05  -354.28   -271.71 
                                                     (53.19)  (27.58)   (23.43) 
C(uf)[T.31]                                           -22.60   -32.14     -1.90   
                                                     (52.30)  (26.35)   (23.04) 
C(uf)[T.32]                                            45.94    29.26     -0.02   
                                                     (55.17)  (28.91)   (25.16) 
C(uf)[T.33]                                           -41.95     2.85    -76.09  
                                                     (51.03)  (26.51)   (23.05) 
C(uf)[T.35]                                           153.48   162.41    120.14  
                                                     (51.56)  (26.19)   (23.02) 
C(uf)[T.41]                                           241.58   219.75    231.28  
                                                     (53.70)  (27.49)   (24.44) 
C(uf)[T.42]                                           410.28   421.08    369.57  
                                                     (52.00)  (26.98)   (24.16) 
C(uf)[T.43]                                           252.37   212.87    208.25  
                                                     (54.35)  (27.77)   (24.58) 
C(uf)[T.50]                                           242.22   182.67    215.63  
                                                     (61.22)  (32.85)   (29.66) 
C(uf)[T.51]                                           197.23   184.80    173.18  
                                                     (57.03)  (31.50)   (28.02) 
C(uf)[T.52]                                           102.61    89.90    120.61  
                                                     (56.47)  (29.78)   (26.31) 
C(uf)[T.53]                                           323.20   183.23    109.22  
                                                    (116.74)  (35.49)   (31.54) 
R-squared                    0.00     0.03     0.08     0.10     0.20      0.15    
No. observations            85122    85122    85122    85122    84147    138204  
===============================================================================
Standard errors in parentheses.             
```

**Modelo final**
 

Variáveis               | Modelo 1 | Modelo 2 | Modelo 3 | Modelo 4 | Modelo 5 | Modelo 6
----------------------- |----------| -------- | -------- | -------- | -------- | --------
Intercepto              | 1.389,44 | 1.608,27 | 421,48   | 593,12   |  791,65  |1.022,69
                        |  (13,49) | (15,03)  | (22,80)  | (51,66)  | (27,11)  | (23,13)
Nível instrução (médio) | 205,56   | 255,81   | 370,55   | 390,54   | 313,08   | 247,93
                        |(14,94)   | (14,73)  | (14,89)  | (14,84)  | (6,96)   | (5,75)
Sexo (feminino)         |          | -605,43  | -622,28  | -621,16  | -491,00  | -624,34       
                        |          | (10,51)  | (10,43)  | (10,27)  | (5,77)   | (5,25)
Idade                   |          |          | 29,31    | 27,95    | 19,61    | 2,91
                        |          |          | (0,56)   | (0,56)   | (0,28)   | (0,19)
Dummy tipo de área      | não      | não      | não      | sim      | sim      | sim
Dummy UF                | não      | não      | não      | sim      | sim      | sim
R2                      | 0,00     | 0,03     | 0,08     | 0,10     | 0,20     | 0,15 
Nº de observações       | 85.122   | 85.122   | 85.122   | 85.122   | 84.147   | 138.204

Esse modelo final é um resumo do modelo anterior. Ele foi resumido com o intuito de facilitar o entendimento e a visualização dos dados. </br>
A interpretação de cada um dos parâmetros pode ser vista com detalhes na <a href="https://drive.google.com/open?id=1Kql_KAfEerWjGXX89nBWbgDGTVAI5YHd" target="_blank">dissertação.</a> </br>