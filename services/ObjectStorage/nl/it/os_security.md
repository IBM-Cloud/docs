---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-04"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Protezione dei file {: #understanding-authentication}


## Comprensione delle credenziali del servizio {: #understanding-credentials}

Le credenziali del servizio sono utilizzate per fornire l'autenticazione e la protezione del servizio. Una serie di credenziali viene generata automaticamente quando viene eseguito il provisioning di un'istanza. Il client Swift prende le seguenti informazioni di autenticazione dalle variabili di ambiente nella seguente tabella.

<table>
  <tr>
    <th> Variabile di ambiente </th>
    <th> Descrizione </th>
  </tr>
  <tr>
    <td> <code>OS_USER_ID</code> </td>
    <td> Il tuo ID utente {{site.data.keyword.objectstorageshort}}. </td>
  </tr>
  <tr>
    <td> <code>OS_PASSWORD</code> </td>
    <td> La password per la tua istanza {{site.data.keyword.objectstorageshort}}. </td>
  </tr>
  <tr>
    <td> <code>OS_PROJECT_ID</code> </td>
    <td> Il tuo ID progetto. </td>
  </tr>
  <tr>
    <td> <code>OS_REGION_NAME</code> </td>
    <td> La regione in cui i tuoi oggetti vengono archiviati. {{site.data.keyword.objectstorageshort}} è disponibile nelle regioni di Dallas e Londra. </td>
  </tr>
  <tr>
    <td> <code>OS_AUTH_URL</code> </td>
    <td> L'URL endpoint. Assicurati che `/v3` sia aggiunto alla fine dell'URL. </td>
  </tr>
</table>

Tabella 1: Descrizioni e variabili di autenticazione 

####  Aggiunta delle credenziali del servizio nella IU
1. Nella scheda **Credenziali del servizio** nel dashboard della tua istanza del servizio, fai clic su **Nuova credenziale** e forniscile un nome.
2. (*Facoltativo*) nel campo di testo **Aggiungi i parametri di configurazione incorporati**, immetti le informazioni sulla credenziale per il ruolo che desideri creare. Le informazioni devono essere formattate come payload JSON. Per ulteriori informazioni sui ruoli utente di {{site.data.keyword.objectstorageshort}}, consulta [Tipi di accesso](../os_security.html#access-types).
    - Per creare un utente amministrativo: `{"role":"admin"}`
    - Per creare un utente non amministrativo: `{"role":"member"}`
3. Fai clic su **Aggiungi**.


## Tipi di accesso. {: #access-types}

L'accesso al servizio è controllato dai ruoli utente e gli elenchi del controllo dell'accesso al contenitore. Gli utenti {{site.data.keyword.objectstorageshort}} possono essere sia amministrativi che non amministrativi. Gli elenchi del controllo dell'accesso vengono abilitati dagli utenti amministrativi al livello del contenitore e non sono disponibili per l'istanza del servizio, per l'account di archiviazione o al livello del progetto.

<table>
  <tr>
    <th> Utenti amministrativi (ammin) </th>
    <th> Utenti non amministrativi (membro) </th>
  </tr>
  <tr>
    <td> Gestisci il controllo dell'accesso </td>
    <td> Per impostazione predefinita, non si dispone dell'accesso al servizio o ai relativi contenitori </td>
  </tr>
  <tr>
    <td> Puoi creare e eliminare i contenitori </td>
    <td> Puoi eseguire azioni in base alle ACL di lettura/scrittura dei contenitori </td>
  </tr>
  <tr>
    <td> Puoi leggere e scrivere nei contenitori </td>
    <td> Puoi eseguire azioni come determinato dall'amministratore </td>
  </tr>
</table>

Tabella 2: Ruoli utente definiti 

Puoi gestire gli utenti {{site.data.keyword.objectstorageshort}} tramite l'interfaccia utente {{site.data.keyword.Bluemix_notm}}, l'API o la CLI Cloud Foundry.




## Concessione dell'accesso in lettura {: #read-access}

Un utente {{site.data.keyword.objectstorageshort}} con un ruolo da amministratore può concedere l'accesso in lettura a un contenitore a un altro utente e modificare le combinazioni ACL di lettura.

<table>
  <tr>
    <th> Autorizzazione </th>
    <th> Opzioni Read ACL </th>
  </tr>
  <tr>
    <td> Legge tutti i riferimenti indipendentemente dall'affiliazione dell'account </td>
    <td> <code> .r,*` </code> </td>
  </tr>
  <tr>
    <td> Legge e elenca tutti i riferimenti e li elenca </td>
    <td> <code>.r:*,.rlistings</code> </td>
  </tr>
  <tr>
    <td> Legge e elenca un utente specifico in un progetto specifico </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> Legge e elenca un utente specifico in qualsiasi progetto </td>
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> Legge e elenca ogni utente in un progetto specifico </td>
    <td> <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> Legge e elenca ogni utente in ogni progetto  </td>
    <td> <code> *:* </code> </td>
  </tr>
</table>

Tabella 3: Autorizzazioni dell'accesso in lettura per opzione 



1. Autenticazione delle tue credenziali. Puoi utilizzare le credenziali trovate nella scheda delle credenziali del servizio della IU o puoi generare nuove credenziali. Per ulteriori informazioni sulla generazione di nuove credenziali, consulta [Generazione delle credenziali del servizio](insert link here). Riceverai il tuo URL e token di autenticazione {{site.data.keyword.objectstorageshort}} come output.
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

    Puoi controllare nel seguente output di esempio se è stato concesso l'accesso in lettura:

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



## Concessione dell'accesso in scrittura {: #write-access}

Un utente {{site.data.keyword.objectstorageshort}} con un ruolo da amministratore può concedere l'accesso in scrittura a un contenitore a un altro utente e modificare le combinazioni ACL di scrittura.

<table>
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
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> Scrivi ogni utente in un progetto specifico </td>
    <td>  <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> Scrivi ogni utente in ogni progetto </td>
    <td>  <code> *:* </code> </td>
  </tr>
</table>

Tabella 4: Autorizzazioni dell'accesso in scrittura per opzione 



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

2. Concedi l'accesso in scrittura immettendo il seguente comando:
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



## Rimozione dell'accesso {: #removing-access}

Per rimuovere i read ACL da un contenitore:
* Comando Swift:

    ```
    swift post <container_name> --read-acl “”
    ```
    {: pre}

*  Comando cURL:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

Per rimuovere i write ACL da un contenitore:

* Comando Swift:

    ```
    swift post <container_name> --write-acl “”
    ```
    {: pre}

*  Comando cURL:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

Per verificare di aver rimosso un ACL:

* Comando Swift:

    ```
    swift stat <container_name>
    ```
    {: pre}

  Il seguente output di esempio mostra sia l'ACL in lettura che in scrittura come vuoti, il che significa che l'accesso è stato rimosso.

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
