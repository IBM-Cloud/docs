---

copyright:
 years: 2015, 2016

---

# Informationen zu Push Notifications
{: #overview-push}

Push Notifications ist ein Service, mit dem Sie Benachrichtigungen an iOS- und Android-Geräte senden können. Benachrichtigungen können zielgruppenspezifisch an alle Anwendungsbenutzer und an bestimmte
Benutzergruppen und Geräte mithilfe von Tags gesendet werden. Sie können Geräte, Tags und Subskriptionen verwalten. Sie können
auch ein SDK (Software Development Kit) und REST-APIs (Representational State Transfer Application Program Interfaces) verwenden, um Ihre Clientanwendungen weiter
zu entwickeln. Informationen zum dedizierten Push-Service finden Sie im Abschnitt zu den [Dedizierten Services](../../dedicated/index.html). 


## Prozess für Push Notifications Service
{: #overview_push_process}

Mobile Clients können Push Notifications Service subskribieren und sich für diesen Service registrieren. Beim Start
registrieren sich mobile Anwendungen selbst und subskribieren Push Notifications Service. Die Benachrichtigungen werden an den Server von Apple Push Notification Service (APNs) oder den Server von Google Cloud Messaging (GCM) und anschließend an registrierte mobile Clients gesendet.

![Überblick über den Push-Service](images/overview.jpg)


###Mobile Anwendungen

Beim Start registrieren sich mobile Anwendungen selbst
und subskribieren Push Notifications Service, um Benachrichtigungen zu empfangen.

###Back-End-Anwendungen

Back-End-Anwendungen können sich in Geschäftsräumen oder in einer öffentlichen Cloud befinden. Back-End-Anwendungen verwenden Push Notifications Service
zum Senden von kontextabhängigen Benachrichtigungen an mobile Benutzer. Die Back-End-Anwendungen
sind für die Verwaltung und Wartung von mobilen Geräten und von Benutzerinformationen zum
Senden von Push-Benachrichtigungen nicht erforderlich. Back-End-Anwendungen können stattdessen
Push Notifications Service verwenden.

###Eigner der Back-End-App

Die Rolle, von der die mobile Back-End-Anwendung erstellt wurde, in der eine Instanz von
Push Notifications Service gebündelt ist. Diese Person konfiguriert Push Notifications Service und richtet
es so ein, dass es für die Back-End-Anwendungen geeignet ist, die Push Notifications Service und mobile
Anwendungen nutzen, die das Ziel von Push-Benachrichtigungen sind.

###Service 'Push Notifications'

Der Service 'Push Notifications' verwaltet alle Informationen, die sich auf die Geräte beziehen, die sich für Benachrichtigungen registrieren. Der Service hält Ihre Anwendungen transparent für die Technologiedetails zum
Senden von Benachrichtigungen an diese heterogenen mobilen Plattformen und verarbeitet dies
alles intern.

###Gateways

Plattformspezifische Cloud-Services für mobile Geräte wie Google Cloud Messaging (GCM) oder
Apple Push Notification Service (APNs) verwenden Push Notifications Service zum Senden von Benachrichtigungen
an die mobilen Anwendungen.

## Typen von Push-Benachrichtigungen
{: #overview-push-types}

###Broadcast

Wenn eine mobile Anwendung sich bei Push Notifications Service registriert, kann sie Rundsendungen (Broadcasts) empfangen. Broadcastbenachrichtigungen sind Benachrichtigungen, die als Ziel alle Geräte haben, auf denen die Anwendung installiert ist und die für Push Notifications Service konfiguriert sind. Broadcastbenachrichtigungen werden standardmäßig mit einer beliebigen Anwendung aktiviert, die für Push-Benachrichtigungen aktiviert ist. Alle Anwendungen, die für Push Notifications Service aktiviert sind, haben eine vordefinierte Subskription für den Tag Push.ALL, der vom Server zum Übertragen von Broadcastbenachrichtigungen an alle Geräte verwendet wird. Zum Senden einer Broadcastbenachrichtigung mithilfe der REST-API von Push müssen Sie während der Übergabe an die Ressource der Nachrichten sicherstellen, dass als 'Ziel' eine leere JSON-Datei angegeben ist.

###Tagbasierte Benachrichtigungen

Tagbenachrichtigungen sind Benachrichtigungen, deren Ziel alle Geräte sind, die eine Subskription für einen bestimmten Tag aufweisen. Tagbasierte Benachrichtigungen ermöglichen die Segmentierung von Benachrichtigungen auf der Basis von Subjektbereichen oder Themen. Benachrichtigungsempfänger können wählen, dass sie Benachrichtigungen nur empfangen, wenn deren Inhalt ein Thema hat, das von Interesse ist. Daher bieten tagbasierte Benachrichtigungen die Möglichkeit, Empfänger zu segmentieren. Diese Funktion ermöglicht es, dass Tags definiert werden und anschließend Nachrichten geordnet nach Tags gesendet und empfangen werden. Eine Nachricht wird zielgruppenspezifisch nur an die Geräte gesendet, die einen Tag subskribiert haben. Sie müssen zunächst die Tags für die Anwendung erstellen, die Tagsubskriptionen einrichten und anschließend die tagbasierten Benachrichtigungen starten. Zum Senden einer tagbasierten Benachrichtigung mithilfe der REST-API müssen Sie sicherstellen, dass während der Übergabe an die Ressource der Nachricht die Tagnamen ('tagNames') angegeben werden.

###Unicast-Benachrichtigungen

Unicast-Benachrichtigungen sind Benachrichtigungen, deren Ziel ein bestimmtes Gerät ist. Unicast-Benachrichtigungen benötigen keine zusätzliche Konfiguration und sie werden standardmäßig aktiviert, wenn die Anwendung für Push-Benachrichtigungen aktiviert wird. Stellen Sie zum Senden einer Unicast-Benachrichtigung mithilfe der REST-API sicher, dass die Geräte-IDs (deviceIds) während der Übergabe an eine Nachrichtenressource bereitgestellt werden.

###Plattformbasierte Benachrichtigungen

Benachrichtigungen können zielgruppenspezifisch an eine bestimmte Geräteplattform gerichtet werden. Eine Benachrichtigung kann beispielsweise nur an alle Android-Benutzer gesendet werden. Stellen Sie zum Senden einer plattformbasierten Benachrichtigung mithilfe der REST-API sicher, dass die Zielplattformen während der Übergabe an eine Nachrichtenressource bereitgestellt werden. Geben Sie die Plattformen als Array an. Folgende Plattformen werden unterstützt:
* A (Apple)
* G (Google)
