---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Usando o pacote de Texto do Watson para Fala
{: #openwhisk_catalog_watson_texttospeech}

O pacote `/whisk.system/watson-textToSpeech` oferece uma maneira conveniente de chamar APIs do Watson para converter o texto em fala.

O pacote inclui as ações a seguir.

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | pacote | username, password | Pacote para converter texto em fala |
| `/whisk.system/watson-textToSpeech/textToSpeech` | ação | payload, voice, accept, encoding, username, password | Converter texto em áudio |

**Nota**: o pacote `/whisk.system/watson` está descontinuado, incluindo a ação `/whisk.system/watson/textToSpeech`.

## Usando o pacote de Texto do Watson para Fala no Bluemix

Se você estiver usando o OpenWhisk a partir do Bluemix, o OpenWhisk criará automaticamente as ligações de pacote para as suas instâncias de serviço do Watson
do Bluemix.

1. Crie uma instância de serviço de Texto do Watson para Fala em seu [painel](http://console.ng.Bluemix.net) do Bluemix.
  
  Certifique-se de lembrar do nome da instância de serviço e da organização e do espaço do Bluemix nos quais você está.
  
2. Atualize os pacotes em seu namespace. A atualização cria automaticamente uma ligação de pacote para a instância de serviço do Watson que você criou.
  
  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_TextToSpeech_Credentials-1
  ```
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_TextToSpeec_Credentials-1 private
  ```
  
  
## Configurando um pacote de Texto do Watson para Fala fora do Bluemix

Se você não estiver usando o OpenWhisk no Bluemix ou se desejar configurar o seu Texto do Watson para Fala fora do Bluemix, deverá criar manualmente uma ligação
de pacote para o seu serviço de Texto do Watson para Fala. Você precisa do nome do usuário e da senha do serviço de Texto do Watson para Fala.

- Crie uma ligação de pacote que esteja configurada para o seu serviço de Fala do Watson para Texto.
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## Converter algum texto para fala

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
  ```json
     {
    "payload": "<base64 encoding of a .wav file>"
  }
  ```
  
