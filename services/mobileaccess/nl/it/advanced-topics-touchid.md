---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27" 

---

# Autorizzazione dell'accesso con Touch ID
{: #before-you-begin}

Touch ID è una funzione di riconoscimento delle impronte digitali per i dispositivi iOS. Puoi utilizzare Touch ID con il servizio {{site.data.keyword.amafull}} per proteggere automaticamente le informazioni di autorizzazione per un uso futuro. 

**Nota:** Touch ID è disponibile solo dall'SDK Objective-C  {{site.data.keyword.amashort}}.

Per configurare la complessità della sicurezza, imposta una delle seguenti politiche di persistenza con il metodo `IMFAuthorizationManager.setAuthorizationPersistencePolicy()`.

* **IMFAuthorizationPersistencePolicyNever** (più sicuro): non rendere mai persistenti le informazioni relative all'autorizzazione sul dispositivo. Un'intestazione di autorizzazione è valida durante una singola sessione dell'applicazione. Le informazioni relative all'autorizzazione sono rese persistenti nella keychain iOS.

* **IMFAuthorizationPersistencePolicyAlways** (meno sicura): rendere sempre persistenti le informazioni relative all'autorizzazione sul dispositivo, indipendentemente dalla presenza, dal supporto o dall'abilitazione di Touch ID. L'autenticazione del passcode del dispositivo e Touch ID non sono mai richiesti.

* **IMFAuthorizationPersistencePolicyWithTouchBiometrics**: utilizza Touch ID per recuperare le informazioni relative all'autorizzazione dalla keychain iOS. Questa opzione bilancia sicurezza e facilità d'uso. Le informazioni relative all'autorizzazione vengono rese persistenti solo se Touch ID è presente, supportato e abilitato. Touch ID o l'autenticazione del passcode del dispositivo sono necessari per accedere alle informazioni relative all'autorizzazione rese persistenti una volta per ciascuna sessione dell'applicazione. Se questa politica è stata impostata, ma non è disponibile alcun accesso a Touch ID, ad esempio perché l'hardware necessario non è presente oppure è stato disabilitato, il fallback è la politica **IMFAuthorizationPersistancePolicyNever**.
