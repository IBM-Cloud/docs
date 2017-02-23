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


# Removendo o acesso

É possível remover o acesso a um contêiner ou objeto usando listas de controle de acesso.
{: shortdesc}

Para remover ACLs de leitura de um contêiner, execute um dos comandos a seguir.

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

Para remover ACLs de gravação de um contêiner, execute um dos comandos a seguir.

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

Para verificar se você removeu uma ACL, execute um dos comandos a seguir.

* Comando Swift:

```
swift stat <container_name>
```
{: pre}

* A saída de exemplo a seguir mostra a ACL de Leitura e a ACL de Gravação em branco, o que significa que o acesso foi removido.

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
