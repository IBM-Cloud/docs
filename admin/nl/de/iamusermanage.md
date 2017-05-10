---

copyright:

  years: 2015, 2017

lastupdated: "2017-04-10"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Benutzerkonten und Benutzerzugriff verwalten
{: #iamusermanage}

Abhängig von den Zugriffsoptionen, zu deren Verwaltung Sie berechtigt sind, können Sie Benutzer aus dem gesamten Konto oder der gesamten Organisation anzeigen und verwalten. Als Kontoeigner können Sie Benutzer in einer beliebigen dieser Zugriffsoptionen, die Sie verwalten und auf die dem Benutzer der Zugriff erteilt ist, unabhängig von der Rolle im aktuellen Konto verwalten. Sie können Zugriffsrechte für Benutzer in einer beliebigen der von Ihnen verwalteten Zugriffsoptionen zuweisen, bearbeiten und entfernen. 
{:shortdesc}

Zur Verwaltung von Benutzern in Ihrem Konten klicken Sie in der Menüleiste auf **Verwalten** &gt; **Konto** &gt; **Benutzer**. Das Fenster 'Benutzer' zeigt eine Liste der Benutzer mit den zugehörigen E-Mail-Adressen und Angaben zum aktuellen Status in den Konten an, die Sie verwalten. Wählen Sie im Fenster 'Benutzer' den zu verwaltenden Benutzer aus oder klicken Sie auf **Benutzer verwalten** im Menü **Aktionen**. Es werden die Richtlinientabellen für die Zugriffsoptionen angezeigt, die Sie für den betreffenden Benutzer verwalten können.

## Durch Identity and Access aktivierte Services
{: #iammanidaccser}

Wenn der Benutzer Zugriff auf einen **durch Identity and Access aktivierten Service** hat, werden Informationen zu den zugewiesenen Richtlinien im Fenster 'Benutzer verwalten' angezeigt.  Die für den betreffenden Benutzer oder die betreffende Gruppe angezeigten Informationen sind von den zugewiesenen Richtlinien abhängig. Wenn keine Richtlinien zugewiesen sind, wird eine Nachricht angezeigt, durch die Sie gefragt werden, ob Sie eine Richtlinie zuweisen möchten. Wenn bereits Richtlinien zugewiesen sind, wird eine Liste der Richtlinien mit der Rolle des Benutzers bzw. der Gruppe und einer Beschreibung der Ressourcenattribute für jede Richtlinie angezeigt. Sie können Richtlinien auf der Seite für Richtlinienzuweisung zuweisen, indem Sie auf **Servicerichtlinien zuweisen** klicken. Die Option **Servicerichtlinien zuweisen** ist aktiviert, wenn Sie berechtigt sind, Richtlinien zu erstellen. Sie können vorhandene Richtlinien verwalten, indem Sie auf die Richtlinie in der Liste klicken oder indem Sie auf die Option **Richtlinie bearbeiten** unter **Aktionen** in der Zeile der Richtlinie klicken, die Sie bearbeiten wollen.

## Cloud Foundry-Servicezugriff verwalten
{: #iammancfser}

Wenn einem Benutzer Zugriff auf **Cloud Foundry** zugewiesen ist, werden Ihnen die Organisationen und Bereiche, die dem Benutzer zugeordnet sind, im Fenster 'Benutzer verwalten' angezeigt. Sie können den Benutzer aus einer Organisation entfernen oder die Rolle ändern, die für eine Organisation oder einen Bereich zugewiesen ist. Sie können einen Benutzer einer anderen Organisation hinzufügen, indem Sie auf **Organisation zuweisen** klicken, wenn Sie der Manager einer Organisation sind, in der der Benutzer noch nicht Mitglied ist. Sie können vorhandene Bereichs- und Organisationsrollen verwalten, indem Sie auf die Option **Bereichsrolle bearbeiten** bzw. **Organisationsrolle bearbeiten** in der Zeile der Rolle klicken, die Sie bearbeiten wollen.

## Richtlinien verwalten
{: #iamusermanpol}

Sie können Richtlinien für einen Benutzer zuweisen und verwalten, der Zugriff auf **durch Identity and Access aktivierte Services** hat. Eine Richtlinie weist einem Benutzer eine oder mehrere Rollen für eine Gruppe von Ressourcen durch eine Kombination von Attributen zur Definition der betreffenden Gruppe von Ressourcen zu.

Wenn Sie eine Richtlinie einem Benutzer zuweisen, geben Sie zuerst den zuzuweisenden Service an. Die Liste **Service** stellt die Option für bestimmte Services und eine Option zur Zuweisung aller verfügbaren Services bereit. Sie wählen außerdem eine oder mehrere Rollen aus, die zugewiesen werden.

Abhängig von dem Service, den Sie auswählen, sind zusätzliche Konfigurationsoptionen verfügbar. Sie können einen Service auswählen, um Optionen für diesen Service anzuzeigen.

Sie können die Liste der angezeigten Serviceoptionen eingrenzen. Klicken Sie auf **Optionalen Servicekontext angeben**, um zusätzliche Optionen wie Regionen und Serviceinstanzen anzugeben.  Sie wollen möglicherweise nicht alle Optionen angeben, die angezeigt werden, jedoch können Sie die Optionen auswählen, die konfiguriert werden sollen.

Sie können Richtlinien zuweisen und verwalten, wenn Sie die entsprechende Rolle haben. In der folgenden Tabelle werden die Richtlinienmanagementtasks und die jeweils erforderliche Rolle aufgeführt.


{: #iamui_table1}

| Aktion | Erforderliche Rolle |
|----------|---------|
| Richtlinie für ein Konto erstellen | Administrator für das Konto |
| Richtlinie für alle Services in einem Konto erstellen | Administrator für das Konto |
| Richtlinie für alle Serviceinstanzen in einem Konto erstellen | Administrator für das Konto |
| Richtlinie für einen Service in einem Konto erstellen | Administrator für das Konto oder Administrator für den Service im Konto |
| Serviceinstanz erstellen | Administrator oder Editor für das Konto oder Administrator oder Editor für den Service im Konto |
| Richtlinie für eine Serviceinstanz erstellen | Administrator für das Konto oder Administrator für den Service im Konto oder Administrator für die Serviceinstanz |
{: caption="Tabelle 1. Verwaltungstasks zum Verwalten von Richtlinien für **durch Identity and Access aktivierte Services**" caption-side="top"}

## Rollen zuweisen und verwalten
{: #iamusermanrol}

Rollen sind Sammlungen von Aktionen. Die Aktionen, die diesen Rollen zugeordnet sind, sind je nach Service unterschiedlich.
Da Aktionen unter Rollen zusammengruppiert sind, können Sie mit einem kleinen Satz definierter Rollen beliebige Aktionen für beliebige Services und Ressourcen unterstützen. Wenn Sie zum Beispiel einen Administrator für virtuelle Maschinen, Speicher und Vernetzung benötigen, können Sie den Benutzer als Administrator für alle drei Bereiche festlegen, indem Sie das Ziel der Richtlinie ändern. In diesem Fall würden Sie die Richtlinie so festlegen, dass sie den Administrator für virtuelle Maschinen, den Speicheradministrator und den Netzadministrator umfasst.

Ressourcen sind nicht in die Rollen einbezogen, sodass nicht für jeden Typ von Ressource, der in das System eingeführt wird, neue Rollennamen erstellt werden. Es ist zum Beispiel nicht erforderlich, eine Rolle für den Administrator virtueller Maschinen, eine Rolle für den Speicheradministrator und eine Rolle für den Netzadministrator für die Ressourcen virtueller Maschinen, für Speicherressourcen und für Netzressourcen zu haben.

Neben den Beschreibungen der Rollen, die in der Benutzerschnittstelle verfügbar sind, werden in der folgenden Tabelle Beispiele für einige der Tasks aufgeführt, die Benutzer, denen eine Rolle zugewiesen ist, ausführen können.

{: #iamui_table2}

| Rolle | Beschreibung von Aktionen | Beispielaktionen|
|:-----------------|:-----------------|:-----------------|
| Viewer (Anzeigeberechtigter) | Führt Aktionen aus, die den Status nicht ändern; Aktionen im Lesezugriff. | <ul><li>Geräte auflisten</li><li>Speicherobjekt lesen</li><li>Abfragen ausführen</li><li>Suchen durchführen</li></ul>|
| Editor (Bearbeiter) | Führt Aktionen aus, die den Status ändern und die Unterressourcen erstellen oder löschen. |<ul><li>Virtuelle Maschinen erstellen oder löschen</li><li>Speicher anhängen</li><li>Neu starten</li><li>Starten oder stoppen</li><li>Umbenennen</li></ul> |
| Administrator | Führt alle Aktionen aus, einschließlich der Möglichkeit, die Zugriffssteuerung zu verwalten. |<ul><li>Benutzer einladen</li><li>Virtuelle Maschinen erstellen oder löschen</li><li>Benutzerzugriffsrichtlinien aktualisieren</li><li>Geräte auflisten</li><li>Speicher anhängen</li><li>Neu starten</li><li>Starten oder stoppen</li><li>Umbenennen</li><li>Backup und Restore durchführen</li></ul>|
{: caption="Tabelle 2. Verwaltungstasks zum Verwalten von Richtlinien für **durch Identity and Access aktivierte Services**" caption-side="top"}

Weitere spezielle Informationen zu Rollen von Benutzern mit Zugriff auf Cloud Foundry finden Sie unter [Benutzerrollen](/docs/admin/users_roles.html#userrolesinfo).

Wenn Sie Benutzer hinzufügen, müssen Sie mindestens eine Rolle auswählen. Sie können jedoch auch mehrere Rollen auswählen. Wenn Sie eine Rolle auswählen, wird eine Definition für diese Rolle angezeigt, sodass Sie die Rolle bzw. Rollen, die angegeben werden sollen, bestimmen können.  Die Rollen, die Sie zuweisen, haben zwar verschiedene Zugriffsoptionen, jedoch immer für den Zugriff auf die Ressourcenattribute, die Sie angeben.

Wenn Sie den **Cloud Foundry**-Service ausgewählt haben, werden die Rollen, die Sie zuweisen, den Organisationen und Bereichen zugeordnet, die Sie auswählen.
