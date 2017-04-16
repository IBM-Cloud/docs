---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Usando as APIs REST do Insights for Twitter
{: #rest_apis}

O serviço {{site.data.keyword.twittershort}} consiste em APIs RESTful para procurar e consumir conteúdo do Twitter. A tabela [Linguagem de consulta](twitter_rest_apis.html#querylanguage){: new.window} lista os termos de consulta que são suportados pelas APIs de serviço. São fornecidos exemplos para demonstrar como as consultas podem ser construídas.
{:shortdesc}

## Documentação da API REST {: #rest_api}
A documentação da API REST é construída usando Swagger, que permite testar operações de API e visualizar instantaneamente os resultados para ajudá-lo a construir seus aplicativos mais rapidamente.
As operações da API a seguir estão disponíveis atualmente:

* Procura: localiza tweets no Decahose ou no fluxo filtrado do PowerTrack.
* Contagem: retorna o número de tweets com base em uma consulta especificada.
* Verificação: determina se uma lista de mensagens obedece às políticas do	Twitter e dos usuários do Twitter.
* Faixas: fornece aos usuários do Plano de entrada um sortimento de terminais para gerenciar filtros do PowerTrack.

Para obter mais informações sobre as APIs REST suportadas e seus recursos, consulte a referência da [API REST](https://cdeservice.{APPDomain}/rest-api/){: new_window}. Selecione a região onde o seu aplicativo existe. Cada
região é independente; não é possível usar as credenciais de
serviço que são fornecidas para um Cliente em uma região para
autenticar um serviço em outra região.

Na
documentação de referência, clique em
**Listar Operações** para visualizar os
detalhes
de cada operação. Depois de clicar no botão **Experimente!**, é possível que você seja solicitado a fornecer credenciais. Será necessário fornecer o nome de usuário e a senha de suas variáveis de ambiente **VCAP_SERVICES**. É possível localizar estas informações abrindo seu aplicativo e
clicando em **Variáveis de Ambiente** a partir do
índice.

**Nota**: a falha em inserir as credenciais adequadas resulta em uma mensagem "Desautorizado" no corpo de resposta.

**Importante**: as faixas ativas que são criadas usando o recurso **Experimente!** coletam tweets do Twitter, que são contabilizados em seu abono mensal. Quando as faixas não são mais necessárias,
altere seu estado para **Inativo** ou simplesmente exclua a faixa.


## Linguagem de consulta {: #querylanguage}

Com o {{site.data.keyword.twittershort}}, é possível procurar
o conteúdo do Twitter usando um conjunto completo de parâmetros de consulta e filtros para produzir
resultados mais precisos.

Os operadores booleanos a seguir são suportados em suas consultas. 

| **Operador**        | **Descrição**                                                                                                                   | **Exemplos**      |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------|-------------------|
| term1 **AND** term2 | Retorna tweets que contêm tanto term1 quanto term2. O espaço em branco entre dois termos é tratado como AND, para que o operador possa ser omitido. | `#ibm twitter`      |
| term1 **OR** term2  | Retorna tweets que contêm term1 ou term2.    | `#money OR revenue` |
| -term1              | Retorna tweets que não contêm term1.  |`ibm -apple`  |

*Tabela 1. Operadores booleanos*

Precedência do operador: "-" tem precedência sobre "AND" e "AND" tem precedência sobre "OR". É necessário usar parênteses para tornar a precedência do operador explícita. Por exemplo, `large animals` -(`giraffes` OR `bears`) procura tweets que contêm os termos "large" e "animals", mas exclui os tweets que contêm "giraffes" e "bears".

A tabela a seguir lista os termos de consulta suportados atualmente.

| **Termo** 	| **Descrição** 	| **Exemplos** 	|
|----------------------------------------------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|---------------------------------------------	|
| palavra-chave 	| Corresponde aos tweets que têm "palavra-chave" em seu corpo. A
procura é sem distinção entre maiúsculas e minúsculas. 	| analítica 	|
| "correspondência de frase exata" 	| Corresponde tweets que contêm a exata sequência da palavra-chave. 	| "IBM e análise" 	|
| `#hashtag` 	| Corresponde aos tweets com a hashtag *#hashtag*. 	| `#insight2015` 	|
| `bio_lang:language` 	| Corresponde aos tweets de usuários cujas configurações
de idioma de perfil correspondem ao código de idioma especificado.  Consulte `lang:` para obter uma lista de idiomas suportados. 	| `bio_lang:en` 	|
| `bio_location:"location"` 	| Corresponde aos tweets de usuários cuja configuração de local de perfil contém a referência `location` especificada. 	| `bio_location:"New York"` 	|
| `country_code:country-code` 	| Corresponde aos tweets cujo lugar ou localização com tag correspondem ao código do país especificado. </br>**Para obter uma lista de códigos de países suportados, consulte**: http://en.wikipedia.org/wiki/ISO_3166-1 	| `country_code:us` 	|
| `followers_count: lowerLimit,upperLimit` 	| Corresponde aos tweets de usuários que têm um número de seguidores que diminui dentro
						do intervalo especificado. O upperLimit é opcional e ambos os limites são inclusivos. 	| `followers_count:500` 	|
| `friends_count: lowerLimit,upperLimit` 	| Corresponde aos tweets de usuários que seguem um número de usuários que diminui dentro do
							intervalo especificado. O upperLimit é opcional e ambos os limites são inclusivos. 	| `friends_count:1000,3000` 	|
| `from:twitterHandle` 	| Corresponde aos tweets de usuários com o preferredUsername *twitterHandle*. Não deve conter o símbolo &commat;. 	| `from:alexlang11` 	|
| `has:children` 	| Corresponde aos tweets de usuários que têm filhos. 	| `has:children` 	|
| `is:married` 	| Corresponde aos tweets de usuários que são casados. 	| `is:married` 	|
| `is:verified` 	| Corresponde aos tweets em que o autor foi verificado pelo Twitter. 	| `analytics is:verified` 	|
| `lang:language-code` 	| Corresponde tweets de um determinado idioma. A lista de códigos de idioma suportados é: <ul><li>`ar` (árabe)</li><li>`zh` (chinês)</li><li>`da` (dinamarquês)</li><li>`dl` (holandês)</li><li>`en`
(Inglês)</li><li>`fi` (finlandês)</li><li>`fr` (Francês)</li><li>`de`
(Alemão)</li><li>`el` (grego)</li><li>`he` (hebraico)</li><li>`id` (indonésio)</li><li>`it`
(Italiano)</li><li>`ja` (Japonês)</li><li>`ko`
(Coreano)</li><li>`no` (norueguês)</li><li>`fa` (persa)</li><li>`pl` (Polonês)</li><li>`pt` (português)</li><li>`ru` (Russo)</li><li>`es`
(Espanhol)</li><li>`sv` (sueco)</li><li>`th` (tailandês)</li><li>`tr` (turco)</li><li>`uk` (ucraniano)</li></ul>    | `lang:de` (para corresponder aos tweets alemães) 	|
| `listed_count: lowerLimit,upperLimit` 	| Corresponde aos tweets em que a listagem do autor do Twitter diminui dentro do intervalo especificado. O upperLimit é opcional e ambos
os limites são inclusivos. 	| `listed_count:1000,3000` 	|
| `point_radius:[longitude latitude radius]` 	| Corresponde aos tweets de uma região geográfica, especificada pelas suas coordenadas de longitude e latitude e um
raio. </br></br>Todas as coordenadas são representadas em graus decimais. A `longitude` deve ser um valor entre -180 e +180, enquanto `latitude` deve ser um valor entre -90 e +90. Especificar um valor fora dos intervalos suportados retorna um erro. Os valores devem ser inseridos
como números de vírgula flutuante; os números inteiros não são suportados. </br></br>O raio da área circundante deve ser especificado em milhas (mi) ou
								quilômetros (km). 	| `point_radius:[41.128611 -73.707778 5.0mi]` 	|
| `posted:startTime  posted:startTime,endTime` 	| Corresponde aos tweets que foram postados em ou depois de "startTime". O "endTime" é opcional e ambos os limites são inclusivos. Os
registros de data e hora devem estar em um dos seguintes formatos:  </br>"yyyy-mm-dd" ou "yyyy-mm-ddTHH:MM:SSZ" </br>  O fuso horário baseia-se no UTC (Hora Universal
Coordenada). Ao especificar horas, minutos e segundos, o tempo deve ser incluído entre "T" e "Z", como no formato prescrito. 	| `posted:2014-12-01,2014-12-12` 	|
| `sentiment:sentiment-value` 	| Corresponde tweets com uma determinada impressão. Os valores suportados são: </br><dl>positivo</dl> <dlentry>O tweet contém mais frases de impressão positiva que negativa.</dlentry> </br></br><dl>negativa</dl> <dlentry>O tweet contém mais frases de impressão negativa que positiva.</dlentry>  </br></br><dl>neutro</dl>  <dlentry>O tweet não contém nenhuma impressão ou está em um idioma que não oferece detecção de impressão.</dlentry> </br></br><dl>ambivalente</dl>  <dlentry>O tweet contém uma quantia igual de frases de impressão positiva e negativa.</dlentry> 	| `sentiment:positive` 	|
| `statuses_count: lowerLimit,upperLimit` 	| Corresponde aos tweets de usuários que postaram um número de status que diminui dentro
							do intervalo especificado. O upperLimit é opcional e ambos os limites são inclusivos. 	| `statuses_count:1000,3000` 	|
| `time_zone:timeZone` 	| Corresponde aos tweets de usuários cujas configurações de perfil correspondem ao fuso horário especificado. 	| `time_zone:"Eastern Time (US & Canada)"` 	|
| `time_zone:city` 	| Corresponde aos tweets de usuários cujas configurações de perfil correspondem à cidade especificada. 	| `time_zone:"Dublin"` 	|
*Tabela 2. Termos de consulta*

Todos os termos de consulta suportados podem ser combinados com os operadores booleanos descritos anteriormente. Por
			exemplo,

`ibm -apple followers_count:500`
