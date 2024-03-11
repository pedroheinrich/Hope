# Identificadores

Os identificadores podem referir-se a:

- Módulos
- Tipos
- Construtores de tipo
- Constantes de dados
- Construtores de dados
- Valores

O mesmo identificador pode referir-se a mais de um desses tipos, mas em qualquer escopo não pode referir-se a mais de uma das três últimas classes.

Identificadores podem ser definidos como operadores infix, por definições `infix` e `infixr`. Isso afeta apenas a maneira como eles são analisados e impressos: se um identificador `@` for declarado como um operador infixo, construções na forma `@(a, b)` serão escritas `a @ b`. Para se referir a `@` sozinho, use `(@)`. Um caso especial: em qualquer declaração subsequente de `@` como construtor de dados, `@(type_1 # type_2)` é escrito `type_1 @ type_2`.

Vários identificadores são predefinidos no módulo `Standard`.
