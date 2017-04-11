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


# Schreibzugriff erteilen

Ein {{site.data.keyword.objectstorageshort}}-Benutzer mit [Administratorrolle](/docs/services/ObjectStorage/os_access_types.html) kann einem anderen Benutzer Schreibzugriff erteilen und verschiedene ACL-Kombinationen für Schreibzugriff angeben.
{: shortdesc}

<table>
<caption> Tabelle 1. Schreibzugriffsberechtigungen nach Option </caption>
  <tr>
    <th> Berechtigung </th>
    <th> Optionen für Schreibzugriffssteuerung (Write ACL) </th>
  </tr>
  <tr>
    <td> Schreiben für angegebenen Benutzer in bestimmtem Projekt </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> Schreiben für angegebenen Benutzer in jedem Projekt </td>
    <td> <code> &#42;:user_id </code> </td>
  </tr>
  <tr>
    <td> Schreiben für jeden Benutzer in angegebenem Projekt </td>
    <td>  <code> project_id:&#42; </code> </td>
  </tr>
  <tr>
    <td> Schreiben für jeden Benutzer in jedem Projekt </td>
    <td>  <code> &#42;:&#42; </code> </td>
  </tr>
</table>



1. Authentifizieren Sie Ihre Berechtigungsnachweise mit den Informationen in den Serviceberechtigungsnachweisen, die Sie erstellt haben.  Sie erhalten Ihre {{site.data.keyword.objectstorageshort}}-URL und das Authentifizierungstoken als Ausgabe.

    Swift-Befehl:

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

    cURL-Befehl:

    ```
    curl -i -H "X-Auth-User:<Benutzer-ID>" -H "X-Auth-Key:<Kennwort>" https://identity.open.softlayer.com/v3
    ```
    {: pre}

2. Führen Sie den folgenden Befehl aus, um Schreibzugriff zu erteilen.

    Swift-Befehl:

    ```
    swift post <Containername> --write-acl "<Benutzer-ID>:<Projekt-ID>"
    ```
    {: pre}

    cURL-Befehl:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <Benutzer-ID>: <Projekt-ID>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}

    **Hinweis**: Verwenden Sie zum Trennen der Zugriffssteuerungslisten ein Komma (,).

3. Überprüfen Sie den Wert für die Schreibzugriffssteuerungsliste (Write ACL).

    Swift-Befehl:

    ```
    swift stat <Containername>
    ```
    {: pre}

    cURL-Befehl:

    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}
