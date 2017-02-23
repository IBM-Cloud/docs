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


# Rimozione dell'accesso

Puoi rimuovere l'accesso al contenitore o all'oggetto utilizzando l'elenco del controllo dell'accesso.
{: shortdesc}

Per rimuovere i read ACL da un contenitore, esegui uno dei seguenti comandi.

* Comando Swift:

```
swift post <container_name> --read-acl “”
```
{: pre}

* Comando cURL:

```
curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
```
{: pre}

Per rimuovere i write ACL da un contenitore, esegui uno dei seguenti comandi.

* Comando Swift:

```
swift post <container_name> --write-acl “”
```
{: pre}

* Comando cURL:

```
curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
```
{: pre}

Per verificare di aver rimosso un ACL, esegui uno dei seguenti comandi.

* Comando Swift:

```
swift stat <container_name>
```
{: pre}

* Il seguente output di esempio mostra sia l'ACL in lettura che in scrittura come vuoti, il che significa che l'accesso è stato rimosso.

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

* Comando cURL:

```
curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
```
{: pre}
