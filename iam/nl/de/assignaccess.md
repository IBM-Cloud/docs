---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-11"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Benutzerzugriff zuordnen
{: #assignaccess}

Bei der Einladung weisen Sie den Benutzern Zugriffsrechte, Rollen und Richtlinien sowie die Konten oder Organisationen (oder beides) zu, auf die sie zugreifen können. Abhängig von den Zugriffsoptionen, zu deren Verwaltung Sie berechtigt sind, können Sie Benutzer aus dem gesamten Konto, der gesamten Organisation, dem gesamten Bereich oder der gesamten Serviceinstanz einladen und mit Zugriffsrechten ausstatten. Als Kontoeigner können Sie Ihrem Konto Zugriffsoptionen für einen Benutzer unabhängig von der Rolle zuweisen, wenn sowohl Sie als auch der Benutzer Mitglieder sind. In den folgenden Abschnitten werden die drei Arten von Zugriff beschrieben, die einem eingeladenen Benutzer zugeordnet werden können.{:shortdesc}

## Durch Identity and Access aktivierte Services

Sie können eine einzelne Servicerichtlinie zuordnen, wenn Sie einen neuen Benutzer einladen. Sobald der Benutzer die Einladung angenommen hat, können Sie zusätzliche Servicerichtlinien hinzufügen.

1. Erweitern Sie in der Anzeige **Benutzer einladen** den Abschnitt **Durch Identity and Access aktivierte Services**.
2. Wählen Sie **Alle durch Identity and Access aktivierten Services** oder einen einzelnen Service aus. **Hinweis:** Wenn Sie die Option **Der Zugriff wird automatisch erteilt, wenn neue Services hinzugefügt werden** auswählen, werden Sie nicht benachrichtigt, um jeden neuen {{site.data.keyword.Bluemix_notm}}-Service für diesen Benutzer abwählen zu können, wenn Services später hinzugefügt werden.
3. Wählen Sie **Alle aktuellen Regionen** oder eine bestimmte Region aus.
4. Wählen Sie **Alle aktuellen Serviceinstanzen** oder eine bestimmte Serviceinstanz aus.
5. Wählen Sie eine Rolle aus, um den Zugriffsbereich für die Richtlinie zu definieren.
6. Optional: Wählen Sie **Rolle hinzufügen** aus, um eine weitere Rolle für die Richtlinie anzugeben.

Nähere Informationen zum Festlegen von Servicerichtlinien finden Sie in [Richtlinien und Rollen für Identity and Access Management](/docs/iam/users_roles.html#iamusermanpol).

## Cloud Foundry-Zugriff

Allen Benutzern wird standardmäßig die Rolle des Organisationsauditors erteilt. Nachdem der Benutzer die Einladung angenommen hat, können Sie diese Rolle auf die Organisationsrolle des Abrechnungsmanagers, Organisationsmanager oder auf keine Organisationsrolle aktualisieren. Während des Einladungsprozesses können Sie mehrere Bereichsrollen nacheinander hinzufügen.

1. Erweitern Sie in der Anzeige **Benutzer einladen** den Abschnitt **Cloud Foundry-Zugriff**.
2. Wählen Sie eine Organisation aus, zu der der Benutzer hinzugefügt werden soll.
3. Wählen Sie **Alle aktuellen Regionen** oder eine bestimmte Region aus.
4. Wählen Sie **Alle aktuellen Bereiche** oder einen bestimmten Bereich aus.
5. Wählen Sie eine Rolle aus, um den Zugriffsbereich zu definieren.
6. Optional: Wählen Sie **Rolle hinzufügen** aus, um eine weitere Rolle für die Richtlinie anzugeben.

Nähere Informationen zu diesen Rollen finden Sie in [Cloud Foundry-Rollen](/docs/iam/users_roles.html#cfroles).

## Infrastructure-Zugriff

Wenn Sie über die entsprechende Berechtigung verfügen, sehen Sie die Option zum Zuweisen von Infrastructure-Berechtigungen. Die tatsächlichen zugewiesenen Berechtigungen werden automatisch auf die Untergruppe von Berechtigungen eingeschränkt, die Sie haben. Weitere Informationen zu den Berechtigungen und welche Aktionen der Benutzer mit jeder dieser Berechtigungen ausführen kann, finden Sie unter [Infrastructure-Berechtigungen](/docs/iam/users_roles.html#infrapermissions).

1. Erweitern Sie in der Anzeige **Benutzer einladen** den Abschnitt **Infrastructure-Zugriff**. 
2. Wählen Sie eine Berechtigung aus, um den Zugriffsbereich zu definieren.

Informationen zum Konfigurieren von Zugriff für Benutzer, nachdem diese Ihrem Konto hinzugefügt wurden, finden Sie unter [Benutzerkonten und Benutzerzugriff verwalten](/docs/iam/iamusermanage.html).
