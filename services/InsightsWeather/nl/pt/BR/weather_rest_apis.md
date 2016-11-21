---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Usando as APIs REST do Insights for Weather
{: #rest_apis}

É possível usar as [APIs REST do Insights for Weather](https://twcservice.{APPDomain}/rest-api-deprecated/){:new_window}
para recuperar dados de clima. É possível testar operações de API e visualizar instantaneamente os resultados para ajudar a construir seus aplicativos mais rapidamente.

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

Com as APIs do Insights for Weather, é possível recuperar dados de clima fornecendo uma localização geográfica como coordenadas de latitude e longitude.
É possível usar as APIs a seguir.

|**API**                                  |**Descrição**              |
|-----------------------------------------|-----------------------------|
|`GET /v2/forecast/daily/10day`           |Retorna previsões climáticas para o dia atual e para os próximos nove dias de uma localização geográfica. Cada previsão diária pode conter uma previsão diurna e uma previsão noturna. Esses segmentos são objetos separados nas respostas JSON. Os dados de previsão diurna da previsão diária não ficam mais disponíveis depois do horário local de 15h. Às 15h, horário local, seu aplicativo não deverá mais exibir a previsão do dia.|
|`GET /v2/forecast/hourly/24hour`         |Retorna previsões de hora em hora para o dia atual e para as próximas 24 horas de uma localização geográfica. Os dados de previsão de hora em hora podem conter até 24 previsões de hora em hora para cada local. Deve-se descartar todas as previsões de hora em hora anteriores de um local quando novos dados são recebidos|
|`GET /v2/observations/current`           |Retorna as condições climáticas atuais de uma localização geográfica. As observações recentes são retidas no banco de dados por até 10 minutos em estações de relatório específicas e 24 horas de observações por estação. Os dados de observação recentes são atualizados continuamente e substituídos com uma metodologia first-in / first-out (dados rotativos com observações mais recentes e deslocamento das observações mais antigas para o armazenamento de archive) com base na formatação do registro de data/hora das observações.|
|`GET /v2/observations/timeseries/24hour` |Retorna as observações atuais e até 24 horas de observações passadas, a partir da data e hora atuais, de uma localização geográfica. As observações climáticas são reunidas a partir e dispositivos físicos implementados em todo o mundo e as observações climáticas tuais.|
*Tabela 1. Resumo da API do Insights for Weather*

## Observações de série temporal
{: #time_series}

Os dados de observações climáticas série temporal fornecem
informações sobre temperatura, precipitação, vento, pressão barométrica, visibilidade,
radiação ultravioleta (UV) e outros elementos de observação
relacionadas, incluindo estação de observação, data/hora de
observação, códigos de ícone de clima e frases. A diferença entre
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

## construção de URL
{: #url_construction}

As APIs do Insights for Weather usam uma estrutura de URL comum e parâmetros de consulta para solicitar e filtrar dados de clima.
As URLs que são passadas para as APIs do Insights for Weather são construídas conforme a seguir:

```
https://twcservice.mybluemix.net/api/weather/v2/<product group>/&format={format type}&geocode={latitude,longitude}&language={language code}&units={units code}

```

|**Atributo**     |**Descrição**                                    |
|------------------|---------------------------------------------------|
|`nome do host`        |O caminho da URL hospedada (por exemplo, `https://twcservice.mybluemix.net:443/api/weather`)|
|`versão`         |A iteração atual (por exemplo, "v2")|
|`grupo de produtos`   |O produto (por exemplo, "observations" ou "forecast")|
|`geocódigo`         |A latitude e longitude opcionais, por exemplo, "45.4214,75.6919" representa Ottawa, Canadá. Se uma coordenada de geocódigo for fornecida, a API retornará dados para o local mais próximo disponível. Os pontos são usados como separadores decimais e as vírgulas são usadas para separar os valores de latitude e longitude. Se um geocódigo for fornecido, os valores de latitude e longitude reais que são usados serão retornados nos metadados da resposta.|
|`linguagem`        |O idioma no qual retornar a resposta. O padrão é en-US. O idioma de tradução padrão ou solicitado é retornado no parâmetro de idioma nos metadados da resposta.|
|`units`           |As unidades opcionais nas quais retornar a resposta. A API suporta as unidade de medida English (e), Metric (m) e UK-Hybrid (h). Se o Cliente fornecer as unidades de medida, mas não fornecer um valor, a API retornará os dados na unidade de medida que correspondem ao código de idioma. A unidade de medida padrão ou solicitada é retornada no parâmetro das unidades nos metadados da resposta.|
*Tabela 2. Detalhes da URL*

## Unidades de Medida
{: #units_measure}

Ao usar as APIs do Insights for Weather, não é necessário passar explicitamente uma unidade de medida. As APIs do Insights for Weather são padronizadas com a unidade de medida associada ao código de idioma na URL. No entanto, se você desejar
fornecer uma unidade de medida que é diferente da padrão, será
possível passar em uma unidade de medida que
substitui a padrão.

* Para en-US ou en, o código de unidade de medida padrão é
Inglês/Imperial. O código de unidade é "e".
* Para en-GB, a unidade de medida padrão é Hybrid-UK. O código de unidade é "h".
* Para todo o resto, a unidade de medida padrão é Metric. O código de unidade é "m".

## Tradução de Idioma
{: #language_translation}

As APIs do Insights for Weather traduzem as frases e a unidade de medida. Ao
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
|`sky_cover`         | Cobertura de pele descritiva baseada na porcentagem de cobertura de nuvem|
|`ptend_desc`        | Texto descritivo da tendência de pressão nas últimas 3 horas|
*Tabela 3. Campos de resposta traduzidos*

## Manipulando campos de dados nulos ou ausentes na resposta da API
{: #handling_null_or_missing}

Se um campo de dados for nulo porque os dados não estão disponíveis, as APIs do Insights for Weather retornarão as tags do campo apropriado com a palavra "nulo" ou nem retornarão o campo.

## Tratamento de Erros
{: #handling_errors}

Os códigos de erro a seguir são comuns a todas as APIs:

|**Erro** |**Descrição**                                    |
|----------|---------------------------------------------------|
|400       |Solicitação inválida. A solicitação não foi entendida pelo servidor devido à sintaxe malformada. Esse código de erro é implementado para todas as APIs. A API rejeita a solicitação se quaisquer parâmetros inválidos forem fornecidos.|
|401       |Desautorizado. A solicitação requer autenticação.|
|403       |Proibido. O servidor entendeu a solicitação mas está se recusando a atendê-la.|
|404       |Não localizado. Se um parâmetro necessário não estiver presente na solicitação da API, um erro MissingParameterException com um código de erro 404 será retornado.|
|405       |Método Não Permitido. Por exemplo, enviar um POST, em vez deum GET.|
|406       |Não aceitável. Por exemplo, não aceitar as respostas compactadas gzip.|
|408       |Tempo limite da solicitação. O cliente não produziu a solicitação dentro do tempo que o servidor estava disposto a esperar.|
|500       |Erro do servidor interno. O servidor encontrou uma condição inesperada que o impediu de atender a solicitação.|
|502-504   |Problema de Serviço ou Gateway Indisponível. Esses códigos de erro são retornados se o serviço estiver temporariamente indisponível.|
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
