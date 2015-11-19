# Getting started with IBM VPN (Beta)

IBM® Virtual Private Network (VPN) provides a secure communication channel between your corporate data center and your resources inside IBM cloud. The connection is established over the Internet. You can use IBM cloud as an extension of your corporate data center. 

IBM VPN service is available to securely access container resources inside IBM cloud.  

The IBM VPN service offering is available at: IBM Bluemix > Catalog > Services > Network. 

### To use IBM VPN service:

1. Open IBM Bluemix > Catalog > Services > Network. You will see the available network services.
2. Select **VPN**. You will see the VPN service description, available plans, and pricing details. 
3. Select a suitable plan. 
4. Select options in the **Add Service** section:
    <ul><li>Space:</li><li>Service Name:</li></ul>
5. Select **CREATE**. The service instance is created.
6. Select IBM Bluemix > Dashboard > Services > Virtual Private Network (VPN).

Proceed with configuring the gateway, site connections, and the Internet Key Exchange (IKE) and IPSec policies.  

#### Gateway Configuration
![Gateway Configuration](images/gateway.png)

Configure the gateway as follows:  
1. Specify the gateway name.  
2. Select the containers or groups with which you want to use the VPN service.  
3. Select **SAVE**. 

#### VPN Site Connection Configuration
![Site Connection](images/siteconn.png)

1. Select **ADD NEW**.
2. Specify the following site connection details:  
	* **Name**: Name of the connection  
	* **Description**: Description of the connection parameters (optional)  
	* **Preshared Key String**: Preshared (secret) key to be used for authentication
	* **Admin State**: Status of the VPN connection. Select from drop-down: UP or DOWN; default value: UP (optional)  
	* **Customer Gateway IP**: Remote endpoint IP address of the VPN tunnel  
	* **Customer Subnet**: Remote subnet address in CIDR format. 
3. (Optional) Configure the following **Advanced Settings** parameters:  
	* **IKE Policy**: Name of the IKE policy
	* **Keep Alive Interval**: Keepalive interval in seconds. Send keepalive messages at the configured interval to check liveliness of the peer. Default value: 15. Range: 15-86400
	* **Action on dead peer**: Action to be taken when the peer is detected as dead
	* **IPSec Policy**: Name of the IPSec policy
	* **Keep Alive Timeout**: Timeout value in seconds after which the session is terminated. Default value: 120. Range: 30-86400
4. Select **SAVE**.

#### IKE and IPSec Policy Configuration

**Note:** You can use the default IKE and IPSec policies or configure custom policies.

![Tab](images/tab.png)  
Select the **IKE & IPSec Policies** tab.

#####IKE Policy Configuration
![IKE Policy Configuration](images/ikepolicy.png)

To configure IKE policy:

1. Select **ADD NEW**.  
2. Specify the following details:
	* **Name**: Name of the IKE policy
	* **Authorization Algorithm**: sha1; cannot be changed  
	* **Encryption Algorithm**: Select from drop-down. Values: aes-128 (default); aes-192; aes-256; 3des
	* **Key Lifetime**: Lifetime value (in seconds) of the IKE security association. Range: 60-86400. Default Value: 86400
	* **PFS**: Diffie-Hellman (DH) group identifier. Values: Group2; Group5; Group14; Default value: Group14
	* **Negotiation Mode**: Main; cannot be changed
	* **Version**: IKEV1; cannot be changed
3. Select **SAVE**.

#####IPSec Policy Configuration
![IPSec Policy](images/ipsecpolicy.png)

To configure IPSec policy:

1. Select **ADD NEW**.  
2. Specify the following details:
	* **Name**: Name of the IPSec policy  
	* **Authorization Algorithm**: sha1; cannot be changed  
	* **Encryption Algorithm**: Select from drop-down. Values: aes-128 (default); aes-192; aes-256; 3des
	* **Key Lifetime**: Lifetime value (in seconds) of the security association. Range: 60-86400. Default Value: 3600
	* **PFS**: Diffie-Hellman (DH) group identifier. Values: Group2; Group5; Group14; Default value: Group14
	* **Transform Protocol**: ESP; cannot be changed
	* **Encapsulation Mode**: Tunnel; cannot be changed
3. Select **SAVE**.  

###IBM VPN Overview
IBM VPN provides the following features:

####Security 
IBM VPN uses industry-standard Internet Protocol Security (IPSec) protocol suite to authenticate and encrypt IP communication between your corporate data center and IBM cloud. IPSec provides network-level peer authentication, data integrity, and data confidentiality (encryption).

IBM VPN supports the following IPSec protocols and transforms:

* Authentication Algorithm:
	* HMAC-SHA1-96; the length of the shared key is 160 bits (default)  
* Encryption Algorithm:
	* 3DES-CBC; the length of the shared key is 192 bits
	* AES-CBC; the lengths of the shared key are 128 (default), 192, 256 bits
* Authentication and Encryption Protocols:
	* Authentication Header (AH) and Encapsulating Security Payload (ESP) protocols are supported. AH is used for authentication only. ESP is used for providing authentication and encryption.
* IKEv1 Diffie-Hellman (DH) Key Exchange groups 2, 5, and 14(default)

IBM VPN supports IPSec tunnel Mode. In this mode, IPSec protects the entire original IP packet. IPSec encrypts the packet, encapsulates it within a new IP packet, and forwards the new packet to the IPSec peer. 

IBM VPN uses Diffie-Hellman key exchange and the preshared key to secure the association between two peers. Authentication fails if any one party does not provide the preshared key. 
 
IBM VPN service is compliant with the following IETF RFCs:

* RFCs 2407, 2408, and 2409 for IKEv1
* RFC 4301 for IPv4 security   
* RFC 4302 for the IPv4 Authentication Header  
* RFC 4303 for IPv4 Encapsulating Security Payload (ESP)  
* RFC 2104 HMAC and RFC 2404 HMAC-SHA-1-96 for authentication  
* RFC 2451 3DES-CBC; RFC 3602 AES128-CBC, AES192-CBC, and AES256-CBC for encryption

####Simplicity
You can create IBM VPN service by using a simple and intuitive graphical interface. You can specify your gateway IP address, your data center subnets, and either use default IPSec and IKE policies or customize the policies to suit your needs.  

####Management
 
You can manage the IBM VPN service by using graphical interface, command line interface, or API.

* [IBM VPN graphical interface](https://console.ng.bluemix.net/?direct=classic)
* [IBM VPN RESTful APIs](http://vpn-api-docs.mybluemix.net)
* [IBM VPN command line interface](../../cli/plugins/vpn/index.html)  


># Related Links {:class="linklist"}
>>## API Reference {:id="api"}
>* [IBM VPN RESTful APIs](http://vpn-api-docs.mybluemix.net)
>## Related Links {:id="general"}
>>## Command line Interface {:id="cli"}
>* [IBM VPN Command line Interface](../../cli/plugins/vpn/index.html)
>
>{:elementKind="article" id="rellinks"}


