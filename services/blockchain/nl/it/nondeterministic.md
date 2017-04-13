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

# Chaincode non deterministico
{: #ndcc}


Le reti IBM Blockchain supportano solo il chaincode deterministico. L'utilizzo di chaincode non deterministico non è supportato e causerà degli errori server su qualsiasi rete blockchain.
{:shortdesc}

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
