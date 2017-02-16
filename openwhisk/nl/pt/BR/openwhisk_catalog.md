---

 

copyright:

  years: 2016, 2017
lastupdated: "2017-01-04"
 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Usando serviços do {{site.data.keyword.Bluemix_notm}} que estão ativados
para {{site.data.keyword.openwhisk_short}}
{: #openwhisk_ecosystem}

No {{site.data.keyword.openwhisk}}, um catálogo de pacotes fornece uma maneira fácil de aprimorar seu app com recursos úteis e de acessar serviços externos no ecossistema. Exemplos de serviços externos que são ativados pelo {{site.data.keyword.openwhisk_short}} incluem Cloudant, The Weather Company, Slack e GitHub.
{: shortdesc}

O catálogo está disponível como pacotes no namespace `/whisk.system`. Consulte [Procurando em pacotes](./openwhisk_packages.html#openwhisk_packagedisplay) para obter informações sobre como procurar no catálogo usando a ferramenta de linha de comandos.

Os tópicos a seguir documentam alguns dos pacotes no catálogo.

## Usando o pacote Cloudant
{: #openwhisk_catalog_cloudant}
O pacote `/whisk.system/cloudant` permite trabalhar com um banco de dados do Cloudant. Ele inclui as ações e os feeds a seguir.

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | pacote | {{site.data.keyword.Bluemix_notm}}ServiceName, host, username, password, dbname, overwrite | Trabalhar com um banco de dados do Cloudant |
| `/whisk.system/cloudant/read` | ação | dbname, includeDoc, id | Ler um documento a partir de um banco de dados |
| `/whisk.system/cloudant/write` | ação | dbname, overwrite, doc | Gravar um documento em um banco de dados |
| `/whisk.system/cloudant/changes` | alimentação | dbname, maxTriggers | Disparar eventos acionadores nas mudanças em um banco de dados |

Os tópicos a seguir percorrem a configuração de um banco de dados do Cloudant, a configuração de um pacote associado e o uso de ações e feeds no pacote `/whisk.system/cloudant`.

### Configurando um banco de dados do Cloudant no {{site.data.keyword.Bluemix_notm}}
{: #openwhisk_catalog_cloudant_in}

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

  Você vê o nome completo da ligação do pacote que corresponde à instância de
serviço do {{site.data.keyword.Bluemix_notm}} Cloudant.

4. Verifique se a ligação do pacote que foi criada anteriormente está configurada
com seu host e credenciais da instância de serviço do {{site.data.keyword.Bluemix_notm}}
Cloudant.

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
{: #openwhisk_catalog_cloudant_outside}

Se não estiver usando o {{site.data.keyword.openwhisk_short}} no {{site.data.keyword.Bluemix_notm}} ou se desejar configurar seu banco de dados do Cloudant fora do {{site.data.keyword.Bluemix_notm}}, deverá criar manualmente uma ligação de pacote para sua conta do Cloudant. Você
precisa do nome do host, do nome do usuário e da senha da conta do Cloudant.

1. Crie uma ligação de pacote que esteja configurada para sua conta do Cloudant.

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username MYUSERNAME -p password MYPASSWORD -p host MYCLOUDANTACCOUNT.cloudant.com
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
{: #openwhisk_catalog_cloudant_listen}

É possível usar o feed `changes` para configurar um serviço para disparar um acionador em cada mudança em seu banco de dados do Cloudant. Os parâmetros são como segue:

- `dbname`: nome do banco de dados do Cloudant.
- `maxTriggers`: parar de disparar acionadores quando esse limite for atingido. O padrão é definido como infinite.

1. Crie um acionador com o feed `changes` na ligação do pacote criada anteriormente. Certifique-se de substituir `/myNamespace/myCloudant` pelo nome de seu pacote.

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
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

**Nota**: se você não for capaz de observar novas ativações, consulte as seções subsequentes sobre leitura e gravação em um banco de dados do Cloudant. O teste das etapas de leitura e
gravação a seguir ajudará a verificar se as suas credenciais do Cloudant estão corretas.

Agora, é possível criar regras e associá-las a ações para reagir às atualizações do documento.

O conteúdo dos eventos gerados tem os parâmetros a seguir:

- `id`: o ID do documento.
- `seq`: o identificador de sequência que é gerado pelo Cloudant.
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
{: #openwhisk_catalog_cloudant_write}

É possível usar uma ação para armazenar um documento em um banco de dados do Cloudant denominado `testdb`. Certifique-se de que esse banco de dados exista em sua conta do Cloudant.

1. Armazene um documento usando a ação `write` na ligação do pacote anteriormente criada. Certifique-se de substituir `/myNamespace/myCloudant` pelo nome de seu pacote.

  ```
  wsk action invoke /myNamespace/myCloudant/write --blocking --result --param dbname testdb --param doc "{\"_id\":\"heisenberg\",\"name\":\"Walter White\"}"
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCloudant/write with id 62bf696b38464fd1bcaff216a68b8287
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
{: #openwhisk_catalog_cloudant_read}

É possível usar uma ação para buscar um documento a partir de um banco de dados do Cloudant chamado `testdb`. Certifique-se de que esse banco de dados exista em sua conta do Cloudant.

1. Busque um documento usando a ação `read` na ligação do pacote anteriormente criada. Certifique-se de substituir `/myNamespace/myCloudant` pelo nome de seu pacote.

  ```
  wsk action invoke /myNamespace/myCloudant/read --blocking --result --param dbname testdb --param id heisenberg
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

### Usando uma sequência de ações e um acionador de mudança para processar um documento de um banco de dados do Cloudant

É possível usar uma sequência de ações em uma regra para buscar e processar o documento associado a um evento de mudança do Cloudant.

Aqui está um código de amostra de uma ação que manipula um documento:
```
function main(doc){
  return { "isWalter:" : doc.name === "Walter White"};
}
```
{: codeblock}

Crie a ação para processar o documento do Cloudant:
```
wsk action create myAction myAction.js
```
{: pre}

Para ler um documento do banco de dados, é possível usar a ação `read` do pacote do Cloudant.
A ação `read` pode ser editada com `myAction` para criar uma sequência de ações.
```
wsk action create sequenceAction --sequence /myNamespace/myCloudant/read,myAction
```
{: pre}

A ação `sequenceAction` pode ser usada em uma regra que ativa a ação em novos eventos acionadores do Cloudant.
```
wsk rule create myRule myCloudantTrigger sequenceAction
```
{: pre}

**Nota**: o acionador `changes` do Cloudant é usado para suportar o parâmetro `includeDoc`, que não é mais suportado.
  Será necessário recriar os acionadores criados anteriormente com `includeDoc`. Sigas estas etapas para recriar o acionador:
  ```
  wsk trigger delete myCloudantTrigger
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}

  O exemplo ilustrado acima pode ser usado para criar uma sequência de ações para ler o documento mudado e chamar suas ações existentes.
  Lembre-se de desativar as regras que podem não ser mais válidas e criar novas usando o padrão de sequência de ações.

## Usando o pacote Alarme
{: #openwhisk_catalog_alarm}

O pacote `/whisk.system/alarms` pode ser usado para disparar um
acionador em uma frequência especificada. Isso é útil para configurar tarefas ou
trabalhos recorrentes, como chamar uma ação de backup do sistema a cada hora.

O pacote inclui o feed a seguir.

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | pacote | - | Alarmes e utilitário periódico |
| `/whisk.system/alarms/alarm` | alimentação | cron, trigger_payload, maxTriggers | Disparar evento acionador periodicamente |


### Disparando um evento acionador periodicamente
{: #openwhisk_catalog_alarm_fire}

O feed `/whisk.system/alarms/alarm` configura o serviço de Alarme para disparar um evento acionador a uma frequência especificada. Os parâmetros são como segue:

- `cron`: Uma sequência, baseada na sintaxe crontab do UNIX, que
indica quando disparar o acionador na Hora Universal Coordenada (UTC). A sequência é composta por cinco campos separados por espaços: `X X X X X`.
Para obter mais detalhes sobre como usar a sintaxe cron, veja: http://crontab.org. Seguem alguns exemplos da frequência indicada
pela sequência:

  - `* * * * *`: na parte superior de cada minuto.
  - `0 * * * *`: na parte superior de cada hora.
  - `0 */2 * * *`: a cada 2 horas (ou seja, 02:00:00, 04:00:00, ...)
  - `0 9 8 * *`: às 9h (UTC) no oitavo dia de cada mês

- `trigger_payload`: o valor desse parâmetro torna-se o conteúdo do acionador toda vez que o acionador for disparado.

- `maxTriggers`: parar de disparar acionadores quando esse limite for atingido. O padrão é definido como 1.000.000. É possível configurá-lo como infinite (-1). 

A seguir está um exemplo de criação de um acionador que será disparado uma vez a cada 2 minutos com valores `name` e `place`
no evento acionador.

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron "*/2 * * * *" --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

Cada evento gerado incluirá como parâmetros as propriedades especificadas no valor de `trigger_payload`. Neste caso, cada evento acionador terá os parâmetros `name=Odin` e `place=Asgard`.

**Nota**: o parâmetro `cron` também suporta uma sintaxe customizada de seis campos, na qual o primeiro campo representa
segundos. 
Para obter mais detalhes sobre como usar a sintaxe cron customizada, veja: https://github.com/ncb000gt/node-cron. 
Aqui está um exemplo usando a notação de seis campos:
  - `*/30 * * * * *`: a cada trinta segundos.

## Usando o pacote Clima
{: #openwhisk_catalog_weather}

O pacote `/whisk.system/weather` oferece uma maneira conveniente
de chamar a API do Weather Company Data for IBM Bluemix.

O pacote inclui a ação a seguir.

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/weather` | pacote | username, password | Serviços da API do Weather Company Data for IBM Bluemix  |
| `/whisk.system/weather/forecast` | ação | latitude, longitude, timePeriod | previsão para o período especificado|

É sugerido criar uma ligação de pacote com os valores `username`
e `password`. Dessa forma, não será necessário especificar as
credenciais toda vez que chamar as ações no pacote.

### Obtendo uma previsão de tempo para um local
{: #openwhisk_catalog_weather_forecast}

A ação `/whisk.system/weather/forecast` retorna uma previsão do tempo para um local, chamando uma API a partir da The Weather Company. Os parâmetros são como segue:

- `username`: nome do usuário do The Weather Company Data for IBM Bluemix que está autorizado a chamar a API de previsão.
- `password`: senha para o The Weather Company Data for IBM Bluemix que está autorizado a chamar a API de previsão.
- `latitude`: a coordenada de latitude do local.
- `longitude`: a coordenadas de longitude do local.
- `timeperiod`: período para a previsão. As opções válidas são '10day' - (padrão) Retorna uma previsão diária de 10 dias, '48hour' - Retorna uma previsão de 2 dias de hora em hora,
'current' - Retorna as condições meteorológicas atuais, 'timeseries' - Retorna as observações atuais e até 24 horas de observações passadas, a partir da data e hora atuais.


Segue um exemplo de criação de uma ligação de pacote e, em seguida, a obtenção de uma previsão de 10 dias.

1. Crie uma ligação de pacote com sua chave da API.

  ```
  wsk package bind /whisk.system/weather myWeather --param username MY_USERNAME --param password MY_PASSWORD
  ```
  {: pre}

2. Chame a ação `forecast` em sua ligação do pacote para obter a previsão do tempo.

  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude 43.7 --param longitude -79.4
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


## Usando os pacotes do Watson
{: #openwhisk_catalog_watson}

Os pacotes do Watson oferecem uma maneira conveniente de chamar várias APIs do Watson.

Os pacotes do Watson a seguir são fornecidos:

| Package | Descrição |
| --- | --- |
| `/whisk.system/watson-translator`   | Pacote para tradução de texto e identificação de idioma |
| `/whisk.system/watson-textToSpeech` | Pacote para converter texto em fala |
| `/whisk.system/watson-speechToText` | Pacote para converter fala em texto |

**Nota** O pacote `/whisk.system/watson` está atualmente descontinuado; migre para os novos pacotes mencionados acima;
as novas ações fornecem a mesma interface.

### Usando o pacote do Tradutor do Watson

O pacote `/whisk.system/watson-translator` oferece uma maneira conveniente de chamar APIs do Watson para traduzir.

O pacote inclui as ações a seguir.

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/watson-translator` | pacote | username, password | Pacote para tradução de texto e identificação de idioma  |
| `/whisk.system/watson-translator/translator` | ação | payload, translateFrom, translateTo, translateParam, username, password | Traduzir texto |
| `/whisk.system/watson-translator/languageId` | ação | payload, username, password | Identificar idioma |

**Nota**: o pacote `/whisk.system/watson` está descontinuado, incluindo as ações `/whisk.system/watson/translate` e `/whisk.system/watson/languageId`.

#### Configurando o pacote do Tradutor do Watson no Bluemix

Se você estiver usando o OpenWhisk a partir do Bluemix, o OpenWhisk criará automaticamente as ligações de pacote para as suas instâncias de serviço do Watson
do Bluemix.

1. Crie uma instância de serviço do Tradutor do Watson em seu [painel](http://console.ng.Bluemix.net) do Bluemix.

  Certifique-se de lembrar do nome da instância de serviço e da organização e do espaço do Bluemix nos quais você está.

2. Certifique-se de que a sua CLI do OpenWhisk esteja no namespace correspondente à organização e ao espaço do Bluemix que você usou na etapa anterior.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  Como alternativa, é possível usar `wsk property set --namespace` para configurar um namespace a partir de uma lista daqueles disponíveis para você.

3. Atualize os pacotes em seu namespace. A atualização cria automaticamente uma ligação de pacote para a instância de serviço do Watson que você criou.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_Translator_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_Translator_Credentials-1 private
  ```
  {: screen}


#### Configurando um pacote do Tradutor do Watson fora do Bluemix

Se você não estiver usando o OpenWhisk no Bluemix ou se desejar configurar o seu Tradutor do Watson fora do Bluemix, deverá criar manualmente uma ligação de
pacote para o seu serviço de Tradutor do Watson. Você precisa do nome do usuário e da senha do serviço de Tradutor do Watson.

- Crie uma ligação de pacote que esteja configurada para o seu serviço de Tradutor do Watson.

  ```
  wsk package bind /whisk.system/watson-translator myWatsonTranslator -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### Traduzindo texto
{: #openwhisk_catalog_watson_translate}

A ação `/whisk.system/watson-translator/translator` traduz o texto de um idioma para outro. Os parâmetros são como segue:

- `username`: o nome do usuário da API do Watson.
- `password`: a senha da API do Watson.
- `payload`: o texto a ser traduzido.
- `translateParam`: o parâmetro de entrada indicando o texto a
ser traduzido. Por exemplo, se `translateParam=payload`, o valor do
parâmetro `payload` que é passado à ação será traduzido.
- `translateFrom`: um código de dois dígitos do idioma de origem.
- `translateTo`: um código de dois dígitos do idioma de destino.

- Chame a ação `translator` em sua ligação de pacote para traduzir algum texto do inglês para o francês.

  ```
  wsk action invoke myWatsonTranslator/translator --blocking --result --param payload 'Blue skies ahead' --param translateFrom 'en' --param translateTo 'fr'
  ```
  {: pre}

  ```
  {
      "payload": "Ciel bleu a venir"
  }
  ```
  {: screen}


#### Identificando o idioma de algum texto
{: #openwhisk_catalog_watson_identifylang}

A ação `/whisk.system/watson-translator/languageId` identifica o idioma de algum texto. Os parâmetros são como segue:

- `username`: o nome do usuário da API do Watson.
- `password`: a senha da API do Watson.
- `payload`: o texto para identificar.

- Chame a ação `languageId` em sua ligação do pacote para identificar o idioma.

  ```
  wsk action invoke myWatsonTranslator/languageId --blocking --result --param payload 'Ciel bleu a venir'
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


### Usando o pacote de Texto do Watson para Fala
{: #openwhisk_catalog_watson_texttospeech}

O pacote `/whisk.system/watson-textToSpeech` oferece uma maneira conveniente de chamar APIs do Watson para converter o texto em fala.

O pacote inclui as ações a seguir.

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | pacote | username, password | Pacote para converter texto em fala |
| `/whisk.system/watson-textToSpeech/textToSpeech` | ação | payload, voice, accept, encoding, username, password | Converter texto em áudio |

**Nota**: o pacote `/whisk.system/watson` está descontinuado, incluindo a ação `/whisk.system/watson/textToSpeech`.

#### Usando o pacote de Texto do Watson para Fala no Bluemix

Se você estiver usando o OpenWhisk a partir do Bluemix, o OpenWhisk criará automaticamente as ligações de pacote para as suas instâncias de serviço do Watson
do Bluemix.

1. Crie uma instância de serviço de Texto do Watson para Fala em seu [painel](http://console.ng.Bluemix.net) do Bluemix.

  Certifique-se de lembrar do nome da instância de serviço e da organização e do espaço do Bluemix nos quais você está.

2. Certifique-se de que a sua CLI do OpenWhisk esteja no namespace correspondente à organização e ao espaço do Bluemix que você usou na etapa anterior.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  Como alternativa, é possível usar `wsk property set --namespace` para configurar um namespace a partir de uma lista daqueles disponíveis para você.

3. Atualize os pacotes em seu namespace. A atualização cria automaticamente uma ligação de pacote para a instância de serviço do Watson que você criou.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_TextToSpeech_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_TextToSpeec_Credentials-1 private
  ```
  {: screen}


#### Configurando um pacote de Texto do Watson para Fala fora do Bluemix

Se você não estiver usando o OpenWhisk no Bluemix ou se desejar configurar o seu Texto do Watson para Fala fora do Bluemix, deverá criar manualmente uma ligação
de pacote para o seu serviço de Texto do Watson para Fala. Você precisa do nome do usuário e da senha do serviço de Texto do Watson para Fala.

- Crie uma ligação de pacote que esteja configurada para o seu serviço de Fala do Watson para Texto.

  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### Converter algum texto para fala
{: #openwhisk_catalog_watson_speechtotext}

A ação `/whisk.system/watson-speechToText/textToSpeech` converte algum texto em uma fala de áudio. Os parâmetros são como segue:

- `username`: o nome do usuário da API do Watson.
- `password`: a senha da API do Watson.
- `payload`: o texto para converter em fala.
- `voice`: a voz do orador.
- `accept`: o formato do arquivo de fala.
- `encoding`: a codificação dos dados binários de fala.


- Chame a ação `textToSpeech` em sua ligação do pacote para converter o texto.

  ```
  wsk action invoke myWatsonTextToSpeech/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```
  {
    "payload": "<base64 encoding of a .wav file>"
  }
  ```
  {: screen}


### Usando o pacote de Fala do Watson para Texto
{: #openwhisk_catalog_watson_speechtotext}

O pacote `/whisk.system/watson-speechToText` oferece uma maneira conveniente de chamar APIs do Watson para converter a fala em texto.

O pacote inclui as ações a seguir.

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/watson-speechToText` | pacote | username, password | Pacote para converter fala em texto |
| `/whisk.system/watson-speechToText/speechToText` | ação | payload, content_type, encoding, username, password, continuous, inactivity_timeout, interim_results, keywords, keywords_threshold, max_alternatives, model, timestamps, watson-token, word_alternatives_threshold, word_confidence, X-Watson-Learning-Opt-Out | Converter
áudio em texto |

**Nota**: o pacote `/whisk.system/watson` está descontinuado, incluindo a ação `/whisk.system/watson/speechToText`.

#### Configurando o pacote de Fala do Watson para Texto no Bluemix

Se você estiver usando o OpenWhisk a partir do Bluemix, o OpenWhisk criará automaticamente as ligações de pacote para as suas instâncias de serviço do Watson
do Bluemix.

1. Crie uma instância de serviço de Fala do Watson para Texto em seu [painel](http://console.ng.Bluemix.net) do Bluemix.

  Certifique-se de lembrar do nome da instância de serviço e da organização e do espaço do Bluemix nos quais você está.

2. Certifique-se de que a sua CLI do OpenWhisk esteja no namespace correspondente à organização e ao espaço do Bluemix que você usou na etapa anterior.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  Como alternativa, é possível usar `wsk property set --namespace` para configurar um namespace a partir de uma lista daqueles disponíveis para você.

3. Atualize os pacotes em seu namespace. A atualização cria automaticamente uma ligação de pacote para a instância de serviço do Watson que você criou.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_SpeechToText_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_SpeechToText_Credentials-1 private
  ```
  {: screen}


#### Configurando um pacote de Fala do Watson para Texto fora do Bluemix

Se você não estiver usando o OpenWhisk no Bluemix ou se desejar configurar a sua Fala do Watson para Texto fora do Bluemix, deverá criar manualmente uma ligação de
pacote para o seu serviço de Fala do Watson para Texto. Você precisa do nome do usuário e da senha do serviço de Fala do Watson para Texto.

- Crie uma ligação de pacote que esteja configurada para o seu serviço de Fala do Watson para Texto.

  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonSpeechToText -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### Convertendo fala para texto

A ação `/whisk.system/watson-speechToText/speechToText` converte fala de áudio em texto. Os parâmetros são como segue:

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
 

- Chame a ação `speechToText` em sua ligação do pacote para converter o áudio codificado.

  ```
  wsk action invoke myWatsonSpeechToText/speechToText --blocking --result --param payload <base64 encoding of a .wav file> --param content_type 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```
  {
    "data": "Hello Watson"
  }
  ```
  {: screen}
 
 
## Usando o pacote Message Hub
{: #openwhisk_catalog_message_hub}

Esse pacote permite criar acionadores que reagem quando as mensagens são postadas em uma instância de serviço do [Message Hub](https://developer.ibm.com/messaging/message-hub/) no Bluemix.

### Criando um acionador que atende a uma Instância do Message Hub
{: #openwhisk_catalog_message_hub_trigger}
Para criar um acionador que reaja quando as mensagens forem postadas em uma instância do Message Hub, será necessário usar o feed chamado `messaging/messageHubFeed`. Esse feed suporta os parâmetros a seguir:

|Nome|Tipo|Descrição|
|---|---|---|
|kafka_brokers_sasl|Matriz JSON de sequência de caracteres|Esse parâmetro é uma matriz de sequências `<host>:<port>` que formam os brokers na instância do Message Hub|
|usuário|Sequência de caracteres|Nome do usuário do Message Hub|
|password|Sequência de caracteres|Senha do Message Hub|
|tópico|Sequência de caracteres|O tópico que você gostaria que o acionador atendesse|
|kafka_admin_url|Sequência URL|A URL da interface REST do administrador do Message Hub|
|api_key|Sequência de caracteres|Sua chave API do Message Hub|
|isJSONData|Booleano (Opcional - padrão=false)|Quando configurado como `true`, isso fará com que o feed tente analisar o conteúdo da mensagem como JSON antes de passá-lo adiante como a carga útil do acionador.|

Embora essa lista de parâmetros possa parecer assustadora, ela pode ser configurada automaticamente por você usando o comando de atualização de pacote da CLI:

1. Crie uma instância do serviço Message Hub em sua organização e espaço atuais que você está usando para o OpenWhisk.

2. Verifique se o tópico que você deseja atender já existe no Message Hub ou crie um novo tópico para atender as mensagens, como `mytopic`.

2. Atualize os pacotes em seu namespace. A atualização cria automaticamente uma ligação de pacote para a instância de serviço do Message Hub que você criou.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Message_Hub_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1 private
  ```
  {: screen}

  Sua ligação de pacote agora contém as credenciais associadas à sua instância do Message Hub.

3. Agora tudo o que você precisa é criar um Acionador para ser disparado quando novas mensagens forem postadas no Message Hub.

  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

### Configurando um pacote Message Hub fora do Bluemix

Caso você não esteja usando o OpenWhisk no Bluemix ou caso queira configurar o Message Hub fora do Bluemix, deve-se criar manualmente uma ligação de pacote para o serviço Message Hub. Você precisa das credenciais de serviço e das informações de conexão do Message Hub.

- Crie uma ligação de pacote que esteja configurada para o serviço Message Hub.

  ```
  wsk trigger create MyMessageHubTrigger -f /whisk.system/messaging/messageHubFeed -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p topic mytopic -p user <your Message Hub user> -p password <your Message Hub password> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443 -p api_key <your API key>
  ```
  {: pre}

### Atendendo mensagens para uma instância do Message Hub
{: #openwhisk_catalog_message_hub_listen}
Depois de criar um acionador, o sistema monitorará o tópico especificado em seu serviço de sistema de mensagens. Quando novas mensagens forem postadas, o acionador será disparado.

A carga útil desse acionador conterá um campo `messages` que é uma matriz de mensagens que foram postadas desde a última vez que o acionador foi disparado. Cada objeto de mensagem na matriz conterá os campos a seguir:
- - tópico
- partição
- Deslocamento
- Chave
- derivado

Em termos Kafka, esses campos devem ser autoevidentes. No entanto, o `value` requer consideração especial. Se o parâmetro `isJSONData` tiver sido configurado como `false` (ou não tiver sido configurado) quando o acionador foi criado, o campo `value` será o valor bruto da mensagem postada. No entanto, se `isJSONData` tiver sido configurado como `true` quando o acionador foi criado, o sistema tentará analisar esse valor como um objeto JSON, no melhor esforço. Se a análise for bem-sucedida, o `value` na carga útil do acionador será o objeto JSON resultante.

Por exemplo, se uma mensagem de `{"title": "Some string", "amount": 5, "isAwesome": true}` for postada com `isJSONData` configurado como `true`, a carga útil do acionador poderá ser semelhante a isto:

```
{
  "messages": [
      {
        "partition": 0,
        "key": null,
        "offset": 421760,
        "topic": "mytopic",
        "value": {
            "amount": 5,
            "isAwesome": true,
            "title": "Some string"
        }
      }
  ]
}
```

No entanto, se o mesmo conteúdo da mensagem fosse postado com `isJSONData` configurado como `false`, a carga útil do acionador seria assim:

```
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421761,
      "topic": "mytopic",
      "value": "{\"title\": \"Some string\", \"amount\": 5, \"isAwesome\": true}"
    }
  ]
}
```

### As mensagens são processadas em lote
Você observará que a carga útil do acionador contém uma matriz de mensagens. Isso significa que se você estiver produzindo mensagens para seu sistema de mensagens muito rapidamente, o feed tentará processar em lote as mensagens postadas em um único disparo do acionador. Isso permite que as mensagens sejam postadas no acionador de maneira mais rápida e eficiente.

Lembre-se de que, ao codificar ações que são disparadas por seu acionador, o número de mensagens na carga útil é tecnicamente sem limites, mas sempre será maior que 0.


## Usando o pacote Slack
{: #openwhisk_catalog_slack}

O pacote `/whisk.system/slack` oferece uma maneira conveniente de usar as [APIs do Slack](https://api.slack.com/).

O pacote inclui as ações a seguir:

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/slack` | pacote | url, channel, username | Interagir com a API do Slack |
| `/whisk.system/slack/post` | ação | text, url, channel, username | Posta uma mensagem para um canal do Slack |

É sugerido criar uma ligação de pacote com os valores `username`, `url` e
`channel`. Com a ligação, não será necessário especificar os valores toda vez que você chamar a ação no pacote.

### Postando uma mensagem para um canal do Slack
{: #openwhisk_catalog_slack_post}

A ação `/whisk.system/slack/post` posta uma mensagem para um canal do Slack especificado. Os parâmetros são como segue:

- `url`: a URL do webhook do Slack.
- `channel`: o canal do Slack no qual postar a mensagem.
- `username`: o nome com o qual postar a mensagem.
- `text`: uma mensagem para postar.
- `token`: (opcional) um [token de acesso](https://api.slack.com/tokens) de Slack. Consulte [abaixo](./openwhisk_catalog.html#openwhisk_catalog_slack_token) para obter mais detalhes sobre o uso dos tokens de acesso de Folga.

A seguir há um exemplo de configuração do Slack, criação de uma ligação de pacote e postagem de uma mensagem para um canal.

1. Configure um [webhook recebido](https://api.slack.com/incoming-webhooks) do Slack para sua equipe.

  Após a configuração do Slack, você obtém uma URL de webhook semelhante a
`https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`. Precisará dela na próxima etapa.

2. Crie uma ligação de pacote com suas credenciais do Slack, o canal no qual deseja postar e o nome de usuário com o qual postar.

  ```
  wsk package bind /whisk.system/slack mySlack --param url "https://hooks.slack.com/services/..." --param username Bob --param channel "#MySlackChannel"
  ```
  {: pre}

3. Chame a ação `post` em sua ligação do pacote para postar uma mensagem em seu canal do Slack.

  ```
  wsk action invoke mySlack/post --blocking --result --param text "Hello from OpenWhisk!"
  ```
  {: pre}

### Usando a API baseada no token de Slack
{: #openwhisk_catalog_slack_token}

Se você preferir, será possível escolher, opcionalmente, usar uma API baseada no token de Slack, em vez de a API do webhook. Se você assim escolher, então, passe em um parâmetro `token` que contém o seu [token de acesso](https://api.slack.com/tokens) do Slack. É possível, então, usar qualquer dos [métodos de API Slack](https://api.slack.com/methods) como o seu parâmetro `url`. Por exemplo, para postar uma mensagem, você utilizaria um valor de parâmetro `url` [slack.postMessage](https://api.slack.com/methods/chat.postMessage).

## Usando o pacote GitHub
{: #openwhisk_catalog_github}

O pacote `/whisk.system/github` oferece uma maneira conveniente de usar as [APIs do GitHub](https://developer.github.com/).

O pacote inclui o feed a seguir:

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/github` | pacote | username, repository, accessToken | Interagir com a API do GitHub |
| `/whisk.system/github/webhook` | alimentação | events, username, repository, accessToken | Disparar eventos acionadores na atividade do GitHub |

É sugerido criar uma ligação de pacote com os valores `username`,
`repository` e `accessToken`.  Com a ligação, não será necessário especificar os valores toda vez que usar o feed no pacote.

### Disparando um evento acionador com atividade do GitHub
{: #openwhisk_catalog_github_fire}

O feed `/whisk.system/github/webhook` configura um serviço para disparar um acionador quando houver atividade em um repositório do GitHub especificado. Os parâmetros são como segue:

- `username`: o nome do usuário do repositório GitHub.
- `repository`: o repositório do GitHub.
- `accessToken`: seu token de acesso pessoal do GitHub. Ao [criar seu token](https://github.com/settings/tokens), certifique-se de que sejam selecionados os escopos repo:status epublic_repo. Além
disso, certifique-se de que não tenha nenhum webhook já definido para seu repositório.
- `events`: o [tipo de evento do GitHub](https://developer.github.com/v3/activity/events/types/) de interesse.

A seguir está um exemplo de criação de um acionador que será disparado toda vez que houver uma nova confirmação em um repositório do GitHub.

1. Gere um [token de acesso pessoal](https://github.com/settings/tokens) do GitHub.

  O token de acesso será usado na próxima etapa.

2. Crie uma ligação de pacote configurada para seu repositório GitHub e com o token de acesso.

  ```
  wsk package bind /whisk.system/github myGit --param username myGitUser --param repository myGitRepo --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}

3. Crie um acionador para o tipo de evento `push` do GitHub usando seu feed `myGit/webhook`.

  ```
  wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}

Uma confirmação para o repositório GitHub usando um `git push` faz
com que o acionador seja disparado pelo webhook. Se houver uma regra que corresponda ao acionador, então, a
ação associada será chamada.
A ação recebe a carga útil de webhook do GitHub como um parâmetro de entrada. Cada evento
de webhook do GitHub tem um esquema JSON semelhante, mas é um objeto de carga útil
exclusivo que é determinado por seu tipo de evento.
Para obter mais informações sobre o
conteúdo da carga útil, consulte a documentação da API de
[Eventos e carga útil
do GitHub](https://developer.github.com/v3/activity/events/types/).


## Usando o pacote Push
{: #openwhisk_catalog_pushnotifications}

O pacote `/whisk.system/pushnotifications` permite trabalhar com um serviço de push. 

O pacote inclui a ação e o feed a seguir:

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | pacote | appId, appSecret  | Trabalhar com o serviço de push |
| `/whisk.system/pushnotifications/sendMessage` | ação | texto, url, deviceIds, plataformas, tagNames, apnsBadge, apnsCategory, apnsActionKeyTitle, apnsSound, apnsPayload, apnsType, gcmCollapseKey, gcmDelayWhileIdle, gcmPayload, gcmPriority, gcmSound, gcmTimeToLive | Enviar notificação push para um ou mais dispositivos especificados |
| `/whisk.system/pushnotifications/webhook` | alimentação | eventos | Disparar eventos acionadores nas atividades de dispositivo (registro, remoção de registro, assinatura, cancelamento de assinatura do dispositivo) no serviço de Push |
É sugerido criar uma ligação de pacote com os valores `appId` e
`appSecret`. Dessa forma, não será necessário especificar essas
credenciais toda vez que chamar as ações no pacote.

### Criando uma ligação de pacote de Push
{: #openwhisk_catalog_pushnotifications_create}

Ao criar uma ligação de pacote de Notificações push, deve-se especificar os parâmetros a seguir,

-  `appId`: o GUID do aplicativo Bluemix.
-  `appSecret`: o appSecret de serviço de notificação push do Bluemix.

A seguir está um exemplo de criação de uma ligação de pacote.

1. Crie um aplicativo Bluemix em [Bluemix Dashboard](http://console.ng.bluemix.net).

2. Inicialize o Serviço de Notificação Push e ligue o serviço ao aplicativo Bluemix

3. Configure o [aplicativo
de Notificação push](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

  Certifique-se de lembrar do `App GUID` e do `App Secret` do aplicativo Bluemix que você criou.


4. Crie uma ligação de pacote com as `/whisk.system/pushnotifications`.

  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId myAppID -p appSecret myAppSecret
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
{: #openwhisk_catalog_pushnotifications_send}

A ação `/whisk.system/pushnotifications/sendMessage` envia notificações push para dispositivos registrados. Os parâmetros são como segue:
- `text`: a mensagem de notificação a ser mostrada ao usuário. Por exemplo: `-p text "Hi ,OpenWhisk send a notification"`.
- `url`: uma URL opcional que pode ser enviada junto com o alerta. Por exemplo: `-p url "https:\\www.w3.ibm.com"`.
- `deviceIds` A lista de dispositivos especificados. Por exemplo: `-p deviceIds "[\"deviceID1\"]"`.
- `platforms` Envie notificação para os dispositivos das plataformas especificadas. 'A' para dispositivos Apple (iOS) e 'G' para dispositivos Google (Android). Por exemplo, `-p platforms "[\"A\"]"`.
- `tagNames` Envie notificação para os dispositivos que foram inscritos em qualquer uma dessas tags. Por exemplo, `-p tagNames "[\"tag1\"]" `.
- `gcmPayload`: carga útil de JSON customizada que será enviada como parte da mensagem de notificação. Por exemplo: `-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmSound`: o arquivo de som (no dispositivo) que tentará ser reproduzido quando a notificação chegar no dispositivo.
- `gcmCollapseKey`: esse parâmetro identifica um grupo de mensagens
- `gcmDelayWhileIdle`: quando esse parâmetro é configurado como verdadeiro, ele indica que a mensagem não será enviada até que o dispositivo fique ativo.
- `gcmPriority`: configura a prioridade da mensagem.
- `gcmTimeToLive`: esse parâmetro especifica por quanto tempo (em segundos) a mensagem será mantida no armazenamento de GCM se o dispositivo estiver off-line.
- `apnsBadge`: o número a ser exibido como o badge do ícone do aplicativo.
- `apnsCategory`: o identificador de categoria a ser usado para as notificações push interativas.
- `apnsIosActionKey`: o título da chave Ação.
- `apnsPayload`: carga útil de JSON customizada que será enviada como parte da mensagem de notificação.
- `apnsType`: ['DEFAULT', 'MIXED', 'SILENT'].
- `apnsSound`: o nome do arquivo de som no pacote configurável do aplicativo. O som desse arquivo é reproduzido como um alerta.

Aqui está um exemplo de envio de notificação push a partir do pacote pushnotification.

1. Envie notificação push usando a ação `sendMessage` na ligação de pacote anteriormente criada. Certifique-se de substituir `/myNamespace/myPush` pelo nome de seu pacote.

  ```
  wsk action invoke /myNamespace/myPush/sendMessage --blocking --result  -p url https://example.com -p text "this is my message"  -p sound soundFileName -p deviceIds "[\"T1\",\"T2\"]"
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

### Disparando um evento acionador na atividade de Push
{: #openwhisk_catalog_pushnotifications_fire}

O `/whisk.system/pushnotifications/webhook` configura o serviço de
push para disparar um acionador quando houver uma atividade de
dispositivo, como registro/remoção de registro ou assinatura/cancelamento
de assinatura de registro em um aplicativo especificado

Os parâmetros são como segue:

- `appId:` o GUID do app Bluemix.
- `appSecret`: o appSecret do serviço de notificação push do Bluemix.
- `events:` os eventos suportados são `onDeviceRegister`, `onDeviceUnregister`, `onDeviceUpdate`, `onSubscribe`,
`onUnsubscribe`. Para ser notificado de todos os eventos use o caractere curinga `*`.

Segue um exemplo de criação de um acionador que será disparado toda vez que houver um novo dispositivo registrado no aplicativo de serviço de Notificações push.

1. Crie uma ligação de pacote configurada para seu serviço de Notificações push com appId e appSecret.

  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}

2. Crie um acionador para o tipo de evento `onDeviceRegister` do serviço de Notificações push usando o feed `myPush/webhook`.

  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}
