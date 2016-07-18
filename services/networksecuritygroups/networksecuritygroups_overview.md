---

copyright:

  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# About {{site.data.keyword.networksecuritygroups_full}}
{: #nsgintro}
*Last updated: 14 July 2016*
{: .last-updated}

A security group is a set of IP filter rules. Each IP rule represents a network security rule. Each security group represents a network security policy. You can have up to 10 security groups per space of your Bluemix organization. These security groups include the five predefined security groups. You can assign multiple security groups to a single virtual server or to a virtual server group. 
{: shortdesc}

**Note:** All instances in a virtual server group must be associated with the same security groups. 

For more information about IBM Virtual Servers and security groups, see: [Security Groups](https://www.{DomainName}/docs/virtualmachines/vm_create.html#vm_security_groups).

The following security groups are provided in Bluemix for IBM Virtual Servers:

* **allow_ssh**: This security group defines the IP rules that allow incoming TCP traffic on the SSH port only (22/TCP).  
* **allow_https**: This security group defines the IP rules that allow incoming TCP traffic on HTTPS port only (443/TCP).  
* **allow_rdp**: This security group defines the IP rules that allow incoming TCP traffic on remote desktop client port only (3389/TCP).  
* **allow_all**: This security group defines the IP rules that allow all incoming traffic on all ports.  
* **default**: This security group defines the IP rules that deny all incoming traffic from outside the private network.  

## Getting help and support for {{site.data.keyword.networksecuritygroups_short}} 
{: #gettinghelp}

If you have problems or questions when using the Network Security Groups service, you can get help by searching for information or by asking questions through a forum. You can also open a support ticket. 

When using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.Bluemix_notm}} development teams.

* If you have technical questions about the {{site.data.keyword.networksecuritygroups_short}} service, post your question on [Stack Overflow](http://stackoverflow.com/search?q=network-security-groups+ibm-bluemix){:new_window} and tag your question with "ibm-bluemix" and "network-security-groups".

* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/security groups/?smartspace=bluemix){:new_window} forum. Include the  "security groups" and "bluemix" tags.

See [Getting help](https://www.{DomainName}/docs/support/index.html#getting-help) for more details about using the forums.

For information about opening an IBM support ticket, or about support levels and ticket severities, see [Contacting support](https://www.{DomainName}/docs/support/index.html#contacting-support).


