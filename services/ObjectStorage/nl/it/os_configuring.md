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

# Configurazione della CLI per utilizzare i comandi Swift e Cloud Foundry

Per interagire con il servizio {{site.data.keyword.objectstorageshort}} utilizzando i comandi Swift o Cloud Foundry, devi installare il software prerequisito.
{: shortdesc}


## Installazione del client Swift {: #install-swift-client}

Se non lo hai già fatto, installa il seguente software prerequisito.
* Python 2.7 o successive
* Package setuptools
* Package pip
* CLI Cloud Foundry


Per installare il client Python Swift, esegui il seguente comando:
```
pip install python-swiftclient
```
{: pre}

Per installare il client Python Keystone, esegui il seguente comando:
```
pip install python-keystoneclient
```
{: pre}

Per ulteriori informazioni sui prequisiti, consulta <a href="http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software" target="_blank">la documentazione OpenStack. <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>



## Impostazione del client {: #setup-swift-client}

Per configurare il client Swift, devi `esportare` le tue informazioni di autenticazione. Puoi [generare le credenziali](/docs/services/ObjectStorage/os_credentials.html) tramite la CLI utilizzando i comandi Cloud Foundry o cURL o tramite la IU {{site.data.keyword.Bluemix_notm}}. Il client prende le informazioni di autenticazione dalle variabili di ambiente nella seguente tabella.

<table>
<caption> Tabella 1. Descrizioni e variabili di ambiente </caption>
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
    <td> L'URL endpoint. Assicurati che <code>/v3</code> sia aggiunto alla fine dell'URL. </td>
  </tr>
</table>



Per esportare le informazioni di autenticazione, immetti le tue credenziali ed esegui il seguente comando:
```
export OS_USER_ID=
export OS_PASSWORD=
export OS_PROJECT_ID=
export OS_AUTH_URL=
export OS_REGION_NAME=
export OS_IDENTITY_API_VERSION=
export OS_AUTH_VERSION=

swift auth
```
{: codeblock}


Esempio:
```
export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
  export OS_PASSWORD=*******
  export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=dallas
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

swift auth
```
{: screen}
