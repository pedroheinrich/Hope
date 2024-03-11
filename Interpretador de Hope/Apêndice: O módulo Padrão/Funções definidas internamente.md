
# :computer: Funções definidas internamente :computer:

**Funções de comparação**: Avaliam seus argumentos apenas na medida necessária para determinar sua ordem. Ao comparar constantes e construtores distintos, o menor é aquele que veio anteriormente na definição dos dados em que ambos foram definidos. Os pares são comparados lexicograficamente, enquanto a comparação de funções desencadeia um erro em tempo de execução. Nos tipos num, char e list(char), essas regras fornecem as ordenações normais.
```hope
    infix =, /= : 3;
    infix <, =<, >, >= : 4;
    dec =, /=, <, =<, >, >= : alpha # alpha -> bool;
```
**Funções de comparação de nível inferior**
```hope
    data relation == LESS ++ EQUAL ++ GREATER;

    dec compare : alpha # alpha -> relation;

    --- x =  y <= (\ EQUAL => true | _ => false) (compare(x, y));
    --- x /= y <= (\ EQUAL => false | _ => true) (compare(x, y));
    --- x <  y <= (\ LESS => true | _ => false) (compare(x, y));
    --- x >= y <= (\ LESS => false | _ => true) (compare(x, y));
    --- x >  y <= (\ GREATER => true | _ => false) (compare(x, y));
    --- x =< y <= (\ GREATER => false | _ => true) (compare(x, y));
```
**Conversões**
```hope
    dec ord : char -> num;
    dec chr : num -> char;

    dec num2str : num -> list char;
    dec str2num : list char -> num;
```
**O conteúdo de um arquivo nomeado (criado lentamente)**
```hope
    dec read : list char -> list char;
```
**Abortar a execução com uma mensagem de erro**
```hope
    dec error : list char -> alpha;
```
**As funções aritméticas usuais**
```hope
    infix +, - : 5;
    infix *, /, div, mod : 6;
    dec +, -, *, /, div, mod : num # num -> num;
```
**Biblioteca matemática**
```hope
    dec cos, sin, tan, acos, asin, atan : num -> num;
    dec atan2, hypot : num # num -> num;
    dec cosh, sinh, tanh, acosh, asinh, atanh : num -> num;
    dec abs, ceil, floor : num -> num;
    dec exp, log, log10, sqrt : num -> num;
    dec pow : num # num -> num;
    dec erf, erfc : num -> num;
```
**Quaisquer argumentos extras na linha de comando do interpretador**
```hope
    dec argv : list(list char);
```
**Parte do tratamento especial do construtor succ**
```hope
    dec succ : num -> num;
    --- succ n <= n+1;
```
