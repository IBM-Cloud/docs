---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Gateway in Ihrem Rechenzentrum oder auf Ihrem SoftLayer-Server konfigurieren
{: #vpn_yourdatacenter}
*Letzte Aktualisierung: 17. März 2016*

Sie benötigen in Ihrem Rechenzentrum oder auf Ihrem SoftLayer-Server ein IPSec-VPN-Gateway, um eine sichere Verbindung zum Service {{site.data.keyword.vpn_short}} herzustellen. Folgende VPN-Gateway-Konfigurationen sind in Ihrem Rechenzentrum oder auf Ihrem SoftLayer-Server erforderlich:

* Aktivieren Sie die NAT-Traversierung (NAT - Network Address Translation) für Ihr VPN-Gateway nur, wenn sich Ihr VPN-Gateway hinter der Netzadressumsetzung befindet. 
* Verwenden Sie den vorab bekannten gemeinsamen Schlüssel, den Sie auch bei der Konfiguration des Service IBM VPN verwendet haben.
* Fügen Sie das folgende Teilnetz als fernes Teilnetz hinzu:
	* Wenn Sie im IBM Bluemix-Bereich einzelne Container erstellt haben, fügen Sie 172.31.0.0/16 hinzu.
	* Wenn Sie im Bluemix-Bereich Containergruppen erstellt haben, fügen Sie 172.30.0.0/16 hinzu.
	* Wenn Sie im IBM Bluemix-Bereich einzelne Container und Containergruppen erstellt haben, fügen Sie 172.31.0.0/16 und 172.30.0.0/16 hinzu.
* Stellen Sie sicher, dass die Einstellungen für die Verschlüsselung, die Authentifizierung und die PFS-Gruppe für das IBM VPN-Gateway und Ihr VPN-Gateway gleich sind.
