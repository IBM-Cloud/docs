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

# Utilisation du package Watson Text to Speech
{: #openwhisk_catalog_watson_texttospeech}

Le package `/whisk.system/watson-textToSpeech` permet d'appeler diverses API Watson pour convertir le texte en parole.

Le package inclut les actions ci-dessous.

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | package | username, password | Package pour la conversion de texte en paroles |
| `/whisk.system/watson-textToSpeech/textToSpeech` | action | payload, voice, accept, encoding, username, password | Convertir le texte en contenu audio |

**Remarque** : Le package `/whisk.system/watson` est obsolète, y compris l'action `/whisk.system/watson/textToSpeech`.

## Configuration du package Watson Text to Speech dans Bluemix

Si vous utilisez OpenWhisk depuis Bluemix, OpenWhisk crée automatiquement des liaisons de package pour vos instances de service Bluemix Watson.

1. Créez une instance de service Watson Text to Speech dans votre [tableau de bord](http://console.ng.Bluemix.net) Bluemix.
  
  Mémorisez le nom de l'instance de service ainsi que l'organisation et l'espace Bluemix dans lesquels vous vous trouvez.
  
2. Actualisez les packages dans votre espace de nom. L'actualisation crée automatiquement une liaison de package pour l'instance de service Watson que vous avez créée.
  
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
  
  
## Configuration d'un package Watson Text to Speech hors de Bluemix

Si vous n'utilisez pas OpenWhisk dans Bluemix ou si vous voulez configurer Watson Text to Speech hors de Bluemix, vous devez créer une liaison de package manuellement pour votre service Watson Text to Speech. Vous avez besoin du nom d'utilisateur du service et du mot de passe du service Watson Text to Speech.

- Créez une liaison de package configurée pour votre service Watson Speech to Text.
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## Conversion de texte en paroles

L'action `/whisk.system/watson-speechToText/textToSpeech` convertit du texte en contenu audio. Les paramètres sont les suivants :

- `username` : nom d'utilisateur de l'API Watson.
- `password` : mot de passe de l'API Watson.
- `payload` : texte à convertir en paroles.
- `voice` : voix du conférencier.
- `accept` : format du fichier vocal.
- `encoding` : codage du fichier binaire vocal.


- Appelez l'action `textToSpeech` dans votre liaison de package pour convertir le texte.
  
  ```
  wsk action invoke myWatsonTextToSpeech/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```json
    {
    "payload": "<Codage en base 64 d'un fichier .wav>"
  }
  ```
  
