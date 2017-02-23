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


# Eliminación de acceso

Puede eliminar el acceso a un contenedor u objeto mediante listas de control de acceso.
{: shortdesc}

Para eliminar los ACL de lectura de un contenedor, ejecute uno de los mandatos siguientes.

* Mandato Swift:

```
swift post <nombre_contenedor> --read-acl “”
```
{: pre}

* Mandato cURL:

```
curl -i <URL_ALMACENAMIENTO_SO> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <SEÑAL_AUTENTICACIÓN_SO>"
```
{: pre}

Para eliminar los ACL de escritura de un contenedor, ejecute uno de los mandatos siguientes.

* Mandato Swift:

```
swift post <nombre_contenedor> --write-acl “”
```
{: pre}

* Mandato cURL:

```
curl -i <URL_ALMACENAMIENTO_SO> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <SEÑAL_AUTENTICACIÓN_SO>"
```
{: pre}

Para comprobar que se ha eliminado un ACL, ejecute uno de los mandatos siguientes.

* Mandato Swift:

```
swift stat <nombre_contenedor>
```
{: pre}

* La siguiente salida de ejemplo muestra tanto el ACL de lectura como el ACL de escritura en blanco, lo que significa que se ha eliminado el acceso.

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

* Mandato cURL:

```
curl -i <URL_ALMACENAMIENTO_SO> -I -H "X-Auth-Token: <SEÑAL_AUTENTICACIÓN_SO>"
```
{: pre}
