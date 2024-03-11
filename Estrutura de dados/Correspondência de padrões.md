# Correspondência de padrões

Uma expressão composta por construtores que aparecem no lado esquerdo de uma equação de recursão é chamada de padrão. Selecionar a equação de recursão correta e desmontar o parâmetro real para nomear suas partes é chamado de correspondência de padrões. Ao escrever uma função, você deve fornecer uma equação de recursão para cada construtor possível que defina o tipo de argumento.

Às vezes não precisamos desmontar o parâmetro real e podemos usar um parâmetro formal no padrão que corresponda a todo o objeto, independentemente de quais construtores foram usados ​​para defini-lo. Como exemplo, vamos ver como poderíamos definir nossa própria função para concatenar duas listas como a operação integrada `<>`:

```hope
infix cat: 4;
dec cat: lista(num) # list(num) -> list(num);
--- (h :: t ) cat l <= h :: (t cat l ) ;
--- nulo cat l <= l ;
```
O primeiro parâmetro da lista é correspondido pelo padrão `( h :: t )` para que seu primeiro item (a `cabeça') e o restante da lista (a `cauda') possam ser referidos separadamente no lado direito. A segunda equação de recursão cobre o caso em que a primeira lista está vazia. O segundo parâmetro da lista corresponde ao padrão `l`, esteja vazio ou não.

Além de escrever equações de recursão suficientes para satisfazer todos os construtores de parâmetros, também devemos ter cuidado para não escrever conjuntos de equações onde mais de um padrão possa corresponder aos parâmetros reais, porque isso seria ambíguo.

Podemos escrever padrões para corresponder a argumentos que são tuplas da mesma maneira, usando o construtor de tupla `,`. Quando escrevemos `mult ( x, y )` você provavelmente pensou que os parênteses e a vírgula tinham algo a ver com a aplicação da função. Na verdade, estávamos construindo uma tupla e os parênteses só eram necessários porque `,` tem baixa prioridade. Hope trata todas as funções como tendo apenas um argumento. Pode ser uma tupla quando você deseja o efeito de vários argumentos. Sem parênteses,

```hope
múltiplo x, y
```
seria interpretado como:
```hope
(múltiplo (x), y)
```
Uma equação de recursão com o lado esquerdo:
```hope
--- mult(x,y) <= ...
```
é apenas uma correspondência de padrões em uma tupla. O primeiro item da tupla é denominado `x` e o segundo `y`.

Também podemos usar correspondência de padrões em parâmetros `num`. Eles são definidos por dois construtores chamados `succ` e `0`. `succ` define um número em termos do próximo número inferior. `0` não tem argumentos e define o valor zero. Certamente `0` é um valor, não uma função? Bem, já estamos acostumados a pensar em aplicações de funções como outra forma de escrever valores, então é bastante consistente pensar em `0` como uma aplicação de funções. Aqui está uma versão do `mult` que usa correspondência de padrões para identificar o caso base:

```hope
infix mult: 8;
dec mult: num # num -> num;
--- x mult 0 <= 0 ;
--- x mult succ ( y ) <= ( x mult y ) + x ;
```
Podemos ler `succ ( y )` como `o sucessor de algum número que chamaremos de y`. Em vez de nomear o parâmetro real `y` como fizemos na versão original de `mult`, estamos nomeando seu antecessor.