# Funtores :rocket:

Cada definição de dado ou tipo introduz uma nova função `map` (ou functor, para teóricos de categorias) com o mesmo nome e aridade do construtor de tipo. 

Por exemplo, a definição de tipo
```hope
    data tree alpha == Empty ++ Node (tree alpha) alpha (tree alpha);
```
também define uma função
```hope
    tree : (alpha -> beta) -> tree alpha -> tree beta
```
que mapeia uma função sobre árvores. Esta definição automática pode ser explicitamente substituída.

É um pouco mais complicado: se o argumento de tipo for usado negativamente, como em
```hope
    type cond alpha == alpha -> bool;
```
a função terá um tipo invertido:
```hope
    cond : (alpha -> beta) -> tree beta -> tree alpha
```
Se o argumento for usado tanto positiva quanto negativamente, como em
```hope
    type endo alpha == alpha -> alpha;
```
a função terá um tipo como
```hope
    endo : (alpha -> alpha) -> tree alpha -> tree alpha
```
Da mesma forma, uma definição de abstype declara esta função correspondente. Para determinar o tipo, presume-se que cada argumento seja usado tanto positiva quanto negativamente, a menos que a variável do argumento seja substituída por uma das palavras-chave especiais `pos`, `neg` ou `none` (indicando que o argumento não é usado). Veja o apêndice anterior para alguns exemplos. :nerd_face: