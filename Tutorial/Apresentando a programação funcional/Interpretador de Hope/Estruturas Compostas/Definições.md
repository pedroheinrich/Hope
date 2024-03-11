# Definições

- `uses module-identifier, ..., module-identifier;`  
Todas as definições visíveis nos módulos nomeados devem estar visíveis no módulo ou sessão atual. Os módulos são procurados primeiro no diretório atual e depois em um diretório de biblioteca. Os módulos utilizados poderão utilizar outros módulos, e assim por diante, desde que não haja ciclos. As definições visíveis no módulo em uso (ou sessão) não serão visíveis em um módulo usado, a menos que as definições residam em um terceiro módulo usado por ambos.

- `private;`  
Todas as definições subsequentes neste módulo serão ocultadas de outros módulos que o utilizam. Em particular, as definições visíveis num módulo utilizado após esta directiva não serão visíveis para nenhum módulo que utilize esta, ao passo que seriam se o módulo fosse utilizado antes da directiva.

- `infix identifier, ..., identifier : numeric-literal;`  
Declare operadores infixos associativos à esquerda com a precedência declarada, de 1 (mais fraco) a 9 (mais forte).

- `infixr identifier, ..., identifier : numeric-literal;`  
Como infix , exceto que os operadores são associativos à direita.

- `abstype identifier [( identifier_ 1, ..., identifier_ n) ];`  
Uma definição de tipo `abstrata', declarando o identificador como um tipo ou identificador de construtor de tipo, que pode ser usado em definições subsequentes. O identificador pode ser definido posteriormente por uma definição de dados ou tipo . Se houver apenas um argumento, os parênteses poderão ser omitidos.

- `data identifier [( identifier_ 1, ..., identifier_ n) ] ==
identifier_ 1' [ type_ 1 ] ++ ... ++ identifier_ k' [ type_ k ];` 
Defina o identificador como um tipo ou construtor de tipo, com o identificador _ k' como suas constantes de dados e construtores. Se houver apenas um argumento simples, os parênteses poderão ser omitidos. A definição pode ser recursiva. Qualquer uso do identificador no tipo _ i deve ter os mesmos parâmetros do lado esquerdo. Qualquer identificador de construtor pode ter sido declarado anteriormente em uma declaração dec , caso em que o novo tipo de identificador deve ser uma instância daquele fornecido na declaração anterior.

- `type identifier [( identifier_ 1, ..., identifier_ n) ] == type;`  
Defina o identificador como uma abreviatura para o tipo , que pode se referir aos identificadores de tipo de argumento. Se houver apenas um argumento simples, os parênteses poderão ser omitidos. A definição pode ser recursiva. Qualquer uso do identificador no tipo deve ter os mesmos parâmetros do lado esquerdo. Consulte Tipos regulares para obter mais detalhes.

- `typevar identifier, ..., identifier;`  
Declare novas variáveis ​​de tipo, para uso em declarações dec . Se o identificador for declarado, então o identificador ' , o identificador '' e assim por diante também poderão ser usados ​​como variáveis ​​de tipo (aspas simples no próprio identificador são ignoradas).

- `dec identifier, ..., identifier : type;`  
Declare os identificadores como identificadores de valor de um determinado tipo, em que variáveis ​​de tipo declaradas por definições de typevar representam qualquer tipo. Se apenas um identificador estiver sendo declarado, a palavra-chave dec é opcional.

- `-- value-identifier pattern_ 1 ... pattern_ n <= expression;`  
Definir o valor de um identificador. Se n for zero, apenas uma definição desse tipo será permitida para cada identificador. Caso contrário, o identificador pode ser definido por uma ou mais dessas definições, cada uma com o mesmo número de argumentos. Consulte Semântica da correspondência de padrões . 

A palavra-chave -- é opcional.