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
Última actualización: 08 de noviembre de 2016
{: .last-updated}

Los siguientes ejemplos demuestran cómo las aplicaciones y el código de encadenamiento funciona en una red de IBM Blockchain de prueba. Para obtener más información sobre cómo el código de Hyperledger Fabric v0.6, que respalda las redes de IBM Blockchain, visite los [Documentos de Fabric](https://github.com/hyperledger/fabric/tree/v0.6/docs) para el Hyperledger Project de la Linux Foundation.  
{:shortdesc}

Para experimentar aplicaciones de código de encadenamiento en acción, puede desplegar inmediatamente la demo Mármoles, Papel comercial o Alquiler de coches que se muestra a continuación (pulse un botón Desplegar en Bluemix). O, siga leyendo para explorar la guía de aprendizaje Hello Chaincode.

- [![Desplegar en Bluemix](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)(https://bluemix.net/deploy/button.png)]  **Mármoles**
- [![Desplegar en Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)(https://bluemix.net/deploy/button.png)]  **Papel comercial**
- [![Desplegar en Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)(https://bluemix.net/deploy/button.png)]  **Alquiler de coches**  

<br>
## Estudie la guía de aprendizaje de código de encadenamiento
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
El código de encadenamiento es código Go (Golang) o Java que permite a los usuarios interactuar con un red de blockchain. Siempre que 'invoca' una transacción en la red está llamando a una función en un código de encadenamiento que lee y graba valores en el libro mayor.  

<br>
## Configuración del entorno de desarrollo
Para empezar a desarrollar código de encadenamiento, instale primero las siguientes dependencias y herramientas recomendadas:

### Git

- [Página de descarga de Git](https://git-scm.com/downloads)
- [Libro de Pro Git](https://git-scm.com/book/en/v2)
- [Git Desktop (una alternativa a la CLI de Git)](https://desktop.github.com/)

Git es una herramienta de control de versiones potente y rápida, y para desarrollo de software en general. Git Bash, que está instalado con Git para Windows, es el terminal de línea de mandatos recomendado.

Después de finalizar las instalaciones de Git, compruebe que Git esté instalado:

```
$ git version
git version 2.9.0.windows.1
```

Después de haber instalado Git, cree una cuenta para usted en [GitHub](https://github.com/). El servicio de IBM Blockchain en Bluemix requiere que el código de encadenamiento esté en un repositorio de GitHub para su despliegue a través de la API REST.  

## Go

Go es actualmente el único lenguaje soportado para escribir código de encadenamiento en Bluemix. La instalación de Go incluye un conjunto de herramientas de CLI útiles para escribir código de encadenamiento. Por ejemplo, el mandato `go build` le permite compilar su código de encadenamiento antes de intentar desplegarlo en una red. Instale Go v1.6, que es la versión usada para desarrollar Hyperledger Fabric v0.6:  

- [Instalación de Go 1.6](https://golang.org/dl/#go1.6.3)
- [Instrucciones de instalación de Go](https://golang.org/doc/install)
- [Documentación y guías de aprendizaje de Go](https://golang.org/doc/)

Compruebe que Go esté correctamente instalado ejecutando los siguientes mandatos. La salida del mandato `go version` puede variar, dependiendo del sistema operativo:

```
$ go version
go version go1.6.3 windows/amd64

$ echo $GOPATH
C:\gopath
```

Su variable de entorno `GOPATH` no tiene que coincidir con el ejemplo anterior, pero tiene que usar un directorio válido del sistema de archivos. Al ejecutar `go build` para verificar que su código de encadenamiento se compila, Go busca en el directorio `$GOPATH/src` dependencias no estándar que liste en el bloque `import` de su código de encadenamiento. El manual [Instrucciones de instalación de Go](https://golang.org/doc/install) le guiará por la configuración de la variable de entorno GOPATH.  

<br>
## Hyperledger Fabric

Se da soporte a dos versiones de Hyperledger Fabric para Blockchain en Bluemix: v0.5 y v0.6.  Tal como se describe a continuación, su versión de código de encadenamiento debe alinearse con la versión de Hyperledger de su red Bluemix.

Atención:
1. Para habilitar las funciones de lectura y escritura del libro mayor, su código de encadenamiento debe importar el corrector de compatibilidad de código de encadenamiento de Hyperledger Fabric.
2. Para compilar su código de encadenamiento localmente, debe haber especificado la ubicación del código de Hyperledger Fabric en su variable de entorno `GOPATH`.

Para determinar qué versión de Hyperledger Fabric ejecuta su instancia de Bluemix, pulse el separador **Estado del servicio** en el monitor del panel de control. Desplácese hasta la sección **Notas del release**; el panel `Su red utiliza esta versión` mostrará el **Nivel de confirmación de Hyperledger** que está ejecutando:

![Versión de programa de fondo Bluemix](images/fabricversion.png "Versión de programa de fondo Bluemix")
Figura 1. Versión de Hyperledger Fabric

La versión de su código de encadenamiento debe alinearse con la versión de Hyperledger Fabric en la que se despliegue su código de encadenamiento. Por ejemplo, la red descrita en la figura 1, requiere clonar Hyperledger Fabric v0.6-preview codebase. El codebase de Fabric, para cualquier versión, debe almacenarse en la vía de acceso `$GOPATH/hyperledger/fabric`:

- [v0.5 Hyperledger Fabric](https://github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview)
- [v0.6 HHyperledger Fabric](https://gerrit.hyperledger.org/r/gitweb?p=fabric.git;a=shortlog;h=refs/heads/v0.6)

Para instalar el codebase de Hyperledger Fabric v0.5, utilice el siguiente mandato git clone:

```
# Create the parent directories on your GOPATH
mkdir -p $GOPATH/src/github.com/hyperledger
cd $GOAPTH/src/github.com/hyperledger

# Clone the appropriate release codebase into $GOPATH/src/github.com/hyperledger/fabric
# Note that the v0.5 release is a branch of the repository.  It is defined below after the -b argument
git clone -b v0.5-developer-preview https://github.com/hyperledger-archives/fabric.git
```

Para instalar el codebase de Hyperledger Fabric v0.6, utilice el siguiente mandato git clone:

```
# The v0.6 release exists as a branch inside the Gerrit fabric repository
git clone -b v0.6 http://gerrit.hyperledger.org/r/fabric
```

Si no se instala correctamente el entramado en `GOPATH`, la creación de su código de encadenamiento devolverá un error parecido al del siguiente ejemplo:
```
$ go build .
chaincode_example02.go:27:2: cannot find package "github.com/hyperledger/fabric/core/chaincode/shim" in any of:
        C:\Go\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOROOT)
        C:\gopath\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOPATH)
```

### Configurar su conducto de desarrollo

Utilice los siguientes pasos para configurar un conducto para escribir, crear y probar su código de encadenamiento. Escribirá el código de encadenamiento en su máquina local, comprobará que compila y lo cargará a GitHub. Desplegará y probará su código de encadenamiento en la red de Bluemix usando la API REST del entramado:

1. Bifurque la versión adecuada del repositorio [learn chaincode](https://github.com/IBM-Blockchain/learn-chaincode) de su versión de red en su cuenta de GitHub. Bifurque v1.0 para una red Fabric v0.5 o bifurque v2.0 para una red Fabric v0.6. Una opción es utilizar el botón **Bifurcar**, situado en la parte superior derecha de la página del repositorio. La bifurcación copia todo el repositorio en su máquina local, incluidas todas las ramas, que aparecen al pulsar el botón **Rama:** de la parte superior izquierda de la página. Para bifurcar con la CLI, especifique los siguientes mandatos en la shell de Git Bash:

2. Clone su bifurcación en su $GOPATH:

  ```bash
  cd $GOPATH
  mkdir -p src/github.com/<YOUR_GITHUB_ID_HERE>/
  cd src/github.com/<YOUR_GITHUB_ID_HERE>/
  git clone -b v1.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  OR
  git clone -b v2.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  ```

  Ahora tiene una copia de su bifurcación en la máquina local. Escribirá el código de encadenamiento cambiando o añadiendo archivos locales, enviándolos a su bifurcación en GitHub y desplegando luego su código de encadenamiento en su red de blockchain con la API REST en un igual de red.

3. Se suministran dos versiones del código de encadenamiento usado en esta guía de aprendizaje: **start** es el código de encadenamiento esqueleto desde el que empezará, y **finished* es el código de encadenamiento completado que está listo para crear. Primero, asegúrese de que **start** se crea en su entorno local:

  ```bash
  cd $GOPATH/src/github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/start
  go build ./
  ```

La versión **start** de learn-chaincode debe compilarse sin errores ni mensajes. Si no es así, revise las instrucciones anteriores para instalar Go correctamente.

5. Escriba cambios en sus archivos de código de encadenamiento locales, y envíe los archivos actualizados a su bifurcación de GitHub:

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

#### Implementar la interfaz de código de encadenamiento
Su siguiente paso es implementar la interfaz shim de código de encadenamiento en el código Go. Las tres funciones principales son **Init**, **Invoke** y **Query**. Las tres funciones toman un nombre de función y una matriz de series como entrada, pero se llaman en puntos diferentes. Su vía de acceso de desarrollo finaliza con el código de encadenamiento en funcionamiento que crea activos genéricos para intercambio en una red blockchain.

### Dependencias
La sentencia `import` lista las dependencias para crear código de encadenamiento:
1. `fmt` - contiene `Println` para su depuración/registro.
2. `errors` - formato de error de Go estándar.
3. `github.com/hyperledger/fabric/core/chaincode/shim` - código que interrelaciona el código de Golang con un igual de red.

#### Init()
La función `Init` se llama al desplegar por primera vez el código de encadenamiento. Como su nombre indica, utilice esta función para inicializar su código de encadenamiento. En este ejemplo, `Init` configura el estado inicial de un par valor/clave único del libro mayor.

En el archivo `chaincode_start.go`, cambie la función `Init` de modo que almacene el primer elemento `args` en la clave "hello_world":

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

Esto se lleva a cabo utilizando la función stub `stub.PutState`. Esta función interpreta el primer argumento enviado en la solicitud de despliegue como el valor que se guardará en la clave 'hello_world'. Si se produce un error porque se ha pasado el número erróneo de argumentos, o algo no ha ido bien al escribir en el libro mayor, esta función devuelve un error. En caso contrario, sale sin problemas, sin devolver mensajes.  

#### Invoke()
Utilice la función `Invoke` para llamar a las funciones de código de encadenamiento para que hagan el "trabajo real" en la red de blockchain. Las funciones de invocación se capturan como transacciones, que se agrupan en bloques para escribir en el libro mayor. La actualización del libro mayor se logra invocando el código de encadenamiento. La estructura de `Invoke` es sencilla; recibe una función y una matriz de argumentos. En función de la función pasada por el parámetro de función en la solicitud de invocación, `Invoke` llamará a la función de ayuda o devolverá un error.

En su archivo `chaincode_start.go`, cambie la función `Invoke` para llamar a una función de escritura genérica:

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

El código busca ahora `write`, así que añada la función de escritura al archivo `chaincode_start.go`:

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

Esta función `write` debe ser parecida al cambio `Init` anterior. Ahora puede establecer la clave y el valor para `PutState`, lo que le permite almacenar todos los pares clave/valor en el libro mayor de blockchain.

#### Query()
La función `Query` se llama para consultar el estado de su código de encadenamiento, y no añade bloques a la cadena (libro mayor). Solamente las funciones de despliegue e invocación añaden nuevos bloques. Utilice `Query` para leer el valor de los pares de clave/valor del estado del código de encadenamiento.

En el archivo `chaincode_start.go`, cambie la función `Query` de modo que llame a una función de lectura genérica:

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

El código busca ahora `read`, así que añada la función 'read' al archivo `chaincode_start.go`:

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

Esta función `read` utiliza `GetState`que es el complemento a `PutState`. Esta función shim acepta únicamente un argumento de cadena: el nombre de la clave a recuperar. A continuación, esta función devuelve el valor como una matriz de bytes, a `Query`, que a su vez lo envía al manejador REST.

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
## Requisitos de demostración
{: #requirements}

Los siguientes requisitos previos, que se incluyen con el servicio de Bluemix, son necesarios para ejecutar las aplicaciones de demostración Mármoles, Papel comercial y Alquiler de coches. El entorno de Bluemix clona Hyperledger Fabric para que proporcione estas dependencias:

- ID de Bluemix https://console.ng.bluemix.net/ (necesario para crear la red de IBM Blockchain y proporcionar credenciales de servicio para iguales y la entidad emisora de certificados)
- Node.js 0.12.0+ y npm v2+
- Entorno de Golang (necesario solo para crear su propio código de encadenamiento)

Las demos también requieren un dominio de Node.js y el módulo express. También debe tener una comprensión conceptual de 'chaincode', 'ledger' y 'peer' en un contexto de blockchain; consulte el [Glosario de Hyperledger Fabric](https://github.com/hyperledger/fabric/blob/v0.6/docs/glossary.md).  

<br>
## Demo Mármoles
{: #marbles}

La aplicación Mármoles demuestra una simple transferencia de activos entre dos partes. La aplicación se ha diseñado para probar el SDK de JavaScript, guiar su desarrollo y ayudar a los desarrolladores a familiarizarse con el SDK y el código de encadenamiento.

Explore las [Guías de aprendizaje de Mármoles](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md) para aprender cómo trabajan juntos la aplicación web, el SDK y el código de encadenamiento. Si ya está familiarizado con el código de encadenamiento e IBM Blockchain, puede  [desplegar manualmente](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#) la demo en Bluemix, o pulsar el botón Desplegar en Bluemix para utilizar la aplicación web:
  
[![Desplegar en Bluemix](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)(https://bluemix.net/deploy/button.png)]  

<br>
## Demo Papel comercial
{: #commercialpaper}

La aplicación Papel comercial demuestra cómo puede implementarse una red de comercio de papel comercial utilizando IBM Blockchain. La demo Papel comercial explora una red de blockchain autorizada, en la que los participantes tienen roles asignados y sus correspondientes niveles de acceso. Visite el [archivo README de Papel comercial](https://github.com/IBM-Blockchain/cp-web#readme) para obtener más información sobre los componentes de esta demo, o desplegarla inmediatamente en Bluemix para ver la red comercial en acción:
  
[![Desplegar en Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)(https://bluemix.net/deploy/button.png)]  

<br>
## Demo Alquiler de coches
{: #carlease}

La aplicación Alquiler de coches demuestra el ciclo de vida de un vehículo, desde la fabricación pasando por una serie de propietarios y terminando con el desguace del vehículo. La demo utiliza Node.js para la programación de lado del servidor y Golang para la ejecución del código de encadenamiento que se ejecuta en la red de IBM Blockchain. La demo incluye dos instancias del código de encadenamiento: una define las reglas para las transacciones del vehículo y la otra registra todas las transacciones del vehículo durante su ciclo de vida. Los dos programas de código de encadenamiento utilizan objetos JSON para almacenar datos. Visite el [archivo README de Alquiler de coches](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) para obtener más información sobre la arquitectura de la aplicación y los atributos del vehículo asociado con esta demo, o desplegar la demo inmediatamente en Bluemix:
  
[![Desplegar en Bluemix](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)(https://bluemix.net/deploy/button.png)]  

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
