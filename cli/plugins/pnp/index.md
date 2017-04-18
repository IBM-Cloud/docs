---

copyright:

  years: 2016, 2017

lastupdated: "2017-01-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Private network peering plug-in for Bluemix CLI
{: #private_network_cli}

Use the private network peering command line interface (CLI) to configure and manage private network peering between two {{site.data.keyword.Bluemix}} spaces. Private network peering is supported for IBM Containers (docker containers). The Bluemix spaces can be located in different availability zones in the same region or can be located in the different regions. The private network peering CLI plug-in is available for use with the Bluemix CLI plug-in.

The private network peering CLI plug-in is available for Windows, MAC, and Linux operating systems. Ensure that you use the plug-in that is applicable to you.

Before you begin, create Bluemix spaces. Ensure that each container in a space has an IP address from a different network. For details, see [Using your own private IP address](https://www.{DomainName}/docs/containers/container_security_network.html#container_cli_ips_byoip)

**Note:** After you use the private network peering with a Bluemix space, if you need to delete the space, first delete the private network peering connections in that space.

To get started, install the IBM Bluemix CLI. See
[Bluemix CLI](http://clis.ng.bluemix.net/ui/home.html) for details.

## Install the private network peering CLI plug-in

**Note**: If you have a previous version of the plug-in that is installed, you need to uninstall it. Use the following command to uninstall the plug-in:

```
bluemix plugin uninstall private-network-peering
```
### Install locally
Download the private network peering plug-in for your platform from [IBM Bluemix CLI plug-in repository](http://plugins.ng.bluemix.net/ui/repository.html#bluemix-plugins).

Install the private network peering plug-in by using the following command:

**Note**: Either switch to the location of the plug-in or specify the path to the plug-in location.

* For Microsoft Windows OS:

```
bluemix plugin install private-network-peering-windows-amd64.exe
```

* For Apple MAC OS:

```
bluemix plugin install private-network-peering-darwin-amd64
```

* For Linux OS:

```
bluemix plugin install private-network-peering-linux-amd64
```

**Note**: While you are installing the plug-in for Linux OS, if you see an error message that shows permission is denied, then run the following command and change the permissions:

```
chmod a+x ./private-network-peering-linux-amd64
```

### Install from Bluemix repository

Follow these steps to install the plug-in from the Bluemix repository:

1. Add the Bluemix plug-in registry endpoint:
	```
	bluemix plugin repo-add bluemix-bx http://plugins.ng.bluemix.net
	```

2. Run the following command:

	```
	bluemix plugin install private-network-peering -r bluemix-bx
	```

## List of private network peering commands
The following commands are supported. Use the `bluemix network` command to see the list of available commands:

| Command     | Description                                    |
|-------------|------------------------------------------------|
| pnp-routers | Lists all available routers for peering        |
| pnp-create  | Creates a private network peering connection   |
| pnp-delete  | Deletes a private network peering connection   |
| pnp-show    | Lists all private network peering connections  |
{: caption="Table 1. Private network peering commands" caption-side="top"}


### Command usage
To view help information for the commands, run: `bluemix network [command] -h`.

#### List all available routers for peering
```
bluemix network pnp-routers [--verbose (or -v)]
```

##### Optional parameters
{: #op1}

* **--verbose (or -v)** (flag): View detailed network information about each router.

###### Command example
{: #ex1}

To view network information about all routers:

	$ bluemix network pnp-routers
	Listing available routers ...
	OK

	IP              NAME            COMPUTE    REGION          ORGANIZATION    SPACE
	129.41.234.246  default-router  Container  US-South        ywu@us.ibm.com  demo1
	129.41.237.172  default-router  Container  US-South        ywu@us.ibm.com  demo2
	129.41.238.212  default-router  Container  United-Kingdom  ywu@us.ibm.com  demo3


To view detailed network information about all routers:


	$ bluemix network pnp-routers -v
	Listing available routers ...
	OK

	Router 'bce1aa25-bad0-4cf1-a831-d53c16463d06':
	FIELD          VALUE
	IP             129.41.234.246
	Name           default-router
	Compute        Container
	Region         US-South
	Organization   ywu@us.ibm.com
	Space          demo1
	Networks       172.31.0.0/16

	Router '9ea160f2-1a30-44cd-bd25-794d441b274b':
	FIELD          VALUE
	IP             129.41.237.172
	Name           default-router
	Compute        Container
	Region         US-South
	Organization   ywu@us.ibm.com
	Space          demo2
	Networks       172.25.0.0/16

	...


#### Create a private network peering connection by using the IP addresses
```
bluemix network pnp-create <router_ip> <router_ip> <name>
```

##### Parameters
{: #p1}

* **router_ip**: IP addresses of the two routers that you want to connect. You can find the IP addresses by using the command: `bluemix network pnp-routers`
* **name**: Name of the private network peering connection.

###### Command example
{: #ex2}

	$ bluemix network pnp-create 129.41.234.246 129.41.237.172 demo
	Creating private network peering connection 'demo' ...
	Connecting 'default-router(129.41.234.246)' and 'default-router(129.41.237.172)' ...
	OK

	Private network peering connection 'demo' created.


#### Create a private network peering connection by using the connection name

```
bluemix network pnp-create -i <name>
```

##### Parameters
{: #p2}

* **--interactive (-i)** (flag): Interactive mode to select routers.
* **name**: Name of the private network peering connection.

###### Command example
{: #ex3}

	$ bluemix network pnp-create -i demo
	Creating private network peering connection 'demo' ...
	List of available routers (select TWO for peering):

	#  ROUTER                          COMPUTE    REGION          ORGANIZATION    SPACE
	1  default-router(129.41.234.246)  Container  US-South        ywu@us.ibm.com  demo1
	2  default-router(129.41.237.172)  Container  US-South        ywu@us.ibm.com  demo2
	3  default-router(129.41.238.212)  Container  United-Kingdom  ywu@us.ibm.com  demo3

	Select first router for peering> 1
	Select second router for peering> 2

	Connecting 'default-router(129.41.234.246)' and 'default-router(129.41.237.172)' ...
	OK

	Private network peering connection 'demo' created.


#### List all private network peering connections
```
bluemix network pnp-show [--verbose (or -v)]
```

##### Optional parameters
{: #op2}

* **--verbose (or -v)** (flag): View detailed network information about each router.

###### Command example
{: #ex4}

View basic information:

	$ bluemix network pnp-show
	Listing private network peering connections ...
	OK

	ID                                    NAME  STATUS  ROUTER1                         ROUTER2
	17b1c3c7-d614-4fc5-9afe-961e38ee79f8  demo  Active  default-router(129.41.234.246)  default-router(129.41.237.172)

View detailed information:

	$ bluemix network pnp-show -v
	Listing private network peering connections ...
	OK

	Connection 'bedbc077-8040-41cc-a4aa-d9ce09a2e8ec':
	FIELD              VALUE
	Name               demo
	Status             Active
	Router1 Name       default-router
	Router1 IP         129.41.234.246
	Router1 Networks   172.31.0.0/16
	Router2 Name       default-router
	Router2 IP         129.41.237.172
	Router2 Networks   172.25.0.0/16


#### Delete a private network peering connection
```
bluemix network pnp-delete [--force (or -f)] <connection_id>
```
##### Parameters
{: #p3}
* **connection_id**: One or more connection IDs separated by a comma.

##### Optional parameters
{: #op3}

* **--force (or -f)** (flag): Deletes the connection without prompting for a confirmation.

###### Command example:
{: #ex5}

Delete a connection:

	$ bluemix network pnp-delete 17b1c3c7-d614-4fc5-9afe-961e38ee79f8
	Warning: deleted connections cannot be restored.
	Are you sure you want to delete the connection? (yes/no)> yes

	Deleting private network peering connection '17b1c3c7-d614-4fc5-9afe-961e38ee79f8' ...
	OK

	Private network peering connection '17b1c3c7-d614-4fc5-9afe-961e38ee79f8' deleted.


Delete multiple connections:

```
bluemix network pnp-delete [-f] <connection_id>,<connection_id>,<connection_id>
```
