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

# Utilisation du package Watson Speech to Text
{: #openwhisk_catalog_watson_texttospeech}

Le package `/whisk.system/watson-speechToText` permet d'appeler diverses API Watson pour convertir des paroles en texte.

Le package inclut les actions ci-dessous.

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/watson-speechToText` | package | username, password | Package pour la conversion de paroles en texte |
| `/whisk.system/watson-speechToText/speechToText` | action | payload, content_type, encoding, username, password, continuous, inactivity_timeout, interim_results, keywords, keywords_threshold, max_alternatives, model, timestamps, watson-token, word_alternatives_threshold, word_confidence, X-Watson-Learning-Opt-Out | Convertir le contenu audio en texte |

**Remarque** : Le package `/whisk.system/watson` est obsolète, y compris l'action `/whisk.system/watson/speechToText`.

## Configuration du package Watson Speech to Text dans Bluemix

Si vous utilisez OpenWhisk depuis Bluemix, OpenWhisk crée automatiquement des liaisons de package pour vos instances de service Bluemix Watson.

1. Créez une instance de service Watson Speech to Text dans votre [tableau de bord](http://console.ng.Bluemix.net) Bluemix.
  
  Mémorisez le nom de l'instance de service ainsi que l'organisation et l'espace Bluemix dans lesquels vous vous trouvez.
  
2. Actualisez les packages dans votre espace de nom. L'actualisation crée automatiquement une liaison de package pour l'instance de service Watson que vous avez créée.
  
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
  

## Configuration d'un package Watson Speech to Text hors de Bluemix

Si vous n'utilisez pas OpenWhisk dans Bluemix ou si vous voulez configurer Watson Speech to Text hors de Bluemix, vous devez créer une liaison de package manuellement pour votre service Watson Speech to Text. Vous avez besoin du nom d'utilisateur du service et du mot de passe du service Watson Speech to Text.

- Créez une liaison de package configurée pour votre service Watson Speech to Text.
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonSpeechToText -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## Conversion de paroles en texte

L'action `/whisk.system/watson-speechToText/speechToText` convertit un contenu audio en texte. Les paramètres sont les suivants :

- `username` : nom d'utilisateur de l'API Watson.
- `password` : mot de passe de l'API Watson.
- `payload` : données binaires des paroles à convertir en texte.
- `content_type` : type MIME du contenu audio.
- `encoding` : codage du fichier binaire vocal.
- `continuous` : indique si plusieurs résultats finaux représentant des phrases consécutives séparées par de longues pauses doivent être renvoyés.
- `inactivity_timeout` : nombre de secondes après lequel, si seul un silence est détecté dans le contenu audio soumis, la connexion est fermée.
- `interim_results` : indique si le service doit renvoyer des résultats intermédiaires.
- `keywords` : liste de mots clés à rechercher dans le contenu audio.
- `keywords_threshold` : niveau de fiabilité plancher pour l'identification d'un mot clé.
- `max_alternatives` : nombre maximal de transcriptions alternatives à renvoyer.
- `model` : identificateur du modèle à utiliser pour la demande de reconnaissance.
- `timestamps`: indique si l'horodatage doit être renvoyé pour chaque mot.
- `watson-token` : fournit un jeton d'authentification pour le service au lieu des données d'identification au service.
- `word_alternatives_threshold` : niveau de fiabilité plancher pour l'identification d'une hypothèse comme alternative possible d'un mot.
- `word_confidence` : indique si un niveau de fiabilité sur la plage 0 à 1 doit être renvoyé pour chaque mot.
- `X-Watson-Learning-Opt-Out` : indique si la collecte de données doit être ignorée pour l'appel.
 

- Appelez l'action `speechToText` dans votre liaison de package pour convertir le contenu audio codé.
  
  ```
  wsk action invoke myWatsonSpeechToText/speechToText --blocking --result --param payload <base64 encoding of a .wav file> --param content_type 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```json
    {
    "data": "Hello Watson"
  }
  ```
  
