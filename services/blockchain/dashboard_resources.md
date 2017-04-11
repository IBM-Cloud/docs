---

copyright:
  years: 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Resources
{: #dashboard_resources}
Last updated: 16 March 2017
{: .last-updated}

This screen contains important network details and real-time status information for your blockchain components.  These 
components include your peer, CA, and ordering node.  Each component has four distinct 
headers - **Name**, **URL**, **Status** and **Actions**. 
{:shortdesc}

**Figure 1** shows the initial dashboard screen displaying your network components:

![Blockchain Network](images/myresources.png "My Resources")
*Figure 1. My Resources*

#### Name

The "Name" header displays the formal system-level name for your component.  We see that our components are 
named `order01`, `peer01` and `ca01`.  

#### URL

The "URL" header displays the API endpoint for each component.  These endpoints are required in order to 
target specific network components from a client-side application, and their definitions will typically 
live in a JSON-modeled configuration file that accompanies the app.  If you are customizing an application 
that requires endorsement from peers that are not part of your Org, then you will need to retrieve these 
IP addresses from the relevant admin(s) in an out-of-band operation.  Clients must be able to connect to 
any peers from which they need a response.

#### Status

The "Status" header displays the current network state of each component (e.g. Running or Stopped).

#### Actions

The "Actions" header provides buttons to start or stop your components.  It also contains a dropdown 
box that links out to your component logs.  The logs expose the remote procedure calls occurring 
between the various network components and prove useful for debugging and troubleshooting.  Experiment 
by stopping a peer and attempting to target it with a transaction; you will see gRPC connectivity errors.  Now restart the peer and attempt the transaction again; you will see a successful connection.  You can 
also leave a peer down for an extended period of time as your channel(s) continue to transact.  When the 
peer is brought back up you will notice a synchronization of the ledger through gossip protocol.  Once 
the peer has fully synchronized the ledger, you are able to perform normal invokes and queries.  

#### Service Credentials

At the top right of this screen you will notice a Service Credentials tab.  Click this tab to expose a 
JSON file containing the low-level networking information for each of your components 
(e.g. enrollID/enrollSecret for your CA).  This is the entirety of the configuration info that you will 
need for an application.  Note, however, that this file only contains your peer IP.  If you need to target 
additional peers then you will need to obtain these endpoints.   
