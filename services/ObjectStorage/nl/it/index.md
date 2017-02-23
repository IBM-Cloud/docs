---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-11"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# Introduzione a {{site.data.keyword.objectstorageshort}} {: #getting-started-with-object-storage}


{{site.data.keyword.objectstoragefull}} fornisce un'archivio dati cloud non strutturato. Puoi archiviare e accedere al tuo contenuto così come comporre e collegare le tue applicazioni e servizi.
{: shortdesc}

Alcuni casi di utilizzo comuni per il servizio {{site.data.keyword.objectstorageshort}} sono:

* Backup dei dati di volume dalle tue istanze
* Utilizzo di un'ubicazione intermedia in fase di trasferimento di grandi quantità di dati
* Trasferimento di dati tra ambienti che non sono connessi direttamente
* Funzione di repository centrale


{{site.data.keyword.Bluemix_notm}} Pubblico {{site.data.keyword.objectstorageshort}} ti fornisce l'accesso a un account Swift {{site.data.keyword.objectstorageshort}} con provisioning completo per gestire i tuoi dati. La crittografia lato provider non è fornita.


1.	Esegui il provisioning della tua istanza del servizio dal catalogo {{site.data.keyword.Bluemix_notm}}. Configura la tua istanza e fai clic su **Crea**. e inizialmente scegli l'opzione **Lascia senza binding** per il campo **Applicazione**, puoi ancora eseguire il bind dell'istanza del servizio alla tua applicazione {{site.data.keyword.Bluemix_notm}} successivamente.
2. Nel tuo dashboard dell'istanza del servizio, crea un contenitore per iniziare ad archiviare gli oggetti.
3. ggiungi un file al tuo contenitore dal menu a discesa **Azioni**.
4. Per verificare l'accesso ai tuoi oggetti, fai clic su **Scarica** e rivedi i file.
5. Quando sei pronto per collegare la tua istanza a un'applicazione, configura le tue credenziali del servizio e [esegui il bind del servizio](/docs/services/reqnsi.html#add_service).



# Link correlati
{: #rellinks}

## Guida di riferimento API
{: #api}
* [OpenStack {{site.data.keyword.objectstorageshort}} (Swift) API v1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
* [OpenStack Identity (Keystone) API v3.0](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}

## SDK
{: #sdk}
* [OpenStack Software Development Kits (SDK)](https://wiki.openstack.org/wiki/SDKs){: new_window}

## Esercitazioni ed esempi
{: #samples}
* [Connecting to IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} with Java](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
* [Use Python to access your {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}}](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
* [Use PHP to leverage {{site.data.keyword.objectstorageshort}}](https://developer.ibm.com/recipes/tutorials/use-php-to-leverage-object-storage-for-bluemix/){: new_window}
* [Use Node js to access Object Storage for Bluemix](https://developer.ibm.com/recipes/tutorials/use-pkgcloud-to-access-ibm-object-storage-for-bluemix-with-node-js/){: new-window}

## Runtime compatibili
{: #buildpacks}
* [Liberty for Java](https://www.ng.bluemix.net/docs/runtimes/liberty/index.html){: new_window}
* [SDK for Node.js](https://www.ng.bluemix.net/docs/runtimes/nodejs/index.html){: new_window}
* [Go](https://www.ng.bluemix.net/docs/runtimes/go/index.html){: new_window}
* [PHP](https://www.ng.bluemix.net/docs/runtimes/php/index.html){: new_window}
* [Python](https://www.ng.bluemix.net/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://www.ng.bluemix.net/docs/runtimes/ruby/index.html){: new_window}
* [Pacchetti di build della community](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}


## Link correlati
{: #general}
* [Listino prezzi IBM {{site.data.keyword.Bluemix_notm}}](https://www.ng.bluemix.net/#/pricing){: new_window}
* [Prerequisiti IBM {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
