---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Usando serviços ativados pelo {{site.data.keyword.openwhisk_short}} 
{: #openwhisk_ecosystem}
*Última atualização: 28 de março de 2016*
{: .last-updated}

No {{site.data.keyword.openwhisk}}, um catálogo de pacotes fornece uma maneira fácil de aprimorar seu app com recursos úteis e de acessar serviços externos no ecossistema. Exemplos de serviços externos que são ativados pelo {{site.data.keyword.openwhisk_short}} incluem Cloudant, The Weather Company, Slack e GitHub.
{: shortdesc}

O catálogo está disponível como pacotes no namespace `/whisk.system`. Consulte [Procurando em pacotes](./openwhisk_packages.html#openwhisk_packagedisplay) para obter informações sobre como procurar no catálogo usando a ferramenta de linha de comandos.

Os tópicos a seguir documentam alguns dos pacotes no catálogo.

## Usando o pacote Cloudant
{: #openwhisk_catalog_cloudant}
O pacote `/whisk.system/cloudant` permite trabalhar com um banco de dados do Cloudant. Ele inclui as ações e os feeds a seguir.

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | pacote | {{site.data.keyword.Bluemix_notm}}ServiceName, host, username, password, dbname, includeDoc, overwrite | Trabalhar com um banco de dados do Cloudant |
| `/whisk.system/cloudant/read` | ação | dbname, includeDoc, id | Ler um documento a partir de um banco de dados |
| `/whisk.system/cloudant/write` | ação | dbname, overwrite, doc | Gravar um documento em um banco de dados |
| `/whisk.system/cloudant/changes` | alimentação | dbname, includeDoc, maxTriggers | Disparar eventos acionadores nas mudanças em um banco de dados |

Os tópicos a seguir percorrem a configuração de um banco de dados do Cloudant, a configuração de um pacote associado e o uso de ações e feeds no pacote `/whisk.system/cloudant`.

### Configurando um banco de dados do Cloudant no {{site.data.keyword.Bluemix_notm}}

Se você está usando o {{site.data.keyword.openwhisk_short}} a partir do {{site.data.keyword.Bluemix}}, o {{site.data.keyword.openwhisk_short}} cria automaticamente ligações de pacote para suas instâncias de serviço do {{site.data.keyword.Bluemix_notm}} Cloudant. Se não estiver usando o {{site.data.keyword.openwhisk_short}} e o Cloudant a partir do {{site.data.keyword.Bluemix_notm}}, vá para a próxima etapa.

1. Crie uma instância de serviço do Cloudant em seu [painel](http://console.ng.{{site.data.keyword.Bluemix_notm}}.net) do {{site.data.keyword.Bluemix_notm}}.

  Certifique-se de lembrar do nome da instância de serviço e da organização e do espaço do {{site.data.keyword.Bluemix_notm}} no qual você se encontra.

2. Certifique-se de sua CLI do {{site.data.keyword.openwhisk_short}} esteja no namespace correspondente à organização e ao espaço do {{site.data.keyword.Bluemix_notm}} usados na etapa anterior.

  ```
  wsk property set --namespace my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space
  ```
  {: pre}

  Como alternativa, é possível usar `wsk property set --namespace` para configurar um namespace a partir de uma lista daqueles disponíveis para você.

3. Atualize os pacotes em seu namespace. A atualização cria automaticamente um pacote de ligação para a instância de serviço do Cloudant criada.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  {{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1 private binding
  ```
  {: screen}

  É necessário ver o nome completo da ligação do pacote que corresponde à sua instância de serviço do {{site.data.keyword.Bluemix_notm}} Cloudant.

4. Verifique se a ligação do pacote criada anteriormente está configurado com seu host e credenciais da instância de serviço do {{site.data.keyword.Bluemix_notm}} Cloudant.

  ```
  wsk package get /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: pre}
  ```
  ok: got package /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1, projecting parameters
  [
      ...
      {
          "key": "username",
          "value": "cdb18832-2bbb-4df2-b7b1-{{site.data.keyword.Bluemix_notm}}"
      },
      {
          "key": "host",
          "value": "cdb18832-2bbb-4df2-b7b1-{{site.data.keyword.Bluemix_notm}}.cloudant.com"
      },
      {
          "key": "password",
          "value": "c9088667484a9ac827daf8884972737"
      }
      ...
  ]
  ```
  {: screen}

### Configurando um banco de dados do Cloudant fora do {{site.data.keyword.Bluemix_notm}}

Se não estiver usando o {{site.data.keyword.openwhisk_short}} no {{site.data.keyword.Bluemix_notm}} ou se desejar configurar seu banco de dados do Cloudant fora do {{site.data.keyword.Bluemix_notm}}, deverá criar manualmente uma ligação de pacote para sua conta do Cloudant. Você precisa do nome do host, do nome do usuário e da senha da conta do Cloudant.

1. Crie uma ligação do pacote configurada para sua conta do Cloudant.

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username 'MYUSERNAME' -p password 'MYPASSWORD' -p host 'MYCLOUDANTACCOUNT.cloudant.com'
  ```
  {: pre}

2. Verifique se a ligação do pacote existe.

  ```
  wsk package list
  ```
  {: pre}
  ```
  pacotes
  /myNamespace/myCloudant private binding
  ```
  {: screen}


### Recebendo mudanças em um banco de dados do Cloudant

É possível usar o feed `changes` para configurar um serviço para disparar um acionador em cada mudança em seu banco de dados do Cloudant. Os parâmetros são como segue:

- `dbname`: nome do banco de dados do Cloudant.
- `includeDoc`: se configurado como verdadeiro, cada evento acionador disparado incluirá o documento do Cloudant modificado. 
- `maxTriggers`: parar de disparar acionadores quando esse limite for atingido. O padrão é 1000. É possível configurá-lo para o máximo de 10.000. Se você tentar configurar mais de
10.000, a solicitação será rejeitada.

1. Crie um acionador com o feed `changes` na ligação do pacote criada anteriormente. Certifique-se de substituir `/myNamespace/myCloudant` pelo nome de seu pacote.

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb --param includeDoc true
  ```
  {: pre}
  ```
  ok: feed do acionador myCloudantTrigger criado
  ```
  {: screen}

2. Pesquisa de ativações.

  ```
  wsk activation poll
  ```
  {: pre}

3. Em seu painel do Cloudant, modifique um documento existente ou crie um novo.

4. Observe novas ativações para o acionador `myCloudantTrigger` para cada mudança no documento.

**Nota**: se você não for capaz de observar novas ativações, consulte as seções subsequentes sobre leitura e gravação em um banco de dados do Cloudant. O teste das etapas de leitura e gravação abaixo ajudará a verificar se suas credenciais do Cloudant estão corretas.

Agora, é possível criar regras e associá-las a ações para reagir às atualizações do documento.

O conteúdo dos eventos gerados depende do valor do parâmetro `includeDoc` ao criar o acionador. Se configurado para true, cada evento acionador disparado incluirá o documento do Cloudant modificado. Por exemplo, considere o documento modificado a seguir:

  ```
  {
    "_id": "6ca436c44074c4c2aa6a40c9a188b348",
    "_rev": "3-bc4960fc13aa368afca8c8427a1c18a8",
    "name": "Heisenberg"
  }
  ```
  {: screen}

O código neste exemplo gera um evento de acionador com os parâmetros `_id`, `_rev` e `name` correspondentes. Na verdade, a representação JSON do evento acionador é idêntica ao documento.

Caso contrário, se `includeDoc` for falso, os eventos incluirão os parâmetros a seguir:

- `id`: o ID do documento.
- `seq`: o identificador de sequência gerado pelo Cloudant.
- `changes`: uma matriz de objetos, cada um dos quais tendo um campo `rev` que contém o ID da revisão do documento.

A representação JSON do evento acionador é a seguinte:

  ```
  {
      "id": "6ca436c44074c4c2aa6a40c9a188b348",
      "seq": "2-g1AAAAL9aJyV-GJCaEuqx4-BktQkYp_dmIfC",
      "changes": [
          {
              "rev": "2-da3f80848a480379486fb4a2ad98fa16"
          }
      ]
  }
  ```


### Gravando em um banco de dados do Cloudant

É possível usar uma ação para armazenar um documento em um banco de dados do Cloudant denominado `testdb`. Certifique-se de que esse banco de dados exista em sua conta do Cloudant.

1. Armazene um documento usando a ação `write` na ligação do pacote anteriormente criada. Certifique-se de substituir `/myNamespace/myCloudant` pelo nome de seu pacote.

  ```
  wsk action invoke /myNamespace/myCoudant/write --blocking --result --param dbname testdb --param doc '{"_id":"heisenberg", "name":"Walter White"}'
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCoudant/write with id 62bf696b38464fd1bcaff216a68b8287
  {
    "id": "heisenberg",
    "ok": true,
    "rev": "1-9a94fb93abc88d8863781a248f63c8c3"
  }
  ```
  {: screen}

2. Verifique se o documento existe procurando-o em seu painel do Cloudant.

  A URL do painel para o banco de dados `testdb` é semelhante à seguinte: `https://MYCLOUDANTACCOUNT.cloudant.com/dashboard.html#database/testdb/_all_docs?limit=100`.


### Lendo de um banco de dados do Cloudant

É possível usar uma ação para buscar um documento a partir de um banco de dados do Cloudant chamado `testdb`. Certifique-se de que esse banco de dados exista em sua conta do Cloudant.

1. Busque um documento usando a ação `read` na ligação do pacote anteriormente criada. Certifique-se de substituir `/myNamespace/myCloudant` pelo nome de seu pacote.

  ```
  wsk action invoke /myNamespace/myCoudant/read --blocking --result --param dbname testdb --param id heisenberg
  ```
  {: pre}
  ```
  {
    "_id": "heisenberg",
    "_rev": "1-9a94fb93abc88d8863781a248f63c8c3"
    "name": "Walter White"
  }
  ```
  {: screen}


## Usando o pacote Alarme
{: #openwhisk_catalog_alarm}

O pacote `/whisk.system/alarms` pode ser usado para disparar um acionador a uma frequência especificada. Isso é útil para configurar tarefas ou trabalhos recorrentes, como chamar uma ação de backup do sistema a cada hora.

O pacote inclui o feed a seguir.

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | pacote | - | Alarmes e utilitário periódico |
| `/whisk.system/alarms/alarm` | alimentação | cron, trigger_payload, maxTriggers | Disparar evento acionador periodicamente |


### Disparando um evento acionador periodicamente

O feed `/whisk.system/alarms/alarm` configura o serviço de Alarme para disparar um evento acionador a uma frequência especificada. Os parâmetros são como segue:

- `cron`: Uma sequência, baseada na sintaxe Unix crontab, que indica quando disparar o acionador na Hora Universal Coordenada (UTC). A sequência é composta por seus campos separados por espaços: `X X X X X X`. Para obter mais detalhes sobre como usar a sintaxe cron, veja: https://github.com/ncb000gt/node-cron. Aqui estão alguns exemplos de frequência indicada pela sequência:

  - `* * * * * *`: a cada segundo.
  - `0 * * * * *`: início de cada minuto.
  - `* 0 * * * *`: início de cada hora.
  - `0 0 9 8 * *`: às 9h (UTC) no oitavo dia de cada mês

- `trigger_payload`: o valor desse parâmetro torna-se o conteúdo do acionador toda vez que o acionador for disparado.

- `maxTriggers`: parar de disparar acionadores quando esse limite for atingido. O padrão é 1000. É possível configurá-lo para o máximo de 10.000. Se você tentar configurar mais de
10.000, a solicitação será rejeitada.

Aqui está um exemplo de criação de um acionador que será disparado uma vez a cada 20 segundos com os valores de `name` e `place` no evento acionador.

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron '*/20 * * * * *' --param trigger_payload '{"name":"Odin","place":"Asgard"}'
  ```
  {: pre}

Cada evento gerado incluirá como parâmetros as propriedades especificadas no valor de `trigger_payload`. Neste caso, cada evento acionador terá os parâmetros `name=Odin` e `place=Asgard`.


## Usando o pacote Clima
{: #openwhisk_catalog_weather}

O pacote `/whisk.system/weather` oferece uma maneira conveniente de chamar a API do IBM Weather Insights.

O pacote inclui a ação a seguir.

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/weather` | pacote | apiKey | Serviços a partir da API do IBM Weather Insights  |
| `/whisk.system/weather/forecast` | ação | apiKey, latitude, longitude, timePeriod | previsão para o período especificado|

Embora não seja obrigatório, é recomendável criar uma ligação de pacote com o valor de `apiKey`. Dessa forma, não será necessário especificar a chave toda vez que você chamar as ações no pacote.

### Obtendo uma previsão de tempo para um local

A ação `/whisk.system/weather/forecast` retorna uma previsão do tempo para um local, chamando uma API a partir da The Weather Company. Os parâmetros são como segue:

- `apiKey`: uma chave de API para a The Weather Company que é autorizada a chamar a API de previsão.
- `latitude`: a coordenada de latitude do local.
- `longitude`: a coordenadas de longitude do local.
- `timeperiod`: período para a previsão. As opções válidas são '10day' - (padrão) Retorna uma previsão diária de 10 dias, '24hour' - Retorna uma previsão de 2 dias a cada hora, 'atual' - Retorna as condições meteorológicas atuais, 'timeseries' - Retorna as observações atuais e até 24 horas de observações passadas, a partir da data e hora atuais. 


Aqui está um exemplo de criação de uma ligação de pacote e, em seguida, a obtenção de uma previsão do tempo de 10 dias.

1. Crie uma ligação de pacote com sua chave da API.

  ```
  wsk package bind /whisk.system/weather myWeather --param apiKey 'MY_WEATHER_API'
  ```
  {: pre}

2. Chame a ação `forecast` em sua ligação do pacote para obter a previsão do tempo.

  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude '43.7' --param longitude '-79.4'
  ```
  {: pre}

  ```
  {
      "forecasts": [
          {
              "dow": "Wednesday",
              "max_temp": -1,
              "min_temp": -16,
              "narrative": "Chance of a few snow showers. Highs -2 to 0C and lows -17 to -15C.",
              ...
          },
          {
              "class": "fod_long_range_daily",
              "dow": "Thursday",
              "max_temp": -4,
              "min_temp": -8,
              "narrative": "Mostly sunny. Highs -5 to -3C and lows -9 to -7C.",
              ...
          },
          ...
      ],
  }
  ```
  {: screen}


## Usando o pacote Watson
{: #openwhisk_catalog_watson}

O pacote `/whisk.system/watson` oferece uma maneira conveniente para chamar várias APIs do Watson.

O pacote inclui as ações a seguir.

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/watson` | pacote | username, password | Ações para as APIs do Watson Analytics |
| `/whisk.system/watson/translate` | ação | translateFrom, translateTo, translateParam, username, password | Traduzir texto |
| `/whisk.system/watson/languageId` | ação | payload, username, password | Identificar idioma |
| `/whisk.system/watson/speechToText` | ação | payload, content_type, encoding, username, password, continuous, inactivity_timeout, interim_results, keywords, keywords_threshold, max_alternatives, model, timestamps, watson-token, word_alternatives_threshold, word_confidence, X-Watson-Learning-Opt-Out | Converter
áudio em texto |
| `/whisk.system/watson/textToSpeech` | ação | payload, voice, accept, encoding, username, password | Converter texto em áudio |

Embora não seja obrigatório, é recomendável criar uma ligação de pacote com os valores de `username` e `password`. Dessa forma, não será necessário especificar essas credenciais toda vez que chamar as ações no pacote.

### Traduzindo texto

A ação `/whisk.system/watson/translate` traduz texto de um idioma para outro. Os parâmetros são como segue:

- `username`: o nome do usuário da API do Watson.
- `password`: a senha da API do Watson.
- `translateParam`: o parâmetro de entrada a ser traduzido. Por exemplo, se `translateParam=payload`, então, o valor do parâmetro `payload` passado à ação será traduzido.
- `translateFrom`: um código de dois dígitos do idioma de origem.
- `translateTo`: um código de dois dígitos do idioma de destino.

A seguir está um exemplo de criação de uma ligação de pacote e tradução de algum texto.

1. Crie uma ligação de pacote com suas credenciais do Watson.

  ```
  wsk package bind /whisk.system/watson myWatson --param username 'MY_WATSON_USERNAME' --param password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. Chame a ação `translate` em sua ligação do pacote para traduzir algum texto do inglês para o francês.

  ```
  wsk action invoke myWatson/translate --blocking --result --param payload 'Blue skies ahead' --param translateParam 'payload' --param translateFrom 'en' --param translateTo 'fr'
  ```
  {: pre}

  ```
  {
      "payload": "Ciel bleu a venir"
  }
  ```
  {: screen}


### Identificando o idioma de algum texto

A ação `/whisk.system/watson/languageId` identifica o idioma de algum texto. Os parâmetros são como segue:

- `username`: o nome do usuário da API do Watson.
- `password`: a senha da API do Watson.
- `payload`: o texto para identificar.

Aqui está um exemplo de criação de uma ligação de pacote e identificação do idioma de algum texto.

1. Crie uma ligação de pacote com suas credenciais do Watson.

  ```
  wsk package bind /whisk.system/watson myWatson -p username 'MY_WATSON_USERNAME' -p password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. Chame a ação `languageId` em sua ligação do pacote para identificar o idioma.

  ```
  wsk action invoke myWatson/languageId --blocking --result --param payload 'Ciel bleu a venir'
  ```
  {: pre}
  ```
  {
    "payload": "Ciel bleu a venir",
    "language": "fr",
    "confidence": 0.710906
  }
  ```
  {: screen}


### Converter algum texto para fala

A ação `/whisk.system/watson/textToSpeech` converte algum texto para uma fala de áudio. Os parâmetros são como segue:

- `username`: o nome do usuário da API do Watson.
- `password`: a senha da API do Watson.
- `payload`: o texto para converter em fala.
- `voice`: a voz do orador.
- `accept`: o formato do arquivo de fala.
- `encoding`: a codificação dos dados binários de fala.

Aqui está um exemplo de criação de uma ligação de pacote e de conversão de algum texto para fala.

1. Crie uma ligação de pacote com suas credenciais do Watson.

  ```
  wsk package bind /whisk.system/watson myWatson -p username 'MY_WATSON_USERNAME' -p password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. Chame a ação `textToSpeech` em sua ligação do pacote para converter o texto.

  ```
  wsk action invoke myWatson/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```
  {
    "payload": "<base64 encoding of a .wav file>"
  }
  ```
  {: screen}


### Convertendo fala para texto

A ação `/whisk.system/watson/speechToText` converte fala de áudio para texto. Os parâmetros são como segue:

- `username`: o nome do usuário da API do Watson.
- `password`: a senha da API do Watson.
- `payload`: os dados binários de fala codificados para transformar em texto.
- `content_type`: o tipo MIME do áudio.
- `encoding`: a codificação dos dados binários de fala.
- `continuous`: indica se múltiplos resultados finais que representam frases consecutivas separadas por pausas longas são retornados.
- `inactivity_timeout`: o tempo em segundos após o qual, se apenas o silêncio for detectado no áudio enviado, a conexão será fechada.
- `interim_results`: indica se o serviço deve retornar resultados provisórios.
- `keywords`: uma lista de palavras-chave para detectar no áudio.
- `keywords_threshold`: um valor de confiança que é o limite inferior para detectar uma palavra-chave.
- `max_alternatives`: o número máximo de transcrições alternativas a serem retornadas.
- `model`: o identificador do modelo a ser usado para a solicitação de reconhecimento.
- `timestamps`: indica se o alinhamento de horário é retornado para cada palavra.
- `watson-token`: fornece um token de autenticação para o serviço como uma alternativa para fornecer credenciais de serviço.
- `word_alternatives_threshold`: um valor de confiança que é o limite inferior para identificar uma hipótese como uma alternativa de palavra possível.
- `word_confidence`: indica se uma medida de confiança no intervalo de 0 a 1 deve ser retornada para cada palavra.
- `X-Watson-Learning-Opt-Out`: indica se deve-se fazer opt-out de coleta de dados para a chamada.
 
Aqui está um exemplo de criação de uma ligação de pacote e de conversão de fala para texto.

1. Crie uma ligação de pacote com suas credenciais do Watson.

  ```
  wsk package bind /whisk.system/watson myWatson -p username 'MY_WATSON_USERNAME' -p password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. Chame a ação `speechToText` em sua ligação do pacote para converter o áudio codificado.

  ```
  wsk action invoke myWatson/speechToText --blocking --result --param payload <base64 encoding of a .wav file> --param content_type 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```
  {
    "data": "Hello Watson"
  }
  ```
  {: screen}
  
 
## Usando o pacote Slack
{: #openwhisk_catalog_slack}

O pacote `/whisk.system/slack` oferece uma maneira conveniente de usar as [APIs do Slack](https://api.slack.com/).

O pacote inclui as ações a seguir:

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/slack` | pacote | url, channel, username | Interagir com a API do Slack |
| `/whisk.system/slack/post` | ação | text, url, channel, username | Posta uma mensagem para um canal do Slack |

Embora não seja obrigatório, é recomendável criar uma ligação de pacote com os valores de `username`, `url` e 'channel'. Com a ligação, não será necessário especificar os valores toda vez que você chamar a ação no pacote.

### Postando uma mensagem para um canal do Slack

A ação `/whisk.system/slack/post` posta uma mensagem para um canal do Slack especificado. Os parâmetros são como segue:

- `url`: a URL do webhook do Slack.
- `channel`: o canal do Slack no qual postar a mensagem.
- `username`: o nome com o qual postar a mensagem.
- `text`: uma mensagem para postar.

A seguir há um exemplo de configuração do Slack, criação de uma ligação de pacote e postagem de uma mensagem para um canal.

1. Configure um [webhook recebido](https://api.slack.com/incoming-webhooks) do Slack para sua equipe.

  Após configurar o Slack, será necessário obter uma URL de webhook semelhante a `https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`. Precisará dela na próxima etapa.

2. Crie uma ligação de pacote com suas credenciais do Slack, o canal no qual deseja postar e o nome de usuário com o qual postar.

  ```
  wsk package bind /whisk.system/slack mySlack --param url 'https://hooks.slack.com/services/...' --param username 'Bob' --param channel '#MySlackChannel'
  ```
  {: pre}

3. Chame a ação `post` em sua ligação do pacote para postar uma mensagem em seu canal do Slack.

  ```
  wsk action invoke mySlack/post --blocking --result --param text 'Hello from OpenWhisk!'
  ```
  {: pre}


## Usando o pacote GitHub
{: #openwhisk_catalog_github}

O pacote `/whisk.system/github` oferece uma maneira conveniente de usar as [APIs do GitHub](https://developer.github.com/).

O pacote inclui o feed a seguir:

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/github` | pacote | username, repository, accessToken | Interagir com a API do GitHub |
| `/whisk.system/github/webhook` | alimentação | events, username, repository, accessToken | Disparar eventos acionadores na atividade do GitHub |

Embora não seja obrigatório, é recomendável criar uma ligação de pacote com os valores de `username`, `repository` e `accessToken`.  Com a ligação, não será necessário especificar os valores toda vez que usar o feed no pacote.

### Disparando um evento acionador com atividade do GitHub

O feed `/whisk.system/github/webhook` configura um serviço para disparar um acionador quando houver atividade em um repositório do GitHub especificado. Os parâmetros são como segue:

- `username`: o nome do usuário do repositório do GitHub.
- `repository`: o repositório do GitHub.
- `accessToken`: seu token de acesso pessoal do GitHub. Ao [criar seu token](https://github.com/settings/tokens), certifique-se de que sejam selecionados os escopos repo:status epublic_repo. Além disso, certifique-se de que não tenha nenhum webhook já definido para seu repositório.
- `events`: o [tipo de evento do GitHub](https://developer.github.com/v3/activity/events/types/) de interesse.

A seguir está um exemplo de criação de um acionador que será disparado toda vez que houver uma nova confirmação em um repositório do GitHub.

1. Gere um [token de acesso pessoal](https://github.com/settings/tokens) do GitHub.

  O token de acesso será usado na próxima etapa.

2. Crie uma ligação de pacote configurada para seu repositório do GitHub e com o token de acesso.

  ```
  wsk package bind /whisk.system/github myGit --param username myGitUser --param repository myGitRepo --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}

3. Crie um acionador para o tipo de evento `push` do GitHub usando seu feed `myGit/webhook`.

  ```
  wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}

Uma confirmação para o repositório do Github através de um `git push` fará com que o acionador seja disparado pelo webhook. Se houver uma regra que corresponda ao acionador, então, a
ação associada será chamada.
A ação recebe a carga útil de webhook do Github como um parâmetro de entrada. Cada evento de webhook do Github tem um esquema de JSON semelhante, mas um objeto de carga útil exclusivo que é determinado por
seu tipo de evento. Para obter mais informações sobre o conteúdo da carga útil, consulte a documentação da API de [Eventos e carga útil
do Github](https://developer.github.com/v3/activity/events/types/).


## Usando o pacote Push
{: #openwhisk_catalog_pushnotifications}

O pacote `/whisk.system/pushnotifications` permite trabalhar com um serviço de push. 

O pacote inclui o feed a seguir:

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | pacote | appId, appSecret  | Trabalhar com o serviço de push |
| `/whisk.system/pushnotifications/sendMessage` | ação | texto, url, deviceIds, plataformas, tagNames, apnsBadge, apnsCategory, apnsActionKeyTitle, apnsSound, apnsPayload, apnsType, gcmCollapseKey, gcmDelayWhileIdle, gcmPayload, gcmPriority, gcmSound, gcmTimeToLive | 
Enviar notificação push para o(s) dispositivo(s) especificado(s) |
| `/whisk.system/pushnotifications/webhook` | alimentação | eventos | Disparar
eventos acionadores nas atividades de dispositivo (registro/remoção
de registro e assinatura/cancelamento de assinatura do dispositivo) no Serviço de Push |
Embora não seja obrigatório, é recomendável criar uma ligação de pacote com os valores de `appId` e `appSecret`. Dessa forma, não será necessário especificar essas credenciais toda vez que chamar as ações no pacote.

### Configurando o pacote do IBM Push Notifications

Ao criar um pacote do IBM Push Notifications você precisa fornecer os parâmetros a seguir,

-  `appId`: o GUID do aplicativo Bluemix.
-  `appSecret`: o appSecret de serviço de notificação push do Bluemix.

A seguir está um exemplo de criação de uma ligação de pacote.

1. Crie um aplicativo Bluemix em [Bluemix Dashboard](http://console.ng.bluemix.net).

2. Inicialize o Serviço de Notificação Push e ligue o serviço ao aplicativo Bluemix

3. Configure o [aplicativo IBM Push Notification](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

  Certifique-se de lembrar do `App GUID` e do `App Secret` do aplicativo Bluemix que você criou.


4. Crie uma ligação de pacote com as `/whisk.system/pushnotifications`.

  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId "myAppID" -p appSecret "myAppSecret"
  ```
  {: pre}

5. Verifique se a ligação do pacote existe.

  ```
  wsk package list
  ```
  {: pre}

  ```
  packages
  /myNamespace/myPush private binding
  ```
  {: screen}

### Enviando notificações push

A ação `/whisk.system/pushnotifications/sendMessage` envia notificações push para dispositivos registrados. Os parâmetros são como segue:
- `text` - A mensagem de notificação a ser mostrada ao usuário. Por exemplo: -p text "Oi, {{site.data.keyword.openwhisk}} envie uma notificação".
- `url`: uma URL opcional que pode ser enviada junto com o alerta. Por exemplo: -p url "https:\\www.w3.ibm.com".
- `gcmPayload` - Carga útil de JSON customizada que será enviada como parte da mensagem de notificação. Por exemplo: -p gcmPayload "{"hi":"hello"}"
- `gcmSound` - O arquivo de som (no dispositivo) que tentará ser reproduzido quando a notificação chegar no dispositivo.
- `gcmCollapseKey` - Esse parâmetro identifica um grupo de mensagens
- `gcmDelayWhileIdle` - Quando esse parâmetro é configurado como verdadeiro, ele indica que a mensagem não deve ser enviada até o dispositivo ficar ativo.
- `gcmPriority` - Configura a prioridade da mensagem.
- `gcmTimeToLive` - Esse parâmetro especifica quanto tempo (em segundos) a mensagem deve ser mantida no armazenamento de GCM se o dispositivo estiver off-line.
- `apnsBadge` - O número para exibir como o badge do ícone do aplicativo.
- `apnsCategory` -  O identificador de categoria a ser usado para as notificações push interativas.
- `apnsIosActionKey` - O título para a chave Ação.
- `apnsPayload` - Carga útil de JSON customizada que será enviada como parte da mensagem de notificação.
- `apnsType` - ['DEFAULT', 'MIXED', 'SILENT'].
- `apnsSound` - O nome do arquivo de som no pacote configurável do aplicativo. O som desse arquivo é reproduzido como um alerta.

Aqui está um exemplo de envio de notificação push a partir do pacote pushnotification.

1. Envie notificação push usando a ação `sendMessage` na ligação de pacote anteriormente criada. Certifique-se de substituir `/myNamespace/myPush` pelo nome de seu pacote.

  ```
  wsk action invoke /myNamespace/myPush/sendMessage --blocking
--result  -p url https://example.com -p text "this is my message"  -p
sound soundFileName -p deviceIds '["T1","T2"]'
  ```
  {: pre}

  ```
  {
  "result": {
  "pushResponse":
"{"messageId":"11111H","message":{"message":{"alert":"this is my
message","url":"http.google.com"},"settings":{"apns":{"sound":"default"},"gcm":{"sound":"default"},"target":{"deviceIds":["T1","T2"]}}}"
  },
      "status": "success",
      "success": true
  }
  ```
  {: screen}

### Disparando um evento acionador na atividade do IBM Push Notifications Service

O `/whisk.system/pushnotifications/webhook` configura o serviço do IBM Push Notifications para disparar um acionador quando houver uma atividade de dispositivo como registro de
dispositivo/remoção de registro ou assinatura/cancelamento de assinatura em um aplicativo especificado

Os parâmetros são como segue:

- `appId:` o appSecret de serviço de notificação push do Bluemix.
- `appSecret:` o GUID do aplicativo Bluemix.
- `events:` os eventos suportados são `onDeviceRegister`, `onDeviceUnregister`, `onDeviceUpdate`, `onSubscribe`,
`onUnsubscribe`. Para ser notificado de todos os eventos use o caractere curinga `*`.

A seguir está um exemplo de criação de um acionador que será disparado toda vez que houver um novo dispositivo registrado com o aplicativo IBM Push Notifications Service.

1. Crie uma ligação de pacote configurada para o seu serviço do IBM Push Notifications com o seu appId e appSecret.

  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}

2. Crie um acionador para o tipo de evento `onDeviceRegister` do IBM Push Notifications Service usando o seu feed `myPush/webhook`.

  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}
