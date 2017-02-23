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


# Lesezugriff erteilen

Ein {{site.data.keyword.objectstorageshort}}-Benutzer mit [Administratorrolle](/docs/services/ObjectStorage/os_access_types.html) kann einem anderen Benutzer Lesezugriff auf einen Container erteilen und verschiedene ACL-Kombinationen für Lesezugriff angeben.
{: shortdesc}

<table>
<caption> Tabelle 1. Lesezugriffsberechtigungen nach Option </caption>
  <tr>
    <th> Berechtigung </th>
    <th> Optionen für Lesezugriffssteuerung (Read ACL) </th>
  </tr>
  <tr>
    <td> Lesen für alle Referrer unabhängig von der Kontozuordnung </td>
    <td> <code> .r,&#42;  </code> </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für alle Referrer und Listen </td>
    <td> <code> .r:&#42;,.rlistings </code> </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für angegebenen Benutzer in bestimmtem Projekt </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für angegebenen Benutzer in jedem Projekt </td>
    <td> <code> &#42;:user_id </code> </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für jeden Benutzer in einem angegebenen Projekt </td>
    <td> <code> project_id:&#42; </code> </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für jeden Benutzer in jedem Projekt  </td>
    <td> <code> &#42;:&#42; </code> </td>
  </tr>
</table>


1. Authentifizieren Sie Ihre Berechtigungsnachweise. Sie können entweder die Berechtigungsnachweise aus der Registerkarte 'Serviceberechtigungsnachweise' der Benutzerschnittstelle verwenden oder neue Berechtigungsnachweise generieren. Weitere Informationen zum Generieren neuer Berechtigungsnachweise finden Sie unter [Serviceberechtigungsnachweise generieren](/docs/services/ObjectStorage/os_credentials.html). Sie erhalten Ihre {{site.data.keyword.objectstorageshort}}-URL und das Authentifizierungstoken als Ausgabe.

    Swift-Befehl:

    ```
    export OS_USER_ID=<Benutzer-ID>
  export OS_PASSWORD=<Kennwort>
  export OS_TENANT_ID=<Projekt-ID>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<Region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

    swift auth
    ```
    {: codeblock}

    cURL-Befehl:

    ```
    curl -i -H "X-Auth-User: <Benutzer-ID>" -H "X-Auth-Key: <Kennwort>" <Authentifizierungs-URL>
    ```
    {: pre}

2. Führen Sie folgenden Befehl aus, um Lesezugriff zu erteilen:
    Swift-Befehl:

    ```
    swift post <Containername> --read-acl "<Benutzer-ID>:<Projekt-ID>"
    ```
    {: pre}

    cURL-Befehl:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <Tenant-ID>:<Projekt-ID>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}
    **Hinweis**: Verwenden Sie zum Trennen der Zugriffssteuerungslisten ein Komma (,).

3. Überprüfen Sie den Wert für die Lesezugriffssteuerungsliste (Read ACL).

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

    Beispiel: Der Wert für `X-Container-Read` zeigt, für welchen Container Lesezugriff erteilt wird und welchen Personen Lesezugriff gewährt wird.

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
