---

copyright:
  years: 2015, 2016
lastupdated: "2016-08-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Usando as APIs REST do {{site.data.keyword.weather_short}}
{: #rest_apis}

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
A falha ao inserir credenciais adequadas resulta em uma mensagem *Não autorizado* no corpo da resposta.

Com as APIs REST, é possível recuperar dados de clima fornecendo uma localização geográfica como coordenadas de latitude e longitude.
É possível usar as APIs a seguir.

|**API**                                  |**Descrição**              |
|-----------------------------------------|-----------------------------|
|`GET /v1/{geocode or location ID}/forecast/hourly/48hour.json`  |Retorna a previsão de clima de hora em hora para as próximas 48 horas para uma localização geográfica dependendo do formato que você fornecer. É possível fornecer um `geocode/{latitude}/{longitude}` ou um `location/{locationId}`. Os dados de previsão de hora em hora podem conter até 48 previsões de hora em hora para cada local. Deve-se descartar todas as previsões de hora em hora anteriores para um local quando novos dados forem recebidos.|
|`GET /v1/{geocode or location ID}/forecast/daily/{format}.json`   |Retorna previsões de clima diário para 3, 5, 7 ou 10 dias para uma localização geográfica dependendo do formato que você fornecer. O número de dias a serem retornados é especificado no formato como `3day`, `5day`, `7day` ou `10day`. É possível fornecer um `geocode/{latitude}/{longitude}` ou um `location/{locationId}`. Cada previsão diária pode conter uma previsão diurna, uma previsão noturna e uma previsão de 24 horas. Esses segmentos são objetos separados nas respostas JSON. Os dados de previsão diurna da previsão diária não ficam mais disponíveis depois do horário local de 15h. Às 15h no horário local, seu aplicativo não deverá mais exibir a previsão do dia.|
|`GET /v1/{geocode or location ID}/forecast/intraday/{format}.json`|Retorna previsões de clima diário em períodos de 6 horas para 3, 5, 7 ou 10 dias para uma localização geográfica, dependendo do formato fornecido. O número de dias a serem retornados é especificado no formato como `3day`, `5day`, `7day` ou `10day`. É possível fornecer um `geocode/{latitude}/{longitude}` ou um `location/{locationId}`. Cada previsão diária pode conter uma previsão da manhã, tarde, noite e de durante a noite. Esses segmentos são objetos separados nas respostas JSON.|
|`GET /v1/{geocode or location ID}/observations.json`              |Retorna as condições climáticas atuais de uma localização geográfica. É possível fornecer um `geocode/{latitude}/{longitude}` ou um `location/{locationId}`.  As observações recentes são retidas no banco de dados por até 10 minutos em estações de relatório específicas e 24 horas de observações por estação. Os dados de observação recentes são atualizados continuamente e substituídos com uma metodologia first-in / first-out (dados rotativos com observações mais recentes e deslocamento das observações mais antigas para o armazenamento de archive) com base na formatação do registro de data/hora das observações.|
|`GET /v1/{geocode or location ID}/observations/timeseries.json`   |Retorna as observações atuais e até 24 horas de observações passadas, a partir da data e hora atuais, de uma localização geográfica. É possível fornecer um `geocode/{latitude}/{longitude}` ou um `location/{locationId}`. As observações climáticas são reunidas a partir de dispositivos físicos implementados em todo o mundo e as observações climáticas atuais.|
|`GET /v1/{geocode, country code, state, or area}/alerts.json`      |Retorna observações de clima, avisos, instruções e avisos que são emitidos pelo Serviço Nacional de Meteorologia (NWS), Environment Canada e MeteoAlarm (Europa) e incluem a tradução da descrição do evento, o nome do país e manchetes de alerta em 49 idiomas. É possível fornecer um `geocode/{latitude}/{longitude}`, `country/{countrycode}`, `country/{countrycode}/state/{statecode}`/ ou `country/{countrycode}/area/{areaid}`.|
|`GET /v1/alert/{detail_key}/details.json`                         |Retorna observações de clima, avisos, instruções e avisos que são emitidos pelo Serviço Nacional de Meteorologia (NWS), Environment Canada e MeteoAlarm (Europa). Os detalhes incluem informações detalhadas sobre o alerta emitido pela autoridade de clima do governo para a área especificada e incluem a tradução da descrição do evento, o nome do país e manchetes de alerta em 49 idiomas.|
|`GET /v1/{geocode or postal code}/almanac/daily.json`             |Retorna informações diárias de almanaque (apenas EUA) que são originadas das estações de observações do Serviço Nacional de Meteorologia a partir de um período de medição de 10 a 30 anos ou mais. As informações são reunidas e fornecidas pelo Centro Nacional de Dados Climáticos (NCDC). É possível fornecer um `geocode/{latitude}/{longitude}` ou `location/{PostalLocationId}`.|
|`GET /v1/{geocode or postal code}/almanac/monthly.json`           |Retorna informações mensais de almanaque (apenas EUA) que são originadas das estações de observações do Serviço Nacional de Meteorologia a partir de um período de medição de 10 a 30 anos ou mais. As informações são reunidas e fornecidas pelo Centro Nacional de Dados Climáticos (NCDC). É possível fornecer um `geocode/{latitude}/{longitude}` ou `location/{PostalLocationId}`.|
|`GET /v3/location/{search or point}`                                  |Fornece a capacidade de procurar um nome ou uma localização geográfica do local (latitude e longitude) para recuperar um conjunto de locais que correspondem à solicitação. O Serviço de Localização suporta procura por nome da cidade ou código de endereçamento postal.|
*Tabela 1. Resumo da API do {{site.data.keyword.weather_short}}*

## Previsões diárias e intradiárias
{: #daily_intraday}
A API de previsão diária pode conter múltiplos dias ou previsões diárias para cada local.
Cada dia de uma previsão pode conter até três previsões separadas. Para qualquer
dia de previsão, a API pode retornar previsões de dia, noite e de 24 horas.

A API de previsão intradiária pode conter múltiplos dias ou previsões diárias para cada local.
Cada dia de uma previsão contém quatro previsões de 6 horas separadas para a manhã (das 7h às 13h),
a tarde (das 13h às 19h), a noite (das 19h à 1h) e durante a noite (da 1h às 7h). A
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

As condições atuais e os dados de observações de clima de série temporal fornecem informações sobre temperatura,
precipitação, ventos, pressão barométrica, visibilidade, radiação ultravioleta (UV)
e outros elementos de observação relacionados, incluindo estação de observação,
data e hora da observação, códigos de ícone e frases de clima. A diferença entre
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
único **deve** ter um zero antecedente, por exemplo, 01.

O formato de data para recuperar resultados do Almanaque Mensal é mês, ou seja, MM. Qualquer mês de dígito
único **deve** ter um zero antecedente, por exemplo, 01. Qualquer outro formato resulta em
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
|`versão`         |A iteração atual. Por exemplo, `v1`.|
|`local`        |O geocode ou ID de local. O grupo do local pode ser `geocode` ou `location`. Por exemplo, `geocode/45.4214/75.6919` representa Ottawa, Canadá. Se uma coordenada de geocódigo for fornecida, a API retornará dados para o local mais próximo disponível. Os pontos são usados como separadores decimais e as vírgulas são usadas para separar os valores de latitude e longitude. Se um geocódigo for fornecido, os valores de latitude e longitude reais que são usados serão retornados nos metadados da resposta.|
|`grupo de produtos`   |O produto. Por exemplo, `observations` ou `forecast`. Um subgrupo do produto, por exemplo, `historical`, é opcional.|
|`data`            |O tipo de data. Por exemplo, `daily` ou `monthly`.|
|`format`          |O formato. Por exemplo, `3day`, `5day`, `7day` ou `10day`.|
|`units`           |As unidades opcionais nas quais retornar a resposta. A API suporta as unidade de medida English (e), Metric (m) e UK-Hybrid (h). Se o Cliente fornecer as unidades de medida, mas não fornecer um valor, a API retornará os dados na unidade de medida que correspondem ao código de idioma. A unidade de medida padrão ou solicitada é retornada no parâmetro das unidades nos metadados da resposta.|
|`linguagem`        |O idioma no qual retornar a resposta. O padrão é en-US. O idioma de tradução padrão ou solicitado é retornado no parâmetro de idioma nos metadados da resposta.|
*Tabela 2. Detalhes da URL*

**Nota**: as APIs REST usam o padrão ISO 3166 para códigos do país. Para obter informações adicionais, consulte
a [Plataforma On-line de Procura de Padrão ISO](https://www.iso.org/obp/ui/#search/code/){:new_window}.
As APIs usam o sistema de referência de coordenada de geocode WGS84. Para obter informações adicionais, consulte
[Vocabulário Básico de Posição Geográfica](https://www.w3.org/2003/01/geo/){:new_window}.

## Códigos e imagens de ícones
{: #icon_code_images}

Quando as APIs REST do {{site.data.keyword.weather_short}} retornam um código de ícone na resposta,
é possível utilizá-lo para determinar qual imagem de ícone exibir no app.
Há um relacionamento de um para um entre o código do ícone na resposta da API e o nome do arquivo da imagem do ícone.
Por exemplo, se a resposta da API contiver um `icon_code` de 1, será possível usar o nome de arquivo `01.png`
para exibir a imagem de ícone correspondente.

No código, é possível criar uma função que usa o `icon_code` para determinar
a URL da imagem do ícone. Por exemplo:

```
function getIconURL(code) {
    return "images/weathericons/icon" + code + ".png";
}
```

A tabela a seguir contém códigos de ícone, descrições e imagens que podem ser usadas
com as APIs REST do {{site.data.keyword.weather_short}}. A tabela indica se um ícone
será usado nas APIs de Previsão ou Observação e se o ícone estará disponível nas partes de previsão
Noturna ou Diurna.

|**Código**|**Descrição**|**Imagem**|**Uso da API** |**Noturna ou Diurna**|
|----|--------------------------|------------|------------|--------------------|
| 0  | Tornado                  | <img src="images/00.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão                | Noite e Dia |
| 1  | Tempestade tropical           | <img src="images/01.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 2  | Hurricane                | <img src="images/02.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão                | Noite e Dia |
| 3  | Tempestades fortes            | <img src="images/03.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão                | Noite e Dia |
| 4  | Trovão e granizo         | <img src="images/04.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 5  | Pancadas de chuva e neve     | <img src="images/05.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 6  | Chuva/Chuva com neve             | <img src="images/06.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 7  | Combinação de neve/Chuva com neve gelada  | <img src="images/07.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 8  | Garoa congelada         | <img src="images/08.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 9  | Garoa                  | <img src="images/09.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 10 | Chuva de Granizo            | <img src="images/10.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 11 | Chuva fraca               | <img src="images/11.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 12 | Chuva                     | <img src="images/12.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 13 | Ondas esparsas       | <img src="images/13.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 14 | Neve fraca               | <img src="images/14.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 15 | Ventos fortes/Neve oscilante  | <img src="images/15.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 16 | Neve                     | <img src="images/16.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 17 | Granizo                     | <img src="images/17.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 18 | Granizo                    | <img src="images/18.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 19 | Vento de areia/Tempestade de areia | <img src="images/19.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 20 | Nevoeiro                    | <img src="images/20.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 21 | Névoa seca/Ventania             | <img src="images/21.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 22 | Fumaça/Ventania            | <img src="images/22.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 23 | Brisa forte                   | <img src="images/23.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão                | Noite e Dia |
| 24 | Rajada de vento/Ventania    | <img src="images/24.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 25 | Frio glacial/Cristais de gelo    | <img src="images/25.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 26 | Cloudy                   | <img src="images/26.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 27 | Nublado na Maior Parte            | <img src="images/27.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 28 | Nublado na Maior Parte            | <img src="images/28.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Dia         |
| 29 | Parcialmente Nublado            | <img src="images/29.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite       |
| 30 | Parcialmente Nublado            | <img src="images/30.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Dia         |
| 31 | Clear                    | <img src="images/31.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite       |
| 32 | Ensolarado                    | <img src="images/32.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Dia         |
| 33 | Melhora/Limpo na maior parte      | <img src="images/33.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite       |
| 34 | Melhora/Ensolarado na maior parte      | <img src="images/34.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Dia         |
| 35 | Combinação de chuva e granizo        | <img src="images/35.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão                | Dia         |
| 36 | Hot                      | <img src="images/36.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão                | Dia         |
| 37 | Tempestades com trovoadas isoladas   | <img src="images/37.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão                | Dia         |
| 38 | Temporais com Relâmpago e Trovão            | <img src="images/38.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 39 | Pancadas esparsas        | <img src="images/39.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão                | Dia          |
| 40 | Chuva Pesada               | <img src="images/40.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 41 | Pancadas de neve esparsas   | <img src="images/41.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão                | Dia         |
| 42 | Neve pesada               | <img src="images/42.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
| 43 | Nevasca                 | <img src="images/43.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão                | Noite e Dia |
| 44 | Not Available (N/A)      | <img src="images/44.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão                | Noite e Dia |
| 45 | Pancadas esparsas        | <img src="images/45.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão                | Noite       |
| 46 | Pancadas de neve esparsas   | <img src="images/46.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão                | Noite       |
| 47 | Tempestades com trovoadas esparsas  | <img src="images/47.png " width="100" height="100" alt="Imagem do ícone."/>| Previsão e Observações | Noite e Dia |
*Tabela 3. Códigos e imagens de ícones*

É possível fazer download desse conjunto de ícones de clima como [PNGs](https://twcdocs.mybluemix.net/download/weather_icons_200x200_png.zip){:new_window}
ou [SVGs](https://twcdocs.mybluemix.net/download/weather_icons_200x200_svg.zip){:new_window} e utilizá-los em seu app. 

Também é possível fazer download do [conjunto de ícones](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window} usado
pelo [app demo do {{site.data.keyword.weather_short}}](http://weather-company-data-demo.{APPDomain}){: new_window}.

## Unidades de Medida
{: #units_measure}

Ao usar as APIs REST, não é necessário passar explicitamente uma unidade de medida. As APIs padronizam para a unidade de medida
associada ao código de idioma na URL. No entanto, se você desejar
fornecer uma unidade de medida que é diferente da padrão, será
possível passar em uma unidade de medida que
substitui a padrão.

* Para en-US ou en, o código de unidade de medida padrão é
Inglês/Imperial. O código de unidade é `e`.
* Para en-GB, a unidade de medida padrão é Hybrid-UK. O código de unidade é `h`.
* Para todo o resto, a unidade de medida padrão é Metric. O código de unidade é `m`.

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
*Tabela 4. Campos de resposta traduzidos*

## Manipulando campos de dados nulos ou ausentes na resposta da API
{: #handling_null_or_missing}

Se um campo de dados for nulo porque os dados não estão disponíveis, as APIs REST retornarão as tags de campo apropriadas com a palavra `null` ou nem retornarão o campo.

## Tratamento de Erros
{: #handling_errors}

Os códigos de erro a seguir são comuns a todas as APIs:

|**Erro** |**Descrição**                                    |
|----------|---------------------------------------------------|
|400       |Solicitação inválida. A solicitação não foi entendida pelo servidor devido à sintaxe malformada. Esse código de erro é implementado para todas as APIs. A API rejeita a solicitação se quaisquer parâmetros inválidos forem fornecidos.|
|401       |Desautorizado. A solicitação requer autenticação.|
|403       |Proibido. O servidor entendeu a solicitação mas está se recusando a atendê-la.|
|404       |Não localizado. Se um parâmetro necessário não estiver presente na solicitação da API, um erro MissingParameterException com um código de erro 404 será retornado.|
|500       |Erro do servidor interno. O servidor encontrou uma condição inesperada que o impediu de atender a solicitação.|
*Tabela 5. Código de resposta de erro*

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
