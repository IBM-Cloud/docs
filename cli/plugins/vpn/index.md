---

copyright:

  years: 2015, 2017

lastupdated: "2017-01-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# VPN CLI plug-in for cf CLI


You can use the command line interface (CLI) to configure and manage your {{site.data.keyword.vpn_full}} service. The {{site.data.keyword.vpn_short}} CLI plug-in is available in two versions: one for use with the Cloud Foundry CLI plug-in and the other for use with the {{site.data.keyword.Bluemix}} CLI plug-in. Both versions of the plug-in provide the same functionality.
{:shortdesc}

The {{site.data.keyword.vpn_short}} plug-in is available for Windows, MAC, and Linux operating systems. Ensure that you use the one that is applicable to you.

The instructions that follow are for working with the Cloud Foundry (cf) CLI plug-in. To use the plug-in with the  {{site.data.keyword.Bluemix_notm}} CLI plug-in, see [{{site.data.keyword.vpn_short}} plug-in for {{site.data.keyword.Bluemix_notm}} CLI](https://console.{DomainName}/docs/cli/plugins/bx_vpn/index.html).

## Install the cf CLI plug-in
Before you begin, install the cf CLI. See [Cloud Foundry command line interface](https://console.{DomainName}/docs/cli/downloads.html) for details.

##Install the VPN CLI plug-in
**Note:** If you have a previous version of the {{site.data.keyword.vpn_short}} CLI plug-in that is installed, you must first uninstall it. Use the command:

```
cf uninstall-plugin vpn
```

### Install locally

1. Download the {{site.data.keyword.vpn_short}} plug-in for your platform from [IBM Bluemix CLI Plug-in Repository](http://plugins.ng.bluemix.net/ui/repository.html#cf-plugins).
2. Install the {{site.data.keyword.vpn_short}} plug-in by using the following command:
**Note:** Either switch to the location of the {{site.data.keyword.vpn_short}} plug-in or specify the path to the plug-in location.

	- For MS Windows OS:

	```
	cf install-plugin vpn_windows64.exe
	```

	- For Apple MAC OS:

	```
	cf install-plugin vpn_mac_os_amd64
	```

	- For Linux OS:

	```
	cf install-plugin vpn_linuxamd64
	```


### Install from Bluemix repository

1. Add the Bluemix repository into the Cloud Foundry CLI repositories. Use the following command:

	```
	cf add-plugin-repo bluemix http://plugins.ng.bluemix.net
	```
2. Run the following command:

	```
	cf install-plugin vpn -r bluemix
	```
## List of IBM VPN service commands

### cf vpn-create connection

Creates a VPN connection.

```
cf vpn-create connection <connection name> -g <gateway name> -k <preshared key> -subnets ["<subnet/mask>"] -cip <customer gateway IP address> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### Parameters
{: #p1}

**connection name:**
Name of the connection.

**gateway name:**
Name of the gateway.

**-k:**
Preshared key.

**subnet/mask:**
Remote subnet address in CIDR format.

**customer gateway IP address:**
Remote endpoint IP address of the VPN tunnel.

##### Optional Parameters:
{: #op1}

**-d:** Description of the parameters specified.

**-peer_id:** ID of the remote peer. Other endpoint of the VPN tunnel.

**-admin_state:** Status of the VPN connection. Values: UP or DOWN.

**-dpd-action:** Action to be taken when the peer is detected as dead. Values: hold; clear; disabled; restart; restart-by-peer. Default value: hold

**-gateway_ip:** IP address of the local VPN tunnel endpoint.

**-i:** State of the initiator. Default value: bi-directional.

**-dpd-timeout:** Timeout value in seconds after which the session is terminated.  Range: 6 - 86400 seconds. Default value: 120 seconds. The keep alive timeout value must be higher than the keep alive interval value.

**-dpd-interval:** Keepalive interval in seconds. Send keepalive messages at the configured interval to check liveliness of the peer. Range: 5-86399 seconds. Default value: 15 seconds

**-ike:** Name of the IKE policy.

**-ipsec:** Name of the IPsec policy.


### cf vpn-create ike

Creates an IKE policy.

```
cf vpn-create ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value> -auth <authorization algorithm>
```
#### Parameters
{: #p2}

**policy name:**
Name of the IKE policy.

**gateway name:**
Name of the gateway.

##### Optional Parameters:
{: #op2}

**-d:** Description of the parameters specified.

**-pfs:** Diffie-Hellman (DH) group identifier. Values: Group2; Group5; Group14. Default value: Group2

**-e:** Encryption algorithm. Values: aes-128; aes-192; aes-256; 3des. Default value: aes-128

**-lv:** Lifetime value of the IKE security association. Range: 60 - 86400 seconds. Default value: 86400 seconds

**-auth:** Authorization algorithm. Values: sha1 or sha256


### cf vpn-create ipsec

Creates an IPsec policy.

```
cf vpn-create ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value> -auth <authorization algorithm>
```
#### Parameters
{: #p3}

**policy name:**
Name of the IPsec policy.

**gateway name:**
Name of the gateway.

##### Optional Parameters:
{: #op3}

**-d:** Description of the parameters specified.

**-pfs:** Diffie-Hellman (DH) group identifier. Values: Group2; Group5; Group14. Default value: Group2

**-e:** Encryption algorithm. Values: aes-128; aes-192; aes-256; 3des. Default value: aes-128

**-lv:** Lifetime value of the security association. Range: 60 - 86400 seconds. Default value: 3600 seconds

**-auth:** Authorization algorithm. Values: sha1 or sha256

### cf vpn-create gateway

Creates a VPN gateway.

```
cf vpn-create gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### Parameters
{: #p4}

**gateway name:**
Name of the gateway.

**-t:** Containers for which you want to enable the service. Values: allSingleContainers; allContainerGroups; allContainers. Default value: No default value; you must specify a type.

#####Optional Parameters:
{: #op4}

**-gateway_ip:**
IP address of the gateway.

**-subnets:**
Subnet address in CIDR format.

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
cf vpn-update connection <connection name> -g <gateway name> -cip <customer gateway IP address> -subnets ["<subnet/mask>"] -k <preshared key> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### Parameters
{: #p5}

**connection name:**
Name of the connection.


##### Optional Parameters:
{: #op5}

**gateway name:**
Name of the gateway.

**customer gateway IP address:**
Remote endpoint IP address of the VPN tunnel.

**subnet/mask:**
Subnet address in CIDR format.

**-k:**
Preshared key.

**-d:** Description of the parameters specified.

**-peer_id:** ID of the remote peer. Other endpoint of the VPN tunnel.

**-admin_state:** Status of the VPN connection. Values: UP or DOWN.

**-dpd-action:** Action to be taken when the peer is detected as dead. Values: hold; clear; disabled; restart; restart-by-peer. Default value: hold

**-gateway_ip:** IP address of the local VPN tunnel endpoint.

**-i:** State of the initiator. Default value: bi-directional.

**-dpd-timeout:** Timeout value in seconds after which the session is terminated. Range: 6 - 86400 seconds. Default value: 120 seconds

**-dpd-interval:** Keepalive interval in seconds. Send keepalive messages at the configured interval to check liveliness of the peer. Range: 5-86399 seconds. Default value: 15 seconds

**-ike:** Name of the IKE policy.

**-ipsec:** Name of the IPsec policy.


### cf vpn-update ike

Updates an IKE policy.

```
cf vpn-update ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value> -auth <authorization algorithm>
```
#### Parameters
{: #p6}

**policy name:**
Name of the IKE policy.

##### Optional Parameters:
{: #op6}

**gateway name:** Name of the gateway.

**-d:** Description of the parameters specified.

**-pfs:** Diffie-Hellman (DH) group identifier. Values: Group2; Group5; Group14. Default value: Group2

**-e:** Encryption algorithm. Values: aes-128; aes-192; aes-256; 3des. Default value: aes-128

**-lv:** Lifetime value of the IKE security association. Range: 60 - 86400 seconds. Default value: 86400 seconds

**-auth:** Authorization algorithm. Values: sha1 or sha256


### cf vpn-update ipsec

Updates an IPsec policy.

```
cf vpn-update ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value> -auth <authorization algorithm>
```
#### Parameters
{: #p7}

**policy name:**
Name of the IPsec policy.


##### Optional Parameters:
{: #op7}

**gateway name:**
Name of the gateway.

**-d:** Description of the parameters specified.

**-pfs:** Diffie-Hellman (DH) group identifier. Values: Group2; Group5; Group14. Default value: Group2

**-e:** Encryption algorithm. Values: aes-128; aes-192; aes-256; 3des. Default value: aes-128

**-lv:** Lifetime value of the security association. Range: 60 - 86400 seconds. Default value: 3600 seconds

**-auth:** Authorization algorithm. Values: sha1 or sha256

### cf vpn-update gateway

Updates an existing VPN gateway.

```
cf vpn-update gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### Parameters
{: #p8}

**gateway name:**
Name of the gateway.

#####Optional Parameters:
{: #op8}

**-t:** Containers for which you want to enable the service. Values: allSingleContainers; allContainerGroups; allContainers. Default value: No default value; you must specify a type.

**-gateway_ip:**
IP address of the gateway.

**-subnets:**
Subnet address in CIDR format.

# rellinks
## general
{: #general}
* [IBM VPN service](/docs/services/vpn/index.html)
* [Cloud Foundry CLI ![External link icon](../../../icons/launch-glyph.svg)](https://console.{DomainName}/docs/cli/downloads.html){: new_window}
