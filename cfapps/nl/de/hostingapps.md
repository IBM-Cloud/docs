---

 

copyright:

  years: 2015，20166

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Apps in {{site.data.keyword.Bluemix_notm}} hosten

*Letzte Aktualisierung: 9. Mai 2016*

<!--The whole topic is staging only -->

In {{site.data.keyword.Bluemix}} können Sie Anwendungen erstellen sowie vorhandene Anwendungen hosten. Sie können Ihre Anwendungen nach {{site.data.keyword.Bluemix_notm}} migrieren, sofern diese für die Cloud geeignet sind. Von {{site.data.keyword.Bluemix_notm}} werden unterschiedliche Methoden zum Ausführen von Anwendungen bereitgestellt, z. B. Cloud Foundry, IBM Containers und virtuelle Maschinen.

##Anwendungen für die Cloud vorbereiten
{: #cloud-readyapps}

Beim Entwickeln und Erstellen einer Cloud-fähigen Anwendung werden die Prinzipien einer Cloudplattform berücksichtigt. Von einer Cloud-fähigen Anwendung können die Funktionen verwendet werden, die von der Cloudplattform bereitgestellt werden.

Wenn alle der folgenden Prinzipien in einer Anwendung beachtet werden, ist die Anwendung Cloud-fähig und kann nach {{site.data.keyword.Bluemix_notm}} migriert werden. Wenn in der Anwendung gegen ein Prinzip verstoßen wird, können Sie die Anwendung in der Regel so ändern, dass sie den Prinzipien entspricht.

* Codieren Sie die Anwendung nicht direkt für eine bestimmte Topologie.

  In einer Umgebung ohne Cloud kann von der Anwendung eine bestimmte Bereitstellungstopologie verwendet werden. Die Anwendungstopologie kann sich in Cloudanwendungen jedoch ändern, weil Cloud-fähige Anwendungen und Services sofortige Änderungen der Skalierbarkeit zulassen. Die Änderungen der Skalierbarkeit umfassen dynamisches Skalieren und eine manuelle Größenänderung der Instanzenanzahl einer Anwendung.

  Erstellen Sie Ihre Anwendung so generisch und statusunabhängig wie möglich, um zu verhindern, dass die Anwendung durch Änderungen der Skalierbarkeit beeinträchtigt wird.

* Gehen Sie nicht davon aus, dass das lokale Dateisystem ein permanentes System ist.

  Eine Anwendungsinstanz kann in der Cloud jederzeit verschoben, gelöscht oder kopiert werden; verlassen Sie sich deswegen nicht auf die Dateien, die in das Dateisystem geschrieben werden. Wenn eine Anwendung das lokale Dateisystem als Cache für häufig verwendete Informationen (einschließlich Anwendungsprotokolle) verwendet, gehen diese Informationen verloren, wenn die Instanz beendet wird und an einer anderen Position oder auf einer anderen virtuellen Maschine erneut gestartet wird.

  Sie können Informationen anstatt im lokalen Dateisystem in einem Service speichern, z. B. in einer SQL- oder NoSQL-Datenbank. In einer dynamischen Cloudumgebung ist es darüber hinaus wichtig, dass die Protokolle durch einen Service bereitgestellt werden, der länger verfügbar ist als die Anwendungsinstanzen, für die die Protokolle erstellt werden.

* Speichern Sie den Sitzungsstatus nicht in der Anwendung.

  Der Status Ihres Systems wird durch die Datenbanken und den gemeinsam genutzter Speicher definiert und nicht durch jede einzelne aktive Anwendungsinstanz. Statusangaben jeder Art schränken die Skalierbarkeit einer Anwendung ein. Versuchen Sie, die Auswirkung des Sitzungsstatus dadurch zu minimieren, dass er an einer zentralen Position auf dem Server gespeichert wird.

  Wenn Sie den Sitzungsstatus nicht vollständig ignorieren können, verlagern Sie ihn in einen Speicher mit hoher Verfügbarkeit, der sich außerhalb des Anwendungsservers befindet. Solche Speicher sind zum Beispiel IBM WebSphere Extreme Scale, Redis, Memcached oder eine externe Datenbank.

* Geben Sie keine konkreten Infrastrukturabhängigkeiten an.

  Hierbei handelt es sich um ein generelles Prinzip, das sich mehrfach auswirkt. Gehen Sie zum Beispiel nicht davon aus, dass den Services, die von der Anwendung verwendet werden, bestimmte Hostnamen oder IP-Adressen zugeordnet sind. Da die Services in der Cloudumgebung verlagert oder neu generiert werden können, können sich auch die Hostnamen und IP-Adressen ändern.

  Das Extrahieren von umgebungsspezifischen Abhängigkeiten in eine Reihe von Eigenschaftendateien ist zwar eine Verbesserung, aber trotzdem unzulänglich. Ein bewährtes Verfahren ist das Verwenden einer externen Service-Registry zum Auflösen von Serviceendpunkten oder das Delegieren der gesamten Routingfunktion an einen Service-Bus oder eine Lastausgleichsfunktion mit einem virtuellen Namen.

* Verwenden Sie in der Anwendung keine Infrastruktur-APIs.

  Wenn Sie in der Anwendung eine bestimmte Infrastruktur-API benötigen, ist eine Änderung der Infrastruktur eine Herausforderung, weil von einer Infrastruktur-API auf viele verschiedene Schichten im Software-Stack verwiesen werden kann.

  Sie können stattdessen auf vorhandene Open Source-Produkte oder kostenpflichtige Produkte zurückgreifen und PaaS-Lösungen (PaaS - Platform as a Service) in der PaaS-Schicht belassen, damit sie nicht zu einem Bestandteil Ihres Anwendungscodes werden.

* Verwenden Sie nicht eingeschränkt lesbare Protokolle.

  Verwenden Sie nicht eingeschränkt lesbare Protokolle, für die eine zusätzliche Konfiguration erforderlich ist, damit sie dauerhaft verfügbar sind.

  Anwendungen, die auf Standardprotokollen basieren, sind ausfallsicherer, wenn die Konfigurationselemente an die Plattform delegiert werden. Zu den Standardprotokollen gehören HTTP, SSL, Standarddatenbanken, Warteschlangensteuerung und Web-Service-Verbindungen.

* Verlassen Sie sich nicht auf betriebssystemspezifische Funktionen.

  Wenn Sie bereits betriebssystemspezifische Funktionen verwendet haben, können Sie dieses Problem mithilfe von Kompatibilitätsbibliotheken, z. B. Cygwin oder Mono, beheben. Cygwin ist eine Kompatibilitätsbibliothek, von der eine Reihe von Linux-Tools in einer Windows-Umgebung bereitgestellt werden. Mono ist eine Kompatibilitätsbibliothek, von der Windows .NET-Funktionen in Linux bereitgestellt werden.

  Vermeiden Sie betriebssystemspezifische Abhängigkeiten; verwenden Sie stattdessen Services, die von der Middlewareinfrastruktur oder von Service-Providern bereitgestellt werden.

* Installieren Sie die Anwendung nicht manuell.

  Es kann vorkommen, dass die Anwendung in der dynamischen Cloudumgebung häufig bedarfsgesteuert installiert wird. Der Installationsprozess muss scriptgesteuert und zuverlässig sein, die Konfigurationsdaten müssen aus den Scripts externalisiert werden.

  Erfassen Sie die Anwendungsinstallation mindestens als einheitlichen Satz aus Scripts, die vom Betriebssystem unabhängig sind. Halten Sie die Anwendungsinstallation klein und portierbar, damit sie an abweichende Automatisierungsverfahren angepasst werden kann. Minimieren Sie auch die Abhängigkeiten, die für die Anwendungsinstallation erforderlich sind.

Weitere Informationen zu Cloud-fähigen Anwendungen finden Sie unter [The Twelve-Factor App](http://12factor.net/){:new_window}.

##Apps migrieren
{: #ht_hostapp}

Sie können Ihre Anwendungen schrittweise nach {{site.data.keyword.Bluemix_notm}} migrieren, anstatt eine Anwendung vollständig in die Cloudumgebung zu verschieben. Sie können zuerst einen Teil der Anwendung migrieren und danach mit dem Service 'Cloud Integration' eine Verbindung zu vorhandenen Daten oder einem System of Record herstellen.

Es kann erforderlich sein, in den Cloudanwendungen auf die Back-End-Daten oder -Services zuzugreifen, zum Beispiel auf ein System of Record (SOR, Kerndatensystem). In {{site.data.keyword.Bluemix_notm}} können Sie den Service 'Secure Gateway' zum Herstellen eines sicheren Tunnels zwischen einer {{site.data.keyword.Bluemix_notm}}-Organisation und dem Back-End-Netz des Unternehmens verwenden. Mithilfe des Service können die Anwendungen in {{site.data.keyword.Bluemix_notm}} auf die Daten und Services des Back-End-Netzes zugreifen. Details hierzu finden Sie unter [Reaching enterprise backend with Bluemix Secure Gateway via console](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}.

Wenn Sie eine Anwendung in {{site.data.keyword.Bluemix_notm}} als Cloud Foundry-Anwendung bereitstellen möchten, wählen Sie eine Laufzeit aus dem {{site.data.keyword.Bluemix_notm}}-Katalog aus. Bestandteil der Laufzeit ist die Startanwendung Hello World, die Sie durch eine eigene Anwendung ersetzen können. Wenn Sie keine Startanwendung finden, von der die gewünschte Laufzeit bereitgestellt wird, können Sie ein angepasstes Cloud Foundry-kompatibles Buildpack zu {{site.data.keyword.Bluemix_notm}} hinzufügen; verwenden Sie hierzu den Befehl 'cf push' mit der Option '-b'. Details hierzu finden Sie unter [Community-Buildpacks verwenden](../cfapps/byob.html).

Sie können die folgenden Tools und Services verwenden, die von {{site.data.keyword.Bluemix_notm}} bereitgestellt werden:

*Tabelle 1. {{site.data.keyword.Bluemix_notm}}-Tools*

| Tool	| Methode |
|:------|:--------|
|Cloud Foundry-Befehlszeilenschnittstelle (Befehlszeilenschnittstelle 'cf')	|Verwalten Sie den Code auf einem lokalen Client und verwenden Sie die Cloud Foundry-Befehlszeilenschnittstelle, um Ihre Anwendung mit einer Push-Operation manuell zu {{site.data.keyword.Bluemix_notm}} zu übertragen. Weitere Informationen finden Sie unter [Apps hochladen](../starters/upload_app.html).|
|Eclipse	|Verwalten Sie den Code in Eclipse und verwenden Sie IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, um Ihre Anwendung mit einer Push-Operation zu übertragen.|
|Git-Integration	|Verwalten Sie den Code mit GitHub und integrieren Sie Git in {{site.data.keyword.Bluemix_notm}}. Sie können mit anderen Entwicklern zusammenarbeiten. Die Anwendung wird automatisch in {{site.data.keyword.Bluemix_notm}} bereitgestellt, wenn Sie Änderungen am Code festschreiben. Sie müssen die Anwendung nicht manuell mit einer Push-Operation übertragen.|
|{{site.data.keyword.Bluemix_notm}} DevOps Delivery Pipeline	|Verwalten Sie den Code mithilfe eines DevOps GitHub-Repositorys und stellen Sie die Anwendung in {{site.data.keyword.Bluemix_notm}} unter Verwendung von DevOps Delivery Pipeline bereit.|


Wenn die Cloud Foundry-Plattform nicht die Anforderungen der Anwendung erfüllt, können Sie einen Container oder eine virtuelle Maschine verwenden, für den bzw. die eine Laufzeit mit entsprechend angepassten Optionen konfiguriert ist und verwaltet wird.

##Apps mithilfe der Befehlszeilenschnittstelle 'cf' hochladen
{: #ht_cfcli}

Sie können Code auf einem lokalen Client verwalten und die Anwendung manuell mithilfe der Cloud Foundry-Befehlszeilenschnittstelle in {{site.data.keyword.Bluemix_notm}} hochladen. Wenn Sie den Code ändern, müssen Sie die Anwendung erneut mit einer Push-Operation zu {{site.data.keyword.Bluemix_notm}} übertragen, um den aktualisierten Code auszuführen.

Führen Sie die folgenden Schritte aus, um die Anwendung zu migrieren:

<ol>
<li>Installieren Sie die Cloud Foundry-Befehlszeilenschnittstelle. Stellen Sie sicher, dass Sie die neueste Version der Befehlszeilenschnittstelle 'cf' verwenden.
<ol>
<li>Laden Sie das Installationsprogramm für Ihr Betriebssystem herunter.</li>
<li>Befolgen Sie die Anweisungen im Assistenten des Tools, um die Befehlszeile zu installieren.</li>
<li>Verwenden Sie den folgenden Befehl, um die Version der Befehlszeilenschnittstelle 'cf' zu überprüfen:
<pre>cf -v</pre></li>
</ol>
</li>

<li>Optional: Wenn Sie die Bereitstellungsdetails angeben und speichern möchten, bevor Sie eine Anwendung mit einer Push-Operation an {{site.data.keyword.Bluemix_notm}} übertragen, können Sie das Anwendungsmanifest mithilfe der folgenden Schritte hinzufügen:
<ol>
<li>Wechseln Sie in das Arbeitsverzeichnis der Anwendung und erstellen Sie eine Datei mit dem Namen 'manifest.yml' (der Standardname).</li>
<li>Geben Sie Bereitstellungsdetails in der Manifestdatei an. Im folgenden Beispiel wird eine Manifestdatei für eine Java™-Anwendung dargestellt.
<pre class="pre codeblock"><code>applications:
- disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M</code></pre>
<p>Weitere Informationen zu den unterstützten Optionen, die Sie in dieser Datei verwenden können, finden Sie unter
[Anwendungsmanifest](../manageapps/depapps.html#appmanifest).

</p></li></ol>
</li>

<li>Übertragen Sie die Anwendung mit einer Push-Operation. Sie können die Anwendung mit dem Befehl 'cf push' hochladen.
<ol>
<li>Stellen Sie eine Verbindung zu {{site.data.keyword.Bluemix_notm}} her und melden Sie sich mit dem folgenden Befehl an. Wählen Sie Ihre Organisation und Ihren Bereich aus, wenn Sie dazu aufgefordert werden.
<pre>cf login -a https://api.ng.bluemix.net</pre></li>
<li>Geben Sie über Ihr Anwendungsverzeichnis den Befehl 'cf push' mit dem Anwendungsnamen ein. Der Anwendungsname muss in der
{{site.data.keyword.Bluemix_notm}}-Umgebung eindeutig sein.
<pre>cf push App-Name</pre></li>
<li>Optional: Wenn Sie ein externes Buildpack verwenden, müssen Sie die Option '-b' mit dem Befehl 'cf push' verwenden. Beispiel:
<pre>cf push App-Name -b Buildpack-URL</pre>
<p>Details hierzu finden Sie unter 'Community-Buildpacks verwenden'.</p>
</li></ol>
</li>

<li>Optional: Wenn Sie Ihre Anwendung ändern, müssen Sie diese Änderungen hochladen, indem Sie den Befehl 'cf push' erneut eingeben. Die Befehlszeilenschnittstelle 'cf' verwendet Ihre vorherigen Optionen und Ihre Antworten auf die Eingabeaufforderungen, um alle aktiven Instanzen Ihrer Anwendung mit den neuen Code-Bits zu aktualisieren.</li>
</ol>

**Hinweise:**

* Wenn Sie den Befehl 'cf push' verwenden, kopiert die Befehlszeilenschnittstelle 'cf' alle Dateien und Verzeichnisse aus Ihrem aktuellen Verzeichnis in {{site.data.keyword.Bluemix_notm}}. Stellen Sie sicher, dass sich in Ihrem Anwendungsverzeichnis nur die erforderlichen Dateien befinden.
* Stellen Sie sicher, dass von Ihrer Organisation ausreichend Speicherplatz für alle Instanzen der Anwendung bereitgestellt wird. Das Speicherkontingent für Ihre Organisation können Sie mit 'cf org Organisationsname' anzeigen.
* Weitere Informationen zum Befehl 'cf push' finden Sie unter ['cf'-Befehle](../cli/reference/cfcommands/index.html).

##Daten migrieren und Services verwenden
{: #ht_service}

Nach dem Upload Ihrer Anwendung in {{site.data.keyword.Bluemix_notm}} wählen Sie den Service, mit dem die Anwendung verbunden ist, im
{{site.data.keyword.Bluemix_notm}}-Katalog aus, erstellen Sie eine Serviceinstanz, binden Sie die Instanz an die Anwendung und starten Sie dann die Anwendung erneut.

Bei der Umgebungsvariablen VCAP_SERVICES Ihrer Anwendung handelt es sich um ein JSON-Objekt mit
Informationen zur Interaktion mit einer Serviceinstanz in {{site.data.keyword.Bluemix_notm}}. Die Informationen umfassen den Namen der Serviceinstanz, die Berechtigungsnachweise und die URL für die Verbindung zu der Serviceinstanz.

Wenn Sie den Code in {{site.data.keyword.Bluemix_notm}} ausführen möchten, müssen Sie die Codelogik zum Analysieren der Variablen VCAP_SERVICES hinzufügen, damit Sie Informationen zur Serviceverbindung erhalten. Ändern Sie die Anwendung, um den dynamisch zugewiesenen Host und Port der Serviceinstanz über die Umgebungsvariable abzurufen. Am folgenden Beispiel wird veranschaulicht, wie die Berechtigungsnachweise der PostgreSQL-Serviceinstanz in einer Ruby-Anwendung abgerufen werden:

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)
        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```		
{:codeblock}

Wenn Sie sicherstellen möchten, dass die Anwendung nach ihrer Änderung für {{site.data.keyword.Bluemix_notm}} in der lokalen Umgebung ausgeführt werden kann, überprüfen Sie, ob die Variable VCAP_SERVICES vorhanden ist, die für alle {{site.data.keyword.Bluemix_notm}} Cloud Foundry-Anwendungen festgelegt wird.


# Zugehörige Links
{: #rellinks}

## Zugehörige Links
{: #general}

* [IBM Containers](../containers/container_cli_ov.html)
* [Virtual Machines](../virtualmachines/vm_index.html)
* [Einführung in Delivery Pipeline](../services/DeliveryPipeline/index.html)
* [Apps mit IBM Eclipse Tools for Bluemix bereitstellen](../manageapps/eclipsetools/eclipsetools.html)
* [The Twelve-Factor App](http://12factor.net/){:new_window}
* [Reaching enterprise backend with Bluemix Secure Gateway via console](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}
