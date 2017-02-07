---

copyright:
  years: 2016, 2017
lastupdated: "2017-2-6"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Developing smart contracts for {{site.data.keyword.iot_short_notm}} blockchain integration
{: #iotblockchain_link}

Use {{site.data.keyword.blockchainfull}} and the Hyperledger development environment to create and test your own smart contracts deriving from IBM-provided sample contracts.
{:shortdesc}

Develop and deploy smart contracts in the form of Golang chaincode executables. Use the {{site.data.keyword.iot_short_notm}} blockchain integration to trigger contract updates and business logic execution with device event data and write a new ledger state to the blockchain for each transaction.

A {{site.data.keyword.iot_short_notm}} blockchain integration development environment consists of the following components:

- {{site.data.keyword.Bluemix_notm}} organization:
  - {{site.data.keyword.iot_short_notm}} service with IoT blockchain integration enabled
  - {{site.data.keyword.blockchainfull_notm}} fabric
  - Node-RED application running IoT device simulator  

**Note:** You can also use a locally deployed Node-RED environment to run the simulator.

- Local environment:
  - Hyperledger development environment to develop and test smart contract chaincode. The environment includes GoLang.
  - Blockchain Monitoring UI
- GitHub environment:
  - IBM-provided GitHub repository for sample smart contracts
  - GitHub repository for deploying smart contracts to the {{site.data.keyword.blockchainfull_notm}} fabric

The following diagram illustrates {{site.data.keyword.iot_short_notm}} blockchain integration development environment:
![The IoT blockchain {{site.data.keyword.iot_short_notm}} integration architecture.](images/architecture_contracts.svg "IoT blockchain {{site.data.keyword.iot_short_notm}} integrationarchitecture")

## Before you begin

{: #byb}

Get an overview of {{site.data.keyword.blockchainfull_notm}}, how it relates to the general blockchain concept, and what it can do for you:
- [{{site.data.keyword.blockchainfull_notm}}](http://www.ibm.com/blockchain/) on IBM.com.
- [{{site.data.keyword.blockchainfull_notm}} DOCS](https://console.ng.bluemix.net/docs/services/blockchain/index.html) -  Getting started with {{site.data.keyword.blockchainfull_notm}} service.
- [{{site.data.keyword.blockchainfull_notm}} API](https://ibmblockchainapi.mybluemix.net/swagger/ui.html?scheme=http&host=127.0.0.1:3000&basepath=/) -  An overview of the {{site.data.keyword.blockchainfull_notm}} API.
- [{{site.data.keyword.blockchainfull_notm}} for Developers](http://www.ibm.com/blockchain/for_developers.html)  - An overview of how blockchain fits into your development environment that includes walk-throughs with live demos and code that is deployable to run on {{site.data.keyword.Bluemix_notm}}.

## Sample smart contracts

{: #samples}

A number of sample contracts are available for download from [https://github.com/ibm-watson-iot/blockchain-samples](https://github.com/ibm-watson-iot/blockchain-samples). You can use the sample contracts as a foundation to develop your own use cases into deployable chaincode:

|Sample contract |Description |
|:---|:---|
|[Basic: Simple Contract](https://github.com/ibm-watson-iot/blockchain-samples/tree/master/contracts/basic/simple_contract) | A simplified version of the advanced contract that allows you to track and store device asset data on the blockchain
|[Advanced: IoT Generic Sample Contract](https://github.com/ibm-watson-iot/blockchain-samples/tree/master/contracts/advanced/iot_sample_contract) | An advanced sample contract with many features and a **trade lane** flavour to its data model and behavior|


## Configure your {{site.data.keyword.blockchainfull_notm}} environment

{: #configure_environment}
Before you can begin deploying and testing smart contracts, you must set up your own blockchain environment.

**Note:** {{site.data.keyword.iot_short_notm}} blockchain integration supports connecting to both {{site.data.keyword.blockchainfull_notm}} fabrics and Hyperledger fabrics. The following examples are based on the usage of {{site.data.keyword.blockchainfull_notm}}.

1. Create and configure your {{site.data.keyword.blockchainfull_notm}} fabric.
{{site.data.keyword.iot_short_notm}} blockchain integration requires the {{site.data.keyword.blockchainfull_notm}} fabric to manage the blockchain ledger, smart contracts, and the general blockchain infrastructure. {{site.data.keyword.Bluemix_notm}} blockchain integration uses {{site.data.keyword.blockchainfull_notm}} to manage the chains. If you have access to an existing {{site.data.keyword.blockchainfull_notm}} environment, you can use it. If not, you must create an instance of {{site.data.keyword.blockchainfull_notm}} from the {{site.data.keyword.Bluemix_notm}} [catalog](https://console.ng.bluemix.net/catalog/services/blockchain/).

  1. From your {{site.data.keyword.Bluemix_notm}} account Dashboard, click **Use services or APIs**.
  2. Locate the Application Services section of the service catalog and select **Blockchain**.  
   **Tip:** Click [here](https://console.ng.bluemix.net/catalog/services/blockchain/) to go directly to the {{site.data.keyword.blockchainfull_notm}} service page.
  3. On the {{site.data.keyword.blockchainfull_notm}} service page, verify the Add Service selections:  
    - Space - If you have more than the default `dev` space, verify that you are deploying the service in the intended space.
    - App - Leave unbound.
    - Service name - Optionally, change the service name to something that is easy to remember. This name is displayed in the {{site.data.keyword.blockchainfull_notm}} tile in the {{site.data.keyword.Bluemix_notm}} dashboard.
    - Selected plan - Select the free plan. The free plan provides two validating peers and one certificate authority.
  4. Click **Create** to deploy {{site.data.keyword.blockchainfull_notm}} to {{site.data.keyword.Bluemix_notm}}.  
  The blockchain is deployed with two peer nodes initially. You can add more nodes as needed.

4. Link {{site.data.keyword.iot_short_notm}} to your {{site.data.keyword.blockchainfull_notm}} service  
    To write to the blockchain from {{site.data.keyword.iot_short_notm}}, you must first link the services.
     1. In {{site.data.keyword.Bluemix_notm}}, go to the Dashboard
     2. Select the space in which you deployed {{site.data.keyword.blockchainfull_notm}}.
     3. Click the **Blockchain** tile.
     4. In the left pane, click **Service credentials**.
     5. Select a set of service credentials or click **Add credentials** to create a new set of service credentials and give them a descriptive name, such as "IoT-Platform-integration."
     6. In the JSON-formatted service credentials, make a note of the following parameters:  
      - Peer information: `api_host` and `api_port`
      - User of type 1 (client) information: `username` and `secret`  

      Example of service credentials:
     ```json
     {
      "credentials": {
      "peers": [
      {
       "discovery_host": "169.44.63.203",
       "discovery_port": "32904",
       "api_host": "169.44.63.203",
       "api_port_tls": "443",
       "api_port": "80",
       "type": "peer",
       "network_id": "f621cde2-bdec-4897-b737-da4df144c41f",
       "container_id": "5750f7734fb06c64d70c443b1dfcf39a3f5de7b51b792294c05dbdbe7d8356f7",
       "id": "f621cde2-bdec-4897-b737-da4df144c41f_vp1",
       "api_url": "http://169.44.63.203:32905"
      },
       ...
      ],
      "users": [
      {
       "username": "user_type1_fa8e6ef0dc",
       "secret": "33401036a9"
      },
       ...
       ]
      }
     }
     ```  
     **Important:** The user that you select must not be previously registered with a peer other than the peer that you selected.
     7. Click **Back to Dashboard** to return to your {{site.data.keyword.Bluemix_notm}} dashboard.
     8. Select the space in which you deployed {{site.data.keyword.iot_short_notm}}.
     9. Click the **{{site.data.keyword.iot_short_notm}}** tile.
     10. Click **Launch** to open the {{site.data.keyword.iot_short_notm}} dashboard.
     11. From the {{site.data.keyword.iot_short_notm}} dashboard, select **Extensions** in the menu side bar.
     12. In the **Extensions** page, in the Blockchain tile, click **Setup**, or click ![Gear icon](../images/gear.png "Configure") if you already have fabrics linked.
     13. In the Configure blockchain section, click **Add Fabric** and then enter the fabric information.
    **Note:** Blockchain integration must be enabled to add fabrics. For information, see [Blockchain](../reference/extensions/index.html#blockchain) in the External service integrations topic.
    1. In the **Fabric** tab, enter a name to identify the fabric in {{site.data.keyword.iot_short_notm}}, then click **Next**.   
    2. In the **Peer** tab, enter the peer information:  
   <table>
   <thead>
   <tr>
   <th>Parameter</th>
   <th>Value</th>
   </tr>
   </thead>
   <tbody>
   <tr>
   <td>Name</td>
   <td>Enter a name to identify the peer in {{site.data.keyword.iot_short_notm}}.</td>
   </tr>
   <tr>
   <td>Host</td>
   <td>The `api_host` address for the Validating Peer 1 server</td>
   </tr>
   <tr>
   <td>Port</td>
   <td>The `api_port` number<ul><li>Use port 80 if your implementation does not use TLS.</li><li>Use port 443 if your implementation uses TLS.</li></ul></td>
   </tr>
   <tr>
   <td>User ID</td>
   <td>The `username` string for the user that was used to register the smart contract with the blockchain. You also use this user ID when you later configure the Simple UI.</td>
   </tr>
   <tr>
   <td>Secret Key</td>
   <td>The `secret` string for the user</td>
   </tr>
   <tr>
   <td>Use TLS</td>
   <td>On or Off</br>Use Transport Layer Security to encrypt the communication between {{site.data.keyword.iot_short_notm}} and the contract in the fabric. The default port numbers are set by the deployed {{site.data.keyword.iot_short_notm}} instance that you are connecting to.</td>
   </tr></tbody>
   </table>  
    3. Click **Finish**.
     3. In the Configure blockchain section, click **Done** to save the fabric information.    

The fabric table is populated with the new fabric connection.  

## Create, test, and deploy your smart contracts
{: #test_contracts}

You can now create your own smart contract chaincode in GoLang, test it in the sandbox environment, and deploy and test it on your own {{site.data.keyword.blockchainfull_notm}} fabric.

1. Create a GitHub project to store your smart contract chaincode.  
The smart contracts that you want to deploy must be in a public GitHub repository. For more information, see https://github.com/.
2.  Set up a local Hyperledger development and testing environment.  
To develop and test your own chaincode before deploying it to {{site.data.keyword.blockchainfull_notm}}, you must set up a local development environment. This environment includes GoLang, which is used to write the chaincode for your contracts.
 1. Set up the development environment.  
 The development environment includes the tools that you need to develop your smart contracts by using the chaincode build in GoLang. For more information, see
 [Setting up the development environment](https://github.com/hyperledger/fabric/blob/master/docs/dev-setup/devenv.md) in the Hyperledger documentation.
 2. Install a chaincode debugging environment.   
 The debugging environment provides you with the tools that you need to test and debug your smart contracts before you deploy them to {{site.data.keyword.blockchainfull_notm}}. For more information, see [Writing, Building, and Running Chaincode in a Development Environment](https://github.com/hyperledger/fabric/blob/master/docs/Setup/Chaincode-setup.md) in the Hyperledger documentation.
 3. Set up a network for development.   
 The network for development provides you with a stricter, production-like, environment for final testing of your smart contracts.  Use this environment for final testing of your tested and debugged contracts before you deploy them to {{site.data.keyword.blockchainfull_notm}}. For more information, see [Setting Up a Network](https://github.com/hyperledger/fabric/blob/master/docs/Setup/Network-setup.md) in the Hyperledger documentation.

3. Optional: Download the IBM-provided sample smart contracts.  
IBM provides a number of smart contracts that you can download and use directly as-is or modify to suit your organization's goals.  
To download the sample contracts:
 1. Go to the Blockchain Samples GitHub repository at: https://github.com/ibm-watson-iot/blockchain-samples/  
 The basic_contract_hyperledger and trade_lane_contract_hyperledger folders contain the basic and trade lane contracts respectively.
 3. Use `git clone` in the terminal to clone the https://github.com/ibm-watson-iot/blockchain-samples project.  
 **Tip:** You can also download a compressed file of the project by clicking **Download ZIP** from the project page.

6. Create and test a smart contract.   
 By using {{site.data.keyword.iot_short_notm}} blockchain integration, you can upload smart contracts in the form of chaincode executables to the {{site.data.keyword.blockchainfull_notm}} to run business logic on the device data that is written to the blockchain. The smart contract chaincode is developed in GoLang.  
 The sample contract is focused on writing IoT device data for events of interest into a blockchain for sharing with third parties or to create tamper-resistant log entries.
2. Create the contract executables.  
  The contract code must be converted to an executable before it can be deployed on the blockchain.  
  **Note:** The sample contract (sample_contract_hyperledger) is already generated and can be deployed as-is.  
  Complete the following steps:
   1. Open your command line and navigate to the contract folder.
   2. Run the `go generate` command.  
   This command runs any ‘go generate’ commands that exist in the code. Go generate is a go program tool that allows pre-build code generation. In the IBM-provided example contracts, go generate is used to create the schemas.go file that outlines the contract schema and sample.go contract file.  
   **Important:** The schemas.go file is a critical component of the {{site.data.keyword.iot_short_notm}} blockchain integration. The file lets the platform confirm that the contract is compliant with the integration specification and lets the mapper see the contract API to which device events can be mapped.
   2. Run the `go build` command.  
   This command creates an executable with the same name as the folder name. The file is the contract executable that will be deployed on the blockchain.

6. Test the smart contract in the Hyperledger sandbox.  
  Before you deploy your finished smart contract to {{site.data.keyword.blockchainfull_notm}}, you can test and debug the chaincode in the Hyperledger sandbox that you installed as part of your development environment.  

6. Deploy the smart contract chaincode to {{site.data.keyword.blockchainfull_notm}}.  
 After you test and verify your contract locally, you can deploy it to your {{site.data.keyword.blockchainfull_notm}} fabric to test.
  1. Upload your contract to your public GitHub repository.  
  For example, upload the sample.go file to:  
  `http://github.com/{my organization}/{my project}/`
  2. Register the contract with the peer that you connected to earlier.  
  Use a REST client like CURL or Postman to submit the register call. For more information about the register call, see the [POST registrar API documentation](https://ibmblockchainapi.mybluemix.net/swagger/ui.html?scheme=http&host=127.0.0.1:3000&basepath=/#!/Registrar/registerUser). Use the following information when registering:
  <ul>
  <li>URL: `http://api_host:api_port/registrar`
  <li>Type: POST
  <li>Header: `Content type: application/x-www-form-urlencoded`
  <li>Payload:  
  ```json
   {  
        "enrollId": "{username}",      
        "enrollSecret": "{secret}"    
   }
   ```

  </ul>
  3. Deploy the contract to the peer.  
  For more information about the deploy call, see the [POST devops/deploy API documentation](https://ibmblockchainapi.mybluemix.net/swagger/ui.html?scheme=http&host=127.0.0.1:3000&basepath=/#!/Devops/chaincodeDeploy).  
  Use the following information when deploying:  
  <ul>
  <li>URL: `http://api_host:api_port/devops/deploy`
  <li>Type: POST
  <li>Header: `Content type: application/x-www-form-urlencoded`
  <li>Payload:  
  ```
  {
      "type": "GOLANG",   
      "chaincodeID": {  
      "path": "http://github.com/{my organization}/{my project}/sample.go",
      "name": "string"
    },
    "ctorMsg": {  
      "function": "init",  
      "args": [
        "{\"version\":\"1.0\}"}"
      ]
    },
    "secureContext": "'username'",
    "confidentialityLevel": "PUBLIC"
  }
  ```  
  </ul>  
  Your contract is deployed to the fabric.  
  **Important:** Note the returned contract ID, which is in the form of a 128-character alphanumeric string. You need the contract ID to map devices to the contract.  

10. Map the device data to the new smart contract.  
  To start writing device data to the new blockchain smart contracts, you must first map device data to the contracts.  
   1. In {{site.data.keyword.Bluemix_notm}}, go to the Dashboard
   2. Select the space in which you deployed {{site.data.keyword.iot_short_notm}}.
   3. Click the **{{site.data.keyword.iot_short_notm}}** tile.
   4. Click **Launch** to open the {{site.data.keyword.iot_short_notm}} dashboard.
   5. Select **Blockchain**  by clicking ![Blockchain.](images/platform_blockchain.png "Blockchain") in the menu side bar.
   6. Click **Link Contract**.
   6. Select the fabric name for the fabric that you created earlier.
   7. Enter the following information:  
     - Contract ID - Paste in the 128-character contract ID that you saved when you deployed the contract.
     - Contract Name - Enter a name to identify the contract in {{site.data.keyword.iot_short_notm}}.
     - Select the device type for which you want to store device data in the blockchain.
     - Select the event name for the events that you want to store.  
     **Tip:** To find the event types for a device, go to the **Devices** page and click the device name to open the device details page. Scroll down to the **Sensor Information** section to see a list of the available events and data points for the device.

   11. Map the available device properties to contract parameters.   
   **Important:** Verify that the data type for each data point that you map corresponds to the data type that is required by the contract parameter that you map it to.  
   For example, a contract property such as Asset ID of the type string must be mapped to a property of the type string. The contract parameter requirements are defined in the `type` definitions in the contract go-code.  
   For example, the basic IBM-provided contract has the following contract parameter requirements:  
    <ul>
    <li>  AssetID - string
    <li>  Location - Geolocation  
    <ul>
    <li> Latitude - float64
    <li>  Longitude - float64
    </ul>
    <li>  Temperature - float64  
    <li>  Carrier - string   
    </ul>  
    For more information about how to map device data to contracts, see the [Data mapping example](https://github.com/ibm-watson-iot/blockchain-samples/wiki/Data-mapping-example) in the IoT Blockchain samples wiki on GitHub.
   12. In the summary page, verify that the information is correct.
   13. The device data to contract mapping is shown in the Blockchain page.

7. Test your smart contract in {{site.data.keyword.blockchainfull_notm}}.  
In order to test your smart contract, perform an end-to-end test by creating a device in {{site.data.keyword.iot_short_notm}}, connecting your device to {{site.data.keyword.iot_short_notm}}, configuring IoT Blockchain to connect to your blockchain fabric, and configuring {{site.data.keyword.iot_short_notm}} to map and store your device messages in the blockchain. By using the {{site.data.keyword.blockchainfull_notm}} console, you can view the blockchain to see the device data in the ledger. If your contract supports the readAsset() function, you can use the monitoring UI to view your blockchain and see the device data from your own scenario being stored indelibly in a blockchain.

5. Configure the Monitoring UI to connect to {{site.data.keyword.blockchainfull_notm}}.  
 **Tip:** If you haven't installed the Monitoring UI in your local environment, you can do it now. Follow the instructions in the Monitoring UI readme document that is available in the [Blockchain Monitoring UI](https://github.com/ibm-watson-iot/blockchain-samples/tree/master/applications/monitoring_ui) GitHub directory.  
 Access the configuration settings by clicking the **CONFIGURATION** button.   
 Use the following information to connect to a contract:
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Value</th>
<th>Comment</th>
</tr>
</thead>
<tbody>
<tr>
<td>API Host and Port</td>
<td>`http://peer_URL:port`</td>
<td>The host and port for the {{site.data.keyword.blockchainfull_notm}} REST API, which is prepended with `http://`. Use the  `api_host` address and `api_port` number. </td>
</tr>
<tr>
<td>Chaincode ID</td>
<td>The contract ID that was returned when you registered the contract.</td>
<td>The contract ID is a 128-character alphanumeric string that corresponds to the Contract ID entry.  
**Important:** When you cut and paste the contract ID, make sure that no spaces are included in the ID. If the ID is incorrectly entered, the blockchain ledger entries are displayed, but the asset search function does not work.
</td>
</tr>
<tr>
<td>Secure Context</td>
<td>Your fabric user</td>
<td>This parameter is required for connecting to {{site.data.keyword.blockchainfull_notm}} instances on {{site.data.keyword.Bluemix_notm}}. Use the `secureContext` entry.  
**Important:** The secureContext should be the `username` that you used to configure the fabric.
</td>
</tr>
<tr>
<td>Number of blocks to display</td>
<td>A positive integer. Default: 10</td>
<td>The number of blockchain blocks to display.
</td>
</tr>
</tbody>
</table>

3. In the Monitoring UI, verify that your setup is working as expected.  
Use the Monitoring UI components to interact with your blockchain contract:  
 - Chaincode operations  
 Verify that the contract-specific chaincode operations can be run as expected. For example, for the Basic contract, verify that running a `createAsset` function results in an asset being added to the blockchain.
 - Response Payloads  
 Verify that peer request responses appear as expected when you submit REST requests from the Chaincode Operations tab.
 - Blockchain  
Verify that blocks are added to the chain when you inject data from a linked device or when you use the Chaincode Operations component.    

## Next steps
{: #next_steps}

You have now deployed and explored the sample IBM-provided smart contracts. However, the basic and trade lane contracts provide limited examples of the many possibilities that well designed smart contract chaincode opens up. Now is the time to experiment and map your business scenarios to chaincode contracts in {{site.data.keyword.blockchainfull_notm}}. You can then use {{site.data.keyword.iot_short_notm}} with IoT blockchain integration to write device data to the blockchain ledger and execute business logic stored as smart contracts in response to the data.     


Happy blockchaining!
