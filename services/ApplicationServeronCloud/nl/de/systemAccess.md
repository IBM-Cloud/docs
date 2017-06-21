---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Systemzugriff
{: #system_access}


In diesen Abschnitten werden verschiedene Methoden der Erstellung und Verwaltung einer Serviceinstanz sowie verschiedene Möglichkeiten des Zugriffs und der Einrichtung des Zugriffs auf Ihre Systeme beschrieben.
{: shortdesc}


## REST-API-Nutzung in WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}
{: #restapi_usage}

In WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} werden Instanzen auf eine der folgenden Weisen erstellt, bereitgestellt, verwaltet und gelöscht: 

* Über das {{site.data.keyword.Bluemix_notm}}-Katalog- und -Service-Dashboard in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle.
* Durch die Erstellung einer Anwendung oder eines Scripts, die bzw. das die REST-konformen APIs nutzt.

Durch die Verwendung der mit Swagger 2.0 kompatiblen REST-APIs können Clients auf dieselben Funktionen zugreifen, die auch über das Portal und das Dashboard verfügbar sind. Weitere Informationen zu den unterstützten REST-APIs und Ressourcen finden Sie in der [REST-API-Dokumentation](https://wasaas-broker.ng.bluemix.net/wasaas-broker/api#/){: new_window} von WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}. Für Beispielcode, der die Verwendung der REST-APIs darstellt, laden Sie die mittels Git gehosteten [REST-API-Beispiele](https://github.com/IBM-Bluemix/WebSphere-for-Bluemix-API-Usage){: new_window} für WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} herunter.

**Hinweis:** Abhängig von der erstellten T-Shirt-Größe ist der Service nach der Erstellung einer Serviceinstanz möglicherweise nicht sofort einsatzbereit. Es wird empfohlen, das Feld **Status** der zurückgegebenen JSON-Daten abzufragen, um den aktuellen Status der Serviceinstanz festzustellen.

**Anmerkung:** Die in den [REST-API-Beispielen](https://github.com/IBM-Bluemix/WebSphere-for-Bluemix-API-Usage){: new_window} referenzierte **apiEndpoint**-URL zeigt auf die Region 'USA - Süden'. Bei der Arbeit mit anderen Regionen müssen Sie sicherstellen, dass Ihre Anwendung die enstprechende **apiEndpoint**-URL referenziert.

*Tabelle 1. API-Endpunkt-URLs für Implementierung der REST-API*

| **Regionsname** | **Geografischer Standort** | **Regionspräfix** | **API-Endpunkt-URL** |       
|:-------------:|:----------:|:--------------:|:-------------:|
| USA - Süden | Dallas, TX, US | ng | https://wasaas-broker.ng.bluemix.net/wasaas-broker/api  |
| Vereinigtes Königreich | London, England | eu-gb | https://wasaas-broker.eu-gb.bluemix.net/wasaas-broker/api  |
| Sydney | Sydney, Australien | au-syd | https://wasaas-broker.au-syd.bluemix.net/wasaas-broker/api  |
| Frankfurt | Frankfurt, Deutschland | eu-de | https://wasaas-broker.eu-de.bluemix.net/wasaas-broker/api  |



## Service-Dashboard
{: #service_dashboard}

Nach der Erstellung der Serviceinstanz werden Sie zum Service-Dashboard weitergeleitet. Sie können jederzeit zum Service-Dashboard zurückkehren, indem Sie im Dashboard Ihrer Organisation auf das Servicesymbol klicken.
Über das Service-Dashboard haben Sie Zugriff auf Folgendes:

* Einen Link zu dieser Dokumentation.
* Einen Link zum Herunterladen der erforderlichen OpenVPN-Konfigurationsdateien.
* Die Möglichkeit, die virtuelle Maschine zu starten und zu stoppen. Die VM ist ursprünglich gestartet.
* Den Hostnamen.
* Den Namen des Benutzers mit Administratorberechtigungen und das Administratorkennwort.
* Einen privaten SSH-Schlüssel.
* Den Namen des Benutzers mit Administratorberechtigungen und das Administratorkennwort für WebSphere®.
* Die URLs für Admin Center und Admin Console.

**Hinweis**: Aufgrund einer bestimmten Menge an Rechen-, Speicher- und E/A-Ressourcen werden für Clients Gebühren für die Summe der virtuellen Maschinen im Status GESTOPPT mit einer reduzierten Rate von 5 % berechnet. Clients werden mit einer festen Anzahl von Instanzen im Status GESTOPPT mit maximal 10 IP-Adressen oder 64 GB Speicherplatz verwaltet. 


## OpenVPN für WebSphere Application Server in Bluemix-Instanzen einrichten
{: #setup_openvpn}

Für den Zugriff auf virtuelle Maschinen in WebSphere Application Server in Bluemix ist OpenVPN erforderlich. Die Installation und Ausführung muss mit Administratorberechtigungen erfolgen.

### Befolgen Sie die folgenden Anweisungen zur Einrichtung von OpenVPN in Windows:

1. Laden Sie über den Link für den [openVPN-Windows-Download](http://swupdate.openvpn.org/community/releases/) Folgendes herunter:
  * [openvpn-install-2.3.4-I001-x86_64.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-x86_64.exe){: new_window} für 64-Bit oder
  * [openvpn-install-2.3.4-I001-i686.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-i686.exe){: new_window} für 32-Bit.
2. Stellen Sie sicher, dass Sie die [Ausführung als Windows-Administrator](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} durchführen und openVPN installiert ist.
3. Laden Sie die VPN-Konfigurationsdateien über den OpenVPN-Download-Link der WebSphere Application Server in Bluemix-Instanz im Service-Dashboard herunter. Extrahieren Sie alle vier Dateien aus der komprimierten Datei in das Verzeichnis **{OpenVPN-Ausgangsverzeichnis}\config**. Beispiel:

  <pre>  
    C:\Program Files\OpenVPN\Config
  </pre>
  {: codeblock}

4. Starten Sie das OpenVPN-Clientprogramm "OpenVPN GUI". Stellen Sie sicher, dass Sie zum Starten des Programms die Option zum [Ausführen als Windows-Administrator](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} ausgewählt haben. Ansonsten kann möglicherweise keine Verbindung hergestellt werden.

### Befolgen Sie die folgenden Anweisungen zur Einrichtung von OpenVPN in Linux:
1. Befolgen Sie für die Installation von OpenVPN die[Anweisungen](https://openvpn.net/index.php/access-server/docs/admin-guides/182-how-to-connect-to-access-server-with-linux-clients.html){: new_window}.
  * Wenn Sie RPM Package Manager manuell herunterladen und installieren müssen, wechseln Sie zum Abschnitt zum [Herunterladen von OpenVPN für UNIX/Linux](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){: new_window}. Hierbei benötigen Sie möglicherweise Unterstützung von Ihrem Linux-Administrator.
3. Laden Sie die VPN-Konfigurationsdateien über den OpenVPN-Download-Link der WebSphere Application Server in Bluemix-Instanz im Service-Dashboard herunter. Extrahieren Sie die Dateien in das Verzeichnis, in dem Sie den OpenVPN-Client starten möchten. Alle vier Dateien müssen sich im selben Verzeichnis befinden.
3. Starten Sie das OpenVPN-Clientprogramm. Öffnen Sie ein Terminalfenster und wechseln Sie in das Verzeichnis, in dem sich die Konfigurationsdateien befinden. Führen Sie den folgenden Befehl als Root aus:

  <pre>
      $ openvpn --config vt-wasaas-wasaas.ovpn
  </pre>
  {: codeblock}  

### Befolgen Sie die folgenden Anweisungen zur Konfiguration von OpenVPN in Mac:
1. Eine Möglichkeit besteht darin, [Tunnelblick](https://tunnelblick.net/){: new_window} (ein Open-Source-Softwareprodukt) zu installieren.
2. Extrahieren Sie die VPN-Konfigurationsdateien über den WebSphere-Service. In Tunnelblick werden Sie dazu aufgefordert, Ihr Administratorkennwort für Mac einzugeben; die Konfiguration wird der Gruppe von VPNs, die Sie zum Herstellen einer Verbindung verwenden können, hinzugefügt.
3. Stellen Sie eine Verbindung zum VPN-Netz her und greifen Sie anschließend auf die virtuelle Maschine zu. Nach dem ersten Zugreifen wird die Konfiguration in [Tunnelblick](https://tunnelblick.net/){: new_window} im Cache gespeichert und Sie können eine Verbindung über Tunnelblick herstellen. Für einen einfachen Zugriff können Sie in der oberen Menüleiste ein entsprechendes Symbol einfügen.


## Mithilfe von SSH auf VMs in WebSphere Application Server in Bluemix zugreifen
{: #using_ssh}

In diesen Anweisungen wird vorausgesetzt, dass Sie OpenSSH als Client verwenden. OpenSSH ist in der Regel unter Linux oder unter Windows in Cygwin verfügbar. Es kann auch so installiert werden, dass es in der Windows-Eingabeaufforderung ausgeführt werden kann.

Geben Sie den folgenden Befehl ein, um die Installation von OpenSSH zu prüfen:
  ```
      $ ssh -V
  ```
  {: codeblock}

Die folgende Nachricht ist ein Beispiel für die Antwort:
  ```
      OpenSSH_6.6p1, OpenSSL 1.0.1g 7 Apr 2014
  ```
  {: codeblock}

Befolgen Sie die folgenden Anweisungen zur Einrichtung von SSH-Zugriff auf Ihre WebSphere Application Server in Bluemix-VMs:

1. Lesen Sie die Warnung, die angezeigt wird, wenn Sie das erste Mal eine Verbindung herstellen: "The authenticity of host x.x.x.x cannot be established." Diese Nachricht ist normal. Wählen Sie bei der entsprechenden Eingabeaufforderung 'yes' aus. Der öffentliche Schlüssel wurde für den Benutzer 'virtuser' nun auf Ihrer VM installiert.
2. Melden Sie sich mithilfe des privaten Schlüssels als 'virtuser' an. Die besten Ergebnisse erzielen Sie mit dieser Authentifizierungsmethode.
3. Kopieren Sie den Inhalt des privaten Schlüssels in eine Datei.
4. Führen Sie den folgenden Befehl aus:

  <pre>
    $ ssh virtuser@169.53.246.xxx -i /path/privateKeyFileName
  </pre>
  {: codeblock}

5. Für eine vollständige Berechtigung des Tys 'sysadmin' müssen Sie mithilfe des folgenden Befehls den 'virtuser' nach 'root' wechseln:

  <pre>
    $ sudo su root
  </pre>
  {: codeblock}

6. Für den Fall, dass beim Zugreifen auf das System mit dem privaten SSH-Schlüssel Probleme auftreten, wird das Rootkennwort bereitgestellt. Melden Sie sich mithilfe des folgenden Befehls als Root an und geben Sie das Kennwort an.

 <pre>
    $ ssh root@169.53.246.x
  </pre>
  {: codeblock}

7. Unabhängig davon, ob Sie mit dem privaten SSH-Schlüssel oder dem Rootkennwort auf das System zugreifen, sollten Sie das Rootkennwort unverzüglich ändern.
8. Sie können Ihre SSH-Befehle vereinfachen, indem Sie im Verzeichnis %HOME%\.ssh eine Datei mit dem Namen "config" erstellen. Beispiel:

  <pre>
   Host VM1
      Hostname 169.53.246.xxx
      User virtuser
      IdentityFile /path/privateKeyFileName
  </pre>
  {: codeblock}

9. Führen Sie "ssh VM1" aus, um als Benutzer virtuser eine Verbindung herzustellen.

## Systempfade
{: #system_paths}

* Die Liberty Profile-Befehle können über */opt/IBM/WebSphere/Liberty/bin* abgesetzt werden.
* Die Position des Liberty Profile-Serverprofils ist */opt/IBM/WebSphere/Profiles/Liberty/servers/server1*.
* Die klassischen WebSphere Application Server-Befehle können über */opt/IBM/WebSphere/AppServer/bin* abgesetzt werden.
* Die klassische WebSphere Application Server-Profilposition für den Server ist */opt/IBM/WebSphere/Profiles/DefaultAppSrv01/servers/server1*.

## Links zu Admin Center und Admin Console verwenden
{: #console_links}

Wenn Sie auf den Link zu Admin Center oder Admin Console klicken, wird möglicherweise eine Warnung zu einer nicht vertrauenswürdigen Verbindung angezeigt. Der Wortlaut der Nachricht kann je nach Browser unterschiedlich sein. Das gilt auch für die Schritte zum Umgehen oder Beheben der Warnung.

Da Sie die von {{site.data.keyword.IBM}} bereitgestellten Links verwenden, können Sie diese Meldung ohne Bedenken ignorieren und eine Verbindung herstellen. Wenn in Ihrem Browser angeboten wird, eine Sicherheitsausnahme zu speichern, können Sie damit am einfachsten verhindern, dass diese Warnung künftig erneut angezeigt wird.

Sie können das eingehende Unterzeichnerzertifikat auch exportieren und anschließend als Trusted-Root-Zertifikat in Ihren Browser importieren. Für diese Option müssen Sie in der Datei *hosts*, in der die IP-Adresse der VM dem allgemeinen Namen des Zertifikatsausstellers zugeordnet ist, einen entsprechenden Eintrag vornehmen. Dieser Name hat das folgende Format: wl<pureapplication.ibmcloud.com. Wenn Sie in der URL nun den Hostnamen anstelle der IP-Adresse verwenden, können Sie eine saubere Verbindung herstellen. Anschließend müssen Sie über den Hostnamen statt über die IP-Adresse in der URL auf das Admin Center oder die Administrationskonsole zugreifen.

Kunden installieren häufig eigene Stammzertifikate für Anwendungen, die sie externalisieren. Weitere Informationen finden Sie im IBM Knowledge Center von [WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/tsec_securecomm.html?cp=SSEQTP_8.5.5%2F1-11-2-6&lang=en){: new_window} oder von [Liberty Core](http://www.ibm.com/support/knowledgecenter/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_comm.html?lang=en){: new_window}.

## Firewall-Ports
{: #firewall_ports}

Möglicherweise ist es erforderlich, an der Firewall Ports zu öffnen, um den Zugriff auf Anwendungen und Datenbanken zuzulassen.
  * Auf jedem Knoten von WebSphere Application Server in Bluemix finden Sie im Verzeichnis WAS_HOME/virtual/bin das Script openFirewallPorts.sh.
  * Auf jedem Host eines Liberty-Verbunds finden Sie im Verzeichnis WAS_HOME/virtual/bin das Script openFirewallPorts.sh.

Syntax:
  ```
      $ openFirewallPorts.sh -ports <PORT>:<PROTOCOL>,... -persist true|false
  ```
  {: codeblock}

* PORT ist eine Portnummer.
* PROTOCOL ist entweder TCP oder UDP.
* -persist ist entweder auf 'true' oder 'false' eingestellt.

Wenn Sie mehrere Ports angeben möchten, müssen Sie diese mit einem Komma (,) voneinander trennen.

**Anmerkung**: 'sport' und 'dport' des Ports werden in den Abschnitten INPUT und OUTPUT der Firewall geöffnet. Dieses Script muss mithilfe von 'sudo' als Root ausgeführt werden. Sie können auch IP-Tabellen (iptables) direkt ändern.

## Web-Server konfigurieren
{: #configure_webserver}

Bei der Bereitstellung einer Zelle oder eines Verbunds erhalten Sie eine vorkonfigurierte Umgebung. Im Falle einer klassischen Network Deployment-Zelle erhalten Sie beispielsweise die folgende Umgebung:

* Einen Deployment Manager, der zu Entwicklungs- und Testzwecken mit IBM HTTP Server kollokiert wird.

* Einen in Deployment Manager integrierten angepassten Knoten.

* Der Deployment Manager, der IHS-Server und der Knotenagent befinden sich bei der Erstbereitstellung im Status 'Gestartet'.

Wenn der Web-Server alle Benutzeranforderungen verarbeiten soll, muss das Plug-in nach der Bereitstellung der Anwendung möglicherweise generiert und weitergegeben werden.

**Störungen vermeiden:** Stellen Sie sicher, dass die folgenden vorausgesetzten Tasks ausgeführt wurden, bevor Sie das Plug-in generieren und weitergeben:

* Stellen Sie in einer lokalen Windows-, Linux- oder MAC-Umgebung sicher, dass [openVPN](systemAccess.html#setup_openvpn) konfiguriert und gestartet ist und Sie mit der entsprechenden Region verbunden sind.

* Klicken Sie im Service-Dashboard von WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} auf **Administrationskonsole öffnen** und melden Sie sich mit 'wsadmin' und dem im Service-Dashboard angegebenen Administratorkennwort an.

* In der Administrationskonsole müssen Sie einen Anwendungsserver (z. B. ***server1***) erstellen, da ein leerer angepasster Knoten in den Deployment Manager integriert ist.

* Starten Sie den erstellten Server.

* Stellen Sie während der Anwendungsinstallation sicher, dass die Module der Anwendung dem gestarteten Server und dem Web-Server zugeordnet werden (z. B. ***webserver1***).

Bei den folgenden allgemeinen Schritten wird davon ausgegangen, dass die vorausgesetzten Tasks ausgeführt wurden:

1. Generieren Sie das Plug-in in der Administrationskonsole mithilfe der Option 'Umgebung':
   1. Wählen Sie 'Umgebung > Globale Webserver-Plug-in-Konfiguration aktualisieren' aus.
   2. Klicken Sie auf **OK** oder auf **Überschreiben**, um eine neue Plug-in-Konfigurationsdatei zu generieren.
2. Kopieren Sie das Plug-in im Deployment Manager in die Web-Server-Konfiguration:

  ```
   cp /opt/IBM/WebSphere/Profiles/DefaultDmgr01/config/cells/plugin-cfg.xml /opt/IBM/WebSphere/Plugins/config/webserver1/plugin-cfg.xml
  ```
  {: codeblock}
3. Bearbeiten Sie **httpd.conf** in **IHS_HOME/conf** (z. B. */opt/IBM/WebSphere/HTTPServer/conf*) und stellen Sie sicher, dass die folgenden beiden Zeilen vorhanden sind:

    ```
    LoadModule was_ap22_module /opt/IBM/WebSphere/Plugins/bin/64bits/mod_was_ap22_http.so
    WebSpherePluginConfig /opt/IBM/WebSphere/Plugins/config/webserver1/plugin-cfg.xml
    ```
    {: codeblock}  
4. Öffnen Sie die Ports mit den folgenden beiden Befehlen:

  ```
   export serverPorts=2810:TCP,2810:UDP,8880:TCP,8880:UDP,9101:TCP,9101:UDP,9061:TCP,9061:UDP,9080:TCP,9080:UDP,9354:TCP,9354:UDP,9044:TCP,9044:UDP,9443:TCP,9443:UDP,5060:TCP,5060:UDP,5061:TCP,5061:UDP,11005:TCP,11005:UDP,11007:TCP,11007:UDP,9633:TCP,9633:UDP,7276:TCP,7276:UDP,7286:TCP,7286:UDP,5558:TCP,5558:UDP,5578:TCP,5578:UDP

   sudo /opt/IBM/WebSphere/AppServer/virtual/bin/openFirewallPorts.sh -ports $serverPorts -persist true
  ```
    {: codeblock}
5. Stoppen und starten Sie den Web-Server mit den folgenden beiden Befehlen:
    ```
    sudo /opt/IBM/WebSphere/HTTPServer/bin/apachectl -k stop
    sudo /opt/IBM/WebSphere/HTTPServer/bin/apachectl -k start
    ```
    {: codeblock}
8. Greifen Sie über das Plug-in auf die Anwendung zu:
  ```
   http://169.53.246.xxx/contextRoot/
  ```
  {: codeblock}

**Anmerkung:** Die hier beschriebenen Schritte stellen nur eine Möglichkeit unter vielen zur Konfiguration eines Web-Servers dar. Weitere Unterstützung finden Sie im [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/search/configure%20web%20server?scope=SSAW57_9.0.0){: new_window}.

**Anmerkung:** Wenn Sie nicht auf die Anwendung zugreifen können, gibt es in der Firewall wahrscheinlich ein Portzugriffsproblem. Deshalb muss möglicherweise einer der folgenden Server erneut gestartet werden: Anwendungsserver, Knotenagent, Web-Server oder Deployment Manager. Darüber hinaus besteht die Möglichkeit, dass Sie auf das Service-Dashboard von WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} zugreifen und die einzelnen virtuellen Maschinen erneut starten müssen.

## SSL-Konfiguration
{: #ssl_configuration}

Der klassische WebSphere Application Server und Liberty Profile sind mit dem Protokoll [SSL_TLSv2](https://www.ibm.com/support/knowledgecenter/en/SSYKE2_8.0.0/com.ibm.java.security.component.80.doc/security-component/jsse2Docs/protocols.html){: new_window} konfiguriert. Modifizieren Sie zum Ändern des Protokolls die folgenden Dateien: 

Für den klassischen WebSphere Application Server:

1. Öffnen Sie **security.xml** in '/opt/IBM/WebSphere/Profiles/*profilname*/config/cell/*zellenname*' zur Bearbeitung und ändern Sie die folgende Zeile:

  ```
  sslProtocol="SSL_TLSv2"
  ```
{: codeblock}

2. Öffnen Sie **ssl.client.props** in '/opt/IBM/WebSphere/Profiles/*profilname*/properties' zur Bearbeitung und ändern Sie die folgende Zeile: 

  ```
  com.ibm.ssl.protocol=SSL_TLSv2
  ```
{: codeblock}

Für Liberty Profile:

1. Öffnen Sie **server.xml** in '/opt/IBM/WebSphere/Profiles/Liberty/servers/server1' zur Bearbeitung und ändern Sie die folgende Zeile im SSL-Konfigurationselement 'defaultSSLConfig':

  ```
  sslProtocol="SSL_TLSv2"
  ```
{: codeblock}
