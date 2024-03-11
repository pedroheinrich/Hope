```markdown
# Padrões

## Identificador (identifier)
*(mas não um data-constant-identifier)* uma variável que corresponde a qualquer valor. Nenhuma variável pode ocorrer duas vezes no mesmo padrão. Cada ocorrência livre do identificador na expressão correspondente ao padrão é vinculada a esse padrão. Ou seja, o identificador é um identificador de valor na expressão, referente ao valor correspondido.

## Identificador de constante de dados (data-constant-identifier)
Corresponde à constante de dados nomeada.

## Padrão de identificador de construtor de dados (data-constructor-identifier pattern)
Corresponde a um valor formado pela aplicação do construtor de dados a um padrão de correspondência de valor.

## Literal numérico (numeric-literal)
`1`, `2`, ... são abreviações para `succ(0)`, `succ(succ(0))` etc.

## Padrão + literal numérico (pattern + numeric-literal
)
O formulário `pattern + k` é uma abreviatura de `succ` aplicado `k` vezes ao `pattern`.

## 'c'
Corresponde à constante do caractere.

## "string"
Abreviatura de uma lista de caracteres.

## [padrão_1, ..., padrão_n] ([ pattern_ 1, ..., pattern_ n])
Equivalente a `padrão_1 :: ... :: padrão_n :: nil`.

## []
Equivalente a `nil`.

## padrão_1, padrão_2  (pattern_ 1, pattern_ 2)
Corresponde a um par de valores correspondentes ao `padrão_1` e ao `padrão_2`, respectivamente.

## (padrão) (( pattern))
Igual ao `pattern`.
```