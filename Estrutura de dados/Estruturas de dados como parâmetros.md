# Estruturas de dados como parâmetros

Suponha que temos uma lista de inteiros e queremos escrever uma função para somar todos os seus elementos. A declaração ficará assim:

```hope
dec somalista: list(num) -> num;
```
Precisamos nos referir aos elementos individuais do parâmetro real nas equações que definem `somalista`. Fazemos isso usando uma equação cujo lado esquerdo se parece com isto:

```hope
---somalista ( x :: y ) ...
```
Esta é uma expressão que envolve construtores de lista e corresponde a um parâmetro real que é uma lista. `x` e `y` são parâmetros formais, mas agora nomeiam partes individuais do valor real do parâmetro. Em uma aplicação de `somalista` como:

```hope
somalista ([ 1, 2, 3 ] )
```
o parâmetro real será `desmontado` para que `x` nomeie o valor 1 e `y` nomeie o valor [ 2, 3 ]. A equação completa será:

```hope
---somalista( x :: y ) <= x + somalista ( y ) ;
```
Observe que não há teste de caso base. Como seria de esperar, é a lista vazia, mas não podemos testá-la diretamente na equação porque não há nenhum parâmetro formal que se refira à lista inteira. Na verdade, se escrevermos o aplicativo:

```hope
somalista (nil)
```
receberemos uma mensagem de erro porque não podemos desmontar `nil` para encontrar os valores de `x` e `y`. Devemos cobrir este caso separadamente usando uma segunda equação de recursão:

```hope
---somalista (nil) <= 0;
```
As duas equações podem ser dadas em qualquer ordem. Quando `somalista` é aplicado, o parâmetro real é examinado para ver qual função construtora foi usada para defini-lo. Se o parâmetro real for uma lista não vazia, a primeira equação será usada, porque as listas não vazias são definidas usando o construtor `::`. O primeiro número da lista é denominado `x` e a lista restante `y`. Se o parâmetro real for a lista vazia, a segunda equação será usada porque as listas vazias são definidas usando o construtor `nil`.