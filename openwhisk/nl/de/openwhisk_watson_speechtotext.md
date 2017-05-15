---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Watson-Paket 'Speech to Text' verwenden
{: #openwhisk_catalog_watson_texttospeech}

Das Paket `/whisk.system/watson-speechToText` bietet eine komfortable Methode zum Aufrufen der Watson-APIs für die Konvertierung von Sprache in Text.

Das Paket enthält die folgenden Aktionen.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/watson-speechToText` | Paket | username, password | Paket zum Umwandeln von Sprache in Text |
| `/whisk.system/watson-speechToText/speechToText` | Aktion | payload, content_type, encoding, username, password, continuous, inactivity_timeout, interim_results, keywords, keywords_threshold, max_alternatives, model, timestamps, watson-token, word_alternatives_threshold, word_confidence, X-Watson-Learning-Opt-Out | Umsetzung von Sprache in Text |

**Hinweis:** Das Paket `/whisk.system/watson` wird einschließlich der Aktion `/whisk.system/watson/speechToText` nicht mehr verwendet.

## Watson-Paket 'Speech to Text' in Bluemix einrichten

Wenn Sie OpenWhisk von Bluemix verwenden, dann erstellt OpenWhisk automatisch Paketbindungen für Ihre Bluemix-Watson-Serviceinstanzen.

1. Erstellen Sie eine Watson-Serviceinstanz für 'Speech to Text' in Ihrem Bluemix-[Dashboard](http://console.ng.Bluemix.net).
  
  Stellen Sie sicher, dass Sie sich den Namen der Serviceinstanz sowie der Bluemix-Organisation und den Bereich merken, in dem Sie sich befinden.
  
2. Aktualisieren Sie die Pakete in Ihrem Namensbereich. Die Aktualisierung erstellt automatisch eine Paketbindung für die Watson-Serviceinstanz, die Sie erstellt haben.
  
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
  

## Watson-Paket 'Speech to Text' außerhalb von Bluemix einrichten

Wenn Sie OpenWhisk nicht in Bluemix verwenden oder wenn Sie den Watson-Service 'Speech to Text' außerhalb von Bluemix einrichten möchten, müssen Sie manuell eine Paketbindung für Ihren Watson-Service 'Speech to Text' erstellen. Sie benötigen hierzu den Benutzernamen und das Kennwort des Watson-Service 'Speech to Text'.

- Erstellen Sie eine Paketbindung, die für Ihren Watson-Service 'Text to Speech' konfiguriert ist.
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonSpeechToText -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## Umsetzung von Sprache in Text

Mit der Aktion `/whisk.system/watson-speechToText/speechToText` kann eine Audioansage in Text konvertiert werden. Die folgenden Parameter sind verfügbar:

- `username`: Der Benutzername für die Watson-API.
- `password`: Das Kennwort für die Watson-API.
- `payload`: Die codierten binären Sprachdaten, die in Text umgesetzt werden sollen.
- `content_type`: Der MIME-Typ der Sprachdaten.
- `encoding`: Die Codierung der binären Sprachdaten.
- `continuous`: Gibt an, ob mehrere Endergebnisse, die durch lange Pausen voneinander getrennte aufeinanderfolgende Phrasen darstellen, zurückgegeben werden.
- `inactivity_timeout`: Die Zeit in Sekunden, nach deren Ablauf die Verbindung geschlossen wird, wenn in den übertragenen Sprachdaten nur Stille festgestellt wird.
- `interim_results`: Gibt an, ob der Service Zwischenergebnisse zurückgeben soll.
- `keywords`: Eine Liste der Schlüsselwörter, die in den Sprachdaten erkannt werden sollen.
- `keywords_threshold`: Ein Übereinstimmungswert, der die Untergrenze für die Erkennung eines Schlüsselworts darstellt.
- `max_alternatives`: Die maximale Anzahl alternativer Aufzeichnungen, die zurückgegeben werden sollen.
- `model`: Die Kennung des Modells für die Erkennungsanforderung.
- `timestamps`: Gibt an, ob für jedes Wort Laufzeitkorrekturen (Time Alignment) zurückgegeben werden.
- `watson-token`: Gibt alternativ zu Serviceberechtigungsnachweisen ein Authentifizierungstoken für den Service an.
- `word_alternatives_threshold`: Ein Übereinstimmungswert, der die Untergrenze für die Angabe einer Hypothese als mögliche Wortalternative darstellt.
- `word_confidence`: Gibt an, ob für jedes Wort ein Übereinstimmungswert im Bereich von 0 bis 1 zurückgegeben wird.
- `X-Watson-Learning-Opt-Out`: Gibt an, ob die Datenerfassung für den Aufruf abgelehnt wird.
 

- Rufen Sie die Aktion `speechToText` in Ihrer Paketbindung auf, um die codierten Sprachdaten umzusetzen.
  
  ```
  wsk action invoke myWatsonSpeechToText/speechToText --blocking --result --param payload <base64 encoding of a .wav file> --param content_type 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```json
  {
    "data": "Hello Watson"
  }
  ```
  
