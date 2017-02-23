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


# Concessione dell'accesso in lettura

Un utente {{site.data.keyword.objectstorageshort}} con un [ruolo da amministratore](/docs/services/ObjectStorage/os_access_types.html) può concedere l'accesso in lettura a un contenitore a un altro utente e modificare le combinazioni ACL di lettura.
{: shortdesc}

<table>
<caption> Tabella 1. Autorizzazioni dell'accesso in lettura per opzione </caption>
  <tr>
    <th> Autorizzazione </th>
    <th> Opzioni Read ACL </th>
  </tr>
  <tr>
    <td> Legge tutti i riferimenti indipendentemente dall'affiliazione dell'account </td>
    <td> <code> .r,&#42;  </code> </td>
  </tr>
  <tr>
    <td> Legge e elenca tutti i riferimenti e li elenca </td>
    <td> <code> .r:&#42;,.rlistings </code> </td>
  </tr>
  <tr>
    <td> Legge e elenca un utente specifico in un progetto specifico </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> Legge e elenca un utente specifico in qualsiasi progetto </td>
    <td> <code> &#42;:user_id </code> </td>
  </tr>
  <tr>
    <td> Legge e elenca ogni utente in un progetto specifico </td>
    <td> <code> project_id:&#42; </code> </td>
  </tr>
  <tr>
    <td> Legge e elenca ogni utente in ogni progetto  </td>
    <td> <code> &#42;:&#42; </code> </td>
  </tr>
</table>


1. Autenticazione delle tue credenziali. Puoi utilizzare le credenziali trovate nella scheda delle credenziali del servizio della IU o puoi generare nuove credenziali. Per ulteriori informazioni sulla generazione di nuove credenziali, consulta [Generazione delle credenziali del servizio](/docs/services/ObjectStorage/os_credentials.html). Riceverai il tuo URL e token di autenticazione {{site.data.keyword.objectstorageshort}} come output.

    Comando Swift:

    ```
    export OS_USER_ID=<user_id>
  export OS_PASSWORD=<password>
  export OS_TENANT_ID=<project_id>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

    swift auth
    ```
    {: codeblock}

    Comando cURL:

    ```
    curl -i -H "X-Auth-User: <user_id>" -H "X-Auth-Key: <password>" <auth_url>
    ```
    {: pre}

2. Concedi l'accesso in lettura immettendo il seguente comando:
    Comando Swift:

    ```
    swift post <container_name> --read-acl "<user_id>:<project_id>"
    ```
    {: pre}

    Comando cURL:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <tenant_id>:<project_id>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}
    **Nota**: utilizza una virgola (,) per separare gli elenchi del controllo dell'accesso.

3. Verifica il valore Read ACL.

    Comando Swift:

    ```
    swift stat <container_name>
    ```
    {: pre}

    Comando cURL:

    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}

    Esempio: il valore `X-Container-Read` mostra quale contenitore e quale accesso di lettura sono stati concessi.

    ```
    HTTP/1.1 204 No Content
  Content-Length: 0
  X-Container-Object-Count: 1
  Accept-Ranges: bytes
  X-Storage-Policy: standard
  X-Container-Read: c727d7e248b448f6b268f31a1bd8691e:3c5b516655e4479881d3d216895faedb
  X-Container-Bytes-Used: 31512
  X-Timestamp: 1462818314.11220
  Content-Type: text/plain; charset=utf-8
  X-Trans-Id: txad7fe001da274b9ba39a6-005772e4d6
  Date: Tue, 28 Jun 2016 20:57:58 GMT
    ```
    {: screen}
