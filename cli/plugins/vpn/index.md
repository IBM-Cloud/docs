# IBM Bluemix VPN CLI
You can use the VPN CLI to configure and manage your VPN connections. The VPN CLI is a plug-in that is used with the Cloud Foundry CLI plug-in. The plug-in is available for MAC and Windows operating systems. Ensure you use the one that is applicable to you.

Before you begin, install the Cloud Foundry CLI. See [Cloud Foundry command line interface](https://www.ng.bluemix.net/docs/cli/downloads.html) for details. 

Install the VPN CLI plug-in as follows:

**Install Locally**

1. Download the VPN plug-in for your platform from [IBM Bluemix CLI Plug-in Repository](http://plugins.ng.bluemix.net).
2. Install the VPN plug-in by using the following command:  
**Note:** Either switch to the location of the VPN plug-in or specify the path to the plug-in location.  

	**For Apple MAC OS:**

	```
	cf install-plugin vpn
	```  

	**For MS Windows OS:**

	```
	cf install-plugin vpn.exe
	```  

**Install from Bluemix Repository**  

1. Add the Bluemix repository into the Cloud Foundry CLI repositories. Use the following command:

	```
	cf add-plugin-repo bluemix http://plugins.ng.bluemix.net
	```  
2. Run the following command:  

	**For Apple MAC OS:**

	```
	cf install-plugin vpn -r bluemix
	```

	**For MS Windows OS:**

	```
	cf install-plugin vpn.exe -r bluemix
	```
##List of VPN Commands

### cf vpn-create connection

Creates a new VPN connection.

```
cf vpn-create connection <connection name> -g <gateway name> -cip <customer gateway IP address> -subnets ["<subnet/mask>"] -k <preshared key>  
```
#### Parameters
**-connection name:** 
Name of the connection.

**-gateway name:** 
Name of the gateway.

**-customer gateway IP address:** 
Local endpoint IP address of the VPN tunnel. 

**-subnet/mask:** 
Subnet address in CIDR format. Default value:1.1.1.1/24

**-k:** 
Preshared key.

##### Optional Parameters:

**-d:** Description of the parameters specified.

**-peer_id:** ID of the remote peer. Other endpoint of the VPN tunnel.

**-admin_state:** Status of the VPN connection. Values: UP or DOWN.

**-dpd-action:** Action to be taken when the configured timeout value has expired.

**-gateway_ip:** IP address of the remote VPN tunnel endpoint. Default value: 1.1.1.1

**-i:** State of the initiator. Default value: bi-directional.

**-dpd-timeout:** Timeout value in seconds after which the session is terminated. Default value: 120

**-dpd-interval:** Keepalive interval in seconds. A timeout message is sent when the configured interval expires. Default value: 30

**-ike:** Name of the IKE policy.

**-ipsec:** Name of the IPsec policy.


### cf vpn-create ike

Creates an IKE policy.

```
cf vpn-create ike <policy name> -g <gateway name> 
```
#### Parameters
**-policy name:** 
Name of the IKE policy. Default value: ike1

**-gateway name:** 
Name of the gateway. 

##### Optional Parameters:

**-d:** Description of the parameters specified.

**-pfs:** Diffie-Hellman (DH) group identifier. Default value: Group1 

**-e:** Encryption algorithm. Default value: aes-128

**-lv:** Lifetime value of the IKE security association. Default value: 86400 seconds


### cf vpn-create ipsec

Creates an IPsec policy.

```
cf vpn-create ipsec <policy name> -g <gateway name> 
```
#### Parameters
**-policy name:** 
Name of the IPsec policy. Default value: ipsec1

**-gateway name:** 
Name of the gateway. 

##### Optional Parameters:

**-d:** Description of the parameters specified.

**-pfs:** Diffie-Hellman (DH) group identifier. Default value: Group1 

**-e:** Encryption algorithm. Default value: aes-128

**-lv:** Lifetime value of the security association. Default value: 86400 seconds

### cf vpn-create gateway

Creates a new VPN gateway.

```
cf vpn-create gateway <gateway name> -t <type> 
```
#### Parameters
**-gateway name:** 
Name of the gateway.

**-t:** Type

#####Optional Parameters:

**-gateway IP address:** 
IP address of the gateway. Default value: 1.1.1.1

**-subnets:** 
Subnet address(es) in CIDR format. Default value: 1.1.1.1/24

### cf vpn-show gateways

Displays information about the current gateways.

```
cf vpn-show gateways
```
### cf vpn-show ikes

Displays information about the current IKE connections.

```
cf vpn-show ikes
```
### cf vpn-show ipsecs

Displays information about the current IPsec connections.

```
cf vpn-show ipsecs
```
### cf vpn-show connections

Displays information about all the current connections.

```
cf vpn-show connections
```
### cf vpn-show ike

Displays information about an IKE connection.

```
cf vpn-show ike <policy name>
```
### cf vpn-show ipsec

Displays information about an IPsec connection.

```
cf vpn-show ipsec <policy name>
```
### cf vpn-show gateway

Displays connection information about a gateway.

```
cf vpn-show gateway <gateway name>
```
### cf vpn-show connection

Displays all information about a particular connection.

```
cf vpn-show connection <connection name>
```
### cf vpn-delete

Deletes an existing connection, policy, or gateway.

```
cf vpn-delete ike <policy name>
```

```
cf vpn-delete ipsec <policy name>
```

```
cf vpn-delete connection <connection name>
```

```
cf vpn-delete gateway <gateway name>
```


### cf vpn-update connection

Updates an existing VPN connection.

```
cf vpn-update connection <connection name>  
```
#### Parameters
**-connection name:** 
Name of the connection.


##### Optional Parameters:

**-gateway name:** 
Name of the gateway.

**-k:** 
Preshared key.


**-customer gateway IP address:** 
Local endpoint IP address of the VPN tunnel. 

**-subnet/mask:** 
Subnet address in CIDR format. Default values: 1.1.1.1/24

**-i:** State of the initiator. Default value: bi-directional.

**-d:** Description of the parameters specified.

**-peer_id:** ID of the remote peer. Other endpoint of the VPN tunnel.

**-admin_state:** Status of the VPN connection. Values: UP or DOWN.

**-dpd-action:** Action to be taken when the configured timeout value has expired.

**-gateway_ip:** IP address of the remote VPN tunnel endpoint. Default value: 1.1.1.1

**-dpd-timeout:** Timeout value in seconds after which the session is terminated. Default value: 120

**-dpd-interval:** Keepalive interval in seconds. A timeout message is sent when the configured interval expires. Default value: 30

**-ike:** Name of the IKE policy.

**-ipsec:** Name of the IPsec policy.


### cf vpn-update ike

Updates an IKE policy.

```
cf vpn-update ike <policy name> 
```
#### Parameters
**-policy name:** 
Name of the IKE policy. 

##### Optional Parameters:

**-gateway name:** 
Name of the gateway. 

**-d:** Description of the parameters specified.

**-pfs:** Diffie-Hellman (DH) group identifier. Default value: Group1 

**-e:** Encryption algorithm. Default value: aes-128

**-lv:** Lifetime value of the IKE security association. Default value: 86400 seconds


### cf vpn-update ipsec

Updates an IPsec policy.

```
cf vpn-update ipsec <policy name> 
```
#### Parameters
**-policy name:** 
Name of the IPsec policy. Default value: ipsec1


##### Optional Parameters:

**-gateway name:** 
Name of the gateway.

**-d:** Description of the parameters specified.

**-pfs:** Diffie-Hellman (DH) group identifier. Default value: Group1 

**-e:** Encryption algorithm. Default value: aes-128

**-lv:** Lifetime value of the security association. Default value: 86400 seconds

### cf vpn-update gateway

Updates an existing VPN gateway.

```
cf vpn-update gateway <gateway name> 
```
#### Parameters
**-gateway name:** 
Name of the gateway.


#####Optional Parameters:

**-t:** Type

**-gateway IP address:** 
IP address of the gateway. Default value: 1.1.1.1

**-subnets:** 
Subnet address(es) in CIDR format. Default value: 1.1.1.1/24