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

# Usando o pacote de Fala do Watson para Texto
{: #openwhisk_catalog_watson_texttospeech}

O pacote `/whisk.system/watson-speechToText` oferece uma maneira conveniente de chamar APIs do Watson para converter a fala em texto.

O pacote inclui as ações a seguir.

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/watson-speechToText` | pacote | username, password | Pacote para converter fala em texto |
| `/whisk.system/watson-speechToText/speechToText` | ação | payload, content_type, encoding, username, password, continuous, inactivity_timeout, interim_results, keywords, keywords_threshold, max_alternatives, model, timestamps, watson-token, word_alternatives_threshold, word_confidence, X-Watson-Learning-Opt-Out | Converter
áudio em texto |

**Nota**: o pacote `/whisk.system/watson` está descontinuado, incluindo a ação `/whisk.system/watson/speechToText`.

## Configurando o pacote de Fala do Watson para Texto no Bluemix

Se você estiver usando o OpenWhisk a partir do Bluemix, o OpenWhisk criará automaticamente as ligações de pacote para as suas instâncias de serviço do Watson
do Bluemix.

1. Crie uma instância de serviço de Fala do Watson para Texto em seu [painel](http://console.ng.Bluemix.net) do Bluemix.
  
  Certifique-se de lembrar do nome da instância de serviço e da organização e do espaço do Bluemix nos quais você está.
  
2. Atualize os pacotes em seu namespace. A atualização cria automaticamente uma ligação de pacote para a instância de serviço do Watson que você criou.
  
  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_SpeechToText_Credentials-1
  ```
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_SpeechToText_Credentials-1 private
  ```
  

## Configurando um pacote de Fala do Watson para Texto fora do Bluemix

Se você não estiver usando o OpenWhisk no Bluemix ou se desejar configurar a sua Fala do Watson para Texto fora do Bluemix, deverá criar manualmente uma ligação de
pacote para o seu serviço de Fala do Watson para Texto. Você precisa do nome do usuário e da senha do serviço de Fala do Watson para Texto.

- Crie uma ligação de pacote que esteja configurada para o seu serviço de Fala do Watson para Texto.
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonSpeechToText -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## Convertendo fala para texto

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
  ```json
     {
    "data": "Hello Watson"
  }
  ```
  
