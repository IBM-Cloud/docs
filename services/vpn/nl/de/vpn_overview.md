---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Informationen zu {{site.data.keyword.vpn_short}}
{: #vpn_overview}  
*Letzte Aktualisierung: 17. März 2016*

Der Service {{site.data.keyword.vpn_full}} (VPN) bietet einen sicheren Kanal für die Kommunikation zwischen dem Rechenzentrum Ihres Unternehmens und Ihren Ressourcen in der IBM Bluemix&reg;-Cloudumgebung. Die Verbindung wird über das Internet hergestellt.
{:shortdesc}

Der Service {{site.data.keyword.vpn_short}} bietet folgende Produktmerkmale:  
##Sicherheit 
Der Service IBM VPN verwendet für die Authentifizierung und die Verschlüsselung der IP-Kommunikation zwischen dem Rechenzentrum Ihres Unternehmens und der IBM Bluemix-Cloudumgebung die standardisierte Protokollsuite Internet Protocol Security (IPSec). IPSec bietet auf Netzwerkebene Peerauthentifizierung, Datenintegrität und Datenschutz (Verschlüsselung).

Der Service IBM VPN unterstützt folgende IPSec-Protokolle und Umsetzungen:

* Authentifizierungsalgorithmus:
	* HMAC-SHA1-96; die Länge des gemeinsam genutzten Schlüssels beträgt 160 Bits (Standardwert)  
* Verschlüsselungsalgorithmus:
	* 3DES-CBC; die Länge des gemeinsam genutzten Schlüssels beträgt 192 Bits
	* AES-CBC; die Länge des gemeinsam genutzten Schlüssels beträgt 128 (Standardwert), 192, 256 Bits
* Authentifizierungs- und Verschlüsselungsprotokolle:
	* Authentifizierungsheader (AH) und ESP-Protokolle (ESP - Encapsulated Security Payload) werden unterstützt. Der Authentifizierungsheader (AH) wird nur zur Authentifizierung verwendet. ESP wird zum Bereitstellen der Authentifizierung und Verschlüsselung verwendet.
* IKEv1-Diffie-Hellman-Schlüsselaustauschgruppen 2 (Standardwert), 5 und 14

Der Service IBM VPN unterstützt den IPSec-Modus 'tunnel'. In diesem Modus unterstützt IPSec das gesamte ursprüngliche IP-Paket. IPSec verschlüsselt das Paket, kapselt es in ein neues IP-Paket ein und leitet das neue Paket an den IPSec-Peer weiter. 

Der Service IBM VPN verwendet den Diffie-Hellman-Schlüsselaustausch und den vorab bekannten gemeinsamen Schlüssel, um die Beziehung zwischen zwei Peers zu schützen. Die Authentifizierung schlägt fehl, wenn eine der Parteien den vorab bekannten gemeinsamen Schlüssel nicht angibt. 
 
Der Service IBM VPN ist konform zu den folgenden IETF-RFCs:

* RFCs 2407, 2408 und 2409 für IKEv1
* RFC 4301 für IPv4-Sicherheit   
* RFC 4302 für den IPv4-Authentifizierungsheader  
* RFC 4303 für IPv4-Encapsulated Security Payload (ESP)  
* RFC 2104 HMAC und RFC 2404 HMAC-SHA-1-96 für Authentifizierung  
* RFC 2451 3DES-CBC; RFC 3602 AES128-CBC, AES192-CBC und AES256-CBC für Verschlüsselung
##Einfachheit
Sie können den Service IBM VPN mithilfe einer einfachen und intuitiv zu bedienenden grafischen Schnittstelle erstellen. Sie können Ihre Gateway-IP-Adresse und die Teilnetze Ihres Rechenzentrums angeben. Sie können entweder IPSec- und IKE-Standardrichtlinien verwenden oder die Richtlinien entsprechend Ihren Bedürfnissen anpassen.  
##Management
Sie können den Service IBM VPN mithilfe einer grafischen Benutzerschnittstelle, einer [Befehlszeilenschnittstelle](../../cli/plugins/vpn/index.html) oder mithilfe von [APIs](https://new-console.ng.bluemix.net/apidocs/101) verwalten.

