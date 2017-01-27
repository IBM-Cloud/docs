---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-05"

---
{:new_window: target="blank"}
{:shortdesc: .shortdesc}



# Einführung in {{site.data.keyword.objectstorageshort}} {: #getting-started-with-object-storage}


{{site.data.keyword.objectstoragefull}} bietet eine unstrukturierte Clouddatenspeicherung. Sie können Ihren Inhalt speichern und darauf zugreifen sowie interaktiv zusammenstellen und mit Apps und Services verbinden.
{: shortdesc}

Beispiele für häufige Anwendungsfälle für den {{site.data.keyword.objectstorageshort}}-Service:

* Sicherung durch Backups von Datenträgerdaten aus Ihren Instanzen
* Verwendung als Zwischenspeicherposition bei der Übertragung umfangreicher Datenvolumen
* Übertragung von Daten zwischen Umgebungen, die nicht direkt verbunden sind
* Einsatz als zentrales Repository


{{site.data.keyword.Bluemix_notm}} Public {{site.data.keyword.objectstorageshort}} ermöglicht Ihnen zur Verwaltung Ihrer Daten den Zugriff auf ein vollständig eingerichtetes Swift {{site.data.keyword.objectstorageshort}}-Konto. Eine providerseitige Verschlüsselung wird nicht bereitgestellt.


1.	Stellen Sie über den {{site.data.keyword.Bluemix_notm}}-Katalog Ihre Serviceinstanz bereit. Konfigurieren Sie Ihre Instanz und klicken Sie auf **Erstellen**. Wenn Sie anfangs die Option **Nicht binden** für das Feld **App** auswählen, können Sie die Serviceinstanz dennoch zu einem späteren Zeitpunkt an Ihre {{site.data.keyword.Bluemix_notm}}-App binden.
2. Erstellen Sie In Ihrem Serviceinstanz-Dashboard einen Container, um mit dem Speichern von Objekten zu beginnen.
3. Fügen Sie Ihrem Container über das Dropdown-Menü **Aktionen** eine Datei hinzu.
4. Um den Zugriff auf Ihre Objekte zu testen, klicken Sie auf **Download** und überprüfen Sie die Datei.
5. Wenn Sie für die Verbindung Ihrer Instanz mit einer Anwendung bereit sind, richten Sie Ihre Serviceberechtigungsnachweise ein und [binden Sie den Service](/docs/services/reqnsi.html#add_service).



# Zugehörige Links
{: #rellinks}

## API-Referenz
{: #api}
* [OpenStack {{site.data.keyword.objectstorageshort}} (Swift) API v1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
* [OpenStack Identity (Keystone) API v3.0](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}

## SDK
{: #sdk}
* [OpenStack Software Development Kits (SDK)](https://wiki.openstack.org/wiki/SDKs){: new_window}

## Lernprogramme und Beispiele
{: #samples}
* [Herstellen einer Verbindung zu IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} mit Java](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
* [Python für den Zugriff auf {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}} verwenden](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
* [PHP zur Nutzung von {{site.data.keyword.objectstorageshort}} verwenden](https://developer.ibm.com/recipes/tutorials/use-php-to-leverage-object-storage-for-bluemix/){: new_window}

## Kompatible Laufzeiten
{: #buildpacks}
* [Liberty for Java](https://www.ng.bluemix.net/docs/runtimes/liberty/index.html){: new_window}
* [SDK for Node.js](https://www.ng.bluemix.net/docs/runtimes/nodejs/index.html){: new_window}
* [Go](https://www.ng.bluemix.net/docs/runtimes/go/index.html){: new_window}
* [PHP](https://www.ng.bluemix.net/docs/runtimes/php/index.html){: new_window}
* [Python](https://www.ng.bluemix.net/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://www.ng.bluemix.net/docs/runtimes/ruby/index.html){: new_window}
* [Community-Buildpacks](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}


## Zugehörige Links
{: #general}
* [IBM {{site.data.keyword.Bluemix_notm}}-Preisliste](https://www.ng.bluemix.net/#/pricing){: new_window}
* [IBM {{site.data.keyword.Bluemix_notm}}-Voraussetzungen](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
