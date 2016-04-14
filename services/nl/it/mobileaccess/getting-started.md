---

copyright:
  years: 2015, 2016

---

# Introduzione
{: #getting-started}
Per iniziare a utilizzare {{site.data.keyword.amashort}}, puoi aggiungere il servizio {{site.data.keyword.amashort}} a
un'applicazione {{site.data.keyword.Bluemix}} oppure puoi creare una nuova applicazione con il contenitore tipo.  

## Creazione di un'istanza del servizio {{site.data.keyword.amashort}}
{: #service-instance}

Puoi creare una nuova istanza di un servizio {{site.data.keyword.amashort}} dal catalogo {{site.data.keyword.Bluemix}}.  Se non utilizzi il contenitore tipo per creare un nuovo backend mobile, devi configurare l'SDK server sul tuo backend esistente.


  * **Nuova applicazione**: le istruzioni nelle seguenti sezioni descrivono come creare una nuova applicazione che crea un backend mobile e protegge con l'SDK server {{site.data.keyword.amashort}}. Fai clic sul contenitore tipo **MobileFirst Services Starter** per creare una nuova applicazione
con il servizio {{site.data.keyword.amashort}}.
  * **Applicazione esistente**: fai clic sull'icona {{site.data.keyword.amashort}} per creare una nuova istanza del servizio associata mediante bind a un'applicazione esistente. per configurare l'SDK server sulla tua applicazione esistente, vedi [Protezione di risorse cloud](protecting-resources.html).


## Creazione di un backend mobile con il contenitore tipo MobileFirst Services Starter
{: #create-backend}
Quando utilizzi MobileFirst Services Starter, ottieni un'istanza di un runtime Node.js che viene eseguito su IBM {{site.data.keyword.Bluemix_notm}} per implementare la tua logica di backend personalizzata. A tale applicazione Node.js viene associata mediante bind una serie di servizi mobili di base che forniscono funzioni di sicurezza, dati, push e monitoraggio. Dopo che l'applicazione {{site.data.keyword.Bluemix_notm}} Node.js è stata creata, puoi configurare il tuo ambiente di sviluppo e iniziare a utilizzare
gli SDK {{site.data.keyword.Bluemix_notm}} Mobile Services. Puoi utilizzare gli SDK per accedere ai servizi associati mediante bind alla tua applicazione cloud con delle semplici chiamate API.

1. Dal catalogo {{site.data.keyword.Bluemix_notm}}, vai alla sezione **Contenitori tipo** e fai clic su **MobileFirst Services Starter**.
1. Aggiungi le informazioni sul tuo backend mobile, compresi spazio, nome, host e piano di servizio.
1. Fai clic su **CREA**.



## Fasi successive
{: #next-steps}
Diversi endpoint dell'applicazione Node.js da te creata con il contenitore tipo sono protetti con {{site.data.keyword.amashort}}. Per ulteriori informazioni sull'applicazione di backend mobile predefinita, vedi [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop).

Puoi configurare la tua applicazione mobile per utilizzare l'SDK {{site.data.keyword.amashort}}.  Dopo che hai configurato l'SDK, puoi iniziare a configurare l'autenticazione e il monitoraggio nella tua applicazione.  Attieniti alle istruzioni per la tua piattaforma di sviluppo mobile:

* [Android](getting-started-android.html)
* [iOS (SDK Swift)](getting-started-ios.html)
* [iOS (SDK Objective-C)](getting-started-ios.html)
* [Cordova](getting-started-cordova.html)
