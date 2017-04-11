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

# Sample apps and tutorials
{: #1stanchor}


The following samples demonstrate how applications and chaincode function on a test IBM Blockchain network. To learn more about the Hyperledger Fabric v0.6 code, which underpins IBM Blockchain networks, visit the [Fabric Docs](https://github.com/hyperledger/fabric/tree/v0.6/docs) for the Linux Foundation's Hyperledger  Project.  
{:shortdesc}

To experience chaincode applications in action, you can immediately deploy the Marbles, Commercial Paper or Car Lease demo below (click a Deploy to Bluemix button). Or continue reading to explore the Hello Chaincode tutorial.

- [![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  **Marbles**
- [![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  **Commercial Paper**
- [![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  **Car Lease**  

<br>
## Learn chaincode tutorial
{: #hellocc}
This tutorial guides you through using basic building blocks to code an elementary chaincode application. You will  incrementally build a working chaincode that creates generic assets for exchanging on a network. Then you will interact with your chaincode through the network API. After completing this tutorial, you will be able to answer the following questions:
- What is chaincode?
- How do I implement chaincode?
- What dependencies exist?
- What are the major functions?
- How do I pass different values to my arguments?
- How do I securely enroll a user on my network?
- How do I compile my chaincode?
- How do I interact with my chaincode through the REST API?

### What is chaincode?
Chaincode is Go (Golang) or Java code that enables users to interact with a blockchain network. Whenever you 'invoke' a transaction on the network, you are calling a function in chaincode that reads and writes values to the ledger.  

<br>
## Setting up the development environment
To start developing chaincode, first install the following dependencies and recommended tools:

### Git

- [Git download page](https://git-scm.com/downloads)
- [Pro Git book](https://git-scm.com/book/en/v2)
- [Git Desktop (an alternative to the Git CLI)](https://desktop.github.com/)

Git is a fast and powerful version control tool for chaincode development, and for software development in general. Git bash, which is installed with Git for Windows, is the recommended command line terminal.

After completing the Git installations, verify that Git is installed:

```
$ git version
git version 2.9.0.windows.1
```

Once you have Git installed, create an account for yourself on [GitHub](https://github.com/). The IBM Blockchain service on Bluemix requires  chaincode to be in a GitHub repository for deployment through the REST API.  

## Go

Go is currently the only supported language for writing chaincode on Bluemix. The Go installation includes a set of useful CLI tools for writing chaincode. For example, the `go build` command allows you to compile your chaincode before attempting to deploy it to a network. Install Go v1.6, which is the version used to develop Hyperledger Fabric v0.6:  

- [Go 1.6 install](https://golang.org/dl/#go1.6.3)
- [Go installation instructions](https://golang.org/doc/install)
- [Go documentation and tutorials](https://golang.org/doc/)

Verify that Go is properly installed by running the following commands. The output of the `go version` command can vary, depending on your operating system:

```
$ go version
go version go1.6.3 windows/amd64

$ echo $GOPATH
C:\gopath
```

Your `GOPATH` environment variable does not have to match the prior example, but you do have to use a valid directory on your filesystem. When you run `go build` to verify that your chaincode compiles, Go looks in the `$GOPATH/src` directory for any non-standard dependencies that you list in the `import` block in your chaincode. The [Go installation instructions](https://golang.org/doc/install) guide you through GOPATH environment variable setup.  

<br>
## Hyperledger Fabric

Two versions of Hyperledger Fabric are supported for Blockchain on Bluemix: v0.5 and v0.6.  As described below, your chaincode version must align with the version of Hyperledger on your Bluemix network.

Attention:
1. To enable read and write functions on the ledger, your chaincode must import the chaincode shim from Hyperledger Fabric.
2. To compile your chaincode locally, you must have the Hyperledger Fabric code location specified in your `GOPATH` environment variable.

To determine which version of Hyperledger Fabric your Bluemix instance is running, click the **Service Status** tab on your Dashboad Monitor.  Scroll down to the **Release Notes** section; the `Your network is using this version` panel will display the **Hyperledger Commit Level** that you are running:

![Bluemix backend version](images/fabricversion.png "Bluemix backend version")
Figure 1. Hyperledger Fabric version

Your chaincode version must align with the Hyperledger Fabric version that you will deploy your chaincode to. For example, the network depicted in Figure 1 requires cloning the Hyperledger Fabric v0.6-preview codebase. The fabric codebase, for either version, must be stored in your  `$GOPATH/hyperledger/fabric` path:

- [v0.5 Hyperledger Fabric](https://github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview)
- [v0.6 HHyperledger Fabric](https://gerrit.hyperledger.org/r/gitweb?p=fabric.git;a=shortlog;h=refs/heads/v0.6)

To install the Hyperledger Fabric v0.5 codebase, use the following git clone command:

```
# Create the parent directories on your GOPATH
mkdir -p $GOPATH/src/github.com/hyperledger
cd $GOAPTH/src/github.com/hyperledger

# Clone the appropriate release codebase into $GOPATH/src/github.com/hyperledger/fabric
# Note that the v0.5 release is a branch of the repository.  It is defined below after the -b argument
git clone -b v0.5-developer-preview https://github.com/hyperledger-archives/fabric.git
```

To install the Hyperledger Fabric v0.6 codebase, use the following git clone command:

```
# The v0.6 release exists as a branch inside the Gerrit fabric repository
git clone -b v0.6 http://gerrit.hyperledger.org/r/fabric
```

If the fabric is not properly installed in your `GOPATH`, building your chaincode will return an error similar to the following example:
```
$ go build .
chaincode_example02.go:27:2: cannot find package "github.com/hyperledger/fabric/core/chaincode/shim" in any of:
        C:\Go\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOROOT)
        C:\gopath\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOPATH)
```

### Set up your development pipeline

Use the following steps to set up a pipeline for writing, building and testing your chaincode. You will write chaincode on your local machine, verify that it compiles, and upload it to GitHub. You will then deploy and test your chaincode on your Bluemix network using the fabric REST API:

1. Fork the appropriate version of the [learn chaincode](https://github.com/IBM-Blockchain/learn-chaincode) repository for your network version to your GitHub account. Fork v1.0 for a v0.5 fabric network, or fork v2.0 for a v0.6 fabric network. One option is to use the **Fork** button, located at the top right of the repository page. Forking copies the entire repository to your local machine, including all branches, which are shown by clicking the **Branch:** button at the upper left of the page. To fork using the CLI, enter the following commands into your Git Bash shell:

2. Clone your fork to your $GOPATH:

  ```bash
  cd $GOPATH
  mkdir -p src/github.com/<YOUR_GITHUB_ID_HERE>/
  cd src/github.com/<YOUR_GITHUB_ID_HERE>/
  git clone -b v1.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  OR
  git clone -b v2.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  ```

  You now have a copy of your fork on your local machine. You will write chaincode by changing or adding local files, pushing them to your fork on GitHub, and then deploy your chaincode to your blockchain network using the REST API on a network peer.

3. Two versions of the chaincode used in this tutorial are provided: **start** is the skeleton chaincode that you will start from, and **finished* is your completed chaincode that is ready to build. First, make sure that **start** builds in your local environment:

  ```bash
  cd $GOPATH/src/github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/start
  go build ./
  ```

The **start** version of learn-chaincode should compile with no errors or messages. If it does not, review the prior instructions for installing Go correctly.

5. Write changes to your local chaincode files, and push the updated files to your GitHub fork:

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

#### Implement the chaincode interface
Your next step is to implement the chaincode shim interface in your Go code. The three main functions are **Init**, **Invoke** and **Query**. All three functions take a function name and an array of strings as input, but are called at different points. Your development path ends with working  chaincode that creates generic assets for exchange on a blockchain network.

### Dependencies
The `import` statement lists the dependencies for building your chaincode:
1. `fmt` - contains `Println` for debugging/logging.
2. `errors` - standard Go error format.
3. `github.com/hyperledger/fabric/core/chaincode/shim` - code that interfaces your Golang code with a network peer.

#### Init()
The `Init` function is called when you first deploy your chaincode. As the name implies, use this function to initialize your chaincode. In this  example, we `Init` configures the initial state of a single key/value pair on the ledger.

In your `chaincode_start.go` file, change the `Init` function so that it stores the first `args` element to the key "hello_world":

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

This is done by using the stub function `stub.PutState`. This function interprets the first argument sent in the deployment request as the value to be stored under the key 'hello_world'. If an error occurs because the wrong number of arguments was passed in, or because something went wrong when writing to the ledger, this function returns an error. Otherwise, it exits cleanly, returning no messages.  

#### Invoke()
Use the `Invoke` function to call chaincode functions to do "real work" on the blockchain network. Invoke functions are captured as transactions, which get grouped into blocks for writing to the ledger. Updating the ledger is achieved by invoking your chaincode. The structure of `Invoke` is simple; it receives a function and an array of arguments. Based on the function passed in by the function parameter in the invoke request, `Invoke` will either call a helper function or return an error.

In your `chaincode_start.go` file, change the `Invoke` function to call a generic write function:

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

The code is now looking for `write`, so add the write function to your `chaincode_start.go` file:

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

This `write` function should look similar to your previous `Init` change. You can now set the key and value for `PutState`, which allows you to store any key/value pair on the blockchain ledger.

#### Query()
The `Query` function is called to query your chaincode state, and does not add blocks to the chain (ledger). Only deploy and invoke functions add new blocks. Use `Query` to read the value of your chaincode state's key/value pairs.

In your `chaincode_start.go` file, change the `Query` function so that it calls a generic read function:

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

The code is now looking for `read`, so add the 'read' function to your `chaincode_start.go` file:

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

This `read` function uses `GetState`, which is the complement to `PutState`. This shim function takes only one string argument: the name of the key to retrieve. Next, this function returns the value, as an array of bytes, to `Query`, which in turn sends it to the REST handler.

#### Main()
The `main` function executes when each peer deploys its instance of the chaincode. It starts the chaincode and registers it with the peer. No code updates are required for 'main'; both chaincode_start.go and chaincode_finished.go include a `main` function at the top of each file:

```go
func main() {
	err := shim.Start(new(SimpleChaincode))
	if err != nil {
		fmt.Printf("Error starting Simple chaincode: %s", err)
	}
}
```

### Interacting with your chaincode
The fastest way to test your chaincode is to use the REST interface on your peers.
The Swagger UI on your Bluemix dashboard monitor allows you to experiment with deploying chaincode, without writing any additional code.  

#### Swagger API
Complete the following steps to use the Swagger API:

1. Log in to [Bluemix](https://console.ng.bluemix.net/login) and ensure that you are on the **Dashboard** tab.
1. Check that you are in the same Bluemix "space" that contains your IBM Blockchain service. The space navigation is on the left.
1. There is a **Services** panel near the bottom; click on your IBM Blockchain service.
1. You should see a "Welcome to the IBM Blockchain..." message; click on the **LAUNCH** button on the right.
1. On the monitor page, you should see two tables; the bottom table may be empty.
	- **Network Tab:**
		- **Peer Logs** are in the top table. In the row for **peer 1**, click the file icon to view the log. In addition to this static view, there are live **streaming peer logs** in the **View Logs** tab near the top of the page.
		- **ChainCode Logs** are in the bottom table. Each chaincode is labeled with the chaincode hash that was returned when it was deployed. Select the peer in any chaincode row, and then click the file icon to view the log.
	- **APIs Tab**: Displays the Swagger API documentation page.
1. Continue with the following steps to implement secure enrollment. Calls to the `/chaincode` endpoint in the REST interface require a secure context ID. For most REST calls to be accepted, you must pass a registered *enrollID* from the service credentials list:
  - Click **+ Network's Enroll IDs** to expand the list of *enrollID* values and their secrets.
  - Copy the set of credentials to a text file for later use.
  - Expand the **Registrar** API section.
  - Expand the `POST /registrar` section.
  - Populate the `Value` field with JSON that specifies an `enrollID` and `enrollSecret' from your credentials:

  ![Register Example](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/registrar.PNG "Register example")

  The *Response Body* should look like the following example:

  ![Register Example](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/register_response.PNG "Register example response body")

Now that you have an `enrollID` set up, you can use this ID when deploying, invoking, and querying chaincode in the following steps.
### Deploying your chaincode
In order to deploy your chaincode through the REST interface, your chaincode must be stored in a public GitHub repository. When you send a deploy request to a peer, you specify the URL for the chaincode repository, and the parameters to initialize the chaincode.

**Before you deploy** your chaincode, verify that it builds locally:
1. Open a command prompt, and browse to the directory that contains `chaincode_start.go`. Enter the following command:
	```
	go build ./
	```
1. Expand the **Chaincode** API section.
1. Expand the `POST /chaincode` section.
1. Set the `DeploySpec` text field (make the other fields blank) with the example code below, specifying your chaincode repository path, and the `enrollID` from the previous `/registrar` step. The `"path":` should look similar to: `"https://github.com/johndoe/learn-chaincode/finished"`. This is the path to your repository fork, plus the path to your chaincode_finished.go file:

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

  The *Response Body* should look similar to the following example:

  ![Deploy Example](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/deploy_response.PNG "Deploy example response body")

  The response for the deployment will contain the ID for this chaincode. The ID is a 128 character alphanumeric hash, which you can use for future invoke or query requests. Copy this ID to your text editor.

#### Query
Query your chaincode for the value of the `hello_world` key, which you set with the `Init` function:
1. Expand the **Chaincode** API section.
1. Expand the `POST /chaincode` section.
1. Populate the `QuerySpec` text field (make the other fields blank) with the following example, specifying the chaincode ID from the previous deployment step, and the `enrollID` from the previous `/registrar` step:

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
  The *Response Body" should look similar to the following example:

  ![Query Example](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query_response.PNG "Query example response body")

  The value of `hello_world` is "hi there", which was set by the body of your previous deploy call.

#### Invoke
Call your generic write function with `invoke`. Change the value of `hello_world` to "go away":
1. Expand the **Chaincode** API section.
1. Expand the `POST /chaincode` section.
1. Populate the `InvokeSpec` text field (make the other fields blank) with the following example, specifying the chaincode ID from the previous deployment step, and the `enrollID` from the previous `/registrar` step:

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
  The *Response Body" should look similar to the following example:

  ![Invoke Example](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/invoke_response.PNG "Invoke example response body")

  Re-run the query above, and you should get the following response:

  ![Query2 Example](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query2_response.PNG "Invoke example response")

You have just completed writing some basic chaincode.  

<br>
## Demo requirements
{: #requirements}

The following prerequisites, which are included with your Bluemix service, are required for running the Marbles, Commercial Paper, and Car Lease demo applications. Your Bluemix environment clones the Hyperledger Fabric to provide these dependencies:

- Bluemix ID https://console.ng.bluemix.net/ (required to create your IBM Blockchain network and provide service credentials for peers and the Certificate Authority)
- Node.js 0.12.0+ and npm v2+
- Golang Environment (required only to build your own chaincode)

The demos also require proficiency with Node.js and the express module. You must also have a conceptual understanding of 'chaincode', 'ledger', and 'peer' in a blockchain context; refer to the [Hyperledger Fabric  Glossary](https://github.com/hyperledger/fabric/blob/v0.6/docs/glossary.md).  

<br>
## Marbles demo
{: #marbles}

The Marbles application demonstrates a simple asset transfer between two parties. The application is designed to test the JavaScript SDK, guide its development, and help developers become familiar with the SDK and chaincode.

Explore the [Marbles Tutorials](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md) to learn how the web application, SDK and chaincode work together. If you arealready familiar with chaincode and IBM Blockchain, you can [manually deploy](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#) the demo to Bluemix, or  click the Deploy to Bluemix button to use the web application:  
[![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  

<br>
## Commercial Paper demo
{: #commercialpaper}

The Commercial Paper application demonstrates how a commercial paper trading network can be implemented using IBM Blockchain. The Commercial Paper demo explores a permissioned blockchain network, on which participants are assigned roles and corresponding levels of access. Visit the [Commercial Paper README](https://github.com/IBM-Blockchain/cp-web#readme) to learn more about the components of this demo, or deploy it  to Bluemix immediately to see the trading network in action:  
[![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  

<br>
## Car Lease demo
{: #carlease}

The Car Lease application demonstrates the lifecycle of a vehicle, from manufacturing, through a series of owners, and  finishing with the vehicle being scrapped. The demo uses Node.js for server-side programming, and Golang for chaincode running on the IBM Blockchain network. The demo includes two instances of chaincode: one defines the rules for vehicle transactions, and the other logs all vehicle transactions during its lifetime. Both chaincode programs use JSON objects to store data. Vist the [Car Lease README](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) to learn more about the application architecture and vehicle attributes associated with this demo, or deploy the demo immediately to Bluemix:  
[![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  

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
