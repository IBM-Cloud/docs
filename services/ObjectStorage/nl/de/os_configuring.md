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

# CLI für die Verwendung von Swift- und Cloud Foundry-Befehlen konfigurieren

Für die Interaktion mit dem {{site.data.keyword.objectstorageshort}}-Service über Swift- oder Cloud Foundry-Befehle müssen Sie die entsprechenden Softwarevoraussetzungen installieren.
{: shortdesc}


## Swift-Client installieren {: #install-swift-client}

Sofern noch nicht geschehen, installieren Sie die folgenden Softwarevoraussetzungen.
* Python 2.7 oder höher
* Setuptools-Paket
* Pip-Paket
* Cloud Foundry-CLI


Zur Installation des Python Swift-Clients führen Sie folgenden Befehl aus:
```
pip install python-swiftclient
```
{: pre}

Zur Installation des Python Keystone-Clients führen Sie folgenden Befehl aus:
```
pip install python-keystoneclient
```
{: pre}

Weitere Informationen zu den Voraussetzungen finden Sie in der <a href="http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software" target="_blank">OpenStack-Dokumentation. <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>



## Client einrichten {: #setup-swift-client}

Zur Konfiguration des Swift-Clients müssen Sie Ihre Authentifizierungsinformationen `exportieren`. Sie können über die CLI [Berechtigungsnachweise generieren](/docs/services/ObjectStorage/os_credentials.html), indem Sie Cloud Foundry- oder cURL-Befehle über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle verwenden. Der Client entnimmt die Informationen den Umgebungsvariablen in der folgenden Tabelle:

<table>
<caption> Tabelle 1. Umgebungsvariablen und Beschreibungen </caption>
  <tr>
    <th> Umgebungsvariable </th>
    <th> Beschreibung </th>
  </tr>
  <tr>
    <td> <code>OS_USER_ID</code> </td>
    <td> Ihre {{site.data.keyword.objectstorageshort}}-Benutzer-ID. </td>
  </tr>
  <tr>
    <td> <code>OS_PASSWORD</code> </td>
    <td> Das Kennwort für Ihre {{site.data.keyword.objectstorageshort}}-Instanz. </td>
  </tr>
  <tr>
    <td> <code>OS_PROJECT_ID</code> </td>
    <td> Ihre Projekt-ID. </td>
  </tr>
  <tr>
    <td> <code>OS_REGION_NAME</code> </td>
    <td> Die Region, in der Ihre Objekte gespeichert sind. {{site.data.keyword.objectstorageshort}} steht in den Regionen Dallas und London zur Verfügung. </td>
  </tr>
  <tr>
    <td> <code>OS_AUTH_URL</code> </td>
    <td> Die Endpunkt-URL. Achten Sie darauf, am Ende der URL die Angabe <code>/v3</code> hinzuzufügen. </td>
  </tr>
</table>



Um Ihre Authentifizierungsdaten zu exportieren, müssen Sie Ihre Berechtigungsnachweise eingeben und den folgenden Befehl ausführen:
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


Beispiel:
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
