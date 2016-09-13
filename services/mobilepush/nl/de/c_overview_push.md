---

copyright:
 years: 2015, 2016

---

# Informationen zu {{site.data.keyword.mobilepushshort}}
{: #overview-push}
Letzte Aktualisierung: 16. August 2016
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}} ist ein Service, mit dem Sie Benachrichtigungen an iOS- und Android-Geräte senden können. Benachrichtigungen können zielgruppenspezifisch an alle Anwendungsbenutzer und an bestimmte
Benutzergruppen und Geräte mithilfe von Tags gesendet werden. Sie können Geräte, Tags und Subskriptionen verwalten. Sie können
auch ein SDK (Software Development Kit) und REST-APIs (Representational State Transfer Application Program Interfaces) verwenden, um Ihre Clientanwendungen weiter
zu entwickeln. 

{{site.data.keyword.mobilepushshort}} ist auch als Bluemix Dedicated-Service verfügbar. Informationen zu {{site.data.keyword.mobilepushshort}} als dediziertem Service finden Sie im Abschnitt [Dedizierte Services](../../dedicated/index.html). Beachten Sie, dass auf der Registerkarte zur Überwachung von Push-Benachrichtigungen keine Analysedaten angezeigt werden. 

Der {{site.data.keyword.mobilepushshort}}-Service ist nun OpenWhisk-fähig. Weitere Informationen finden Sie unter [OpenWhisk](../../openwhisk/index.html).


## Prozess für den {{site.data.keyword.mobilepushshort}}-Service
{: #overview_push_process}

Mobile Clients können den {{site.data.keyword.mobilepushshort}}-Service subskribieren und sich für diesen Service registrieren. Beim Start registrieren sich mobile Anwendungen selbst und subskribieren den {{site.data.keyword.mobilepushshort}}-Service. Die Benachrichtigungen werden dem Server von Apple Push Notification Service (APNs) oder dem Server von Google Cloud Messaging (GCM) zugeteilt und anschließend an registrierte mobile Clients gesendet.

![Überblick über den Push-Service](images/overview.jpg)


###Mobile Anwendungen
{: mobile-applications}

Beim Start registrieren sich mobile Anwendungen selbst und subskribieren den {{site.data.keyword.mobilepushshort}}-Service, um Benachrichtigungen zu empfangen. 

###Back-End-Anwendungen
{: backend-applications}

Back-End-Anwendungen können sich vor Ort oder in einer öffentlichen Cloud befinden. Back-End-Anwendungen verwenden den {{site.data.keyword.mobilepushshort}}-Service zum Senden kontextabhängiger Benachrichtigungen an mobile Benutzer. Die Back-End-Anwendungen sind für die Verwaltung und Wartung von mobilen Geräten und von Benutzerinformationen zum Senden von Push-Benachrichtigungen nicht erforderlich. Stattdessen können Back-End-Anwendungen den {{site.data.keyword.mobilepushshort}}-Service verwenden. 

###Eigner der Back-End-App
{: app-backend-owner}

Der Eigner der Back-End-App erstellt die mobile Back-End-Anwendung, die eine Instanz des {{site.data.keyword.mobilepushshort}}-Service bündelt. Der Eigner der Back-End-App konfiguriert außerdem den {{site.data.keyword.mobilepushshort}}-Service und richtet ihn so ein, dass er sich für die Back-End-Anwendungen eignet, die den Service verwenden, sowie für mobile Anwendungen, die als Ziel für Push-Nachrichten fungieren. 

###{{site.data.keyword.mobilepushshort}}-Service
{: push-notification-service}

Der {{site.data.keyword.mobilepushshort}}-Service ist für die Verwaltung aller Informationen im Zusammenhang mit Geräten zuständig, die für Benachrichtigungen registriert sind. Der Service sorgt dafür, dass Ihre Anwendungen transparent gegenüber den Technologiedetails beim Senden von Benachrichtigungen an heterogene mobile Plattformen bleiben, und verarbeitet dies
alles intern.

###Gateways
{: gateways}

Plattformspezifische Cloud-Services für mobile Geräte wie Google Cloud Messaging (GCM) oder
Apple Push Notification Service (APNs) verwenden den {{site.data.keyword.mobilepushshort}}-Service zum Zuteilen von Benachrichtigungen an die mobilen Anwendungen. 

###Sicherheit von Push-Benachrichtigungen
{: push-security}

Die APIs für Push-Nachrichten sind durch zwei geheime Schlüssel geschützt: i) 'appSecret' und ii) 'clientSecret'. Der geheime Schlüssel 'appSecret' schützt APIs, die normalerweise von Back-End-Anwendungen wie der API zum Senden von Push-Nachrichten oder der API zum Konfigurieren von Einstellungen aufgerufen werden. Der geheime Schlüssel 'clientSecret' schützt APIs, die normalerweise von mobilen Clientanwendungen aufgerufen werden. Gegenwärtig gibt es nur eine API, die an der Registrierung von Geräten beteiligt ist und der eine Benutzer-ID zugeordnet ist, die diesen geheimen Clientschlüssel 'clientSecret' erfordert. Alle übrigen APIs, die von mobilen Clients aufgerufen werden, benötigen 'clientSecret' nicht. Die geheimen Schlüssel 'appSecret' und 'clientSecret' werden jeder Serviceinstanz beim Binden einer Anwendung mit dem {{site.data.keyword.mobilepushshort}}-Service zugeordnet. Weitere Informationen dazu, auf welche Weise und für welche APIs die geheimen Schlüssel übergeben werden sollen, finden Sie in der REST-API-Dokumentation. 

## Typen von Push-Benachrichtigungen
{: #overview-push-types}

###Broadcast
{: broadcast}

Wenn sich eine mobile Anwendung beim {{site.data.keyword.mobilepushshort}}-Service registriert, kann sie Rundsendungen (Broadcasts) empfangen. Broadcast-Benachrichtigungen sind Benachrichtigungen, die all diejenigen Geräte zum Ziel haben, auf denen eine Anwendung installiert und für den {{site.data.keyword.mobilepushshort}}-Service konfiguriert ist. Broadcast-Benachrichtigungen sind standardmäßig für jede beliebige Anwendung aktiviert, die Push-Benachrichtigungen empfangen kann. Alle Anwendungen, die für den {{site.data.keyword.mobilepushshort}}-Service aktiviert sind, verfügen über eine vordefinierte Subskription für den Tag 'Push.ALL', der vom Server zum Übertragen von Broadcast-Benachrichtigungen an alle Geräte verwendet wird. Zum Senden einer Broadcast-Benachrichtigung mithilfe der REST-API von Push müssen Sie während der Übergabe an die Ressource der Nachrichten sicherstellen, dass als 'Ziel' eine leere JSON-Datei angegeben ist.

###Tagbasierte Benachrichtigungen
{: tag-based-notifications}

Tag-Benachrichtigungen sind Benachrichtigungen, die all diejenigen Geräte zum Ziel haben, die einen bestimmten Tag subskribiert haben. Tagbasierte Benachrichtigungen ermöglichen die Segmentierung von Benachrichtigungen auf der Basis von Subjektbereichen oder Themen. Benachrichtigungsempfänger können wählen, dass sie Benachrichtigungen nur empfangen, wenn deren Inhalt ein Thema hat, das von Interesse ist. Daher bieten tagbasierte Benachrichtigungen die Möglichkeit, Empfänger zu segmentieren. Diese Funktion ermöglicht es, dass Tags definiert werden und anschließend Nachrichten geordnet nach Tags gesendet und empfangen werden. Eine Nachricht wird zielgruppenspezifisch nur an die Geräte gesendet, die einen Tag subskribiert haben. Sie müssen zunächst Tags für die Anwendung erstellen, die Tagsubskriptionen einrichten und anschließend die tagbasierten Benachrichtigungen starten. Zum Senden einer tagbasierten Benachrichtigung mithilfe der REST-API müssen Sie sicherstellen, dass während der Übergabe an die Ressource der Nachricht die Tagnamen ('tagNames') angegeben werden. 

###Unicast-Benachrichtigungen
{: unicast-notifications}

Unicast-Benachrichtigungen sind Nachrichten, die ein bestimmtes Gerät oder einen bestimmten Benutzer zum Ziel haben. Unicast-Benachrichtigungen, die auf Geräte abzielen, benötigen keine zusätzliche Konfiguration und werden standardmäßig aktiviert, wenn die Anwendung für Push-Benachrichtigungen aktiviert wird.

Bei Unicast-Benachrichtigungen, die Benutzer zum Ziel haben, ist jedoch Folgendes erforderlich: 

- Zuordnen einer Benutzer-ID zu einem Gerät beim Registrieren des mobilen Geräts für Push-Benachrichtigungen.   

- Autorisieren einer solchen Benutzer-ID-Registrierung durch Übergeben eines geheimen Clientschlüssels 'clientSecret', dessen Zuordnung beim Binden einer Back-End-Anwendung an den {{site.data.keyword.mobilepushshort}}-Service erfolgt.  

Normalerweise führt eine mobile Anwendung zuerst einen Authentifizierungszyklus aus, in dessen Verlauf der Benutzer mobiler Anwendungen bei einem Authentifizierungsservice wie [Mobile Client Access](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html) authentifiziert wird. Nach der erfolgreichen Authentifizierung wird die ID des authentifizierten Benutzers dann zusammen mit einem geheimen Clientschlüssel an die API für Push-Geräteregistrierungen übergeben. Das Vorhandensein eines geheimen Clientschlüssels setzt die Zuordnung nur von autorisierten Benutzer-IDs bei der Registrierung mobiler Geräte um. Zum Senden einer Unicast-Benachrichtigung über die REST-API müssen Sie sicherstellen, dass während der Übergabe an die Ressource der Nachricht die Geräte- oder Benutzer-IDs ('deviceId' bzw. 'userId') angegeben werden. 

###Plattformbasierte Benachrichtigungen
{: platform-based-notifications}

Benachrichtigungen können zielgruppenspezifisch an eine bestimmte Geräteplattform gerichtet werden. Eine Benachrichtigung kann beispielsweise nur an alle Android-Benutzer gesendet werden. Stellen Sie zum Senden einer plattformbasierten Benachrichtigung mithilfe der REST-API sicher, dass die Zielplattformen während der Übergabe an eine Nachrichtenressource bereitgestellt werden. Geben Sie die Plattformen als Array an. Folgende Plattformen werden unterstützt:
* A (Apple)
* G (Google)

## Größe von {{site.data.keyword.mobilepushshort}}-Nachrichten
{: #push-message-size}

Die Größe der Nutzdaten bei {{site.data.keyword.mobilepushshort}}-Nachrichten richtet sich nach den Mediatoren.  

###iOS
{: ios-message-size}

Ab iOS 8 beträgt die zulässige maximale Größe 2 Kilobyte. Der Push Notification-Service für Apple sendet keine Benachrichtigungen, die dieses Limit überschreiten.

###Android
{: android-message-size}

Für die Android-Plattform gibt es keine Einschränkungen.
