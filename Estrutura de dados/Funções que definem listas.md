# Funções que definem listas

Se quiséssemos escrever um programa Pascal para imprimir os primeiros n números naturais em ordem decrescente, provavelmente escreveríamos um loop que imprimisse um valor em cada iteração, como:

```pascal
para i := n até 1 escreva ( i );
```
Em Hope escrevemos uma expressão que define todos os valores de uma vez, como fizemos para `mult`:

```hope
dec nats: num -> lista (num);
--- nats(n) <= se n = 0 então nil else n :: nats(n-1);
```
`nil` é útil para escrever o caso base de uma função recursiva que define uma lista. Se tentarmos a função no terminal digitando:

```hope
limpos (10);
[10,9,8,7,6,5,4,3,2,1]: lista (num)
```
podemos ver que os números estão em ordem decrescente porque foi assim que os organizamos na lista, e não porque foram definidos nessa ordem. Os valores na expressão que define a lista são tratados como se tivessem sido gerados todos ao mesmo tempo. Na máquina ALICE eles são gerados ao mesmo tempo.

Para obter os resultados de um programa Hope na ordem correta, devemos colocá-los no lugar certo na estrutura de dados final. Se quisermos a lista dos números de n a 1 na ordem oposta, não podemos escrever a definição como:

```hope
... senão nats(n-1)::n;
```
porque os tipos de argumento para `::` estão ao contrário. Precisamos usar outra operação interna `<>` (lida como `append`) que concatena duas listas. A definição ficará assim:

```hope
--- nats ( n ) <= se n = 0 então nil else nats ( n-1 ) <> [ n ] ;
```
Colocamos `n` entre colchetes para transformá-lo em uma lista (de item único) porque `<>` espera que ambos os seus argumentos sejam listas. Também poderíamos ter escrito `( n :: nil )` em vez de `[ n ]`.