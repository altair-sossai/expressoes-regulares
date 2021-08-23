# Expressões regulares
Em ciência da computação, uma expressão regular ou "Regex" provê uma forma concisa e flexível de identificar cadeias de caracteres de interesse, como caracteres particulares, palavras ou padrões de caracteres. 
Expressões regulares são escritas numa linguagem formal que pode ser interpretada por um processador de expressão regular, um programa que serve um gerador de analisador sintático ou examina o texto e identifica as partes que casam com a especificação dada. 

Fonte: https://pt.wikipedia.org/wiki/Express%C3%A3o_regular

De forma bem resumida, expressões regulares permitem encontrar padrões de textos e manipulá-los.

## Expressões Regulares - Uma abordagem divertida
Grande parte do conteúdo apresentado tem como base o livro **Expressões Regulares - Uma abordagem divertida**, recomendo a compra para apreciar esta obra maravilhosa.

![Livro Expressões Regulares - Uma abordagem divertida](https://www.piazinho.com.br/ed5/capa-292.jpg)

Site: https://www.piazinho.com.br/

## Expressões Regulares Cookbook
Este livro oferece mais de 100 receitas que vão ajudá-lo a manipular dados e textos usando expressões regulares. Todo programador deve entender um pouco de expressões regulares, mas aproveitá-las plenamente não é tão simples assim. Mesmo os usuários mais experientes, muitas vezes, sofrem com baixo desempenho, falsos positivos, falsos negativos ou defeitos imprevisíveis. Expressões Regulares Cookbook oferece orientação detalhada para algumas das tarefas mais comuns envolvendo essa ferramenta, com receitas para C#, Java, JavaScript, Perl, PHP, Python, Ruby e VB.NET.

![Expressões Regulares Cookbook](https://images-na.ssl-images-amazon.com/images/I/512WUfzhAsL._SX360_BO1,204,203,200_.jpg)

Compre em: https://www.amazon.com.br/Express%C3%B5es-Regulares-Cookbook-Jan-Goyvaerts/dp/8575222791

## Testes
Todas as expressões regulares apresentadas neste documento podem ser testadas através dos sites abaixo:
- https://www.regexpal.com/
- https://regexr.com/
- https://regex101.com/

## Aplicações
Na pratica, as expressões regulares podem ser aplicadas para uma infinidade de tarefas, elas são uteis sempre que você precisa buscar ou validar um padrão de texto, podem ser utilizadas, por exemplo, para os seguintes itens:

- Data e/ou hora nos mais diversos formatos
- Número IP
- Nome em geral
- Endereços de e-mail
- Endereços da web
- Conteúdos entre tags
- Número de documentos (CPF/RG)
- Entre outras infinitas possibilidades

## Use com moderação
Expressões regulares podem ser aplicadas para uma infinidade de problemas, mas isso não significa que você deva utilizar.

Em alguns cenários o uso de expressões regulares pode se tornar extremamente complexo e difícil de dar manutenção, veja abaixo o exemplo para validar datas no formato DD/MM/YYYY.

```
^(?:(?:31(\/|-|\.)(?:0?[13578]|1[02]))\1|(?:(?:29|30)(\/|-|\.)(?:0?[13-9]|1[0-2])\2))(?:(?:1[6-9]|[2-9]\d)?\d{2})$|^(?:29(\/|-|\.)0?2\3(?:(?:(?:1[6-9]|[2-9]\d)?(?:0[48]|[2468][048]|[13579][26])|(?:(?:16|[2468][048]|[3579][26])00))))$|^(?:0?[1-9]|1\d|2[0-8])(\/|-|\.)(?:(?:0?[1-9])|(?:1[0-2]))\4(?:(?:1[6-9]|[2-9]\d)?\d{2})$
```
**Fonte:** *https://stackoverflow.com/questions/15491894/regex-to-validate-date-format-dd-mm-yyyy-with-leap-year-support*

Abaixo, um exemplo de validação de data no mesmo formato (DD/MM/YYYY) utilizando o tipo DateTime do C#.
```csharp
const string input = "19/08/2012";
const string format = "dd/MM/yyyy";

DateTime.TryParseExact(input, format, CultureInfo.InvariantCulture, DateTimeStyles.None, out var dateTime);
```
Ambos os exemplos resolvem um problema em comum utilizando técnicas diferentes, talvez não seja uma comparação justa, mas o objetivo é apresentar o quão complexo uma expressão regular pode se tornar em relação a outras técnicas.

Sempre se questione sobre opções além do uso de expressões regulares para resolver um problema, por exemplo, devo fazer o parse de arquivos .xml, .json .yaml ou .html utilizando expressões regulares? Não seria mais interessante utilizar uma biblioteca para isso, por exemplo, Newtonsoft para JSON e HtmlAgilityPack para HTML?

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

### Exemplo de uso utilizando C#
O código abaixo faz uso da classe Regex para encontrar todas as palavras que iniciam com a letra M e exibi-las no console.
```csharp
// Create a pattern for a word that starts with letter "M"  
var pattern = @"\b[M]\w+";  

// Create a Regex  
var regex = new Regex(pattern);  
  
// Long string  
var authors = "Mahesh Chand, Raj Kumar, Mike Gold, Allen O'Neill, Marshal Troll";

// Get all matches  
var matches = regex.Matches(authors);

// Print all matched authors  
for (int count = 0; count < matches.Count; count++)  
    Console.WriteLine(matches[count].Value);  
```
**Fonte:** *https://www.c-sharpcorner.com/article/c-sharp-regex-examples/*

**Documentação classe Regex**: *https://docs.microsoft.com/pt-br/dotnet/api/system.text.regularexpressions.regex?view=net-5.0*

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

Caso seja necessário casar o caractere literal ponto ( . ), é possível utilizando o Escape ( \\ ) ou adiciona-lo em uma lista ( [] ).

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
O metacaractere lista negada ( [^] ) em uma expressão regular casa qualquer caractere não presente na lista.
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
O metacaractere opcional ( ? ) em uma expressão regular permite que a entidade anterior ocorra zero ou uma vez.
|Expressão|Casa com|
|-|-|
|Natural?|Natura, Natural|
|Desaparece[rum!]?|Desaparece, Desaparecer, Desapareceu, Desaparecem, Desaparece!|

Uma outra forma de expressar o metacaractere opcional ( ? ) é utilizando o metacaractere chaves ( {n,m} ).

**Observação:** Para utilizar a versão não gulosa do opcional, utilize o metacaractere ( ?? ).

|Expressão|Casa com|
|-|-|
|Natural{0,1}|Natura, Natural|
|Desaparece[rum!]{0,1}|Desaparece, Desaparecer, Desapareceu, Desaparecem, Desaparece!|

### Asterisco ( * )
O metacaractere asterisco ( * ) em uma expressão regular permite que a entidade anterior ocorra em qualquer quantidade.
|Expressão|Casa com|
|-|-|
|Natural*|Natura, Natural, Naturalllllllllllllll|
|Desaparece[rum!]*|Desaparece, Desaparecerrr, Desapareceu!!!!, Desaparecem!!!rrrrmmmmuuu, Desaparece!|

Uma outra forma de expressar o metacaractere asterisco ( * ) é utilizando o metacaractere chaves ( {n,m} ).

**Observação:** Para utilizar a versão não gulosa do asterisco, utilize o metacaractere ( *? ).

|Expressão|Casa com|
|-|-|
|Natural{0,}|Natura, Natural, Naturalllllllllllllll|
|Desaparece[rum!]{0,}|Desaparece, Desaparecerrr, Desapareceu!!!!, Desaparecem!!!rrrrmmmmuuu, Desaparece!|

### Mais ( + )
O metacaractere mais ( + ) em uma expressão regular permite que a entidade anterior ocorra uma ou mais vezes.
|Expressão|Casa com|
|-|-|
|Natural+|Natural, Naturalllllllllllllll|
|Desaparece[rum!]+|Desaparecerrr, Desapareceu!!!!, Desaparecem!!!rrrrmmmmuuu, Desaparece!|

Uma outra forma de expressar o metacaractere mais ( + ) é utilizando o metacaractere chaves ( {n, m} ).

**Observação:** Para utilizar a versão não gulosa do mais, utilize o metacaractere ( +? ).

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
O metacaractere chaves ( {n,m} ) em uma expressão regular permite especificar a quantidade exata de vezes que a entidade anterior deve ocorrer.
|Expressão|Descrição|
|-|-|
|{2,3}|Deve ocorrer de 2 até 3 vezes|
|{0,4}|Deve ocorrer até 4 vezes|
|{3,3}|Exatamente 3 vezes|
|{3}|Exatamente 3 vezes|
|{0,1}|Deve ocorrer até 1 vez, igual ao opcional ( ? )|
|{0,}|Deve ocorrer 0 ou mais vezes, igual ao asterisco ( * )|
|{1,}|Deve ocorrer pelo menos 1 vez, igual ao mais ( + )|

**Observação:** Para utilizar a versão não gulosa das chaves, utilize o metacaractere ( {n,m}? )

### Circunflexo: Início de linha ( ^ )
O metacaractere circunflexo ( ^ ) em uma expressão regular marca o inicio de linha.
|Expressão|Descrição|
|-|-|
|^[0-9]|Casa todas as linhas que iniciam com números|
|^[^0-9]|Casa todas as linhas que não iniciam com números |

### Cifrão: Fim de linha ( $ )
O metacaractere cifrão ( $ ) em uma expressão regular marca o fim de linha.
|Expressão|Descrição|
|-|-|
|[0-9]$|Casa todas as linhas que terminam com números|
|[^0-9]$|Casa todas as linhas que não terminam com números|

### Borda ( \b )
O metacaractere borda ( \b ) em uma expressão regular marca a borda entre as palavras.
|Expressão|Descrição|
|-|-|
|dia|Casa dia em qualquer parte da palavra|
|\bdia|Casa apenas palavras que iniciam com dia|
|dia\b|Casa apenas palavras que terminam com dia|
|\bdia\b|Casa a palavra dia por completo|
|\Bdia\B|Casa a palavra dia dentro de outras palavras|
**Exemplo:** dia, diafragma, melodia, radial, bom-dia!

### Escape ( \ )
O metacaractere escape ( \ ) em uma expressão regular desativa o poder de um metacaractere.
|Expressão|Descrição|Equivalente|
|-|-|-|
|10 \\+ 20|Casa com o literal 10 + 20|10 [+] 20|
|\\$|Casa com o literal $|[$]|
|\\.|Casa com o literal .|[.]|

### Ou ( | )
O metacaractere ou ( | ) em uma expressão regular torna possível casar com duas ou mais opções.
|Expressão|Descrição|Equivalente|
|-|-|-|
|boa-tarde\|boa-noite|Casa com o literal boa-tarde ou boa-noite ||
|boa-(tarde\|noite)|Casa com o literal boa-tarde ou boa-noite ||
|amig(a\|o)|Casa com o literal amiga ou amigo|amig[ao]|

### Grupo ( ( ) )
O metacaractere grupo ( ( ) ) em uma expressão regular permite agrupar expressões regulares e potencializar o uso dos outros metacaracteres.
|Expressão|Descrição|
|-|-|
|amig(a\|o)|Casa com o literal amiga ou amigo|
|(haha)+|Casa o literal haha uma ou mais vezes|
|(www\\.)?github\\.com(\\.br)?|Casa com github.com, github.com.br, www.github.com, www.github.com.br|

### Retrovisor ( \1...\9 )
O metacaractere retrovisor ( \1...\9 ) em uma expressão regular permite acessar o texto casado em um determinado grupo.
|Expressão|Descrição|
|-|-|
|(quero)-\1|Casa com o literal quero-quero|
|(\b\w+\b)-\1|Casa duas palavras iguais separadas por um hífen, por exemplo, quero-quero, quebra-quebra|

## Metacaracteres adicionais
Abaixo um consolidado de alguns metacaracteres frequentemente utilizados na construção de expressões regulares.
|Expressão|Casa com|Equivalente|
|-|-|-|
|\\w|Casa com a-z, A-Z, 0-9 ou _ |[a-zA-Z0-9_]|
|\\W|Casa com todos os caracteres, exceto os presentes em \w |[^a-zA-Z0-9_]|
|\\d|Casa com 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 |[0-9]|
|\\D|Casa com todos os caracteres, exceto os presentes em \d |[^0-9]|
|\\s|Casa com qualquer caractere de espaço em branco|[\\r\\n\\t\\f\\v ]|
|\\S|Casa com todos os caracteres, exceto os presentes em \s |[^\\r\\n\\t\\f\\v ]|

## Links Úteis
Abaixo alguns links para conhecer um pouco mais sobre o uso de expressões regulares.

**Lookahead and Lookbehind**<br/>
Tutorial sobre os recursos de lookahead e lookbehind<br/>
*https://www.regular-expressions.info/lookaround.html*

**Regular Expression Tips**<br/>
Learn to use regular expressions by following RegexTip. From 
@JohnDCook<br/>
*https://twitter.com/RegexTip*

**Regex Cross­word:** <br/>
Jogo de palavras cruzadas utilizando expressões regulares<br/>
*https://regexcrossword.com*

**Regex Class (C#):**<br/>
Documentação oficial Microsoft das classes de uso de expressões regulares em dotnet<br/>
*https://docs.microsoft.com/pt-br/dotnet/api/system.text.regularexpressions.regex?view=net-5.0*

**HackerRank - Regex:** <br/>
Problemas no formato ‘Maratona de Programação’ que devem ser resolvidos utilizando expressões regulares<br/>
*https://www.hackerrank.com/domains/regex*