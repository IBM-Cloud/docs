---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Serviceberechtigungsnachweise generieren {: #credentials}

Serviceberechtigungsnachweise werden zur Bereitstellung der Authentifizierung und Sicherheit für den Service verwendet. Sie können mithilfe der CLI oder der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle neue Berechtigungsnachweise generieren.
{: shortdesc}


## Führen Sie die folgenden Schritte durch, um in der Benutzerschnittstelle Berechtigungsnachweise hinzuzufügen:

1. Klicken Sie auf der Registerkarte **Serviceberechtigungsnachweise** in Ihrem Serviceinstanz-Dashboard auf **Neuer Berechtigungsnachweis** und benennen Sie diesen.
2. Optional: Geben Sie in das Textfeld **Lineare Konfigurationsparameter hinzufügen** die Informationen zu dem Berechtigungsnachweis für die Rolle mit der [Art des Zugriffs](/docs/services/ObjectStorage/os_access_types.html) ein, den Sie gewähren möchten. Die Informationen müssen als JSON-Nutzdaten formatiert sein.
    - Zum Erstellen eines Benutzers mit Administratorberechtigungen: `{"role":"admin"}`
    - Zum Erstellen eines Benutzers ohne Administratorberechtigungen: `{"role":"member"}`
3. Klicken Sie auf **Hinzufügen**.


## Führen Sie die folgenden Schritte aus, um Berechtigungsnachweise mithilfe von Cloud Foundry-Befehlen in der CLI hinzuzufügen:

1. Wenn Sie nicht bei {{site.data.keyword.Bluemix_notm}} angemeldet sind, melden Sie sich als Benutzer mit einer Entwicklerrolle an. Sie müssen sich in dem Bereich der Serviceinstanz befinden, die Sie verwalten wollen.
  ```
  cf login -a api.ng.bluemix.net -u <Benutzer-ID> -p <Kennwort> -o <Organisation> -s <Bereich>
  ```
  {: pre}

2. Generieren Sie Serviceberechtigungsnachweise. Geben Sie dem Berechtigungsnachweis einen Namen, indem Sie die Variable
`serviceschlüsselname` entsprechend ersetzen. Optional können Sie auch eine [Benutzerrolle](/docs/services/ObjectStorage/os_access_types.html) zuweisen.

  ```
  cf create-service-key "<Serviceinstanzname>" <Serviceschlüsselname> -c '{"role":"<Benutzerrolle>"}'
  ```
  {: pre}

  Beispiel:
  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'
  ```
  {: screen}

3. Validieren Sie die Berechtigungsnachweise für den von Ihnen erstellten Schlüssel.

  ```
  cf service-keys <Serviceinstanzname>
  ```
  {: pre}

  Beispielschlüssel für eine Instanz mit dem Namen 'Object-Storage-Acl-Test' für einen Benutzer mit einer Mitgliedsrolle:

  ```
  {
    "auth_url": "https://identity.open.softlayer.com",
    "domainId": "8753ff40ac1a4f4a9f162ad8026b6ce0",
    "domainName": "757955",
    "password": "xxxxxxxx",
    "project": "object_storage_6046b6e2_ee53_4884_916f_89c65e4d408e",
    "projectId": "c727d7e248b448f6b268f31a1bd8691e",
    "region": "dallas",
    "role": "member",
    "userId": "3c5b516655e4479881d3d216895faedb",
    "username": "member_2afbeea1d58b1867f46c699553d1e4513e7df83a"
  }
  ```
  {: screen}



#### Führen Sie die folgenden Schritte aus, um Berechtigungsnachweise mithilfe von cURL-Befehlen in der CLI hinzuzufügen:

1. Wenn Sie nicht bei {{site.data.keyword.Bluemix_notm}} angemeldet sind, melden Sie sich als Benutzer mit einer Entwicklerrolle an. Sie müssen sich in dem Bereich der Serviceinstanz befinden, die Sie verwalten wollen.

  ```
  cf login -a api.ng.bluemix.net -u <Benutzer-ID> -p <Kennwort> -o <Organisation> -s <Bereich>
  ```
  {: pre}

2. Führen Sie den folgenden Befehl aus, um Serviceberechtigungsnachweise zu generieren.

  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<Serviceinstanz-GUID>",   "name: <Serviceinstanzname>", "role: <Benutzerrolle>"}' -X POST -H "Authorization: <Trägertoken>" -H "Content-Type: <Inhaltstyp" -H "Cookie: <Cookie>"
  ```
  {: pre}

  <table>
  <caption> Tabelle 1. Beschriebene Variablen für die cURL-Serviceberechtigungsnachweise</caption>
    <tr>
      <th> Variable  </th>
      <th> Erläuterung </th>
    </tr>
    <tr>
      <td> <code>https://api.ng.bluemix.net/v2/service_keys</code> </td>
      <td> Der Endpunkt des Serviceschlüssels.  </td>
    </tr>
    <tr>
      <td><i> service_instance_guid </i></td>
      <td> Befindet sich in Ihrer URL.  </td>
    </tr>
    <tr>
      <td><i> name </i></td>
      <td> Der Name der Serviceinstanz. </td>
    </tr>
    <tr>
      <td><i> role </i></td>
      <td> Gibt die <a href= /docs/services/ObjectStorage/os_constructing.html>Benutzerrolle</a> als Administrator oder als Mitglied an. </td>
    </tr>
    <tr>
      <td><i> bearer_token </i></td>
      <td> Das Token, das Sie bei der Authentifizierung der Instanz mit Keystone erhalten haben. </td>
    </tr>
  </table>



3. Überprüfen Sie Ihre Berechtigungsnachweise, indem Sie den folgenden Befehl ausführen.

  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <Trägertoken>" -H "Cookie: "
  ```
  {: screen}
