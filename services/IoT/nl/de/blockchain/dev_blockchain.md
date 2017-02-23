---

copyright:
  years: 2016, 2017
lastupdated: "2017-2-6"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Intelligente Verträge für die {{site.data.keyword.iot_short_notm}}-Blockchain-Integration entwickeln
{: #iotblockchain_link}

Verwenden Sie {{site.data.keyword.blockchainfull}} und die Hyperledger-Entwicklungsumgebung zum Erstellen und Testen eigener intelligenter Verträge, die aus Beispielverträgen abgeleitet sind, die von IBM bereitgestellt wurden.
{:shortdesc}

Entwickeln und implementieren Sie intelligente Verträge im Format von ausführbaren Dateien mit GoLang-Chaincode. Verwenden Sie die {{site.data.keyword.iot_short_notm}}-Blockchain-Integration, um mithilfe von Geräteereignisdaten Vertragsaktualisierungen und die Ausführung von Geschäftslogik auszulösen und für jede Transaktion einen neuen Kontostatus an Blockchain zu schreiben.

Eine Entwicklungsumgebung mit {{site.data.keyword.iot_short_notm}}-Blockchain-Integration besteht aus folgenden Komponenten:

- {{site.data.keyword.Bluemix_notm}}-Organisation:
  - {{site.data.keyword.iot_short_notm}}-Service mit aktivierter IoT-Blockchain-Integration
  - {{site.data.keyword.blockchainfull_notm}}-Fabric
  - Node-RED-Anwendung, die einen IoT-Gerätesimulator ausführt
   

**Hinweis:** Sie können auch eine lokal implementierte Node-RED-Umgebung verwenden, um den Simulator auszuführen.

- Lokale Umgebung:
  - Hyperledger-Entwicklungsumgebung zum Entwickeln und Testen von Chaincode für intelligente Verträge. Die Umgebung beinhaltet GoLang.
  - Blockchain-Benutzerschnittstelle für die Überwachung
- GitHub-Umgebung:
  - Von IBM bereitgestelltes GitHub-Repository für Beispiele von intelligenten Verträgen
  - GitHub-Repository zum Bereitstellen von intelligenten Verträgen für das {{site.data.keyword.blockchainfull_notm}}-Fabric

Das folgende Diagramm veranschaulicht die Entwicklungsumgebung für die {{site.data.keyword.iot_short_notm}}-Blockchain-Integration:
![Die Integrationsarchitektur von IoT-Blockchain und {{site.data.keyword.iot_short_notm}}.](images/architecture_contracts.svg "Integrationsarchitektur von IoT-Blockchain und {{site.data.keyword.iot_short_notm}}")

## Vorbereitende Schritte

{: #byb}

Verschaffen Sie sich eine Übersicht über {{site.data.keyword.blockchainfull_notm}}, wie die Beziehung zum allgemeinen Blockchain-Konzept ist und welche Aufgaben es für Sie erledigen kann:
- [{{site.data.keyword.blockchainfull_notm}}](http://www.ibm.com/blockchain/) bei IBM.com.
- [{{site.data.keyword.blockchainfull_notm}}-DOKUMENTATION](https://console.ng.bluemix.net/docs/services/blockchain/index.html) - Einführung in den {{site.data.keyword.blockchainfull_notm}}-Service.
- [{{site.data.keyword.blockchainfull_notm}}-API](https://ibmblockchainapi.mybluemix.net/swagger/ui.html?scheme=http&host=127.0.0.1:3000&basepath=/) -  Eine Übersicht der {{site.data.keyword.blockchainfull_notm}}-API.
- [{{site.data.keyword.blockchainfull_notm}} für Entwickler](http://www.ibm.com/blockchain/for_developers.html)  - Eine Übersicht dazu, wie sich Blockchain in Ihre Entwicklungsumgebung einfügt, die einen Rundgang mit Live-Demos und Code enthält, der für eine Ausführung in {{site.data.keyword.Bluemix_notm}} bereitgestellt werden kann.

## Beispiele für intelligente Verträge

{: #samples}

Wenn Sie die Webadresse [https://github.com/ibm-watson-iot/blockchain-samples](https://github.com/ibm-watson-iot/blockchain-samples) aufrufen, können Sie eine Reihe von Beispielverträgen herunterladen. Sie können die Beispielverträge als Basis verwenden, um Ihre eigenen Anwendungsfälle im Format bereitstellbaren Chaincodes zu entwickeln.

|Beispielvertrag |Beschreibung |
|:---|:---|
|[Grundlegend: Einfacher Vertrag](https://github.com/ibm-watson-iot/blockchain-samples/tree/master/contracts/basic/simple_contract) | Eine vereinfachte Version des erweiterten Vertrags, mit der Sie Assetdaten zu Geräten in Blockchain verfolgen und speichern können.
|[Erweitert: Generischer IoT-Beispielvertrag](https://github.com/ibm-watson-iot/blockchain-samples/tree/master/contracts/advanced/iot_sample_contract) | Ein erweiterter Beispielvertrag, der viele Merkmale aufweist und dessen Datenmodell und Verhalten stärker an **Trade Lane** erinnert.|


## {{site.data.keyword.blockchainfull_notm}}-Umgebung konfigurieren

{: #configure_environment}
Bevor Sie mit der Bereitstellung und dem Testen von intelligenten Verträgen beginnen, müssen Sie Ihre eigene Blockchain-Umgebung einrichten.

**Hinweis:** Die {{site.data.keyword.iot_short_notm}}-Blockchain-Integration unterstützt das Herstellen von Verbindungen sowohl zu {{site.data.keyword.blockchainfull_notm}}-Fabrics als auch zu Hyperledger-Fabrics. In den folgenden Beispielen wird {{site.data.keyword.blockchainfull_notm}} verwendet.

1. Erstellen und konfigurieren Sie Ihr {{site.data.keyword.blockchainfull_notm}}-Fabric.
Für die {{site.data.keyword.iot_short_notm}}-Blockchain-Integration ist das {{site.data.keyword.blockchainfull_notm}}-Fabric erforderlich, damit das Blockchain-Konto, intelligente Verträge und die allgemeine Blockchain-Infrastruktur verwaltet werden können. Bei der {{site.data.keyword.Bluemix_notm}}-Blockchain-Integration wird zum Verwalten der Ketten (Chains) {{site.data.keyword.blockchainfull_notm}} verwendet. Wenn Sie Zugriff auf eine vorhandene {{site.data.keyword.blockchainfull_notm}}-Umgebung haben, können Sie diese verwenden. Falls nicht, müssen Sie ausgehend vom {{site.data.keyword.Bluemix_notm}}-[Katalog](https://console.ng.bluemix.net/catalog/services/blockchain/) eine Instanz von {{site.data.keyword.blockchainfull_notm}} erstellen.

  1. Klicken Sie im Dashboard Ihres {{site.data.keyword.Bluemix_notm}}-Kontos auf **Services oder APIs verwenden**.
  2. Suchen Sie den Abschnitt für Anwendungsservices im Servicekatalog und wählen Sie **Blockchain** aus.  
   **Tipp:** Klicken Sie [hier](https://console.ng.bluemix.net/catalog/services/blockchain/), um direkt zur Seite mit dem {{site.data.keyword.blockchainfull_notm}}-Service zu gelangen.
  3. Überprüfen Sie auf der Seite des {{site.data.keyword.blockchainfull_notm}}-Service die Auswahl für 'Service hinzufügen':  
    - Bereich - Wenn Sie außer dem Standardbereich `dev` weitere Bereiche haben, müssen Sie überprüfen, dass der Service im gewünschten Bereich bereitgestellt wird.
    - App - Nicht binden.
    - Servicename - Sie können den Servicenamen optional in einen Namen ändern, der leichter zu merken ist. Dieser Name wird auf der {{site.data.keyword.blockchainfull_notm}}-Kachel im Dashboard von {{site.data.keyword.Bluemix_notm}} angezeigt.
    - Ausgewählter Plan - Wählen Sie den kostenlosen Plan aus ('Free'). Mit dem kostenlosen Plan werden zwei Peers zum Prüfen und eine Zertifizierungsstelle bereitgestellt.
  4. Klicken Sie auf **Erstellen**, um {{site.data.keyword.blockchainfull_notm}} in {{site.data.keyword.Bluemix_notm}} bereitzustellen.  
  Die Blockchain-Instanz wird zunächst mit zwei Peerknoten bereitgestellt. Sie können nach Bedarf weitere Knoten hinzufügen.

4. Verlinken Sie {{site.data.keyword.iot_short_notm}} mit Ihrem {{site.data.keyword.blockchainfull_notm}}-Service.  
    Um von {{site.data.keyword.iot_short_notm}} aus an Blockchain zu schreiben, müssen Sie die Services zunächst verlinken.
     1. Wechseln Sie in {{site.data.keyword.Bluemix_notm}} zum Dashboard.
     2. Wählen Sie den Bereich aus, in dem Sie {{site.data.keyword.blockchainfull_notm}} bereitgestellt haben.
     3. Klicken Sie auf die Kachel **Blockchain**.
     4. Klicken Sie im linken Teilfenster auf **Serviceberechtigungsnachweise**.
     5. Wählen Sie eine Gruppe von Serviceberechtigungsnachweisen aus oder klicken Sie auf **Berechtigungsnachweise hinzufügen**, um eine neue Gruppe von Serviceberechtigungsnachweisen zu erstellen, und benennen Sie diese Gruppe mit einem beschreibenden Namen wie beispielsweise 'IoT Platform-Integration'.
     6. Notieren Sie sich in den Serviceberechtigungsnachweisen, die das JSON-Format aufweisen, folgende Parameter:  
      - Peerinformationen: `api_host` und `api_port`.
      - Benutzer der Informationen des Typs 1 (Client): `username` und `secret`.  

      Beispiel für Serviceberechtigungsnachweise:
     ```json
     {
      "credentials": {
      "peers": [
      {
       "discovery_host": "169.44.63.203",
       "discovery_port": "32904",
       "api_host": "169.44.63.203",
       "api_port_tls": "443",
       "api_port": "80",
       "type": "peer",
       "network_id": "f621cde2-bdec-4897-b737-da4df144c41f",
       "container_id": "5750f7734fb06c64d70c443b1dfcf39a3f5de7b51b792294c05dbdbe7d8356f7",
       "id": "f621cde2-bdec-4897-b737-da4df144c41f_vp1",
       "api_url": "http://169.44.63.203:32905"
      },
       ...
      ],
      "users": [
      {
       "username": "user_type1_fa8e6ef0dc",
       "secret": "33401036a9"
      },
       ...
       ]
      }
     }
     ```  
     **Wichtig:** Der Benutzer, den Sie auswählen, darf nicht zuvor für einen anderen als den von Ihnen ausgewählten Peer registriert worden sein.
     7. Klicken Sie auf **Zurück zum Dashboard**, um zu Ihrem {{site.data.keyword.Bluemix_notm}}-Dashboard zurückzukehren.
     8. Wählen Sie den Bereich aus, in dem Sie {{site.data.keyword.iot_short_notm}} bereitgestellt haben.
     9. Klicken Sie auf die Kachel für **{{site.data.keyword.iot_short_notm}}**.
     10. Klicken Sie auf die Option zum **Starten**, um das {{site.data.keyword.iot_short_notm}}-Dashboard zu öffnen.
     11. Wählen Sie im {{site.data.keyword.iot_short_notm}}-Dashboard in der seitlichen Menüleiste die Option **Erweiterungen** aus.
     12. Klicken Sie auf der Seite **Erweiterungen** der Kachel 'Blockchain' auf **Einrichten** oder klicken Sie auf ![Zahnradsymbol](../images/gear.png "Konfigurieren"), falls bereits Fabrics verbunden sind.
     13. Klicken Sie im Abschnitt zum Konfigurieren von Blockchain auf **Fabric hinzufügen** und geben Sie anschließend die Fabric-Informationen ein.
    **Hinweis:** Damit Fabrics hinzugefügt werden können, muss die Blockchain-Integration aktiviert sein. Informationen dazu finden Sie unter [Blockchain](../reference/extensions/index.html#blockchain) im Abschnitt 'Externe Services integrieren'.
    1. Geben Sie auf der Registerkarte **Fabric** einen Namen ein, um das Fabric in {{site.data.keyword.iot_short_notm}} anzugeben, und klicken Sie anschließend auf **Weiter**.   
    2. Geben Sie auf der Registerkarte **Peer** die Peerinformationen ein.  
   <table>
   <thead>
   <tr>
   <th>Parameter</th>
   <th>Wert</th>
   </tr>
   </thead>
   <tbody>
   <tr>
   <td>Name</td>
   <td>Geben Sie einen Namen ein, um den Peer in {{site.data.keyword.iot_short_notm}} anzugeben.</td>
   </tr>
   <tr>
   <td>Host</td>
   <td>Die Adresse `api_host` für den Server des überprüfenden Peers 1.</td>
   </tr>
   <tr>
   <td>Port</td>
   <td>Die Nummer `api_port`.<ul><li>Verwenden Sie Port 80, wenn Ihre Implementierung kein TLS verwendet.</li><li>Verwenden Sie Port 443, wenn Ihre Implementierung TLS verwendet.</li></ul></td>
   </tr>
   <tr>
   <td>Benutzer-ID</td>
   <td>Die Zeichenfolge `username` (Benutzername) für den Benutzer, die zum Registrieren des intelligenten Vertrags bei Blockchain verwendet wurde. Sie verwenden diese Benutzer-ID auch, wenn Sie später die einfache Benutzerschnittstelle konfigurieren (Simple UI).</td>
   </tr>
   <tr>
   <td>Geheimer Schlüssel</td>
   <td>Die Zeichenfolge `secret` für den Benutzer.</td>
   </tr>
   <tr>
   <td>TLS verwenden</td>
   <td>An oder Aus</br>Verwenden Sie Transport Layer Security, um die Kommunikation zwischen {{site.data.keyword.iot_short_notm}} und dem Vertrag im Fabric zu verschlüsseln. Die Standardportnummern werden durch die bereitgestellte {{site.data.keyword.iot_short_notm}}-Instanz festgelegt, zu der Sie eine Verbindung herstellen.</td>
   </tr></tbody>
   </table>  
    3. Klicken Sie auf **Fertigstellen**.
     3. Klicken Sie im Abschnitt zum Konfigurieren von Blockchain auf **Fertig**, um die Fabric-Informationen zu speichern.    

Die Fabric-Tabelle wird mit der neuen Verbindung für das Fabric gefüllt..  

## Intelligente Verträge erstellen, testen und bereitstellen
{: #test_contracts}

Sie können nun in GoLang Ihren eigenen Chaincode für intelligente Verträge erstellen, ihn in der Sandboxumgebung testen und ihn in Ihrem eigenen {{site.data.keyword.blockchainfull_notm}}-Fabric bereitstellen und testen.

1. Erstellen Sie ein GitHub-Projekt, um den Chaincode für intelligente Verträge zu speichern.  
Intelligente Verträge, die Sie bereitstellen möchten, müssen sich in einem öffentlichen GitHub-Repository befinden. Weitere Informationen finden Sie unter https://github.com/.
2.  Richten Sie eine lokale Hyperledger-Entwicklung- und Testumgebung ein.  
Um Ihren eigenen Chaincode vor dem Bereitstellen in {{site.data.keyword.blockchainfull_notm}} zu entwickeln und zu testen, müssen Sie eine lokale Entwicklungsumgebung einrichten. Diese Umgebung umfasst GoLang, das zum Schreiben des Chaincodes für Ihre Verträge verwendet wird.
 1. Richten Sie die Entwicklungsumgebung ein.  
 Die Entwicklungsumgebung umfasst die Tools, die Sie benötigen, um mithilfe der Chaincodeerstellung in GoLang intelligente Verträge zu entwickeln. Weitere Informationen finden Sie in [Setting up the development environment](https://github.com/hyperledger/fabric/blob/master/docs/dev-setup/devenv.md) in der Hyperledger-Dokumentation.
 2. Installieren Sie eine Debugumgebung für den Chaincode.   
 Durch die Debugumgebung verfügen Sie über die Tools, die Sie zum Testen und für die Fehlerbehebung der intelligenten Verträge benötigen, bevor Sie sie in {{site.data.keyword.blockchainfull_notm}} bereitstellen. Weitere Informationen finden Sie in [Writing, Building, and Running Chaincode in a Development Environment](https://github.com/hyperledger/fabric/blob/master/docs/Setup/Chaincode-setup.md) in der Hyperledger-Dokumentation.
 3. Richten Sie ein Netzwerk für die Entwicklung ein.   
 Durch das Netz für die Entwicklung verfügen Sie über eine striktere, produktionsähnliche Umgebung zum abschließenden Testen Ihrer intelligenten Verträge.  Verwenden Sie diese Umgebung zum abschließenden Testen Ihrer getesteten Verträge, für die ein Debugging ausgeführt wurde, bevor Sie sie in {{site.data.keyword.blockchainfull_notm}} bereitstellen. Weitere Informationen finden Sie in [Setting Up a Network](https://github.com/hyperledger/fabric/blob/master/docs/Setup/Network-setup.md) in der Hyperledger-Dokumentation.

3. Optional: Laden Sie die von IBM bereitgestellten Beispiele für intelligente Verträge herunter.  
IBM stellt eine Reihe von intelligenten Verträgen bereit, die Sie herunterladen und unverändert sofort verwenden können bzw. für Ihre Unternehmensziele anpassen können.  
Gehen Sie wie folgt vor, um die Beispielverträge herunterzuladen:
 1. Wechseln Sie zum GitHub-Repository mit den Blockchain-Beispielen unter https://github.com/ibm-watson-iot/blockchain-samples/.  
Die Ordner 'basic_contract_hyperledger' und 'trade_lane_contract_hyperledger' enthalten den Basisvertrag bzw. den Trade Lane-Vertrag.
 3. Mit der Option `git clone` im Terminal können Sie das https://github.com/ibm-watson-iot/blockchain-samples-Projekt klonen.  
 **Tipp:** Sie können auch eine komprimierte Datei des Projekts herunterladen, indem Sie auf der Projektseite auf **Download ZIP** klicken.

6. Erstellen und testen Sie einen intelligenten Vertrag.   
 Durch Verwendung der {{site.data.keyword.iot_short_notm}}-Blockchain-Integration können Sie intelligente Verträge im Format ausführbarer Chaincode-Dateien in {{site.data.keyword.blockchainfull_notm}} hochladen, um für die Gerätedaten, die an Blockchain geschrieben werden, Geschäftslogik auszuführen. Der Chaincode für intelligente Verträge wird in GoLang entwickelt.  
 Der Fokus bei dem Beispielvertrag liegt darauf, IoT-Gerätedaten für interessante Ereignisse an Blockchain zu schreiben, um diese mit Dritten gemeinsam zu nutzen oder um manipulationsresistente Protokolleinträge zu erstellen.
2. Erstellen Sie die ausführbaren Dateien für den Vertrag.  
  Der Vertragscode muss in eine ausführbare Datei konvertiert werden, bevor er in Blockchain bereitgestellt werden kann.  
  **Hinweis:** Der Beispielvertrag (sample_contract_hyperledger) wurde bereits generiert und kann unverändert bereitgestellt werden.  
  Führen Sie folgende Schritte aus:
   1. Öffnen Sie die Befehlszeile und navigieren Sie zum Vertragsordner.
   2. Führen Sie den Befehl `go generate` aus.  
   Mit diesem Befehl werden alle 'go generate'-Befehle ausgeführt, die im Code vorhanden sind. 'Go generate' ist ein 'go program'-Tool, mit dem eine Codegenerierung in der Buildvorbereitung möglich ist. In den von IBM bereitgestellten Beispielverträgen wird 'go generate' zum Erstellen der Datei 'schemas.go' verwendet, in der das Vertragsschema und die Vertragsdatei 'sample.go' dargestellt ist.  
   **Wichtig:** Die Datei 'schemas.go' ist eine kritische Komponente für die {{site.data.keyword.iot_short_notm}}-Blockchain-Integration eine kritische Komponente. Mithilfe der Datei bestätigt die Plattform, dass der Vertrag die Integrationsspezifikation einhält und der Mapper kann die Vertrags-API anzeigen, der Geräteereignisse zugeordnet werden können.
   2. Führen Sie den Befehl `go build` aus.  
   Mit diesem Befehl wird eine ausführbare Datei erstellt, die denselben Namen wie der Ordner hat. Die Datei ist die ausführbare Datei des Vertrags und sie wird in Blockchain bereitgestellt.

6. Testen Sie den intelligenten Vertrag in der Hyperledger-Sandbox.  
  Vor dem Bereitstellen Ihres abgeschlossenen intelligenten Vertrags in {{site.data.keyword.blockchainfull_notm}} können Sie den Chaincode in der Hyperledger-Sandbox, die als Bestandteil Ihrer Entwicklungsumgebung installiert wurde, testen und ein Debugging ausführen.  

6. Stellen Sie den Chaincode des intelligenten Vertrags in {{site.data.keyword.blockchainfull_notm}} bereit.  
 Nach dem lokalen Testen und Bestätigen Ihres Vertrags können Sie ihn zum Testen in Ihrem {{site.data.keyword.blockchainfull_notm}}-Fabric bereitstellen.
  1. Laden Sie Ihren Vertrag in Ihr öffentliches GitHub-Repository hoch.  
  Laden Sie die Datei 'sample.go' beispielsweise an diese Position hoch:
    
  `http://github.com/{my organization}/{my project}/`
  2. Registrieren Sie den Vertrag auf dem Peer, zu dem Sie zuvor eine Verbindung hergestellt haben.  
  Verwenden Sie einen REST-Client wie beispielsweise CURL oder Postman, um den Registrierungsaufruf zu übergeben. Weitere Informationen zum Registrierungsaufruf finden Sie in der [Dokumentation zur POST-Registrator-API](https://ibmblockchainapi.mybluemix.net/swagger/ui.html?scheme=http&host=127.0.0.1:3000&basepath=/#!/Registrar/registerUser). Verwenden Sie bei der Registrierung folgende Informationen:
  <ul>
  <li>URL: `http://api_host:api_port/registrar`
  <li>Typ: POST
  <li>Header: `Content type: application/x-www-form-urlencoded`
  <li>Nutzdaten:  
  ```json
   {  
        "enrollId": "{username}",      
        "enrollSecret": "{secret}"    
   }
   ```

  </ul>
  3. Stellen Sie den Vertrag auf dem Peer bereit.  
  Weitere Informationen zum Aufruf für das Bereitstellen finden Sie in der [Dokumentation zur POST-API 'devops/deploy'](https://ibmblockchainapi.mybluemix.net/swagger/ui.html?scheme=http&host=127.0.0.1:3000&basepath=/#!/Devops/chaincodeDeploy).  
  Verwenden Sie bei der Bereitstellung folgende Informationen:  
  <ul>
  <li>URL: `http://api_host:api_port/devops/deploy`
  <li>Typ: POST
  <li>Header: `Content type: application/x-www-form-urlencoded`
  <li>Nutzdaten:  
  ```
  {
      "type": "GOLANG",   
      "chaincodeID": {  
      "path": "http://github.com/{my organization}/{my project}/sample.go",
      "name": "string"
    },
    "ctorMsg": {  
      "function": "init",  
      "args": [
        "{\"version\":\"1.0\}"}"
      ]
    },
    "secureContext": "'username'",
    "confidentialityLevel": "PUBLIC"
  }
  ```  
  </ul>  
  Ihr Vertrag wird im Fabric bereitgestellt.  
  **Wichtig:** Notieren Sie die ID des Vertrags, die zurückgegeben wird und die das Format einer alphanumerischen Zeichenfolge mit 128 Zeichen hat. Sie benötigen die Vertrags-ID, um dem Vertrag Geräte zuzuordnen.  

10. Ordnen Sie die Gerätedaten dem neuen intelligenten Vertrag zu.  
  Bevor Sie an die neuen intelligenten Blockchain-Verträge Gerätedaten schreiben, müssen Sie den Verträgen zunächst Gerätedaten zuordnen.  
   1. Wechseln Sie in {{site.data.keyword.Bluemix_notm}} zum Dashboard.
   2. Wählen Sie den Bereich aus, in dem Sie {{site.data.keyword.iot_short_notm}} bereitgestellt haben.
   3. Klicken Sie auf die Kachel für **{{site.data.keyword.iot_short_notm}}**.
   4. Klicken Sie auf die Option zum **Starten**, um das {{site.data.keyword.iot_short_notm}}-Dashboard zu öffnen.
   5. Wählen Sie **Blockchain** aus, indem Sie in der seitlichen Menüleiste auf ![Blockchain](images/platform_blockchain.png "Blockchain") klicken.
   6. Klicken Sie auf **Link zu Vertrag erstellen**.
   6. Wählen Sie den Fabric-Namen für das Fabric aus, das Sie zuvor erstellt haben.
   7. Geben Sie folgende Informationen ein:  
     - Vertrags-ID - Fügen Sie die aus 128 Zeichen bestehende Vertrags-ID ein, die Sie beim Bereitstellen des Vertrags gespeichert haben.
     - Vertragsname - Geben Sie einen Namen ein, um den Vertrag in {{site.data.keyword.iot_short_notm}} anzugeben.
     - Wählen Sie den Gerätetyp aus, für den Sie Gerätedaten in Blockchain speichern wollen.
     - Wählen Sie den Ereignisnamen für die Ereignisse aus, die Sie speichern möchten.  
     **Tipp:** Um die Ereignistypen für ein Gerät zu finden, wechseln Sie zur Seite **Geräte** und klicken Sie auf den Gerätenamen, um die Detailseite des Geräts zu öffnen. Blättern Sie abwärts zum Abschnitt **Sensorinformationen**, um eine Liste der verfügbaren Ereignisse und Datenpunkte für das Gerät anzuzeigen.

   11. Ordnen Sie die verfügbaren Geräteeigenschaften den Vertragsparametern zu.   
   **Wichtig:** Überprüfen Sie, dass der Datentyp für die jeweiligen von Ihnen zugeordneten Datenpunkte dem Datentyp entspricht, der für den Vertragsparameter, dem sie ihn zuordnen, erforderlich ist.  
   Eine Vertragseigenschaft wie eine Asset-ID des Typs 'Zeichenfolge' (string) muss beispielsweise einer Eigenschaft mit dem Typ 'Zeichenfolge' zugeordnet werden. Die für Vertragsparameter bestehenden Anforderungen sind in den `type`-Definitionen im Go-Code des Vertrags definiert.  
   Der von IBM bereitgestellte Basisvertrag gibt für Vertragsparameter beispielsweise folgende Anforderungen an:  
    <ul>
    <li>  Asset-ID - string
    <li>  Position - Geoortung  
    <ul>
    <li> Breitengrad - float64
    <li>  Längengrad - float64
    </ul>
    <li>  Temperatur - float64  
    <li>  Netzbetreiber - string   
    </ul>  
    Weitere Informationen zur Vorgehensweise, wie Gerätedaten Verträgen zugeordnet werden, finden Sie im [Datenzuordnungsbeispiel](https://github.com/ibm-watson-iot/blockchain-samples/wiki/Data-mapping-example) im Wiki mit den IoT-Blockchain-Beispielen unter GitHub.
   12. Überprüfen Sie auf der Übersichtsseite die Richtigkeit der Informationen.
   13. Die Zuordnung der Gerätedaten zum Vertrag wird auf der Blockchain-Seite angezeigt.

7. Testen Sie Ihren intelligenten Vertrag in {{site.data.keyword.blockchainfull_notm}}.  
Zum Testen Ihres intelligenten Vertrags führen Sie einen umfassenden Test durch, indem Sie in {{site.data.keyword.iot_short_notm}} ein Gerät erstellen, für Ihr Gerät eine Verbindung zu {{site.data.keyword.iot_short_notm}} herstellen, IoT-Blockchain konfigurieren, um eine Verbindung zu Ihrem Blockchain-Fabric herzustellen und {{site.data.keyword.iot_short_notm}} so konfigurieren, dass Ihre Gerätenachrichten in Blockchain zugeordnet und gespeichert werden. Bei Verwendung der {{site.data.keyword.blockchainfull_notm}}-Konsole können Sie die Blockchain anzeigen, um die Gerätedaten im Konto zu lesen. Wenn Ihr Vertrag die Funktion 'readAsset()' unterstützt, können Sie die Blockchain mithilfe der Benutzerschnittstelle für die Überwachung anzeigen, um die Gerätedaten Ihres eigenen Szenarios zu lesen, die unlöschbar in Blockchain gespeichert sind.

5. Konfigurieren Sie die Benutzerschnittstelle für die Überwachung, um eine Verbindung zu {{site.data.keyword.blockchainfull_notm}} herzustellen.  
 **Tipp:** Wenn Sie die Benutzerschnittstelle für die Überwachung nicht in Ihrer lokalen Umgebung installiert haben, können Sie dies jetzt tun. Folgen Sie den Anweisungen im Readme-Dokument der Benutzerschnittstelle für die Überwachung, das im GitHub-Verzeichnis der [Blockchain-Benutzerschnittstelle für die Überwachung](https://github.com/ibm-watson-iot/blockchain-samples/tree/master/applications/monitoring_ui) verfügbar ist.  
 Rufen Sie die Konfigurationseinstellungen durch Klicken auf die Schaltfläche **Konfiguration** auf.   
 Verwenden Sie zum Herstellen einer Verbindung zu einem Vertrag folgende Informationen:
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Wert</th>
<th>Kommentar</th>
</tr>
</thead>
<tbody>
<tr>
<td>API Host and Port</td>
<td>`http://peer_URL:port`</td>
<td>Der Host und der Port für die {{site.data.keyword.blockchainfull_notm}}-REST-API, der `http://` vorangestellt ist. Verwenden Sie die Adresse `api_host` und die Nummer `api_port`. </td>
</tr>
<tr>
<td>Chaincode ID</td>
<td>Die Vertrags-ID, die zurückgegeben wurde, als Sie den Vertrag registriert haben.</td>
<td>Die Vertrags-ID ist eine alphanumerische Zeichenfolge aus 128 Zeichen, die dem Eintrag für die Vertrags-ID entspricht.  
**Wichtig:** Wenn Sie die Vertrags-ID ausschneiden und einfügen, müssen Sie sicherstellen, dass in der ID keine Leerzeichen enthalten sind. Wenn die ID falsch eingegeben wird, werden die Einträge des Blockchain-Kontos angezeigt, aber die Suchfunktion für Assets funktioniert nicht.
</td>
</tr>
<tr>
<td>Secure Context</td>
<td>Der Benutzer des Fabrics.</td>
<td>Dieser Parameter ist für das Herstellen einer Verbindung zu {{site.data.keyword.blockchainfull_notm}}-Instanzen in {{site.data.keyword.Bluemix_notm}} erforderlich. Verwenden Sie den Eintrag `secureContext`.  
**Wichtig:** Der Wert für 'secureContext' sollte der Benutzername (`username`) sein, den Sie zum Konfigurieren des Fabrics verwendet haben.
</td>
</tr>
<tr>
<td>Number of blocks to display</td>
<td>Eine positive ganze Zahl. Standardwert: 10</td>
<td>Die Anzahl der anzuzeigenden Blockchain-Blöcke.
</td>
</tr>
</tbody>
</table>

3. Überprüfen Sie in der Benutzerschnittstelle für die Überwachung, dass Ihr Setup wie erwartet funktioniert.  
Verwenden Sie die Komponenten der Benutzerschnittstelle für die Überwachung, um mit dem Blockchain-Vertrag zu interagieren:  
 - Chaincode-Operationen  
Überprüfen Sie, dass die vertragsspezifischen Chaincode-Operationen wie erwartet ausgeführt werden können. Überprüfen Sie beispielsweise für den Basisvertrag, dass die Ausführung der Funktion `createAsset` dazu führt, dass ein Asset zu Blockchain hinzugefügt wird.
 - Antwortnutzdaten  
Stellen Sie sicher, dass Antworten auf Peer-Anforderungen wie erwartet angezeigt werden, wenn Sie REST-Anforderungen über die Registerkarte für Chaincode-Operationen übergeben.
 - Blockchain  
Überprüfen Sie, dass beim Einfügen von Daten, die von einem verbundenen Gerät stammen, oder bei der Verwendung der Komponente für Chaincode-Operationen in der Kette (Chain) Blöcke hinzugefügt werden.    

## Nächste Schritte
{: #next_steps}

Sie haben nun die von IBM bereitgestellten Beispiele für intelligente Verträge bereitgestellt und untersucht. Der Basisvertrag und der Trade Lane-Vertrag bieten jedoch nur eingeschränkte Beispiele für die vielen Möglichkeiten, die Ihnen durch gut entworfenen Chaincode für intelligente Verträge eröffnet werden. Sie können nun experimentieren und Ihre Geschäftsszenarios in {{site.data.keyword.blockchainfull_notm}} Chaincode-Verträgen zuordnen. Anschließend können Sie {{site.data.keyword.iot_short_notm}} mit der IoT-Blockchain-Integration verwenden, um Gerätedaten in das Blockchain-Konto zu schreiben und als Antwort auf die Daten als intelligente Verträge gespeicherte Geschäftslogik auszuführen.     


Viel Spaß beim Arbeiten mit Blockchain!
