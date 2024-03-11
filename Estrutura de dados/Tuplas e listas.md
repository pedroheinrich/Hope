# Tuplas e Listas

Os programas práticos precisam de estruturas de dados e o Hope já possui dois tipos padrão integrados. O tipo mais simples corresponde a um registro Pascal. Podemos vincular um número fixo de objetos de qualquer tipo em uma estrutura chamada tupla, por exemplo:

```
( 2, 3 )
```
ou
```python
( 'um', 'verdadeiro' )
```
são tuplas do tipo `num # num` e `char # truval` respectivamente. Usamos tuplas quando queremos que uma função defina mais de um valor. Aqui está um que define a hora do dia, considerando o número de segundos desde a meia-noite:

```
dez time24: num -> num # num # num;
--- tempo24 ( s ) <= ( s div 3600,
                  mod 3600 div 60,
                  s contra 3600 contra 60);
```
`div` é a função integrada de divisão de inteiros e `mod` fornece o restante após a divisão de inteiros. Se digitarmos uma aplicação `time24` no terminal, a tupla resultante e seu tipo serão impressos na tela da maneira usual:

```
hora24 (45756);
(12,42,36): (número # número # número)
```
O segundo tipo de dados padrão, chamado lista, corresponde aproximadamente a um array unidimensional em Pascal. Ele pode conter qualquer número de objetos (incluindo nenhum), mas todos devem ser do mesmo tipo. Podemos escrever expressões em nossos programas que representem listas, como:

```
[ 1, 2, 3 ]
```
que é do tipo `list (num)`. Existem duas funções padrão para definir listas. O operador infixo `::` (lido como `cons`) define uma lista em termos de um único objeto e uma lista contendo o mesmo tipo de objeto, então

```
10 :: [ 20, 30, 40 ]
```
define a lista:

```
[ 10, 20, 30, 40 ]
```
Não pense em `::` como adicionar 10 à frente de `[ 20, 30, 40 ]`. Na verdade, define uma nova lista `[ 10, 20, 30, 40 ]` em termos de dois outros objetos sem alterar seu significado, da mesma forma que `1 + 3` define um novo valor de `4` sem alterar o significado de `1` ou `3`.

A outra função de lista padrão é `nil`, que define uma lista sem elementos nela. Podemos representar cada lista por uma expressão que consiste em aplicações de `::` e `nil`. Quando escrevemos uma expressão como:

```
[uma + 1, b - 2, c * d]
```
é considerado uma forma abreviada de escrever:

```
a + 1 :: ( b - 2 :: ( c * d :: nulo ) )
```
Há também uma forma abreviada de escrever listas de personagens. As três expressões a seguir são todas equivalentes:

```
"gato"
[ 'g', 'a', 't', 'o' ]
'g' :: ( 'a' :: ( 't' :: ( 'o' :: nulo ) ) )
```
Quando o resultado de um programa Hope é uma lista, ele é sempre impresso em notação concisa entre colchetes; se for uma lista de caracteres, será impressa entre aspas.

Cada tipo de dados em Hope é definido por um conjunto de funções primitivas como `::` e `nil`. Elas são chamadas de funções construtoras e não são definidas por equações de recursão. Quando definimos uma tupla, na verdade estávamos usando um construtor padrão chamado `,` (leia-se como `vírgula`). Mais tarde veremos como os construtores são definidos para outros tipos de dados.