---

 

copyright:

  years: 2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Bluemix CLI plug-in for VPN

*Last updated:* 18 January 2016

*Version:* 0.1.5

You can use the Bluemix CLI VPN plug-in to configure and manage your IBM Virtual Private Network (VPN) service.
{:shortdesc}

The information that follows lists all commands that are supported by Bluemix CLI VPN plug-in and includes their names, options, usage, prerequisites, descriptions, and examples.

**Note:** *Prerequisites* list which actions are required before using the command. Prerequisites might include one or more of the following actions:
<dl>
<dt>**Endpoint**</dt>
<dd>An API endpoint must be set through the `bluemix api` before using the command.</dd>
<dt>**Login**</dt>
<dd>Login by using the `bluemix login` command is required before using this command.</dd>
<dt>**Target**</dt>
<dd>The `bluemix target` command must be used to set an org and space before using this command.</dd>
</dl>


## bluemix vpn connection-create
Creates a VPN connection.

```
bluemix vpn connection-create CONNECTION_NAME -g GATEWAY_NAME -k PRESHARED_KEY -subnets "SUBNET/MASK" -cip CUSTOMER_GATEWAY_IP_ADDRESS [-d DESCRIPTION] [-peer_id PEER_ID] [-admin_state ADMIN_STATE] [-dpd-action ACTION] [-gateway_ip IP_ADDRESS] [-i INITIATOR_STATE] [-dpd-timeout VALUE] [-dpd-interval VALUE] [-ike NAME] [-ipsec NAME]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*CONNECTION_NAME*  (required):  Name of the connection.

-g *GATEWAY_NAME*  (required):  Name of the gateway.

-k *PRESHARED_KEY*  (required):  Preshared key.

-subnets "*SUBNET*/*MASK*"  (required):  Remote subnet address in CIDR format.

-cip *CUSTOMER_GATEWAY_IP_ADDRESS*  (required):  Remote endpoint IP address of the VPN tunnel.

-d *DESCRIPTION*  (optional):  Description of the parameters specified.

-peer_id *PEER_ID*  (optional):  ID of the remote peer. Other endpoint of the VPN tunnel.

-admin_state *ADMIN_STATE*  (optional):  Status of the VPN connection. Valid value is `UP` or `DOWN`.

-dpd-action *ACTION*  (optional):  Action to be taken when the peer is detected as dead. Valid value is  `hold`, `clear`, `disabled`, `restart` or `restart-by-peer`. Default value is `hold`.

-gateway_ip *IP_ADDRESS*  (optional):  IP address of the local VPN tunnel endpoint.

-i *INITIATOR_STATE*  (optional):  State of the initiator. Default value is `bi-directional`.

-dpd-timeout *VALUE*  (optional):  Timeout value in seconds after which the session is terminated. Range: 6 - 86400 seconds. Default value is `120` seconds.

-dpd-interval *VALUE*  (optional):  Keepalive interval in seconds. Send keepalive messages at the configured interval to check liveliness of the peer. Range: 5-86399 seconds. Default value is `15` seconds.

-ike *NAME*  (optional):  Name of the IKE policy.

-ipsec *NAME*  (optional):  Name of the IPSec policy.

**Examples**:

Create a new vpn connection with name `my_connection`:
```
bluemix vpn connection-create my_connection -g my_gateway -k 123456 -subnets "192.168.10.0/24" -cip 162.135.1.1
```


## bluemix vpn ike-create
Creates an IKE policy.

```
bluemix vpn ike-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*POLICY_NAME*  (required):  Name of the IKE policy.

-g *GATEWAY_NAME*  (required):  Name of the gateway.

-d *DESCRIPTION*  (optional):  Description of the parameters specified.

-pfs *GROUP*  (optional):  Diffie-Hellman (DH) group identifier. Valid value is `Group2`, `Group5` or `Group14`. Default value is `Group2`.

-e *ENCRYPTION_ALGORITHM*  (optional):  Encryption algorithm. Valid value is `aes-128`, `aes-192`, `aes-256` or `3des`. Default value is `aes-128`.

-lv *LIFETIME_VALUE*  (optional):  Lifetime value of the IKE security association. Range: 60 - 86400 seconds. Default value is `86400` seconds.

**Examples**:

Create a new IKE policy with name `my_ike`:
```
bluemix vpn ike-create my_ike -g my_gateway
```


## bluemix vpn ipsec-create
Creates an IPSec policy.

```
bluemix vpn ipsec-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*POLICY_NAME*  (required):  Name of the IPSec policy.

-g *GATEWAY_NAME*  (required):  Name of the gateway.

-d *DESCRIPTION*  (optional):  Description of the parameters specified.

-pfs *GROUP*  (optional):  Diffie-Hellman (DH) group identifier. Valid value is `Group2`, `Group5` or `Group14`. Default value is `Group2`.

-e *ENCRYPTION_ALGORITHM*  (optional):  Encryption algorithm. Valid value is `aes-128`, `aes-192`, `aes-256` or `3des`. Default value is `aes-128`.

-lv *LIFETIME_VALUE*  (optional):  Lifetime value of the security association. Range: 60 - 86400 seconds. Default value is `3600` seconds.

**Examples**:

Create an IPSec policy with name `my_policy`:
```
bluemix vpn ipsec-create my_policy -g my_gateway
```


## bluemix vpn gateway-create
Creates a VPN gateway.

```
bluemix vpn gateway-create GATEWAY_NAME -t TYPE [-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*GATEWAY_NAME*  (required):  Name of the gateway.

-t *TYPE*  (required):  Containers for which you want to enable the service. Valid value is `allSingleContainers`, `allContainerGroups` or `allContainers`. No default value; you must specify a type.

-gateway_ip *IP_ADDRESS*  (optional):  IP address of the gateway.

-subnets *SUBNET_ADDRESS*  (optional):  Subnet address in CIDR format.

**Examples**:

Create a gateway with name `my_gateway` and type `allContainerGroups`:
```
bluemix vpn gateway-create my_gateway -t allContainerGroups
```


## bluemix vpn connections
Displays information about all the current connections.

```
bluemix vpn connections
```

**Prerequisites**:  Endpoint, Login, Target


## bluemix vpn ikes
Displays information about the current IKE connections.

```
bluemix vpn ikes
```

**Prerequisites**:  Endpoint, Login, Target


## bluemix vpn ipsecs
Displays information about the current IPSec connections.

```
bluemix vpn ipsecs
```

**Prerequisites**:  Endpoint, Login, Target


## bluemix vpn gateways
Displays information about the current gateways.

```
bluemix vpn gateways
```

**Prerequisites**:  Endpoint, Login, Target


## bluemix vpn connection
Displays all information about a particular connection.

```
bluemix vpn connection CONNECTION_NAME
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*CONNECTION_NAME*  (required):  Name of the connection to be displayed.


## bluemix vpn ike
Displays information about an IKE connection.

```
bluemix vpn ike POLICY_NAME
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*POLICY_NAME*  (required):  Name of the IKE policy to be displayed.


## bluemix vpn ipsec
Displays information about an IPSec connection.

```
bluemix vpn ipsec POLICY_NAME
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*POLICY_NAME*  (required):  Name of the IPSec policy to be displayed.


## bluemix vpn gateway
Displays connection information about a gateway.

```
bluemix vpn gateway GATEWAY_NAME
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*GATEWAY_NAME*  (required):  Name of the gateway to be displayed.


## bluemix vpn connection-delete
Deletes an existing connection.

```
bluemix vpn connection-delete CONNECTION_NAME
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*CONNECTION_NAME*  (required):  Name of the connection to be deleted.


## bluemix vpn ike-delete
Deletes an existing IKE policy.

```
bluemix vpn ike-delete POLICY_NAME
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*POLICY_NAME*  (required):  Name of the IKE policy to be deleted.


## bluemix vpn ipsec-delete
Deletes an existing IPSec policy.

```
bluemix vpn ipsec-delete POLICY_NAME
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*POLICY_NAME*  (required):  Name of the IPSec policy to be deleted.


## bluemix vpn gateway-delete
Deletes an existing gateway.

```
bluemix vpn gateway-delete GATEWAY_NAME
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*GATEWAY_NAME*  (required):  Name of the gateway to be deleted.


## bluemix vpn connection-update
Updates an existing VPN connection.

```
bluemix vpn connection-update CONNECTION_NAME [-g GATEWAY_NAME] [-k PRESHARED_KEY] [-subnets "SUBNET/MASK"] [-cip CUSTOMER_GATEWAY_IP_ADDRESS] [-d DESCRIPTION] [-peer_id PEER_ID] [-admin_state ADMIN_STATE] [-dpd-action ACTION] [-gateway_ip IP_ADDRESS] [-i INITIATOR_STATE] [-dpd-timeout VALUE] [-dpd-interval VALUE] [-ike NAME] [-ipsec NAME]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*CONNECTION_NAME*  (required):  Name of the connection.

-g *GATEWAY_NAME*  (optional):  Name of the gateway.

-k *PRESHARED_KEY*  (optional):  Preshared key.

-subnets "*SUBNET*/*MASK*"  (optional):  Subnet address in CIDR format.

-cip *CUSTOMER_GATEWAY_IP_ADDRESS*  (optional):  Remote endpoint IP address of the VPN tunnel.

-d *DESCRIPTION*  (optional):  Description of the parameters specified.

-peer_id *PEER_ID*  (optional):  ID of the remote peer. Other endpoint of the VPN tunnel.

-admin_state *ADMIN_STATE*  (optional):  Status of the VPN connection. Valid value is `UP` or `DOWN`.

-dpd-action *ACTION*  (optional):  Action to be taken when the peer is detected as dead. Valid value is  `hold`, `clear`, `disabled`, `restart` or `restart-by-peer`.

-gateway_ip *IP_ADDRESS*  (optional):  IP address of the local VPN tunnel endpoint.

-i *INITIATOR_STATE*  (optional):  State of the initiator.

-dpd-timeout *VALUE*  (optional):  Timeout value in seconds after which the session is terminated. Range: 6 - 86400 seconds.

-dpd-interval *VALUE*  (optional):  Keepalive interval in seconds. Send keepalive messages at the configured interval to check liveliness of the peer. Range: 5-86399 seconds.

-ike *NAME*  (optional):  Name of the IKE policy.

-ipsec *NAME*  (optional):  Name of the IPSec policy.


## bluemix vpn ike-update
Updates an IKE policy.

```
bluemix vpn ike-update POLICY_NAME [-g GATEWAY_NAME] [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*POLICY_NAME*  (required):  Name of the IKE policy.

-g *GATEWAY_NAME*  (optional):  Name of the gateway.

-d *DESCRIPTION*  (optional):  Description of the parameters specified.

-pfs *GROUP*  (optional):  Diffie-Hellman (DH) group identifier. Valid value is `Group2`, `Group5` or `Group14`.

-e *ENCRYPTION_ALGORITHM*  (optional):  Encryption algorithm. Valid value is `aes-128`, `aes-192`, `aes-256` or `3des`.

-lv *LIFETIME_VALUE*  (optional):  Lifetime value of the IKE security association. Range: 60 - 86400 seconds.


## bluemix vpn ipsec-update
Updates an IPSec policy.

```
bluemix vpn ipsec-update POLICY_NAME [-g GATEWAY_NAME] [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*POLICY_NAME*  (required):  Name of the IPSec policy.

-g *GATEWAY_NAME*  (optional):  Name of the gateway.

-d *DESCRIPTION*  (optional):  Description of the parameters specified.

-pfs *GROUP*  (optional):  Diffie-Hellman (DH) group identifier. Valid value is `Group2`, `Group5` or `Group14`.

-e *ENCRYPTION_ALGORITHM*  (optional):  Encryption algorithm. Valid value is `aes-128`, `aes-192`, `aes-256` or `3des`.

-lv *LIFETIME_VALUE*  (optional):  Lifetime value of the security association. Range: 60 - 86400 seconds.


## bluemix vpn gateway-update
Updates an existing VPN gateway.

```
bluemix vpn gateway-update GATEWAY_NAME [-t TYPE] [-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*GATEWAY_NAME*  (required):  Name of the gateway.

-t *TYPE*  (optional):  Containers for which you want to enable the service. Valid value is `allSingleContainers`, `allContainerGroups` or `allContainers`.

-gateway_ip *IP_ADDRESS*  (optional):  IP address of the gateway.

-subnets *SUBNET_ADDRESS*  (optional):  Subnet address in CIDR format.
