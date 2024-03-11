# Semântica de Correspondência de Padrões

O seguinte é uma especificação parcial; nada mais é garantido. Informalmente, quando os padrões se sobrepõem, os padrões mais específicos são preferidos aos mais específicos. Além disso, a escolha não é especificada. Mais formalmente:

Combinar um valor com um padrão envolve avaliar o valor o suficiente para comparar suas constantes de dados e construtores com aqueles no padrão, em alguma ordem consistente, de cima para baixo (mas de outra forma não especificada). Esta correspondência pode resultar em:

- **success**: O valor pode ser visto como uma instância do padrão.
- **failure**: O valor não pode ser uma instância do padrão, porque possui uma constante de dados ou construtor diferente em alguma posição.
- **non-termination**: O valor não pode ser suficientemente avaliado para decidir entre os itens acima, na ordem específica de verificação utilizada.

Se a correspondência for bem-sucedida, ela fornecerá valores para as variáveis ​​do padrão. Um padrão (ou subpadrão) que consiste apenas em variáveis ​​e pares sempre corresponde a um valor do tipo apropriado, mesmo que o cálculo do valor não termine. Tais padrões são chamados de **irrefutable**.

Agora suponha que uma função tenha sido definida por uma série de definições:

```hope
f p_1 e1 ... p_m em <= e_i;
```

Para `i = 1, ..., k`, ou é a expressão:

```hope
lambda p_11 ... p_1n => e_1 | ... | p_k1 ... p_kn => e_k
```

Atualmente, as funções anônimas devem ser unárias. Uma aplicação desta função a `n` valores de argumentos terá zero ou mais valores possíveis, como segue:

- Se alguns padrões `p_ij` corresponderem com sucesso aos argumentos correspondentes para algum `i`, e todos os padrões mais específicos (se houver) falharem, então um valor possível é o valor de `e_i`, com as variáveis ​​de `p_ij` assumindo os valores com os quais corresponderam.
- Se a correspondência de algum padrão não terminar, sob alguma ordem de verificação, então a não terminação é um valor possível.
- Se não houver valores possíveis, o valor do aplicativo será um erro em tempo de execução. Caso contrário, um dos valores possíveis é escolhido, de forma determinística (mas não especificada).