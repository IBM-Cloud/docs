---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Removing access

You can remove access to a container or object by using access control lists.
{: shortdesc}

To remove read ACLs from a container, run one of the following commands.

* Swift command:

```
swift post <container_name> --read-acl “”
```
{: pre}

* cURL command:

```
curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
```
{: pre}

To remove write ACLs from a container, run one of the following commands.

* Swift command:

```
swift post <container_name> --write-acl “”
```
{: pre}

* cURL command:

```
curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
```
{: pre}

To verify that you have removed an ACL run one of the following commands.

* Swift command:

```
swift stat <container_name>
```
{: pre}

* The following example output shows both the Read ACL and Write ACL as blank, which means that access has been removed.

```
         Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
       Container: Test
         Objects: 1
           Bytes: 31512
        Read ACL:
       Write ACL:
         Sync To:
        Sync Key:
   Accept-Ranges: bytes
X-Storage-Policy: standard
     X-Timestamp: 1462818314.11220
      X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
    Content-Type: text/plain; charset=utf-8
```
{: screen}

* cURL command:

```
curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
```
{: pre}
