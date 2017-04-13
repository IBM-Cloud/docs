---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# High Security Business Network (HSBN) vNext Beta
{: #etn_overview}

Der **HSBN vNext Beta**-Service stellt eine Komplettlösung für die Erstellung eines Blockchain-Unternehmensnetzes dar. Er stellt Ihnen schnell das Netz bereit und bietet eine Überwachung für die einfache Verwaltung und Wartung Ihrer Ressourcen. Durch dieses einfache Entwerfen und Regeln von Netzen können Benutzer mehr Zeit und Augenmerk auf die Entwicklung und Bereitstellung von Geschäftslösungen richten.
{:shortdesc}

**HSBN vNext Beta**-Netze werden in einer Umgebung mit hoher Sicherheit unter LinuxONE ausgeführt, wo Netzressourcen (Peers, Anordnungsprogramme, Zertifizierungsstellen, Quellencode, Konto) alle in einem **IBM Secure Service Container** (SSC) enthalten sind. Zu den Funktionen zählen:
* Leistungsoptimierung für die Peer-to-Peer-Kommunikation
* Hohe Verfügbarkeit und Framework für Skalierbarkeit 
* Hardwareverschlüsselung, manipulationssichere Verschlüsselungsschlüssel und sicher verschlüsselte virtuelle Maschinen
* Sicheres Booten mit manipulationssicherer Software
* Kein Rootzugriff
* FIPS-Konformität, hoher EAL-Schutz, Überprüfbarkeit und Verschlüsselungsoptimierung

Eine Subskription für den **HSNB vNext Beta**-Plan umfasst die Unterstützung für die folgenden Netzressourcen:

- Fehlertoleranter Anordnungsservice
- Zwei Peers pro Mitglied
- Bis zu fünf zusätzliche Netzmitglieder
- Fünf instanziierte Chaincodes pro Mitglied
- Mitgliedsspezifische Zertifizierungsstelle
- Bis zu 100 Kanäle
- Standard-Governance-Richtlinien (alle Mitglieder sind Administratoren und können Einladungen zur Teilnahme am Netz ausgeben)

Weitere Details zu den Sicherheitsfunktionen der Umgebung finden Sie im Abschnitt [IBM Secure Service Container](etn_ssc.html).

## Verwendung des HSBN vNext Beta-Plans
{: #use_hsbn}

### Planzugriff

Der Zugriff auf den IBM Blockchain on Bluemix **HSBN vNext Beta**-Plan wird auf Anfrage erteilt. Wenn Sie HSBN vNext Beta aus dem Bluemix-Katalog auswählen und eine Serviceinstanz erstellen, wird Ihre Anfrage zur Teilnahme am aktuellen Beta-Release an das IBM Blockchain-Team gesendet. Sobald diese Anfrage genehmigt wurde, erhalten Sie eine E-Mail-Einladung für die Teilnahme an dem Plan; befolgen Sie die Anweisungen zum Starten des Dashboards des HSBN vNext Beta-Plans.

Wählen Sie auf dem HSBN vNext Beta-Dashboard eine der folgenden drei Optionen aus:
1. **Netzschnellstart**: Erstellen Sie ein HSBN vNext Beta-Netz und laden Sie andere Bluemix-Organisationen zur Teilnahme ein.
2. **Netz beitreten**: Zeigen Sie Einladungen für Sie für die Teilnahme an anderen HSBN vNext Beta-Netzen an.
3. **Netz überwachen**: Verwalten Sie Ihre Netzressourcen (Peers, Kanäle und Chaincode).

<!-- to do - the rest of this page final edit -->

### Beispielszenario

Angenommen, Sie sind ein Marmorhersteller und möchten das IBM Blockchain-Netz für Transaktionen mit unterschiedlichen Anbietern verwenden. Wie kann das funktionieren? Sie könnten einen Konsortium-Kanal erstellen, der alle Netzmitglieder und den aktuellen Status Ihres öffentlich verfügbaren Marmordepots enthält. Alle Transaktionen auf diesem Kanal sind für alle Mitglieder im Netz sichtbar und können entsprechend abgefragt werden. Sie könnten jedoch auch zu Datenschutz- und Vertraulichkeitszwecken "Unterkanäle" oder eigenständige Kanäle erstellen. Angenommen, Sie bieten einem bestimmten Anbieter einen besseren Preis, wenn dieser bestimmte Bedingungen erfüllt. Diese Transaktion kann auf einem Unterkanal durchgeführt werden, wobei die daraus resultierenden Auswirkungen auf Ihren Mamorgesamtbestand sich auf dem Konsortium-Kanal widerspiegeln. Oder Sie möchten mit einer bestimmten Art von Marmor handeln, die noch nicht mal auf dem Konsortium-Kanal verfügbar ist. Dazu würden Sie die entsprechende Transaktion einfach mit der entsprechenden Partei über einen eigenständigen Kanal abwickeln, was keinerlei Auswirkungen auf das Konto des Konsortium-Kanals hätte. Kanäle stellen einen leistungsfähigen Mechanismus für den Datenschutz dar, da sie alle über eindeutige Konten verfügen und nur Mitglieder, die für einen Kanal subskribiert und authentifiziert sind, mit dem Konto interagieren können.  

### Netz erstellen
{: create_a_network}
Das Netz besteht aus den folgenden Komponenten:
* Einem Anordnungsservice, mit dem Transaktionen authentifiziert und diese in Blöcken für die Konten von Kanälen angeordnet werden.
* Einer mitgliedsspezifischen Zertifizierungsstelle, die Identitätsmaterialien für die Netzkomponenten der einzelnen Mitglieder ausgibt.
* Mitgliedsspezifischen Peers, die Transaktionen ausführen und festschreiben und ein Kanalkonto verwalten.

Klicken Sie auf dem Dashboard des Blockchain-Service auf die Schaltfläche **Netzschnellstart** und befolgen Sie die Anweisungen des Assistenten:
1. Geben Sie auf der Seite **Netz benennen** den Namen des Blackchain-Netzes und den Namen des Unternehmens ein, die Ihre Mitgliedsindentität darstellen, und klicken Sie dann auf **Weiter**.
2. Geben Sie auf der nächsten Seite **Mitglieder einladen** die entsprechenden Organisationsinformationen für die Teilnehmer ein, die Sie einladen möchten. Jedem Teilnehmer wird beim Beitritt zum Netz ein Peer und eine Zertifizierungstelle bereitgestellt und alle Netzmitglieder verwalten ein Konto für die Kanäle, denen sie beigetreten sind.<br>
   **Hinweis:** Sie können höchstens fünf Mitglieder für das Netz einladen.
3. Auf der Seite **Governanceregeln definieren** werden die Einstellungen für die Netzrichtlinien angezeigt. Standardmäßig kann jeder Teilnehmer im Netz Kanäle erstellen und Mitglieder einladen.  
4. Verwenden Sie auf der Seite **Zertifikat generieren** die Option **Automatisch generiert**, um die Zertifikate für die Netzkomponenten Ihrer Organisation zu erstellen. Diese x509-Zertifikate sind für die Benutzer nicht zugänglich.  
5. Überprüfen Sie abschließend auf der Seite **Zusammenfassung überprüfen** die Konfiguration für das Netz und klicken Sie auf **Fertig**, um das Netz zu booten.

Mit diesem Prozess ist die Ersteinrichtung Ihres Netzes abgeschlossen.

### Netz beitreten
{: invite_members}

Nachdem das Netz initialisiert wurde, erhalten die Einladungsempfänger eine E-Mail, die das Netz für den Beitritt sowie entsprechende Anweisungen dazu enthält. Auf dem Dashboard des HSBN vNext-Plans ist die Schaltfläche **Anstehende Einladungen** aktiviert. Klicken Sie auf die Schaltfläche, um dem Netz beizutreten:

1. Wählen Sie das Netz in der Liste aus und klicken Sie auf **Netz beitreten**.
2. Überprüfen Sie in der nächsten Anzeige die Governanceregeln und klicken Sie auf **Weiter**.
3. Geben Sie auf der Seite **Zertifikat generieren** den Namen Ihrer Organisation ein und wählen Sie dann die Option **Automatisch generiert** aus.
4. Überprüfen Sie auf der Seite **Netzzusammenfassung überprüfen** die Einstellungen des Netzes und klicken Sie auf **Fertig**. In den Einstellungen werden auch die eingeladenen Teilnehmer angezeigt, die Einladungen für den Beitritt zum Netz erhalten haben.

Anweisungen zum Erstellen von Kanälen und zum Installieren/Instanziieren von Chaincode finden Sie im Abschnitt [Überwachung](v10_dashboard.html).

<!-- I think all of this is adequately covered in the Monitor Section; and we already tell the story in the Sample Scenario topic above -->


<!-- From Jeff: Agreed. Commenting out all the rest sections on the page.


### Creating new channels
{: prepare_private_channels}

With the latest HSBN vNext plan, you can create a private channel, install a customized chaincode, complete the trade, and update the inventory number upon the other parties in the network make a query or propose a new transaction.

1. On the HSBN vNext plan dashboard, select **Enter Monitor**.
2. Select **Channels**, and click **New Channel**.
3. On the **Create a Channel** page, enter the channel name and choose the company that you want to make trade with by adding members. Then, click **Create** to create another private consortium channel.
4. Select **Chaincode** after you click the **Enter Monitor** button on the dashboard. You can view the chaincode that are already installed on your peer, or install a new chaincode to the peer.<br>
  **Note:** You can install at most 5 chaincode apps per peer.
5. Click **Install Chaincode** to install the smart contract to the peer. A smart contract, also known as chaincode, is the programmatic code installed and instantiated onto a channel’s peers by an appropriately authorized member. End users then invoke chaincode through a client-side application that interfaces with a network peer. Chaincode runs network transactions, which if validated, are appended to the shared ledger and modify world state. Chaincode can be developed for business contracts, asset definitions, and collectively-managed decentralized applications. You can download [this sample code](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window} to your local environment for testing.

**Note:** After you install the chaincode onto the peer, you must instantiate the chaincode by providing the initial arguments. In the case of the Marbles sample chaincode, you can input `marble1, blue, 35` in a comma separated list to indicate that you have 35 blue marble1 for trade.


### Commencing transactions
{: commence_txs}

To make transactions within your network, the trading parties must:
* Join the same channel within the network.
* Install the same version of the chaincode onto the peer that represents each organization.


Each successful transaction results in a new block appended to the blockchain, and the ledger in the levelDB updated with the new state. Other members in the network can query the ledger or the transaction history to decide the next transaction.



### Monitoring your network
{: monitor_network}

You can perform the following tasks after you click the **Enter Monitor** button on the dashboard:
* Create new channels and invite other members to join your channels to trade privately.
* Install new chaincodes to your peer to initiate or participate into new trade.
* View the changes of blocks, transactions, chaincode invocations.
* View the log on your peer.
* View the information of resources that your organization owns.
* Export a JSON file containing the low-level networking information for each of your components (such as enrollID/enrollSecret for your CA).  

See the [HSBN vNext Beta dashboard](v10_dashboard.md) for more information about the usage of each panel on the dashboard. 


-->
