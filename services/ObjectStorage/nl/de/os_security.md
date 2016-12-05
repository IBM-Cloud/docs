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


# Dateien schützen {: #understanding-authentication}


## Informationen zu Berechtigungsnachweisen {: #understanding-credentials}

Serviceberechtigungsnachweise werden zur Bereitstellung der Authentifizierung und Sicherheit für den Service verwendet. Bei der Bereitstellung einer Instanz wird automatisch ein Satz von Berechtigungsnachweisen generiert. Der Swift-Client entnimmt die Authentifizierungsinformationen den Umgebungsvariablen in der folgenden Tabelle:

<table>
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
    <td> Die Endpunkt-URL. Achten Sie darauf, am Ende der URL die Angabe `/v3` hinzuzufügen. </td>
  </tr>
</table>

Tabelle 1: Variablen und Beschreibungen für die Authentifizierung

####  Serviceberechtigungsnachweise in der Benutzerschnittstelle hinzufügen
1. Klicken Sie auf der Registerkarte **Serviceberechtigungsnachweise** in Ihrem Serviceinstanz-Dashboard auf **Neuer Berechtigungsnachweis** und benennen Sie diesen.
2. (*Optional*) Geben Sie in das Textfeld **Lineare Konfigurationsparameter hinzufügen** die Informationen zu dem Berechtigungsnachweis für die Rolle ein, die Sie erstellen wollen. Die Informationen müssen als JSON-Nutzdaten formatiert sein. Weitere Informationen zu {{site.data.keyword.objectstorageshort}}-Benutzerrollen finden Sie unter [Zugriffstypen](../os_security.html#access-types).
    - Zum Erstellen eines Benutzers mit Administratorberechtigungen: `{"role":"admin"}`
    - Zum Erstellen eines Benutzers ohne Administratorberechtigungen: `{"role":"member"}`
3. Klicken Sie auf **Hinzufügen**.


## Zugriffstypen {: #access-types}

Der Zugriff auf den Service wird durch Benutzerrollen und Zugriffssteuerungslisten für Container gesteuert. {{site.data.keyword.objectstorageshort}}-Benutzer können Benutzer mit Administratorberechtigungen oder Benutzer ohne Administratorberechtigungen sein. Zugriffssteuerungslisten werden durch Administratorbenutzer auf der Containerebene aktiviert und sind für die Serviceinstanz, das Speicherkonto oder auf Projektebene nicht verfügbar.

<table>
  <tr>
    <th> Benutzer mit Administratorberechtigungen (admin) </th>
    <th> Benutzer ohne Administratorberechtigungen (member) </th>
  </tr>
  <tr>
    <td> Zugriffssteuerung verwalten </td>
    <td> Standardmäßig kein Zugriff auf den Service oder seine Container </td>
  </tr>
  <tr>
    <td> Container erstellen und löschen </td>
    <td> Aktionen abhängig von den Lese-/Schreibzugriffssteuerungslisten der Container </td>
  </tr>
  <tr>
    <td> Containerinhalt lesen und schreiben </td>
    <td> Durch den Administrator festgelegte Aktionen </td>
  </tr>
</table>

Tabelle 2: Definierte Benutzerrollen

Sie können {{site.data.keyword.objectstorageshort}}-Benutzer über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle, die Cloud Foundry-API oder die Cloud Foundry CLI verwalten.




## Lesezugriff erteilen {: #read-access}

Ein {{site.data.keyword.objectstorageshort}}-Benutzer mit Administratorrolle kann einem anderen Benutzer Lesezugriff auf einen Container erteilen und verschiedene ACL-Kombinationen für Lesezugriff angeben.

<table>
  <tr>
    <th> Berechtigung </th>
    <th> Optionen für Lesezugriffssteuerung (Read ACL) </th>
  </tr>
  <tr>
    <td> Lesen für alle Referrer unabhängig von der Kontozuordnung </td>
    <td> <code> .r,*` </code> </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für alle Referrer und Listen </td>
    <td> <code>.r:*,.rlistings</code> </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für angegebenen Benutzer in bestimmtem Projekt </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für angegebenen Benutzer in jedem Projekt </td>
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für jeden Benutzer in angegebenem Projekt </td>
    <td> <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für jeden Benutzer in jedem Projekt  </td>
    <td> <code> *:* </code> </td>
  </tr>
</table>

Tabelle 3: Lesezugriffsberechtigungen nach Option



1. Authentifizieren Sie Ihre Berechtigungsnachweise. Sie können entweder die Berechtigungsnachweise aus der Registerkarte 'Serviceberechtigungsnachweise' der Benutzerschnittstelle verwenden oder neue Berechtigungsnachweise generieren. Weitere Informationen zum Generieren neuer Berechtigungsnachweise finden Sie unter [Serviceberechtigungsnachweise generieren](insert link here). Sie erhalten Ihre {{site.data.keyword.objectstorageshort}}-URL und das Authentifizierungstoken als Ausgabe.
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

    In der folgenden Beispielausgabe sehen Sie, dass Lesezugriff erteilt wurde:

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



## Schreibzugriff erteilen {: #write-access}

Ein {{site.data.keyword.objectstorageshort}}-Benutzer mit Administratorrolle kann einem anderen Benutzer Schreibzugriff auf einen Container erteilen und verschiedene ACL-Kombinationen für Schreibzugriff angeben.

<table>
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
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> Schreiben für jeden Benutzer in angegebenem Projekt </td>
    <td>  <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> Schreiben für jeden Benutzer in jedem Projekt </td>
    <td>  <code> *:* </code> </td>
  </tr>
</table>

Tabelle 4: Schreibzugriffsberechtigungen nach Option



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

2. Führen Sie folgenden Befehl aus, um Schreibzugriff zu erteilen:
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



## Zugriff entfernen {: #removing-access}

Gehen Sie wie folgt vor, um Lesezugriffssteuerungslisten von einem Container zu entfernen:
* Swift-Befehl:

    ```
    swift post <Containername> --read-acl “”
    ```
    {: pre}

*  cURL-Befehl:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

Gehen Sie wie folgt vor, um Schreibzugriffssteuerungslisten von einem Container zu entfernen:

* Swift-Befehl:

    ```
    swift post <Containername> --write-acl “”
    ```
    {: pre}

*  cURL-Befehl:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

Überprüfen Sie, ob eine Zugriffssteuerungsliste (ACL) entfernt wurde:

* Swift-Befehl:

    ```
    swift stat <Containername>
    ```
    {: pre}

  Die folgende Beispielausgabe zeigt sowohl die Lesezugriffssteuerung (Read ACL) als auch die Schreibzugriffssteuerung (Write ACL) leer an, d. h. der Zugriff wurde entfernt.

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

* cURL-Befehl:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
  {: pre}
