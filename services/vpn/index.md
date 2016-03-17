---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Getting started with {{site.data.keyword.vpn_short}}
{: #vpn}  
*Last updated: 17 March 2016*

The {{site.data.keyword.vpn_full}} service for Bluemix&reg; is available to securely access IBM Containers (Docker containers) inside the IBM Bluemix cloud environment. You can use the IBM Bluemix cloud environment as an extension of your corporate data center. You can also connect with the SoftLayer servers using the IBM VPN service.
{:shortdesc}

Before you begin, ensure that you have an IBM Docker container ready to use. See [IBM Containers for Bluemix](https://www.ng.bluemix.net/docs/containers/container_index.html) for details on how to create and manage IBM Containers.  

To get started, select the **Virtual Private Network** service instance tile on the Bluemix dashboard. Complete the following steps:

1. Configure the {{site.data.keyword.vpn_short}} gateway by selecting **CREATE GATEWAY**. A default gateway is created. If required, edit the gateway configuration as shown in the following steps.  
{: #gateway}  

  1. Select **EDIT**.  
  2. Specify the gateway name.  
  3. Select the containers or groups with which you want to use the VPN service.  
  4. Select **SAVE**.  

 You can use the default IKE and IPSec policies, or configure custom policies. If you want to use the default policies, skip to step 4.

2. Configure the IKE policy by selecting the **IKE & IPSec Policies** tab.
  1. Select **ADD NEW**.  
  2. Specify the following details:
	* **Name**: Name of the IKE policy
	* **Authorization Algorithm**: sha1; cannot be changed  
	* **Encryption Algorithm**: Select from drop-down. Values: aes-128 (default), aes-192, aes-256, 3des
	* **Key Lifetime**: Lifetime value (in seconds) of the IKE security association. Range: 60-86400. Default Value: 86400
	* **PFS**: Diffie-Hellman (DH) group identifier. Values: Group2, Group5, Group14. Default value: Group2
	* **Negotiation Mode**: Main; cannot be changed
	* **Version**: IKEV1; cannot be changed
  3. Select **SAVE**.

3. Configure the IPSec policy:
  1. Select **ADD NEW**.  
  2. Specify the following details:
  	* **Name**: Name of the IPSec policy  
  	* **Authorization Algorithm**: sha1; cannot be changed  
  	* **Encryption Algorithm**: Select from drop-down. Values: aes-128 (default), aes-192, aes-256, 3des
  	* **Key Lifetime**: Lifetime value (in seconds) of the security association. Range: 60-86400. Default Value: 3600
  	* **PFS**: Diffie-Hellman (DH) group identifier. Values: Group2, Group5, Group14. Default value: Group2
  	* **Transform Protocol**: ESP; cannot be changed
  	* **Encapsulation Mode**: Tunnel; cannot be changed
  3. Select **SAVE**.  

4. Provide the details to establish a connection between your data center or SoftLayer server VPN gateway, and the IBM VPN gateway.  
{: #site}  

  1. Select the **VPN Gateway Appliance** tab.
  2. Select **ADD NEW** in the **VPN Site Connections** section.
  3. Specify the following site connection details:  
  	* **Name**: Name of the connection  
  	* **Description**: Description of the connection (optional)  
  	* **Preshared Key String**: Preshared (secret) key to be used for authentication
  	* **Admin State**: Status of the VPN connection. Select from drop-down: UP or DOWN. Default value: UP  
  	* **Customer Gateway IP**: Remote endpoint IP address of the VPN tunnel  
  	* **Customer Subnet**: Remote subnet address in CIDR format. Select the plus sign to save the subnet details.
  4. (Optional) Configure the following **Advanced Settings** parameters:  
  	* **IKE Policy**: Select the IKE policy.  
  	* **Keep Alive Interval**: Keepalive interval in seconds. Send keepalive messages at the configured interval to check liveliness of the peer. Default value: 15. Range: 5-86399
  	* **Action on dead peer**: Action to be taken when the peer is detected as dead.  
    	Values: 
  		* hold (default value): the security association (SA) is put on hold 
  		* clear: the SA is deleted
  		* disabled: the SA is disabled
  		* restart: the SA is renegotiated
  		* restart-by-peer: all SAs with the dead peer are renegotiated  
  	* **IPSec Policy**: Select the IPSec policy.
  	* **Keep Alive Timeout**: Timeout value in seconds after which the session is terminated. Default value: 120. Range: 6-86400. The keep alive timeout value must be higher than the keep alive interval value.
  5. Select **SAVE**.

  **Note:** When the connection is being established, the connection status displays as ***pending create***. When you see this status, refresh the screen a few times to see the connection active status.

**Important:** If you are using a web application, you must bind the web application to the Docker container you are using. This binding is required for the traffic to pass through the IPSec VPN tunnel.

**Important:** The IBM VPN service currently operates in responder mode. To initiate the VPN connection, a data packet must flow out from the IBM VPN gateway to your on-premises data center or SoftLayer server. Once the VPN connection is established, traffic can flow in either direction between endpoints of the VPN connection.

 
# rellinks
## samples 
* [On-premises strongSwan Gateway Configuration Example](vpn_onpremises.html#strongswan){: new_window}
* [On-premises Vyatta Gateway Configuration Example](vpn_onpremises.html#vyatta){: new_window}
* [On-premises SoftLayer Gateway Appliance Service (GaaS) Configuration Example](vpn_onpremises.html#gaas){: new_window}
* [On-premises Cisco ASA Configuration Example](vpn_onpremises.html#cisco){: new_window}

## api 
* [IBM VPN RESTful APIs](https://new-console.ng.bluemix.net/apidocs/101){: new_window}

## general 
* [IBM VPN Command line Interface](../../cli/plugins/vpn/index.html){: new_window}
* [IBM VPN FAQs](vpn_faq.html#vpn_faq){: new_window}
* [IBM Bluemix Pricing Sheet](https://console.{DomainName}/pricing/){: new_window}
* [IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs)
