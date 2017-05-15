---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# GitHub-Paket verwenden
{: #openwhisk_catalog_github}

Das Paket `/whisk.system/github` bietet eine komfortable Methode zur Verwendung der [GitHub-APIs](https://developer.github.com/).

Das Paket enthält den folgenden Feed:

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/github` | Paket | username, repository, accessToken | Interaktion mit der GitHub-API |
| `/whisk.system/github/webhook` | Feed | events, username, repository, accessToken | Aktivieren von Auslöserereignissen für GitHub-Aktivitäten |

Es wird empfohlen, eine Paketbindung mit den Werten `username`, `repository` und `accessToken` zu erstellen.  Mit der Bindung brauchen Sie die Werte nicht jedes Mal anzugeben, wenn Sie den Feed im Paket verwenden.

## Auslöserereignis für GitHub-Aktivität aktivieren

Der Feed `/whisk.system/github/webhook` konfiguriert einen Service so, dass ein Auslöser aktiviert wird, wenn eine Aktivität in einem angegebenen GitHub-Repository stattfindet. Die folgenden Parameter sind verfügbar:

- `username`: Der Benutzername für das GitHub-Repository.
- `repository`: Das GitHub-Repository.
- `accessToken`: Ihr persönliches GitHub-Zugriffstoken. Wenn Sie Ihr [Token erstellen](https://github.com/settings/tokens), stellen Sie sicher, dass Sie die Geltungsbereiche 'repo:status' und 'public_repo' auswählen. Stellen Sie außerdem sicher, dass noch keine Web-Hooks für Ihr Repository definiert sind.
- `events`: Der interessierende [GitHub-Ereignistyp](https://developer.github.com/v3/activity/events/types/).

Das folgende Beispiel zeigt, wie ein Auslöser erstellt wird, der jedes Mal aktiviert wird, wenn eine neue Festschreibung (Commit) in einem GitHub-Repository erfolgt.

1. Generieren Sie ein [persönliches Zugriffstoken](https://github.com/settings/tokens) für GitHub.
  
  Das Zugriffstoken wird im nächsten Schritt verwendet.
  
2. Erstellen Sie eine Paketbindung, die für Ihr GitHub-Repository und mit Ihrem Zugriffstoken konfiguriert ist.
  
  ```
  wsk package bind /whisk.system/github myGit \
    --param username myGitUser \
    --param repository myGitRepo \
    --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}
  
3. Erstellen Sie einen Auslöser für den GitHub-Ereignistyp `push` unter Verwendung Ihres Feeds `myGit/webhook`.
  
  ```
  wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}
  
  Ein Commit für ein Github-Repository mithilfe von `git push` führt dazu, dass der Auslöser durch den Web-Hook ausgelöst wird. Falls eine Regel zutrifft, die mit dem Auslöser übereinstimmt, wird die zugeordnete Aktion aufgerufen.
  Von der Aktion werden die Nutzdaten für den GitHub-Web-Hook als Eingabeparameter empfangen. Jedes GitHub-Web-Hook-Ereignis weist ein ähnliches JSON-Schema und ein eindeutiges Nutzdatenobjekt auf, das vom jeweiligen Ereignistyp abhängt.
  Weitere Informationen zum Nutzdateninhalt finden Sie in der API-Dokumentation unter [GitHub-Ereignisse und -Nutzdaten](https://developer.github.com/v3/activity/events/types/).
  
