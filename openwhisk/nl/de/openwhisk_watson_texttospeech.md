---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Watson-Paket 'Text to Speech' verwenden
{: #openwhisk_catalog_watson_texttospeech}

Das Paket `/whisk.system/watson-textToSpeech` bietet eine komfortable Methode zum Aufrufen der Watson-APIs für die Konvertierung von Text in Sprache.

Das Paket enthält die folgenden Aktionen.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | Paket | username, password | Paket zum Umwandeln von Text in Sprache |
| `/whisk.system/watson-textToSpeech/textToSpeech` | Aktion | payload, voice, accept, encoding, username, password | Umsetzung von Text in Sprache |

**Hinweis:** Das Paket `/whisk.system/watson` wird einschließlich der Aktion `/whisk.system/watson/textToSpeech` nicht mehr verwendet.

## Watson-Paket 'Text to Speech' in Bluemix einrichten

Wenn Sie OpenWhisk von Bluemix verwenden, dann erstellt OpenWhisk automatisch Paketbindungen für Ihre Bluemix-Watson-Serviceinstanzen.

1. Erstellen Sie eine Watson-Serviceinstanz für 'Text to Speech' in Ihrem Bluemix-[Dashboard](http://console.ng.Bluemix.net).
  
  Stellen Sie sicher, dass Sie sich den Namen der Serviceinstanz sowie der Bluemix-Organisation und den Bereich merken, in dem Sie sich befinden.
  
2. Aktualisieren Sie die Pakete in Ihrem Namensbereich. Die Aktualisierung erstellt automatisch eine Paketbindung für die Watson-Serviceinstanz, die Sie erstellt haben.
  
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
  
  
## Watson-Paket 'Text to Speech' außerhalb von Bluemix einrichten

Wenn Sie OpenWhisk nicht in Bluemix verwenden oder wenn Sie den Watson-Service 'Text to Speech' außerhalb von Bluemix einrichten möchten, müssen Sie manuell eine Paketbindung für Ihren Watson-Service 'Text to Speech' erstellen. Sie benötigen hierzu den Benutzernamen und das Kennwort des Watson-Service 'Text to Speech'.

- Erstellen Sie eine Paketbindung, die für Ihren Watson-Service 'Text to Speech' konfiguriert ist.
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## Umsetzung von Text in Sprache

Mit der Aktion `/whisk.system/watson-speechToText/textToSpeech` kann Text in eine Audioansage konvertiert werden. Die folgenden Parameter sind verfügbar:

- `username`: Der Benutzername für die Watson-API.
- `password`: Das Kennwort für die Watson-API.
- `payload`: Der Text, der in Sprache umgesetzt werden soll.
- `voice`: Die Stimme des Sprechers.
- `accept`: Das Format der Sprachdatei.
- `encoding`: Die Codierung der binären Sprachdaten.


- Rufen Sie die Aktion `textToSpeech` in Ihrer Paketbindung auf, um den Text umzusetzen.
  
  ```
  wsk action invoke myWatsonTextToSpeech/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```json
  {
    "payload": "<base64 encoding of a .wav file>"
  }
  ```
  
