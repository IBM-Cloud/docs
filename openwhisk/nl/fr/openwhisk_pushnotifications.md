---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-01"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilisation du package Push Notifications
{: #openwhisk_catalog_pushnotifications}

Le package `/whisk.system/pushnotifications` vous permet d'utiliser un service push.

Le package inclut l'action et le flux suivants :

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | package | appId, appSecret  | utilisation du service push |
| `/whisk.system/pushnotifications/sendMessage` | action | text, url, deviceIds, platforms, userIds, tagNames, gcmCollapseKey, gcmCategory, gcmIcon, gcmDelayWhileIdle, gcmSync, gcmVisibility, gcmPayload, gcmPriority, gcmSound, gcmTimeToLive, gcmStyleType, gcmStyleTitle, gcmStyleUrl, gcmStyleText, gcmStyleLines, gcmLightsLedArgb, gcmLightsLedOnMs, gcmLightsLedOffMs, apnsBadge, apnsCategory, apnsIosActionKey, apnsPayload, apnsType, apnsSound, apnsTitleLocKey, apnsLocKey, apnsLaunchImage, apnsTitleLocArgs, apnsLocArgs, apnstitle, apnsSubtitle, apnsAttachmentUrl, fireFoxTitle, fireFoxIconUrl, fireFoxTimeToLive, fireFoxPayload, safariTitle, safariUrlArgs, safariAction, chromeTitle, chromeIconUrl, chromeTimeToLive, chromePayload, chromeAppExtTitle, chromeAppExtCollapseKey, chromeAppExtDelayWhileIdle, chromeAppExtIconUrl, chromeAppExtTimeToLive, chromeAppExtPayload | Envoi de notification push à un ou plusieurs périphérique(s) spécifié(s) |
| `/whisk.system/pushnotifications/webhook` | flux | events | Exécution d'événements déclencheur sur des activités de périphérique (enregistrement, annulation d'enregistrement, abonnement ou annulation d'abonnement de périphérique) sur le service Push |
Il est recommandé de créer une liaison de package avec les valeurs `appId` et `appSecret`. Ainsi, il n'est pas nécessaire de spécifier ces données d'identification à chaque fois que vous appelez les actions du package.

## Création d'une liaison de package Push
{: #openwhisk_catalog_pushnotifications_create}

Lors de la création d'une liaison de package Notifications push, vous devez spécifier les paramètres suivants :

-  `appId` : Identificateur global unique d'application Bluemix.
-  `appSecret` : Valeur confidentielle d'application du service de notification push Bluemix.

Voici un exemple de création d'une liaison de package.

1. Créez une application Bluemix dans le [tableau de bord Bluemix](http://console.ng.bluemix.net).

2. Initialisez le service de notification push et liez celui-ci à l'application Bluemix.

3. Configurez l'[application de notification push](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

  Prenez soin de mémoriser l'`identificateur global unique d'application` et la `valeur confidentielle d'application` de l'application Bluemix que vous avez créée.

4. Créez une liaison de package avec `/whisk.system/pushnotifications`.

  ```
  wsk package bind /whisk.system/pushnotifications monPush -p appId monIDApp -p appSecret maValeurConfApp
  ```
  {: pre}
  
5. Vérifiez que la liaison de package existe.

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /nomEspaceNom/monPush private binding
  ```


## Envoi de notifications push
{: #openwhisk_catalog_pushnotifications_send}

L'action `/whisk.system/pushnotifications/sendMessage` envoie des notifications push à des périphériques enregistrés. Les paramètres sont les suivants :

- `text` : message de notification à présenter à l'utilisateur. Par exemple : `-p text "Bonjour, OpenWhisk a envoyé une
notification"`.
- `url` : URL facultative qui peut être envoyée en même temps que l'alerte. Par exemple : `-p url "https:\\www.w3.ibm.com"`.
- `deviceIds` : liste des périphériques spécifiés. Exemple : `-p deviceIds ["deviceID1"]`.
- `platforms` : envoyez une notification aux périphériques des plateformes spécifiées. 'A' pour les périphériques Apple (iOS) et 'G' pour les périphériques Google (Android). Exemple : `-p platforms ["A"]`.
- `userIds` : envoyez une notification aux périphériques des utilisateurs spécifiés. Exemple : `-p id_utilisateur "[\"testUser\"]"`
- `tagNames` : envoyez une notification aux périphériques abonnés à l'une des étiquettes spécifiées. Exemple : `-p tagNames "[\"étiquette1\"]" `.

- `gcmCollapseKey` : ce paramètre identifie un groupe de messages
- `gcmCategory` : identificateur de catégorie à utiliser pour les notifications push interactives.
- `gcmIcon` : spécifiez le nom de l'icône à afficher pour la notification. Assurez-vous que l'icône est déjà conditionnée avec l'application client. 
- `gcmDelayWhileIdle` : lorsque ce paramètre a pour valeur true, il indique que le message ne doit pas être envoyé tant que le périphérique n'est pas actif.
- `gcmSync` : la messagerie de groupe de périphériques permet à chaque instance d'application d'un groupe de refléter le dernier état de messagerie.
- `gcmVisibility` : privé/public - visibilité de cette notification, qui affecte comment et quand les notifications sont révélées sur un écran verrouillé.
- `gcmPayload` : contenu JSON personnalisé qui sera envoyé dans le cadre du message de notification. Exemple : `-p gcmPayload "{\"Salut\":\"Bonjour\"}"`
- `gcmPriority` : définit la priorité du message.
- `gcmSound` : fichier son (sur le périphérique) qui est utilisé lorsque la notification arrive sur le périphérique.
- `gcmTimeToLive` : ce paramètre spécifie le nombre de secondes pendant lesquelles le message doit être conservé dans le stockage GCM si le périphérique est hors ligne.
- `gcmStyleType` : spécifie les types de notification pouvant être développés. Les valeurs possibles sont `bigtext_notification`, `picture_notification`, `inbox_notification`.
- `gcmStyleTitle` : spécifie le titre de la notification. Le titre s'affiche lorsque la notification est développée. Un titre doit être spécifié pour les trois notifications pouvant être développées.
- `gcmStyleUrl` : URL à partir de laquelle l'image doit être obtenue pour la notification. Elle doit être spécifiée pour `picture_notification`.
- `gcmStyleText` : grand texte qui doit être affiché sur une notification `bigtext_notification` pouvant être développée. Il doit être spécifié pour `bigtext_notification`.
- `gcmStyleLines` : tableau de chaînes qui doit être affiché dans le style boîte de réception pour `inbox_notification`. Il doit être spécifié pour `inbox_notification`.
- `gcmLightsLedArgb` : couleur du voyant. Le matériel utilisera sa meilleure approximation.
- `gcmLightsLedOnMs` : durée en millisecondes pendant laquelle le voyant reste allumé lorsqu'il clignote. Le matériel utilisera sa meilleure approximation.
- `gcmLightsLedOffMs` : durée en millisecondes pendant laquelle le voyant reste éteint lorsqu'il clignote. Le matériel utilisera sa meilleure approximation.

- `apnsBadge` : numéro à afficher en tant que badge de l'icône d'application.
- `apnsCategory` : identificateur de catégorie à utiliser pour les notifications push interactives.
- `apnsIosActionKey` : titre de la clé d'action.
- `apnsPayload` : contenu JSON personnalisé qui sera envoyé dans le cadre du message de notification.
- `apnsType` : ['DEFAULT', 'MIXED', 'SILENT'].
- `apnsSound` : nom du fichier son dans l'ensemble d'applications. Le son de ce fichier est utilisé pour une alerte.
- `apnsTitleLocKey` : clé d'une chaîne de titre dans le fichier Localizable.strings pour la localisation en cours. La chaîne de clé peut être formatée avec les spécificateurs %@ et %n$@ pour inclure les variables spécifiées dans le tableau `titleLocArgs`. 
- `apnsLocKey` : clé d'une chaîne de message d'alerte dans un fichier Localizable.strings pour la localisation en cours (définie par la préférence de langue de l'utilisateur). La chaîne de clé peut être formatée avec les spécificateurs %@ et %n$@ pour inclure les variables spécifiées dans le tableau locArgs. 
- `apnsLaunchImage` : nom d'un fichier image dans le bundle d'application, avec ou sans extension de nom de fichier. L'image est utilisée comme image de lancement lorsque les utilisateurs appuient sur le bouton d'action ou déplacement le curseur d'action.
- `pnsTitleLocArgs` : valeurs de chaîne variables devant apparaître à la place des spécificateurs de format dans `title-loc-key`.
- `apnsLocArgs` : valeurs de chaîne variables devant apparaître à la place des spécificateurs de format dans `locKey`.
- `apnstitle` : titre des notifications push Rich (pris en charge sous iOS 10 et versions ultérieures uniquement). 
- `apnsSubtitle` : sous-titre des notifications push riches (pris en charge sous iOS 10 et versions ultérieures uniquement). 
- `apnsAttachmentUrl` : lien vers le support des notifications iOS (vidéo, audio, GIF, images - pris en charge sous iOS 10 et versions ultérieures uniquement). 

- `fireFoxTitle` : spécifie le titre qui doit être défini pour WebPush Notification.
- `fireFoxIconUrl` : URL de l'icône qui doit être définie pour WebPush Notification.
- `fireFoxTimeToLive` : ce paramètre spécifie la durée de conservation (exprimée en secondes) du message dans le stockage GCM si le périphérique est hors ligne.
- `fireFoxPayload` : contenu JSON personnalisé qui est envoyé dans le cadre du message de notification.

- `chromeTitle` : spécifie le titre qui doit être défini pour WebPush Notification.
- `chromeIconUrl` : URL de l'icône qui doit être définie pour WebPush Notification.
- `chromeTimeToLive` : ce paramètre spécifie la durée de conservation (exprimée en secondes) du message dans le stockage GCM si le périphérique est hors ligne.
- `chromePayload` : contenu JSON personnalisé qui est envoyé dans le cadre du message de notification.

- `safariTitle` : spécifie le titre à définir pour les notifications push Safari. 
- `safariUrlArgs` : arguments d'URL à utiliser avec cette notification. Ils doivent être fournis sous la forme d'un tableau JSON. 
- `safariAction` : libellé du bouton d'action. 

- `chromeAppExtTitle` : spécifie le titre qui doit être défini pour WebPush Notification.
- `chromeAppExtCollapseKey` : ce paramètre identifie un groupe de messages.
- `chromeAppExtDelayWhileIdle` : lorsque ce paramètre a pour valeur true, il indique que le message ne doit pas être envoyé tant que le périphérique n'est pas actif.
- `chromeAppExtIconUrl` : URL de l'icône qui doit être définie pour WebPush Notification.
- `chromeAppExtTimeToLive` : ce paramètre spécifie la durée de conservation (exprimée en secondes) du message dans le stockage GCM si le périphérique est hors ligne.
- `chromeAppExtPayload` : contenu JSON personnalisé qui est envoyé dans le cadre du message de notification.

Voici un exemple d'envoi d'une notification push depuis le package *pushnotification*.

- Envoyez une notification push à l'aide de l'action `sendMessage` dans la liaison de package que vous avez créée précédemment. Prenez soin de remplacer `/nomEspaceNom/monPush` par votre nom de package.

  ```
  wsk action invoke /nomEspaceNom/monPush/sendMessage --blocking --result  -p url https://exemple.com -p text "ceci est mon message"  -p sound
nomFichierSon -p deviceIds "[\"T1\",\"T2\"]"
  ```
  {: pre}
  ```json
    {
    "result": {
    "pushResponse": 
      {
        "messageId":"11111H",
        "message":{
          "alert":"this is my message",
          "url":""
        },
        "settings":{
          "apns":{
            "sound":"default"
          },
          "gcm":{
            "sound":"default"
            },
          "target":{
            "deviceIds":["T1","T2"]
          }
        }
      }
    },
      "status": "success",
      "success": true
  }
  ```


## Exécution d'un événement déclencheur sur une activité de service Push Notifications
{: #openwhisk_catalog_pushnotifications_fire}

`/whisk.system/pushnotifications/webhook` configure le service Push pour qu'il exécute un déclencheur lorsqu'il existe une activité de périphérique, telle qu'un enregistrement ou une annulation d'enregistrement ou un abonnement ou une annulation d'abonnement de périphérique dans une application spécifiée.

Les paramètres sont les suivants :

- `appId :` identificateur global unique d'application Bluemix.
- `appSecret :` valeur confidentielle d'application du service de notification push Bluemix.
- `events :` les événements pris en charge sont `onDeviceRegister`, `onDeviceUnregister`, `onDeviceUpdate`, `onSubscribe`, `onUnsubscribe`. Pour être avertis de tous les événements, utilisez le caractère générique `*`.

Voici un exemple de création d'un déclencheur qui sera exécuté chaque fois qu'un nouveau périphérique est enregistré avec l'application Push Notifications :

1. Créez une liaison de package configurée pour votre service Push Notifications avec vos paramètres appId et appSecret.

  ```
  wsk package bind /whisk.system/pushnotifications monNouveauFluxPériphérique --param appID monapp --param appSecret mavaleurconfapp --param
events onDeviceRegister
  ```
  {: pre}

2. Créez un déclencheur pour le type d'événement `onDeviceRegister` du service Push Notifications en utilisant votre flux `monPush/webhook`.

  ```
  wsk trigger create monDéclencheurPush --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}

3. Vous pouvez créer une règle qui envoie un message à chaque fois qu'un nouveau périphérique est enregistré. Créez une règle à l'aide de l'action et du déclencheur précédents.

  ```
  wsk rule create --enable myRule myPushTrigger sendMessage
  ```
  {: pre}

  Vérifiez les résultats dans `wsk activation poll`.

  Enregistrez un périphérique dans votre application Bluemix. Vous pouvez voir l'exécution de la `règle`, du `déclencheur` et de l'`action` dans openWhisk [dashboard] (https://console.{Domain}/openwhisk/dashboard).

  L'action enverra une notification push.

