## **Excel avançado (versão 2010):**
Aqui veremos algumas funções mais avançadas do Excel, assim como algumas dicas de atalhos que podem ser utilizados e a descrição dos principais erros que podem ocorrer.
Então vamos lá!

</br>

#### **1. PROCV e PROCH**

Suponha que você tenha uma lista de números de localização do Office e precisa saber quais funcionários estão em cada escritório. A planilha é grande, portanto, você pode pensar que é uma tarefa desafiadora. Na verdade, é muito fácil fazer com uma função proc.

Aqui está um exemplo de como usar PROCV.

``=PROCV(B2,C2:E7,3,VERDADEIRO)`` 

Neste exemplo, B2 é o primeiro argumento, que é o valor que você deseja encontrar. Esse argumento pode ser uma referência de célula ou um valor fixo, como "Smith" ou 21.000. O segundo argumento é o intervalo de células, ``C2:E7``, no qual pesquisar o valor que você deseja encontrar. O terceiro argumento é a coluna nesse intervalo de células que contém o valor que você busca.

O quarto argumento é opcional. Insira verdadeiro ou falso. Se você inserir ``verdadeiro`` ou deixar o argumento em branco, a função retornará uma correspondência aproximada do valor especificado no primeiro argumento. Se você inserir ``falso``, a função corresponderá ao valor fornecido pelo primeiro argumento. Em outras palavras, deixar o quarto argumento em branco — ou inserir verdadeiro — oferece mais flexibilidade.

Vamos para um exemplo.

![exemplo_procv](img/excel/procv.jpg)

Vamos então para um exemplo de PROCH.

Bom, a função PROCH localiza um valor na linha superior de uma tabela ou matriz de valores e retorna um valor na mesma coluna de uma linha especificada na tabela ou matriz. Você deve usar PROCH quando seus valores de comparação estiverem localizados em uma linha ao longo da parte superior de uma tabela de dados e você quiser observar um número específico de linhas mais abaixo. Quando os valores de comparação estiverem em uma coluna à esquerda dos dados que você deseja localizar, use ``PROCV``.

</br>

#### **2. Função Índice** 
A função índice é usada para retornar um valor ou a referência a um valor de dentro de uma tabela ou intervalo. Esta função possui duas formas: a matricial e a referencial. Veremos cada uma delas a seguir.

</br>

##### **2.1 Matricial**
A forma matricial da função índice retorna o valor de um elemento em uma tabela ou uma matriz, selecionado pelos índices de número de linha e coluna (nesta ordem: primeiro a linha e depois a coluna).
A fórmula possui dois argumentos obrigatórios e um opcional: </br>
- o primeiro argumento é o intervalo de células da constante ou matriz; </br>
- o segundo é o número da linha (se ficar em branco, o número da coluna deve ser preenchido); </br>
- o terceiro (opcional) é o número da coluna.

A forma matricial deve ser usada se o primeiro argumento de ÍNDICE for uma constante de matriz.
Veja um exemplo a seguir.

![exemplo_indice_matricial](img/excel/indice_matricial.jpg)

</br>

##### **2.2 Referencial**
A função índice referencial retorna a referência da célula na interseção de linha e coluna específicas. Se a referência for composta de seleções não adjacentes, você poderá escolher a seleção que deseja examinar. 

Esta versão da função índice permite que você selecione mais de uma área (ou seja, pode ser usada também com mais de uma tabela).

A fórmula é composta por dois argumentos obrigatórios: </br>
- uma referência a um ou mais intervalos de célula; </br>
- o número da linha de onde será fornecidade uma referência; </br>
O número da coluna e da área são opcionais.

![exemplo_indice_referencial](img/excel/indice_referencial.jpg)

</br>

#### **3. Função Corresp**
A função Corresp procura um item especificado em um intervalo de células e retorna a posição relativa desse item no intervalo. Por exemplo, se o intervalo ``A1:A3`` contiver os valores 5, 25 e 38, a fórmula ``=CORRESP(25,A1:A3,0)`` retornará o número 2, porque 25 é o segundo item no intervalo.

Dica: Use Corresp no lugar de uma das funções PROC quando você precisar da posição de um item em um intervalo em vez do item propriamente dito. Por exemplo, você pode usar a função CORRESP para fornecer um valor para o argumento núm_lin da função ÍNDICE.

A sintaxe é composta por dois argumentos obrigatórios e um argumento opcional: </br>
- o primeiro argumento é o valor procurado por você, que pode ser um número, texto ou valor lógico. </br>
- o segundo item é a matriz procurada, ou seja, o intervalo de células a serem pesquisadas. </br>
- o terceiro item (opcional) é o tipo de correspondência, que especifica como o excel faz a correspondência do valor procurado. O valor padrão para este argumento é 1.

Segue um exemplo:

![exemplo_corresp](img/excel/corresp.jpg)

Tipo de correspondência | Comportamento
----------------------- | -------------
1 ou não especificado | CORRESP localiza o maior valor que é menor do que ou igual a valor procurado. Os valores no argumento matriz procurada devem ser colocados em ordem crescente; por exemplo: ...-2, -1, 0, 1, 2, ..., A-Z, FALSO, VERDADEIRO.
0 | CORRESP localiza o primeiro valor que é exatamente igual a valor procurado. Os valores no argumento matriz procurada podem estar em qualquer ordem.
-1 | CORRESP localiza o menor valor que é maior ou igual ao valor procurado. Os valores no argumento matriz_procurada devem ser colocados em ordem decrescente como, por exemplo: VERDADEIRO, FALSO, Z-A... 2, 1, 0, -1, -2... e assim por diante.

</br>

#### **4. Combinando as funções Índice e Corresp**

Como vimos anteriormente, os argumentos da função índice representam a posição de um dado em células organizadas em uma mesma linha, ou em uma mesma coluna, ou seja, justamente o que a função Corresp faz. Assim podemos incluir o Corresp nestes argumentos da função índice.

A tabela abaixo contém alguns dados sobre a população dos países membros do BRICS e queremos descobrir qual dos países tem o percentual de população feminina igual a 48,29%.

![exemplo_indice_corresp](img/excel/indice_corresp.jpg)

matriz → B6:B10 = área onde estão os dados com os nomes dos países. </br>
núm_linha → função CORRESP </br>
valor_procurado → C2 = célula onde está o valor do indicador que queremos a informação. </br>
matriz_procurada → F6:F10 = intervalo onde estão os dados do indicador desejado. </br>
[tipo_correspondência] → 0 (zero), pois é o valor que indica a função que queremos uma correspondência exata. </br>
[núm_coluna] → Não aparece na função. Se trata de um dado opcional e desnecessário neste caso, já que a área que selecionamos em matriz possui somente uma coluna. Deixar esse argumento em branco ou com o valor 1, dá na mesma.

Então, resumindo, o que dissemos para esta fórmula fazer foi: </br>
No intervalo de B6:B10, retorne o dado que estiver na mesma posição que o valor 48,29% está no intervalo de F6:F10. Ou seja, retorne o dado que estiver na 3ª posição no intervalo de B6:B10.

O resultado dessa fórmula é Índia, pois é o país com 48,29% de população feminina.

Fonte da questão <a href="https://www.funcaoexcel.com.br/indice-corresp-um-procv-melhorado/" target="_blank">aqui</a>.

</br>

#### **5. Função Somase**
A função somase é utilizada para somar os valores em um intervalo que atendem aos critérios estabelecidos.
Por exemplo, imagine que em uma coluna você precisa somar apenas os valores maiores do que 100. Você pode fazer isso usando a fórmula ``=SOMASE(C2:C11;">100")``. Note que o primeiro argumento da fórmula simplesmente define o intervalo escolhido e o segundo argumento define a condição estabelecida por você.
A seguir temos um exemplo de como usar essa função:

![exemplo_somase](img/excel/somase.jpg)

Outro exemplo: 

![exemplo_somase2](img/excel/somase2.jpg)

</br>

#### **6. Função Cont.se**
Esta função é usada para contar o número de células que atendem a um determinado critério. A função é composta por dois argumentos: </br>
- o primeiro argumento é o intervalo onde você quer procurar algo. </br>
- o segundo argumento é o seu critério. </br>
Por exemplo, ``CONT.SE(A2:A5;"maçãs")``. Este e outros exemplos podem ser observados a seguir:

![exemplo_contse](img/excel/contse.jpg)

</br>

#### **7. Função Cont.ses**
A função cont.ses aplica critérios a células em vários intervalos e conta o número de vezes que todos os critérios são atendidos.
A sintaxe da função tem dois argumentos obrigatórios: </br>
- O primeiro argumento é o intervalo no qual iremos avaliar os critérios estabelecidos. </br>
- O segundo argumento trata dos critérios que devem ser avaliados. </br>
Além disso, podem ser adicionados outros critérios, sendo permitidos até 127 critérios ou intervalos.
Seguem um exemplo:

![exemplo_contses](img/excel/contses.jpg)

Outro exemplo:

![exemplo_contses2](img/excel/contses2.jpg)

Observação: Se você pretende fazer a contagem usando um único critério, use a função ``cont.se``, já abordada anteriormente.

</br>

#### **8. Gráficos**

</br>

#### **9. Tabela Dinâmica**

</br>

#### **10. Gráfico Dinâmico**

</br>

#### **11. Dashboard**

</br>

#### **12. Guia Desenvolvedor**

</br>

#### **13. Macros**

**a) Botões para Macros** 
**b) Habilitar Macros** 
**c) Salvar pasta de trabalho**
**d) Criando uma Macro no VBE**

</br>

### **Atalhos:**

</br>

#### **1. Selecionar linhas e colunas:**
Primeira opção: clicar no número da linha ou no nome da coluna.
Segunda opção: parar na coluna de interesse e usar ctrl e espaço (seleciona a coluna inteira); ou parar na linda de interesse e pressionar ``shift`` + ``espaço`` (seleciona a linha inteira).

</br>

#### **2. Inserir linhas:**
Primeira opção: clicar no número da linha e clicar em Inserir ou clicar no número da linha e digitar ``i``.

Segunda opção: selecionar a linha abaixo da qual você pretende inserir uma nova linha (lembre-se da primeira dica: selecione a linha utilizando o atalho ``shift`` + ``espaço``). Depois que a linha estiver selecionada, pressione ``ctrl`` + ``+`` (caso não tenha o + separado no seu teclado, pressione ``ctrl`` + ``shift`` + ``+``).

Dica adicional: caso você queira incluir mais de uma linha, basta selecionar o número de linhas que você quer incluir segurando a tecla shift e indo com a seta para baixo ou para cima e depois usar o atalho para inserir as linhas (``ctrl`` + ``+``). O mesmo vale para as colunas.

</br>

#### **3. Apagar linhas:**
Para apagar a linha, o atalho segue a mesma ideia da dica anterior: selecione a linha e pressione ``ctrl`` + ``-``.

</br>

#### **4. Andando pelas células da planilha:**
Se você tem uma planilha com muitos dados e quer andar entre as células, há alguns atalhos úteis para isso:

Para ir para a última linha: ``ctrl`` + ``seta para baixo``; </br>
Para ir para a primeiro linha: ``ctrl`` + ``seta para cima``; </br>
Para ir para a primeira coluna: ``ctrl`` + ``seta para a esquerda``; </br>
Para ir para a última coluna: ``ctrl`` + ``seta para a direita``; </br>
Para ir para a primeira célula da planilha (A1): ``ctrl`` + ``home``.

</br>

#### **5. Selecionando linhas e colunas:**
Usando os mesmos atalhos da dica 4 juntamente com a tecla ``shift``, é possível selecionar várias linhas e várias colunas.

Ex.: para selecionar uma linha inteira (a partir da célula em que você está), pressione ``ctrl`` + ``shift`` + ``seta para cima`` ou ``seta para baixo``. O mesmo vale para selecionar várias colunas. Use os mesmos atalhos combinados com as setas para os lados.

Se a intenção é selecionar toda a sua planilha, pressione ``ctrl`` + ``*``. No caso de laptops, o ``*`` costuma ficar acima do número 8. Então o atalho é: ``ctrl`` + ``shift`` + ``8``.

</br>

#### **6. Aumentando a altura das linhas:**
Selecione todas as linhas. Lembra do nosso atalho para isso? Nesse caso, basta selecionar a primeira linha com o atalho ``shift`` + ``espaço`` e depois selecionar até a última linha com o atalho ``ctrl`` + ``shift`` + ``seta para baixo``.

Caso ache mais fácil, selecione tudo com o mouse ou marque a primeira linha e pressione ``shift`` + ``seta para baixo`` até chegar na linha desejada.
Depois, vá com o cursor até a linha entre os números das linhas. O cursor vai virar uma pequena cruz. Selecione e puxe para baixo deixando a linha do tamanho desejado. Com isso, todas as linhas ficarão com a mesma altura.

</br>

#### **7. Preenchendo as células automaticamente:**
Se você precisa enumerar algumas células do número 1 ao 100, por exemplo, você já sabe que pode inserir o número 1 em uma célula, o número 2 na célula seguinte, selecionar as duas, clicar com o mouse no canto inferior direito da célula de baixo e puxar para baixo, certo? Com isso, as próximas células serão preenchidas automaticamente até o número que você deseja.

Porém, se você colocar o indicador ordinal, assim: 1º, 2º, 3º etc. esse atalho não funciona mais, pois o tipo da célula muda.
Qual a solução então? Terei que digitar tudo até o 100 ou até o 500, 700, dependendo do caso? Não. Tem uma forma muito mais simples. Vamos lá!

Primeiro faça normalmente o primeiro passo (digitar os dois primeiros números, selecionar e puxar até o número desejado). Com isso, todos os números estarão selecionados. Se não estiverem, selecione-os. Então pressione ``ctrl`` + ``1`` e a aba de formatação de células será aberta (outro atalho bacana, olha só!). Clique em ``personalizado``, depois escolha o número ``0`` (ele provavelmente estará como ``geral``). Agora edite o ``tipo`` adicionando ``"º"`` (o símbolo de grau entre aspas) na frente do número e clique em ``ok``. Pronto! Parece complicado, mas é muito simples. É só seguir esses passos e a sua lista de números ordinais está pronta!

Ah, e caso você queira adicionar mais números, agora é só selecionar e puxar para baixo que vai funcionar normalmente.

</br>

#### **8. Tabela zebrada:**
Primeiro selecione a sua tabela (``ctrl`` + ``*``), depois clique em ``formatação condicional`` e em ``nova regra``. Escolha a última opção da lista (``Usar uma fórmula para determinar quais células devem ser formatadas``). 

Agora clique na caixa de texto logo abaixo e digite: ``=MOD(LIN();2)=0``.

O próximo passo é clicar em ``formatar`` ainda nesta janela. Com isso, uma nova janela será aberta. Selecione a opção ``preenchimento`` e escolha a cor desejada. Prontinho! Sua planilha agora tem uma linha de cada cor. Inclusive, você pode adicionar mais linhas que o padrão será mantido.

</br>

#### **Erros comuns no Excel**





