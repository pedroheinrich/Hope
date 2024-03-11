
# :computer: Construtores de tipo padrão :computer:

**Variáveis ​​de tipo padrão**
```hope
typevar alpha, beta, gamma;
```
**Função e tipos de produtos**
```hope
    infixr -> : 2;
    abstype neg -> pos;

    infixr # : 4;
    abstype pos # pos;

    --- (a # b) (x, y) <= (a x, b y);

    infixr X : 4;
    type alpha X beta == alpha # beta;
```
**Composição normal da direita para a esquerda de f e g**
```hope
    infix o : 2;
    dec o : (beta -> gamma) # (alpha -> beta) -> alpha -> gamma;
    --- (f o g) x <= f(g x);

    --- (a -> b) f <= b o f o a;
```
**A função identidade**
```hope
    dec id : alpha -> alpha;
    --- id x <= x;
```
**Booleanos com as operações padrão**
```hope
    data bool == false ++ true;
    type truval == bool;

    infix or : 1;
    infix and : 2;

    dec not : bool -> bool;
    --- not true <= false;
    --- not false <= true;

    dec and : bool # bool -> bool;
    --- false and p <= false;
    --- true and p <= p;

    dec or : bool # bool -> bool;
    --- true or p <= true;
    --- false or p <= p;

    dec if_then_else : bool -> alpha -> alpha -> alpha;
    --- if true then x else y <= x;
    --- if false then x else y <= y;
```
**Listas**
```hope
    infixr :: : 5;
    data list alpha == nil ++ alpha :: list alpha;
```
**Concatenação de lista**
```hope
    infixr <> : 5;
    dec <> : list alpha # list alpha -> list alpha;
    --- [] <> ys <= ys;
    --- (x::xs) <> ys <= x::(xs <> ys);
```
**O tipo num se comporta como se fosse definido por: "!"**
```hope
!        data num == 0 ++ succ num;
```
mas na verdade é implementado com um pouco mais de eficiência. O tipo também contém números negativos (e reais em algumas implementações).
```hope
data num == succ num;
```
Da mesma forma, o tipo char se comporta como se fosse definido como uma enumeração (na ordem normal) de todas as constantes de caracteres ASCII.
```hope
    abstype char;

    --- char x <= x;
```
