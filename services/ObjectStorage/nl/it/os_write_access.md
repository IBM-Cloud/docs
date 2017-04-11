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


# Concessione dell'accesso in scrittura

Un utente {{site.data.keyword.objectstorageshort}} con un [ruolo da amministratore](/docs/services/ObjectStorage/os_access_types.html) può concedere l'accesso in scrittura a un altro utente e modificare le combinazioni ACL di scrittura.
{: shortdesc}

<table>
<caption> Tabella 1. Autorizzazioni dell'accesso in scrittura per opzione </caption>
  <tr>
    <th> Autorizzazione </th>
    <th> Opzioni Write ACL </th>
  </tr>
  <tr>
    <td> Scrivi un utente specifico in un progetto specifico </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> Scrivi un utente specifico in qualsiasi progetto </td>
    <td> <code> &#42;:user_id </code> </td>
  </tr>
  <tr>
    <td> Scrivi ogni utente in un progetto specifico </td>
    <td>  <code> project_id:&#42; </code> </td>
  </tr>
  <tr>
    <td> Scrivi ogni utente in ogni progetto </td>
    <td>  <code> &#42;:&#42; </code> </td>
  </tr>
</table>



1. Autentica le tue credenziali utilizzando le informazioni nelle credenziali del servizio che hai creato.  Riceverai il tuo URL e token di autenticazione {{site.data.keyword.objectstorageshort}} come output.

    Comando Swift:

    ```
    export OS_USER_ID="<user_id>"
    export OS_PASSWORD="<password>"
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
    curl -i -H "X-Auth-User:< user_id>" -H "X-Auth-Key:< password>" https://identity.open.softlayer.com/v3
    ```
    {: pre}

2. Concedi l'accesso in scrittura immettendo il seguente comando.

    Comando Swift:

    ```
    swift post <container_name> --write-acl "<user_id>:<project_id>"
    ```
    {: pre}

    Comando cURL:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <user_id>: <project_id>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}

    **Nota**: utilizza una virgola (,) per separare gli elenchi del controllo dell'accesso.

3. Verifica il valore write ACL.

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
