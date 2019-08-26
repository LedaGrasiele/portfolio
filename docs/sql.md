#### **SQL**

**Structured Query Language (SQL)** ou Linguagem de Consulta Estruturada é uma linguagem de consulta utilizada por bancos de dados relacionais. Os comandos SQL permitem que haja uma interação com o banco de dados, executando diversas tarefas desde inserção até edição e exclusão de dados e tabelas.
</br>
</br>

#### **Banco de dados relacional versus não relacional**

A principal diferença entre banco de dados relacional e não relacional tem a ver com o modo como as informações são inseridas e organizadas.
</br>
</br>
O banco de dados relacional oferece maior consistência e confiabilidade, mas exige o relacionamento entre várias tabelas para o acesso à informação. Já o não relacional tem como vantagem uma escalabilidade maior, com a informação agrupada e armazenada no mesmo registro.
</br>
</br>
O **banco de dados relacional** utiliza tabelas para a sua organização. Com a ajuda da linguagem **SQL**, as informações são guardadas nas linhas e nas colunas. Porém, para que seja possível inserir coisas nas tabelas, é preciso projetar cada estrutura.
</br>
</br>
Um **banco de dados não relacional** tem como diferencial a oferta de melhor performance e alta escalabilidade. Garante um gerenciamento mais eficiente, com linguagem **NoSQL**. Não exige a elaboração de um esquema antes de sua implementação, pois todas as informações ficam agrupadas em um único registro. Por isso, é necessário fazer cada um deles de modo que o banco consiga entender.
</br>
</br>

Nesta documentação estarão presentes os principais comandos da linguagem. Vale destacar que os comandos podem ter pequenas variações entre os vários Sistema de Gerenciamento de Banco de Dados (SGBDs) existentes como Oracle, PostgreSQL, SQLite, Microsoft SQL Server, MySQL etc.
</br>
</br>
#### **Principais comandos de SQL:**

</br>
#####  **1. Select**

A sintaxe é a seguinte:

```sql
SELECT <lista_de_campos>
FROM <nome_da_tabela><nome_da_tabela><lista_de_campos>
```

Segue um exemplo:

```sql
SELECT CODIGO, NOME FROM CLIENTES
SELECT * FROM CLIENTES
```

Colocar o asterisco significa que queremos todos os campos.

</br>
##### **2. Where**

O comando Where permite que haja condições de filtragem. Exemplo:

```sql
SELECT CODIGO, NOME FROM CLIENTES
WHERE CODIGO = 10
SELECT CODIGO, NOME FROM CLIENTES
WHERE UF = ‘RJ’
SELECT CODIGO, NOME FROM CLIENTES
WHERE CODIGO >= 100 AND CODIGO <= 500
SELECT CODIGO, NOME FROM CLIENTES
WHERE UF = ‘MG’ OR UF = ‘SP’
```

Parênteses também podem ser usados, como no exemplo a seguir:
```sql
SELECT CODIGO, NOME FROM CLIENTES
WHERE UF = ‘RJ’ OR (UF = ‘SP’ AND ATIVO = ‘N’)
```

Nesse exemplo, todos os clientes do Rio de Janeiro e apenas os clientes inativos de São Paulo seriam capturados.

Outro exemplo:

```sql
SELECT CODIGO, NOME FROM CLIENTES
WHERE (ENDERECO IS NULL) OR (CIDADE IS NULL)
```

Nesse caso, todos os clientes que não possuem endereço ou cidade cadastrada serão selecionados.

</br>
##### **3. Like**

Para busca parcial de string, o SELECT fornece o operador LIKE.

```sql
SELECT CODIGO, NOME FROM CLIENTES
 WHERE NOME LIKE ‘MARIA%’
```

No comando acima, serão retornados todos os clientes cujos nomes iniciam com Maria. Se quisermos retornar os nomes que contenham ‘MARIA’ também no meio, podemos adicionar o símbolo "%" antes do nome MARIA. Veja a seguir:

```sql
SELECT CODIGO, NOME FROM CLIENTES
WHERE NOME LIKE ‘%MARIA%’
```

Outra dica é que por padrão, a SQl diferencia caixa baixa e caixa alta. Para eliminar essa diferença, utiliza a função UPPER:

```sql
SELECT CODIGO, NOME FROM CLIENTES
WHERE UPPER(NOME) LIKE ‘MARIA %SILVA%’
```

</br>
##### **4. Order By**

O comando para ordenção é o ORDER BY. Veja no exemplo a seguir:

```sql
SELECT CODIGO, NOME FROM CLIENTES
ORDER BY NOME
SELECT CODIGO, NOME FROM CLIENTES
ORDER BY UF, NOME
```

A palavra DESC especifica uma ordenação invertida, ou seja, decrescente:

```sql
SELECT CODIGO, NOME FROM CLIENTES
ORDER BY NOME DESC
SELECT CODIGO, NOME FROM CLIENTES
ORDER BY UF DESC
```

</br>
##### **5. Join**

A junção de tabelas pode ser feita com o comando JOIN. 

Este comando deve ser utilizado com a palavra INNER ou OUTER:

- INNER: semelhante ao uso do operador “=” na junção de tabelas. Aqui os registros sem correspondências não são incluídos. Esta cláusula é opcional e pode ser omitida no comando JOIN.

- OUTER: os registros que não se relacionam também são exibidos. Neste caso, é possível definir qual tabela será incluída na seleção, mesmo não tendo correspondência.

Observe os exemplos a seguir:

```sql
SELECT A.CODIGO, A.DESCRICAO, B.DESCRICAO, B.QTD
FROM PRODUTOS A
INNER JOIN COMPONENTES B
ON (A.CODIGO = B.CODPRODUTO)
```

Este comando pode ser escrito na versão resumida abaixo:

```sql
SELECT A.CODIGO, A.DESCRICAO, B.DESCRICAO
FROM PRODUTOS A
JOIN COMPONENTES B
ON (A.CODIGO = B.CODPRODUTO)
```

Como mostrado no resultado 1, os produtos que não possuem componentes não são incluídos na seleção.

```sql
SELECT A.CODIGO, A.DESCRICAO, B.DESCRICAO, B.QTDE
FROM PRODUTOS A
LEFT OUTER JOIN COMPONENTES B
ON (A.CODIGO = B.CODPRODUTO)
```

No comando acima todos os produtos serão incluídos na seleção, independente de possuírem um componente. Observe que a palavra LEFT se refere à primeira tabela do relacionamento.

</br>
##### **6. Union**

Há uma segunda forma de juntar tabelas com o comando SELECT: através do parâmetro UNION, em que é possível colar o conteúdo de duas tabelas. Exemplo:

```sql
SELECT CODIGO, NOME FROM CLIENTES
UNION
SELECT CODIGO. NOME FROM FUNCIONARIOS
```

O resultado deste comando é a listagem de todos os clientes e a listagem de todos os funcionários, dentro do mesmo result set. No comando JOIN á união é horizontal e no UNION a união é vertical.
</br>
</br>
Por padrão, os registros duplicados são eliminados na cláusula UNION. No exemplo anterior, se tivéssemos um cliente com o mesmo nome e código de um funcionário, apenas o registro da primeira tabela seria exibido. Para incluir todos os registros, independente de duplicidade, utilize a palavra ALL:

```sql
SELECT CODIGO, NOME FROM CLIENTES
UNION ALL
SELECT CODIGO, NOME FROM FUNCIONARIOS
```

</br>
##### **7. Group By**

Um poderoso recurso do comando SELECT é o parâmetro GROUPY BY. Através dele podemos retornar informações agrupadas de um conjunto de registros, estabelecendo uma condição de agrupamento. É um recurso muito utilizado na criação de relatórios. Para exemplificar, temos as tabelas CLIENTES E PEDIDOS a seguir:

```sql
SELECT CODCLIENTE, MAX(VALOR)
FROM PEDIDOS
GROUP BY CODCLIENTE
```

O comando acima retorna o maior valor de pedido de cada cliente.

```sql
SELECT CODCLIENTE, COUNT(*)
FROM PEDIDOS
GROUPY BY CODCLIENTE
```

Aqui vemos quantos pedidos foram feitos por cada cliente.

</br>
##### **8. Having**

Através do comando HAVING podemos filtrar a cláusula GROUP BY. Observe o comando abaixo:

```sql
SELECT CODCLIENTE, COUNT(*)
FROM PEDIDOS
GROUPY BY CODCLIENTE
HAVING COUNT(*) >= 2
```

Somente os clientes com 2 ou mais pedidos serão selecionados. O HAVING é utilizado, geralmente com alguma função de agrupamento. Para filtros normais, pode-se utilizar o comando WHERE. Observe o exemplo abaixo:

```sql
SELECT CODCLIENTE, COUNT(*)
FROM PEDIDOS
WHERE DATA > ‘06/10/2002’
GROUPY BY CODCLIENTE
HAVING COUNT(*) >= 2
```

</br>
##### **9. Funções de agrupamento**

**AVG**: retorna a média do campo especificado

```sql
SELECT AVG(VALOR) FROM PEDIDOS
```

**MIN/MAX/SUM**: retorna o menor valor, o maior e o somatório de um grupo de registros, respectivamente

```sql
SELECT MIN(VALOR) FROM PEDIDOS
SELECT MAX(VALOR) FROM PEDIDOS
SELECT AVG(VALOR) FROM PEDIDOS
```

**COUNT**: retorna a quantidade de itens da seleção

```sql
SELECT COUNT(CODIGO) FROM CLIENTES
```
</br>
</br>
Fontes consultadas: <a href="https://www.devmedia.com.br/sql-select-guia-para-iniciantes/29530" target="_blank">devmedia</a>, <a href=https://mercadoemfoco.unisul.br/banco-de-dados-relacional-e-nao-relacional-quando-utilizar/ target="_blank">mercadoemfoco</a>.
