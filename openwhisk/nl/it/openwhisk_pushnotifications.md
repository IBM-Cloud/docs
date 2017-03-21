---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilizzo del pacchetto Push Notifications
{: #openwhisk_catalog_pushnotifications}

Il pacchetto `/whisk.system/pushnotifications` ti consente di lavorare con un servizio push.

Il pacchetto include l'azione e il feed che seguono:

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | pacchetto | appId, appSecret  | Lavorare con il servizio push |
| `/whisk.system/pushnotifications/sendMessage` | azione | text, url, deviceIds, platforms, tagNames, gcmPayload, gcmSound, gcmCollapseKey, gcmDelayWhileIdle, gcmPriority, gcmTimeToLive, gcmSync, gcmVisibility, gcmStyleType, gcmStyleTitle, gcmStyleUrl, gcmStyleText, gcmStyleLines, apnsBadge, apnsCategory, apnsIosActionKey, apnsPayload, apnsType, apnsSound, fireFoxTitle, fireFoxIconUrl, fireFoxTimeToLive, fireFoxPayload, chromeTitle, chromeIconUrl, chromeTimeToLive, chromePayload, chromeAppExtTitle, chromeAppExtCollapseKey, chromeAppExtDelayWhileIdle, chromeAppExtIconUrl, chromeAppExtTimeToLive, chromeAppExtPayload | Invia notifica di push a uno o più dispositivi specificati |
| `/whisk.system/pushnotifications/webhook` | feed | events | Attiva gli eventi trigger sulle attività del dispositivo (registrazione, annullamento della registrazione, sottoscrizione o annullamento della sottoscrizione del dispositivo) sul servizio Push |
Si consiglia di effettuare la creazione di un bind di pacchetto con i valori `appId` e `appSecret`. In questo modo, non dovrai specificare queste credenziali ogni volta che richiami le azioni nel pacchetto.

## Creazione di un bind di pacchetto Push
{: #openwhisk_catalog_pushnotifications_create}

Durante la creazione di un bind di pacchetto Notifiche di push, devi specificare i seguenti parametri:

-  `appId`: il GUID dell'applicazione Bluemix.
-  `appSecret`: l'appSecret del servizio di notifica push Bluemix.

Il seguente è un esempio di creazione di un bind di pacchetto.

1. Crea un'applicazione Bluemix nel [Dashboard Bluemix](http://console.ng.bluemix.net).

2. Inizializza il servizio di notifica push ed esegui il bind del servizio all'applicazione Bluemix.

3. Configura l'[applicazione Notifica di push](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).
  
  Assicurati di ricordare il `GUID applicazione` e il `Segreto applicazione` dell'applicazione Bluemix che hai creato.
  
4. Crea un bind al pacchetto con `/whisk.system/pushnotifications`.
  
  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId myAppID -p appSecret myAppSecret
  ```
  {: pre}
  
5. Verifica che il bind di pacchetto esista.
  
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myNamespace/myPush private binding
  ```
  

## Invio di notifiche di push
{: #openwhisk_catalog_pushnotifications_send}

L'azione `/whisk.system/pushnotifications/sendMessage` invia notifiche push ai dispositivi registrati. I parametri sono i seguenti:
- `text`: il messaggio della notifica visualizzato dall'utente. Ad esempio: `-p text "Hi ,OpenWhisk send a notification"`.
- `url`: un URL facoltativo che può essere inviato con l'avviso. Ad esempio: `-p url "https:\\www.w3.ibm.com"`.
- `deviceIds`: l'elenco di dispositivi specificati. Ad esempio: `-p deviceIds ["deviceID1"]`.
- `platforms`: invia notifiche ai dispositivi delle piattaforme specificate. 'A' per i dispositivi Apple (iOS) e 'G' per i dispositivi Google (Android). Ad esempio `-p platforms ["A"]`.
- `tagNames`:  invia notifiche ai dispositivi sottoscritti a una di queste tag. Ad esempio `-p tagNames "[\"tag1\"]" `.
- `gcmPayload`: payload JSON personalizzato che verrà inviato come parte del messaggio di notifica. Ad esempio: `-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmSound`: il file audio (sul dispositivo) che tenterà di essere eseguito quando la notifica arriva al dispositivo.
- `gcmCollapseKey`: questo parametro identifica un gruppo di messaggi.
- `gcmDelayWhileIdle`: quando questo parametro è impostato su true, indica che il messaggio non verrà inviato finché il dispositivo non diventa attivo.
- `gcmPriority`: imposta la priorità del messaggio.
- `gcmTimeToLive`: questo parametro specifica per quanto tempo (in secondi) il messaggio viene conservato nella memoria GCM se il dispositivo è offline.
- `gcmSync`: la messaggistica del gruppo di dispositivi consente a ogni istanza dell'applicazione di rispecchiare lo stato più recente della messaggistica.
- `gcmVisibility`: privato/pubblico - Visibilità di questa notifica che può influire sul quando e come vengono mostrate le notifiche su uno schermo bloccato protetto.
- `gcmStyleType`: specifica il tipo di notifiche espandibili. I valori possibili sono `bigtext_notification`, `picture_notification`, `inbox_notification`.
- `gcmStyleTitle`: specifica il titolo della notifica. Il titolo viene visualizzato quando si espande la notifica. Il titolo deve essere specificato per tutte le tre notifiche espandibili.
- `gcmStyleUrl`: un URL da cui deve essere ottenuta l'immagine per la notifica. Deve essere specificato per picture_notification.
- `gcmStyleText`: il testo di grandi dimensioni che deve essere visualizzato quando si espande una bigtext_notification. Deve essere specificato per bigtext_notification.
- `gcmStyleLines`: un array di stringhe che deve essere visualizzato in stile posta in arrivo per inbox_notification. Deve essere specificato per inbox_notification.
- `apnsBadge`: il numero da visualizzare come badge dell'icona dell'applicazione.
- `apnsCategory`: l'identificativo della categoria da utilizzare per le notifiche di push interattive.
- `apnsIosActionKey`: il titolo per la chiave Azione.
- `apnsPayload`: payload JSON personalizzato che verrà inviato come parte del messaggio di notifica.
- `apnsType`: ['DEFAULT', 'MIXED', 'SILENT'].
- `apnsSound`: il nome del file audio nel bundle dell'applicazione. L'audio di questo file viene riprodotto come un avviso.
- `fireFoxTitle`: specifica il titolo da impostare per WebPush Notification.
- `fireFoxIconUrl`: l'URL dell'icona da impostare per WebPush Notification.
- `fireFoxTimeToLive`: questo parametro specifica per quanto tempo (in secondi) il messaggio deve essere conservato nella memoria GCM se il dispositivo è offline.
- `fireFoxPayload`: payload JSON personalizzato che verrà inviato come parte del messaggio di notifica.
- `chromeTitle`: specifica il titolo da impostare per WebPush Notification.
- `chromeIconUrl`: l'URL dell'icona da impostare per WebPush Notification.
- `chromeTimeToLive`: questo parametro specifica per quanto tempo (in secondi) il messaggio deve essere conservato nella memoria GCM se il dispositivo è offline.
- `chromePayload`: payload JSON personalizzato che verrà inviato come parte del messaggio di notifica.
- `chromeAppExtTitle`: specifica il titolo da impostare per WebPush Notification.
- `chromeAppExtCollapseKey`: questo parametro identifica un gruppo di messaggi.
- `chromeAppExtDelayWhileIdle`: quando questo parametro è impostato su true, indica che il messaggio non deve essere inviato finché il dispositivo non diventa attivo.
- `chromeAppExtIconUrl`: l'URL dell'icona da impostare per WebPush Notification.
- `chromeAppExtTimeToLive`: questo parametro specifica per quanto tempo (in secondi) il messaggio deve essere conservato nella memoria GCM se il dispositivo è offline.
- `chromeAppExtPayload`: payload JSON personalizzato che verrà inviato come parte del messaggio di notifica.

Ecco un esempio di invio di una notifica push dal pacchetto *pushnotification*.

- Invia una notifica push utilizzando l'azione `sendMessage` nel bind di pacchetto che hai creato precedentemente. Accertati di sostituire `/myNamespace/myPush` con il tuo nome pacchetto.
  
  ```
  wsk action invoke /myNamespace/myPush/sendMessage --blocking --result  -p url https://example.com -p text "this is my message"  -p sound soundFileName -p deviceIds "[\"T1\",\"T2\"]"
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
  

## Attivazione di un evento di trigger sull'attività del servizio Push Notifications
{: #openwhisk_catalog_pushnotifications_fire}

`/whisk.system/pushnotifications/webhook` configura il servizio Push per attivare un trigger quando, in un'applicazione specificata, si verifica un'attività del dispositivo, ad esempio la registrazione/l'annullamento della registrazione o la sottoscrizione/l'annullamento della sottoscrizione del dispositivo.

I parametri sono i seguenti:

- `appId:` il GUID dell'applicazione Bluemix.
- `appSecret:` l'appSecret del servizio di notifica push Bluemix.
- `events:` gli eventi supportati sono `onDeviceRegister`, `onDeviceUnregister`, `onDeviceUpdate`, `onSubscribe`, `onUnsubscribe`.Per ricevere notifiche da tutti gli eventi utilizzare il carattere jolly `*`.

Di seguito viene riportato un esempio di creazione di un trigger che verrà attivato ogni volta che viene registrato un nuovo dispositivo con l'applicazione del servizio di notifiche di push.

1. Crea un bind di pacchetto configurato per il tuo servizio di notifica di push con i tuoi appId e appSecret.
  
  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}
  
2. Crea un trigger per il tipo di evento `onDeviceRegister` del servizio di notifica di push utilizzando il feed `myPush/webhook`.
  
  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}  
  
3. Potresti creare una regola che invia un messaggio ogni volta che viene registrato un nuovo dispositivo. Crea una nuova regola utilizzando l'azione e il trigger precedenti.
  
  ```
  wsk rule create --enable myRule myPushTrigger sendMessage
  ```
  {: pre}
  
  Controlla i risultati in `wsk activation poll`.

  Registra un dispositivo nella tua applicazione Bluemix; puoi vedere che `rule`,`trigger` e `action` vengono eseguiti in openWhisk [dashboard] (https://console.{Domain}/openwhisk/dashboard).

  L'azione invierà una notifica di push.
  
