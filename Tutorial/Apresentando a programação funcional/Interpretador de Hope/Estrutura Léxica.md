Estrutura lexical
A entrada é dividida em uma sequência de símbolos dos seguintes tipos:

um caractere de pontuação: um de `` ( ) , ; [ ] '',
um identificador: qualquer
1.
uma letra ou sublinhado seguido de zero ou mais letras, sublinhados ou dígitos (seguido de zero ou mais aspas simples), ou
2.
uma sequência de caracteres gráficos que não são espaços em branco, letras, sublinhados, dígitos, pontuação nem `` ! "' ',
um literal numérico: uma sequência de dígitos (em alguns sistemas, opcionalmente com um ponto decimal incorporado e um expoente opcionalmente assinado),
um caractere literal: um único caractere (mas não uma nova linha) ou uma sequência de escape de caracteres (como na linguagem C), entre aspas simples, ou
uma string literal: uma sequência de zero ou mais caracteres (mas não novas linhas de aspas duplas) ou sequências de escape de caracteres, entre aspas duplas.
Os símbolos podem ser separados por espaços em branco e comentários. Um comentário é introduzido por ` ! ' e continua até o final da linha.

Os seguintes identificadores são reservados pelo idioma:

      ++ --- : <= == => |
      abstype data dec display else edit exit se estiver
      infix infixr lambda deixe letrec private salvar então
      tipo typevar usa onde whererec escreve
Os seguintes identificadores também são reservados, para compatibilidade com outras implementações:
      módulo final nãoop pubconst pubfun pubtype
Além disso, os seguintes sinônimos estão disponíveis: \para lambda , use para usos e infixrl para infixr .