# Expressões regulares
Em ciência da computação, uma expressão regular ou "Regex" provê uma forma concisa e flexível de identificar cadeias de caracteres de interesse, como caracteres particulares, palavras ou padrões de caracteres. 
Expressões regulares são escritas numa linguagem formal que pode ser interpretada por um processador de expressão regular, um programa que serve um gerador de analisador sintático ou examina o texto e identifica as partes que casam com a especificação dada. Fonte: https://pt.wikipedia.org/wiki/Express%C3%A3o_regular

De forma bem resumida, é uma forma de especificar um padrão de texto.

## Fonte
Grande parte do conteúdo apresentado tem como base o livro **Expressões Regulares - Uma abordagem divertida**, recomendo a compra para apreciar esta obra maravilhosa.

![Livro Expressões Regulares - Uma abordagem divertida](https://www.piazinho.com.br/ed5/capa-292.jpg)

site: https://www.piazinho.com.br/

## Teste
Todos os exemplos apresentados podem ser testados no site https://www.regexpal.com/

## Aplicações
Na pratica, as expressões regulares servem para uma infinidade de tarefas, elas são uteis sempre que você precisa buscar ou validar um padrão de texto, podem ser utilizadas, por exemplo, para os seguintes itens:

- Data e/ou hora nos mais diversos formatos
- Número IP
- Nome em geral
- Endereços de e-mail
- Endereços da web
- Conteúdos entre tags
- Número de documentos (CPF/RG)
- Entre outras infinitas possibilidades

## Linguagens de programação
Uma grande variedade de linguagens de programação tem suporte a expressões regulares, algumas de forma nativa, outras através de pacotes de terceiros. 

É importante ressaltar que podem existir pequenas variações entre as linguagens, a grande maioria dos itens apresentado neste documento são suportados em todas as linguagens abaixo, porém, é sempre importante consultar a documentação para garantir um bom funcionamento.

- C# (dotnet core / full framework)
- JavaScript / TypeScript
- Java
- Python
- Ruby
- Go
- C / C++
- Entre outras

## Metacaracteres
Os metacaracteres possuem funções especificas que podem variar de acordo com o contexto no qual estão inseridos, permitindo serem combinados para aumentar o poder de cada um deles.

|Metacaractere|Nome|Função|Exemplo de uso|
|-|-|-|-|
|.|Ponto|Casa com qualquer caractere|.|
|[ ]|Lista|Casa um conjunto de caracteres|[abc]|
|[^]|Lista negada|Casa todos os caracteres que não estiverem presentes na lista|[^abc]|
|?|Opcional|Torna opcional a existência da entidade anterior, devendo ocorrer zero ou uma vez|Casas?|
|\*|Asterisco|A entidade anterior pode ocorrer em qualquer quantidade, zero ou mais vezes|oii\*|
|+|Mais|A entidade anterior deve ocorrer uma ou mais vezes|oi+|
|{n,m}|Chaves|Especifica uma quantidade de vezes que a entidade anterior deve ocorrer|oi{1,4}|
|^|Circunflexo|Início de linha|^Bem-vindos|
|$|Cifrão|Fim de linha|Até mais$|
|\b|Borda|Início ou fim de palavra|\bdia\b|
||||dia, bom-dia, melodia, diafragma, radial|
| \ |Espace|Torna literal um metacaracteres|Tudo bem\\?|
|\||Ou|Um ou outro|amigo\|amiga|
|( )|Grupo|Delimita um grupo|^O (sabiá) (não) (sabia) (que) o sábio \3 \4 o \1 \2 \3 assobiar$|
||||O sabiá não sabia que o sábio sabia que o sabiá não sabia assobiar|
|\\1...\\9|Retrovisor|Texto casado no grupo n|(\\b\\w+\\b) \1|
||||Identifica a ocorrência de palavras palavras repetidas|

### Ponto ( . )
O metacaractere ponto (.) em uma expressão regular casa com qualquer outro caractere.
|Expressão|Casa com|
|-|-|
|Ca.a|Cama, Cana, Ca.a, Ca@a|
|.lpiste|Alpiste, alpiste, _lpiste|
|Final feliz.|Final feliz., Final feliz!, Final feliz@|

Caso seja necessário casar o caractere literal ponto ( . ), é possível utilizando o Escape ( \\ ) ou adiciona-lo em uma lista ( [] )
|Expressão|Casa com|Não casa com|
|-|-|-|
|Final feliz\\.|Final feliz.|Final feliz!, Final feliz@
|Final feliz[.]|Final feliz.|Final feliz!, Final feliz@

**Observação:** O caractere ponto ( . ) dentro de uma lista perde seu poder de casar qualquer caractere, isto também ocorre com outros metacaracteres.

### Lista ( [ ] )
O metacaractere lista ( [ ] ) em uma expressão regular casa um conjunto de caracteres.
|Expressão|Casa com|
|-|-|
|Re[vs]ista|Revista, Resista|
|<[pabPAB]>|\<p>, \<a>, \<b>, \<P>, \<A>, \<B>|
|[0123]|0, 1, 2, 3|

Em uma lista é possível especificar um intervalo através do caractere hífen ( - ), o intervalo leva em consideração a posição do caractere na tabela ASCII - https://www.ascii-code.com/
|Expressão|Casa com|
|-|-|
|[a-z]|Letras de a até z|
|[A-Z]|Letras de A até Z|
|[0-9]|Números de 0 até 9|

### Lista negada ( [^] )
O metacaractere lista negada ( [^] ) em uma expressão regular casa qualquer caractere não presente na lista
|Expressão|Casa com|
|-|-|
|Re[^vs]ista|Remista, Redista|
|<[^pabPAB]>|\<x>, \<y>|
|[^0123]|4, 5, 6, 7, @, A|

Em uma lista negada também é possível especificar um intervalo através do caractere hífen ( - ), o intervalo leva em consideração a posição do caractere na tabela ASCII - https://www.ascii-code.com/
|Expressão|Casa com|
|-|-|
|[^a-z]|Casa com qualquer caractere não presente entre a até z|
|[^A-Z]|Casa com qualquer caractere não presente entre A até Z|
|[^0-9]|Casa com qualquer caractere não presente entre 0 até 9|

### Opcional ( ? )
O metacaractere opcional ( ? ) em uma expressão regular permite que a entidade anterior ocorra zero ou uma vez
|Expressão|Casa com|
|-|-|
|Natural?|Natura, Natural|
|Desaparece[rum!]?|Desaparece, Desaparecer, Desapareceu, Desaparecem, Desaparece!|

Uma outra forma de expressar o metacaractere opcional ( ? ) é utilizando o metacaractere chaves ( {n,m} )
|Expressão|Casa com|
|-|-|
|Natural{0,1}|Natura, Natural|
|Desaparece[rum!]{0,1}|Desaparece, Desaparecer, Desapareceu, Desaparecem, Desaparece!|

### Asterisco ( * )
O metacaractere asterisco ( * ) em uma expressão regular permite que a entidade anterior ocorra em qualquer quantidade
|Expressão|Casa com|
|-|-|
|Natural*|Natura, Natural, Naturalllllllllllllll|
|Desaparece[rum!]*|Desaparece, Desaparecerrr, Desapareceu!!!!, Desaparecem!!!rrrrmmmmuuu, Desaparece!|

Uma outra forma de expressar o metacaractere asterisco ( * ) é utilizando o metacaractere chaves ( {n,m} )
|Expressão|Casa com|
|-|-|
|Natural{0,}|Natura, Natural, Naturalllllllllllllll|
|Desaparece[rum!]{0,}|Desaparece, Desaparecerrr, Desapareceu!!!!, Desaparecem!!!rrrrmmmmuuu, Desaparece!|

### Mais ( + )
O metacaractere mais ( + ) em uma expressão regular permite que a entidade anterior ocorra uma ou mais vezes
|Expressão|Casa com|
|-|-|
|Natural+|Natural, Naturalllllllllllllll|
|Desaparece[rum!]+|Desaparecerrr, Desapareceu!!!!, Desaparecem!!!rrrrmmmmuuu, Desaparece!|

Uma outra forma de expressar o metacaractere mais ( + ) é utilizando o metacaractere chaves ( {n, m} )
|Expressão|Casa com|
|-|-|
|Natural{1,}|Natural, Naturalllllllllllllll|
|Desaparece[rum!]{1,}|Desaparecerrr, Desapareceu!!!!, Desaparecem!!!rrrrmmmmuuu, Desaparece!|

### Resumo ( ? ), ( + ) e ( * )
|Expressão|Descrição|Equivalente|
|-|-|-|
|?|Deve ocorrer 0 ou 1 vez|{0,1}|
|*|Deve ocorrer 0 ou mais vezes|{0,}|
|+|Deve ocorrer 1 ou mais vezes|{1,}|

### Chaves ( {n,m} )
O metacaractere chaves ( {n,m} ) em uma expressão regular permite especificar a quantidade exata de vezes que a entidade anterior deve ocorrer
|Expressão|Descrição|
|-|-|
|{2,3}|Deve ocorrer de 2 até 3 vezes|
|{0,4}|Deve ocorrer até 4 vezes|
|{3,3}|Exatamente 3 vezes|
|{3}|Exatamente 3 vezes|
|{0,1}|Deve ocorrer até 1 vez, igual ao opcional ( ? )|
|{0,}|Deve ocorrer 0 ou mais vezes, igual ao asterisco ( * )|
|{1,}|Deve ocorrer pelo menos 1 vez, igual ao mais ( + )|

### Circunflexo: Início de linha ( ^ )
O metacaractere circunflexo ( ^ ) em uma expressão regular marca o inicio de linha
|Expressão|Descrição|
|-|-|
|^[0-9]|Casa todas as linhas que iniciam com números|
|^[^0-9]|Casa todas as linhas que não iniciam com números |

### Cifrão: Fim de linha ( $ )
O metacaractere cifrão ( $ ) em uma expressão regular marca o fim de linha
|Expressão|Descrição|
|-|-|
|[0-9]$|Casa todas as linhas que terminam com números|
|[^0-9]$|Casa todas as linhas que não terminam com números|

### Borda ( \b )
O metacaractere borda ( \b ) em uma expressão regular marca a borda entre as palavras
|Expressão|Descrição|
|-|-|
|dia|Casa dia em qualquer parte da palavra|
|\bdia|Casa apenas palavras que iniciam com dia|
|dia\b|Casa apenas palavras que terminam com dia|
|\bdia\b|Casa a palavra dia por completo|
|\Bdia\B|Casa a palavra dia dentro de outras palavras|
**Exemplo:** dia, diafragma, melodia, radial, bom-dia!

### Escape ( \ )
O metacaractere escape ( \ ) em uma expressão regular desativa o poder de um metacaractere
|Expressão|Descrição|Equivalente|
|-|-|-|
|10 \\+ 20|Casa com o literal 10 + 20|10 [+] 20|
|\\$|Casa com o literal $|[$]|
|\\.|Casa com o literal .|[.]|

### Ou ( | )
O metacaractere ou ( | ) em uma expressão regular torna possível casar com duas ou mais opções
|Expressão|Descrição|Equivalente|
|-|-|-|
|boa-tarde\|boa-noite|Casa com o literal boa-tarde ou boa-noite ||
|boa-(tarde\|noite)|Casa com o literal boa-tarde ou boa-noite ||
|amig(a\|o)|Casa com o literal amiga ou amigo|amig[ao]|

### Grupo ( ( ) )
O metacaractere grupo ( ( ) ) em uma expressão regular permite agrupar expressões regulares e potencializar o uso dos outros metacaracteres
|Expressão|Descrição|
|-|-|
|amig(a\|o)|Casa com o literal amiga ou amigo|
|(haha)+|Casa o literal haha uma ou mais vezes|
|(www\\.)?github\\.com(\\.br)?|Casa com github.com, github.com.br, www.github.com, www.github.com.br|

### Retrovisor ( \1...\9 )
O metacaractere retrovisor ( \1...\9 ) em uma expressão regular permite acessar o texto casado em um determinado grupo
|Expressão|Descrição|
|-|-|
|(quero)-\1|Casa com o literal quero-quero|
|(\b\w+\b)-\1|Casa duas palavras iguais separadas por um hífen, por exemplo, quero-quero, quebra-quebra|