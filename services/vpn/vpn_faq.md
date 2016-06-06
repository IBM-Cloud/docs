---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.vpn_short}} FAQs
{: #vpn_faq}
*Last updated: 06 June 2016*

Following are some frequently asked questions.
{:shortdesc}

1. Which third-party vendor devices are qualified in IBM labs for interoperability with the IBM VPN service?

	IBM lab has tested the following VPN gateway devices for interoperation with the IBM VPN service:

	* Cisco Adaptive Security Appliance (ASA) Software Version 8.2(1). [See configuration example](vpn_onpremises.html#cisco) 
	* Brocade Vyatta 5415 vRouter 6.7 R7. [See configuration example](vpn_onpremises.html#vyatta){: new_window}
	* Linux StrongSwan U5.1.2/K3.13.0-55-generic. [See configuration example](vpn_onpremises.html#strongswan){: new_window}
	* Linux StrongSwan U5.2.2/K3.13.0-55-generic. [See configuration example](vpn_onpremises.html#strongswan){: new_window}

	In addition, an IPSec standards-compliant VPN gateway device from any other vendor is expected to work well with the IBM VPN service.

2. How soon will a peer failure be detected?
 
	A failed peer is detected at the configured keepalive timeout value. The default setting is 60 seconds.

3. How many VPN gateways and connections can I create per VPN service?
 
	You can create one VPN gateway appliance per VPN service in a Bluemix space. You can define up to 16 connections to different destinations per VPN gateway. 

4. When should I use the IBM VPN service versus the Bluemix Secure Gateway service?

	Both the services are used to provide secure connectivity between your Bluemix resources and your on-premises data center. 

	Use the IBM VPN service when you are looking to ensure connectivity between any two endpoints. The VPN service forms a secure, Layer 3 IPSec connection between your on-premises networks and the IBM Bluemix cloud environment. The IBM VPN service is available to securely access IBM containers (Docker containers) only. 

	Use the Bluemix Secure Gateway service if you want to establish a secure connection from a specific application endpoint in Bluemix to another endpoint inside your on-premises data center. 

5. Can I use the IBM VPN service to access my containers and virtual servers inside the IBM Bluemix cloud environment by using their private IP addresses?
 
	Currently, the IBM VPN service is available for accessing Bluemix containers only.

6. Can I define the IBM VPN service at Bluemix Organization level?

	Currently, the IBM VPN service is available only at the Bluemix Space level. If your Bluemix Organization has multiple Spaces, then a separate VPN service can be defined for each space.

7. How do I connect the IBM VPN service with the SoftLayer Gateway Appliance service (GaaS)?

	You can build an IPSec tunnel to establish secure communication between the IBM VPN service and the SoftLayer GaaS. [See configuration example.](vpn_onpremises.html#gaas){: new_window}

8. Can I access the container and container group using their private IP addresses?

	The container and container group private subnets are preselected so that you can access them over the VPN connection.  

9. How do I change the security setting of an existing, in-use VPN policy?

	If your current VPN security policy uses SHA1 and you want to migrate to SHA256, you can do so as given in the following steps.  
	1. Open the IBM VPN service dashboard and complete the following tasks.
		1. Create an IKE policy with SHA256 as the authorization algorithm.
		2. Create an IPSec policy with SHA256 as the authorization algorithm.
		3. Delete the existing connection that uses SHA1 as the authorization algorithm for IKE and IPSec.
		4. Create a connection with the IKE and IPSec policies that you created with SHA256 as the authorization algorithm.
		5. Complete the remaining configurations to enable the VPN connection. See the [Getting Started](https://console.stage1.ng.bluemix.net/docs/services/vpn/index.html) page.
	2. Configure or update the remote end (your on-premises VPN gateway) IKE and IPSec policies with SHA256. Restart the IPSec connection.
