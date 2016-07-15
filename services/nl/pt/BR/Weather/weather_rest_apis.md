---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Usando as APIs REST do {{site.data.keyword.weather_short}}
{: #rest_apis}

*Última atualização: 01 de julho de 2016*
{: .last-updated}

É possível usar as [APIs REST](https://twcservice.{APPDomain}/rest-api/){:new_window}
para recuperar dados de clima. É possível testar operações de API e visualizar instantaneamente os resultados para ajudar a construir seus aplicativos mais rapidamente.
{: shortdesc}

Na
documentação de referência, clique em
**Listar Operações** para visualizar os
detalhes
de cada operação.
Ao especificar parâmetros e clicar em
**Experimente!**, pode ser solicitado que se
forneça credenciais.
Deve-se fornecer o nome do usuário e senha de
suas variáveis de ambiente `VCAP_SERVICES`.
É possível localizar estas informações abrindo seu aplicativo e
clicando em **Variáveis de Ambiente** a partir do
índice.

**Nota:** cada região é independente. Não é possível usar credenciais de serviço
fornecidas a você em uma região para se autenticar em um serviço em outra região.
A falha ao inserir credenciais adequadas resultará em uma mensagem "Desautorizado" no corpo da resposta.

Com as APIs REST, é possível recuperar dados de clima fornecendo uma localização geográfica como coordenadas de latitude e longitude.
É possível usar as APIs a seguir.

|**API**                                  |**Descrição**              |
|-----------------------------------------|-----------------------------|
|`GET /v1/{geocode or location
ID}/forecast/hourly/48hour.json`  |Retorna a previsão de clima de hora em hora para as próximas 48 horas para uma localização geográfica dependendo do
formato que você fornecer. É possível fornecer um `geocode/{latitude}/{longitude}` ou um `location/{locationId}`. Os dados de previsão de hora em hora podem conter até 48
previsões de hora em hora para cada local. Deve-se descartar todas as
previsões de hora em hora anteriores para um local quando novos dados
forem recebidos.|
|`GET /v1/{geocode or location
ID}/forecast/daily/{format}.json`   |Retorna previsões de clima diário para 3, 5, 7 ou 10 dias para uma localização geográfica dependendo do formato que você
fornecer. O número de dias retornados é especificado no formato como `3day`, `5day`, `7day` ou
`10day`. É possível fornecer um `geocode/{latitude}/{longitude}` ou um `location/{locationId}`. Cada previsão diária pode conter uma previsão diurna, uma
previsão noturna e uma previsão de 24 horas. Esses segmentos são objetos
separados nas respostas JSON. Os dados de previsão diurna da previsão diária não ficam mais disponíveis depois do horário local de 15h. Às 15h, horário local, seu aplicativo não
deverá mais exibir a previsão do dia.|
|`GET /v1/{geocode or location
ID}/forecast/intraday/{format}.json`|Retorna previsões de clima diário em períodos de 6 horas para 3, 5, 7 ou 10 dias para uma localização geográfica
dependendo do formato que você fornecer. O número de dias retornados é especificado no formato como `3day`, `5day`, `7day` ou `10day`. É
possível fornecer um `geocode/{latitude}/{longitude}` ou um `location/{locationId}`. Cada previsão diária pode conter uma previsão da manhã, tarde, noite e de
durante a noite. Esses segmentos são objetos
separados nas respostas JSON.|
|`GET /v1/{geocode or location ID}/observations.json`              |Retorna as condições climáticas atuais de uma localização geográfica. É possível fornecer um
`geocode/{latitude}/{longitude}` ou um `location/{locationId}`. As observações recentes são retidas no banco de dados por até 10 minutos em estações de relatório específicas e 24 horas de observações por estação. Os dados de
observação recentes são atualizados continuamente e substituídos
com uma metodologia first-in / first-out (dados rotativos com
observações mais recentes e deslocamento das observações mais
antigas para o armazenamento de archive)
com base na formatação do registro de data/hora das observações.|
|`GET /v1/{geocode or location
ID}/observations/timeseries.json`   |Retorna as observações atuais e até 24 horas de observações passadas, a partir da data e hora atuais, de uma localização geográfica. 
É possível fornecer um `geocode/{latitude}/{longitude}` ou um `location/{locationId}`. As observações climáticas são reunidas a partir
de dispositivos físicos implementados em todo o mundo e as observações climáticas
atuais.|
|`GET /v1/{geocode, country code, state, or
area}/alerts.json`      |Retorna observações de clima, avisos, instruções e avisos que são emitidos pelo Serviço Nacional de Meteorologia (NWS),
Environment Canada e MeteoAlarm (Europa) e incluem a tradução da descrição do evento, o nome do país e manchetes de alerta em 49 idiomas. É possível fornecer um `geocode/{latitude}/{longitude}`,
`country/{countrycode}`, `country/{countrycode}/state/{statecode}`/ ou `country/{countrycode}/area/{areaid}`.|
|`GET /v1/alert/{detail_key}/details.json`                         |Retorna observações de clima, avisos, instruções e avisos que são emitidos pelo Serviço Nacional de Meteorologia (NWS),
Environment Canada e MeteoAlarm (Europa). Os detalhes incluem informações detalhadas sobre o alerta emitido pela autoridade meteorológica do governo para a área especificada e incluem a tradução da descrição
do evento, o nome do país e manchetes de alerta em 49 idiomas.|
|`GET /v1/{geocode or postal code}/almanac/daily.json`             |Retorna informações diárias de almanaque (apenas EUA) que são originadas das estações de observações do Serviço Nacional de
Meteorologia a partir de um período de medição de 10 a 30 anos ou mais. As informações são reunidas e fornecidas pelo Centro Nacional de Dados Climáticos (NCDC). É possível fornecer um `geocode/{latitude}/{longitude}` ou
`location/{PostalLocationId}`.|
|`GET /v1/{geocode or postal
code}/almanac/monthly.json`           |Retorna informações mensais de almanaque (apenas EUA) que são originadas das estações de observações do
Serviço Nacional de Meteorologia a partir de um período de medição de 10 a 30 anos ou mais. As
informações são reunidas e fornecidas pelo Centro Nacional de Dados Climáticos (NCDC). É possível fornecer um
`geocode/{latitude}/{longitude}` ou `location/{PostalLocationId}`.|
|`GET /v3/location/{search or point}`                                  |Fornece a capacidade de procurar um nome ou uma localização geográfica do local (latitude e longitude) para recuperar
um conjunto de locais que correspondem à solicitação. O Serviço de Localização suporta procura por nome da cidade ou código de endereçamento postal.|
*Tabela 1. Resumo da API do {{site.data.keyword.weather_short}}*

## Previsões diárias e intradiárias
{: #daily_intraday}
A API de previsão diária pode conter múltiplos dias ou previsões diárias para cada local.
Cada dia de uma previsão pode conter até três previsões separadas. Para qualquer dia de
previsão especificado a API pode retornar previsões de dia, noite e de 24 horas.

A API de previsão intradiária pode conter múltiplos dias ou previsões diárias para cada local.
Cada dia de uma previsão contém quatro previsões de 6 horas separadas
para manhã (das 7h às 13h),
tarde (das 13h às 19h), noite (das 19h às 1h) e durante a
noite (da 1h às 7h). A
previsão intradiária é semelhante em estrutura à previsão diária.

Cada segmento tem um número da parte do dia, dia do nome da semana e nome da parte do dia. Por exemplo,
o exemplo a seguir mostra a ordem do campo de dados e os valores dos dados para
`num`, `dow` e o `daypart_name`, para uma previsão que é gerada
pelas APIs em uma manhã de quinta-feira:
* 1, Quinta-feira, Manhã
* 2, Quinta-feira, Tarde
* 3, Quinta-feira, Noite
* 4, Quinta-feira, Durante a noite
* 5, Sexta-feira, Manhã
* 6, Sexta-feira, Tarde
* 7, Sexta-feira, Noite
* 8, Sexta-feira, Durante a noite

## Observações atuais de série temporal
{: #time_series}

Os dados de observações meteorológicas de condições atuais e de série temporal fornecem informações sobre temperatura,
precipitação, vento, pressão barométrica, visibilidade, radiação ultravioleta (UV)
e outros elementos de observação relacionados, incluindo estação de observação,
data/hora de observação, códigos e frases de ícone de clima. A diferença entre
observações séries temporais e observações atuais é o período de
tempo da observação, que resulta em um ou mais conjuntos de dados de
observação.

As condições atuais são as observações mais recentes para o local
que é solicitado sem parâmetro de horário. Um conjunto de dados é
retornado. As observações séries temporais incluem observações
passadas que ocorreram até e incluindo as últimas 24 horas para o
local solicitado.

As observações recentes são retidas no banco de dados
principal até 48 horas (2 dias) em estações de relatório específicas. Os dados de observação recentes são atualizados continuamente e
substituídos com uma metodologia first-in/first-out (dados rotativos com observações mais recentes e deslocamento das
observações mais antigas para o armazenamento de archive) com base na formatação do
registro de data/hora das observações. A quantidade de dados retidos
e disponíveis a partir de qualquer estação pode ser mais de 24
relatórios de observação individuais. O número de observações é
determinado pelo tipo de observação que ele é.

## Manchetes e detalhes de alerta
{: #alerts_levels}
As APIs de alerta retornam manchetes de alerta meteorológico que estão relacionadas com graves
tempestades, furacões, terremotos e inundações.
Essas APIs também retornam alertas não climáticos, como alertas de rapto de criança e
avisos de aplicação da lei.

**Nota**: essa API está disponível apenas para os Estados Unidos, o Canadá e a Europa.

A API Alert Headlines fornece um valor da chave no atributo `detail_key`
para acessar os detalhes de alerta na API Alert Details.
Consulte a API Alert Headlines para obter o valor `detail_key` e, em seguida, recupere a
resposta da API Alert Details com a `detail_key`.

**Nota**: deve-se exibir a atribuição da origem de dados para qualquer dado de alerta que for exibido em seu aplicativo.

A frase de atribuição deve exibir as informações a seguir:

*Emitido por <Nome do Escritório> - &lt;Código do Distrito do Administrador do Escritório&gt;, &lt;Código do País do Escritório&gt;, &lt;Origem&gt;, &lt;Renúncia de
Responsabilidade&gt;*

Por exemplo:
* Emitido pelo Serviço Nacional de Meteorologia - Bismarck, EUA
* Emitido pelo Instituto Central para Meteorologia e Geodinâmica - Áustria, EMETNET-Meteoalarm

## Informações de Almanaque
{: #almanac_details}
A API Almanac requer um ID de local e tipo de local (cidade ou código de endereçamento postal)
ou um par de latitude e longitude para recuperar as informações para um local específico.

Ao usar `location` na URL, o local deve incluir um ID de local
(código de endereçamento postal) com um tipo de local e um
código do país. Ao usar `geocode` na URL, o local da procura deve ser uma combinação
válida de latitude e longitude.

A API Almanac usa parâmetros para especificar dados diários ou mensais,
uma data específica ou um intervalo de dados de informações e as unidades de medida nas quais retornar os dados.

Os parâmetros de data são `start` e `end`. O parâmetro `start` é um parâmetro necessário,
mas o parâmetro `end` é opcional. Quando os parâmetros são usados em conjunto, a combinação retorna um
intervalo de dados em vez de um mês ou dia de dados específico.

O formato de data para recuperar resultados do Almanaque Diário é um valor numérico de quatro dígitos que representa
o mês e o dia para os dados necessários, ou seja, MMDD. Qualquer dia de dígito
exclusivo **deve** ter um zero (0) antecedente, por exemplo, 01.

O formato de data para recuperar resultados do Almanaque Mensal é mês, ou seja, MM. Qualquer mês de dígito
exclusivo **deve** ter um zero (0) antecedente, por exemplo, 01.  Qualquer outro formato resulta em
um erro de API e nenhum dado será retornado.

**Nota**: se você não fornecer o valor de data na solicitação, o sistema retornará um
status 404 (Solicitação Ruim). A API não fornece um valor padrão.

## construção de URL
{: #url_construction}

As APIs REST usam uma estrutura de URL comum e parâmetros de consulta para solicitar e filtrar dados de clima.
As URLs que são transmitidas para as APIs são construídas
conforme a seguir:

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/<latitude>/<longitude>/<product group>/<date>/<format>&units={units code}&language={language code}
```

Por exemplo:

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/33.40/83.42/forecast/daily/3day.json?units=m&language=en-US
```

|**Atributo**     |**Descrição**                                    |
|------------------|---------------------------------------------------|
|`nome do host`        |O caminho da URL hospedada. Por exemplo, `https://twcservice.mybluemix.net:443/api/weather`.|
|`versão`         |A iteração atual. Por exemplo, "v1".|
|`local
`        |O geocode ou ID de local. O grupo do local pode ser "geocode" ou "local". Por exemplo, "geocode/45.4214/75.6919" representa Ottawa, Canadá. Se uma coordenada de geocódigo for fornecida, a API
retornará dados para o local mais próximo disponível. Os pontos são usados como separadores decimais e as vírgulas são
usadas para separar os valores de latitude e longitude. Se um
geocódigo for fornecido, os valores de latitude e longitude reais
que são usados serão retornados nos metadados da resposta.|
|`grupo de produtos`   |O produto. Por exemplo, "observações" ou "previsão". Um subgrupo de produto, por exemplo, "histórico", é opcional.|
|`data
`            |O tipo de data. Por exemplo, "diário" ou "mensal".|
|`format`          |O formato. Por exemplo, "3day", "5day", "7day" ou "10day".|
|`units`           |As unidades opcionais nas quais retornar a resposta. A API
suporta as unidade de medida English (e), Metric (m) e UK-Hybrid (h). Se o Cliente fornecer as unidades de
medida, mas não fornecer um valor, a API retornará os dados na unidade
de medida que correspondem ao código de idioma. A unidade de medida
padrão ou solicitada é retornada no parâmetro das unidades nos
metadados da resposta.|
|`linguagem`        |O idioma no qual retornar a resposta. O padrão é en-US. O
idioma de tradução padrão ou solicitado é retornado no parâmetro de
idioma nos metadados da resposta.|
*Tabela 2. Detalhes da URL*

**Nota**: as APIs REST usam o padrão ISO 3166 para códigos do país. Para obter informações adicionais, consulte
a [Plataforma On-line de Procura de Padrão ISO](https://www.iso.org/obp/ui/#search/code/){:new_window}.
As APIs usam o sistema de referência de coordenada de geocode WGS84. Para obter informações adicionais, consulte
[Vocabulário Básico de Posição Geográfica](https://www.w3.org/2003/01/geo/){:new_window}.

## Unidades de Medida
{: #units_measure}

Ao usar as APIs REST, não é necessário passar explicitamente uma unidade de medida. As APIs padronizam para a unidade de medida
associada ao código de idioma na URL. No entanto, se você desejar
fornecer uma unidade de medida que é diferente da padrão, será
possível passar em uma unidade de medida que
substitui a padrão.

* Para en-US ou en, o código de unidade de medida padrão é
Inglês/Imperial. O código de unidade é "e".
* Para en-GB, a unidade de medida padrão é Hybrid-UK. O código de unidade é "h".
* Para todo o resto, a unidade de medida padrão é Metric. O código de unidade é "m".

## Tradução de Idioma
{: #language_translation}

As APIs REST traduzem as frases e a unidade de medida. Ao
formatar uma URL de solicitação, deve-se fornecer um idioma válido.
Os campos seguintes são convertidos:

|**Campo**           |**Descrição**                                    |
|--------------------|---------------------------------------------------|
|`narrative`         |A previsão narrativa para o período de 24 horas|
|`dow`               |Dias da semana|
|`wind_phrase`       |A frase que descreve a direção e a velocidade do vento para uma parte do dia de 12 horas|
|`wdir_cardinal`     |Direção média do vento durante o dia em notação cardinal|
|`daypart_name`      |O nome de uma parte do dia de 12 horas, sem incluir os nomes dos dias nas primeiras 48 horas|
|`temp_phrase`       |A frase curta que contém a temperatura alta ou baixa prevista para o período de previsão de 12 horas|
|`shortcast`         |Uma parte abreviada razoável do tempo da previsão narrativa|
|`long_daypart_name` |O prazo nomeado para a previsão climática válida em um formato expandido. O prazo nomeado pode ser para períodos de 12 horas ou 24 horas.|
|`golf_category`     |A categoria de índice de golfe que é expressa como uma frase para as condições climáticas para jogar golfe|
|`phrase_nnchar`     |Frase do clima razoável diurno|
|`lunar_phrase`      |Código curto de três caracteres para fases lunares|
|`uv_desc`           |A descrição do índice UV que complementa o valor de índice UV, fornecendo um nível associado de risco de dano de aparência devido à exposição|
|`wx_phrase`         |Uma descrição de texto das condições climáticas observadas na estação de relatório.|
|`pressure_desc`     |Uma frase que descreve a mudança na leitura de pressão barométrica durante a última hora.|
|`headline_text`     |O texto do título de um evento para o local.|
|`event_desc`        |Uma descrição de um evento.|
|`cntry_name`        |O nome do país no qual um evento ocorreu, especificado em letras maiúsculas e minúsculas.|
*Tabela 3. Campos de resposta traduzidos*

## Manipulando campos de dados nulos ou ausentes na resposta da API
{: #handling_null_or_missing}

Se um campo de dados for nulo porque os dados não estão disponíveis, as APIs REST retornarão as tags do campo apropriado com a palavra "nulo" ou nem retornarão o campo.

## Tratamento de Erros
{: #handling_errors}

Os códigos de erro a seguir são comuns a todas as APIs:

|**Erro** |**Descrição**                                    |
|----------|---------------------------------------------------|
|400       |Solicitação inválida. A solicitação não foi entendida pelo
servidor devido à sintaxe malformada. Esse código de erro é implementado para todas as APIs. A API rejeita a solicitação
se quaisquer parâmetros inválidos forem fornecidos.|
|401       |Desautorizado. A solicitação requer autenticação.|
|403       |Proibido. O servidor entendeu a solicitação mas está se recusando a atendê-la.|
|404       |Não localizado. Se um parâmetro necessário não estiver presente na solicitação da API, um erro MissingParameterException com um código de erro 404 será retornado.|
|500       |Erro do servidor interno. O servidor encontrou uma condição inesperada que o impediu de atender a solicitação.|
*Tabela 4. Código de resposta de erro*

A resposta sobre o erro é sempre a mesma. Vários códigos de
erro podem ser retornados em uma única resposta.
Por exemplo, uma resposta de erro JSON pode ser retornada conforme a
seguir:

```
{
  metadata: {
    transaction_id: "1411496413365:-1880721071"
  },
  success: false,
  errors: [
    {
      error: {
        code: "NDF-0001",
        message: "There was no data found for your product query."
      }
    }
}
```
