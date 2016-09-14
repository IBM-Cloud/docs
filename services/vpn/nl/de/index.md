---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Einführung in {{site.data.keyword.vpn_short}}
{: #vpn}  
*Letzte Aktualisierung: 09. Mai 2016*

Mit dem Service {{site.data.keyword.vpn_full}} für Bluemix&reg; kann innerhalb der IBM Bluemix-Cloudumgebung sicher auf IBM Container (Docker-Container) zugegriffen werden. Sie können die IBM Bluemix-Cloudumgebung als Erweiterung des Rechenzentrums Ihres Unternehmens verwenden. Sie können mithilfe des Service IBM VPN außerdem eine Verbindung zu den SoftLayer-Servern herstellen.
{:shortdesc}

Stellen Sie bei der Vorbereitung sicher, dass Sie über einen IBM Docker-Container verfügen, der zur Verwendung bereit ist. In [IBM Containers for Bluemix](https://www.ng.bluemix.net/docs/containers/container_index.html) finden Sie Details zur Erstellung und Verwaltung von IBM Containers.  

Wählen Sie zu Beginn die Kachel für eine Instanz des Service **Virtual Private Network** im Bluemix-Dashboard aus. Führen Sie folgende Schritte aus:

1. Konfigurieren Sie das {{site.data.keyword.vpn_short}}-Gateway durch Auswählen von **Gateway erstellen**. Es wird ein Standardgateway erstellt. Bearbeiten Sie, falls erforderlich, die Gateway-Konfiguration wie in den folgenden Schritten gezeigt.  
{: #gateway}  

  1. Wählen Sie **Bearbeiten** aus.  
  2. Geben Sie den Gateway-Namen an.  
  3. Wählen Sie den Container und die Containergruppe aus, mit denen Sie den VPN-Service verwenden wollen.
	**Anmerkung:** Die privaten Teilnetze des Containers und der Containergtuppe werden vorab ausgewählt, damit Sie darauf über die VPN-Verbindung zugreifen können.
  4. Wählen Sie **SPEICHERN** aus.  

 Sie können die standardmäßigen IKE- und IPSec-Richtlinien verwenden oder angepasste Richtlinien konfigurieren. Wenn Sie die Standardrichtlinien verwenden wollen, springen Sie zu Schritt 4.

2. Konfigurieren Sie die IKE-Richtlinie, indem Sie die Registerkarte **IKE- und IPSec-Richtlinien** auswählen.
  1. Wählen Sie **Neues Element hinzufügen** aus.  
  2. Geben Sie folgende Details an:
	* **Name**: Name der IKE-Richtlinie
	* **Autorisierungsalgorithmus**: sha1; kann nicht geändert werden  
	* **Verschlüsselungsalgorithmus**: Treffen Sie eine Auswahl in der Dropdown-Liste. Werte: aes-128 (Standardwert), aes-192, aes-256, 3des
	* **Lebensdauer des Schlüssels**: Wert für Lebensdauer (in Sekunden) der IKE-Sicherheitszuordnung. Bereich: 60 bis 86400. Standardwert: 86400
	* **PFS**: Kennung für DH-Gruppe (DH - Diffie-Hellman). Werte: Gruppe 2, Gruppe 5, Gruppe 14. Standardwert: Gruppe 2
	* **Verhandlungsmodus**: Main; kann nicht geändert werden
	* **Version**: IKEV1; kann nicht geändert werden
  3. Wählen Sie **SPEICHERN** aus.

3. Konfigurieren Sie die IPSec-Richtlinie:
  1. Wählen Sie **Neues Element hinzufügen** aus.  
  2. Geben Sie folgende Details an:
  	* **Name**: Name der IPSec-Richtlinie  
  	* **Autorisierungsalgorithmus**: sha1; kann nicht geändert werden  
  	* **Verschlüsselungsalgorithmus**: Treffen Sie eine Auswahl in der Dropdown-Liste. Werte: aes-128 (Standardwert), aes-192, aes-256, 3des
  	* **Lebensdauer des Schlüssels**: Wert für Lebensdauer (in Sekunden) der Sicherheitszuordnung. Bereich: 60 bis 86400. Standardwert: 3600
  	* **PFS**: Kennung für DH-Gruppe (DH - Diffie-Hellman). Werte: Gruppe 2, Gruppe 5, Gruppe 14. Standardwert: Gruppe 2
  	* **Transformationsprotokoll**: ESP; kann nicht geändert werden
  	* **Kapselungsmodus**: Tunnel; kann nicht geändert werden
  3. Wählen Sie **SPEICHERN** aus.  

4. Geben Sie die Details für das Herstellen einer Verbindung zwischen dem VPN-Gateway Ihres Rechenzentrums oder des SoftLayer-Servers und dem IBM VPN-Gateway an.  
{: #site}  

  1. Wählen Sie die Registerkarte **Gateway Appliance** aus.
  2. Wählen Sie **Verbindung erstellen** im Abschnitt **Siteverbindungen** aus.
  3. Geben Sie folgende Siteverbindungsdetails an:  
  	* **Name**: Name der Verbindung  
  	* **Beschreibung**: Beschreibung der Verbindung (optional)  
  	* **Vorab bekannter gemeinsamer Schlüssel**: Vorab bekannter gemeinsamer (geheimer) Schlüssel zur Verwendung bei der Authentifizierung
  	* **Administratorstatus**: Status der VPN-Verbindung. Treffen Sie eine Auswahl in der Dropdown-Liste: UP (aktiv) oder DOWN (inaktiv). Standardwert: UP  
  	* **IP-Adresse des Kundengateways**: IP-Adresse des fernen Endpunkts des VPN-Tunnels.  
  	* **Kundenteilnetz**: Adresse des fernen Teilnetzes im CIDR-Format. Wählen Sie das Pluszeichen aus, um ein weiteres Teilnetz hinzuzufügen.
  4. (Optional) Konfigurieren Sie folgende Parameter für **Erweiterte Einstellungen**:  
  	* **IKE-Richtlinie**: Wählen Sie die IKE-Richtlinie aus.  
  	* **Keepalive-Intervall**: Keepalive-Intervall in Sekunden. Senden Sie im konfigurierten Intervall Keepalive-Nachrichten, um den Aktivitätszustands des Peers zu überprüfen. Standardwert: 15. Bereich: 5 bis 86399
  	* **Aktion bei inaktivem Peer**: Auszuführende Aktion, wenn erkannt wird, dass der Peer inaktiv ist.  
    	Werte: 
  		* hold (Standardwert): die Sicherheitszuordnung wird gehalten 
  		* clear: die Sicherheitszuordnung wird gelöscht
  		* disabled: die Sicherheitszuordnung ist inaktiviert
  		* restart: die Sicherheitszuordnung wird neu vereinbart
  		* restart-by-peer: alle Sicherheitszuordnungen mit dem inaktiven Peer werden neu vereinbart  
  	* **IPSec-Richtlinie**: Wählen Sie die IPSec-Richtlinie aus.
  	* **Zeitlimitwert für Keepalive**: Zeitlimitwert in Sekunden, nach dessen Ablauf die Sitzung beendet wird. Standardwert: 120. Bereich: 6 bis 86400. Der Zeitlimitwert für das Keepalive muss höher als der Wert für das Keepalive-Intervall sein.
  5. Wählen Sie **SPEICHERN** aus.

  **Hinweis:** Beim Einrichten der Verbindung wird der Verbindungsstatus als ***pending create*** (Erstellen anstehend) angezeigt. Wird dieser Status angezeigt, aktualisieren Sie die Anzeige einige Male, damit für die Verbindung der aktive Status angezeigt wird.

**Wichtig:** Bei Verwendung einer Webanwendung müssen Sie die Webanwendung an den von Ihnen verwendeten Docker-Container binden. Diese Bindung ist erforderlich, damit der Datenverkehr den IPSec-VPN-Tunnel durchlaufen kann.

**Wichtig:** Der Service IBM VPN wird aktuell im Modus des Antwortenden ausgeführt. Damit die VPN-Verbindung ausgeführt wird, muss ein Datenpaket vom IBM VPN-Gateway zu Ihrem lokalen Rechenzentrum oder Ihrem SoftLayer-Server fließen. Sobald die VPN-Verbindung eingerichtet ist, kann der Datenverkehr zwischen den Endpunkten der VPN-Verbindung in beiden Richtungen fließen.

 
# Zugehörige Links
## Beispiele 
{: #samples}  
* [Konfigurationsbeispiel für lokales strongSwan-Gateway](vpn_onpremises.html#strongswan){: new_window}
* [Konfigurationsbeispiel für lokales Vyatta-Gateway](vpn_onpremises.html#vyatta){: new_window}
* [Konfigurationsbeispiel für lokalen SoftLayer-Gateway Appliance Service (GaaS)](vpn_onpremises.html#gaas){: new_window}
* [Konfigurationsbeispiel für lokale Cisco ASA](vpn_onpremises.html#cisco){: new_window}

## API  
{: #api}  
* [IBM VPN-REST-konforme APIs](https://new-console.ng.bluemix.net/apidocs/101){: new_window}

## Allgemein  
{: #general}  
* [IBM VPN-Befehlszeilenschnittstelle](../../cli/plugins/vpn/index.html){: new_window}
* [IBM VPN - Häufig gestellte Fragen](vpn_faq.html#vpn_faq){: new_window}
* [IBM Bluemix - Preisliste](https://console.{DomainName}/pricing/){: new_window}
* [IBM Bluemix - Voraussetzungen](https://developer.ibm.com/bluemix/support/#prereqs)
