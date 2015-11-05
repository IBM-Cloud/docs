{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} Local
{: #local}
*Letzte Aktualisierung: 20. Oktober 2015*

{{site.data.keyword.Bluemix}} Local bringt das Leistungsstärke und Beweglichkeit (der Geschäftsabläufe) der cloudbasierten {{site.data.keyword.Bluemix_notm}}-Plattform in Ihr Rechenzentrum. Mit {{site.data.keyword.Bluemix_notm}} Local können Sie die hochsensiblen Verarbeitungsprozesse hinter der Firewall des Unternehmens schützen und gleichzeitig eine sichere Verbindung und Synchronisation mit {{site.data.keyword.Bluemix_notm}} Public gewährleisten.
{:shortdesc}

IBM® verwendet Cloudoperationen als Service zum Überwachen und Verwalten Ihrer Umgebung, damit Sie sich auf das Erstellen von Apps und Services konzentrieren können, die in dieser Umgebung ausgeführt werden. IBM führt zudem Plattformaktualisierungen aus, während Sie sich um Ihre Geschäftsabläufe kümmern. 

{{site.data.keyword.Bluemix_notm}} Local umfasst einen privaten, syndizierten Katalog, in dem die lokalen Services angezeigt werden, die ausschließlich Ihnen zur Verfügung stehen. Er umfasst
außerdem zusätzliche Services, die aus {{site.data.keyword.Bluemix_notm}} Public
syndiziert werden und die Sie verwenden können. 

{{site.data.keyword.Bluemix_notm}} Local befindet sich auf einer virtuellen Maschine hinter der Firewall Ihres Unternehmens. Das bedeutet, dass Ihnen eine besonders leistungsfähige und sichere Cloudinfrastruktur zur Verfügung steht. Mit seiner Relay-Technologie installiert und verwaltet IBM {{site.data.keyword.Bluemix_notm}} Local in Ihrem Rechenzentrum und führt eine Fernüberwachung durch. 

Relay ist eine in {{site.data.keyword.Bluemix_notm}} Local integrierte Zustellungsfunktion, mit der IBM automatisch und konsistent Aktualisierungen für alle lokalen Implementierungen bereitstellt und Sie somit stets ein aktuelles, stabiles und sicheres System haben. Relay erreicht eine sichere Konnektivität mittels eines offenen VPN-Tunnels mit ausgehender SSL, der von der virtuellen Konzeptionsmaschine stammt. Dabei werden die entsprechenden Zertifikate der einzelnen {{site.data.keyword.Bluemix_notm}} Local-Instanzen verwendet. Bei dem Datenverkehr über diesen Tunnel handelt es sich um eine UrbanCode Deploy-Automatisierung zum Bereitstellen und Verwalten der Plattform, Rechenressourcen und Services für Ihre Instanz. 

![Übersicht über {{site.data.keyword.Bluemix_notm}} Local](images/bluemixlocalarchitecture.png "Übersicht über Bluemix Local")

*Abbildung 1. Detaillierte Übersicht über {{site.data.keyword.Bluemix_notm}} Local*

{{site.data.keyword.Bluemix_notm}} Local-Umgebungen besitzen
in Hinblick auf die Betriebssicherheit dieselben Sicherheitsstandards wie die
öffentliche {{site.data.keyword.Bluemix_notm}}-Plattform. Sie stellen die Hardware und Infrastruktur bereit und erhalten so die Kontrolle über die Infrastruktur und physische Sicherheit. Der Zugriff von Entwicklern auf die lokale
{{site.data.keyword.Bluemix_notm}}-Plattform wird durch Ihre LDAP-Richtlinien
gesteuert, die bei der Einrichtung Ihrer Umgebung durch das
{{site.data.keyword.Bluemix_notm}}-Team konfiguriert werden können. Sie können innerhalb der lokalen Umgebung über die Administrationskonsole Benutzerrollen und Berechtigungen verwalten. 

{{site.data.keyword.Bluemix_notm}} Local wird mit vollständig
integrierten {{site.data.keyword.Bluemix_notm}}-Laufzeiten und 64 GB
Rechenspeicher ausgeliefert. 

Des Weiteren gibt es eine Reihe verfügbarer Services für {{site.data.keyword.Bluemix_notm}} Local. 

| **Typ** | **Name** | **Beschreibung** |    
|----------|----------|-----------------|
|Inbegriffen | {{site.data.keyword.Bluemix_notm}}-Laufzeiten | Machen Sie mit Laufzeiten Ihre App schnell betriebsbereit, ohne VMs und Betriebssysteme einrichten und verwalten zu müssen. Alle {{site.data.keyword.Bluemix_notm}}-Laufzeiten stehen Ihnen zur Verwendung in Ihrer {{site.data.keyword.Bluemix_notm}} Local-Instanz zur Verfügung. |
|Inbegriffen | {{site.data.keyword.autoscaling}}| Dynamisches Erhöhen oder Verringern der Rechenleistung Ihrer Anwendung basierend auf Richtlinien. Mit diesem
Service können Sie Ihre {{site.data.keyword.Bluemix}} Local-Umgebung
unbegrenzt nutzen. |
|Optional |{{site.data.keyword.datacshort}}| Dieser Service bietet ein speicherinternes Datengitter, durch das Szenarios mit verteiltem
Caching für Ihre Apps unterstützt werden. Umfasst 50 GB speicherinternen Cache.  |
|Optional | {{site.data.keyword.APIM}} | Verwenden Sie den {{site.data.keyword.APIMfull}}-Service
zum Erstellen, Verwalten und Mitteilen von APIs. Sie können mit einer Proxy-URL oder
durch Zusammenstellen von Daten aus HTTP-Datenquellen neue APIs mit Ressourcen importieren. Die
Verwendung des {{site.data.keyword.APIM}}-Service bietet den Vorteil, dass Sie steuern können, wie
Ihre APIs genutzt werden.  |

*Tabelle 1. Lokale Services*

##{{site.data.keyword.Bluemix_notm}} Local-Instanz einrichten
{: #setuplocal}

{{site.data.keyword.Bluemix_notm}} Local wurde konzipiert,
um eine private Version des Produktangebots {{site.data.keyword.Bluemix_notm}}
Public bereitzustellen, die auf Ihrer eigenen, von Ihnen verwalteten Hardware gehostet ist. Sie können {{site.data.keyword.Bluemix_notm}}-Services
und -Laufzeiten verwenden, um Ihre Datenverarbeitungsanforderungen in einer sicheren, vom Kunden gehosteten und verwalteten Cloudumgebung zu unterstützen. 

IBM bietet Ihnen über eine kennwortgesicherte Anmeldung Zugriff auf
{{site.data.keyword.Bluemix_notm}} Local. Sie können auf die Services,
Laufzeiten und zugehörigen Ressourcen zugreifen und
{{site.data.keyword.Bluemix_notm}}-Apps bereitstellen und entfernen. Überprüfen Sie die folgenden Schritte zur Arbeit mit Ihrem IBM Ansprechpartner zum Einrichten Ihrer lokalen Instanz von {{site.data.keyword.Bluemix_notm}}. 

Gehen Sie wie folgt vor, um Ihre private Version von
{{site.data.keyword.Bluemix_notm}} einzurichten: 

<ol>
<li>Prüfen Sie die <a href="index.html#localinfra">Infrastrukturanforderungen für {{site.data.keyword.Bluemix_notm}} Local</a> für die Einrichtung der lokalen Instanz. </li>
<li>Wenden Sie sich an Ihren zugewiesenen IBM Kundenbeauftragten oder wenden
Sie sich an <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">{{site.data.keyword.Bluemix_notm}}</a>,
um mit der Arbeit zu beginnen. </li>
<li>Erstellen Sie Ihre Vereinbarung zu {{site.data.keyword.Bluemix_notm}} Local einschließlich Meilensteindaten für die Bereitstellung mit IBM. <ol type="a">
	<li>Erarbeiten Sie mit IBM Ihre Gebühren für Ihre
{{site.data.keyword.Bluemix_notm}} Local-Instanz. Die monatlich fällige Gebühr basiert auf den lokalen Services, die Sie nutzen möchten. Hinzu kommt
ein Abonnement für alle {{site.data.keyword.Bluemix_notm}} Public-Services. Sie erhalten dann eine Rechnung für alle Nutzungen, die über die Abonnementvereinbarung hinausgehen. </li>
	<li>Ermitteln Sie die Fristen für die einzelnen Einrichtungsphasen Ihrer
{{site.data.keyword.Bluemix_notm}} Local-Instanz. </li>
	</ol>
	</li>
<li>Nach dem Erstellen der Plattform und des Kontos ermitteln Sie die Personen in Ihrer Organisation für die Rollen,
die benötigt werden, um Ihre lokale Instanz betriebsbereit zu machen. Für jede Rolle gibt es einen entsprechenden IBM Ansprechpartner. <br />
<p>Kundenrollen:</p>
<dl>
<dt>**Zentraler Ansprechpartner für das Beschaffungswesen**</dt>
<dd>Arbeitet mit dem IBM Ansprechpartner zusammen an der Einrichtung Ihrer {{site.data.keyword.Bluemix_notm}} Local-Umgebung. Dazu gehört
das Ermitteln geeigneter Personen in Ihrer Organisation für die Arbeit an den einzelnen Aspekten des Projekts. Diese Rolle überwacht die Musterauswahl, geschäftliche Vereinbarungen und die Regelung für den Zugang zu Kundenressourcen. Dieser zentraler Ansprechpartner ist der allgemeine Ansprechpartner für die Einrichtung der lokalen Instanz. </dd>
<dt>**Compliance-Manager**</dt>
<dd>Arbeitet mit dem IBM Ansprechpartner zusammen, um eine Topologie
und eine Bereitstellungsoption auszuwählen, die Ihren Sicherheitsanforderungen entsprechen. Zudem legt der Compliance-Manager gemeinsam mit dem IBM Compliance-Berater fest, mit welchen Implementierungsmustern die Compliance-Ziele und -Zielsetzungen erreicht werden. </dd>
<dt>**Netz-Spezialist**</dt>
<dd>Arbeitet mit dem IBM Ansprechpartner zusammen an den Netzplänen für die {{site.data.keyword.Bluemix_notm}}-Bereitstellung.
Diese Rolle stellt dem IBM Ansprechpartner die Anforderungen zur Verfügung
und arbeitet am Implementierungsplan mit. Am Ende der Installations- und Verifizierungsphase zeichnet diese Rolle ab, dass die Netzkonfiguration im Einklang mit den Unternehmensstandards ist. </dd>
<dt>**Zentraler DevOps-Ansprechpartner**</dt>
<dd>Arbeitet mit dem IBM Ansprechpartner zusammen, um die für die {{site.data.keyword.Bluemix_notm}}-Plattform, -Services und -Laufzeiten benötigten Wartungsaktualisierungen zu planen und anzuwenden. Diese Rolle arbeitet auch mit dem
IBM Ansprechpartner an der Konfiguration Ihrer {{site.data.keyword.Bluemix_notm}} Local-Instanz zusammen. </dd>
</dl>
<p>IBM Rollen:</p>
<dl>
<dt>**IBM Bereitstellungsmanager**</dt>
<dd>Arbeitet gemeinsam mit dem zentralen Ansprechpartner für das Beschaffungswesen des Kunden an der Erstellung der Umgebung des Kunden. </dd>
<dt>**IBM Compliance-Berater**</dt>
<dd>Arbeitet mit dem Compliance-Manager des Kunden zusammen, um eine Topologie
und eine Bereitstellungsoption auszuwählen, die Ihren Sicherheitsanforderungen entsprechen. </dd>
<dt>**IBM Netzspezialist**</dt>
<dd>Arbeitet mit dem Netzspezialisten des Kunden zusammen an den Netzplänen für die Implementierung. Diese Rolle arbeitet gemeinsam mit dem Kunden, um anhand zusammengetragener Anforderungen einen Implementierungsplan zu erstellen. Zudem führt der Netzspezialist automatisierte Tests durch, um das physische Ergebnis des Implementierungsplans zu überprüfen. </dd>	
<dt>**Zentraler IBM DevOps-Ansprechpartner**</dt>
<dd>Arbeitet mit dem zentralen DevOps-Ansprechpartner des Kunden an der Installation und ständigen Wartung der Implementierungstopologie. Diese Rolle arbeitet mit dem Kunden zusammen, um die für die Plattform und Services erforderlichen Aktualisierungen zu planen und durchzuführen. </dd>
</dl>
</li>
<li>Sie stellen die Hardware bereit und IBM hilft Ihnen beim Definieren und Festlegen der Netzkonnektivität zwischen Ihrem Unternehmensnetz und Ihrer {{site.data.keyword.Bluemix_notm}} Local-Instanz. Weitere Informationen zu Infrastrukturanforderungen finden Sie im Abschnitt zu den <a href="index.html#localinfra">Infrastrukturanforderungen von {{site.data.keyword.Bluemix_notm}} Local</a>.
<ol type="a">
	<li>IBM konfiguriert den Netzzugriff und LDAP Ihren Angaben entsprechend. Die von Ihnen bestimmten Ansprechpartner erhalten Verwaltungszugriff. Sie müssen auch einen Ansprechpartner
für die Unterstützung und die Abrechnung bestimmen. </li>
	<li>IBM richtet in Ihrer lokalen Umgebung einen syndizierten Katalog ein,
um Ihnen Ihre lokalen Services und viele der öffentlichen {{site.data.keyword.Bluemix_notm}}-Services zu zeigen. </li>
	<li>Sie überprüfen die Netz- und Firewallkonfiguration sowie den LDAP-Endpunkt und -Zugriff. </li>
	</ol>
</li>
</ol>
	
##Infrastrukturanforderungen für {{site.data.keyword.Bluemix_notm}} Local
{: #localinfra}

Bei
{{site.data.keyword.Bluemix_notm}} Local
entscheiden Sie über die physische Sicherheit und die Hosting-Infrastruktur
für die lokale Instanz.
Die Anforderungen für das Einrichten von {{site.data.keyword.Bluemix_notm}}
Local sind von IBM wie im Folgenden angegeben festgelegt. 
###Hardware
Während es feste Anforderungen für Typ und Größe der verfügbaren Hardware gibt, können Sie sich
für eine beliebige Kombination entscheiden, die
die definierten
Gesamtressourcenanforderungen erfüllt. 
<dl>
<dt>**VMware ESXi-Hardware**</dt>
<dd>
Bei ESXi handelt es sich um eine Virtualisierungsebene, die auf physischen Servern ausgeführt
wird und auf abstrakter Ebene Prozessor, Hauptspeicher, Speicher und Ressourcen in mehreren virtuellen
Maschinen bereitstellt. Wählen Sie eine beliebige Kombination, die dem folgenden Gesamtumfang an
Ressourcen entspricht. Berücksichtigen Sie dabei, dass die Mindestanzahl an physischen Kernen pro
ESXi-Server
bei 8 liegt. Die folgenden Spezifikationen beziehen sich nur auf die {{site.data.keyword.Bluemix_notm}}-Kernlaufzeit.
<ul>
<li>48 physische Kerne mit jeweils mindestens 2.0 GHz</li>
<li>756 GB physischer Arbeitsspeicher</li>
</li>Gesamtdatenspeichergröße von 7,5 TB <ul>
<li>7 TB Datenspeicher für
{{site.data.keyword.Bluemix_notm}}</li>
<li>500 GB Datenspeicher für die virtuelle Anfangsmaschine</li>
</ul>
</ul>
<p><strong>Hinweis:</strong> Wenn Sie mehrere
Datenspeicher verwenden, muss das Präfix bei diesen Datenspeichern übereinstimmen. </p>
</dd>
<dt>**Hochverfügbarkeit**</dt>
<dd>
Um den Ausfall eines einzelnen Knotens auffangen zu können, müssen Sie über
n+1
ESXi-Server verfügen. Werden beispielsweise zwei ESXi-Server mit jeweils 16 Kernen verwendet,
wird ein
dritter ESXi-Server benötigt. <p><strong>Hinweis:</strong> Der VMware-Administrator beim Kunden kann über ein striktes
Durchsetzen
der automatischen Funktionsübernahme für hohe Verfügbarkeit im Cluster entscheiden, die
die Verfügbarkeit von Ressourcen garantiert. </p>
</dd>
<dt>**Netz**</dt>
<dd>
Zu den empfohlenen Voraussetzungen gehört eine für den Kunden zugängliche Portgruppe mit 10
IP-Adressen des Kundennetzes, die einen abgehenden Internetzugriff ermöglichen. Definieren Sie
anschließend ein zweites privates VLAN, das auf die ESXi-Server beschränkt ist, die für
{{site.data.keyword.Bluemix_notm}} Local verwendet werden.
Dieses VLAN wird in VMware als Portgruppe angezeigt. {{site.data.keyword.Bluemix_notm}}
Local verwendet dieses VLAN für das private Teilnetz, das sicherer ist und Probleme bei der
Weiterleitung verringern kann. </dd>
</dl>

###vCenter Server-Konfiguration
Informieren Sie sich über die folgenden
Anforderungen in Bezug auf Version, Rechenzentrum, Ressourcenpool und Datenspeicher. 
<dl>
<dt>**Unterstützte VMware-Versionen**</dt>
<dd>vCenter und ESXi 5.1 sowie 5.5</dd>
<dt>**Rechenzentrum**</dt>
<dd>Erstellen Sie ein Rechenzentrum, soweit noch nicht vorhanden. </dd>
<dt>**Ordner für Rechenzentrum**</dt>
<dd>Erstellen Sie einen VM-Ordner mit dem Namen des Clusters, wenn nicht geplant ist, das
ein Administratorzugriff erteilt werden soll, der über das Rechenzentrum weitergegeben wird. </dd>
<dt>**Cluster**</dt>
<dd>Erstellen Sie speziell für
{{site.data.keyword.Bluemix_notm}} Local einen Cluster.
Wählen Sie als Namen für den Cluster beispielsweise den Namen `bluemix`. </dd>
<dt>**Ressourcenpool**</dt>
<dd>Erstellen Sie einen Ressourcenpool für den
{{site.data.keyword.Bluemix_notm}} Local-Cluster.
Wählen Sie als Namen für den Ressourcenpool beispielsweise den Namen
`local`. </dd>
</dt>**Datenspeicher**</dt>
<dd>Erfordert 7,5 TB für die Erstbereitstellung von {{site.data.keyword.Bluemix_notm}}. <br />
<br />
**Hinweis**: Wenn
Sie mehrere Datenspeicher verwenden, müssen Sie sicherstellen, dass alle Datenspeicher mit
demselben Präfix beginnen. Die Datenspeicher könnten z. B. als
`bluemix_datastore_01` und
`bluemix_datastore_02` bezeichnet werden. </dd>
</dl>

###Netzbandbreite
Der empfohlene Durchsatz liegt bei 5
Mbps (Hochladen) und 5 Mbps (Herunterladen). Es ist im Schnitt mit einer monatlichen Datennutzung im
Umfang
von 10 GB zu rechnen. IBM richtet vereinbarte Fenster
ein, wenn umfangreiche Datenpakete eingehen, die bis zu 3 GB groß sein können. 
###VMware-Berechtigungen
Legen Sie die im Folgenden beschriebenen Rollen und
Berechtigungen fest. Für alle Berechtigungen ist eine Weitergabe eingerichtet. Wird eine Berechtigung
weitergegeben, wird sie bis in die unterste Objekthierarchie durchgereicht. Berechtigungen für
untergeordnete Objekte setzen Berechtigungen eines übergeordneten Objekts jedoch immer außer
Kraft.  
<dl>
<dt>**v Center Server**</dt>
<dd>Definieren Sie die Rolle als Nur-Lese-Berechtigung
ohne Weitergabe. <br />
<br />
**Note**: Diese Rolle wird benötigt,
um den Taskstatus für bestimmte Plattenoperationen abzurufen. </dd>
<dt>**Rechenzentrum**</dt>
<dd>Erstellen Sie die Rolle '{{site.data.keyword.Bluemix_notm}}' und erteilen Sie Berechtigungen für
den Datenspeicher (untergeordnete Dateioperationen und das Aktualisieren von Dateien virtueller Maschinen eingeschlossen).
<br />
<br />
**Hinweis**: Diese Rolle wird zur Unterstützung von Dateisendungen an die Datenspeicher benötigt. </dd>
<dt>**Cluster**</dt>
<dd>Definieren Sie die Rolle als Administratorrolle mit Weitergabe. </dd>
<dt>**Datenspeicher**</dt>
<dd>Definieren Sie die Administratorberechtigung und eine Weitergabe an alle
{{site.data.keyword.Bluemix_notm}}-Datenspeicher. </dd>
<dt>**Netz**</dt>
<dd>Definieren Sie öffentliche und private Portgruppen mit Administratorberechtigung ohne
Weitergabe. </dd>
</dl>

###Droplet Execution Agent-Pool
Jeder DEA (Droplet Execution Agent) ist wie folgt konfiguriert: 
- 16 bis 32 GB RAM
- 2 bis 4 vCPU
- 150 bis 300 GB Speicher


Ist z. B. der ESXi-Host mit 256 GB Hauptspeicher und 16 Kernen ausgestattet, werden
acht DEA hinzugefügt. Sind für den ESXi-Host 64 GB Hauptspeicher und 8 Kerne vorgesehen, werden zwei
ESXi-Server benötigt und es müssen vier DEA hinzugefügt werden. Weitere 1,5 TB Speicher werden für
jeweils vier DEA benötigt. Bei diesem Beispiel wird davon ausgegangen, dass ein DEA mit 32 GB RAM, 4
vCPUs und 300 GB Speicher konfiguriert ist. 

##Lokale Instanz warten
{: #maintainlocal}

IBM wartet und installiert Aktualisierungen und Fixes, sofern IBM dies für die Bluemix Local-Plattform, -Laufzeiten und
-Services für angemessen hält. Es kann vorkommen, dass Services während Wartungszeiten nicht verfügbar sind. 

**Wichtig**: IBM behält sich das Recht vor,
Services zu unterbrechen, um im Bedarfsfall Notfallwartungen vorzunehmen. IBM
kann die geplanten Wartungszeiten ändern, wird Sie aber über solche Änderungen sowie über eventuelle
Notfallwartungen benachrichtigen. 

Die folgenden Wartungsarten sind für {{site.data.keyword.Bluemix_notm}} Local erforderlich: 
<dl>
<dt>**Standardwartungsfenster**</dt>
<dd>Die Services verwenden vordefinierte Standardwartungsfenster, die dazu führen können, dass die Services nicht verfügbar sind. IBM benötigt nicht die Genehmigung des Kunden, um Wartungsarbeiten durchzuführen, versucht jedoch, die Auswirkungen auf Ihre Services so gering wie möglich zu halten. <br />
<br />
IBM übermittelt per E-Mail, Telefon oder über andere Medien Rundsendungen zu den jeweils für ein Wartungsfenster
geplanten Änderungen. <br />
<br />
**Wichtig**: Einige Services stehen Ihnen während des Wartungszeitraums möglicherweise nicht zur Verfügung. </dd>

<dt>**Monatliches Änderungsfenster**</dt>
<dd>Das monatliche Änderungsfenster wird basierend auf der entsprechenden Koordination zwischen Ihnen und IBM innerhalb eines 21-tägigen Fensters angewendet. Sie können IBM bestimmte Daten oder Zeiten innerhalb dieses 21-tägigen Zeitfensters mitteilen, die für Sie ungünstig sind. IBM wird sich bemühen, Aktualisierungen außerhalb dieser angegebenen Daten oder Zeiten zu planen. Basierend auf den Anfragen teilt Ihnen IBM das Wartungsfenster mit. Monatliche Änderungsfenster haben für gewöhnlich keinerlei Auswirkungen auf die aktive Bluemix Local-Umgebung. <br />
<br />
**Hinweis:** Wenn Sie für die Aktualisierung keine bestimmte Zeit anfordern, wird die Wartung automatisch am Ende des Zeitfensters durchgeführt. <br />
<br />
Wechseln Sie zu **ADMINISTRATION > SYSTEM INFORMATION**, um anstehende Aktualisierungen anzuzeigen, nicht verfügbare Daten festzulegen und Aktualisierungen zu genehmigen. Weitere Informationen zu Benachrichtigungen und zum Planen anstehender Aktualisierungen finden Sie im Abschnitt zum <a href="../admin/index.html#oc_system">Anzeigen von Systeminformationen</a>. </dd>

<dt>**Sonstige**</dt>
<dd>IBM beabsichtigt, alle Wartungstätigkeiten, die Ihre Services beeinträchtigen, insbesondere die Verfügbarkeit Ihrer Bluemix Local-Umgebung, -Laufzeiten und -Services auf die monatlichen und Standardaktualisierungen zu beschränken.
In Ausnahmefällen können andere Änderungsfenster für die Verwaltung der Umgebung verwendet werden. IBM
wird sich in angemessenem Maße bemühen, die Auswirkungen auf Sie während solcher Änderungsfenster zu minimieren
und Sie im Voraus benachrichtigen. </dd>
</dl>

Arbeiten Sie mit Ihrem von IBM zugewiesenen Kundenbeauftragten zusammen, um die Wartung Ihrer lokalen
Instanz festzulegen und sich auf ein Fenster für die Standardwartung zu einigen. 
   
