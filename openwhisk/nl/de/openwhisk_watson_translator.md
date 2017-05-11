---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Watson Translator-Paket verwenden
{: #openwhisk_catalog_watson_translator}

Das Paket `/whisk.system/watson-translator` bietet eine komfortable Methode zum Aufrufen der Watson-APIs für die Übersetzung.

Das Paket enthält die folgenden Aktionen.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/watson-translator` | Paket | username, password | Paket für Textübersetzung und Spracherkennung  |
| `/whisk.system/watson-translator/translator` | Aktion | payload, translateFrom, translateTo, translateParam, username, password | Übersetzung von Text |
| `/whisk.system/watson-translator/languageId` | Aktion | payload, username, password | Ermittlung einer Sprache |

**Hinweis:** Das Paket `/whisk.system/watson` wird einschließlich der Aktionen `/whisk.system/watson/translate` und `/whisk.system/watson/languageId` nicht mehr verwendet.

## Watson Translator-Paket in Bluemix einrichten

Wenn Sie OpenWhisk von Bluemix verwenden, dann erstellt OpenWhisk automatisch Paketbindungen für Ihre Bluemix-Watson-Serviceinstanzen.

1. Erstellen Sie eine Watson Translator-Serviceinstanz in Ihrem Bluemix-[Dashboard](http://console.ng.Bluemix.net).
  
  Stellen Sie sicher, dass Sie sich den Namen der Serviceinstanz sowie der Bluemix-Organisation und den Bereich merken, in dem Sie sich befinden.
  
2. Aktualisieren Sie die Pakete in Ihrem Namensbereich. Die Aktualisierung erstellt automatisch eine Paketbindung für die Watson-Serviceinstanz, die Sie erstellt haben.
  
  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_Translator_Credentials-1
  ```
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_Translator_Credentials-1 private
  ```
  
  
## Watson Translator-Paket außerhalb von Bluemix einrichten

Wenn Sie OpenWhisk nicht in Bluemix verwenden oder wenn Sie Watson Translator außerhalb von Bluemix einrichten möchten, müssen Sie manuell eine Paketbindung für Ihren Watson Translator-Service erstellen. Sie benötigen hierzu den Benutzernamen und das Kennwort des Watson Translator-Service.

- Erstellen Sie eine Paketbindung, die für Ihren Watson Translator-Service konfiguriert ist.

  ```
  wsk package bind /whisk.system/watson-translator myWatsonTranslator -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


## Text übersetzen

Die Aktion `/whisk.system/watson-translator/translator` übersetzt Text aus einer Sprache in eine andere. Die folgenden Parameter sind verfügbar:

- `username`: Der Benutzername für die Watson-API.
- `password`: Das Kennwort für die Watson-API.
- `payload`: Der zu übersetzende Text.
- `translateParam`: Der Eingabeparameter, der den zu übersetzenden Text angibt. Beispiel: Wenn `translateParam=payload` angegeben wird, wird der Wert des Parameters `payload`, der an die Aktion übergeben wird, übersetzt.
- `translateFrom`: Ein zweistelliger Code für die Ausgangssprache.
- `translateTo`: Ein zweistelliger Code für die Zielsprache.

- Rufen Sie die Aktion `translator` in Ihrer Paketbindung auf, um einen Text aus dem Englischen ins Französische zu übersetzen.
  
  ```
  wsk action invoke myWatsonTranslator/translator \
  --blocking --result \
  --param payload "Blue skies ahead" --param translateFrom "en" \
  --param translateTo "fr"
  ```
  {: pre}
  ```json
  {
      "payload": "Ciel bleu a venir"
  }
  ```
  
  
## Sprache eines Texts ermitteln

Die Aktion `/whisk.system/watson-translator/languageId` ermittelt die Sprache eines Texts. Die folgenden Parameter sind verfügbar:

- `username`: Der Benutzername für die Watson-API.
- `password`: Das Kennwort für die Watson-API.
- `payload`: Der zu ermittelnde Text.

- Rufen Sie die Aktion `languageId` in Ihrer Paketbindung auf, um die Sprache zu ermitteln.
  
  ```
  wsk action invoke myWatsonTranslator/languageId \
  --blocking --result \
  --param payload "Ciel bleu a venir"
  ```
  {: pre}
  ```json
  {
    "payload": "Ciel bleu a venir",
    "language": "fr",
    "confidence": 0.710906
  }
  ```
  
