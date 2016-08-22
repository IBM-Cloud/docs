---

copyright:
 years: 2015, 2016

---

# Informationen zu Push Notifications
{: #overview-push}
*Letzte Aktualisierung: 14. Juni 2016*
{: .last-updated}

Push Notifications ist ein Service, mit dem Sie Benachrichtigungen an iOS- und Android-Geräte senden können. Benachrichtigungen können zielgruppenspezifisch an alle Anwendungsbenutzer und an bestimmte
Benutzergruppen und Geräte mithilfe von Tags gesendet werden. Sie können Geräte, Tags und Subskriptionen verwalten. Sie können
auch ein SDK (Software Development Kit) und REST-APIs (Representational State Transfer Application Program Interfaces) verwenden, um Ihre Clientanwendungen weiter
zu entwickeln. 

Push Notification ist auch als Bluemix Dedicated-Service verfügbar. Informationen zum dedizierten Push-Service finden Sie im Abschnitt zu den [Dedizierten Services](../../dedicated/index.html). Beachten Sie, dass auf der Registerkarte zur Überwachung von Push Notifications keine Analysedaten angezeigt werden.

Der Push Notification-Service ist nun OpenWhisk-fähig. Weitere Informationen finden Sie unter [OpenWhisk](../../openwhisk/index.html).


## Prozess für Push Notification-Service
{: #overview_push_process}

Mobile Clients können den Push Notification-Service subskribieren und sich für diesen Service registrieren. Beim Start registrieren sich mobile Anwendungen selbst und subskribieren den Push Notification-Service. Die Benachrichtigungen werden an den Server von Apple Push Notification Service (APNS) oder den Server von Google Cloud Messaging (GCM) und anschließend an registrierte mobile Clients gesendet.

![Überblick über den Push-Service](images/overview.jpg)


###Mobile Anwendungen

Beim Start registrieren sich mobile Anwendungen selbst und subskribieren den Push Notification-Service, um Benachrichtigungen zu empfangen.

###Back-End-Anwendungen

Back-End-Anwendungen können sich in Geschäftsräumen oder in einer öffentlichen Cloud befinden. Back-End-Anwendungen verwenden den Push Notification-Service zum Senden von kontextabhängigen Benachrichtigungen an mobile Benutzer. Die Back-End-Anwendungen sind für die Verwaltung und Wartung von mobilen Geräten und von Benutzerinformationen zum Senden von Push-Benachrichtigungen nicht erforderlich. Back-End-Anwendungen können stattdessen den Push Notification-Service verwenden.

###Eigner der Back-End-App

Die Rolle, von der die mobile Back-End-Anwendung erstellt wurde, in der eine Instanz des Push Notification-Service gebündelt ist. Diese Person konfiguriert den Push Notification-Service und richtet ihn so ein, dass er für die Back-End-Anwendungen geeignet ist, die den Push Notification-Service und mobile Anwendungen nutzen, die das Ziel von Push-Benachrichtigungen sind.

###Push Notification-Service

Der Service 'Push Notification' verwaltet alle Informationen, die sich auf die Geräte beziehen, die sich für Benachrichtigungen registrieren. Der Service hält Ihre Anwendungen transparent für die Technologiedetails zum
Senden von Benachrichtigungen an diese heterogenen mobilen Plattformen und verarbeitet dies
alles intern.

###Gateways

Plattformspezifische Cloud-Services für mobile Geräte wie Google Cloud Messaging (GCM) oder Apple Push Notification Service (APNS) verwenden den Push Notification-Service zum Senden von Benachrichtigungen an die mobilen Anwendungen.

## Typen von Push-Benachrichtigungen
{: #overview-push-types}

###Broadcast

Wenn eine mobile Anwendung sich beim Push Notification-Service registriert, kann sie Rundsendungen (Broadcasts) empfangen. Broadcastbenachrichtigungen sind Benachrichtigungen, die als Ziel alle Geräte haben, auf denen die Anwendung installiert ist und die für den Push Notification-Service konfiguriert sind. Broadcastbenachrichtigungen werden standardmäßig mit einer beliebigen Anwendung aktiviert, die für Push-Benachrichtigungen aktiviert ist. Alle Anwendungen, die für den Push Notification-Service aktiviert sind, haben eine vordefinierte Subskription für den Tag Push.ALL, der vom Server zum Übertragen von Broadcastbenachrichtigungen an alle Geräte verwendet wird. Zum Senden einer Broadcastbenachrichtigung mithilfe der REST-API von Push müssen Sie während der Übergabe an die Ressource der Nachrichten sicherstellen, dass als 'Ziel' eine leere JSON-Datei angegeben ist.

###Tagbasierte Benachrichtigungen

Tagbenachrichtigungen sind Benachrichtigungen, deren Ziel alle Geräte sind, die eine Subskription für einen bestimmten Tag aufweisen. Tagbasierte Benachrichtigungen ermöglichen die Segmentierung von Benachrichtigungen auf der Basis von Subjektbereichen oder Themen. Benachrichtigungsempfänger können wählen, dass sie Benachrichtigungen nur empfangen, wenn deren Inhalt ein Thema hat, das von Interesse ist. Daher bieten tagbasierte Benachrichtigungen die Möglichkeit, Empfänger zu segmentieren. Diese Funktion ermöglicht es, dass Tags definiert werden und anschließend Nachrichten geordnet nach Tags gesendet und empfangen werden. Eine Nachricht wird zielgruppenspezifisch nur an die Geräte gesendet, die einen Tag subskribiert haben. Sie müssen zunächst die Tags für die Anwendung erstellen, die Tagsubskriptionen einrichten und anschließend die tagbasierten Benachrichtigungen starten. Zum Senden einer tagbasierten Benachrichtigung mithilfe der REST-API müssen Sie sicherstellen, dass während der Übergabe an die Ressource der Nachricht die Tagnamen ('tagNames') angegeben werden.

###Unicast-Benachrichtigungen

Unicast-Benachrichtigungen sind Benachrichtigungen, deren Ziel ein bestimmtes Gerät ist. Unicast-Benachrichtigungen benötigen keine zusätzliche Konfiguration und sie werden standardmäßig aktiviert, wenn die Anwendung für Push-Benachrichtigungen aktiviert wird. Stellen Sie zum Senden einer Unicast-Benachrichtigung mithilfe der REST-API sicher, dass die Geräte-IDs (deviceIds) während der Übergabe an eine Nachrichtenressource bereitgestellt werden.

###Plattformbasierte Benachrichtigungen

Benachrichtigungen können zielgruppenspezifisch an eine bestimmte Geräteplattform gerichtet werden. Eine Benachrichtigung kann beispielsweise nur an alle Android-Benutzer gesendet werden. Stellen Sie zum Senden einer plattformbasierten Benachrichtigung mithilfe der REST-API sicher, dass die Zielplattformen während der Übergabe an eine Nachrichtenressource bereitgestellt werden. Geben Sie die Plattformen als Array an. Folgende Plattformen werden unterstützt:
* A (Apple)
* G (Google)

## Nachrichtengröße bei Push Notification
{: #push-message-size}

Die Größe der Nachrichtennutzdaten bei Push Notification richtet sich nach den Mediatoren. 

###iOS

Ab iOS 8 beträgt die zulässige maximale Größe 2 Kilobyte. Der Push Notification-Service für Apple sendet keine Benachrichtigungen, die dieses Limit überschreiten.

###Android

Für die Android-Plattform gibt es keine Einschränkungen.
