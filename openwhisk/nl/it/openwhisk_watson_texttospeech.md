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

# Utilizzo del pacchetto Watson Text to Speech
{: #openwhisk_catalog_watson_texttospeech}

Il pacchetto `/whisk.system/watson-textToSpeech` offre una soluzione pratica per richiamare le diverse API Watson per la conversione da testo a voce.

Il pacchetto include le seguenti azioni.

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | pacchetto | username, password | Pacchetto per convertire il testo in voce |
| `/whisk.system/watson-textToSpeech/textToSpeech` | azione | payload, voice, accept, encoding, username, password | Convertire testo in audio |

**Nota**: il pacchetto `/whisk.system/watson` è obsoleto, inclusa l'azione `/whisk.system/watson/textToSpeech`.

## Configurazione del pacchetto Watson Text to Speech in Bluemix

Se stai utilizzando OpenWhisk da Bluemix, OpenWhisk crea automaticamente i bind di pacchetto per le tue istanze del servizio Bluemix Watson.

1. Crea un'istanza del servizio Watson Text to Speech nel tuo [dashboard](http://console.ng.Bluemix.net) Bluemix.
  
  Assicurati di ricordare il nome dell'istanza del servizio e dell'organizzazione e dello spazio Bluemix in cui ti trovi.
  
2. Aggiorna i pacchetti nel tuo spazio dei nomi. L'aggiornamento crea automaticamente un bind di pacchetto per l'istanza del servizio Watson da te creata.
  
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
  
  
## Configurazione del pacchetto Watson Text to Speech esternamente a Bluemix

Se non stai utilizzando OpenWhisk in Bluemix o se vuoi configurare Watson Text to Speech esternamente a Bluemix, devi creare manualmente un bind di pacchetto per il tuo servizio Watson Text to Speech. Ti servono il nome utente e la password del servizio Watson Text to Speech.

- Crea un bind di pacchetto configurato per il tuo servizio Watson Speech to Text.
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## Conversione da testo a voce

L'azione `/whisk.system/watson-speechToText/textToSpeech` converte un testo in audio. I parametri sono i seguenti:

- `username`: il nome utente dell'API Watson API.
- `password`: la password della API Watson.
- `payload`: il testo da convertire in voce.
- `voice`: la voce dello speaker.
- `accept`: il formato del file audio.
- `encoding`: la codifica dei dati binari del file audio.


- Richiama l'azione `textToSpeech` nel tuo bind di pacchetto per convertire il testo.
  
  ```
  wsk action invoke myWatsonTextToSpeech/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```json
  {
    "payload": "<base64 encoding of a .wav file>"
  }
  ```
  
