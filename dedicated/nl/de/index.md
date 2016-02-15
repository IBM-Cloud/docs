{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} Dedicated
{: #dedicated}

*Letzte Aktualisierung: 18. Januar 2016*

{{site.data.keyword.Bluemix}} ist eine cloudbasierte Plattform mit offenen Standards für das Erstellen, Ausführen und Verwalten von Anwendungen. Mit {{site.data.keyword.Bluemix_notm}} Dedicated erhalten Sie die Leistung und Einfachheit von {{site.data.keyword.Bluemix_notm}} &mdash; und zwar in Ihrer eigenen dedizierten SoftLayer-Umgebung, die sowohl mit der {{site.data.keyword.Bluemix_notm}} Public-Umgebung als auch Ihrem eigenen Netz sicher verbunden ist.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} Dedicated umfasst einen privaten Katalog, in dem die dedizierten Services angezeigt werden, die ausschließlich Ihnen zur Verfügung stehen. Er umfasst außerdem zusätzliche Services, die aus {{site.data.keyword.Bluemix_notm}} Public syndiziert werden und die Sie verwenden können.

{{site.data.keyword.Bluemix_notm}} Dedicated basiert auf SoftLayer. Das bedeutet, dass Ihnen eine besonders leistungsfähige Cloudinfrastruktur zur Verfügung steht. In jedem Rechenzentrum besteht rund um die Uhr die ganze Woche über ein Sicherheitsschutz mit strengen Kontrollen. Sie und IBM greifen über einen VPN-Tunnel und ein privates VLAN auf die {{site.data.keyword.Bluemix_notm}} Dedicated-Instanz zu.

![{{site.data.keyword.Bluemix_notm}} Dedicated](images/detaileddedicated.png "{{site.data.keyword.Bluemix_notm}} Dedicated")

*Abbildung 1. Ausführliches Diagramm zu {{site.data.keyword.Bluemix_notm}} Dedicated*

{{site.data.keyword.Bluemix_notm}} Dedicated-Umgebungen besitzen in Hinblick auf Infrastruktur, Betriebssicherheit und physische Sicherheit dieselben Sicherheitsstandards wie die öffentliche {{site.data.keyword.Bluemix_notm}}-Plattform. Der Zugriff von Entwicklern auf die dedizierte {{site.data.keyword.Bluemix_notm}}-Plattform wird jedoch durch Ihre LDAP-Richtlinien gesteuert, die bei der Einrichtung Ihrer Umgebung durch das {{site.data.keyword.Bluemix_notm}}-Team konfiguriert werden können. Sie können innerhalb der dedizierten Umgebung Benutzerrollen und Berechtigungen verwalten. Weitere Informationen finden Sie unter [Benutzer und Berechtigungen verwalten](../admin/index.html#oc_useradmin).

{{site.data.keyword.Bluemix_notm}} Dedicated wird mit vollständig integrierten {{site.data.keyword.Bluemix_notm}}-Laufzeiten und 128 GB Anwendungsspeicher ausgeliefert.

Des Weiteren gibt es eine Reihe inbegriffener Standardservices sowie optionale Services, die Sie für Ihre dedizierte Instanz auswählen können.

| **Typ**        | **Name**            | **Beschreibung** |      
|-----------------|-------------------|-------------------|
| Inbegriffen | {{site.data.keyword.autoscaling}} | Dynamisches Erhöhen oder Verringern der Rechenleistung Ihrer Anwendung basierend auf Richtlinien. Mit diesem Service können Sie Ihre {{site.data.keyword.Bluemix_notm}} Dedicated-Umgebung unbegrenzt nutzen. |
| Inbegriffen | {{site.data.keyword.datacshort}} | Dieser Service bietet ein speicherinternes Datengitter, durch das Szenarios mit verteiltem Caching für Ihre Apps unterstützt werden. Umfasst 50 GB speicherinternen Cache. |
| Optional | {{site.data.keyword.mql}} | {{site.data.keyword.mqlfull}} for {{site.data.keyword.Bluemix_notm}} ist ein cloudbasierter Nachrichtenübertragungsservice, der flexible und benutzerfreundliche Messaging-Funktionalität für {{site.data.keyword.Bluemix_notm}}-Apps zur Verfügung stellt. {{site.data.keyword.mql}} bietet eine Messaging-Lösung mit geringem Verwaltungsaufwand. Mit {{site.data.keyword.mql}} können Sie Ihre Apps reaktionsfähiger und flexibler gestalten und mithilfe einer einfachen und leistungsfähigen API die Arbeitslast zwischen Apps aufteilen und auslagern. |
| Optional | {{site.data.keyword.dashdbshort}} | Verwenden Sie dashDB zum Speichern relationaler Daten (einschließlich spezieller Datentypen wie Geodaten). Analysieren Sie die Daten anschließend mit SQL oder mit erweiterten integrierten Analyseverfahren wie Vorhersageanalyse, Data Mining oder Geodatenanalyse. |
|Optional | {{site.data.keyword.APIM}} | Verwenden Sie den {{site.data.keyword.APIMfull}}-Service zum Erstellen, Verwalten und Mitteilen von APIs. Sie können mit einer Proxy-URL oder durch Zusammenstellen von Daten aus HTTP-Datenquellen neue APIs mit Ressourcen importieren. Die Verwendung des {{site.data.keyword.APIM}}-Service bietet den Vorteil, dass Sie steuern können, wie Ihre APIs genutzt werden. |
|Optional | {{site.data.keyword.SecureGateway}} | Der {{site.data.keyword.SecureGateway}}-Service stellt eine sichere Methode zur Verbindung von {{site.data.keyword.Bluemix_notm}}-Anwendungen mit fernen Standorten lokal oder in der Cloud bereit.  |

*Tabelle 1. Dedizierte Services*


##{{site.data.keyword.Bluemix_notm}} Dedicated einrichten
{: #setupdedicated}

{{site.data.keyword.Bluemix_notm}} Dedicated wurde konzipiert, um eine private Version des Produktangebots {{site.data.keyword.Bluemix_notm}} Public bereitzustellen. Sie können {{site.data.keyword.Bluemix_notm}}-Services und -Laufzeiten verwenden, um Ihre Datenverarbeitungsanforderungen in einem von IBM gehosteten SoftLayer-Konto zu unterstützen.

IBM bietet Ihnen über eine kennwortgesicherte Anmeldung Zugriff auf {{site.data.keyword.Bluemix_notm}} Dedicated. Sie können auf die Services, Laufzeiten und zugehörigen Ressourcen zugreifen und {{site.data.keyword.Bluemix_notm}}-Apps bereitstellen und entfernen. IBM nutzt mehrere SoftLayer-Positionen, um {{site.data.keyword.Bluemix_notm}} Dedicated bereitzustellen, sodass sich Ihre private Version an einem Standort in Ihrer Nähe befindet.

Gehen Sie wie folgt vor, um Ihre private Version von {{site.data.keyword.Bluemix_notm}} einzurichten:

<ol>
<li>Wenden Sie sich an Ihren zugewiesenen IBM Kundenbeauftragten oder <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">wenden Sie sich an {{site.data.keyword.Bluemix_notm}}</a>, um mit der Arbeit zu beginnen.</li>
<li>Erarbeiten Sie mit IBM Ihre Gebühren für Ihre {{site.data.keyword.Bluemix_notm}} Dedicated-Instanz. Die monatlich fällige Gebühr basiert auf den dedizierten Services, die Sie nutzen möchten. Hinzu kommt ein Abonnement für alle {{site.data.keyword.Bluemix_notm}} Public-Services. Sie erhalten dann eine Rechnung für alle Nutzungen, die über die Abonnementvereinbarung hinausgehen.</li>
<li>Ermitteln Sie die Fristen für die einzelnen Einrichtungsphasen Ihrer {{site.data.keyword.Bluemix_notm}} Dedicated-Instanz. Informationen zu den einzelnen relevanten Phasen und Tasks finden Sie unter <a href="index.html#rolesresponsibilities" target="_blank">{{site.data.keyword.Bluemix_notm}} Dedicated-Rollen und -Zuständigkeiten</a>.</li>
<li>Sie wählen den <a href="http://www.softlayer.com/data-centers" target="_blank">Standort des SoftLayer-Rechenzentrums</a> für Ihre dedizierte Instanz aus. Anschließend werden Ihre dedizierte Plattform und Ihr Konto erstellt. Für Ihr Konto ermitteln Sie die Personen in Ihrer Organisation für die Rollen, die benötigt werden, um Ihre dedizierte Instanz betriebsbereit zu machen. Informationen zu den Rollen, die Sie zuweisen, finden Sie unter <a href="index.html#rolesresponsibilities" target="_blank">{{site.data.keyword.Bluemix_notm}} Dedicated-Rollen und -Zuständigkeiten</a>.
</li>
<li>Definieren Sie die Netzkonnektivität zwischen Ihrem Unternehmensnetz und Ihrer {{site.data.keyword.Bluemix_notm}} Dedicated-Instanz und richten Sie sie ein.
	<ol type="a">
	<li>IBM installiert die Überwachungs- und Sicherheitsinfrastruktur für die dedizierte Instanz.</li>
	<li>IBM installiert die von Ihnen ausgewählten dedizierten Single-Tenant-Services.</li>
	<li>Sie stellen die Netzkonfiguration und die Endpunkte z. B. für IP-Adressen oder Firewalls sowie Zugriff auf Ihr LDAP für die Integration mit {{site.data.keyword.Bluemix_notm}} bereit.</li>
	</ol>
</li>
<li>Ermitteln Sie die Rollen für Ihr Verwaltungsteam für die Umgebung und weisen Sie sie zu.
	<ol type="a">
	<li>IBM konfiguriert den Netzzugriff und LDAP Ihren Angaben entsprechend. Die von Ihnen bestimmten Ansprechpartner erhalten Verwaltungszugriff. Sie müssen auch einen Ansprechpartner für die Unterstützung und die Abrechnung bestimmen.</li>
	<li>IBM richtet in Ihrer dedizierten Umgebung einen syndizierten Katalog ein, um Ihnen Ihre dedizierten Services zu zeigen. Der syndizierte Katalog umfasst außerdem zusätzliche Services, die aus {{site.data.keyword.Bluemix_notm}} Public syndiziert werden und die Sie verwenden können. Sie können auf der Basis Ihrer Kriterien für Datenschutz und Sicherheit entscheiden, welche öffentlichen Services die Anforderungen Ihres Unternehmens erfüllen.</li>
	<li>Sie überprüfen die Netz- und Firewallkonfiguration sowie den LDAP-Endpunkt und -Zugriff.</li>
	</ol>
</li>
</ol>

Für die Erstbereitstellung und Erstkonfiguration Ihrer Umgebung können Sie einen Prozess wie in der folgenden Liste dargestellt erwarten. Details dazu, wer für die einzelnen Tasks verantwortlich ist, finden Sie unter [Rollen und Zuständigkeiten](../dedicated/index.html#rolesresponsibilities).

<ol>
<li>Sie wählen das Rechenzentrum aus, das als Host Ihrer dedizierten Instanz verwendet werden soll. Weitere Informationen zu Optionen für das Rechenzentrum finden Sie unter <a href="http://www.softlayer.com/data-centers" target="_blank">Standort des SoftLayer-Rechenzentrums</a>.</li>
<li>Sie geben die Domänennamen für die Bereitstellung und die gewünschten IDs an. Sie erhalten drei Domänen, wenn Sie Ihre {{site.data.keyword.Bluemix_notm}}-Instanz einrichten. Sie wählen das Präfix für <code>*mycompany*.*region*.bluemix.net</code> und <code>*mycompany*.*region*.mybluemix.net</code> aus. Und Sie wählen den vollständigen Name für die dritte Domäne aus.<br />
<p>Sie können so viele angepasste Domänen wählen, wie Sie möchten. Sie sind jedoch für die Zertifikate für die angepassten Domänen verantwortlich. Informationen zur Erstellung einer angepassten Domäne finden Sie unter <a href="../manageapps/updapps.html#domain">Angepasste Domäne erstellen und verwenden</a>.</p></li>
<li>Sie geben einen Eigner für das öffentliche Konto an, das zur Darstellung Ihres Unternehmens in {{site.data.keyword.Bluemix_notm}} Public verwendet wird. IBM verwendet dieses Konto zur Verfolgung der Nutzung syndizierter Services.</li>
<li>Sie wählen den Typ der sicheren Verbindung zu Ihrem Rechenzentrum aus. Sie haben die Auswahl zwischen SoftLayer VPN, SoftLayer Direct Link und AT&T Net Bond.</li>
<li>Sie entscheiden, ob ein Zugriff auf Ihre dedizierte Umgebung über das öffentliche Internet erfolgen soll.</li>
<li>Sie wählen den Typ der Authentifizierung aus, die verwendet werden soll. Sie haben die Auswahl zwischen IBM ID oder Active Directory. Informationen zur Verwendung und Registrierung einer IBM ID finden Sie auf der Seite für <a href="https://www.ibm.com/account/profile/us?page=regfaqhelp#4">Hilfe und FAQ</a>.
</li>
<li>Sie ermitteln die Rollen für Ihr Verwaltungsteam für die Umgebung und weisen sie zu. Informationen zu den Rollen, die Sie zuweisen müssen, finden Sie unter <a href="index.html#rolesresponsibilities" target="_blank">{{site.data.keyword.Bluemix_notm}} Dedicated-Rollen und -Zuständigkeiten</a>.</li>
<li>IBM stellt die zentrale Plattform bereit, die elastische Laufzeiten, Konsolen, Verwaltungsfunktionen und Überwachung umfasst.</li>
<li>IBM konfiguriert Ihren Verwaltungszugriff auf die Umgebung.</li>
<li>Sie können mit der Verwendung Ihrer dedizierten Instanz beginnen, die vom IBM Operationsteam überwacht wird, um auf Alerts zu reagieren.</li>
</ol>

Nach der Einrichtung Ihrer {{site.data.keyword.Bluemix_notm}}-Instanz können Sie die Ihre {{site.data.keyword.Bluemix_notm}}-Instanz über die Verwaltungsseite ('Administration') überwachen und verwalten. Weitere Informationen finden Sie unter [{{site.data.keyword.Bluemix_notm}} Local und Dedicated verwalten](../administer/index.html#mng). Weitere Informationen zu Upgrades und Wartung finden Sie unter [Dedizierte Instanz warten](index.html#maintaindedicated).

##Rollen und Zuständigkeiten
{: #rolesresponsibilities}

Wenn Sie ein {{site.data.keyword.Bluemix_notm}} Dedicated-Konto einrichten, ermitteln Sie die Personen in Ihrer Organisation für die Rollen, die benötigt werden, um Ihre dedizierte Instanz betriebsbereit zu machen.

###Rollen

In der folgenden Liste sind die Kundenrollen und -zuständigkeiten enthalten, die Sie zuweisen:

<dl>
<dt>**Zentraler Ansprechpartner für das Beschaffungswesen**</dt>
<dd>Arbeitet mit dem IBM Ansprechpartner zusammen an der Einrichtung Ihrer {{site.data.keyword.Bluemix_notm}} Dedicated-Umgebung. Dazu gehört das Ermitteln geeigneter Personen in Ihrer Organisation für die Arbeit an den einzelnen Aspekten des Projekts. Die Person, die dieser Rolle zugewiesen ist, übernimmt eine Projektmanagementrolle und überwacht die Musterauswahl, geschäftlichen Vereinbarungen und die Regelung für den Zugang zu Kundenressourcen. Dieser zentrale Ansprechpartner ist der allgemeine Ansprechpartner für die Einrichtung der dedizierten Instanz und die Überwachung des Bereitstellungsprozesses.</dd>
<dt>**Compliance-Manager**</dt>
<dd>Arbeitet mit dem IBM Ansprechpartner zusammen, um eine Topologie
und eine Bereitstellungsoption auszuwählen, die Ihren Sicherheitsanforderungen entsprechen. Die Person, die dieser Rolle zugewiesen ist, legt gemeinsam mit dem IBM Compliance-Berater fest, mit welchen Implementierungsmustern die Compliance-Ziele erreicht werden. </dd>
<dt>**Netzspezialist**</dt>
<dd>Arbeitet mit dem IBM Ansprechpartner zusammen an den Netzplänen für die {{site.data.keyword.Bluemix_notm}}-Bereitstellung.
Die Person, die dieser Rolle zugewiesen ist, überprüft die von IBM vorausgesetzten Netzspezifikationen und arbeitet gemeinsam mit IBM an einem Implementierungsplan. Am Ende der Installations- und Verifizierungsphase prüft die Person, die dieser Rolle zugewiesen ist, dass die Netzkonfiguration im Einklang mit den Unternehmensstandards ist. </dd>
<dt>**Zentraler DevOps-Ansprechpartner**</dt>
<dd>Arbeitet mit dem IBM Ansprechpartner zusammen, um die für die {{site.data.keyword.Bluemix_notm}}-Plattform, -Services und -Laufzeiten benötigten Wartungsaktualisierungen zu planen und anzuwenden. Die Person, die dieser Rolle zugewiesen ist, arbeitet auch mit dem
IBM Ansprechpartner an der Konfiguration Ihrer {{site.data.keyword.Bluemix_notm}} Dedicated-Instanz. </dd>
</dl>

Ihre Ansprechpartner beim Kunden arbeiten mit dem Dedicated-Fachmann und anderen IBM Spezialisten zusammen, um sicherzustellen, dass Sie immer die benötigte Unterstützung erhalten. Der Dedicated-Fachmann ist Ihr Ansprechpartner im {{site.data.keyword.Bluemix_notm}}-Entwicklungssupport-Team, der die folgenden Tasks ausführt:

<ul>
<li>Schnelle Einführung Ihrer {{site.data.keyword.Bluemix_notm}} Dedicated-Umgebung.</li>
<li>Bereitstellung wertvoller Schulungs- und Weiterbildungsmaterialien, damit Sie selbstständiger arbeiten können.</li>
<li>Pflege eine langfristigen Beziehung zwischen Ihnen und den zuständigen {{site.data.keyword.Bluemix_notm}}-Entwicklungs-, -Support- und -Services-Mitarbeitern.</li>
</ul>

Das {{site.data.keyword.Bluemix_notm}}-Support- und -Operationsteam, das gemeinsam mit Ihnen an der {{site.data.keyword.Bluemix_notm}}-Instanz arbeitet, kann auf die lokale Umgebung zugreifen, tut dies aber nur unter den folgenden Umständen.

<ul>
<li>Zum Antworten auf Alerts und zum Durchführen einer Betriebswartung</li>
<li>Zum Reproduzieren eines Problems, das in einem Supportticket berichtet wurde</li>
</ul>

###Zuständigkeiten

Von der Einrichtung Ihrer Umgebung bis hin zur kontinuierlichen Wartung muss eine Vielfalt von Tasks abgeschlossen werden. Die folgende Tabelle beschreibt grob die erforderlichen Tasks und den Eigner zum Abschließen der Task in den Phasen der Konzeption, des Fortschritts und der Fertigstellung.

In der Konzeptionsphase wird die {{site.data.keyword.Bluemix_notm}} Dedicated-Umgebung eingerichtet. Die primären Ziele dieser Phase sind unter anderem:

- Überprüfung der finanziellen Vereinbarung und Festlegung der Meilensteindaten für die Bereitstellung.
- Erstellung der {{site.data.keyword.Bluemix_notm}}-Plattform und Bereitstellung von Zugriff auf Laufzeiten und Services.
- Definition und Einrichtung der Netzkonnektivität zwischen Ihrem Unternehmensnetz und {{site.data.keyword.Bluemix_notm}}-Operationen.
- Ermittlung und Zuweisung von Rollen für Ihr Verwaltungsteam.

*Tabelle 1. Tasks in der Konzeptionsphase*

| **Task** | **Taskdetails** | **Zuständiges Team** |
|----------|------------------|-----------------------|
|Festlegen von Konformitätsstandards | Ermitteln Sie Behörden-, Branchen- und proprietäre Unternehmensstandards, die für die Umgebung erforderlich sind. | Kunde |
|Erstellen eines Sicherheits- und Konformitätsintegrationsplans | Erstellen Sie einen Sicherheits- und Integrationsplan, der Kosten, Planung und Ressourcen einbezieht, die für die Einhaltung von Sicherheitsbestimmungen erforderlich sind. | IBM |
|Genehmigen des Konformitätsplans | Genehmigen Sie den Konformitätsplan. | Kunde |
|Dimensionieren der Umgebung |  	Dimensionieren Sie die Umgebung auf der Basis von vordefinierten Optionen, die die Hochverfügbarkeits- und Disaster-Recovery-Ziele sowie den ursprünglichen DEA und die Servicebereitstellung berücksichtigen, die zur Unterstützung der mit der Plattform erstellten Apps erforderlich sind. Gemeinsam mit IBM definieren Sie beispielsweise, welche Datenbanken erforderlich sind, welche Services im syndizierten Katalog des Benutzers angeboten werden und vieles mehr. | IBM und Kunde |
|Auswählen der Architektur | Wählen Sie die Architektur auf der Basis vordefinierter Optionen aus, die Hochverfügbarkeits- und Disaster-Recovery-Anforderungen berücksichtigen. | IBM |
|Definieren von Disaster-Recovery-Zielen | Definieren Sie die Disaster-Recovery-Anforderungen für die Umgebung. | Kunde |
|Erstellen eines Disaster-Recovery-Plans | Konsultieren und definieren Sie den Disaster-Recovery-Plan. IBM erstellt ein Disaster-Recovery-Modell und berät mit Ihnen, wo Sie Feedback bereitstellen und den Plan genehmigen. | IBM und Kunde |
|Erstellen eines Sicherungs- und Wiederherstellungsplans | Erstellen Sie einen Sicherungs- und Wiederherstellungsplan, der die Häufigkeit und die Anforderungen einer zentralen bzw. dezentralen Verteilung der Sicherung definiert. IBM sichert Fabric-Komponenten, IBM Services, Servicemetadaten wie Benutzerrollen und vieles mehr. Sie sichern alle anwendungsspezifischen Daten, für die Sie verantwortlich sind. | IBM und Kunde |
|Angeben von Tools für Ereigniserkennung und Problembestimmung | Geben Sie IBM Tools und Tools von Drittanbietern für die Ereigniserkennung und Problembestimmung auf der {{site.data.keyword.Bluemix_notm}}-Plattformebene an. | IBM |
|Definieren eines Eskalationsplans | Definieren Sie den Eskalationsplan zur Klassifizierung und Auflösung von Ereignissen, die von Überwachungskomponenten erkannt werden. | IBM |
|Unterzeichnen von Infrastruktur-, Plattform- und Supportvereinbarungen | Unterzeichnen Sie die Abonnementvereinbarung, einschließlich der finanziellen Vertragsbedingungen für die Umgebung. Unterzeichnen Sie eine Vereinbarung zur Netz- und Sicherheitsüberwachung. Unterzeichnen Sie ein Supportabonnement. | Kunde |
|Beschaffen einer Umgebung | Beschaffen Sie Rechenressourcen, Netz und Speicher, einschließlich Core- und Services-VLAN zum Hosten von {{site.data.keyword.Bluemix_notm}} sowie Bare-Metal-Services zum Hosten von Data Power und SoftLayer-Firewall. Stellen Sie eine Infrastruktur bereit, die einen VPN-Tunnel ermöglicht. | Kunde |
|Installieren von Fabric-, Anwendungs- sowie Überwachungs- und Verwaltungskomponenten | Installieren, konfigurieren und überprüfen Sie Fabric-Komponenten wie BOSH Director, Cloud-Controller, Statusmanager, Messaging, Routers, DEAs und Service-Provider sowie die Überwachungskomponenten, die im Eskalations- und Problemerkennungsplan definiert sind. | IBM |
|Installieren und Konfigurieren von Sicherheitskomponenten | Installieren und konfigurieren Sie Sicherheitskomponenten, die in den Überwachungs- und Eskalationsplan eingebunden sind, darunter IBM QRadar, Vault für Berechtigungsnachweise, Abwehrsystem gegen Angriffe von außen, IBM BigFix und IBM Security Privileged Identity Management. | IBM |
|Installieren und Konfigurieren von angepassten Komponenten |  	Installieren und konfigurieren Sie angepasste Komponenten, die sich außerhalb des Geltungsbereichs des {{site.data.keyword.Bluemix_notm}}-Produkts und der -Services befinden. | Kunde |
|Einrichten einer Netzerstkonfiguration | Richten Sie eine Netzerstkonfiguration mit Firewalls, DataPower, Fortigate und DNS ein. | IBM |
|Verbinden einer {{site.data.keyword.Bluemix_notm}}-Pipeline | Verbinden Sie eine {{site.data.keyword.Bluemix_notm}}-Pipeline für kontinuierliche Integration und Bereitstellung mit IBM Repositorys. | IBM |
|Anpassen externer Lösungskomponenten | Passen Sie Lastausgleichsfunktionen für Disaster-Recovery-Szenarios an. | Kunde |
|Installieren einer VPN-Lösung | Installieren Sie eine bidirektionale VPN-Lösung. | IBM |
|Konfigurieren eines Anmeldungsservers | Konfigurieren Sie den Anmeldungsserver für die Verwendung mit dem unternehmensweiten LDAP. | IBM |
|Verfolgen des Status von Sicherheits-, Konformitäts- und Prüfungsmaßnahmen  | Verfolgen Sie den Status bis zu dem Zeitpunkt, an dem alle Tools und Prozesse zum Erzielen der gewünschten Konformität vorhanden und einsatzbereit sind. | Kunde |
|Überprüfen der physischen Infrastruktur | Überprüfen Sie die Orte, an denen die Lösungskomponenten für Bedrohungen gehostet werden, und überprüfen Sie die Sicherheitsmaßnahmen zum Schutz des Rechenzentrums. | Kunde |
|Untersuchen der Überwachungssoftware | Untersuchen Sie Überwachungs- und Verwaltungskomponenten, wie im Eskalations- und Problembestimmungsplan definiert. | Kunde |
|Untersuchen des Betriebssystems | Stellen Sie sicher, dass das Betriebssystemimage Konfomitätsstandards entspricht. IBM stellt Zugriff auf das Betriebssystemimage bereit. | IBM und Kunde |

Als nächstes folgt die Fortschrittsphase. Die Fortschrittsphase beschreibt die laufende, interaktive Beziehung zwischen Ihnen und IBM Cloud. Die primären Ziele dieser Phase sind unter anderem:

- Überprüfen der Kapazität und Koordinieren von erforderlichen Anpassungen.
- Überprüfen von Wartungs- und Plattformverbesserungen.
- Koordinieren der Aktivitäten für Fehlerbehebung und Ursachenanalyse.

*Tabelle 2. Tasks in der Fortschrittsphase*

| **Task** | **Taskdetails** | **Zuständiges Team** |
|----------|------------------|-----------------------|
|Überprüfen von wöchentlichen Kapazitätsberichten | Überprüfen Sie die wöchentlichen Kapazitätsberichte und ergreifen Sie ggf. Korrekturmaßnahmen. | Kunde |
|Erstellen von monatlichen Projektionen | Erfassen Sie Informationen und erstellen Sie eine monatliche Projektion von Kapazität und Nutzung. | IBM und Kunde |
|Überprüfen von Kapazitätsprojektionen | Überprüfen Sie die Kapazitätsprojektionen hinsichtlich externer Ereignisse, die sich sowohl auf die Kapazität als auch auf geplante neue Implementierungen von Apps auswirken können. Arbeiten Sie gemeinsam mit IBM an der Überprüfung der Projektionen und der entsprechenden Planung. | IBM und Kunde |
|Überprüfen von Projektionen | Überprüfen Sie die Kapazitätsprojektionen hinsichtlich externer Ereignisse, die sich auf die Kapazität auswirken können. | Kunde |
|Anpassen der Kapazität |  Fügen Sie Kapazität hinzu oder entfernen Sie Kapazität nach Bedarf. | IBM |
|Veröffentlichen zukünftiger Aktualisierungen und Wartungen | Erstellen Sie eine Dokumentation für die erforderliche Wartung von IBM Komponenten. | IBM |
|Durchführen einer Wartung | Planen Sie gemeinsam mit IBM die erforderliche Wartung in einem 30-tägigen Zeitraum. Sie können innerhalb des 30-tägigen Zeitraums Daten angeben, an denen keine Arbeit ausgeführt wird, und IBM bemüht sich, die Wartung entsprechend zu planen. | IBM und Kunde |
|Adressieren von Bereitstellungsfehlern | Beheben Sie ggf. auftretende Bereitstellungsfehler für vom Kunden erstellte Services, die im Katalog implementiert werden. | IBM |
|Durchführen von Netz- und IP-Scans | Führen Sie tägliche und monatliche Netz- und IP-Scans durch. | IBM und Kunde |
|Bereitstellen von Zugriff auf Prüfprotokolle | Stellen Sie Zugriff auf alle Sicherheits- und Verwaltungsprüfprotokolle bereit.   | IBM und Kunde |
|Durchführen von Tests | Führen Sie regelmäßige Kontrollen für Operationstests und Penetrationstests von Drittanbietern durch. | IBM und Kunde |
|Statusberichterstattung, Prüfungskoordination und Konformitätsbesprechungen  | Führen Sie eine Statusberichterstattung, eine externe Prüfungskoordination und eine Präsentation bei Statusbesprechungen zur Konformitätsprüfung aus. | IBM |
|Prüfung der Beschäftigungssituation und Geschäftsanforderungen | Führen Sie eine vierteljährliche Prüfung der Beschäftigungssituation sowie eine Prüfung kontinuierlicher Geschäftsanforderungen für IBM Ansprechpartner aus, die Zugriff auf die Umgebung des Kunden haben. | IBM |
|Beheben von Sicherheitslücken | Beheben Sie berichtete Sicherheitslücken in der Plattform. | IBM |

Die finale Phase der Fertigstellung stellt das Ende der Beziehung zwischen Ihnen und IBM {{site.data.keyword.Bluemix_notm}} dar. Die primären Tasks in dieser Phase sind unter anderem:

* Beenden der finanziellen Vereinbarung
* Entfernen aller Netzverbindungen
* Recyceln der Infrastruktur

*Tabelle 3. Tasks in der Fertigstellungsphase*

| **Task** | **Taskdetails** | **Zuständiges Team** |
|----------|------------------|-----------------------|
|Beenden der finanziellen Vereinbarung | Erörtern und vereinbaren Sie ein Ende der finanziellen Vereinbarung. | IBM und Kunde |
|Stilllegen der Umgebung | Inaktivieren Sie den Zugriff auf und die Berechtigungsnachweise für die Umgebung. | IBM und Kunde |
|Entfernen von Kundennetzverbindungen | Entfernen Sie Netzverbindungen zwischen IBM und der Umgebung des Kunden. | IBM und Kunde |
|Recyceln der Infrastruktur | Ihre Umgebung wird auf der Basis von SoftLayer-definierten Prozessen recycelt. | IBM |

##Dedizierte Instanz warten
{: #maintaindedicated}

IBM wartet und installiert Aktualisierungen und Fixes, sofern IBM dies für die
{{site.data.keyword.Bluemix_notm}} Dedicated-Plattform, -Laufzeiten und
-Services für angemessen hält.

**Wichtig**: IBM behält sich das Recht vor,
Services zu unterbrechen, um im Bedarfsfall Notfallwartungen vorzunehmen. IBM
kann die geplanten Wartungszeiten ändern, wird Sie aber über solche Änderungen sowie über eventuelle
Notfallwartungen benachrichtigen.

Die folgenden Wartungsarten sind für
{{site.data.keyword.Bluemix_notm}} Dedicated erforderlich:
<dl>
<dt>**Standardwartungsfenster**</dt>
<dd>Die Services verwenden vordefinierte Standardwartungsfenster, die dazu führen können, dass die Services nicht verfügbar sind. IBM benötigt nicht die Genehmigung des Kunden, um Wartungsarbeiten durchzuführen, versucht jedoch, die Auswirkungen auf Ihre Services so gering wie möglich zu halten.<br />
<br />
IBM übermittelt per E-Mail, Telefon oder über andere Medien Rundsendungen zu den jeweils für ein Wartungsfenster
geplanten Änderungen.<br />
<br />
**Wichtig**: Einige Services stehen Ihnen während des Wartungszeitraums möglicherweise nicht zur Verfügung.</dd>

<dt>**Monatliches Änderungsfenster**</dt>
<dd>Das monatliche Änderungsfenster wird basierend auf der entsprechenden Koordination zwischen Ihnen und IBM innerhalb eines 21-tägigen Fensters angewendet. Sie können IBM bestimmte Daten oder Zeiten innerhalb dieses 21-tägigen Zeitfensters mitteilen, die für Sie ungünstig sind. IBM wird sich bemühen, Aktualisierungen außerhalb dieser angegebenen Daten oder Zeiten zu planen. Basierend auf den Anfragen teilt Ihnen IBM das Wartungsfenster mit. Monatliche Änderungsfenster haben für gewöhnlich keinerlei Auswirkungen auf die aktive Bluemix Dedicated-Umgebung.<br />
<br />
**Hinweis:** Wenn Sie für die Aktualisierung keine bestimmte Zeit anfordern, wird die Wartung automatisch am Ende des Zeitfensters durchgeführt.<br />
<br />
Wechseln Sie zu **ADMINISTRATION > SYSTEM INFORMATION**, um anstehende Aktualisierungen anzuzeigen, nicht verfügbare Daten festzulegen und Aktualisierungen zu genehmigen. Weitere Informationen zu Benachrichtigungen und zum Planen anstehender Aktualisierungen finden Sie unter <a href="../admin/index.html#oc_system">Systeminformationen anzeigen</a>.</dd>

<dt>**Sonstige**</dt>
<dd>IBM beabsichtigt, alle Wartungstätigkeiten, die Ihre Services
beeinträchtigen, insbesondere die Verfügbarkeit Ihrer {{site.data.keyword.Bluemix_notm}} Dedicated-Umgebung, -Laufzeiten und -Services auf die monatlichen und Standardaktualisierungen zu beschränken. In Ausnahmefällen können andere Änderungsfenster für die Verwaltung der Umgebung verwendet werden. IBM
wird sich in angemessenem Maße bemühen, die Auswirkungen auf Sie während solcher Änderungsfenster zu minimieren
und Sie im Voraus benachrichtigen.</dd>
</dl>

Arbeiten Sie mit Ihrem von IBM zugewiesenen Kundenbeauftragten zusammen, um die Wartung Ihrer dedizierten
Instanz festzulegen und sich auf ein Fenster für die Standardwartung zu einigen.

Falls nach einer Wartungsaktualisierung ein Problem berichtet wird, entscheiden Sie gemeinsam mit Ihrem IBM Ansprechpartner, ob es sinnvoll wäre, dass IBM die Aktualisierung rückgängig macht. Nachdem Sie sich geeinigt haben, macht IBM die Aktualisierung rückgängig und stellt die Umgebung in ihrem ursprünglichen Zustand wieder her.

## Disaster-Recovery
{: #dr}

{{site.data.keyword.Bluemix_short}} Public stellt eine kontinuierlich verfügbare Plattform für Innovation bereit. Mehrere Sicherheitsmaßnahmen garantieren, dass Ihre Organisationen, Bereiche und Apps immer verfügbar sind. Durch das Bereitstellen von Apps in mehreren geografischen Regionen lässt sich eine kontinuierliche Verfügbarkeit realisieren, die vor einem ungeplanten, gleichzeitigen Ausfall mehrerer Hardware- und Softwarekomponenten bzw. dem Ausfall eines gesamten Rechenzentrums schützt. Auf diese Weise sind selbst im Fall einer Naturkatastrophe an einem spezifischen Standort die verteilten Instanzen der {{site.data.keyword.Bluemix_notm}} Public-App an anderen Standorten weiterhin verfügbar.
{: shortdesc}

Disaster-Recovery für {{site.data.keyword.Bluemix_short}} Dedicated ist aufgrund einer kontinuierlichen Verfügbarkeit für Ihre Apps, der integrierten Hochverfügbarkeit der Plattform und der Möglichkeit, Ihre Instanz im Fall eines Fehlers wiederherzustellen, möglich. Ihre Aufgabe ist es, eine kontinuierliche Verfügbarkeit für Ihre Apps zu ermöglichen, indem Sie die Apps in mehreren Regionen bereitstellen. Hochverfügbarkeit ist über Technologien in Cloud Foundry und anderen Komponenten auf Plattformebene integriert. Und Sie können gemeinsam mit IBM sicherstellen, dass Ihre Daten ordnungsgemäß gesichert werden, falls Sie Ihre Instanz zu einem beliebigen Zeitpunkt wiederherstellen müssen.

### Kontinuierliche Verfügbarkeit für {{site.data.keyword.Bluemix_notm}} Dedicated aktivieren
{: #enabling}

Standardmäßig wird {{site.data.keyword.Bluemix_notm}} Public an mehreren Standorten bereitgestellt. Sie müssen jedoch folgende Schritte ausführen, um global verteilte {{site.data.keyword.Bluemix_notm}} Dedicated-Instanzen zu ermöglichen:

* Stellen Sie entweder manuell oder mithilfe eines automatisierten Prozesses sicher, dass Ihre Entwickler Apps in mehr als einer Region bereitstellen. Regionen sollten mehr als 200 km auseinander liegen, damit sichergestellt ist, dass eine Naturkatastrophe nicht beide Standorte betrifft.
* Konfigurieren Sie eine globale Lastausgleichsfunktion wie Akamai oder Dyn, um auf Apps in mindestens zwei unterschiedlichen Regionen zu verweisen.

**Hinweis**: Nicht alle {{site.data.keyword.Bluemix_notm}}-Services unterstützen eine regionale Verteilung. Wenn Sie eine Anwendung erstellen, müssen Sie, falls Sie eine geografische Verteilung erzielen möchten, sicherstellen, dass die von dieser Anwendung verwendeten Services über eine Datensynchronisation als Schlüsselfunktion verfügen.

#### {{site.data.keyword.Bluemix_notm}} Dedicated-Apps an mehreren Standorten bereitstellen
{: #deploying}

Für eine Bereitstellung an einem zweiten Standort bzw. an mehreren Standorten müssen Sie einen Prozess ganz ähnlich dem zur Aktivierung Ihres primären Standorts ausführen:

1. Aktivieren Sie eine neue dedizierte Umgebung, in der zusätzliche Instanzen Ihrer Anwendungen gehostet werden sollen. Wenden Sie sich zum Erstellen einer neuen Umgebung an Ihr IBM Vertriebsteam, das den Prozess einleitet. Weitere Informationen zum Einrichten einer dedizierten Instanz finden Sie unter [{{site.data.keyword.Bluemix_notm}} Dedicated einrichten](../dedicated/index.html#setupdedicated). Für den Zugriff auf die einzelnen Umgebungen müssen Sie sich bei jeder Umgebung separat anmelden. Die Standorte für die gehosteten Umgebungen sollten mindestens 200 km entfernt von dem ursprünglichen Standort liegen, damit ihre Verfügbarkeit sichergestellt werden kann.
2. Rufen Sie den eindeutigen Namen der Domäne ab, in der Ihre neue bereitgestellte App gehostet wird. Beispiel: Wenn Ihre ursprüngliche Domäne *mycompany.east.bluemix.net* ist, können Sie eine neue lokale Umgebung mit einer neuen Domäne wie *mycompany.west.bluemix.net* erstellen und die App in der neuen Domäne bereitstellen.
3. Stellen Sie Ihre ursprüngliche App jedes Mal auch an dem neuen Standort bereit. Weitere Informationen zur Bereitstellung finden Sie unter [Anwendung hochladen](../starters/upload_app.html).


#### Globale Lastausgleichsfunktion für {{site.data.keyword.Bluemix_notm}} Dedicated aktivieren
{: #glb}

Eine globale Lastausgleichsfunktion stellt nicht nur eine kontinuierliche Verfügbarkeit sicher und ist für eine Disaster-Recovery unverzichtbar, sie hat auch diverse andere Vorteile:

* Standardmäßige Weiterleitung von Benutzern zur nächstgelegenen {{site.data.keyword.Bluemix_notm}}-Region.
* Leistungsabhängige Weiterleitung.
* Gezielte Übertragung eines Prozentsatzes des Datenverkehrs an eine neue Anwendungsversion.
* Bereitstellung von Failover für einen Standort auf der Basis einer Regionsdiagnose.
* Bereitstellung von Failover für einen Standort auf der Basis einer Anwendungsdiagnose.
* Gewichtete Weiterleitung zwischen Endpunkten.

Sie können eine globale Lastausgleichsfunktion wie Akamai oder Dyn auswählen. Weitere Informationen zur Verwendung von Akamai als globaler Lastausgleichsfunktion finden Sie unter [Global Traffic Management](https://www.akamai.com/us/en/solutions/products/web-performance/global-traffic-management.jsp){: new_window}. Weitere Informationen zur Verwendung von Dyn als globaler Lastausgleichsfunktion finden Sie unter [4 Reasons Businesses Are Taking Global Load Balancing to the Cloud](http://dyn.com/blog/4-reasons-businesses-are-taking-global-load-balancing-to-the-cloud/){: new_window}.

### Hochverfügbarkeit
{: #ha}

Zusätzlich zur Aktivierung einer kontinuierlichen Verfügbarkeit stellt {{site.data.keyword.Bluemix_notm}} durch den Einsatz von Technologien, die in Cloud Foundry, Docker und andere Komponenten integriert sind, auch eine plattformübergreifende Hochverfügbarkeit bereit.

Zu diesen Technologien zählen die folgenden:

<dl>
<dt>Skalierbarkeit in Cloud Foundry</dt>
<dd>Ein Cloud Foundry <a href="https://docs.cloudfoundry.org/concepts/architecture/execution-agent.html" target="_blank">Droplet Execution Agent (DEA)</a> führt Diagnosen der integrierten Apps aus. Falls ein Problem mit der App oder dem DEA selbst auftritt, werden zusätzliche Instanzen der App in einem alternativen DEA bereitgestellt, um das Problem zu beheben. Weitere Informationen finden Sie unter <a href="https://docs.cloudfoundry.org/concepts/high-availability.html" target="_blank">Configuring CF for High Availability with Redundancy</a>.
</dd>
<dt>SoftLayer-Redundanz</dt>
<dd>Mit SoftLayer in dedizierten Umgebungen werden Daten in den einzelnen Cloudspeicherclustern mehrfach geschrieben und Speichercluster werden für den Fall eines Laufwerkausfalls mit Selbstheilungsfunktionen konfiguriert. Falls ein Problem mit einer virtuellen Maschine auftritt, versucht SoftLayer, die virtuelle Maschine auf einem anderen Host erneut zu starten.</dd>
<dt>Metadatensicherung</dt>
<dd>Metadaten werden mithilfe von SoftLayer EVault Backup an einem Standort in mindestens 200 km Entfernung gesichert.</dd>
</dl>

##Dedizierte Instanz wiederherstellen
{: #restorededicated}

{{site.data.keyword.Bluemix_notm}} Dedicated-Einstellungen, -Metadaten und -Konfigurationen werden für den Fall ungeplanter Ausfälle in der Umgebung regelmäßig gesichert. Zu den Daten, für deren Sicherung Sie zuständig sind, zählen Anwendungsdaten, Daten aus Clouddatenbankservices und Objektspeicher.

Im Rahmen der Datensicherung, die Systemmetadaten und Konfigurationen umfasst, führt IBM die folgenden Tasks aus:

<ul>
<li>Verschlüsselung aller Sicherungskopien und Verwaltung von Verschlüsselungsschlüsseln</li>
<li>Überwachung und Verwaltung der Sicherungsaktivität</li>
<li>Bereitstellung der verschlüsselten Sicherungsdateien</li>
<li>Wiederherstellen der angeforderten Daten</li>
<li>Beheben von Planungskonflikten beim Optionen des Sicherungs- und Fixmanagements</li>
</ul>

Da der Schutz privater Daten kritisch ist, ist IBM beim Umgang mit dem Sicherungsdateimanagement auf Ihre Kooperation angewiesen, damit die Dateien nicht an einen Ort außerhalb der Rechenzentren verschoben werden können. Deswegen fordert Sie IBM auf, die folgenden Tasks auszuführen:

<ul>
<li>Lagern Sie eine Kopie Ihrer verschlüsselten Sicherungsdaten analog zur Vorgehensweise für alle anderen von Ihnen verwalteten Sicherungsdaten aus.</li>
<li>Stellen Sie die Sicherungsdateien für den IBM Operator bereit, falls eine Wiederherstellung erforderlich sein sollte.</li>
</ul>

# Zugehörige Links
## Allgemein
* [Entdecken Sie: {{site.data.keyword.Bluemix_notm}} Dedicated](http://www.ibm.com/cloud-computing/bluemix/hybrid/dedicated/)
* [{{site.data.keyword.Bluemix_notm}} Local und {{site.data.keyword.Bluemix_notm}} Dedicated verwalten](../admin/index.html#mng)
* [Support kontaktieren](../troubleshoot/getting_customer_support.html#bluemix_support)
