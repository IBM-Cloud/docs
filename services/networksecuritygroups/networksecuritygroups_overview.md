---

copyright:

  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# About {{site.data.keyword.networksecuritygroups_full}}
{: #nsgintro}
*Last updated: 04 May 2016*

A security group is a set of IP filter rules. Each IP rule represents a network security rule. Each security group represents a network security policy. You can have up to 10 security groups per space of your Bluemix organization. These security groups include the five predefined security groups. You can assign multiple security groups to a single virtual server or to a virtual server group. 
{: shortdesc}

**Note:** All instances in a virtual server group must be associated with the same security groups. 

For more information about IBM Virtual Servers and security groups, see: [Security Groups](https://www.{DomainName}/docs/virtualmachines/vm_index.html#vm_security_groups).

The following security groups are provided in Bluemix for IBM Virtual Servers:

* **allow_ssh**: This security group defines the IP rules that allow incoming TCP traffic on the SSH port only (22/TCP).  
* **allow_https**: This security group defines the IP rules that allow incoming TCP traffic on HTTPS port only (443/TCP).  
* **allow_rdp**: This security group defines the IP rules that allow incoming TCP traffic on remote desktop client port only (3389/TCP).  
* **allow_all**: This security group defines the IP rules that allow all incoming traffic on all ports.  
* **default**: This security group defines the IP rules that deny all incoming traffic from outside the private network.  

