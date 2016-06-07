---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Sample apps and tutorials for {{site.data.keyword.blockchain}}
{: #1stanchor}
*Last updated: 2 June 2016*

Sample applications and tutorials for {{site.data.keyword.blockchainfull}} demonstrate how fundamental applications and chaincodes function in a blockchain network.  To learn more about the fabric code that is underpinning your blockchain network, visit the [Docs](https://github.com/hyperledger/fabric/tree/master/docs) section of the Linux Foundation's Hyperledger Project.  
{:shortdesc}

You can immediately deploy the Marbles, Commercial Paper or Car Lease demos to see chaincode applications in action.  Keep reading to explore the Hello Chaincode tutorial.

- [![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  **Marbles**
- [![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  **Commercial Paper**
- [![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  **Car Lease**

## Using the Hello Chaincode tutorial
{: #hellocc}
This tutorial demonstrates the basic building blocks and functionality necessary to build an elementary chaincode application. You will be incrementally building up to a working chaincode that will be able to create generic assets.
Then, you will interact with the chaincode by using the network's API. After reading and completing this tutorial, you should be able to explicitly answer the following questions:
- What is chaincode?
- How do I implement the chaincode?
- What dependencies exist?
- What are the major functions?
- How do I pass different values to my arguments?
- How do I securely enroll a user on my network?
- How do I compile my chaincode?
- How do I interact with my chaincode by using the REST API?

### What is chaincode?
Chaincode is a piece of code that lets you interact with a network's shared ledger.  Whenever you 'invoke' a transaction on the network, you are effectively calling a function in a piece of chaincode that reads and writes values to the ledger.

### Implementing your first chaincode

#### Setting up the environment
1. Download and install Golang for your operating system at [GoLang](https://golang.org/dl/).
2. Setting your GOPATH
	- If you jump right to step 3, you might encounter an error similar to this: `$GOPATH must not be set to $GOROOT`.  The $GOPATH is simply a path within your **environment variables** where your Go code and future projects will exist.  The $GOPATH must be set to get, build, and install packages outside the standard Go tree.  As a result, this path needs to be unique from the $GOROOT path - where your original go tree resides.  It's not too tricky; just create a directory and point your $GOPATH there.
	- Here's an example for a machine running Windows.
		- Create a workspace for your project:
		- C:\Users\ADMIN\Documents\GoProjects (Note that we named our workspace "GoProjects").
		- Click the **Start** menu and execute a search for "system environment variables."
		- Click **Edit the system environment variables**.
		- Make sure you are on the **Advanced** tab, then click **Environment variables**.
		- Now look through your system variables and find GOPATH and GOROOT.  If you don't see a GOPATH, simply click **New** and create one.  
		- Again, GOROOT and GOPATH are the two paths that need to be unique.  Your GOROOT is auto-generated when you install Go.  It should be C:\Go\.
		- All you need to do now is point your GOPATH to the directory you created.  Our path for **Environment Variable: GOPATH** would equal **C:\Users\ADMIN\Documents\GoProjects**.  
		- If you're still confused there are some additional resources.  Try typing `go help gopath` into your command terminal, or visit the [Go Documentation](https://golang.org/doc/install).
3. Add the Hyperledger shim code to your Go path by opening a command prompt or terminal and entering the following:

	```
	go get github.com/hyperledger/fabric/core/chaincode/shim
	```

#### Setting up GitHub
The {{site.data.keyword.blockchain}} service currently requires chaincode to be in a [GitHub](https://Github.com/) repository.
Therefore, you must register a GitHub account and set up Git locally on your computer. Go to [set up git](https://help.github.com/articles/set-up-git/) for more information.  
1. Visit [learn chaincode](https://github.com/IBM-Blockchain/learn-chaincode) and fork this repo.  
2. Now clone your fork to your $GOPATH.  
3. Notice that in this repo there are two different sets of chaincode:  [Start](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/start/chaincode_start.go) - the chaincode you will start building from, and [Finished](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/finished/chaincode_finished.go) - the chaincode that you will ultimately build.
4. Make sure that it builds in your local environment:
- Open a terminal or command prompt.
- Browse to the folder that contains `chaincode_start.go` and enter:

	```
	go build ./
	```
- It should return with no errors/text.


#### Implementing the chaincode interface
The first thing you need to do is implement the chaincode shim interface in your Golang code.
The three main functions are **Init**, **Invoke**, and **Query**.
All three functions have the same prototype; they take in a function name and an array of strings.
The main difference between the functions is when they will be called.
We will be building up to a working chaincode to create generic assets.

### Dependencies
The `import` statement lists a few dependencies that you will need for your chaincode to build successfully:
- `fmt` - contains `Println` for debugging/logging.
- `errors` - standard go error format.
- `github.com/hyperledger/fabric/core/chaincode/shim` - the code that interfaces your Golang code with a peer.

### Passing values

#### Init()
Init is called when you first deploy your chaincode.
As the name implies, this function should be used to do any initialization your chaincode needs.
In the example, you use `Init` to configure the initial state of one variable on the ledger.

In your `chaincode_start.go` file,  change the `Init` function so that it stores the first element in the `args` argument to the key "hello_world".

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

This is done by using the shim function `stub.PutState`.
The first argument is the key as a string, and the second argument is the value as an array of bytes.
This function may return an error which your code inspects and returns if present.

#### Invoke()
`Invoke` is called when you want to call chaincode functions to do real work.
Invocation transactions will be captured as blocks on the chain.
The structure of `Invoke` is simple.
It receives a `function` argument and based on this argument calls Go functions in the chaincode.

In your `chaincode_start.go` file, change the `Invoke` function so that it calls a generic write function.

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

Now that it’s looking for `write`, you need to make that function somewhere in your `chaincode_start.go` file.

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

This `write` function should look similar to the `Init` change you just did.
One major difference is that you can now set the key and value for `PutState`.
This function allows you to store any key/value pair you want into the blockchain ledger.  

#### Query()
As the name implies, `Query` is called whenever you query your chaincode state.
Queries do not result in blocks being added to the chain.  (Only deploy and invoke functions add new blocks).
You will use `Query` to read the value of your chaincode state's key/value pairs.

In your `chaincode_start.go` file, change the `Query` function so that it calls a generic read function.

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

Now that it’s looking for `read`, make that function somewhere in your `chaincode_start.go` file.

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

This `read` function is using the complement to `PutState` called `GetState`.
This shim function just takes one string argument.
The argument is the name of the key to retrieve.
Next, this function returns the value as an array of bytes back to `Query`, which in turn sends it back to the REST handler.

#### Main()
Finally, you need to create a short `main` function that will execute when each peer deploys its instance of the chaincode.
It simply starts the chaincode and registers it with the peer.
You don’t need to add any code for this function.  Both chaincode_start.go and chaincode_finished.go have a `main` function that lives at the top of the file.  The function looks like this:

```go
func main() {
	err := shim.Start(new(SimpleChaincode))
	if err != nil {
		fmt.Printf("Error starting Simple chaincode: %s", err)
	}
}
```

### Interacting with your first chaincode
The fastest way to test your chaincode is to use the REST interface on your peers.
There is a Swagger UI in the dashboard for your service instance that allows you to experiment with deploying chaincode without needing to write any additional code.

#### Swagger API
The first step is to find the Swagger API page:

1. Log in to [Bluemix](https://console.ng.bluemix.net/login)
1. You probably landed on the dashboard, but double check the top nav bar.  Click the **Dashboard** tab if you are not already there.
1. Also make sure you are in the same Bluemix "space" that contains your IBM Blockchain service. The space navigation is on the left.
1. There is a **Services** panel on this Bluemix dashboard near the bottom.  Look through your services and click your IBM Blockchain service square.
1. Now you should see a white page with the words "Welcome to the IBM Blockchain..." and there should be a teal **LAUNCH** button on the right. Click it.
1. You are on the monitor page and you should see two tables, though the bottom one may be empty.
	- Noteworthy information on the network tab:
		- **Peer Logs** will be found in the top table. Find the row for **peer 1** and then click the file icon in the last row.
			- It should have opened a new window. Congratulations you found your peer logs!
			- In addition to this static view there are live **streaming peer logs** in the **View Logs** tab near the top of the page.
		- **ChainCode Logs** will be found in the bottom table. There is one row for each chaincode, and they are labeled using the same chaincode hash that was returned to you when it was deployed. Find the chaincode ID you want, and then select the peer. Finally click the file icon.
			- It should have opened a new window. Congratulations you've found your peer's chaincode logs!
	- **Swagger Tab** is the one labeled **APIs**. Click it to see the API interactive documentation.
		- You are now on your Swagger API page.
1. You should be familiar with this entire process if you already created a service instance back on **Getting Started**.
### Implementing secure enrollment
Calls to the `/chaincode` endpoint of the REST interface require a secure context ID.
This means that you must pass in a registered enrollID from the service credentials list in order for most REST calls to be accepted.
- Click the link **+ Network's Enroll IDs** to expand a list of enrollIDs and their secrets for your network.
- Open a notepad and copy a set of credentials.  You will need them later.
- Expand the **Registrar** API section by clicking it.
- Expand the `POST /registrar` section by clicking it.
- Set the body's text field.  It should be JSON that contains an enrollID and secret from your list above. Example:


![Register Example](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/registrar.PNG)

The response body should look like:

![Register Example](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/register_response.PNG)

Now that you have enrollID set up, you can use this ID when deploying, invoking, and querying chaincode in the subsequent steps.

### Deploying the chaincode
In order to deploy chaincode through the REST interface, you will need to have the chaincode stored in a public git repository.
When you send a deploy request to a peer, you send it the url to your chaincode repository, as well as the parameters necessary to initialize the chaincode.

**Before you deploy** the code, make sure it builds locally!
- Open a terminal/command prompt.
- Browse to the folder that contains `chaincode_start.go` and type:

	```
	go build ./
	```
- It should return with no errors/text.


- Expand the **Chaincode** API section by clicking it.
- Expand the `POST /chaincode` section by clicking it.
- Set the `DeploySpec` text field (make the other fields blank). Copy the example below but substitute in your chaincode repo path. Also use the same enrollID you used in the `/registrar` step.
- The `"path":` will look something like this: `"https://github.com/johndoe/learn-chaincode/finished"`.  It's the path of your fork and then one directory down, where your chaincode_finished.go file lives.

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

The response should look like:

![Deploy Example](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/deploy_response.PNG)

The response for the deployment will contain an ID that is associated with this chaincode.  The ID is a 128 character alphanumeric hash.  
This is how you will reference the chaincode in any future invoke or query requests, so copy this ID to your notepad as well.  

#### Query
Next, query the chaincode for the value of the `hello_world` key you set with the `Init` function.
- Expand the **Chaincode** API section by clicking it.
- Expand the `POST /chaincode` section by clicking it.
- Set the `QuerySpec` text field (make the other fields blank). Copy the example below but substitute in your chaincode name (the hashed ID from deploy). Also use the same enrollID you used in the `/registrar` step.

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
The response should look like:

![Query Example](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query_response.PNG)

Hopefully you see that the value of `hello_world` is "hi there".
This was set by the body of the deploy call you sent earlier.

#### Invoke
Next, call your generic write function with `invoke`.
Change the value of `hello_world` to "go away".
- Expand the **Chaincode** API section by clicking it.
- Expand the `POST /chaincode` section by clicking it.
- Set the `InvokeSpec` text field (make the other fields blank). Copy the example below, but substitute in your chaincode name (the hashed ID from deploy). Also use the same enrollID you used in the `/registrar` step.

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

The response should look like:

![Invoke Example](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/invoke_response.PNG)

To test if it's stuck, just re-run the query above, and you should get:

![Query2 Example](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query2_response.PNG)

That’s all it takes to write basic chaincode.


## Requirements for Marbles, Commercial Paper, and Car Lease demos
{: #requirements}

The following prerequisites are necessary to run the Marbles, Commercial Paper, and Car Lease applications:

- Bluemix ID https://console.ng.bluemix.net/ (needed to create your IBM Blockchain network).
- Node.js 0.12.0+ and npm v2+ (only needed if you want to run the app locally, npm comes with Node.js).
- Node.js + express experience. Marbles is a very simple blockchain app but it's still a fairly involved node app. You should be comfortable with node and the express module.
- Golang Environment (needed only to build your own chaincode, not needed if you just run the application as-is).
- You have a conceptual understanding of the terms 'chaincode', 'ledger', and 'peer' in a blockchain context. See the [Hyperledger Project Glossary](https://github.com/hyperledger/fabric/blob/master/docs/glossary.md) for more information on blockchain terminology.

## Using the Marbles demo
{: #marbles}

The Marbles application demonstrates a simple asset transfer between two parties.  The expectations of this application are to test the JavaScript SDK, guide its development, and help a developer become familiar with the SDK, + chaincode.

Explore the [Marbles Tutorials](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md) to learn how the web application, SDK and chaincode operate together.  If you're already familiar with chaincode and IBM Blockchain, you can [manually deploy](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#) to Bluemix or use the web application. [![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)

## Using the Commercial Paper demo
{: #commercialpaper}

The Commercial Paper (CP) application demonstrates how a commercial paper trading network might be implemented by using the IBM Blockchain service. The CP demo explores a permissioned blockchain network in which participants are assigned roles and corresponding levels of access.  Visit the [Commercial Paper README](https://github.com/IBM-Blockchain/cp-web#readme) to learn more about the components of this demo or deploy immediately to Bluemix and see the trading network in action. [![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)

## Using the Car Lease demo
{: #carlease}

The Car Lease application demonstrates the lifecycle of a vehicle from creation to manufacture, through a series of owners, and finishing with the vehicle being scrapped. The demo makes use of Node.js for the server side programming, with Golang used for the chaincode running on the IBM Blockchain network. The demo has two chaincodes, the first defines the rules about what can and can't happen to a vehicle (similar to a v5c), and the second stores a log of what has happened to a vehicle during its lifetime. Both chaincodes use JSON objects to store their data.  Vist the [Car Lease README](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) to learn more about the application architecture and vehicle attributes associated with this demo, or deploy immediately to Bluemix.  [![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)

## Using Node SDK
{: #nodesdk}

Use the [Node.js SDK](https://github.com/IBM-Blockchain/ibm-blockchain-js/blob/master/README.md) for easier interaction with IBM Blockchain chaincode.  Pay specific attention to the `ibc.load()` function.  This is a function that wraps a typical startup using a standard IBM Blockchain Network.  This allows you to integrate your network, registry and chaincodes with the Bluemix network.  

## Using a web application
{: #appjs}

View the source code for the [app.js](https://github.com/IBM-Blockchain/marbles/blob/master/app.js) to understand the interaction between the web application, SDK, and chaincode.  You can use this code as a template when developing your own web app.  

One interesting dynamic is the interaction between the web application and the JavaScript SDK.  Your application interacts with a peer on the network through a REST HTTP call. The SDK then abstracts the details of the REST call away, and allows you to use dot notation to call GoLang functions.  The code snippet below shows where the JavaScript SDK is a required variable in your application:

```javascript
// =========================================
var part1 = require('./utils/ws_part1');
var part2 = require('./utils/ws_part2');
var ws = require('ws');
var wss = {};
var Ibc1 = require('ibm-blockchain-js');
var ibc = new Ibc1();
// =========================================
```
{: codeblock}
