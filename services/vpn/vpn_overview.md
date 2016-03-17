---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# About {{site.data.keyword.vpn_short}}
{: #vpn_overview}  
*Last updated: 17 March 2016*

The {{site.data.keyword.vpn_full}} (VPN) service provides a secure communication channel between your corporate data center and your resources in the IBM Bluemix&reg; cloud environment. The connection is established over the Internet.
{:shortdesc}

The {{site.data.keyword.vpn_short}} service provides the following features:  
##Security 
The IBM VPN service uses the industry-standard Internet Protocol Security (IPSec) protocol suite to authenticate and encrypt IP communication between your corporate data center and the IBM Bluemix cloud environment. IPSec provides network-level peer authentication, data integrity, and data confidentiality (encryption).

The IBM VPN service supports the following IPSec protocols and transforms:

* Authentication Algorithm:
	* HMAC-SHA1-96; the length of the shared key is 160 bits (default)  
* Encryption Algorithm:
	* 3DES-CBC; the length of the shared key is 192 bits
	* AES-CBC; the lengths of the shared key are 128 (default), 192, 256 bits
* Authentication and Encryption Protocols:
	* Authentication Header (AH) and Encapsulating Security Payload (ESP) protocols are supported. AH is used for authentication only. ESP is used for providing authentication and encryption.
* IKEv1 Diffie-Hellman (DH) Key Exchange groups 2 (default), 5, and 14

The IBM VPN service supports IPSec tunnel Mode. In this mode, IPSec protects the entire original IP packet. IPSec encrypts the packet, encapsulates it within a new IP packet, and forwards the new packet to the IPSec peer. 

The IBM VPN service uses Diffie-Hellman key exchange and the preshared key to secure the association between two peers. Authentication fails if any one party does not provide the preshared key. 
 
The IBM VPN service is compliant with the following IETF RFCs:

* RFCs 2407, 2408, and 2409 for IKEv1
* RFC 4301 for IPv4 security   
* RFC 4302 for the IPv4 Authentication Header  
* RFC 4303 for IPv4 Encapsulating Security Payload (ESP)  
* RFC 2104 HMAC and RFC 2404 HMAC-SHA-1-96 for authentication  
* RFC 2451 3DES-CBC; RFC 3602 AES128-CBC, AES192-CBC, and AES256-CBC for encryption
##Simplicity
You can create the IBM VPN service by using a simple and intuitive graphical interface. You can specify your gateway IP address and your data center subnets. You can either use default IPSec and IKE policies, or customize the policies to suit your needs.  
##Management
You can manage the IBM VPN service by using a graphical interface, a [command line interface](../../cli/plugins/vpn/index.html), or [APIs](https://new-console.ng.bluemix.net/apidocs/101).

