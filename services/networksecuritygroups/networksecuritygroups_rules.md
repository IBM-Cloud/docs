---

copyright:

  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuring rules
{: #nsgrules}  
*Last updated: 04 May 2016*

You can configure rules to manage inbound traffic (ingress traffic) to a virtual server, and outbound traffic (egress traffic) from a virtual server. 
{:shortdesc}

Configure rules as shown in the following steps. 

1. Select the security group for which you want to configure the rules.  
2. Select **Inbound Rules** or **Outbound Rules**, as required.  
3. Select **ADD RULE**.  
4. Specify inbound or outbound rules:  
	* **Type:** Select IPv4.  
	* **Protocol:** Select the protocol from the drop-down list. If you want to specify a protocol that is not in the list, select **Other protocol** from the drop-down list.  
	Provide the following information if you select **Other protocol**:  
	  * **Protocol value:** The IP number of the protocol. For example: You enter 1 for ICMP protocol.  
	* **Port:** or **Port Range:** The port configuration parameter depends on the protocol you select.  
		* If you select **ALL ICMP**, **ALL TCP**, or **ALL UDP**, no port information is required.  
		* If you select a single protocol, the port number is automatically displayed. For example: If you select **HTTP**, port **80** is displayed.  
		* If you select **Custom TCP Rule** or **Custom UDP rule**, select a port type. Values: port, port range. If you select **Port**, enter the port number; if you select **Port range**, enter the range of port numbers.  
		* If you select **Custom ICMP Rule**, enter the ICMP **Code** and **Type**.
	* **Select source type:** Select **IP** or **SG** or **Server**.  
		* If you select **IP**, enter an IP address in the **Source IP** or **Destination IP** field.  
		* If you select **SG**, select a security group from the **Source SG** or **Destination SG** drop-down list. The list displays all the configured security groups, including the default security group.  
		* If you select **Server**, select a virtual server from the **Source Virtual Server** or **Destination Virtual Server** drop-down.
5. Select **ADD**.
