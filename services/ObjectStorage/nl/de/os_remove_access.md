---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Zugriff entfernen

Sie können mithilfe von Zugriffssteuerungslisten (ACLs, Access Control Lists) Zugriffsberechtigungen für einen Container oder ein Objekt entfernen.
{: shortdesc}

Führen Sie einen der folgenden Befehle aus, um Lesezugriffssteuerungslisten von einem Container zu entfernen:

* Swift-Befehl:

```
swift post <Containername> --read-acl “”
```
{: pre}

* cURL-Befehl:

```
curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
```
{: pre}

Führen Sie einen der folgenden Befehle aus, um Schreibzugriffssteuerungslisten von einem Container zu entfernen:

* Swift-Befehl:

```
swift post <Containername> --write-acl “”
```
{: pre}

* cURL-Befehl:

```
curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
```
{: pre}

Um sicherzustellen, dass Sie eine Zugriffssteuerungsliste entfernt haben, führen Sie einen der folgenden Befehle aus.

* Swift-Befehl:

```
swift stat <Containername>
```
{: pre}

* Die folgende Beispielausgabe zeigt sowohl die Lesezugriffssteuerung (Read ACL) als auch die Schreibzugriffssteuerung (Write ACL) leer an, d. h. der Zugriff wurde entfernt.

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

* cURL-Befehl:

```
curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
```
{: pre}
