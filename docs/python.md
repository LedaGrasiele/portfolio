#### **Easter eggs**

Aqui estão três easter eggs:
``` python
in [1]: import __hello__
out[1]: Hello world!
```

Este segundo easter egg é o mais interessante. Basicamente vemos nele os "mandamentos" do Python: 
```python 
in [1]: import this
out[1]:
"""
The Zen of Python, by Tim Peters

Beautiful is better than ugly. 
Explicit is better than implicit. 
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
"""
```

Por fim, um terceiro easter egg é o seguinte comando: </br>
``` python
import antigravity
```

Se você executar esse código, você é levado a um quadrinho do site <a href="https://xkcd.com/" target="_blank">xkcd</a>. </br>
O quadrinho fica nesse <a href="https://xkcd.com/353/" target="_blank">link</a>. </br>

#### **Comandos básicos**
</br>

**Listas:** </br>
```python
in [1]: list1 = [1, 2, 3]
in [2]: list1[2]
out[2]: 3

in [3]]: list1[2] = 5
in [4]: list1
out [4]: [1, 2, 5]
```

**Dicionários** </br>
Aqui, em vez de acessar o valor com um índice, acessamos com valores de chaves (aqueles que estão entre {}):
```python
in [1]: dic = {'var1': 1, 'var2': 2}
in [2]: dic
out [2]: {'var1': 1, 'var2': 2}

in [3]: dic['var1'] = 3
in [4]: dic['var1']
out[4]: 3

in [5]: dic2 = {'list': [1,2,3], 'string': 'hello, world', 'number': 1.0}
in [6]: dic2
out[6]: {'list': [1, 2, 3], 'string': 'hello, world', 'number': 1.0}

in [7]: dic2['string']
out[7]: 'hello, world'

in [8]: type(dic2['number'])
out[8]: float

in [9]: dic2['list'][2]
out[9]: 3
```

**Tuplas** </br>

```python
As tuplas são semelhantes às listas, mas após a definição dos valores, não é permitido atribuir novos valores.

in [1]: tup = (1, 2, 3)
in [2]: tup
out[2]: (1, 2, 3)

in [3]: tup[1]
out[3]: 2

in [4]: tup[1]=3
out[4]: a saída será um erro, pois como foi dito, as tuplas não aceitam atribuições (assigments).
```

**Booleanos e operações lógicas** </br>

Resumo das operações: </br>

Operador | Comparação
-------- | ----------
== | igual a
!= | diferente de
< | menor que
> | maior que
<= | menor ou igual a
>= | maior ou igual a


```python
in [1]: x = 10
in [2]: x >= 10
out[2]: True

in [3]: x >= 10 and x < 11
out[3]: True

in [4]: x >= 10 or x > 20
out[4]: True

in [5]: x < 10 or x > 10
out[5]: False

in [6]: x == 10
out[6]: True

in [7]: x != 10
out[7]: False
```

**If, else e elif** </br>
```python
in [1]: x = 10
in [2]:
if x == 10:
    y = 'approved'
elif 5 < x < 6:
    y = 'retrieve'
else:
    y = 'disapproved'
print(y)
out[2]: approved

in [3]: y
out[3]: 'approved'

in [4]: x = 5.5
in [5]:
if x == 10:
    y = 'approved'
elif 5 < x < 6:
    y = 'retrieve'
else:
    y = 'disapproved'
print(y)
out[5]: retrieve
```

**Iteráveis (for, range e while)** </br>
```python
in [1]: x = [1, 2, 3, 4]
in [2]:
for i in x:
    print (i)
out[3]: 
1
2
3
4

in [4]:
for i in range(0,10):
    print(i)
out[5]:
0
1
2
3
4
5
6
7
8
9

in [6]: seq = list(range(0,10))
in [7]: seq
out[7]: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

**While** </br>

```python
in [1]: i = 1
in [2]:
while i < 5:
    print('i is: {}'.format(i))
    i = i + 1
out[2]:
i is: 1
i is: 2
i is: 3
i is: 4

in [3]]: out = []
in [4]: x = [1, 2, 3, 4]
in [5]:
for item in x:
    out.append(item**2)
out
out[5]: [1, 4, 9, 16]
```

**Funções** 

```python
in [1]:
x = 2
def my_func(param):
    exp = param**2
    return exp

in [2]: y = my_func(x)
in [3]: y
out[3]: 4
```

**Função lambda**

```python
in [1]:
def squared(var):
    return var**2
squared(2)
out[1]: 4

in [2]:
def squared(var): return var**2
squared(2)
out[2]: 4

in [3]: 
lambda var: var**2
squared(2)
out[3]: 4
```

**Funções map e filter**

```python
in [1]: seq = [1, 2, 3, 4, 5]
in [2]: map(squared, seq);
in [3]: list(map(squared, seq))
out[3]: [1, 4, 9, 16, 25]

in[4]: list(map(lambda x:x**2, seq))
out[4]: [1, 4, 9, 16, 25]

in[5]: list(filter(lambda item:item%2==0, seq))
ou[5]: [2, 4]
```

**Métodos**

```python
in [1]: hw = 'Hello, world!'
in [2]: hw.upper()
out[2]: 'HELLO, WORLD!'

in [3]: list = [1, 2, 3]
in [4]: list.append(4)
in [5]: list
out[5]: [1, 2, 3, 4]

in [6]: list.pop() # para remover valores de uma lista
out[6]: 4

in [7]: list
out[7]: [1, 2, 3]

in [8]: first = list.pop(0) # removendo um valor específico
in [9]: list
out[9]: [2, 3]

in [10]: 'x' in [1, 2, 3]
out[10]: False

in [11]: 'x' in [1, 2, 'x']
out[11]: True
```

**Split para strings**

´´´python
in [1]: text = ('Red, blue and black')
in [2]: text
out[2]: 'Red, blue and black'

in [3]: text.split()
out[3]: ['red,', 'blue', 'and', 'black']

in [4]: text.split('and')
out[4]: ['red, blue ', ' black']

in [5]: text.upper()
out[5]: 'RED, BLUE AND BLACK'

in [6]: text.lower()
out[6]: 'red, blue and black'
´´´

### **Numpy** 

```python
in [1]: import numpy as np

in [2]: my_list = [1, 2, 3]
in [3]: my_list
out[3]: [1, 2, 3]

in [4]: np.array(my_list)
out[4]: array([1, 2, 3])

in [5]: my_list[-1]
out[5]: 3
```

**Matriz (np.arange, np.linspace)**

```python
in [1]: my_matrix = [[1, 3, 3], [4, 5, 6], [7, 8, 9]]
in [2]: my_matrix
out[2]: [[1, 3, 3], [4, 5, 6], [7, 8, 9]]

in [3]: np.array(my_matrix)
out[3]: 
array([[1, 3, 3],
       [4, 5, 6],
       [7, 8, 9]])

in [4]: np.arange(0,10)
out[4]: array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

in [5]: np.arange(0, 10, 2) # the third argument defines the interval
out[5]: array([0, 2, 4, 6, 8])

in [6]: np.zeros(3)
out[6]: array([0., 0., 0.])

in [7]: ar = np.zeros((5, 5))
in [8]: ar
out[8]: 
array([[0., 0., 0., 0., 0.],
       [0., 0., 0., 0., 0.],
       [0., 0., 0., 0., 0.],
       [0., 0., 0., 0., 0.],
       [0., 0., 0., 0., 0.]])

in [9]: np.ones((3, 3))
out[9]:
array([[1., 1., 1.],
       [1., 1., 1.],
       [1., 1., 1.]])

in [10]: np.eye(4) # matriz identidade
out[10]: 
array([[1., 0., 0., 0.],
       [0., 1., 0., 0.],
       [0., 0., 1., 0.],
       [0., 0., 0., 1.]])

in [11]: np.linspace(0, 10, 3) # o terceiro argumento define quantos número queremos
out[11]: array([ 0.,  5., 10.])
```

**Numpy random**

```python

in [1]: np.random.rand(3) # números de 0 a 1
out[1]: array([0.41671642, 0.27110098, 0.68021772])

in [2]: np.random.rand(2) * 100 # nnúmeros de 0 a 100
out[2]: array([84.91907808, 18.09757989])

in [3]: np.random.rand(3, 2) # matriz 3x2
out[3]:
array([[0.97041758, 0.67253306],
       [0.0126004 , 0.86894573],
       [0.40713987, 0.66303445]])

in [4]: np.random.randn(4)
out[4]: array([ 0.64014424, -0.37955834,  0.60433726, -0.66348324])

in [5]: np.random.randint(0, 100, 10)
out[5]: array([43, 59, 56, 15, 76, 90, 43, 74, 70, 54])

in [6]: np.random.rand(4) * 100
out[6]: array([45.0946955 , 25.68386088, 50.81856534, 90.34075123])

in [7]: np.round(np.random.rand(4), 0) * 100
out[7]: array([  0., 100.,   0., 100.])

in [8]: arr = np.random.rand(25)
in [9]: arr
out[9]: 
array([0.70457937, 0.14398985, 0.31900377, 0.11890531, 0.56503378,
       0.56102052, 0.4487779 , 0.12641164, 0.97500985, 0.21741891,
       0.35641972, 0.91385335, 0.7476478 , 0.12000251, 0.39924327,
       0.21224457, 0.23037201, 0.74209167, 0.80416263, 0.07611099,
       0.21483552, 0.39899085, 0.14722631, 0.38143338, 0.06336958])

in [10]: arr2 = arr.reshape((5,5)) # matriz 5x5
in [11]: arr2.shape
out[11]: (5, 5)

in [12]: arr.max()
out[12]: 0.9750098522689852

in [13]: arr.mean()
out[13]: 0.39952620203645706

in [14]: arr.min()
out[14]: 0.06336957700117996

in [15]: arr.argmax() # mostra a posição do número máximo
out[15]: 8
```


















