```markdown
# Expressões Booleanas Simbólicas em Hope 🎉

Primeiro, definimos um tipo de variável simples:

```hope
var == char;
```

Representamos expressões booleanas por árvores:

```hope
    infixrl IMPLIES: 1;
     infix   OR: 2;
     infix   AND: 3;

    data bexp ==    VAR var ++ bexp AND bexp ++ bexp OR bexp ++
                     NOT bexp ++ bexp IMPLIES bexp;
```

Definimos uma atribuição como uma lista atribuindo valores booleanos às variáveis:

```hope
assignment == list(var # truval);
```

Agora, definimos uma função para avaliar uma expressão booleana em relação a uma atribuição de valores booleanos às variáveis ​​que ela contém:

```hope
    dec lookup : alpha # list(alpha#beta) -> beta;
     --- lookup(a, (key, datum)::rest) <=
             if a = key then datum else lookup(a, rest);

    dec evaluate : bexp # assignment -> truval;
     --- evaluate(VAR v, a) <= lookup(v, a);
     --- evaluate(e1 AND e2, a) <= evaluate(e1, a) and evaluate(e2, a);
     --- evaluate(e1 OR e2, a) <= evaluate(e1, a) or evaluate(e2, a);
     --- evaluate(NOT e, a) <= not(evaluate(e, a));
     --- evaluate(e1 IMPLIES e2, a) <=
             not(evaluate(e1, a)) or evaluate(e2, a);
```

Vamos testar a função `avaliar` com algumas expressões booleanas:

```hope
    evaluate (VAR 'a' AND VAR 'b' OR VAR 'c',
               [('a', false), ('b', true), ('c', false)]);
    evaluate (VAR 'a' AND VAR 'b' OR VAR 'c',
               [('a', true), ('b', true), ('c', false)]);
```

Pretendemos usar esta função em uma função para testar se alguma expressão booleana é uma tautologia, ou seja, é verdadeira para qualquer atribuição de suas variáveis. Primeiro, precisamos de uma função para extrair a lista de variáveis ​​de uma expressão. A função a seguir mescla duas listas ordenadas para formar uma lista ordenada sem duplicatas:

```hope
    dec merge : list alpha # list alpha -> list alpha;
     --- merge([], l) <= l;
     --- merge(l, []) <= l;
     --- merge(x1::l1, x2::l2) <=
             if x1 = x2 then x1::merge(l1, l2)
             else if x1 < x2 then x1::merge(l1, x2::l2)
                             else x2::merge(x1::l1, l2);
```

A próxima função retorna a lista ordenada de variáveis ​​em uma expressão booleana, sem duplicatas:

```hope
dec vars : bexp -> list var;
     --- vars(VAR v) <= [v];
     --- vars(e1 AND e2) <= merge(vars e1, vars e2);
     --- vars(e1 OR e2) <= merge(vars e1, vars e2);
     --- vars(NOT e) <= vars e;
     --- vars(e1 IMPLIES e2) <= merge(vars e1, vars e2);
```

Vamos testar a função `vars` com algumas expressões booleanas:

```hope
    vars (VAR 'a' AND VAR 'b' OR VAR 'a');
    vars ((VAR 'a' IMPLIES VAR 'b' IMPLIES VAR 'c') IMPLIES
             (VAR 'a' IMPLIES VAR 'b') IMPLIES
             VAR 'a' IMPLIES VAR 'c');
```

Agora queremos gerar a lista de todas as atribuições possíveis para uma lista de variáveis:

```hope
uses list;

     dec interpretations: list var -> list assignment;
     --- interpretations [] <= [[]];
     --- interpretations(h::t) <=
             (map ((h, false)::) l <> map ((h, true)::) l)
             where l == interpretations t;;
```

Vamos testar a função `interpretações` com algumas listas de variáveis:

```hope
    interpretations "a";
    interpretations "ab";
    interpretations "abc";

```

Finalmente, juntamos tudo isso. Uma expressão é uma tautologia se for avaliada como verdadeira para todas as atribuições possíveis às variáveis ​​que contém:

```hope
    dec tautology: bexp -> truval;
     --- tautology e <=
             foldr(true, (and))
                     (map evaluate
                             (dist(e, interpretations(vars(e)))));
```

Vamos testar a função `tautologia` com algumas expressões booleanas:

```hope
    tautology (VAR 'a' AND VAR 'b' OR VAR 'a');
    tautology ((VAR 'a' IMPLIES VAR 'b' IMPLIES VAR 'c') IMPLIES
                     (VAR 'a' IMPLIES VAR 'b') IMPLIES
                     VAR 'a' IMPLIES VAR 'c');
```