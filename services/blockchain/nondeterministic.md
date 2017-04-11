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

# Non-deterministic chaincode
{: #ndcc}


IBM Blockchain networks support deterministic chaincode only. Using non-deterministic chaincode is not supported, and will cause severe errors, on any blockchain network.
{:shortdesc}

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
