---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
# Einführung in {{site.data.keyword.objectstorageshort}}  {: #using-object-storage}
*Letzte Aktualisierung: 19. Oktober 2016*
{: .last-updated}

# Mithilfe der Swift-CLI auf {{site.data.keyword.objectstorageshort}} zugreifen{: #using-swift-cli}


Der {{site.data.keyword.objectstorageshort}}-Service basiert auf OpenStack Swift und ist für jede beliebige kompatible Clientanwendung zugänglich. In diesem Abschnitt wird die Verwendung des Python Swift-Clients beschrieben. Dies ist die Befehlszeilenschnittstelle (CLI, Command-Line Interface) für die {{site.data.keyword.objectstorageshort}}-API und die zugehörigen Erweiterungen für die Arbeit mit Containern und Dateien.
{: shortdesc}

## Swift-Client installieren {: #install-swift-client}

Sofern noch nicht geschehen, installieren Sie die folgenden [Softwarevoraussetzungen](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}.
* Python 2.7 oder höher
* Setuptools-Paket
* Pip-Paket

Zur Installation des Python Swift-Clients führen Sie folgenden Befehl aus:
  ```
  sudo pip install python-swiftclient
  ```
  {: pre}

Zur Installation des Python Keystone-Clients führen Sie folgenden Befehl aus:
  ```
  sudo pip install python-keystoneclient
  ```
  {: pre}




## Client einrichten {: #setup-swift-client}

Zur Einrichtung des Swift-Clients müssen Sie Ihre Authentifizierungsinformationen `exportieren`. Sie können Ihre Berechtigungsnachweise aus der Benutzerschnittstelle verwenden oder [neue Berechtigungsnachweise generieren](../ObjectStorage/os_cli.html#generating-cli).

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
  {: codeblock}




## {{site.data.keyword.objectstorageshort}}-Serviceberechtigungsnachweise generieren {: #generating-cli}

Zum Generieren von Serviceberechtigungsnachweisen mithilfe der Swift-CLI können Sie die folgenden Schritte ausführen.

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} als Benutzer mit einer Entwicklerrolle an. Sie müssen sich in dem Bereich der Serviceinstanz befinden, die Sie verwalten wollen.
      ```
      cf login -a api.ng.bluemix.net -u <Benutzer-ID> -p <Kennwort> -o <Organisation> -s <Bereich>
      ```
      {: pre}
2. Generieren Sie Serviceberechtigungsnachweise. `Serviceschlüsselname` ist der Name für Ihren Berechtigungsnachweis. Sie können entweder den Cloud Foundry-Befehl oder den cURL-Befehl verwenden.
    Cloud Foundry-Befehl:
      ```
      cf create-service-key "<Name der Object Storage-Serviceinstanz>" <Serviceschlüsselname> -c '{"role":"<Object Storage-Rolle>"}'
      ```
      {: pre}
      Cloud Foundry-Beispielbefehl:
      ```
      cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'
      ```
      {: screen}
      cURL-Befehl:
      ```
      curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<Serviceinstanz-GUID>",   "name": "<Benutzername>", "role": "member"}' -X POST -H "Authorization: <Trägertoken>" -H "Content-Type: " -H "Cookie: "
      ```
      {: pre}
3. Validieren Sie die Berechtigungsnachweise für den von Ihnen erstellten Serviceschlüssel.
      Cloud Foundry-Befehl:
      ```
      cf service-key <Serviceschlüsselname> <Member-Name>
      ```
      {: pre}
      Beispiel-Member-Serviceschlüssel für eine Instanz mit dem Namen 'Object-Storage-Acl-Test':
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
      cURL-Befehl:
      ```
      curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <Trägertoken>" -H "Cookie: "
      ```
      {: pre}




## Mithilfe der CLI Objekte in Containern speichern{: #storing-cli}

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an. Stellen Sie sicher, dass Sie sich in der richtigen Organisation und dem richtigen Arbeitsbereich befinden, um mit Ihrer Instanz von {{site.data.keyword.objectstorageshort}} zu arbeiten.
    ```
    cf login -a api.ng.bluemix.net -u <Benutzer-ID> -p <Kennwort> -o <Organisation> -s <Bereich>
    ```
    {: pre}
2. Erstellen Sie einen neuen Container, indem Sie folgenden Befehl ausführen. Die Variable *Containername* wird zu diesem Zeitpunkt von Ihnen festgelegt.
    ```
    swift post <Containername>
    ```
    {: pre}
3. (*Optional*) Um zu überprüfen, ob Ihr Container erstellt wurde, führen Sie folgenden Befehl zur Auflistung Ihrer Container aus.
    ```
    swift list
    ```
    {: pre}
4. Laden Sie eine Datei in Ihren Container hoch, indem Sie folgenden Befehl ausführen.
    ```
    swift upload <Containername> <Dateiname>
    ```
    {: pre}
    **Hinweis**: Zum Hochladen von Dateien von mehr als 5 GB sind zusätzliche Schritte erforderlich. Weitere Informationen finden Sie unter [Mit umfangreichen Dateien arbeiten](../ObjectStorage/os_large_files.html#large-files).
5. (*Optional*) Um zu überprüfen, ob der Upload erfolgreich war, führen Sie den folgenden Befehl aus, mit dem der Inhalt Ihres Containers angezeigt wird:
    ```
    swift list <Containername>
    ```
    {: pre}

**Hinweis**: Wenn Sie eine Datei mit identischem Namen hochladen, ersetzt {{site.data.keyword.objectstorageshort}} die gespeicherte Datei durch die neue Datei. Wenn Sie eine Datei herunterladen und Bearbeitungen vornehmen, achten Sie darauf, die Datei umzubenennen, oder [richten Sie eine Objektversionierung ein](../ObjectStorage/os_versioning.html#work-with-object-versioning), bevor Sie sie hochladen, um beide Versionen der Datei beizubehalten.



## Mithilfe der Swift-CLI Objekte herunterladen{: #downloading-cli}

1.  Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an. Stellen Sie sicher, dass Sie sich in der richtigen Organisation und dem richtigen Arbeitsbereich befinden, um mit Ihrer Instanz von {{site.data.keyword.objectstorageshort}} zu arbeiten.
    ```
    cf login -a api.ng.bluemix.net -u <Benutzer-ID> -p <Kennwort> -o <Organisation> -s <Bereich>
    ```
    {: pre}
2. Laden Sie eine Datei herunter, indem Sie folgenden Befehl ausführen:
    ```
    swift download <Containername> <Dateiname>
    ```
    {: pre}




## Mithilfe der CLI Objekte und Container löschen{: #deleting-cli}

1.  Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an. Stellen Sie sicher, dass Sie sich in der richtigen Organisation und dem richtigen Arbeitsbereich befinden, um mit Ihrer Instanz von {{site.data.keyword.objectstorageshort}} zu arbeiten.
    ```
    cf login -a api.ng.bluemix.net -u <Benutzer-ID> -p <Kennwort> -o <Organisation> -s <Bereich>
    ```
    {: pre}
2. Führen Sie folgenden Befehl aus, um eine Datei zu löschen:
    ```
    swift delete <Containername> <Dateiname>
    ```
    {: pre}
    **Hinweis**: Sie können [für die Löschung Ihres Objekts einen bestimmten Zeitpunkt festlegen](../ObjectStorage/os_deletion.html#schedule-object-deletion).
3. Zum Löschen des Containers führen Sie folgenden Befehl aus:
    ```
    swift delete <Containername>
    ```
    {: pre}
    **Achtung**: Mit dem Löschen Ihres Containers löschen Sie alle Objekte, die im Container enthalten sind.





## Mit Verzeichnissen arbeiten{: #directory-cli}

#### Mithilfe der Swift-CLI einem Container ein Verzeichnis hinzufügen

Swift hat keine eigentliche Verzeichnisstruktur, verwendet jedoch eine bestimmte Benennung, um eine Verzeichnisstruktur darzustellen. Wenn Sie einen Verzeichnisnamen angeben, wird dieser als Teil des relativen Pfads an alle Dateinamen angehängt.

1. Führen Sie folgenden Befehl aus, um einem Container ein Verzeichnis hinzuzufügen:
    ```
    swift upload <Containername> <Verzeichnisname>
    ```
    {: pre}

#### Verzeichnis herunterladen
Zum Herunterladen einer Verzeichnisstruktur verwenden Sie den Parameter `-prefix`, um das Verzeichnis bzw. die Verzeichnisstruktur anzugeben, das/die heruntergeladen werden soll.

1. Führen Sie folgenden Befehl aus, um ein Verzeichnis herunterzuladen:
    ```
    swift download <Containername> --prefix <Verzeichnis>
    ```
    {: pre}
