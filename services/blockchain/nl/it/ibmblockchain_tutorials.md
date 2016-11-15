---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Applicazioni di esempio ed esercitazioni
{: #1stanchor}
Ultimo aggiornamento: 5 ottobre 2016
{: .last-updated}

I seguenti esempi illustrano la modalità di funzionamento di applicazioni e chaincode in una rete IBM Blockchain. Per ulteriori informazioni sul codice Hyperledger Fabric v0.5, che è alla base della rete blockchain, visita la sezione [Fabric Docs](https://github.com/hyperledger/fabric/tree/master/docs) del progetto Hyperledger della Linux Foundation.  
{:shortdesc}

Per provare le applicazioni chaincode in azione, puoi distribuire immediatamente le demo Marbles, Commercial Paper o Car Lease qui di seguito (fai clic su un pulsante Distribuisci a Bluemix). Altrimenti, continua a leggere per esplorare l'esercitazione Hello Chaincode.

- [![Distribuisci a Bluemix](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)(https://bluemix.net/deploy/button.png)]  **Marbles**
- [![Distribuisci a Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)(https://bluemix.net/deploy/button.png)]  **Commercial Paper**
- [![Distribuisci a Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)(https://bluemix.net/deploy/button.png)]  **Car Lease**  

<br>
## Utilizzo dell'esercitazione Hello Chaincode
{: #hellocc}
Questa esercitazione ti guida nell'utilizzo degli elementi di base per codificare una semplice applicazione chaincode. Svilupperai in modo incrementale un chaincode funzionante che crea le risorse generiche per lo scambio su una rete. Interagirai quindi con il chaincode tramite la API di rete. Dopo aver completato questa esercitazione, sarai in grado di rispondere alle seguenti domande:
- Cos'è chaincode?
- Come implemento il chaincode?
- Quali dipendenze esistono?
- Quali sono le funzioni principali?
- Come passo diversi valori ai miei argomenti?
- Come completo la registrazione in modo protetto di un utente sulla mia rete?
- Come compilo il mio chaincode?
- Come interagisco con il chaincode tramite la API REST?

### Cos'è chaincode?
Chaincode è codice Go (GoLang) o Java che consente agli utenti di interagire con una rete blockchain. Quando 'richiami' una transazione sulla rete, richiami una funzione in chaincode che legge e scrive valori nel registro.

### Implementazione del tuo primo chaincode
Completa i seguenti argomenti per implementare chaincode su una rete IBM Blockchain su Bluemix:
#### Impostazione dell'ambiente
1. Scarica e installa Golang per il tuo sistema operativo da: [GoLang](https://golang.org/dl/).
2. Imposta il tuo GOPATH:
	- $GOPATH è un percorso **Variabile di ambiente** al tuo codice e ai tuoi progetti Go. Il tuo $GOPATH deve essere impostato per ottenere, sviluppare e installare pacchetti al di fuori della struttura ad albero Go standard. Pertanto, $GOPATH deve essere univoco dal percorso $GOROOT dove si trova la tua struttura ad albero Go originale. Ti basta creare una directory e puntare quindi il tuo $GOPATH a essa.
	- Imposta il tuo $GOPATH su Windows:
		- Crea una directory di spazio di lavoro per il tuo progetto, come ad esempio C:\Users\ADMIN\Documents\GoProjects.
		- Fai clic sul menu **Start** di Windows e cerca "variabili di ambiente di sistema".
		- Fai clic su **Modificare le variabili di ambiente relative al sistema**.
		- Dalla scheda **Avanzate**, fai clic su **Variabili di ambiente**.
		- Trova le tue variabili di ambiente di sistema GOPATH e GOROOT. Se devi creare GOPATH, fai clic su **Nuovo**.  
		- I tuoi valori GOROOT e GOPATH devono essere univoci. GOROOT viene generato automaticamente quando installi Go e dovrebbe essere C:\Go\.
		- Imposta il tuo GOPATH sulla directory di spazio di lavoro che hai creato. In questo esempio, **GOPATH** è **C:\Users\ADMIN\Documents\GoProjects**.  
		- Per ulteriori dettagli, esegui il comando `go help gopath` oppure visita la [documentazione di Go](https://golang.org/doc/install).
3. Aggiungi il codice shim Hyperledger Fabric v0.5 al tuo percorso Go immettendo il seguente comando:

	```
	go get github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview/core/chaincode/shim
	```

4. **Nota**: assicurati di seguire il link precedente per importare il codice shim v0.5 hyperledger-archives.  Il beckend Bluemix è costruito con lo stesso controllo delle versioni; di conseguenza, è importante che la versione shim e la versione Bluemix siano allineate.

#### Impostazione di GitHub
I piani Blockchain su Bluemix richiedono che il tuo chaincode si trovi in un repository [GitHub](https://Github.com/). Crea un account GitHub e imposta Git come descritto in [Set Up Git](https://help.github.com/articles/set-up-git/). Dopo aver impostato GitHub, completa la seguente procedura:
1. Vai a [learn chaincode](https://github.com/IBM-Blockchain/learn-chaincode) e biforca il repository.  
2. Clona la biforcazione alla directory specificata nel tuo $GOPATH.  
3. Il repository include due directory chaincode: [Start](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/start/chaincode_start.go) è il chaincode dal quale inizierai l'attività di sviluppo. [Finished](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/finished/chaincode_finished.go) è il chaincode finale prodotto dalla tua attività di sviluppo.
4. Accertati che lo sviluppo del chaincode abbia luogo nel tuo ambiente locale. Apri un prompt dei comandi e vai alla cartella che contiene `chaincode_start.go`. Immetti il seguente comando:

	```
	go build ./
	```
Il comando non dovrebbe restituire alcun errore o messaggio.

#### Implementazione dell'interfaccia chaincode
Il prossimo passo consiste nell'implementazione dell'interfaccia shim chaincode nel tuo codice Golang. Le tre funzioni principali sono **Init**, **Invoke** e **Query**. Tutte e tre le funzioni prendono un nome funzione e un array di stringhe come input ma variano per quanto riguarda il quando vengono richiamate. Eseguirai l'attività di sviluppo su un chaincode funzionante che crea risorse generiche per lo scambio si una rete blockchain.

### Dipendenze
L'istruzione `import` elenca le dipendenze necessarie per sviluppare il tuo chaincode:
1. `fmt` - contiene `Println` per attività di debug/registrazione.
2. `errors` - formato di errore Go standard.
3. `github.com/hyperledger/fabric/core/chaincode/shim` - codice che interfaccia il tuo codice Golang con un peer di rete.

### Passaggio di valori

Vengono passati i seguenti valori di chaincode:
#### Init()
Init viene richiamato per inizializzare il tuo chaincode quando ne esegui la distribuzione iniziale alla rete. In questo esempio, utilizzi `Init` per configurare lo stato iniziale di una variabile nel registro.

Nel tuo file `chaincode_start.go`, modifica la funzione `Init` in modo che memorizzi il primo elemento `args` nella chiave "hello_world":

```go
func (t *SimpleChaincode) Init(stub *shim.ChaincodeStub, function string, args []string) ([]byte, error) {
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

Questa operazione viene eseguita utilizzando la funzione shim `stub.PutState`. Il primo argomento è la chiave come una stringa e il secondo argomento è il valore come un array di byte. Questa funzione può restituire un errore, che il tuo codice ispeziona e restituisce, se presente.

#### Invoke()
`Invoke` viene richiamato per aggiungere una richiesta di transazione alla catena. La struttura di `Invoke` è semplice;
riceve un argomento `function` e, in base a questo argomento, richiama le funzioni Go nel chaincode.

Nel tuo file `chaincode_start.go`, modifica la funzione `Invoke` in modo che richiami una funzione di scrittura (write) generica.

```go
func (t *SimpleChaincode) Invoke(stub *shim.ChaincodeStub, function string, args []string) ([]byte, error) {
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

Il codice sta ora cercando `write`; aggiungi quindi tale funzione al tuo file `chaincode_start.go`:

```go
func (t *SimpleChaincode) write(stub *shim.ChaincodeStub, args []string) ([]byte, error) {
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

Questa funzione `write` dovrebbe presentarsi in modo simile alla precedente modifica `Init`. Puoi ora impostare la chiave e il valore per`PutState`, che ti consente di memorizzare qualsiasi coppia chiave/valore nel registro del blockchain.

#### Query()
`Query` viene richiamato per eseguire una query dello stato del tuo chaincode e non aggiunge blocchi alla catena. Solo le funzioni di distribuzione e richiamano aggiungono dei nuovi blocchi. Utilizza `Query` per leggere il valore delle coppie chiave/valore dello stato del tuo chaincode.

Nel tuo file `chaincode_start.go`, modifica la funzione `Query` in modo che richiami una funzione di lettura (read) generica:

```go
func (t *SimpleChaincode) Query(stub *shim.ChaincodeStub, function string, args []string) ([]byte, error) {
	fmt.Println("query is running " + function)

	// Handle different functions
	if function == "read" {                            //read a variable
		return t.read(stub, args)
	}
	fmt.Println("query did not find func: " + function)

	return nil, errors.New("Received unknown function query")
}
```

Il codice sta ora cercando `read`; aggiungi quindi tale funzione al tuo file `chaincode_start.go`:

```go
func (t *SimpleChaincode) read(stub *shim.ChaincodeStub, args []string) ([]byte, error) {
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

Questa funzione `read` utilizza `GetState`, che è il complemento di `PutState`. Questa funzione shim prende solo un singolo argomento stringa, che è il nome della chiave da richiamare. Questa funzione restituisce quindi il valore, come un array di byte, a `Query`, che a sua volta lo invia al gestore REST.

#### Main()
La funzione `main` viene eseguita quando ciascun peer distribuisce la sua istanza del chaincode. Avvia il chaincode e lo registra presso il peer. Non è richiesto alcun aggiornamento del codice per 'main'; sia chaincode_start.go che chaincode_finished.go includono una funzione `main` all'inizio di ciascun file:

```go
func main() {
	err := shim.Start(new(SimpleChaincode))
	if err != nil {
		fmt.Printf("Error starting Simple chaincode: %s", err)
	}
}
```

### Interazione con il tuo chaincode
Il modo più rapido per testare il tuo chaincode consiste nell'utilizzare l'interfaccia REST sui tuoi peer.
L'IU Swagger sul tuo monitor dashboard Bluemix ti consente di provare la distribuzione di chaincode senza scrivere del codice aggiuntivo.  

<br>
#### API Swagger
Per utilizzare la API Swagger, completa la seguente procedura:

1. Accedi a [Bluemix](https://console.ng.bluemix.net/login) e accertati di essere nella scheda **Dashboard**.
1. Controlla di trovarti nello stesso "spazio" Bluemix che contiene il tuo servizio IBM Blockchain. Lo spostamento nello spazio si trova sulla sinistra.
1. Vicino alla parte inferiore si trova un pannello **Servizi**; fai clic sul tuo servizio IBM Blockchain.
1. Dovresti vedere un messaggio di benvenuto in IBM Blockchain; fai clic sul pulsante **AVVIA** sulla destra.
1. Nella pagina del monitor, dovresti vedere due tabelle; la tabella inferiore potrebbe essere vuota.
	- **Scheda Rete:**
		- I **log dei peer** si trovano nella tabella superiore. Nella riga per **peer 1**, fai clic sull'icona di file per visualizzare il log. Oltre a questa vista statica, ci sono dei **log dei peer in streaming** dal vivo nella scheda **Visualizza i log** vicino alla parte superiore della pagina.
		- I **log dei chaincode** si trovano nella tabella inferiore. Ogni chaincode è etichettato con l'hash di chaincode restituito quando è stato distribuito. Seleziona il peer in qualsiasi riga di chaincode e fai quindi clic sull'icona di file per visualizzare il log.
	- **Scheda API**: visualizza la pagina di documentazione della API Swagger.
1. Continua con la seguente procedura per implementare il completamento della registrazione protetto. Le chiamate all'endpoint `/chaincode` nell'interfaccia REST richiedono un ID di contesto protetto. Perché la maggior parte delle chiamate REST venga accettata, devi passare un *enrollID* registrato dall'elenco di credenziali di servizio:
  - Fai clic su **+ ID registrazione di rete** per espandere l'elenco di valori *enrollID* e i loro segreti.
  - Copia la serie di credenziali in un file di testo per un uso successivo.
  - Espandi la sezione API **Registrar**.
  - Espandi la sezione `POST /registrar`.
  - Compila il campo ``Valore`` con il JSON che specifica un ``enrollID` e `enrollSecret' dalle tue credenziali:

  ![Esempio di registro](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/registrar.PNG "Esempio di registro")

  Il *Corpo della risposta* dovrebbe essere simile al seguente esempio:

  ![Esempio di registro](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/register_response.PNG "Corpo risposta esempio di registro")

Ora che hai impostato un `enrollID`, puoi utilizzare questo ID quando distribuisci, richiami ed esegui query del chaincode nei passi successivi.
### Distribuzione del tuo chaincode
Per distribuire il tuo chaincode tramite l'interfaccia REST; il tuo chaincode deve essere memorizzato in un repository GitHub pubblico. Quando invii una richiesta di distribuzione a un peer, specifichi l'URL per il repository di chaincode e i parametri per inizializzare il chaincode.

**Prima di distribuire** il tuo chaincode, verifica che esegua l'attività di sviluppo in locale:
1. Apri un prompt dei comandi e vai alla directory che contiene `chaincode_start.go`. Immetti il seguente comando:
	```
	go build ./
	```
1. Espandi la sezione API **Chaincode**.
1. Espandi la sezione `POST /chaincode`.
1. Imposta il campo di testo `DeploySpec` (svuota gli altri campi) con il codice di esempio qui di seguito, specificando il tuo percorso al repository di chaincode e l'`enrollID` dal passo `/registrar` precedente. Il `"path":` dovrebbe presentarsi simile a: `"https://github.com/johndoe/learn-chaincode/finished"`. Questo è il percorso alla tua biforcazione del repository più il percorso al tuo file chaincode_finished.go:

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

  Il *Corpo della risposta* dovrebbe essere simile al seguente esempio:

  ![Esempio di distribuzione](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/deploy_response.PNG "Corpo risposta esempio di distribuzione")

  La risposta per la distribuzione conterrà l'ID per questo chaincode. L'ID è un hash alfanumerico di 128 caratteri, che puoi utilizzare per delle future richieste di richiamo o di query. Copia questo ID nel tuo editor di testo.

#### Query
Esegui una query del tuo chaincode per il valore della chiave `hello_world`, che hai impostato con la funzione `Init`:
1. Espandi la sezione API **Chaincode**.
1. Espandi la sezione `POST /chaincode`.
1. Compila il campo di testo `QuerySpec` (svuota gli altri campi) con il seguente esempio, specificando l'ID chaincode dal passo di distribuzione precedente e l'`enrollID` dal passo `/registrar` precedente:

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
  Il *Corpo della risposta" dovrebbe essere simile al seguente esempio:

  ![Esempio di query](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query_response.PNG "Corpo risposta esempio di query")

  Il valore di `hello_world` è "hi there", che è stato impostato dal corpo della chiamata di distribuzione precedente.

#### Richiamo
Richiama la funzione di scrittura (write) generica con `invoke`. Modifica il valore di `hello_world` in "go away":
1. Espandi la sezione API **Chaincode**.
1. Espandi la sezione `POST /chaincode`.
1. Compila il campo di testo `InvokeSpec` (svuota gli altri campi) con il seguente esempio, specificando l'ID chaincode dal passo di distribuzione precedente e l'`enrollID` dal passo `/registrar` precedente:

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
  Il *Corpo della risposta" dovrebbe essere simile al seguente esempio:

  ![Esempio di richiamo](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/invoke_response.PNG "Corpo risposta esempio di richiamo")

  Esegui nuovamente la query sopra indicata; dovresti ottenere la seguente risposta:

  ![Esempio query2](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query2_response.PNG "Risposta esempio di richiamo")

Hai appena completato la scrittura di un po' di chaincode di base.  

<br>
## Requisiti per le demo Marbles, Commercial Paper e Car Lease
{: #requirements}

I seguenti prerequisiti sono inclusi con il tuo servizio Bluemix per eseguire le applicazioni Marbles, Commercial Paper e Car Lease localmente. Il tuo ambiente Bluemix clona l'Hyperledger Fabric per fornire queste dipendenze:

- ID Bluemix https://console.ng.bluemix.net/ (richiesto per creare la tua rete IBM Blockchain e fornire le credenziali di servizio per i peer e per l'autorità di certificazione)
- Node.js 0.12.0+ e npm v2+
- Ambiente Golang (richiesto solo per sviluppare un tuo chaincode)

Le demo richiedono dimestichezza con Node.js e il modulo express. Devi anche avere una comprensione concettuale di 'chaincode', 'registro' (in inglese 'ledger') e 'peer' in un contesto di blockchain; consulta il [glossario di Hyperledger Fabric](https://github.com/hyperledger/fabric/blob/master/docs/glossary.md).  

<br>
## Utilizzo della demo Marbles
{: #marbles}

L'applicazione Marbles illustra un semplice trasferimento di risorsa tra due parti. L'applicazione è progettata per testare l'SDK JavaScript, guidarne lo sviluppo e aiutare gli sviluppatori ad acquisire dimestichezza con l'SDK e il chaincode.

Esplora le [esercitazioni Marbles](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md) per capire in che modo applicazione web, SDK e chaincode operano insieme. Se già hai dimestichezza con chaincode e IBM Blockchain, puoi [distribuire manualmente](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#) la demo a Bluemix oppure fare clic sul pulsante Distribuisci a Bluemix per utilizzare l'applicazione web:
  
[![Distribuisci a Bluemix](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)(https://bluemix.net/deploy/button.png)]  

<br>
## Utilizzo della demo Commercial Paper
{: #commercialpaper}

L'applicazione Commercial Paper illustra il modo in cui è possibile implementare una rete di scambi commerciali di commercial paper utilizzando IBM Blockchain. La demo Commercial Paper esplora una rete blockchain con autorizzazioni, su cui ai partecipanti vengono assegnati dei ruoli e i corrispondenti livelli di accesso. Consulta il [README di Commercial Paper](https://github.com/IBM-Blockchain/cp-web#readme) per saperne di più sui componenti di questa demo oppure distribuiscila a Bluemix immediatamente per vedere la rete di scambi commerciali in azione:
  
[![Distribuisci a Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)(https://bluemix.net/deploy/button.png)]  

<br>
## Utilizzo della demo Car Lease
{: #carlease}

L'applicazione Car Lease illustra il ciclo di vita di un veicolo, andando dalla produzione, passando per diversi proprietari e finendo con la rottamazione del veicolo. La demo utilizza Node.js per la programmazione lato server e Golang per il chaincode in esecuzione sulla rete IBM Blockchain. La demo include anche due istanze di chaincode: una definisce le regole per le transazioni del veicolo e l'altra registra tutte le transazioni del veicolo durante il suo ciclo di vita. Entrambi i programmi chaincode utilizzano gli oggetti JSON per memorizzare i dati. Consulta il [README di Car Lease](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) per saperne di più sull'architettura dell'applicazione e gli attributi di veicolo associati a questa demo oppure distribuisci la demo immediatamente a Bluemix:
  
[![Distribuisci a Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)(https://bluemix.net/deploy/button.png)]  

<br>
## Chaincode non deterministico
{: #ndcc}

Le reti IBM Blockchain supportano solo il chaincode deterministico. L'utilizzo di chaincode non deterministico non è supportato e causerà degli errori server su qualsiasi rete blockchain.

Un **chaincode non deterministico** è qualsiasi chaincode che **non** produce lo stesso valore accodato, nel corso del tempo e tra i nodi, sul registro del blockchain. Il **chaincode deterministico**, invece, produce sempre lo stesso valore accodato, nel tempo e tra i nodi, sul registro del blockchain.

### Esempio di chaincode deterministico
Una transazione di richiamo (**invoke**) che incrementa sempre il valore di una variabile di uno è deterministica perché il risultato è sempre lo stesso, su ogni nodo, senza variazioni. Quando questa transazione viene eseguita su un valore fisso di cinque, ad esempio, il valore accodato è sempre sei, su ogni nodo e ogni volta. L'esito di rete per il chaincode deterministico non vede alcuna divergenza nel blockchain; la copia del registro su ciascun nodo indica sempre (dopo la sincronizzazione) che il valore è di uno più grande del richiamo precedente.

### Esempio di chaincode non deterministico
Una transazione di richiamo (**invoke**) che incrementa il valore di una variabile blockchain con il numero di secondi trascorsi dall'inizio del giorno (00:00) è non deterministico perché nel corso del tempo il valore varierà tra i nodi. Ogni volta che questa transazione viene eseguita su un valore fisso di cinque, ad esempio, il valore accodato è diverso tra i nodi (con rare eccezioni) perché il numero di secondi trascorso da 00:00 varierà inevitabilmente. L'esito di rete per questo chaincode non deterministico vede dei blockchain divergenti; tutti i nodi non concorderanno sul valore di cinque + il numero di secondi trascorsi da 00:00.

### Casualità
Il chaincode non deve presentare alcuna casualità nei valori accodati, nel tempo e tra i nodi. Qualsiasi casualità produce dei blockchain divergenti tra i nodi che devono quindi essere risolti dalla rete. Per evitare casualità, devi assicurarti che nessun chaincode parallelo possa influenzare il valore di input dal chaincode di richiamo. Ad esempio, non eseguire transazioni di **query** in parallelo con le transazioni di richiamo (**invoke**) perché le query parallele potrebbero produrre delle variazioni nei valori del richiamo tra i nodi.

### Utilizzo di una variabile globale
L'utilizzo di una variabile globale o di istanza per memorizzare un valore richiamato da un registro o per impostare un valore sul registro, può portare al non determinismo. Il chaincode non dovrebbe basarsi sulle variabili globali o di istanza che non mantengono il proprio stato tra i riavvii di un contenitore chaincode. Di seguito, viene riportato un esempio che utilizza una variabile globale; il valore di `key`, che viene scritto nel registro tramite la funzione `stub.PutState`, è derivato da una variabile globale:

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### Iterazione su un tipo di associazione
L'iterazione su un tipo di associazione può portare al non determinismo in quanto l'ordine non è deterministico nel linguaggio di programmazione Go. Di seguito è riportato un esempio di iterazione sull'associazione denominata `columnTypes`:

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

<!---## Using the Node.js SDK
{: #nodesdk}

Use the [Hyperledger fabric client SDK ](https://github.com/IBM-Blockchain/ibm-blockchain-js/blob/master/README.md) library for easier interaction with an IBM Blockchain network.  The SDK, through importing packages and libraries, allows for an application developer to build Node.js applications that can invoke functionality on the blockchain network from the client side.  Member services and asset management are now pluggable components on client side applications.  See the [Enhanced Node.js SDK](etn_sdk.html) section for full documentation and application examples.--->
