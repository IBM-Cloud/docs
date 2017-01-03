---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# IBM Secure Service Container
{: #etn_ssc}

Letzte Aktualisierung: 13. Oktober 2016
{: .last-updated}

Das Unternehmensnetz mit hohem Sicherheitsniveau von IBM Blockchain wird als eine Appliance in IBM Secure Service Container bereitgestellt, von dem die Basisinfrastruktur für das Hosting der Blockchain-Services bereitgestellt wird. Von der Appliance werden Betriebssysteme, Docker-Container, Middleware und Softwarekomponenten, die autonom arbeiten, miteinander kombiniert; außerdem werden Basisservices und eine Infrastruktur mit optimierter Sicherheit bereitgestellt.
{:shortdesc}

IBM Secure Service Container bietet eine innovative Verschlüsselung, Sicherheit und die Zuverlässigkeit einer LinuxONE on z Systems-Plattform für Blockchain-Services zum Verarbeiten vertraulicher Daten und von Daten mit gesetzlicher Aufbewahrungsfrist. Blockchain wird durch eine Reihe von Funktionen von IBM Secure Service Container geschützt: ein gekapseltes Betriebssystem, verschlüsselte Applianceplatten, Manipulationsschutz, geschützter Hauptspeicher und eine starke LPAR-Isolation, die so konfiguriert werden kann, dass sie der Zertifizierung EAL5+ entspricht.

Im folgenden Architekturdiagramm wird veranschaulicht, wie IBM Secure Service Container und die Blockchain-Appliances organisiert sind:

![Architekturdiagramm](images/Architecture_HSBN_SSC.png "IBM Secure Service Container und Blockchain-Appliances")
*Abbildung 1. Übersicht über IBM Secure Service Container und Blockchain-Appliances*
<br><br>
## Wichtigste Sicherheitsfunktionen
Von IBM Secure Service Container werden die folgenden optimierten Sicherheitsfunktionen für Blockchain-Services bereitgestellt:  

### Schutz vor Systemadministratoren
>Auf den Appliance-Code können nicht einmal Plattform- oder Systemadministratoren zugreifen.  Der Datenzugriff wird von der Appliance kontrolliert, unbefugter Zugriff ist somit nicht möglich.  Dies wird auch durch eine Kombination aus Signierungen und Verschlüsselungen aller momentan aktiven bzw. übertragenen Daten und ruhenden Daten unterstützt. Auch der Zugriff auf den Hauptspeicher ist nicht möglich. Von der Firmware wird dies durch eine Architektur zum sicheren Booten (Secure Boot Architecture) unterstützt.

>Systemadministratoren unterliegen den folgenden Beschränkungen, wenn Blockchain durch IBM Secure Service Container gesichert ist:
>* Kein Zugriff auf Knoten
>* Kein Anzeigen des Blockchain-Netzes

### Schutz vor Manipulation  
>Von IBM Secure Service Container werden alle externen Schnittstellen inaktiviert, von denen Zugriff auf den LPAR-Hauptspeicher bereitgestellt wird. Ein Bootladeprogramm für Images ist signiert, um sicherzustellen, dass es nicht manipuliert oder gegen ein anderes ausgetauscht werden kann.

### Verschlüsselte Applianceplatten
>Der gesamte Code und alle Daten auf den Platten werden fortlaufend unter Verwendung der Linux-Verschlüsselungsebene verschlüsselt:  
- Gekapseltes Betriebssystem
- Geschützte IP
- Integrierte Überwachung und automatische Fehlerbehebung  
<br>

## Appliances über REST-APIs verwalten
Die Software-Appliances sind für die Verwendung auf einer zuverlässigen, sicheren und skalierbaren z Systems-Plattform vorkonfiguriert. Sie können diese Appliances über REST-APIs ohne Konfiguration verwalten.

Zum Verwalten von Blockchain-Assets über REST-APIs können Sie die Swagger-Benutzerschnittstelle im Blockchain-Dashboard für Bluemix oder REST-Befehlstools wie `curl` oder `Postman` verwenden.

Wenn Sie zum Beispiel Informationen zu allen Peers im Netz abrufen möchten, setzen Sie mithilfe von `curl` den folgenden Befehl ab:
```
curl -u <username>:<password> https://<peer_ip>:<port>/network/peers
```
Im Folgenden werden der curl-Beispielbefehl und die zurückgegebenen Ergebnisse angegeben:
* Befehl:
```
curl -u dashboarduser_type0_2ef27***:89317***https://ad3130e8-4a1a-4ce6-a084-689a345a3308_vp1-api.blockchain.ibm.com:443/network/peers
```
* Für alle Peers im Netz zurückgegebene Informationen:
```
{
	"peers": [{
		"ID": {
			"name": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp2"
		},
		"address": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp2-discovery.blockchain.ibm.com:30303",
		"type": 1,
		"pkiID": "rC0uvv0cbSbiT8RUGKPQM3q/o09oyWlcBmRxogi2Cls="
	},
	{
		"ID": {
			"name": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp1"
		},
		"address": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp1-discovery.blockchain.ibm.com:30303",
		"type": 1,
		"pkiID": "oeoI+Xa/lW8Xvrvv71A+Nvzit+JDa+oIkthpZHwfaTE="
	}]
}
```
Weitere Informationen zum Interagieren mit Blockchain über REST-APIs finden Sie in [Dashboard-Überwachung](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchainmonitor.html) und [Beispielapps und Lernprogramme](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchain_tutorials.html).
