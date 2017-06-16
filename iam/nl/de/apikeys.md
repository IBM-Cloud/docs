---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-10"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# API-Schlüssel verwalten
{: #manapikey}

Ein API-Schlüssel ist ein Code, der von Computerprogrammen übergeben wird, die eine Anwendungsprogrammierschnittstelle (API) aufrufen, um das aufrufende Programm, dessen Entwickler oder den zugehörigen Benutzer der Website zu identifizieren. Mit API-Schlüsseln kann überwacht und gesteuert werden, wie die API verwendet wird, beispielsweise um die böswillige Verwendung oder den Missbrauch der API zu verhindern (wie z. B. durch die Nutzungsbestimmungen festgelegt). Der API-Schlüssel dient oft als eine eindeutige Kennung und geheimes Token für Authentifizierung und normalerweise ist ihm eine Gruppe von Zugriffsberechtigungen für die API zugeordnet. API-Schlüssel können auf einem UUID-System (UUID - Universal Unique Identifier) basieren, um sicherzustellen, dass sie für jeden Benutzer eindeutig sind.

Als {{site.data.keyword.Bluemix_notm}}-Benutzer können Sie einen API-Schlüssel verwenden, wenn Sie ein Programm oder Script aktivieren, ohne Ihr Kennwort an das Script weiterzugeben. Ein Vorteil bei der Verwendung eines API-Schlüssels kann sein, dass ein Benutzer oder eine Organisation mehrere API-Schlüssel für verschiedene Programme erstellen kann und die API-Schlüssel können einzeln gelöscht werden, wenn diese kompromittiert wurden, ohne dass sich dies auf andere API-Schlüssel oder gar den Benutzer auswirkt. Darüber hinaus können Sie als [föderierter Benutzer](/docs/admin/adminpublic.html#federatedid) einen API-Schlüssel für die Anmeldung verwenden. Weitere Informationen zur Verwendung eines API-Schlüssel für die Anmeldung finden Sie in der Dokumentation zum [{{site.data.keyword.Bluemix_notm}}-CLI-Befehl `bluemix login`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_login) und zum [Befehl `cf login` der Befehlszeilenschnittstelle 'cf'](/docs/cli/reference/cfcommands/index.html#cf_login).

Sie können die {{site.data.keyword.Bluemix_notm}}-API-Schlüssel über das Fenster 'Bluemix-API-Schlüssel' verwalten. Wechseln Sie zu **Verwalten** &gt; **Sicherheit** &gt; **Bluemix-API-Schlüssel**, um eine Liste der API-Schlüssel mit entsprechenden Beschreibungen und Datumsangaben anzuzeigen. Sie können über diese Seite API-Schlüssel erstellen, bearbeiten oder löschen.

Gehen Sie wie folgt vor, um einen API-Schlüssel zu erstellen:

1. Wechseln Sie zu **Verwalten** &gt; **Sicherheit** &gt; **Bluemix-API-Schlüssel**.
2. Klicken Sie auf **API-Schlüssel erstellen**.
3. Geben Sie einen Namen und eine Beschreibung für den API-Schlüssel ein.
4. Klicken Sie auf **API-Schlüssel erstellen**.
5. Klicken Sie anschließend auf **Anzeigen**, um den API-Schlüssel anzuzeigen, um ihn zu kopieren und für eine spätere Verwendung zu speichern, oder klicken Sie auf **API-Schlüssel herunterladen**.

**Hinweis**: Der API-Schlüssel steht nur zum Zeitpunkt seiner Erstellung zum Anzeigen oder Herunterladen zur Verfügung. Wenn der API-Schlüssel verloren geht, müssen Sie einen neuen API-Schlüssel erstellen.

Gehen Sie wie folgt vor, um einen API-Schlüssel zu bearbeiten:

1. Wechseln Sie zu **Verwalten** &gt; **Sicherheit** &gt; **Bluemix-API-Schlüssel**.
2. Klicken Sie im Menü **Aktionen** eines in der Tabelle aufgeführten API-Schlüssels auf **Name & Beschreibung bearbeiten**. 
3. Aktualisieren Sie die Informationen für den API-Schlüssel.
4. Klicken Sie auf **API-Schlüssel aktualisieren**.

Gehen Sie wie folgt vor, um einen API-Schlüssel zu löschen: 

1. Wechseln Sie zu **Verwalten** &gt; **Sicherheit** &gt; **Bluemix-API-Schlüssel**.
2. Klicken Sie im Menü **Aktionen** eines in der Tabelle aufgeführten API-Schlüssels auf **Löschen**.
3. Bestätigen Sie anschließend den Löschvorgang durch Klicken auf **Schlüssel löschen**.

Sie können auch die {{site.data.keyword.Bluemix_notm}}-CLI für die Verwaltung der API-Schlüssel verwenden, indem Sie Schlüssel auflisten, erstellen, aktualisieren oder löschen. Weitere Informationen finden Sie im Abschnitt zum Befehl [`bluemix iam api-keys`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam).

