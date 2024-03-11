# Comandos Interativos

Em uma sessão HOPE, qualquer definição pode ser inserida (embora `private` seja ignorada), bem como os seguintes comandos:

## 1. `expression;`
Exibir o valor e o tipo mais geral de `expressão`. A avaliação lenta é usada, mas nada é exibido até que o valor seja totalmente avaliado. A expressão pode envolver a variável especial `input`, que denota a lista de caracteres digitados no terminal.

```hope
expression;
```

## 2. `escrever expressão [para "arquivo"];`
Imprima o valor da `expression;` (que deve ser uma lista de valores) de forma mais direta: se o valor for uma lista de caracteres, os caracteres serão impressos; caso contrário, cada valor será impresso sozinho em uma linha. Cada elemento da lista é impresso assim que seu valor é calculado (por avaliação lenta). Se a cláusula `to` estiver presente, a saída será gravada no arquivo; caso contrário, será impresso na tela. É seguro gravar em um arquivo que é lido pela expressão – nenhuma interferência ocorrerá. A expressão pode envolver a variável especial `input`, que denota a lista de caracteres digitados no terminal.

```hope
write expression  [to " file" ];
```

## 3. `display;`
Exibir as definições da sessão atual.

```hope
display;
```

## 4. `save module-identifier;`
Salve as definições da sessão atual em um novo módulo com o nome fornecido. As definições são substituídas na sessão atual por uma referência ao novo módulo.

```hope
save "modulo";
```

## 5. `edit [ module-identifier ];`
(Somente Unix) Invoque o editor padrão no módulo nomeado, se fornecido, ou de outra forma em um arquivo contendo as definições atuais e, em seguida, insira novamente o interpretador com as definições revisadas.

```hope
edit "modulo";
```

## 6. `exit;`
Sair do intérprete.

```hope
exit;
```
