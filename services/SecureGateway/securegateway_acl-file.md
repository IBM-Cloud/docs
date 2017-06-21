---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-10"

---
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# ACL File

```
#Lines preceded by a # will be ignored as a comment
#To allow specific port on a specific host:
#acl allow <hostname>:<port>

#To allow all ports on a specific host:
#acl allow <hostname>:

#To allow all hosts from a specific port:
#acl allow :<port>

#To allow all hosts and ports, use below command:
#acl allow :

#To deny specific port on a specific host:
#acl deny <hostname>:<port>

#To deny all ports on a specific host:
#acl deny <hostname>:

#To deny all hosts from a specific port:
#acl deny :<port>

#To deny all hosts and ports, use below command:
#acl deny :
```
{: codeblock}
