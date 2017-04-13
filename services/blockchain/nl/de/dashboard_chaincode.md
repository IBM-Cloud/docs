---

copyright:
  years: 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Chaincode
{: #v10_dashboard}
Letzte Aktualisierung: 16. März 2017
{: .last-updated}

Bei Chaincode handelt es sich um Software (derzeit in Go oder Java geschrieben), die die Geschäftslogik und transaktionsorientierten Anweisungen zum Erstellen und Ändern von Assets umfasst. Sie wird in einem Docker-Container ausgeführt, der den Peers zugeordnet ist, die mit diesem Container interagieren müssen.  
{:shortdesc}

Chaincode wird zunächst im Dateisystem eines Peers installiert und anschließend auf einem Kanal instanziiert. Bei der Instanziierung müssen Schlüssel/Wert-Paare initialisiert und der Chaincode-Container bereitgestellt werden. Für jeden Peer, der mit
einem Chaincode interagieren möchten, muss der Quellcode im entsprechenden Dateisystem installiert und ein Chaincode-Container aktiv sein. Wenn jedoch ein Peer dieselbe Chaincode-Anwendung auf mehreren Kanälen verwenden möchte, benötigt er nur eine einzelne Instanz des Containers.  

**Abbildung 8** zeigt eine Übersicht der Chaincode-Installation:

![Blockchain-Netz](images/chaincode_install_overview.png "Chaincode-Installation")
*Abbildung 8. Übersicht der Chaincode-Installation*

* Wählen Sie über das Dropdown-Menü einen Peer aus, für den Chaincode installiert werden soll.  
* Klicken Sie auf der rechten Seite der Anzeige auf die Schaltfläche zur Chaincode-Installation; dadurch wird eine neue Anzeige geöffnet.

**Abbildung 9** zeigt das Fenster für die Chaincode-Installation:

![Blockchain-Netz](images/chaincode_install.png "Chaincode-Installation")
*Abbildung 9. Fenster der Chaincode-Installation*

* Füllen Sie die Felder für die Chaincode-ID und die Chaincode-Version aus. Beachten Sie dabei Benennungsschemas, da diese Zeichenfolgen in Client-Apps für die Interaktion mit bestimmten Chaincodes verwendet werden.
* Klicken Sie auf die Schaltfläche "Durchsuchen", um im lokalen Dateisystem zur Speicherposition der Chaincode-Quelle zu navigieren. Wählen Sie mindestens eine Datei aus, die für den Peer installiert werden soll. **Hinweis**: Es wird empfohlen, nur in Go oder Java geschriebenen Chaincode hochzuladen.  

Sobald ein Chaincode im Dateisystem eines Peers installiert wurde, muss er auf einem Kanal instanziiert werden. Bei dieser Instanziierung wird die Funktion `init` aufgerufen, um die erforderliche Initialisierung des Chaincodes durchzuführen. Dazu ist es häufig notwendig, die Schlüssel/Wert-Paare anzugeben, die den ursprünglichen World-Status eines Chaincodes umfassen.

**Abbildung 10** zeigt das Fenster für die Instanziierung des Chaincodes: 

![Blockchain-Netz](images/chaincode_instantiate.png "Chaincode-Instanziierung")
*Abbildung 10. Fenster für die Instanziierung des Chaincodes*

Beachten Sie, dass die Schlüssel/Wert-Paare mit der Zeichenfolge - `["a","b","200","250"]` - angegeben werden und in einem Fenster der Kanal für die Instanziierung ausgewählt werden kann. Dieses Beispiel zeigt einen Chaincode namens `end2end`, der auf `fabric-peer1a` installiert ist und auf einem Kanal namens `mychannel` instanziiert wird:

Die Kombination von Installation und Instanziierung ist eine leistungsfähig Funktion, da so ein Peer mit demselben Chaincode-Container auf mehreren Kanälen interagieren kann. Die einzige Voraussetzung ist, dass die eigentliche Chaincode-Quelle im Dateisystem des Peers installiert ist. Wenn nämlich ein Teil eines allgemeinen Chaincodes auf Dutzenden von Kanälen verwendet wird, würde ein Peer nur einen einzigen Chaincode-Container benötigen, um Lese-/Schreibvorgänge für alle Kanalkonten durchzuführen. Dieser einfache Ansatz ist für die Rechenleistung und den Durchsatz von Vorteil, da Netze skalieren und Chaincode-Anwendungen optimiert werden.    
