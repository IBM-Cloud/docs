---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Construction de votre URL {{site.data.keyword.objectstorageshort}} pour utiliser l'API Swift REST

Vous pouvez vous servir de l'API Swift REST avec une interface client de ligne de commande, comme cURL, ou appeler l'API depuis votre application.
{: shortdesc}


Pour une liste complète des options d'API REST {{site.data.keyword.objectstorageshort}} avec des exemples, voir [Swift/API - OpenStack, dans le site openstack](http://developer.openstack.org/api-ref-objectstorage-v1.html).

Avant de composer votre URL, vous devez [authentifier](/docs/services/ObjectStorage/os_authenticate.html) votre
instance de service auprès de Keystone. Prenez soin de noter la réponse du catalogue. Elle sera similaire à l'exemple ci-après.

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


Ajoutez l'espace de nom de votre conteneur et l'objet à la fin de votre URL {{site.data.keyword.objectstorageshort}}, comme illustré dans l'image ci-après.

![Eléments de l'URL {{site.data.keyword.objectstorageshort}} montrés dans une image exemple](images/Swift_URL.png)

Figure 1. Exemple d'URL {{site.data.keyword.objectstorageshort}}
