{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# IBM Network Security Groups CLI

*Last updated:* 01 March 2016

*Version:* 0.1.1

You can use the command line interface (CLI) to configure and manage your {{site.data.keyword.networksecuritygroups_full}} service. The IBM Network Security Groups CLI is a plug-in that is used with the [Bluemix&reg; CLI](http://clis.ng.bluemix.net/ui/home.html). The plug-in is available for Windows, Mac OS, and Linux operating systems. Ensure that you use the plug-in that is applicable to you.

Before you begin, install the IBM Bluemix CLI. See [Bluemix CLI](http://clis.ng.bluemix.net/ui/home.html) for details.

## Install IBM Network Security Groups CLI Plug-in

**Note:** If you have a previous version of the IBM Network Security Groups CLI plug-in that is installed, you need to first uninstall it. Use the command:

```
bluemix plugin uninstall "Network Security Group"
```

**Install Locally**

1. Download the IBM Network Security Groups plug-in for your platform from [IBM Bluemix CLI Plug-in Repository](http://plugins.ng.bluemix.net/ui/repository.html#bluemix-plugins).  
2. Install the IBM Network Security Groups plug-in by using the following command:  
**Note:** Either switch to the location of the Network Security Groups plug-in or specify the path to the plug-in location.  

	**For Microsoft Windows:**  
	```
	bluemix plugin install nsg-windows-amd64.exe  
	```  
	**For Apple Mac OS:**  
	```  
	bluemix plugin install nsg-darwin-amd64
	```  
	**For Linux OS:**  
	```
	bluemix plugin install nsg-linux-amd64
	```  
	**Note:** If you see a ***permission denied*** error message while installing the plug-in for Linux OS, run the following command and change the permissions:  
	```
	chmod a+x ./nsg-linux-amd64
	```

**Install from Bluemix Repository**

1. Add the Bluemix plug-in registry endpoint:  
	```
	bluemix plugin repo-add bluemix-bx http://plugins.ng.bluemix.net
	```  
2. Run the following command:

	**For Microsoft Windows:**  
	```
	bluemix plugin install nsg-windows-amd64.exe -r bluemix-bx
	```  
	**For Apple Mac OS:**  
	```
	bluemix plugin install nsg-darwin-amd64 -r bluemix-bx
	```  
	**For Linux OS:**  
	```
	bluemix plugin install nsg-linux-amd64 -r bluemix-bx
	```  

**Note:** After you install the Network Security Groups plug-in, log in to Bluemix. If you do not log in, you will not be able to run the Network Security Groups service commands. 

Run the following command to log in to the United Kingdom region:

```
bluemix login -a https://api.eu-gb.bluemix.net
```  

See [Bluemix CLI](http://clis.ng.bluemix.net/ui/home.html) for details.

## List of IBM Network Security Groups Service Commands  

| 			Command 			| | |			Description 				|  
| :----------------------------	| | |:------------------------------------	|  
| [security-group-create](index.html#sgcreate) 		| | |Creates a security group 			|  
| [security-group-update](index.html#sgupdate) 		| | |Updates an existing security group 	|
| [security-group-delete](index.html#sgdelete) 		| | |Deletes an existing security group and all its rules |
| [security-group-list](index.html#sglist)        | | |Lists all or assigned security groups for a virtual server or virtual server group|
| [security-group-show](index.html#sgshow)        | | |Shows details of an existing security group and its rules|
| [security-group-rule-create](index.html#sgrulecreate) | | |Creates a security group rule |
| [security-group-rule-delete](index.html#sgruledelete) | | |Deletes an existing security group rule |
| [security-group-rule-list](index.html#sgrulelist)   | | |Lists all security group rules |
| [security-group-rule-show](index.html#sgruleshow)   | | |Shows details of an existing security group rule |
| [instance-list](index.html#inslist)              | | |Lists all virtual servers or virtual servers assigned to a security group|
| [instance-group-list](index.html#grplist)        | | |Lists all virtual server groups or virtual server groups assigned to a security group|
| [security-group-assign](index.html#sggrpassign)      | | |Assigns a security group to a virtual server or virtual server group |
| [security-group-unassign](index.html#sggrpunassign)    | | |Removes a security group from a virtual server or virtual server group|

### Command Usage

####bluemix network security-group-create
{: #sgcreate}

Creates a security group.

```
bluemix network security-group-create [-d "<description>"] <name>
```

***Parameters:***

**name**: Name of the new security group. Data type: string

***Optional Parameters:***

**-d**: Description of the security group. Data type: string

***Command Example:***

Create a security group and validate it:

	$ bluemix network security-group-create -d "Security group created" test-00
	
	Created network security group [test-00] with ID [6ed0111f-73a7-4f4b-8cf3-2a9ac5ecf747]

	$ bluemix network security-group-list
	+---------------------------------------------------------------------+
	| ID                                   NAME    DESCRIPTION            |
	+---------------------------------------------------------------------+
	| 6ed0111f-73a7-4f4b-8cf3-2a9ac5ecf747 test-00 Security group created |
	| 291cbfdc-e384-4219-b8f8-6ab2a3792732 tcp-all Allow all TCP traffics |
	| 71aca377-1a34-46eb-83b5-f471c9741c84 default Default security group |
	+---------------------------------------------------------------------+

####bluemix network security-group-update
{: #sgupdate}

Updates the name and description of an existing security group.

```
bluemix network security-group-update [-n <name>] [-d "<description>"] <name or ID>
```

***Parameters:***

**name or ID**: Name or ID of an existing security group. Data type: string

***Optional Parameters:***

**-n**: New name of the security group. Data type: string  
**-d**: New description of the security group. Data type: string

***Command Example:***

Update an existing security group and validate it:

	$ bluemix network security-group-update -n test-01 -d "Security group updated" test-00

	Updated network security group [test-01] with ID [6ed0111f-73a7-4f4b-8cf3-2a9ac5ecf747]

	$ bluemix network security-group-list
	+---------------------------------------------------------------------+
	| ID                                   NAME    DESCRIPTION            |
	+---------------------------------------------------------------------+
	| 6ed0111f-73a7-4f4b-8cf3-2a9ac5ecf747 test-01 Security group updated |
	| 291cbfdc-e384-4219-b8f8-6ab2a3792732 tcp-all Allow all TCP traffics |
	| 71aca377-1a34-46eb-83b5-f471c9741c84 default Default security group |
	+---------------------------------------------------------------------+

####bluemix network security-group-delete
{: #sgdelete}

Deletes an existing security group and all its rules.

```
bluemix network security-group-delete <name or ID>
```

***Parameters:***

**name or ID**: Name or ID of an existing security group. Data type: string

***Command Example:***

Delete an existing security group and validate it:

	$ bluemix network security-group-delete test-01
	
	Deleted security group test-01
	
	$ bluemix network security-group-list
	+---------------------------------------------------------------------+
	| ID                                   NAME    DESCRIPTION            |
	+---------------------------------------------------------------------+
	| 291cbfdc-e384-4219-b8f8-6ab2a3792732 tcp-all Allow all TCP traffics |
	| 71aca377-1a34-46eb-83b5-f471c9741c84 default Default security group |
	+---------------------------------------------------------------------+

####bluemix network security-group-list
{: #sglist}

Lists all security groups or the security groups assigned to a virtual server or virtual server group.

```
bluemix network security-group-list [-v] [-i <name or ID>] [-ig <name or ID>]
```

***Parameters:***

None. If no option is specified, the command lists all the security groups.

***Optional Parameters:***

**-v**: Prints list of rules with details for each security group

**-i**: Lists security groups assigned to the specified virtual server. Data type: string

**-ig**: Lists security groups assigned to the specified virtual server group. Data type: string

***Command Examples:***

* List all security groups:

		$ bluemix network security-group-list
		+---------------------------------------------------------------------+
		| ID                                   NAME    DESCRIPTION            |
		+---------------------------------------------------------------------+
		| 291cbfdc-e384-4219-b8f8-6ab2a3792732 tcp-all Allow all tcp traffics |
		| 71aca377-1a34-46eb-83b5-f471c9741c84 default Default security group |
		+---------------------------------------------------------------------+

* List security groups assigned to the virtual server **test-inst-1**:

		$ bluemix network security-group-list -i test-inst-1
		+---------------------------------------------------------------------+
		| ID                                   NAME    DESCRIPTION            |
		+---------------------------------------------------------------------+
		| 71aca377-1a34-46eb-83b5-f471c9741c84 default Default security group |
		+---------------------------------------------------------------------+

* List security groups assigned to the virtual server group **test-stack-1**:

		$ bluemix network security-group-list -ig test-stack-1
		+---------------------------------------------------------------------+
		| ID                                   NAME    DESCRIPTION            |
		+---------------------------------------------------------------------+
		| 71aca377-1a34-46eb-83b5-f471c9741c84 default Default security group |
		+---------------------------------------------------------------------+

####bluemix network security-group-show
{: #sgshow}

Shows details of an existing security group and its rules.

```
bluemix network security-group-show <security group name or ID>
```

***Parameters:***

**security group name or ID**: Name or ID of an existing security group. Data type: string

***Command Example:***

View information about the security group named **default**:

	$ bluemix network security-group-show default
	+----------------------------------------------------------------------------------------------------------------------------------+
	| ID                                   DIRECTION PROTOCOL TYPE PORT_MIN PORT_MAX REMOTE_IP_PREFIX REMOTE_GROUP_ID                  |
	+----------------------------------------------------------------------------------------------------------------------------------+
	| 690470aa-5eb6-4875-9e48-311618a7334a ingress            IPv6                                71aca377-1a34-46eb-83b5-f471c9741c84 |
	| 744491b5-4540-4689-ae0d-4cd12af9abea ingress            IPv4                                71aca377-1a34-46eb-83b5-f471c9741c84 |
	| b7ea43fd-558d-4e66-8462-807ff32c14ca egress             IPv4                                                                     |
	| c7ff45b1-86fb-4386-9fb0-6c5675b5ee30 egress             IPv6                                                                     |
	+----------------------------------------------------------------------------------------------------------------------------------+

####bluemix network security-group-rule-create
{: #sgrulecreate}

Creates a security group rule.

```
bluemix network security-group-rule-create -d <direction> -p <protocol> -t <type> [-ip <remote IP prefix> | -r <remote group name or ID>] [-min <minimum value of port range] [-max <maximum value of port range>] <security group name or ID>
```

***Parameters:***

**-d**: Direction of traffic: ingress or egress. Data type: string

**-p**: Protocol. Values: UDP, TCP, ICMP, ICMPv6. Data type: string 

**-t**: Ethernet type: IPv4 or IPv6. Data type: string 

**-ip**: Remote IP address or CIDR to be matched in the rule. Data type: string  
	
**-r**: Remote security group name or ID to be matched in the rule. Data type: string 

**security group name or ID**: Name or ID of an existing security group. Data type: string

***Optional Parameters:***

**-min**: Starting port range. Data type: integer

**-max**: Ending port range. Data type: integer

***Command Example:***

	$ bluemix network security-group-rule-create -d ingress -p tcp -ip 10.10.10.1 default

	Created network security group rule [9a988876-36e0-47dd-9a7e-76c5a6be7379]

####bluemix network security-group-rule-delete
{: #sgruledelete}

Deletes an existing security group rule.

```
bluemix network security-group-rule-delete <ID>
```

***Parameters:***

**ID**: ID of an existing security group rule. Data type: string

***Command Example:***

	$ bluemix network security-group-rule-delete f191473c-9dd4-4465-8c5e-697a3a5e2385
	
	Deleted security group rule f191473c-9dd4-4465-8c5e-697a3a5e2385

####bluemix network security-group-rule-list
{: #sgrulelist}

Lists all security group rules.

```
bluemix network security-group-rule-list
```

***Command Example:***

	$ bluemix network security-group-rule-list
	+----------------------------------------------------------------------------------------------------------------------------------+
	|ID									DIRECTION	PROTOCOL	TYPE	PORT_MIN	PORT_MAX	REMOTE_IP_PREFIX	REMOTE_GROUP_ID|
	+----------------------------------------------------------------------------------------------------------------------------------+
	|0f467437-b3b1-4f38-9597-006e054ef8cc	ingress	tcp		 IPv4	22			22			0.0.0.0/0					  |
	|8fa3b4d7-70e9-483b-b51d-ac808bbfa96f	egress				 IPv4															   |
	|c5ff6cac-945e-4126-84ce-5ff63f2dce66	egress	 tcp		 IPv4	1			65535										 |
	|c60ca7c3-31c3-4f41-bdbf-8ed89f359c97	egress				 IPv6															   |
	+----------------------------------------------------------------------------------------------------------------------------------+

####bluemix network security-group-rule-show
{: #sgruleshow}

Shows details of an existing security group rule.

```
bluemix network security-group-rule-show <ID>
```

***Parameters:***

**ID**: ID of an existing security group rule. Data type: string

***Command Example:***

	$ bluemix network security-group-rule-show 9a988876-36e0-47dd-9a7e-76c5a6be7379
	+------------------------------------------------+
	| FIELD     VALUE                                |
	+------------------------------------------------+
	| ID        9a988876-36e0-47dd-9a7e-76c5a6be7379 |
	| DIRECTION ingress                              |
	| PROTOCOL  TCP                                  |
	| TYPE      IPv4                                 |
	| PORT_MIN  1                                    |
	| PORT_MAX  65535                                |
	| REMOTE_IP 10.10.10.1/32                        |
	| REMOTE_SG                                      |
	+------------------------------------------------+

####bluemix network instance-list
{: #inslist}

Lists all virtual servers, virtual servers that are assigned to a security group, or virtual server instances that are part of a virtual server group.

```
bluemix network instance-list [-sg <security group name or ID> | -ig <virtual server group name or ID>]
```

***Parameters:***

None. If no option is specified, the command lists all instances.

***Optional Parameters:***

**-sg**: Name or ID of a security group. Data type: string

**-ig**: Name or ID of a virtual server group. Data type: string

***Command Examples:***

* List all instances:

		$ bluemix network instance-list
		+--------------------------------------------------+
		| ID                                   NAME        |
		+--------------------------------------------------+
		| 84d435c8-9468-4fd1-90a9-171903cf460f test-inst-3 |
		| ec26e0f9-ee9c-4493-beb8-8f551a9a68d8 test-inst-2 |
		| e8e66653-fed5-4901-8116-ccdfef443f28 test-inst-1 |
		+--------------------------------------------------+

* List virtual servers assigned to the security group **default**:

		$ bluemix network instance-list -sg default
		+--------------------------------------------------+
		| ID                                   NAME        |
		+--------------------------------------------------+
		| e8e66653-fed5-4901-8116-ccdfef443f28 test-inst-1 |
		+--------------------------------------------------+

####bluemix network instance-group-list
{: #grplist}

Lists all virtual server groups, or virtual server groups that are assigned to a security group.

```
bluemix network instance-group-list [-sg <security group name or ID>]
```
***Parameters:***

None. If no option is specified, the command lists all virtual server groups.

***Optional Parameters:***

**-sg**: Name or ID of a security group. Data type: string

***Command Examples:***

* List all virtual server groups:

		$ bluemix network instance-group-list
		+---------------------------------------------------+
		| ID                                   NAME         |
		+---------------------------------------------------+
		| 098578a7-fadc-415c-835e-6518fb08dbc0 test-stack-2 |
		| c9549664-05e9-46c0-a1b2-ac84e59ce3b0 test-stack-1 |
		+---------------------------------------------------+

* List virtual server groups that are assigned to the security group **default**:

		$ bluemix network instance-group-list -sg default
		+---------------------------------------------------+
		| ID                                   NAME         |
		+---------------------------------------------------+
		| 098578a7-fadc-415c-835e-6518fb08dbc0 test-stack-1 |
		+---------------------------------------------------+

####bluemix network security-group-assign
{: #sggrpassign}

Assigns a security group to a virtual server or a virtual server group.

```
bluemix network security-group-assign [-i <virtual server name or ID> |-ig <virtual server group name or ID>] <security group name or ID>
```

***Parameters:***

**-i**: Name or ID of the virtual server that you want to assign to. Data type: string or strings separated by comma/space 

**-ig**: Name or ID of the virtual server group that you want to assign to. Data type: string or strings separated by comma/space

***Command Examples:***

* Assign security group **default** to virtual server **test-inst-1**:

		$ bluemix network security-group-assign default -i test-inst-1
		Assigned network security group [default] to instance [test-inst-1]

* Assign security group **default** to virtual server group **test-stack-1**:

		$ bluemix network security-group-assign default -ig test-stack-1
		Assigned security group [default] to instance group [test-stack-1]

* Assign security group **default** to multiple virtual servers and virtual server groups:

		$ bluemix network security-group-assign default -i test-inst-1,test-inst-2 -ig test-stack-1,test-stack-2
		Assigned network security group [default] to instance [test-inst-1]
		Assigned network security group [default] to instance [test-inst-2]
		Assigned network security group [default] to instance group [test-stack-1]
		Assigned network security group [default] to instance group [test-stack-2]

####bluemix network security-group-unassign
{: #sggrpunassign}

Removes a virtual server or virtual server group from a security group.

```
bluemix network security-group-unassign [-i <virtual server name or ID> | -ig <virtual server group name or ID>] <security group name or ID>
```

***Parameters:***

**security group name or ID**: Name or ID of the security group from which you want to delete the virtual server or virtual server group. Data type: string

**-i**: Name or ID of the virtual server that you want to delete. Data type: string or strings separated by comma/space

**-ig**: Name or ID of the virtual server group that you want to delete. Data type: string or strings separated by comma/space

***Command Examples:***

* Remove virtual server **test-inst-1** from the security group **default** and validate it:

		$ bluemix network security-group-unassign default -i test-inst-1
		Unassigned security group [default] to instance [test-inst-1]
		
		$ bluemix network instance-list -sg default
		No instances assigned to security group [default]

* Remove virtual server group **test-stack-1** from the security group **default** and validate it:

		$ bluemix network security-group-assign default -ig test-stack-1
		Unassigned security group [default] to instance group [test-stack-1]
		
		$ bluemix network instance-group-list -sg default
		No instance groups assigned to security group [default]

* Remove multiple virtual servers and virtual server groups from the security group **default**:

		$ bluemix network security-group-unassign default -i "test-inst-1 test-inst-2" -ig "test-stack-1 test-stack-2"
		Unassigned network security group [default] for instance [test-inst-1]
		Unassigned network security group [default] for instance [test-inst-2]
		Unassigned network security group [default] for instance group [test-stack-1]
		Unassigned network security group [default] for instance group [test-stack-2]

# rellinks
## general  
{: #general}  
* [IBM Network Security Groups service](../../../services/networksecuritygroups/index.html)
* [Bluemix CLI](http://clis.ng.bluemix.net/ui/home.html)