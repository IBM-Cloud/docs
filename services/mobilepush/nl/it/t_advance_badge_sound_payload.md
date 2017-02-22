---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#Abilitazione delle notifiche di push avanzate
Ultimo aggiornamento: 11 gennaio 2017
{: .last-updated}

Configura un badge iOS, audio, payload JSON aggiuntivo, notifiche operative e notifiche messe in pausa.

## Configurazione di audio e payload e badge iOS
{: #badge-sound-payload}

Configura un badge, l'audio e del payload JSON aggiuntivo iOS.

1. Nel dashboard {{site.data.keyword.mobilepushshort}}, vai alla scheda **Notifications**.
2. Vai alla sezione **Optional Fields** per configurare le funzioni di {{site.data.keyword.mobilepushshort}}. 
	- **Sound File** - immetti una stringa per puntare al file audio nella tua applicazione mobile. Nel payload, specifica il nome stringa del file audio da utilizzare.
	- **iOS Badge** - per i dispositivi iOS, il numero da visualizzare come badge dell'icona
                            applicazione. Se questa proprietà
                            non è presente, il badge non viene modificato. Per rimuovere il badge, imposta
                            il valore di questa proprietà su 0.
	
###Android

Aggiungi il file audio nella directory `res/raw` della tua applicazione android. Mentre invii le notifiche aggiungi il nome del file audio nel campo audio di {{site.data.keyword.mobilepushshort}}.

```
"settings": {
     "gcm" : {
     "sound":"tt.wav",
	  }
 }  
```
    {: codeblock}	
	
###iOS

```
"settings": {
     "apns" : {
      "badge": 10,
	      "sound": "tt.wav",
	  }
}
``` 
	{: codeblock}
		
**Additional Payload** - This payload can be any key-value pair and must be a JSON object that you want to send with th**Additional Payload** - questo payload può essere qualsiasi coppia chiave-valore e deve essere un oggetto JSON che vuoi inviare con {{site.data.keyword.mobilepushshort}}.

```
{"chiave":"valore", "chiave2":"valore2"}
```
	{: codeblock}

## Messa in pausa delle notifiche Android 
{: #hold-notifications-android}

Quando la tua applicazione va in background, probabilmente vuoi che {{site.data.keyword.mobilepushshort}} metta in pausa le notifiche inviate alla tua applicazione. Per mettere in pausa le notifiche, richiama il metodo hold() nel metodo onPause() dell'attività che sta gestendo {{site.data.keyword.mobilepushshort}}.

```
@Override
protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
} 
```
	{: codeblock}
## Abilitazione di notifiche operative iOS  
{: #enable-actionable-notifications-ios}

A differenza di {{site.data.keyword.mobilepushshort}} tradizionale,  le notifiche operative richiedono agli utenti di effettuare una selezione al momento della ricezione dell'avviso di notifica senza aprire l'applicazione. 

Completa la seguente procedura per abilitare {{site.data.keyword.mobilepushshort}} operativo nella tua applicazione.

1. Crea un'azione di risposta utente.
```
//Per Swift
	let acceptAction = UIMutableUserNotificationAction()
	acceptAction.identifier = "ACCEPT_ACTION"
	acceptAction.title = "Accept"
	acceptAction.destructive = false
	acceptAction.authenticationRequired = false
	acceptAction.activationMode = UIUserNotificationActivationMode.Foreground
```
	{: codeblock}
```
//Per Swift
	let declineAction = UIMutableUserNotificationAction()
	declineAction.identifier = "DECLINE_ACTION"
	declineAction.title = "Decline"
	declineAction.destructive = true
	declineAction.authenticationRequired = false
	declineAction.activationMode = UIUserNotificationActivationMode.Background
```
	{: codeblock}

2. Crea la categoria di notifica e imposta un'azione. **UIUserNotificationActionContextDefault** o
                **UIUserNotificationActionContextMinimal** sono
contesti validi.
```
// Per Swift
	let pushCategory = UIMutableUserNotificationCategory()
	pushCategory.identifier = "TODO_CATEGORY"
	pushCategory.setActions([acceptAction, declineAction], forContext: UIUserNotificationActionContext.Default)
```
	{: codeblock}

1. Crea l'impostazione di notifica e assegna le categorie dal passo precedente.
```
// Per Swift
	let categories = NSSet(array:[pushCategory]);
```
	{: codeblock}

1. Crea la notifica locale o remota e assegnale
l'identità della categoria.
```
//Per Swift
	let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: categories as? Set<UIUserNotificationCategory>)
    UIApplication.sharedApplication().registerUserNotificationSettings(settings)
    UIApplication.sharedApplication().registerForRemoteNotifications() 
```
	{: codeblock}
	
## Gestione di notifiche iOS operative  
{: #actionable-notifications}

Quando viene ricevuta una notifica operativa, il controllo viene spostato sul seguente metodo in base all'identificativo scelto.

 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
      //è necessario richiamare il gestore del completamente quando finito
      completionHandler()
  }
```    
	{: codeblock}
    
