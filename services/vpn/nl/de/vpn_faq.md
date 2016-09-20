---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.vpn_short}} Häufig gestellte Fragen
{: #vpn_faq}
*Letzte Aktualisierung: 17. März 2016*

Im Folgenden finden Sie einige häufig gestellte Fragen.
{:shortdesc}

1. Welche Einheiten anderer Anbieter sind in IBM Labs für die Interoperabilität mit dem Service IBM VPN qualifiziert?

	IBM Lab hat folgende VPN-Gateway-Einheiten für den gemeinsamen Einsatz mit dem Service IBM VPN getestet:

	* Cisco Adaptive Security Appliance (ASA) Softwareversion 8.2(1). [Siehe Konfigurationsbeispiel.](vpn_onpremises.html#cisco) 
	* Brocade Vyatta 5415 vRouter 6.7 R7. [Siehe Konfigurationsbeispiel.](vpn_onpremises.html#vyatta){: new_window}
	* Linux StrongSwan U5.1.2/K3.13.0-55-generic. [Siehe Konfigurationsbeispiel.](vpn_onpremises.html#strongswan){: new_window}
	* Linux StrongSwan U5.2.2/K3.13.0-55-generic. [Siehe Konfigurationsbeispiel.](vpn_onpremises.html#strongswan){: new_window}

	Darüber hinaus wird erwartet, dass auf IPSec-Standards basierende VPN-Gateway-Einheiten anderer Anbieter zusammen mit dem Service IBM VPN verwendet werden können.

2. Wie schnell wird der Ausfall eines Peers erkannt?
 
	Der Ausfall eines Peers wird bei Erreichen des konfigurierten Zeitlimitwerts für das Keepalive-Intervall erkannt. Die Standardeinstellung ist 60 Sekunden.

3. Wie viele VPN-Gateways und Verbindungen kann ich pro VPN-Serviceinstanz erstellen?
 
	Sie können in einem Bluemix-Bereich pro VPN-Serviceinstanz eine VPN-Gateway-Einheit erstellen. Sie können pro VPN-Gateway bis zu 16 Verbindungen zu unterschiedlichen Zielen definieren. 

4. Wann sollte ich den Service IBM VPN statt des Bluemix-Service Secure Gateway verwenden?

	Beide Services werden zum Bereitstellen von sicheren Verbindungen zwischen Ihren Bluemix-Ressourcen und Ihrem lokalen Rechenzentrum verwendet. 

	Verwenden Sie den Service IBM VPN, wenn Sie nach einer Möglichkeit zum Sicherstellen der Verbindung zwischen zwei beliebigen Endpunkten suchen. Der Service VPN bildet eine sichere IPSec-Verbindung der Ebene 3 zwischen Ihren lokalen Netzen und der IBM Bluemix-Cloudumgebung. Mit dem Service IBM VPN kann nur auf IBM Container (Docker-Container) sicher zugegriffen werden. 

	Verwenden Sie den Bluemix-Service Secure Gateway, wenn Sie eine sichere Verbindung von einem bestimmten Endpunkt einer Anwendung in Bluemix zu einem anderen Endpunkt in Ihrem lokalen Rechenzentrum herstellen wollen. 

5. Kann ich mit dem Service IBM VPN auf meine Container und virtuellen Server innerhalb der IBM Bluemix-Cloudumgebung zugreifen, indem ich deren private IP-Adressen verwende?
 
	Aktuell kann mit dem Service IBM VPN nur auf Bluemix-Container zugegriffen werden.

6. Kann ich den Service IBM VPN auf der Ebene der Bluemix-Organisation definieren?

	Aktuell ist der Service IBM VPN nur auf der Ebene des Bluemix-Bereichs verfügbar. Wenn Ihre Bluemix-Organisation über mehrere Bereiche verfügt, kann für jeden Bereich ein separater Service VPN definiert werden.

7. Wie kann ich eine Verbindung zwischen dem Service IBM VPN und SoftLayer-Gateway Appliance Service (GaaS) herstellen?

	Sie können einen IPSec-Tunnel erstellen, um eine sichere Verbindung zwischen dem Service IBM VPN und SoftLayer-GaaS einzurichten. [Siehe Konfigurationsbeispiel.](vpn_onpremises.html#gaas){: new_window}
