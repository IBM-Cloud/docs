---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Creazione del tuo URL {{site.data.keyword.objectstorageshort}} per utilizzare l'API REST Swift

Puoi utilizzare l'API REST Swift con un'interfaccia client di riga di comando, come cURL, oppure richiamare l'API dalla tua applicazione.
{: shortdesc}


Per un elenco completo delle opzioni dell'API REST {{site.data.keyword.objectstorageshort}} e dei relativi esempi, consulta la [guida di riferimento completa per l'API Swift OpenStack](http://developer.openstack.org/api-ref-objectstorage-v1.html).

Quando hai autenticato la tua istanza del servizio con Keystone, prendi nota della risposta del catalogo. Dovrebbe essere simile al seguente esempio.

```
{
  "id" : "4207049680fa4effbecd044c7448a8cb",
  "region" : "dallas",
  "region_id" : "dallas",
  "url" : "https://dal.objectstorage.open.softlayer.com/v1/AUTH_4abf7d7bac2c4eda89c03dd3afa7a0a3",
  "interface" : "public"
},
```
{: codeblock}


Aggiungi lo spazio di nomi del tuo contenitore e oggetto alla fine del tuo URL {{site.data.keyword.objectstorageshort}} come illustrato nella seguente immagine.

  Parti URL![{{site.data.keyword.objectstorageshort}} illustrate in un'immagine di esempio](images/swift_URL.png)
  Figura 1: Esempio URL {{site.data.keyword.objectstorageshort}}
