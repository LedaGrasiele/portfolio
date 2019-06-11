# Excel avançado (versão 2010):

## 1- Função Índice 
## a) Matricial
## b) Referencial
 
## 2- Função Corresp

## 3- Combinando as funções Índice e Corresp

## 4- Plano de fundo

## 5- Função Somases

## 6- Função Cont.ses

## 7- Erros do Excel

## 8- Gráficos

## 9- Tabela Dinâmica

## 10- Gráfico Dinâmico

## 11- Dashboard

## 12- Guia Desenvolvedor

## 13- Macros

## a) Botões para Macros
## b) Habilitar Macros
## c) Salvar pasta de trabalho
## d) Criando uma Macro no VBE



# **Atalhos:**

## 1- Selecionar linhas e colunas: 
Primeira opção: clicar no número da linha ou no nome da coluna.
Segunda opção: parar na coluna de interesse e usar ctrl e espaço (seleciona a coluna inteira); ou parar na linda de interesse e pressionar ``shift`` + ``espaço`` (seleciona a linha inteira).

## 2- Inserir linhas:
Primeira opção: clicar no número da linha e clicar em Inserir ou clicar no número da linha e digitar ``i``.

Segunda opção: selecionar a linha abaixo da qual você pretende inserir uma nova linha (lembre-se da primeira dica: selecione a linha utilizando o atalho ``shift`` + ``espaço``). Depois que a linha estiver selecionada, pressione ``ctrl`` + ``+`` (caso não tenha o + separado no seu teclado, pressione ``ctrl`` + ``shift`` + ``+``).

Dica adicional: caso você queira incluir mais de uma linha, basta selecionar o número de linhas que você quer incluir segurando a tecla shift e indo com a seta para baixo ou para cima e depois usar o atalho para inserir as linhas (``ctrl`` + ``+``). O mesmo vale para as colunas.

## 3- Apagar linhas:
Para apagar a linha, o atalho segue a mesma ideia da dica anterior: selecione a linha e pressione ``ctrl`` + ``-``.

## 4- Andando pelas células da planilha:
Se você tem uma planilha com muitos dados e quer andar entre as células, há alguns atalhos úteis para isso:

Para ir para a última linha: ``ctrl`` + ``seta para baixo``;
Para ir para a primeiro linha: ``ctrl`` + ``seta para cima``;
Para ir para a primeira coluna: ``ctrl`` + ``seta para a esquerda``;
Para ir para a última coluna: ``ctrl`` + ``seta para a direita``.
Para ir para a primeira célula da planilha (A1): ``ctrl`` + ``home``.

## 5- Selecionando linhas e colunas:
Usando os mesmos atalhos da dica 4 juntamente com a tecla ``shift``, é possível selecionar várias linhas e várias colunas.

Ex.: para selecionar uma linha inteira (a partir da célula em que você está), pressione ``ctrl`` + ``shift`` + ``seta para cima`` ou ``seta para baixo``. O mesmo vale para selecionar várias colunas. Use os mesmos atalhos combinados com as setas para os lados.

Se a intenção é selecionar toda a sua planilha, pressione ``ctrl`` + ``*``. No caso de laptops, o ``*`` costuma ficar acima do número 8. Então o atalho é: ``ctrl`` + ``shift`` + ``8``.

## 6- Aumentando a altura das linhas:
Selecione todas as linhas. Lembra do nosso atalho para isso? Nesse caso, basta selecionar a primeira linha com o atalho ``shift`` + ``espaço`` e depois selecionar até a última linha com o atalho ``ctrl`` + ``shift`` + ``seta para baixo``.

Caso ache mais fácil, selecione tudo com o mouse ou marque a primeira linha e pressione ``shift`` + ``seta para baixo`` até chegar na linha desejada.
Depois, vá com o cursor até a linha entre os números das linhas. O cursor vai virar uma pequena cruz. Selecione e puxe para baixo deixando a linha do tamanho desejado. Com isso, todas as linhas ficarão com a mesma altura.

## 7- Preenchendo as células automaticamente:
Se você precisa enumerar algumas células do número 1 ao 100, por exemplo, você já sabe que pode inserir o número 1 em uma célula, o número 2 na célula seguinte, selecionar as duas, clicar com o mouse no canto inferior direito da célula de baixo e puxar para baixo, certo? Com isso, as próximas células serão preenchidas automaticamente até o número que você deseja.

Porém, se você colocar o indicador ordinal, assim: 1º, 2º, 3º etc. esse atalho não funciona mais, pois o tipo da célula muda.
Qual a solução então? Terei que digitar tudo até o 100 ou até o 500, 700, dependendo do caso? Não. Tem uma forma muito mais simples. Vamos lá!

Primeiro faça normalmente o primeiro passo (digitar os dois primeiros números, selecionar e puxar até o número desejado). Com isso, todos os números estarão selecionados. Se não estiverem, selecione-os. Então pressione ``ctrl`` + ``1`` e a aba de formatação de células será aberta (outro atalho bacana, olha só!). Clique em ``personalizado``, depois escolha o número ``0`` (ele provavelmente estará como ``geral``). Agora edite o ``tipo`` adicionando ``"º"`` (o símbolo de grau entre aspas) na frente do número e clique em ``ok``. Pronto! Parece complicado, mas é muito simples. É só seguir esses passos e a sua lista de números ordinais está pronta!

Ah, e caso você queria adicionar mais números, agora é só selecionar e puxar para baixo que vai funcionar normalmente.

## 8- Planilha zebrada:
Primeiro selecione a planilha (``ctrl`` + ``*``), clique em ``formatação condicional`` e clique em ``nova regra``. Clique na última opção da lista (``Usar uma fórmula para determinar quais células devem ser formatadas``). 

Agora clique na caixa de texto logo abaixo e digite: ``=MOD(LIN();2)=0``.

O próximo passo é clicar em ``formatar`` ainda nesta janela. Com isso, uma nova janela será aberta. Clique em ``preenchimento`` e escolha a cor desejada. Prontinho! Sua planilha agora tem uma linha de cada cor. Inclusive, você pode adicionar mais linhas que o padrão será mantido.







