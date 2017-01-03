---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Was Sie wissen müssen
{: #etn_overview}
Letzte Aktualisierung: 10. November 2016
{: .last-updated}

**Achtung:** Lesen Sie vor Verwendung eines der Pläne von IBM Blockchain on Bluemix - also des Starter Developer-Plans (Betaversion) oder des High Security Business Network-Plans (allgemein verfügbar) - unbedingt die folgenden Informationen.
<br><br>

## IBM Support-Aussage

IBM ist seit langem führend in der Innovation und setzt dies mit den neuen Produktangeboten von IBM Blockchain fort. Die sich schnell weiterentwickelnde Blockchain-Technologie wird in einer Reihe von Branchen von der Finanzwirtschaft bis hin zur Logistik zu durchgreifenden Änderungen führen. Durch verschiedene Early-Adoption-Programme beeinflussen IBM Kunden und Business Partner bereits heute die künftige Entwicklung von Blockchain. IBM Blockchain on Bluemix ist eines dieser Programme. **Wie bei jeder neuen Technologie sollten sich Benutzer von IBM Blockchain on Bluemix auf eine rasche Abfolge von grundlegenden Änderungen einstellen**.  
{:shortdesc}

IBM Blockchain stützt sich auf die Architektur des Hyperledger Projects der Linux Foundation. Hyperledger Fabric ist ein Open-Source-Projekt, das sich gegenwärtig im *Incubation* genannten Entwicklungsstadium befindet. Jeder Beitrag der Open-Source-Community macht Hyperledger Fabric stabiler, kann jedoch im Hinblick auf die Akzeptanz eine Herausforderung darstellen. Während des Zyklus im Stadium *Incubation* können Kunden Hyperledger Fabric v0.6 für Netztests und -simulation verwenden. **IBM warnt jedoch vor der direkten Ausführung finanziell wertvoller Assets in einem Blockchain-Netz mit Hyperledger Fabric v0.6.**  
<br>

## Open-Source-Aussage

IBM Blockchain on Bluemix &mdash; sowohl der Starter Developer-Plan als auch der High Security Business Network-Plan verwendet den Open-Source-Code von Hyperledger Fabric v0.6.1 der Linux Foundation. Hyperledger Project-Mitglieder, einschließlich IBM, stellen für diese Struktur Code bereit; danach wird er von der Community überprüft, untersucht und getestet. Hyperledger Fabric v0.6.1 befindet sich gegenwärtig im Stadium *Incubation*; Details über das Stadium *Incubation* und den gesamten Lebenszyklus für das Hyperledger Project sind unter der Adresse https://github.com/hyperledger/hyperledger/wiki/Project-Lifecycle verfügbar.
<br><br>

## Support-Aussage für Chaincode

Von IBM Blockchain wird nicht deterministischer nicht Chaincode unterstützt, der für die Datenkonsistenz und Integrität in einem Blockchain-Netz ein Risiko darstellt. Lesen Sie vor der Bereitstellung von neuem Chaincode in Ihrem IBM Blockchain on Bluemix-Netz die Details unter [Nicht deterministischer Chaincode](nondeterministic.html).

Neben [nicht deterministischem Chaincode](nondeterministic.html) werden die folgenden Programmierpraktiken in IBM Blockchain-Netzen NICHT unterstützt:

1. Verwendung von assoziativen Feldgruppen mit Iteration (Reihenfolge ist in Go randomisiert).
2. Lesen einer Liste von Einträgen aus einer KVS-Tabelle (Reihenfolge ist nicht garantiert).
3. Schreiben von nicht threadsicherem Chaincode (Abfrage und Aufruf können parallel erfolgen).
4. Ersetzen von globalem Hauptspeicher oder Cachespeicher für Hauptbuchstatusvariablen im Chaincode.
5. Direkter Zugriff auf externe Services wie Datenbanken aus dem Chaincode.
6. Verwendung von Bibliotheken oder globalen Variablen, die zu Nichtdeterminismus führen könnten (z. B. "random" oder "time").
7. Iteration mit GetRows.  

Unterstützte Chaincode-Beispiele finden Sie in der Beispielbibliothek; das Verzeichnis enthält in Go und Java geschriebene Beispiele.
<br><br>

## Aspekte der Migration

Es gibt mehrere Programmierungsänderungen, die implementiert werden müssen, damit in Hyperledger Fabric v0.5-developer-preview entwickelter Code mit dem Bluemix-Back-End funktioniert (für Hyperledger Fabric v0.6.1 aufgebaut).  Weitere Details zu neuen Features und Codeänderungen finden Sie im Abschnitt [Aspekte der Migration](http://hyperledger-fabric.readthedocs.io/en/v0.6/v0.6_migration/) in der Dokumentation zu Hyperledger Fabric.  

## HSBN - Bekannte Probleme

1. Bei Verwendung von High Security Business Network, das mit Hyperledger Fabric v0.6.1 arbeitet, ist es empfehlenswert, das Netz während einer Entwicklungsphase regelmäßig zurückzusetzen, wenn es zu mehr als schätzungsweise fünfzig Chaincode-Bereitstellungen kam.  Durch das Zurücksetzen des Netzes werden bereitgestellter Chaincode sowie die erfassten Daten entfernt.  Das ist eine Gelegenheit, um älteren Chaincode zu entfernen, der durch Verbesserungen während einer iterativen Entwicklungsphase abgelöst wurde.  Während einer Entwicklungsnachphase muss die Anzahl der Chaincode-Bereitstellungen dann überwacht werden, damit Kapazität für den wichtigsten Chaincode übrig bleibt.
2. Vereinzelte Fehler des Typs "503 Service Unavailable" und "502 Bad Gateway" beim Durchführen einer Statusabfrage des Netzes und der Peers empfangen.
3. Mögliche Fehler des Typs "Server.Serve failed to complete security handshake" in den vp1-Protokollen. Dies ist kein schwerwiegender Fehler; er bezieht sich nicht auf die Netzoperation.
4. Die **Serviceberechtigungsnachweise** werden möglicherweise nicht von selbst ausgefüllt; generieren Sie die Berechtigungsnachweise in diesem Fall wie folgt:

 a) Klicken Sie im Service-Dashboard auf die Registerkarte **Serviceberechtigungsnachweise**:

  ![Serviceberechtigungsnachweise für HSBN](images/hsbn.png "Serviceberechtigungsnachweise für HSBN")

 b) Klicken Sie auf der Registerkarte **Serviceberechtigungsnachweise** auf die Schaltfläche **Neuer Berechtigungsnachweis**:

  ![Neuer Berechtigungsnachweis für HSBN](images/hsbn1.png "Neuer Berechtigungsnachweis für HSBN")

c) Es wird ein neues Fenster mit dem Titel **Neuen Berechtigungsnachweis hinzufügen** angezeigt; klicken Sie im unteren Bereich dieses Fensters auf die Schaltfläche **Hinzufügen**:

  ![Neuen Berechtigungsnachweis für HSBN hinzufügen](images/hsbn2.png "Neuen Berechtigungsnachweis für HSBN hinzufügen")

 d) Nun sollte Ihre Anzeige dem folgenden Beispiel ähneln. Wenn Sie auf **Berechtigungsnachweise anzeigen** klicken, werden JSON-Nutzdaten mit den Serviceberechtigungsnachweisen für Ihre HSBN-Instanz sichtbar.  

  ![Generierte Berechtigungsnachweise für HSBN](images/hsbn3.png "Generierte Berechtigungsnachweise")



## Hilfe anfordern

Wenn Sie Unterstützung und Hilfe für Ihr IBM Blockchain on Bluemix-Netz benötigen, lesen Sie die Informationen im Abschnitt [Support und bekannte Probleme](ibmblockchain_support.html).
