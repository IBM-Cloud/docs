---

copyright:
  years: 2015, 2017
lastupdated: "2016-07-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Dicas de tradução de máquina
{: #globalizationpipeline_tips}


A tradução de máquina pode ser eficaz em fornecer uma aproximação do significado do texto de origem. Entretanto, a qualidade e utilidade da tradução de máquina varia muito dependendo do idioma de destino e do mecanismo de tradução de máquina que você usa. Um dos principais fatores na qualidade da tradução de máquina é a qualidade da origem em si. Um texto de origem carregado de coloquialismos, sentenças incompletas, pontuação incorreta e palavras e frases ambíguas pode não ser traduzido com precisão.
{:shortdesc}

Quando você estiver criando a IU de seu app {{site.data.keyword.Bluemix_notm}}, siga algumas diretrizes básicas de composição para melhorar não apenas seu idioma de origem, mas também a qualidade da tradução de máquina.

Além disso, peça aos falantes do idioma nativo para revisar e editar a tradução de máquina. Reúna também feedback dos usuários de seu app; eles talvez sejam os melhores juízes da utilidade e precisão da tradução.

## Dicas de estilo de composição
{: #writingstyletips}

* **Use sentenças simples de curtas a médias (5 a 20 palavras):** os mecanismos de tradução de máquina muitas vezes têm dificuldade de traduzir sentenças compostas e complexas, incluindo sentenças com ponto-e-vírgula. Transmita um pensamento por sentença. Se uma sentença contiver dois verbos ativos para transmitir dois pensamentos, divida a sentença em duas. Os mecanismos de tradução de máquina também têm problema na análise sintática de sentenças que são muito curtas para fornecer contexto suficiente.
* **Evite frases:** use sentenças completas sempre que possível. Frases são aceitáveis para títulos e subtítulos, mas evite composição no estilo telegráfico de manchete. Use sentenças completas para introduzir listas.
* **Evite idiomas, gírias e jargões:** substitua frases para as quais traduções literais não façam sentido. Por exemplo, substitua "on the fly" por "dynamic", "on the other hand" por "alternatively" e "keep in mind" por "remember."
* **Evite piadas, ironias, coloquialismos, emoticons e metáforas.**
* **Seja sucinto:** remova texto desnecessário e redundâncias. Por exemplo, substitua "It is useful to remember that large values increase the response time" por "Large values increase the response time."
* **Evite sentenças escritas totalmente em letras maiúsculas:** a capitalização fornece pistas para o significado da palavra. Por exemplo, se você escrever "BILL", o mecanismo de tradução de máquina não poderá determinar se você quis dizer o nome "Bill" ou a palavra "bill".
* **Evite palavras ambíguas:** por exemplo, não use "once" no lugar de "after" ou "when". Não use "while" no lugar de "although" ou "whereas". Não use "may" quando você quiser dizer "might" ou "can".
* **Evite pronomes:** repita substantivos ou frases nominais quando possível. O pronome "it" é especialmente problemático.
* **Escreva na voz ativa quando possível:**
sentenças ativas normalmente ficam mais claras do que passivas. Por exemplo, escreva "The utility determines which path is most efficient", em vez de "The most efficient path is determined".
* **Evite informações culturalmente específicas.**
* **Esteja ciente de que mecanismos de tradução de
máquina podem traduzir nomes de produto:** muitos países mantêm o nome do produto do inglês original, mas mecanismos de tradução de máquina poderão tentar traduzi-los, especialmente se os nomes contiverem palavras reais. Antes de usar um nome de produto, teste a tradução dele. Se encontrar problemas, modifique o texto ou a tradução adequadamente.
* **Assegure-se de que todas as informações sejam
escritas em um só idioma:** mecanismos de tradução de máquina podem assumir que todas as informações estão em um único idioma, mesmo que o texto inclua uma ou duas palavras em outro idioma. Por exemplo, se o texto incluir "en route" (francês), o mecanismo de tradução de máquina ainda tentará traduzir essas palavras como se fossem palavras em inglês.
* **Evite slogans de marketing:** os slogans de marketing geralmente confiam no entendimento do público de uma determinada cultura. Evite esses tipos de slogans porque mecanismos de tradução de máquina provavelmente terão problema para traduzi-los com precisão.
* **Assegure-se de que itens de lista sejam completos e paralelos:** por exemplo, se um item começar com verbo, certifique-se de que todos os itens comecem com verbo.
* **Evite usar por favor e obrigado:** essas palavras podem parecer fora de lugar ou até paternalistas em algumas culturas.
* **Escreva datas em formato não numérico:** formatos numéricos para datas variam dependendo do país. Escreva o nome do mês, o dia e o ano. Por exemplo, use 1 de setembro de 2003, em vez de 9/01/03, que poderá ser interpretado como 1 de setembro de 2003 ou como 9 de janeiro de 2003.

## Dicas de gramática
{: #grammartips}

* **Use pontuação adequada:** a omissão de pontos e vírgulas pode fazer com que um mecanismo de tradução de máquina interprete incorretamente as informações.
* **Assegure-se de que os sujeitos concordem com seus
verbos:** assegure-se de que sujeitos no plural tenham verbos no plural e sujeitos no singular tenham verbos no singular.
* **Use tempos verbais no presente simples:** muitos outros idiomas não têm as características verbais do inglês, como voz e tempo. Sempre que possível, evite tempos verbais no futuro e no passado. Por exemplo, você pode reescrever "If you run this program, DB2® will return an error message" como "If you run this program, DB2 returns an error message".
* **Assegure-se de que os pronomes concordem com seus antecedentes:** por exemplo, "A user should first determine their tasks" deveria ser reescrito como "Users should first determine their tasks"..
* **Evite modificadores soltos:** coloque os modificadores na posição apropriada para que eles modifiquem o substantivo desejado. Por exemplo, "While typing in commands, the program does not send any messages to you" pode ser reescrito como "While typing in commands, you do not receive any messages from the program".
* **Evite negativos duplos:** por exemplo,
"Do not omit the date" pode ser substituído por "Include the date."
* **Evite as formas de verbos no infinitivo
(escrever), gerúndio (escrevendo) e particípio passado (escreveu) no início de sentenças:** essas formas verbais geralmente são ambíguas e difíceis de traduzir.
* **Evite sequências de substantivos:** limite frases com substantivos compostos, como "special filter factor estimate considerations", a não mais que três palavras.
* **Evite usar palavras em categorias gramaticais
múltiplas:** em inglês, muitas palavras, como "default", podem ser substantivo ou verbo. Essa estrutura não se aplica a muitos outros idiomas. Seja consistente no modo de usar cada palavra. Por exemplo, sempre use "default" como substantivo.
* **Assegure-se de que os elementos de uma sentença
sejam paralelos:** por exemplo, use só substantivos ou só verbos em uma lista dentro da sentença; não misture substantivos e verbos.
* **Não omita palavras necessárias:** por exemplo, em vez de "The file names are displayed in uppercase characters and the file extensions in lowercase", use "The file names are displayed in uppercase characters and the file extensions are displayed in lowercase characters". Use a palavra "that" para fornecer esclarecimento, conforme necessário. Por exemplo, substitua "If you determine the problem is a missing file" por "If you determine that the problem is a missing file".
* **Não use um traço com função de parênteses:** por exemplo, não escreva "When you get to this point - the point when all data has been loaded - you need to test the system". Substitua os traços por vírgulas ou reescreva a
sentença.
 
## Dicas de terminologia
{: #terminologytips}

* **Use terminologia de forma consistente:** evite usar diversos termos para se referir à mesma coisa. Evite usar um único termo para se referir a mais de uma coisa.
* **Inclua explicações para qualquer termo especializado.**
* **Evite termos que tenham significados diferentes em outros ambientes e contextos:** esses termos incluem "billion," "domestic," e "foreign".
* **Use letras maiúsculas e minúsculas, hifens e formação de palavras de forma consistente e padronizada:** por exemplo, escreva "fix pack" em vez de "fix pack".
* **Use minúscula, a menos que o termo seja um substantivo próprio.**
* **Evite símbolos especiais:** se você precisar usar o símbolo #, não se refira a ele como cerquilha. Em vez disso, chame-o como símbolo de número (#).
* **Evite abreviações:** mecanismos de tradução de máquina podem reconhecer abreviações comuns, como IBM e DB2, mas não reconhecem todas. Evite abreviações sempre que possível. Não use abreviações do latim, como "i.e." e "etc."

## Dicas de pontuação
{: #punctuationtips}

* **Evite usar uma barra como significado de "e
ou":** reescreva a sentença para indicar o significado exato. Por exemplo, você pode reescrever "You can view the draft copy and/or the review copy" como "You can view the draft copy, the review copy, or both".
* **Não indique plural acrescentando (s):**
use a frase "one or more" ou use a forma plural somente.
* **Não use e comercial (&) como significado de e.**
* **Use vírgula para separar itens em uma lista
dentro da sentença e coloque vírgula antes da conjunção na
lista:** por exemplo, "Select your company, location, and profession".

## Dicas de ortografia
{: #spellingtips}

* **Verifique a ortografia:** palavras com erros ortográficos podem causar erros de tradução. Verifique sempre se há erros de digitação!
* **Use ortografia consistente:** assegure-se de que termos, acrônimos e nomes próprios sejam escritos sempre da mesma maneira, inclusive quanto ao uso de letras maiúsculas e minúsculas.

## Dicas de apresentação visual
{: #visualtips}

* **Evite texto em gráficos.**
* **Evite usar formatação para enfatizar.**

