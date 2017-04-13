---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-01"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Nicht deterministischer Chaincode
{: #ndcc}


Von IBM Blockchain-Netzen wird nur deterministischer Chaincode unterstützt. Die Verwendung von nicht deterministischem Chaincode wird nicht unterstützt und führt in jedem Blockchain-Netz zu schwerwiegenden Fehlern.
{:shortdesc}

**Nicht deterministischer Chaincode** ist jeder Chaincode, der im zeitlichen Verlauf und für alle Knoten **nicht** denselben angehängten Wert im Blockchain-Hauptbuch zum Ergebnis hat. Im Gegensatz dazu wird bei Verwendung eines **deterministischen Chaincodes** im zeitlichen Verlauf und für alle Knoten immer derselbe angehängte Wert im Blockchain-Hauptbuch generiert.

### Beispiel für deterministischen Chaincode
Die Transaktion **Aufrufen**, die den Wert einer Variable immer um eins erhöht, ist deterministisch, weil das Ergebnis für jeden Knoten ohne Abweichung immer dasselbe ist. Sobald diese Transaktion bei einem festen Wert von beispielsweise fünf ausgeführt wird, ist der angehängte Wert immer für jeden Knoten sechs. Das Netzergebnis für deterministischen Chaincode ergibt in Blockchain keine Divergenz; aus der Kopie des Hauptbuchs auf jedem Knoten geht somit (nach der Synchronisation) immer hervor, dass der Wert um eins größer als beim vorherigen Aufruf ist.

### Beispiel für nicht deterministischen Chaincode
Die Transaktion **Aufrufen**, die den Wert der Blockchain-Variablen um die Anzahl der abgelaufenen Sekunden seit dem Beginn des Tages (00:00) erhöht, ist nicht deterministisch, weil der Wert im zeitlichen Verlauf für die Knoten unterschiedlich ist. Sobald diese Transaktion bei einem festen Wert von beispielsweise fünf ausgeführt wird, ist der angehängte Wert auf den Knoten (mit seltenen Ausnahmen) unterschiedlich, weil die Anzahl der abgelaufenen Sekunden seit 00:00 unvermeidlich von einander abweicht. Das Netzergebnis für diesen nicht deterministischen Chaincode ergibt Abweichungen in Blockchain; der Wert fünf plus die Anzahl der abgelaufenen Sekunden seit 00:00 ist nicht auf allen Knoten identisch.

### Zufälligkeit
Durch Chaincode dürfen sich im zeitlichen Verlauf für alle Knoten keine zufälligen Werte ergeben. Zufällige Werte führen zu Abweichungen auf den Blockchain-Knoten, die schließlich vom Netz aufgelöst werden müssen. Zur Vermeidung von zufälligen Werten müssen Sie sicherstellen, dass der Eingabewert vom Aufruf-Chaincode nicht durch parallele Chaincodes beeinträchtigt wird. Führen Sie zum Beispiel nicht Transaktionen des Typs **Abfragen** parallel mit Transaktionen des Typs **Aufrufen** aus, weil parallele Abfragen zu Abweichungen in Bezug auf die Aufrufwerte für die Knoten führen können.

### Globale Variable verwenden
Wenn Sie eine globale Variable oder eine Instanzvariable verwenden, um einen Wert zu speichern, der aus dem Hauptbuch abgerufen wurde, oder einen Wert für das Hauptbuch festzulegen, kann dies zu einem Nichtdeterminismus führen. Chaincode sollte sich nicht auf globale Variablen oder Instanzvariablen stützen, die ihren Status bei Neustarts eines Chaincode-Containers nicht beibehalten. Das folgende Beispiel zeigt die Verwendung einer globalen Variablen. Der Wert von `key`, der über die Funktion `stub.PutState` in das Hauptbuch geschrieben wird, wird aus einer globalen Variablen abgeleitet:

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### Zuordnungstyp iterieren
Die Iteration über einen Zuordnungstyp kann zu einem Nichtdeterminismus führen, weil die Reihenfolge in der Programmiersprache Go nicht deterministisch ist. Das folgende Beispiel zeigt eine Iteration über die Zuordnung namens `columnTypes`:

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
