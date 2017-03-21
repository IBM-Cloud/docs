---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# High Security Business Network (HSBN) vNext Beta
{: #etn_overview}

The **HSBN vNext Beta** provides a turnkey solution for generating a blockchain business network.  The service quickly provisions you the network and offers a monitor for easy management and maintenance of your resources.  This straightforward process of forming and governing a network allows for more time and attention to be directed at developing and deploying business solutions. 
{:shortdesc}

**HSBN vNext Beta** networks run in a highly secured environment on LinuxONE, where the network resouces (peers, orderers, CA, source code, ledger)  are all contained within an **IBM Secure Service Container** (SSC). Features include:
* Performance optimization for peer-to-peer communication
* High availability and framework for scalability 
* Hardware encryption, tamper-proof cryptographic keys and securely encrypted virtual machines
* Secure boot with tamper-resistant software
* No root access
* FIPS compliance, high EAL protection, auditability, and crypto optimization

A subscription to the **HSNB vNext Beta** plan includes support for the following network resources:

- A crash fault tolerant ordering service
- 2 peers per member
- Up to 5 additional network members
- 5 instantiated chaincodes per member
- A member-specific Certificate Authority
- Up to 100 channels
- Default governance policies (all members are admins and can issue invitations to join the network)

See the [IBM Secure Service Container](etn_ssc.html) section for more details on environment security features.

## Using the HSBN vNext Beta plan
{: #use_hsbn}

### Plan Access

The IBM Blockchain on Bluemix **HSBN vNext Beta** plan is granted by request. When you select HSBN vNext Beta from the Bluemix Catalog and create a service instance, your request to participate in the latest Beta release is sent to the IBM Blockchain team. Once approved, you will receive an email invitation to participate in the plan; follow the instructions to launch the HSBN vNext Beta plan dashboard.

On the HSBN vNext Beta dashboard, select from the three options:
1. **Network Quick Start**: Create an HSBN vNext Beta network, and invite other Bluemix Orgs to join.
2. **Join Network**: View invitations for you to join other HSBN vNext Beta networks.
3. **Monitor Network**: Manage your network resources - peers, channels and chaincode.

<!-- to do - the rest of this page final edit -->

### Sample Scenario

Let's assume you are a marble manufacturer, and want to leverage the IBM Blockchain network to transact with different vendors. How might this work?  You could create a consortium channel containing all network members and the current state of your publicly-available marble repository.  Any transactions occurring on this channel will be visible and query-able for all members on the network.  However, you could also create "sub-channels" or standalone channels in order to accomodate privacy and confidentiality concerns.  Say for instance that you are offering a certain vendor a better price if they meet a certain set of conditions.  This transaction can be conducted on the sub-channel, with the ensuing impact on your overall marble supply updated on the consortium channel.  Or perhaps you want to trade a specific class of marble that is not even available on the consortium channel.  You would simply transact with the necessary party on a standalone channel and the consortium channel's ledger would not be affected.  Channels provide a powerful mechanism for privacy because they all have unique ledgers, and only members that are subscribed and authenticated to a channel can interact with the ledger.  

### Creating a network
{: create_a_network}
The network consists of the following components:
* An ordering service responsible for authenticating transactions and ordering them into blocks for channels' ledgers.
* A member-specific Certificate Authority(CA) responsible for issuing identity material for each member's network components.
* Member-specifc peers that execute and commit transactions, and maintain a channel ledger.

On the dashboard of blockchain service, click **Network Quick Start** button and follow the wizard:
1. On the **Name your Network** page, enter the blockchain network name and the company name that will represent your member identity and then click **Next**;
2. On the next **Invite members** page, specify the relevant organizational information for the participants you wish to invite. Each will be provisioned a peer and CA upon joining the network, and all network members will maintain a ledger for any channel to which they have joined.  <br>
   **Note:** You can invite at most 5 members into a network.
3. On the **Define Governance Rules** page, you will see the network policy settings. By default, anyone in the network can create new channels and invite members.  
4. On the **Generate Certificate** page, use the **Auto generated** option to create the certificates for your Org's network components.  These x509 certificates are not exposed to the user.  
5. Finally, on the **Review summary** page, review the configuration for your network and click **Done** to bootstrap your network.

This process completes the initial setup of your network.

### Joining a network
{: invite_members}

After the network is initialized, your invitees will receive an email indicating the network you have been invited to join and instructions for joining.  Invitees will see the **Pending invites** button enabled on the HSBN vNext plan dashboard. Click the button to join the network:

1. Select the network on the list and click **Join Network**.
2. On the next screen, review the governance rules and click **Next**.
3. On the **Generate Certificate** page, enter your Organization Name and then select the **Auto generated** option.
4. On the **Review Network Summary** page, review the settings of the network and click **Done**. The settings also show the **Invited Participants** who have received invitations to join the network.

See the [Monitor](v10_dashboard.html) for instructions on creating channels and installing/instantiating chaincode.

<!-- I think all of this is adequately covered in the Monitor Section; and we already tell the story in the Sample Scenario topic above -->


<!-- From Jeff: Agreed. Commenting out all the rest sections on the page.


### Creating new channels
{: prepare_private_channels}

With the latest HSBN vNext plan, you can create a private channel, install a customized chaincode, complete the trade, and update the inventory number upon the other parties in the network make a query or propose a new transaction.

1. On the HSBN vNext plan dashboard, select **Enter Monitor**.
2. Select **Channels**, and click **New Channel**.
3. On the **Create a Channel** page, enter the channel name and choose the company that you want to make trade with by adding members. Then, click **Create** to create another private consortium channel.
4. Select **Chaincode** after you click the **Enter Monitor** button on the dashboard. You can view the chaincode that are already installed on your peer, or install a new chaincode to the peer.<br>
  **Note:** You can install at most 5 chaincode apps per peer.
5. Click **Install Chaincode** to install the smart contract to the peer. A smart contract, also known as chaincode, is the programmatic code installed and instantiated onto a channel’s peers by an appropriately authorized member. End users then invoke chaincode through a client-side application that interfaces with a network peer. Chaincode runs network transactions, which if validated, are appended to the shared ledger and modify world state. Chaincode can be developed for business contracts, asset definitions, and collectively-managed decentralized applications. You can download [this sample code](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window} to your local environment for testing.

**Note:** After you install the chaincode onto the peer, you must instantiate the chaincode by providing the initial arguments. In the case of the Marbles sample chaincode, you can input `marble1, blue, 35` in a comma separated list to indicate that you have 35 blue marble1 for trade.


### Commencing transactions
{: commence_txs}

To make transactions within your network, the trading parties must:
* Join the same channel within the network.
* Install the same version of the chaincode onto the peer that represents each organization.


Each successful transaction results in a new block appended to the blockchain, and the ledger in the levelDB updated with the new state. Other members in the network can query the ledger or the transaction history to decide the next transaction.



### Monitoring your network
{: monitor_network}

You can perform the following tasks after you click the **Enter Monitor** button on the dashboard:
* Create new channels and invite other members to join your channels to trade privately.
* Install new chaincodes to your peer to initiate or participate into new trade.
* View the changes of blocks, transactions, chaincode invocations.
* View the log on your peer.
* View the information of resources that your organization owns.
* Export a JSON file containing the low-level networking information for each of your components (such as enrollID/enrollSecret for your CA).  

See the [HSBN vNext Beta dashboard](v10_dashboard.md) for more information about the usage of each panel on the dashboard. 


-->
