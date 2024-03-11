# Simplificando expressões

Nos programas Pascal podemos simplificar expressões complexas removendo subexpressões comuns e avaliando-as separadamente. Em vez de:

```pascal
writeln((x+y)*(x+y));
```
provavelmente escreveríamos:
```pascal
z := x + y ; writeln(z*z);
```
que é mais claro e eficiente. Os programas Hope consistem apenas em expressões e é ainda mais importante simplificá-los. Fazemos isso usando uma expressão qualificada:
```hope
let z == x + y in z * z ;
```
Parece uma tarefa, mas não é. `==` é lido como `é definido como` e `z` é local para a expressão após `in`. Se escrevermos algo como:
```hope
let z == z + 1 in z * z ;
```
na verdade, estamos introduzindo uma nova variável `z` para usar na subexpressão `z * z`. Oculta o original na subexpressão `z + 1`.

Existe uma segunda forma de expressão qualificada para pessoas que gostam de usar variáveis ​​primeiro e definir seus significados depois. Se parece com isso:

```hope
z * z where z == x + y ;
```
O resultado da expressão qualificada é o mesmo, quer a definamos usando `let` ou `where`. `x + y` é avaliado primeiro e seu valor é usado na expressão principal.

A expressão de qualificação geralmente será um aplicativo de função que define uma estrutura de dados. Se quisermos nomear parte da estrutura, podemos usar um padrão no lado esquerdo do símbolo `==`:

```hope
dec hora12: num -> num # num;
--- hora12 ( s ) <= ( if h > 12 then h-12 else h, m ) where
                    (h, m, s) == hora12 (s);
```
Usaremos essa construção com mais frequência quando escrevermos funções recursivas que definem tuplas. Aqui está um exemplo típico. Suponha que queiramos formar uma sequência de palavras a partir de uma frase. Para simplificar, uma palavra é considerada qualquer sequência de caracteres e as palavras são separadas na frase por qualquer número de espaços em branco. A sentença e uma única palavra serão do tipo `list (char)` e a seqüência final de palavras uma `list (list(char))`.

É bastante simples obter a primeira palavra. Aqui está uma função que faz isso:

```hope
dec primeira-tentativa: list (char) -> list (char);
---primeira-tentativa (nil) <= nil;
---primeira-tentativa ( c :: s ) <= if c = ' '
                             then nil
                             else c :: primeira-tentativa ( s );
```
Um dos recursos interessantes do Hope é que podemos digitar e imprimir qualquer tipo de valor, por isso é fácil verificar as funções individuais do nosso programa separadamente. Se testarmos primeiro, veremos:
```hope
primeira-tentativa("Você pode caçá-lo com foices e esperança");
"Você": list (char)
```
Mas há um problema aqui porque precisaremos do resto da frase se quisermos encontrar as palavras restantes. Devemos fazer com que a função retorne a lista restante, bem como a primeira palavra. É aqui que entram as tuplas:
```hope
dec primeira-palavra: list (char) -> list (char) # list (char);
---primeira-palavra (nil) <= (nil, nil);
---primeira-palavra ( c :: s ) <= if c = ' '
                              then (nil, s)
                              else (( c :: w, r ) where
                                     ( w, r ) == primeira-palavra ( s ) ) ;
```
A expressão qualificada está entre parênteses, portanto só se aplica à expressão após o `else`; caso contrário, avaliaremos a primeira palavra recursivamente, desde que a frase não esteja vazia, mesmo que comece com um espaço em branco. Esta versão da função produz:
```hope
primeira-palavra("A esperança é eterna...");
( "Esperança","primavera eterna..." ) : ( list ( char ) # list ( char ) )
```
Podemos usar isso para definir uma função para dividir a frase em uma lista de suas palavras individuais:
```hope
lista de palavras dec: list (char) -> list (list (char));
--- lista-de-palavras (nil) <= nil;
--- lista-de-palavras ( c :: s ) <= if c = ' '
                             then lista-de-palavras(s)
                             else ( w :: lista-de-palavras ( r ) where
                                  ( w, r ) == primeira-palavra ( c :: s ) ) ;
```
que podemos testar digitando uma aplicação no terminal:
```hope
lista-de-palavras (“Enquanto há vida há Esperança”);
["Enquanto","há","vida","há","Esperança"]: list (lisa (char))
```