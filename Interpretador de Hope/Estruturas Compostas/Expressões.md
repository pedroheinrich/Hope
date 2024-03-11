
# Expressões

- **Identificador de valor**: (value-identifier) o valor vinculado ao identificador.
- **Identificador de constante de dados**: (data-constant-identifier) uma constante de dados.
- **Identificador do construtor de dados**: (data-constructor-identifier) um construtor de dados.
- **Literal numérico**: (numeric-literal) `1`, `2`, ... são abreviações para `succ(0)`, `succ(succ(0))` etc.
- **'c'**: constante de caractere.
- **"string"**: abreviatura de uma lista de caracteres.
- **[expression_1, ..., expression_n]**: ([ expression_ 1, ..., expression_ n]) equivalente a `expression_1 :: ... :: expression_n :: nil`.
- **[]**: equivalente a `nil`.
- **expression_1, expression_2**: (expression_ 1, expression_ 2) um par formado a partir dos valores de `expression_1` e `expression_2`.
- **(expression)**: (_expression) o mesmo que `expression`.
- **expression_1 expression_2**: (expression_ 1 expression_ 2) o resultado da aplicação do valor da função ou do construtor de `expression_1` ao valor de `expression_2`.
- **pattern lambda_1 => expression_1 | ... | pattern_k => expression_k**: (lambda pattern_ 1 => expression_ 1 | ... | pattern_ k => expression_ k) uma função anônima. Consulte Semântica da correspondência de padrões.
- **se expression_1 então expression_2 senão expression_3**: uma expression condicional, igual a `expression_2` se `expression_1` for `true` ou `expression_3` se for `false`.
- **if expression_ 1 then expression_ 2 else expression_ 3**: o mesmo que `expression_ 2`, com as variáveis ​​em `expression_ 2` substituídas pelos valores atribuídos a elas no pattern correspondente à `expression_ 1`. É equivalente a `(lambda pattern => expression_2) expression_1`.
- **let pattern == expression_ 1 in expression_ 2**: como `let`, exceto que o pattern deve ser irrefutável e suas variáveis ​​também podem aparecer na `expresssion_1`. É uma versão mais eficiente do `(lambda pattern => expression_ 2)(corrigir(lambda pattern => expression_1))` para uma correção de função definida como `correção de dec: (alfa -> alfa) -> alfa; --- consertar f <= f(corrigir f);`.
- **expression_1 onde pattern == expression_2**: o mesmo que `let pattern == expression_2 na expression_1`.
- **expression_1 pattern whererec== expression_2**: igual a `pattern letrec == expression_2 na expression_1`.

As ambigüidades em padrões e expressões são resolvidas pelas seguintes precedências vinculativas, da mais fraca à mais forte:
- vírgula (associativo direito)
- lambda
- let e letrec
- where e whererec
- if
- operadores infix de precedência 1 a 9
- aplicação de função (associativa esquerda)

Para quaisquer operadores infix `@` e expressão `e`, são permitidas as seguintes abreviações, chamadas de seções de operadores:
- `(e @)`: é a abreviação de `lambda x => e @ x`.
- `(@ e)`: é a abreviação de `lambda x => x @ e`.
