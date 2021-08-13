# Expressões regulares
Em ciência da computação, uma expressão regular ou "Regex" provê uma forma concisa e flexível de identificar cadeias de caracteres de interesse, como caracteres particulares, palavras ou padrões de caracteres. 
Expressões regulares são escritas numa linguagem formal que pode ser interpretada por um processador de expressão regular, um programa que serve um gerador de analisador sintático ou examina o texto e identifica as partes que casam com a especificação dada.
Fonte: https://pt.wikipedia.org/wiki/Express%C3%A3o_regular

De forma bem resumida, é uma forma de especificar um padrão de texto.

## Fonte
Grande parte do conteúdo apresentado tem como base o livro *Livro Expressões Regulares - Uma abordagem divertida*, recomendo a compra para apreciar esta obra maravilhosa.

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
|\b|Borda|Início ou fim de palavra|Até mais$|
| \ |Espace|Torna literal um metacaracteres|Tudo bem\\?|
|\||Ou|Um ou outro|Amiga\|o|
|( )|Grupo|delimite um grupo|([0-9]{2})\\.([0-9]{3})|
|\\n|Retrovisor|Texto casado no grupo n|(\\b\\w+\\b) \1|

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

### Lista ( [] )
O metacaractere lista ( [] ) em uma expressão regular casa um conjunto predefinido de caracteres.
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

Uma outra forma de expressar o metacaractere opcional ( ? ) é utilizando o metacaractere chaves ( {n, m} )
|Expressão|Casa com|
|-|-|
|Natural{0, 1}|Natura, Natural|
|Desaparece[rum!]{0, 1}|Desaparece, Desaparecer, Desapareceu, Desaparecem, Desaparece!|

### Asterisco ( * )
O metacaractere asterisco ( * ) em uma expressão regular permite que a entidade anterior ocorra em qualquer quantidade
|Expressão|Casa com|
|-|-|
|Natural*|Natura, Natural, Naturalllllllllllllll|
|Desaparece[rum!]*|Desaparece, Desaparecerrr, Desapareceu!!!!, Desaparecem!!!rrrrmmmmuuu, Desaparece!|

Uma outra forma de expressar o metacaractere asterisco ( * ) é utilizando o metacaractere chaves ( {n, m} )
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

### Chaves ( {n, m} )
O metacaractere chaves ( {n, m} ) em uma expressão regular permite especificar a quantidade exata de vezes que a entidade anterior deve ocorrer
|Expressão|Descrição|
|-|-|
|{2, 3}|Deve ocorrer de 2 até 3 vezes|
|{0, 4}|Deve ocorrer até 4 vezes|
|{3, 3}|Exatamente 3 vezes|
|{3}|Exatamente 3 vezes|
|{0, 1}|Deve ocorrer até 1 vez, igual ao opcional ( ? )|
|{0,}|Deve ocorrer 0 ou mais vezes, igual ao asterisco ( * )|
|{1,}|Deve ocorrer pelo menos 1 vez, igual ao mais ( + )|
