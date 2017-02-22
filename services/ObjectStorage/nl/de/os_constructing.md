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


# {{site.data.keyword.objectstorageshort}}-URL für die Verwendung der Swift-REST-API festlegen

Sie können die Swift-REST-API mit einer Befehlszeilen-Clientschnittstelle, wie cURL, verwenden oder die API über die Anwendung aufrufen.
{: shortdesc}


Eine umfassende Liste der Optionen und Beispiele der {{site.data.keyword.objectstorageshort}}-REST-API finden Sie in der [vollständige Referenz zur OpenStack-Swift-API](http://developer.openstack.org/api-ref-objectstorage-v1.html).

Bevor Sie die URL bilden können, müssen Sie die Serviceinstanz mit Keystone [authentifizieren](/docs/services/ObjectStorage/os_authenticate.html). Denken Sie daran, die Katalogantwort zu notieren. Diese sieht ähnlich wie das folgende Beispiel aus.

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


Fügen Sie die Namensbereiche des Containers und Objekts am Ende Ihrer {{site.data.keyword.objectstorageshort}}-URL ein, wie in der nachfolgenden Abbildung dargestellt.

In einem Beispiel-Image gezeigte Teile einer ![{{site.data.keyword.objectstorageshort}}-URL](images/Swift_URL.png)

Abbildung 1. {{site.data.keyword.objectstorageshort}}-URL-Beispiel
