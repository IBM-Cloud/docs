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

# Chaincode não determinístico
{: #ndcc}


As redes do IBM Blockchain suportam chaincode determinístico apenas. O uso de chaincode não determinístico não é suportado e causará erros graves, em qualquer rede de blockchain.
{:shortdesc}

**Chaincode não determinístico** é qualquer chaincode que **não** resulte no mesmo valor anexado, ao longo do tempo e entre nós, no livro razão de blockchain. Em contraste, o **chaincode determinístico** sempre produz o mesmo valor anexado, ao longo do tempo e entre nós, no livro razão de blockchain.

### Exemplo de chaincode determinístico
Uma transação **chamar** que sempre incrementa o valor de uma variável por um é determinística, porque o resultado é sempre o mesmo, em cada nó, sem variação. Sempre que essa transação for executada com relação a um valor fixo, por exemplo, o valor anexado será sempre seis, em cada nó, toda vez. O resultado de rede para chaincode determinístico é nenhuma divergência no blockchain; a cópia do livro razão em cada nó sempre indica (após a sincronização) que o valor é um maior que a chamada anterior.

### Exemplo de chaincode não determinístico
Uma transação **chamar** que incrementa o valor de uma variável de blockchain com o número de segundos decorridos desde o início do dia (00h) é não determinística, porque ao longo do tempo o valor irá variar entre nós. Cada vez que esta transação for executada com relação a um valor fixo, por exemplo, o valor anexado divergirá entre nós (com raras exceções), porque o número de segundos decorridos desde às 00h irá variar inevitavelmente. O resultado da rede para esse chaincode não determinístico são blockchains divergentes; todos os nós não concordarão com o valor de cinco + o número de segundos decorridos desde as 00h.

### Aleatoriedade
O chaincode deve apresentar nenhuma aleatoriedade nos valores anexados, ao longo do tempo e entre nós. Qualquer aleatoriedade produz blockchains divergentes entre nós, que devem, então, ser resolvidos pela rede. Para evitar aleatoriedade, deve-se assegurar que nenhum chaincode paralelo pode afetar o valor de entrada a partir do chaincode de chamada. Por exemplo, não execute nenhuma transação **consultar** em paralelo com transações **chamar**, porque consultas paralelas poderiam produzir variação nos valores de chamada entre nós.

### Usando uma variável global
Usar uma variável global ou de instância para armazenar um valor que foi recuperado do livro razão ou para configurar um valor no livro razão pode levar a não
determinismo. O chaincode não deve depender de variáveis globais ou de instância que não reterão seu
estado ao longo de reinicializações de um contêiner de chaincode. A seguir está um exemplo que usa uma variável global; o valor de `key`, que é gravado no livro razão por meio da função
`stub.PutState`, é derivado de uma variável global:

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### Iteração sobre um tipo de mapa
A iteração sobre um tipo de mapa pode levar a não determinismo, porque a ordem não é determinística na linguagem de programação Go. A seguir está um exemplo de
iteração sobre o mapa chamado `columnTypes`:

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
