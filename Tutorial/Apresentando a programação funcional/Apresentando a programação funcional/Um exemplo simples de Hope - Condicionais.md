```markdown
# Um exemplo simples de Hope - condicionais

Vamos ver como podemos definir `max` em Hope. Assim como Pascal, é uma linguagem fortemente tipada, o que significa que devemos informar ao compilador sobre os tipos de todos os objetos em nossos programas para que ele possa verificar se eles são usados ​​de forma consistente. A definição da função vem em duas partes. Primeiro declaramos os tipos de argumento e resultado:

```hope
dec max: num # num -> num;
```

`dec` é uma palavra reservada: você não pode usá-la como nome. `max` é o nome da função que está sendo definida. Os nomes consistem em letras maiúsculas e minúsculas (que são distintas) e dígitos e devem começar com uma letra. A moda atual é usar letras minúsculas. O layout não é significativo e você pode separar os símbolos com qualquer número de espaços em branco, tabulações e novas linhas para maior clareza, como neste exemplo. Os símbolos só precisam ser separados quando, de outra forma, poderiam ser confundidos como um só, como `dec` e `max`.

A próxima parte da declaração fornece os tipos de argumentos (leia o símbolo `:` como `leva a`). Inteiros não negativos são do tipo predefinido `num` (em letras minúsculas). `#` é lido como `e a`; (ou você pode usar a palavra reservada `X`). `->` é lido como `rendimento`. O ponto e vírgula marca o final da declaração, o que informa ao compilador que `max` recebe dois números como argumentos e retorna um único número como resultado.

O resultado de uma função é definido por uma ou mais equações de recursão. `max` precisa apenas de uma equação para defini-lo:

```hope
--- max ( x, y ) <= se x > y então x senão y ;
```

Leia o símbolo `–` como “o valor de”. A expressão `max ( x, y )` é chamada de lado esquerdo da equação. Ele define `x` e `y` como parâmetros formais, ou nomes locais para os valores que serão fornecidos quando a função for aplicada. Os nomes dos parâmetros são locais na equação, portanto `x` e `y` não serão confundidos com nenhum outro `x` ou `y` no programa. O símbolo `<=` é lido como `é definido como`.

O resto da equação (chamado de lado direito) define o resultado. É uma expressão condicional. Os símbolos `if`, `then` e `else` são palavras reservadas. A declaração condicional de Pascal escolhe entre ações alternativas, mas a expressão condicional de Hope escolhe entre valores alternativos, em linha com a nossa visão de que as aplicações de funções são formas de escrever valores e não receitas para calculá-los. Se o valor da expressão `x > y` for `true`, o valor de toda a expressão condicional será o valor de `x`, caso contrário, será o valor de `y`. Os valores alternativos podem ser definidos por quaisquer expressões Hope.

Quando o valor de uma função é definido por mais de uma expressão como esta, elas são avaliadas em uma ordem não especificada. Em um computador adequado, como a máquina ALICE do Imperial College, é possível até avaliar as duas expressões e o teste em paralelo e descartar um dos valores de acordo com o resultado do teste.
```