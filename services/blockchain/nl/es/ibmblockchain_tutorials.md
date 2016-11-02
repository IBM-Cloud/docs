---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Apps de ejemplo y guías de aprendizaje
{: #1stanchor}
Última actualización: 5 de octubre de 2016
{: .last-updated}

Los siguientes ejemplos demuestran cómo las aplicaciones y el código de encadenamiento funciona en una red de IBM Blockchain. Para obtener más información sobre cómo el código de Hyperledger Fabric v0.5, que respalda la red de blockchain, visite la sección [Documentos de Fabric](https://github.com/hyperledger/fabric/tree/master/docs) de Hyperledger Project de Linux Foundation.  
{:shortdesc}

Para experimentar aplicaciones de código de encadenamiento en acción, puede desplegar inmediatamente la demo Mármoles, Papel comercial o Alquiler de coches que se muestra a continuación (pulse un botón Desplegar en Bluemix). O, siga leyendo para explorar la guía de aprendizaje Hello Chaincode.

- [![Desplegar en Bluemix](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)(https://bluemix.net/deploy/button.png)]  **Mármoles**
- [![Desplegar en Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)(https://bluemix.net/deploy/button.png)]  **Papel comercial**
- [![Desplegar en Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)(https://bluemix.net/deploy/button.png)]  **Alquiler de coches**  

<br>
## Utilización de la guía de aprendizaje Hello Chaincode
{: #hellocc}
Esta guía de aprendizaje le lleva por los componentes básicos para codificar una aplicación de código de encadenamiento elemental. Se creará de forma incremental un código de encadenamiento de trabajo que crea activos genéricos para su intercambio en una red. A continuación interactuará con el código de encadenamiento a través de la API de red. Después de completar esta guía de aprendizaje, podrá responder a las siguientes preguntas:
- ¿Qué es código de encadenamiento?
- ¿Cómo implemento código de encadenamiento?
- ¿Qué dependencias existen?
- ¿Cuáles son las funciones principales?
- ¿Cómo puedo pasar valores distintos a mis argumentos?
- ¿Cómo puedo inscribir de forma segura un usuario en mi red?
- ¿Cómo puedo compilar mi código de encadenamiento?
- ¿Cómo puedo interactuar con mi código de encadenamiento a través de la API REST?

### ¿Qué es código de encadenamiento?
El código de encadenamiento es código Go (GoLang) o Java que permite a los usuarios interactuar con un red de blockchain. Siempre que 'invoca' una transacción en la red está llamando a una función en un código de encadenamiento que lee y graba valores en el libro mayor.

### Implementación del primer código de encadenamiento
Complete los siguientes temas para implementar el código de encadenamiento en una red de IBM Blockchain en Bluemix:
#### Configuración del entorno
1. Descargue e instale Golang para el sistema operativo desde: [GoLang](https://golang.org/dl/).
2. Establezca GOPATH:
	- $GOPATH es una vía de acceso de **variable de entorno** para el código Go y los proyectos. $GOPATH se debe establecer para obtener, compilar e instalar paquetes fuera del árbol Go estándar. Por lo tanto, $GOPATH debe ser exclusiva en la vía de acceso $GOROOT donde reside el árbol Go original. Simplemente cree un directorio y, a continuación, apunte $GOPATH al mismo.
	- Establezca $GOPATH en Windows:
		- Cree un directorio de espacio de trabajo para su proyecto, como por ejemplo C:\Users\ADMIN\Documents\GoProjects.
		- Pulse el menú **Inicio** de Windows y busque "variables de entorno del sistema".
		- Pulse **Editar las variables de entorno del sistema**.
		- En el separador **Avanzado**, pulse **Variables de entorno**.
		- Busque las variables de entorno del sistema GOPATH y GOROOT. Si necesita crear GOPATH, pulse **Nuevo**.  
		- Los valores GOROOT y GOPATH deben ser exclusivos. GOROOT se genera automáticamente al instalar Go y debe ser C:\Go\.
		- Establezca GOPATH en el directorio de espacio de trabajo que ha creado. En este ejemplo, **GOPATH** es **C:\Users\ADMIN\Documents\GoProjects**.  
		- Para obtener más información, ejecute el mandato `go help gopath` o visite la [Documentación de Go](https://golang.org/doc/install).
3. Añada el código shim de Hyperledger Fabric v0.5 a la vía de acceso de Go ejecutando el siguiente mandato:

	```
	go get github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview/core/chaincode/shim
	```

4. **Nota**: Asegúrese de seguir el enlace anterior para importar el código shim de v0.5 hyperledger-archives. El programa de fondo de Bluemix se crea con la misma versión; como resultado, es importante que se alinee la versión de shim y la versión de Bluemix.

#### Configuración de GitHub
Los planes de Blockchain en Bluemix requieren que el código de encadenamiento esté ubicado en un repositorio [GitHub](https://Github.com/). Cree una cuenta GitHub y configure Git tal como se describe en [Configuración de Git](https://help.github.com/articles/set-up-git/). Después de configurar GitHub, complete los siguientes pasos:
1. Vaya a [obtener información sobre código de encadenamiento](https://github.com/IBM-Blockchain/learn-chaincode) y bifurque el repositorio.  
2. Clone la bifurcación en el directorio especificado en $GOPATH.  
3. El repositorio incluye dos directorios de código de encadenamiento: [Iniciar](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/start/chaincode_start.go) es el código de encadenamiento a partir del que se empezará a construir. [Finalizado](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/finished/chaincode_finished.go) es el código de encadenamiento que se creará últimamente.
4. Asegúrese de que el código de encadenamiento se crea en el entorno local. Abra un indicador de mandatos y vaya a la carpeta que contiene `chaincode_start.go`. Escriba el siguiente mandato:

	```
	go build ./
	```
El mandato debe devolverse sin errores ni mensajes.

#### Implementación de la interfaz de código de encadenamiento
El siguiente paso es implementar la interfaz shim de código de encadenamiento en el código Golang. Las tres funciones principales son **Init**, **Invoke** y **Query**. Las tres funciones toman un nombre de función y una matriz de series como entrada, pero varían en cuanto a cuando se llaman. Estará desarrollando un código de encadenamiento de trabajo que crea activos genéricos para su intercambio en una red de blockchain.

### Dependencias
La sentencia `import` lista dependencias que son necesarias para crear el código de encadenamiento:
1. `fmt` - contiene `Println` para su depuración/registro.
2. `errors` - formato de error de Go estándar.
3. `github.com/hyperledger/fabric/core/chaincode/shim` - código que interrelaciona el código de Golang con un igual de red.

### Pasar valores

Se pasan los siguientes valores de código de encadenamiento:
#### Init()
Se llama a Init para inicializar el código de encadenamiento la primera vez que se despliega en la red. En este ejemplo, utilice `Init` para configurar el estado inicial de una variable en el libro mayor.

En el archivo `chaincode_start.go`, cambie la función `Init` de modo que almacene el primer elemento `args` en la clave "hello_world":

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

Esto se lleva a cabo utilizando la función shim `stub.PutState`. El primer argumento es la clave como una serie, y el segundo argumento es el valor como matriz de bytes. Esta función puede devolver un error, que el código inspecciona y devuelve si está presente.

#### Invoke()
Se llama a `Invoke` para añadir una solicitud de transacción a la cadena. La estructura de `Invoke` es simple; recibe un argumento
`function` y basándose en este argumento, llama a funciones Go en el código de encadenamiento.

En el archivo `chaincode_start.go`, cambie la función `Invoke` de modo que llame a una función de grabación genérica.

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

El código ahora busca `write`, por lo que debe añadir esa función en el archivo `chaincode_start.go`:

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

Esta función `write` debe ser parecida al cambio `Init` anterior. Ahora puede establecer la clave y el valor para `PutState`, lo que le permite almacenar todos los pares clave/valor en el libro mayor de blockchain.

#### Query()
Se llama a `Query` para consultar el estado del código de encadenamiento y no añade bloques a la cadena. Solamente las funciones de despliegue e invocación añaden nuevos bloques. Utilice `Query` para leer el valor de los pares de clave/valor del estado del código de encadenamiento.

En el archivo `chaincode_start.go`, cambie la función `Query` de modo que llame a una función de lectura genérica:

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

El código ahora busca `read`, por lo que debe añadir esa función en el archivo `chaincode_start.go`:

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

Esta función `read` utiliza `GetState`que es el complemento a `PutState`. Esta función shim acepta únicamente un argumento de cadena, que es el nombre de la clave a recuperar. A continuación, esta función devuelve el valor como una matriz de bytes, a `Query`, que a su vez lo envía al manejador REST.

#### Main()
La función `main` se ejecuta cuando cada igual despliegue su instancia del código de encadenamiento. Inicia el código de encadenamiento y lo registra con el igual. No es necesario ninguna actualización en el código para 'main'; chaincode_start.go y chaincode_finished.go incluyen una función `main` al principio de cada archivo:

```go
func main() {
	err := shim.Start(new(SimpleChaincode))
	if err != nil {
		fmt.Printf("Error starting Simple chaincode: %s", err)
	}
}
```

### Interacción con el código de encadenamiento
La manera más rápida de probar el código de encadenamiento es utilizar la interfaz REST en sus iguales.
La interfaz de usuario de Swagger en el panel de control de Bluemix le permite experimentar con el despliegue del código de encadenamiento, sin escribir ningún código adicional.  

<br>
#### API de Swagger
Complete los siguientes pasos para utilizar la API de Swagger:

1. Inicie la sesión en [Bluemix](https://console.ng.bluemix.net/login) y asegúrese de que está en el separador **Panel de control**.
1. Compruebe que está en el mismo "espacio" de Bluemix que contiene el servicio de IBM Blockchain. La navegación de espacio está a la izquierda.
1. Hay un panel **Servicios** cerca de la parte inferior; pulse en el servicio de IBM Blockchain.
1. Debería ver un mensaje "Bienvenido a IBM Blockchain..."; pulse en el botón **INICIAR** de la derecha.
1. En la página de supervisión, debe ver dos tablas; la tabla inferior puede estar vacía.
	- **Separador Red:**
		- Los **registros de iguales** están en la tabla superior. En la fila para **igual 1**, pulse el icono del archivo para ver el registro. Además de esta vista estática, existen **registros de iguales en modalidad continua** en el separador **Ver registros** cerca del principio de la página.
		- Los **registros de código de encadenamiento** están en la tabla inferior. Cada código de encadenamiento se etiqueta con el hash del código de encadenamiento que se devolvió cuando se desplegó. Seleccione el igual en cualquier fila del código de encadenamiento y luego pulse el icono de archivo para ver el registro.
	- **Separador API**: Visualiza la página de documentación de la API de Swagger.
1. Continúe con los siguientes pasos para implementar la inscripción segura. Las llamadas al punto final `/chaincode` en la interfaz REST requieren un ID de contexto seguro. Para que la mayoría de llamadas REST se acepten, debe pasar un *enrollID* registrado de la lista de credenciales de servicio:
  - Pulse **+ ID de inscripción de red** para expandir la lista de valores *enrollID* y sus secretos.
  - Copie el conjunto de credenciales en un archivo de texto para utilizarlo más adelante.
  - Expanda la sección de API **Registrar**.
  - Expanda a sección `POST /registrar`.
  - Rellene el campo `Valor` con JSON que especifica un `enrollID` y 'enrollSecret' de las credenciales:

  ![Ejemplo de registro](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/registrar.PNG "Ejemplo de registro")

  El *Cuerpo de la respuesta* debería tener el siguiente aspecto:

  ![Ejemplo de registro](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/register_response.PNG "Cuerpo de respuesta del ejemplo de registro")

Ahora que tiene configurado un `enrollID`, puede utilizar este ID al desplegar, invocar y consultar código de encadenamiento en los siguientes pasos.
### Despliegue del código de encadenamiento
Para poder desplegar el código de encadenamiento a través de la interfaz REST, el código de encadenamiento debe estar almacenado en un repositorio GitHub público. Cuando envía una solicitud de despliegue a un igual, se especifica el URL del repositorio del código de encadenamiento y los parámetros para inicializar el código de encadenamiento.

**Antes de desplegar** el código de encadenamiento, verifique que se crea localmente:
1. Abra un indicador de mandatos y vaya al directorio que contiene `chaincode_start.go`. Escriba el siguiente mandato:
	```
	go build ./
	```
1. Expanda la sección de API **Chaincode**.
1. Expanda la sección `POST /chaincode`.
1. Establezca el campo de texto `DeploySpec` (haga que los demás campos estén en blanco) con el siguiente código de ejemplo, especificando la vía de acceso del repositorio del código de encadenamiento y el `enrollID` del paso `/registrar` anterior. `"path":` debe ser parecido a: `"https://github.com/johndoe/learn-chaincode/finished"`. Es la vía de acceso a la bifurcación del repositorio, más a vía de acceso al archivo chaincode_finished.go:

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

  El *Cuerpo de la respuesta* debería tener el siguiente aspecto:

  ![Ejemplo de despliegue](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/deploy_response.PNG "Cuerpo de respuesta del ejemplo de despliegue")

  La respuesta para el despliegue incluirá el ID para este código de encadenamiento. El ID es un hash alfanumérico de 128 caracteres, que puede utilizar para futuras solicitudes de invocación o consulta. Copie este ID en el editor de texto.

#### Consultar
Consulte el código de encadenamiento para el valor de la clave `hello_world`, que establece con la función `Init`:
1. Expanda la sección de API **Chaincode**.
1. Expanda la sección `POST /chaincode`.
1. Rellene el campo de texto `QuerySpec` (haga que los demás campos estén en blanco) con el siguiente ejemplo, especificando el ID de código de encadenamiento del paso de despliegue anterior y el `enrollID` del paso `/registrar` anterior.

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
  El *Cuerpo de la respuesta" debería tener el siguiente aspecto:

  ![Ejemplo de consulta](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query_response.PNG "Cuerpo de respuesta del ejemplo de consulta")

  El valor de `hello_world` es "hi there", que se ha establecido por el cuerpo de la llamada de despliegue anterior.

#### Invocar
Llame a la función de grabación genérica con `invoke`. Cambie el valor de `hello_world` por "go away":
1. Expanda la sección de API **Chaincode**.
1. Expanda la sección `POST /chaincode`.
1. Rellene el campo de texto `InvokeSpec` (haga que los demás campos estén en blanco) con el siguiente ejemplo, especificando el ID de código de encadenamiento del paso de despliegue anterior y el `enrollID` del paso `/registrar` anterior.

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
  El *Cuerpo de la respuesta" debería tener el siguiente aspecto:

  ![Ejemplo de invocación](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/invoke_response.PNG "Cuerpo de respuesta del ejemplo de invocación")

  Vuelva a ejecutar la consulta anterior y debe obtener la siguiente respuesta:

  ![Ejemplo de consulta2](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query2_response.PNG "Respuesta del ejemplo de invocación")

Acaba de completar la grabación de un código de encadenamiento básico.  

<br>
## Requisitos para las demos Mármoles, Papel comercial y Alquiler de coches
{: #requirements}

Los siguientes requisitos se incluyen con el servicio de Bluemix para ejecutar localmente las aplicaciones Mármoles, Papel comercial y Alquiler de coches. El entorno de Bluemix clona Hyperledger Fabric para que proporcione estas dependencias:

- ID de Bluemix https://console.ng.bluemix.net/ (necesario para crear la red de IBM Blockchain y proporcionar credenciales de servicio para iguales y la entidad emisora de certificados)
- Node.js 0.12.0+ y npm v2+
- Entorno de Golang (necesario solo para crear su propio código de encadenamiento)

Las demos requieren un dominio de Node.js y el módulo express. También debe tener una comprensión conceptual de 'chaincode', 'ledger' y 'peer' en un contexto de blockchain; consulte el [Glosario de Hyperledger Fabric](https://github.com/hyperledger/fabric/blob/master/docs/glossary.md).  

<br>
## Utilización de la demo Mármoles
{: #marbles}

La aplicación Mármoles demuestra una simple transferencia de activos entre dos partes. La aplicación se ha diseñado para probar el SDK de JavaScript, guiar su desarrollo y ayudar a los desarrolladores a familiarizarse con el SDK y el código de encadenamiento.

Explore las [Guías de aprendizaje de Mármoles](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md) para aprender cómo trabajan juntos la aplicación web, el SDK y el código de encadenamiento. Si ya está familiarizado con el código de encadenamiento e IBM Blockchain, puede  [desplegar manualmente](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#) la demo en Bluemix, o pulsar el botón Desplegar en Bluemix para utilizar la aplicación web:
  
[![Desplegar en Bluemix](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)(https://bluemix.net/deploy/button.png)]  

<br>
## Utilización de la demo Papel comercial
{: #commercialpaper}

La aplicación Papel comercial demuestra cómo puede implementarse una red de comercio de papel comercial utilizando IBM Blockchain. La demo Papel comercial explora una red de blockchain autorizada, en la que los participantes tienen roles asignados y sus correspondientes niveles de acceso. Visite el [archivo README de Papel comercial](https://github.com/IBM-Blockchain/cp-web#readme) para obtener más información sobre los componentes de esta demo, o desplegarla inmediatamente en Bluemix para ver la red comercial en acción:
  
[![Desplegar en Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)(https://bluemix.net/deploy/button.png)]  

<br>
## Utilización de la demo Alquiler de coches
{: #carlease}

La aplicación Alquiler de coches demuestra el ciclo de vida de un vehículo, desde la fabricación pasando por una serie de propietarios y terminando con el desguace del vehículo. La demo utiliza Node.js para la programación de lado del servidor y Golang para la ejecución del código de encadenamiento que se ejecuta en la red de IBM Blockchain. La demo incluye dos instancias del código de encadenamiento: una define las reglas para las transacciones del vehículo y la otra registra todas las transacciones del vehículo durante su ciclo de vida. Los dos programas de código de encadenamiento utilizan objetos JSON para almacenar datos. Visite el [archivo README de Alquiler de coches](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) para obtener más información sobre la arquitectura de la aplicación y los atributos del vehículo asociado con esta demo, o desplegar la demo inmediatamente en Bluemix:
  
[![Desplegar en Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)(https://bluemix.net/deploy/button.png)]  

<br>
## Código de encadenamiento no determinista
{: #ndcc}

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

<!---## Using the Node.js SDK
{: #nodesdk}

Use the [Hyperledger fabric client SDK ](https://github.com/IBM-Blockchain/ibm-blockchain-js/blob/master/README.md) library for easier interaction with an IBM Blockchain network.  The SDK, through importing packages and libraries, allows for an application developer to build Node.js applications that can invoke functionality on the blockchain network from the client side.  Member services and asset management are now pluggable components on client side applications.  See the [Enhanced Node.js SDK](etn_sdk.html) section for full documentation and application examples.--->
