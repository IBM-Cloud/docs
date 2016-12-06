---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Código de encadenamiento no determinista
{: #ndcc}
Última actualización: 08 de noviembre de 2016
{: .last-updated}

La red de IBM Blockchain da soporte únicamente al código de encadenamiento determinista. El uso del código de encadenamiento no determinista no se admite y causará errores graves en cualquier red de blockchain.
{:shortdesc}

La red de IBM Blockchain da soporte únicamente al código de encadenamiento determinista. El uso del código de encadenamiento no determinista no se admite y causará errores graves en cualquier red de blockchain.

**Código de encadenamiento no determinista** es cualquier código que **no** resulta en el mismo valor añadido, a lo largo del tiempo y en todos los nodos, en el libro mayor de blockchain. En cambio, **código de encadenamiento determinista** siempre produce el mismo valor añadido, a lo largo del tiempo y en todos los nodos, en el libro mayor de blockchain.

### Ejemplo de código de encadenamiento determinista
Una transacción **invoke** que siempre incrementa el valor de una variable por uno es determinista, porque el resultado es siempre el mismo, en cada nodo, sin variar. Siempre que esta transacción se ejecute respecto a un valor fijo de cinco, por ejemplo, el valor añadido siempre será seis, cada vez y en cada nodo. El resultado de red para el código de encadenamiento determinista no tiene ninguna divergencia en el blockchain; la copia del libro mayor de cada nodo siempre indica (después de la sincronización) que el valor es uno mayor que la invocación anterior.

### Ejemplo de código de encadenamiento no determinista
Una transacción **invoke** que incrementa el valor de una variable de blockchain con el número de segundos transcurridos desde el inicio del día (00:00) no es determinista porque a lo largo del tiempo el valor variará en los nodos. Cada vez que se ejecuta esta transacción respecto a un valor fijo de cinco, por ejemplo, el valor añadido diverge entre los nodos (con raras excepciones) porque el número de segundos transcurridos desde las 00:00 inevitablemente variará. El resultado de red para este código de encadenamiento no determinista son blockchains divergentes; no todos los nodos coincidirán en el valor de cinco + el número de segundos transcurridos desde las 00:00.

### Aleatoriedad
El código de encadenamiento no debe mostrar aleatoriedad en los valores añadidos, a lo largo del tiempo y en todos los nodos. Cualquier comportamiento aleatorio produce blockchains divergentes en los nodos lo que deberá resolverse mediante la red. Para evitar la aleatoriedad, debe asegurarse de que ningún código de encadenamiento paralelo pueda afectar el valor de entrada desde el código de encadenamiento de invocación. Por ejemplo, no ejecute ninguna transacción **query** en paralelo con transacciones **invoke** porque las consultas paralelas pueden producir variación en los valores de invocación en los nodos.

### Uso de una variable global
El uso de una variable global o de instancias para almacenar un valor que se ha recuperado del libro mayor, o para establecer un valor en el libro mayor, puede dar lugar a la no determinación. El chaincode no se debe basar en variables globales ni de instancias que no guardarán su estado al reiniciar un contenedor de chaincode. A continuación se muestra un ejemplo que utiliza una variable global; el valor de `key`, que se escribe en el libro mayor mediante la función `stub.PutState`, se deriva de una variable global:

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### Iteración sobre un tipo de correlación
La iteración sobre un tipo de correlación puede dar lugar a la no determinación, ya que el orden no es determinante en el lenguaje de programación Go. A continuación se muestra un ejemplo de iteración sobre la correlación denominado `columnTypes`:

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
