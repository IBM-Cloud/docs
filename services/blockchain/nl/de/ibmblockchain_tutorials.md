---

copyright:
  years: 2016
lastupdated: "2016-11-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Beispielapps und Lernprogramme
{: #1stanchor}


In den folgenden Beispielen wird veranschaulicht, wie Anwendungen und Chaincode in einem IBM Blockchain-Testnetz funktionieren. Weitere Informationen zum Hyperledger Fabric v0.6-Code, der als Grundlage für IBM Blockchain-Netze verwendet wird, finden Sie in der [Fabric-Dokumentation](https://github.com/hyperledger/fabric/tree/v0.6/docs) des Hyperledger Projects der Linux Foundation.  
{:shortdesc}

Wenn Sie praktische Erfahrungen mit Chaincode-Anwendungen sammeln möchten, können Sie hierfür sofort eines der nachfolgend aufgeführten Demos für Marbles, Wertpapiere oder Autoleasing verwenden (klicken Sie auf die Schaltfläche 'In Bluemix bereitstellen'). Alternativ können Sie mit dem Lesen fortfahren, um das Lernprogramm zur Einführung in Chaincode durchzuarbeiten.

- [![In Bluemix bereitstellen](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  **Marbles**
- [![In Bluemix bereitstellen](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  **Wertpapier**
- [![In Bluemix bereitstellen](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  **Autoleasing**  

<br>
## Lernprogramm zum Kennenlernen von Chaincode
{: #hellocc}
Dieses Lernprogramm führt Sie durch die Verwendung der Grundbausteine zum Codieren der Grundlagen einer Chaincode-Anwendung. Sie erstellen nach und nach einen funktionierenden Chaincode, von dem generische Assets für den Austausch in einem Netz erstellt werden. Danach interagieren Sie mit dem Chaincode über die Netz-API. Nach Abschluss dieses Lernprogramms können Sie die folgenden Fragen beantworten:
- Was ist ein Chaincode?
- Wie implementiere ich Chaincode?
- Welche Abhängigkeiten gibt es?
- Was sind die wichtigsten Funktionen?
- Wie übergeben ich unterschiedliche Werte an die Argumente?
- Wie trage ich einen Benutzer sicher in meinem Netz ein?
- Wie kompiliere ich den Chaincode?
- Wie interagiere ich mit dem Chaincode über die REST-API?

### Was ist ein Chaincode?
Chaincode ist ein Go- (bzw. Golang-) oder Java-Code, der den Benutzern das Interagieren mit einem Blockchain-Netz ermöglicht. Wenn Sie eine Transaktion im Netz 'aufrufen', rufen Sie eine Funktion im Chaincode auf, durch die Werte im Hauptbuch gelesen und geschrieben werden.  

<br>
## Entwicklungsumgebung einrichten
Um mit der Entwicklung von Chaincode zu beginnen, müssen Sie zuerst die folgenden Abhängigkeiten und empfohlenen Tools installieren:

### Git

- [Git-Downloadseite](https://git-scm.com/downloads)
- [Pro Git-Handbuch](https://git-scm.com/book/en/v2)
- [Git-Desktop (eine Alternative zur Git-CLI)](https://desktop.github.com/)

Git ist ein schnelles und leistungsfähiges Tool zur Versionssteuerung für die Chaincode-Entwicklung sowie für die Softwareentwicklung im Allgemeinen. Git Bash ist das empfohlene Befehlszeilenterminal; es wird mit Git for Windows installiert.

Überprüfen Sie nach den Git-Installationen, ob Git tatsächlich installiert ist:

```
$ git version
git version 2.9.0.windows.1
```

Sobald Sie Git installiert haben, erstellen Sie für sich selbst ein Konto in [GitHub](https://github.com/). Für den IBM Blockchain-Service in Bluemix muss sich Chaincode für die Bereitstellung über die REST-API in einem GitHub-Repository befinden.  

## Go

Go ist derzeit die einzige unterstützte Sprache zum Schreiben von Chaincode in Bluemix. Die Go-Installation umfasst eine Reihe nützlicher CLI-Tools zum Schreiben von Chaincode. Sie können beispielsweise mit dem Befehl `go build` Ihren Chaincode kompilieren, bevor Sie versuchen, ihn in einem Netz bereitzustellen. Installieren Sie Go v1.6; dies ist die für die Entwicklung von Hyperledger Fabric v0.6 verwendete Version:  

- [Go 1.6-Installation](https://golang.org/dl/#go1.6.3)
- [Go-Installationsanweisungen](https://golang.org/doc/install)
- [Go-Dokumentation und -Lernprogramme](https://golang.org/doc/)

Überprüfen Sie durch Ausführen der folgenden Befehle, ob Go ordnungsgemäß installiert wurde. Die Ausgabe des Befehls `go version` kann in Abhängigkeit von Ihrem Betriebssystem variieren:

```
$ go version
go version go1.6.3 windows/amd64

$ echo $GOPATH
C:\gopath
```

Ihre Umgebungsvariable `GOPATH` muss nicht mit dem vorherigen Beispiel übereinstimmen, doch Sie müssen ein gültiges Verzeichnis auf Ihrem Dateisystem verwenden. Wenn Sie `go build` ausführen, um zu prüfen, ob Ihr Chaincode kompiliert wird, sucht Go im Verzeichnis `$GOPATH/src` nach sämtlichen Nicht-Standardabhängigkeiten, die Sie im Block `import` Ihres Chaincodes auflisten. Die [Go-Installationsanweisungen](https://golang.org/doc/install) führen Sie durch die Einrichtung der Umgebungsvariablen GOPATH.  

<br>
## Hyperledger Fabric

Für Blockchain on Bluemix werden zwei Versionen von Hyperledger Fabric unterstützt: v0.5 und v0.6.  Wie unten beschrieben, muss Ihre Chaincode-Version zur Version von Hyperledger in Ihrem Bluemix-Netz passen.

Achtung:
1. Zur Aktivierung der Lese- und Schreibfunktionen für das Ledger muss Ihr Chaincode das Chaincode-Shim aus Hyperledger Fabric importieren.
2. Zur lokalen Kompilierung Ihres Chaincodes muss die Hyperledger Fabric-Codeposition in Ihrer Umgebungsvariablen `GOPATH` angegeben sein.

Um festzustellen, welche Version von Hyperledger Fabric auf Ihrer Bluemix-Instanz ausgeführt wird, müssen Sie in Ihrem Dashboad-Monitor auf die Registerkarte **Servicestatus** klicken.  Blättern Sie zum Abschnitt mit den **Releaseinformationen**; im Fenster `Vom Netz wird diese Version verwendet` wird die **Hyperledger-COMMIT-Stufe** angezeigt, auf der die Ausführung stattfindet:

![Bluemix-Back-End-Version](images/fabricversion.png "Bluemix-Back-End-Version")
Abbildung 1. Hyperledger Fabric-Version

Ihre Chaincode-Version muss zur Version von Hyperledger Fabric passen, für die Sie Ihren Chaincode bereitstellen. Beispiel: Für das in Abbildung 1 dargestellte Netz ist ein Klonen der Hyperledger Fabric v0.6-Voranzeigecodebasis erforderlich. Die Fabric-Codebasis muss für jede Version in Ihrem Pfad `$GOPATH/hyperledger/fabric` gespeichert werden:

- [v0.5 Hyperledger Fabric](https://github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview)
- [v0.6 Hyperledger Fabric](https://gerrit.hyperledger.org/r/gitweb?p=fabric.git;a=shortlog;h=refs/heads/v0.6)

Verwenden Sie für die Installation der Hyperledger Fabric v0.5-Codebasis den folgenden Befehl des Typs 'git clone':

```
# Create the parent directories on your GOPATH
mkdir -p $GOPATH/src/github.com/hyperledger
cd $GOAPTH/src/github.com/hyperledger

# Clone the appropriate release codebase into $GOPATH/src/github.com/hyperledger/fabric
# Note that the v0.5 release is a branch of the repository.  It is defined below after the -b argument
git clone -b v0.5-developer-preview https://github.com/hyperledger-archives/fabric.git
```

Verwenden Sie für die Installation der Hyperledger Fabric v0.6-Codebasis den folgenden Befehl des Typs 'git clone':

```
# The v0.6 release exists as a branch inside the Gerrit fabric repository
git clone -b v0.6 http://gerrit.hyperledger.org/r/fabric
```

Wenn das Fabric in Ihrem `GOPATH` nicht ordnungsgemäß installiert ist, wird bei der Erstellung Ihres Chaincodes ein Fehler ähnlich wie im folgenden Beispiel zurückgegeben:
```
$ go build .
chaincode_example02.go:27:2: cannot find package "github.com/hyperledger/fabric/core/chaincode/shim" in any of:
        C:\Go\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOROOT)
        C:\gopath\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOPATH)
```

### Eigene Entwicklungspipeline einrichten

Führen Sie die folgenden Schritte aus, um eine Pipeline zum Schreiben, Aufbauen und Testen Ihres Chaincodes einzurichten. Sie schreiben Chaincode auf Ihrer lokalen Maschine, überprüfen dessen Kompilierung und laden ihn nach GitHub hoch. Anschließend stellen Sie Ihren Chaincode in Ihrem Bluemix-Netz bereit und testen ihn dort, und zwar mithilfe der Fabric-REST-API:

1. Verzweigen Sie die entsprechende Version des Repositorys [learn chaincode](https://github.com/IBM-Blockchain/learn-chaincode) für Ihre Netzversion für Ihr GitHub-Konto. Verzweigen Sie v1.0 für ein v0.5-Fabric-Netz oder v2.0 für ein v0.6-Fabric-Netz. Eine Option ist die Verwendung der Schaltfläche **Verzweigen**, die sich auf der Repository-Seite rechts oben befindet. Durch die Verzweigung wird das gesamte Repository auf Ihre lokale Maschine kopiert, einschließlich aller Zweige, die durch Klicken auf die Schaltfläche für die Verzweigung links oben auf der Seite angezeigt werden. Für die Durchführung der Verzweigung mit der CLI müssen Sie die folgenden Befehle in Ihre Git-Bash-Shell eingeben:

2. Klonen Sie Ihre Verzweigung in Ihren $GOPATH:

  ```bash
  cd $GOPATH
  mkdir -p src/github.com/<YOUR_GITHUB_ID_HERE>/
  cd src/github.com/<YOUR_GITHUB_ID_HERE>/
  git clone -b v1.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  OR
  git clone -b v2.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  ```

  Sie haben auf Ihrer lokalen Maschine nun eine Kopie Ihrer Verzweigung. Sie schreiben Chaincode durch Ändern oder Hinzufügen lokaler Dateien, durch Übermitteln dieser Dateien per Push-Operation an Ihre GitHub-Verzweigung und durch anschließendes Bereitstellen Ihres Chaincodes in Ihrem Blockchain-Netz, und zwar mittels Verwendung der REST-API in einem gleichgeordneten Netz.

3. Es werden zwei Versionen des Chaincodes bereitgestellt, die in diesem Lernprogramm verwendet werden: **start** ist das Chaincode-Gerüst zum Starten und **finished* ist Ihr beendeter Chaincode, der für die Erstellung bereitsteht. Stellen Sie zunächst sicher, dass mit **start** der Aufbau in Ihrer lokalen Umgebung stattfindet:

  ```bash
  cd $GOPATH/src/github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/start
  go build ./
  ```

Die **start**-Version von learn-chaincode muss ohne Fehler oder Nachrichten kompiliert werden. Falls dies nicht der Fall ist, lesen Sie noch einmal die oben stehenden Anweisungen zur ordnungsgemäßen Installation von Go.

5. Schreiben Sie Änderungen an Ihren lokalen Chaincode-Dateien und übermitteln Sie die aktualisierten Dateien per Push-Operation an Ihre GitHub-Verzweigung:

  ```bash
  cd $GOPATH/src/github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/
  # See what files have changed locally.  You should see chaincode_start.go
  git status
  # Stage all changes in the local repository for commit
  git add --all
  # Commit all staged changes.  Insert a short description after the -m argument
  git commit -m "Compiled my code"
  # Push local commits back to https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/
  git push
  ```

#### Chaincode-Schnittstelle implementieren
Im nächsten Schritt wird die Chaincode-Shim-Schnittstelle in den Go-Code implementiert. Die drei wichtigsten Funktionen sind **Initialisieren**, **Aufrufen** und **Abfragen**. Für alle drei Funktionen werden ein Funktionsname und eine Reihe an Zeichenfolgen als Eingabe verwendet, der Zeitpunkt ihres Aufrufs ist jedoch unterschiedlich. Ihr Entwicklungspfad endet mit einem funktionierenden Chaincode, von dem generische Assets für den Austausch in einem Blockchain-Netz erstellt werden.

### Abhängigkeiten
Mit der Anweisung `import` werden die Abhängigkeiten für die Erstellung Ihres Chaincodes aufgeführt:
1. `fmt` - enthält `Println` zur Fehlerbehebung/Protokollierung.
2. `errors` - Standardformat für Go-Fehler.
3. `github.com/hyperledger/fabric/core/chaincode/shim` - Code, der eine Schnittstelle zum Golang-Code mit einem Netzpeer darstellt.

#### Init()
Die Funktion `Init` wird aufgerufen, wenn Sie Ihren Chaincode zum ersten Mal bereitstellen. Der Name impliziert bereits, dass Sie diese Funktion zum Initialisieren Ihres Chaincodes verwenden müssen. In diesem Beispiel wird mit `Init` der Anfangsstatus eines einzelnen Schlüssel/Wert-Paares für das Ledger konfiguriert.

Ändern Sie in der Datei `chaincode_start.go` die Funktion `Init` so, dass von ihr das erste `args`-Element für den Schlüssel "hello_world" gespeichert wird:

```go
func (t *SimpleChaincode) Init(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
	if len(args) != 1 {
		return nil, errors.New("Incorrect number of arguments. Expecting 1")
	}

	err := stub.PutState("hello_world", []byte(args[0]))
	if err != nil {
		return nil, err
	}

	return nil, nil
}
```

Hierfür wird die Stubfunktion `stub.PutState` verwendet. Diese Funktion interpretiert das erste in der Bereitstellungsanforderung gesendete Argument als Wert, der im Schlüssel 'hello_world' gespeichert werden soll. Falls ein Fehler auftritt, weil die falsche Anzahl an Argumenten übergeben wurde oder weil es beim Schreiben in das Ledger zu einem Problem kam, gibt diese Funktion einen Fehler zurück. Ohne Fehler wird sie ordnungsgemäß beendet und es werden keine Nachrichten zurückgegeben.  

#### Invoke()
Verwenden Sie die Funktion `Invoke`, um Chaincode-Funktionen für die Ausführung echter Arbeitsschritte im Blockchain-Netz aufzurufen. Aufruffunktionen werden als Transaktionen erfasst, die zum Schreiben in das Ledger in Blöcken zusammengefasst werden. Die Ledgeraktualisierung wird durch Aufrufen Ihres Chaincodes erreicht. Die Struktur von `Invoke` ist einfach; sie empfängt eine Funktion und ein Array von Argumenten. Auf Basis der vom Funktionsparameter in der Aufrufanforderung übergebenen Funktion ruft `Invoke` entweder eine Helper-Funktion auf oder gibt einen Fehler zurück.

Ändern Sie in der Datei `chaincode_start.go` die Funktion `Invoke` so, dass eine generische Schreibfunktion aufgerufen wird:

```go
func (t *SimpleChaincode) Invoke(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
	fmt.Println("invoke is running " + function)

	// Handle different functions
	if function == "init" {
		return t.Init(stub, "init", args)
	} else if function == "write" {
		return t.write(stub, args)
	}
	fmt.Println("invoke did not find func: " + function)

	return nil, errors.New("Received unknown function invocation")
}
```

Vom Code wird jetzt nach `write` gesucht; fügen Sie die Schreibfunktion daher zur Datei `chaincode_start.go` hinzu:

```go
func (t *SimpleChaincode) write(stub shim.ChaincodeStubInterface, args []string) ([]byte, error) {
	var name, value string
	var err error
	fmt.Println("running write()")

	if len(args) != 2 {
		return nil, errors.New("Incorrect number of arguments. Expecting 2. name of the variable and value to set")
	}

	name = args[0]                            //rename for fun
	value = args[1]
	err = stub.PutState(name, []byte(value))  //write the variable into the chaincode state
	if err != nil {
		return nil, err
	}
	return nil, nil
}
```

Diese Funktion `write` muss der vorherigen Änderung von `Init` ähneln. Sie können jetzt Schlüssel und Wert für `PutState` festlegen, was Ihnen das Speichern eines beliebigen Schlüssel/Wertpaares im Blockchain-Hauptbuch ermöglicht.

#### Query()
Die Funktion `Query` wird zum Abfragen des Chaincode-Status aufgerufen; hierbei werden keine Blöcke zur Chain (Ledger) hinzugefügt. Nur bei Verwendung der Funktionen zum Bereitstellen und Aufrufen werden neue Blöcke hinzugefügt. Verwenden Sie `Query` zum Lesen des Werts der Schlüssel/Wertpaare des Chaincode-Status.

Ändern Sie in der Datei `chaincode_start.go` die Funktion `Query` so, dass von ihr eine generische Lesefunktion aufgerufen wird:

```go
func (t *SimpleChaincode) Query(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
	fmt.Println("query is running " + function)

	// Handle different functions
	if function == "read" {                            //read a variable
		return t.read(stub, args)
	}
	fmt.Println("query did not find func: " + function)

	return nil, errors.New("Received unknown function query")
}
```

Vom Code wird jetzt nach `read` gesucht; fügen Sie daher die Lesefunktion zur Datei `chaincode_start.go` hinzu:

```go
func (t *SimpleChaincode) read(stub shim.ChaincodeStubInterface, args []string) ([]byte, error) {
	var name, jsonResp string
	var err error

	if len(args) != 1 {
		return nil, errors.New("Incorrect number of arguments. Expecting name of the var to query")
	}

	name = args[0]
	valAsbytes, err := stub.GetState(name)
	if err != nil {
		jsonResp = "{\"Error\":\"Failed to get state for " + name + "\"}"
		return nil, errors.New(jsonResp)
	}

	return valAsbytes, nil
}
```

Von dieser Funktion `read` wird `GetState` verwendet, das Komplement für `PutState`. Von dieser Shim-Funktion wird nur ein einziges Zeichenfolgeargument akzeptiert, das für den Namen des abzurufenden Schlüssels verwendet wird. Danach wird von dieser Funktion der Wert als Array aus Bytes an `Query` zurückgegeben, anschließend wird der Wert an den REST-Handler weitergesendet.

#### Main()
Die Funktion `main` wird ausgeführt, wenn von jedem Peer seine Instanz des Chaincodes bereitgestellt wird. Von ihr wird der Chaincode gestartet und beim Peer registriert. Für 'main' sind keine Codeaktualisierung erforderlich; sowohl in 'chaincode_start.go' als auch in 'chaincode_finished.go' ist eine Funktion des Typs `main` ganz oben in jeder Datei enthalten:

```go
func main() {
	err := shim.Start(new(SimpleChaincode))
	if err != nil {
		fmt.Printf("Error starting Simple chaincode: %s", err)
	}
}
```

### Mit Chaincode interagieren
Die schnellste Möglichkeit zum Testen des Chaincodes ist die Verwendung der REST-Schnittstelle der Peers.
In der Swagger-Benutzerschnittstelle in der Bluemix-Dashboard-Überwachung können Sie mit dem Bereitstellen von Chaincode experimentieren, ohne zusätzlichen Code zu schreiben.  

#### Swagger-API
Führen Sie die folgenden Schritte aus, um die Swagger-API zu verwenden:

1. Melden Sie sich an [Bluemix](https://console.ng.bluemix.net/login) an und stellen Sie sicher, dass Sie sich in der Registerkarte **Dashboard** befinden.
1. Stellen Sie sicher, dass Sie sich in dem Bluemix-Bereich befinden, in dem Ihr IBM Blockchain-Service enthalten ist. Die Navigation für den Bereich befindet sich auf der linken Seite.
1. Unten befindet sich die Anzeige **Services**; klicken Sie auf Ihren IBM Blockchain-Service.
1. Daraufhin sollte die Nachricht "Willkommen beim IBM Blockchain-Service" angezeigt werden; klicken Sie auf der rechten Seite auf **STARTEN**.
1. Auf der Seite für die Überwachung sollten zwei Tabellen angezeigt werden; die untere Tabelle kann leer sein.
	- **Registerkarte 'Netz':**
		- **Peer-Protokolle** sind in der oberen Tabelle. Klicken Sie in der Zeile für **Peer 1** auf das Dateisymbol, um das Protokoll anzuzeigen. Zusätzlich zu dieser statischen Anzeige sind zeitnahe **Streaming-Peer-Protokolle** in der Registerkarte **Protokolle anzeigen** oben auf der Seite enthalten.
		- **Chaincode-Protokolle** sind in der unteren Tabelle. Jeder Chaincode ist mit dem Chaincode-Hashwert gekennzeichnet, der bei seiner Bereitstellung zurückgegeben wurde. Wählen Sie den Peer in der Chaincode-Zeile aus und klicken Sie auf das Dateisymbol, um das Protokoll anzuzeigen.
	- **Registerkarte 'APIs':** Zeigt die Dokumentationsseite für die Swagger-API an.
1. Fahren Sie mit den folgenden Schritten zum Implementieren der sicheren Eintragung fort. Für Aufrufe des Endpunkts `/chaincode` in der REST-Schnittstelle ist eine sichere Kontext-ID erforderlich. Die meisten REST-Aufrufe werden nur akzeptiert, wenn Sie eine registrierte *enrollID* aus der Liste der Serviceberechtigungsnachweise übergeben:
  - Klicken Sie auf **+ Eintragungskennungen des Netzes**, um die Liste der *enrollID*-Werte und ihre geheimen Schlüssel zu erweitern.
  - Kopieren Sie die Berechtigungsnachweise zur späteren Verwendung in eine Textdatei.
  - Erweitern Sie den API-Abschnitt **Registrator**.
  - Erweitern Sie den Abschnitt `POST /registrar`.
  - Füllen Sie das Feld `Wert` mit dem JSON-Wert, von dem `enrollID` und 'enrollSecret' aus den Berechtigungsnachweise angegeben wird:

  ![Registrierungsbeispiel](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/registrar.PNG "Register example")

  Der *Antworthauptteil* muss wie das folgende Beispiel aussehen:

  ![Registrierungsbeispiel](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/register_response.PNG "Antworthauptteil für Registrierungsbeispiel")

Jetzt haben Sie eine `enrollID` konfiguriert, die Sie zum Bereitstellen, Aufrufen und Abfragen des Chaincodes in den folgenden Schritten verwenden können.
### Chaincode implementieren
Damit Sie den Chaincode über die REST-Schnittstelle bereitstellen können, muss der Chaincode in einem öffentlichen GitHub-Repository gespeichert sein. Wenn Sie eine Bereitstellungsanforderung an einen Peer senden, geben Sie die URL für das Chaincode-Repository sowie die Parameter zum Initialisieren des Chaincodes an.

Stellen Sie **vor dem Bereitstellen** des Chaincodes sicher, dass er lokal erstellt wird:
1. Öffnen Sie eine Eingabeaufforderung und navigieren Sie zu dem Verzeichnis, in dem `chaincode_start.go` enthalten ist. Geben Sie den folgenden Befehl ein:
	```
	go build ./
	```
1. Erweitern Sie den API-Abschnitt **Chaincode**.
1. Erweitern Sie den Abschnitt `POST /chaincode`.
1. Füllen Sie das Textfeld `DeploySpec` mit dem nachfolgenden Beispielcode (leeren Sie alle anderen Felder); geben Sie den Pfad zum Chaincode-Repository und die `enrollID` aus dem vorherigen Schritt für `/registrar` an. Der Wert für `"path":` sollte dem folgenden ähneln: `"https://github.com/johndoe/learn-chaincode/finished"`. Hierbei handelt es sich um den Pfad zur Repositoryverzweigung und den Pfad zur Datei 'chaincode_finished.go':

	```
	{
		"jsonrpc": "2.0",
		"method": "deploy",
		"params": {
			"type": 1,
			"chaincodeID": {
				"path": "https://github.com/ibm-blockchain/learn-chaincode/finished"
			},
			"ctorMsg": {
				"function": "init",
				"args": [
					"hi there"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 1
	}
	```

  Der *Antworthauptteil* muss ähnlich wie das folgende Beispiel aussehen:

  ![Bereitstellungsbeispiel](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/deploy_response.PNG "Antworthauptteil für Bereitstellungsbeispiel")

  Die Antwort auf die Bereitstellung enthält die ID für diesen Chaincode. Die ID ist ein aus 128 Zeichen bestehender alphanumerischer Hashwert, den Sie für zukünftige Aufruf- und Abfrageanforderungen verwenden können. Kopieren Sie diese ID in einen Texteditor.

#### Abfragen (query)
Fragen Sie den Chaincode für den Wert des Schlüssels `hello_world` ab, den Sie mit der Funktion `Init` festlegen:
1. Erweitern Sie den API-Abschnitt **Chaincode**.
1. Erweitern Sie den Abschnitt `POST /chaincode`.
1. Füllen Sie das Textfeld `QuerySpec` mit dem nachfolgenden Beispielcode (leeren Sie alle anderen Felder); geben Sie die Chaincode-ID aus dem vorherigen Bereitstellungsschritt und die `enrollID` aus dem vorherigen Schritt für `/registrar` an:

	```
	{
		"jsonrpc": "2.0",
		"method": "query",
		"params": {
			"type": 1,
			"chaincodeID": {
				"name": "CHAINCODE_HASH_HERE"
			},
			"ctorMsg": {
				"function": "read",
				"args": [
					"hello_world"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 2
	}
	```
  Der 'Antworthauptteil' sollte dem folgenden Beispiel ähneln:

  ![Abfragebeispiel](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query_response.PNG "Antworthauptteil für Abfragebeispiel")

  Der Wert von `hello_world` lautet 'hi there'; er wurde im Hauptteil des vorherigen Bereitstellungsaufrufs eingestellt.

#### Aufrufen (invoke)
Rufen Sie die generische Schreibfunkton mit `invoke` auf. Ändern Sie den Wert für `hello_world` in 'go away':
1. Erweitern Sie den API-Abschnitt **Chaincode**.
1. Erweitern Sie den Abschnitt `POST /chaincode`.
1. Füllen Sie das Textfeld `InvokeSpec` mit dem nachfolgenden Beispielcode (leeren Sie alle anderen Felder); geben Sie die Chaincode-ID aus dem vorherigen Bereitstellungsschritt und die `enrollID` aus dem vorherigen Schritt für `/registrar` an:

	```
	{
		"jsonrpc": "2.0",
		"method": "invoke",
		"params": {
			"type": 1,
			"chaincodeID": {
				"name": "CHAINCODE_HASH_HERE"
			},
			"ctorMsg": {
				"function": "write",
				"args": [
					"hello_world",
					"go away"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 3
	}
	```
  Der 'Antworthauptteil' sollte dem folgenden Beispiel ähneln:

  ![Aufrufbeispiel](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/invoke_response.PNG "Antworthauptteil für Aufrufbeispiel")

  Führen Sie die obige Abfrage erneut aus; daraufhin sollte die folgende Antwort zurückgegeben werden:

  ![Abfragebeispiel2](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query2_response.PNG "Antwort für Aufrufbeispiel")

Damit ist das Schreiben des Basis-Chaincodes abgeschlossen.  

<br>
## Voraussetzungen für Demos
{: #requirements}

Die folgenden Voraussetzungen, die im Lieferumfang Ihres Bluemix-Service enthalten sind, sind für die Ausführung der Demoanwendungen 'Marbles', 'Commercial Paper' und 'Car Lease' erforderlich. Von der Bluemix-Umgebung wird Hyperledger Fabric zum Bereitstellen dieser Abhängigkeiten geklont:

- Bluemix-ID https://console.ng.bluemix.net/ (erforderlich zum Erstellen des IBM Blockchain-Netzes und Bereitstellen der Serviceberechtigungsnachweise für Peer und die Zertifizierungsstelle)
- Node.js 0.12.0 oder höher und npm Version 2 oder höher
- Golang-Umgebung (nur zum Erstellen eines eigenen Chaincodes erforderlich)

Für die Demos sind außerdem Kenntnisse im Umgang mit Node.js und dem Expressmodul erforderlich. Außerdem ist ein konzeptionelles Verständnis der Begriffe 'Chaincode', 'Hauptbuch' und 'Peer' im Blockchain-Kontext nötig; Informationen hierzu finden Sie im [Hyperledger Fabric-Glossar](https://github.com/hyperledger/fabric/blob/v0.6/docs/glossary.md).  

<br>
## Marbles-Demo
{: #marbles}

Anhand der Marbles-Anwendung wird ein einfacher Assettransfer zwischen zwei Parteien veranschaulicht. Die Anwendung ist dazu konzipiert, das JavaScript-SDK zu testen, die Entwicklung zu unterstützen und den Entwicklern dabei zu helfen, sich mit dem SDK und Chaincode vertraut zu machen.

In den [Marbles-Lernprogrammen](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md) können Sie sich damit vertraut machen, wie die Webanwendung, das SDK und der Chaincode zusammenarbeiten. Wenn Sie bereits mit Chaincode und IBM Blockchain vertraut sind, können Sie das Demo in Bluemix [manuell bereitstellen](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#) oder auf die Schaltfläche 'In Bluemix bereitstellen' klicken, um die Webanwendung zu verwenden:   
[![In Bluemix bereitstellen ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  

<br>
## Wertpapier-Demo
{: #commercialpaper}

Anhand der Anwendung für Wertpapiere wird veranschaulicht, wie ein Handelsnetz für Wertpapiere mithilfe von IBM Blockchain implementiert werden kann. Im Wertpapier-Demo wird ein genehmigtes Blockchain-Netz untersucht, in dem zwei Teilnehmern Rollen und die entsprechenden Zugriffsebenen zugeordnet sind. Weitere Informationen zu den Komponenten dieses Demos finden Sie in der [Wertpapier-README](https://github.com/IBM-Blockchain/cp-web#readme); alternativ können Sie es sofort in Bluemix bereitstellen, um das Handelsnetz in der Praxis kennenzulernen:   
[![In Bluemix bereitstellen ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  

<br>
## Autoleasing-Demo
{: #carlease}

Anhand der Anwendung für Autoleasing wird die Lebensdauer eines Autos von der Herstellung über eine Reihe von Besitzern bis zum Verschrotten des Autos veranschaulicht. Im Demo werden Node.js für die serverseitige Programmierung und Golang für den Chaincode verwendet, der im IBM Blockchain-Netz ausgeführt wird. Das Demo umfasst zwei Chaincode-Instanzen: von einer werden die Regeln für die Autotransaktionen definiert, vom anderen alle Autotransaktionen in seiner Lebensdauer protokolliert. Von beiden Chaincode-Programmen werden JSON-Objekte zum Speichern der Daten verwendet. Weitere Informationen zur Anwendungsarchitektur und den Autoattributen in diesem Demo finden Sie in der [Autoleasing-README](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md); alternativ können Sie das Demo sofort in Bluemix bereitstellen:   
[![In Bluemix bereitstellen ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  

<br>

<!-- comment out - moving to separate file for now jh
## Non-deterministic chaincode
{: #ndcc}

IBM Blockchain networks support deterministic chaincode only. Using non-deterministic chaincode is not supported, and will cause severe errors, on any blockchain network.

**Non-deterministic chaincode** is any chaincode that does **not** result in the same appended value, over time and across nodes, on the blockchain ledger. By contrast, **deterministic chaincode** always produces the same appended value, over time and across nodes, on the blockchain ledger.

### Deterministic chaincode example
An **invoke** transaction that always increments the value of a variable by one is deterministic, because the result is always the same, on every node, without variance. Whenever this transaction is run against a fixed value of five, for example, the appended value is always six, on every node, every time. The network outcome for deterministic chaincode is no divergence in the blockchain; the copy of the ledger on each node always indicates (after syncing) that the value is one greater than the previous invocation.

### Non-deterministic chaincode example
An **invoke** transaction that increments the value of a blockchain variable with the number of elapsed seconds since the start of the day (00:00) is non-deterministic, because over time the value will vary across nodes. Each time this transaction is run against a fixed value of five, for example, the appended value diverges across nodes (with rare exceptions), because the number of elapsed seconds since 00:00 will inevitably vary. The network outcome for this non-deterministic chaincode is divergent blockchains; all nodes will not agree on the value of five + the number of elapsed seconds since 00:00.

### Randomness
Chaincode must exhibit no randomness in the appended values, over time and across nodes. Any randomness produces divergent blockchains across nodes, which must then be resolved by the network. To avoid randomness, you must ensure that no parallel chaincode can affect the input value from invocation chaincode. For example, do not run any **query** transactions in parallel with **invoke** transactions, because parallel queries could produce variance in the invocation values across nodes.

### Using a global variable
Using a global or instance variable to store a value that was retrieved from the ledger, or to set a value on the ledger, can lead to non-determinism. Chaincode should not rely on global or instance variables that will not retain their state across restarts of a chaincode container. The following is an example that uses a global variable; the value of `key`, which is written to the ledger via the `stub.PutState` function, is derived from a global variable:

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### Iterating over a map type
Iteration over a map type can lead to non-determinism, because order is not deterministic in the Go programming language. The following is an example of iteration over the map named `columnTypes`:

```go
 func generateColumns(colTypes map[string]string, colKeys []bool) ([]*shim.ColumnDefinition, error) {
	var tableColumns []*shim.ColumnDefinition
	keyIndex := 0
	for k, _ := range colTypes {
		tableColumns = append(tableColumns, &shim.ColumnDefinition{k, shim.ColumnDefinition_STRING, colKeys[keyIndex]})

		keyIndex++
	}
	return tableColumns, nil
}
```

-->


<!-- ## Using the Node.js SDK
{: #nodesdk}

Use the [Hyperledger fabric client SDK ](https://github.com/IBM-Blockchain/ibm-blockchain-js/blob/master/README.md) library for easier interaction with an IBM Blockchain network.  The SDK, through importing packages and libraries, allows for an application developer to build Node.js applications that can invoke functionality on the blockchain network from the client side.  Member services and asset management are now pluggable components on client side applications.  See the [Enhanced Node.js SDK](etn_sdk.html) section for full documentation and application examples. -->
