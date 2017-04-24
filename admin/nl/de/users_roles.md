---

copyright:

  years: 2015, 2016
lastupdated: "2017-03-01"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Benutzer und Rollen für den Cloud Foundry-Servicezugriff im Teamverzeichnis verwalten
{: #userroles}

Sie können Plattformbenutzer, denen Cloud Foundry-Servicezugriff erteilt wurde, über die Seite 'Teamverzeichnis' für Ihr Konto verwalten. Sie können vorhandene Teammitglieder und ihre Rollen in Ihrer Organisation und Ihren Bereichen verwalten.
{:shortdesc}

Sie können auf das Teamverzeichnis für Ihr Konto über einen Link im oberen Bereich der neuen Seite 'Benutzer' zugreifen. Um auf die Seite 'Benutzer' zuzugreifen, klicken Sie im {{site.data.keyword.Bluemix_notm}}-Menü auf **Verwalten** &gt; **Konto** &gt; **Benutzer**. 

Kontoeigner führen alle Operationen für Organisationen und Bereiche aus, einschließlich Operationen zur Verwaltung von Teammitgliedern und ihren zugewiesenen Rollen. Organisationsmanager haben Zugriff zur Verwaltung von Rollen. Bereichsmanager können die Seite **Organisationen verwalten** verwenden, um vorhandene Kontomitglieder dem Bereich hinzuzufügen und deren Rollen anzupassen. Lesen Sie die folgenden Informationen, um mehr über Rollen zu erfahren.

## Benutzerrollen
{: #userrolesinfo}

Auf Kontoebene gibt es zwei Rollen, die den Zugriff auf andere Kontoverwaltungsfunktionen ermöglichen:

| Kontorolle | Berechtigungen |
|----------------|---------|
|Eigner | Ein Eigner für das Konto verfügt über Zugriff auf sein Profil, das Teamverzeichnis, die Rechnungsinformationen, die Informationen zu Ausgaben und das Nutzungsdashboard. Auf der Seite 'Teamverzeichnis' kann der Eigner neue Teammitglieder einladen und deren Rollen anpassen. Der Eigner kann auch Werbeguthaben hinzufügen, das Abrechnungslimit festlegen oder ändern, den Servicezugriff festlegen und Organisationen und Bereiche verwalten. |
|Mitglied | Ein Mitglied hat Zugriff auf sein Profil, das Teamverzeichnis und auf Limits für Kontoguthaben und Abrechnung im {{site.data.keyword.Bluemix_notm}}-Header. Ein Mitglied kann auf der Seite 'Teamverzeichnis' jedoch nur die Teammitglieder innerhalb des Kontos anzeigen. |
{:caption="Table 1. Account roles and permissions" caption-side="top"}

Alle neuen Teammitglieder werden als Mitglied des Kontos hinzugefügt. Sie können Organisations- und Bereichsrollen für eingeladene Personen zuordnen, um bestimmte Ansichten und Berechtigungen in {{site.data.keyword.Bluemix_notm}} zu aktivieren. Neue Teammitglieder, die einer Organisation hinzugefügt wurden (lokale oder dedizierte Umgebungen ausgenommen), erhalten standardmäßig die Rolle des Organisationsauditors. Für einen bestimmten Bereich können Sie eingeladenen Personen die Rollen 'Entwickler' oder 'Auditor' zuordnen. Sobald die eingeladenen Personen die Einladung annehmen und an {{site.data.keyword.Bluemix_notm}} teilnehmen, können Sie deren Rollen auf der Seite 'Teamverzeichnis' bearbeiten. 

Die folgenden Rollen können auf Organisationsebene hinzugefügt werden:

| Organisationsrolle | Berechtigungen |
|-------------------|-------------|
|Manager | Organisationsmanager können Bereiche innerhalb der Organisation erstellen, anzeigen, bearbeiten oder löschen, die Nutzung und das Kontingent der Organisation anzeigen, Teammitglieder zur Organisation einladen, steuern, wer Zugriff auf die Organisation und die Rollen in der Organisation hat, und die angepassten Domänen für die Organisation verwalten. |
|Abrechnungsmanager | Abrechnungsmanager können Informationen zur Laufzeit- und Servicenutzung für die Organisation auf der Seite 'Nutzungsdashboard' anzeigen.  |
|Auditor | Organisationsauditoren können Anwendungs- und Serviceinhalte in der Organisation anzeigen. Auditoren können Teammitglieder in der Organisation und deren zugeordnete Rollen sowie das Kontingent für die Organisation auch anzeigen. Außer in lokalen oder dedizierten Umgebungen ist diese Rolle standardmäßig allen eingeladenen Personen zugeordnet. |
{:caption="Table 2. Organization roles and permissions" caption-side="top"}

Die folgenden Rollen können auf Bereichsebene zugeordnet werden:

| Bereichsrolle | Berechtigungen |
|------------|-------------|
|Manager | Bereichsmanager können vorhandene Teammitglieder hinzufügen und Rollen innerhalb des Bereichs verwalten. Der Bereichsmanager kann auch die Anzahl der Instanzen, die Servicebindungen und die Nutzung der Ressource für jede Anwendung im Bereich anzeigen. |
|Entwickler | Bereichsentwickler können Anwendungen und Services innerhalb des Bereichs erstellen, löschen und verwalten. Einige der Verwaltungstasks umfassen das Bereitstellen, Starten oder Stoppen von Apps, das Umbenennen oder Löschen von Apps, das Umbenennen eines Bereichs, das Binden oder Aufheben der Bindung eines Service an eine Anwendung, das Anzeigen der Anzahl der Instanzen, Servicebindungen und der Ressourcennutzung für jede Anwendung im Bereich. Darüber hinaus kann der Bereichsentwickler eine interne oder externe URL einer Anwendung im Bereich zuordnen.   |
|Auditor | Bereichsauditoren haben Lesezugriff auf alle Informationen zu Bereichen, beispielsweise auf Informationen zur Anzahl der Instanzen, zu Servicebindungen und zur Ressourcennutzung für jede Anwendung im Bereich. |
{:caption="Table 3. Space roles and permissions" caption-side="top"}

**Hinweis:** Teammitglieder, denen eine Bereichsmanager- oder Bereichsentwicklerrolle zugeordnet wurde, können auf die Umgebungsvariable VCAP_SERVICES zugreifen. Ein Teammitglied, dem die Auditorrolle zugeordnet wurde, kann nicht auf VCAP_SERVICES zugreifen.

## Rollen bearbeiten
{: #editinguserroles}

Kontoeigner und Organisationsmanager können Organisationen und Bereichsrollen für vorhandene Teammitglieder auf der Seite 'Teamverzeichnis' bearbeiten. 

1. Suchen Sie die Teammitglieder, deren Rollen Sie bearbeiten möchten, und wählen Sie sie aus. 
2. Klicken Sie auf **Rollen anzeigen**. 
3. Wählen Sie die Bereichsrolle aus oder löschen Sie die Auswahl der Bereichsrolle, um den Bereichszugriff für das Teammitglied zu ändern.
4. Klicken Sie auf **Speichern**.

Bereichsmanager können Rollen für die Teammitglieder in ihrem Bereich verwalten. 

1. Suchen Sie die Teammitglieder, deren Rollen Sie bearbeiten möchten, und wählen Sie sie aus. 
2. Klicken Sie auf **Rollen anzeigen**. 
3. Klicken Sie auf **Bereiche anzeigen**. 
4. Wählen Sie die Option für die Bereichsrolle aus oder löschen Sie die Auswahl für die Option der Bereichsrolle, die Sie für das Teammitglied hinzufügen oder entfernen möchten.
5. Klicken Sie anschließend auf **Speichern**. 

## Teammitglieder einladen
{: #inviteteammembers}

Sie können einen Benutzer über das Fenster 'Teamverzeichnis' hinzufügen, wenn die Benutzer-ID kein verknüpftes Konto ist und wenn Sie Kontoeigner oder Organisationsmanager sind. Wenn Sie neue Teammitglieder hinzufügen (lokale oder dedizierte Umgebungen ausgenommen), werden diesen automatisch Auditorrollen zugewiesen. Sie können die Rollen später auf der Seite 'Teamverzeichnis' ändern. Führen Sie die folgenden Schritte aus, um ein Teammitglied einzuladen:

<ol>
<li>Klicken Sie auf **Benutzer einladen**. </li>
<li>Geben Sie die E-Mail-Adresse für den einzuladenden Benutzer ein. </li>
<li>Wählen Sie die Rolle aus, die für die Organisation zugewiesen werden soll. </li>
<li>Wählen Sie die Rolle aus, die für einen oder mehrere Bereiche in der Organisation zugewiesen werden soll. </li>
<li>Wählen Sie die Option zum Bestätigen aus, dass Sie die finanzielle Verantwortung für alle Gebühren übernehmen, die für das Konto anfallen. </li>
<li>Klicken Sie auf **Einladen**. </li>
</ol>

Der Benutzer wird der angezeigten Liste von Teammitgliedern für das Konto hinzugefügt. 

## Teammitglieder entfernen
{: #removingteammembers}

Wenn der Benutzer über die Seite 'Teamverzeichnis' hinzugefügt wurde und kein verknüpftes Konto ist, können Kontoeigner und Organisationsmanager Teammitglieder aus einem Konto über die Seite 'Teamverzeichnis' entfernen. Führen Sie die folgenden Schritte aus, um ein Teammitglied zu entfernen:

1. Suchen Sie den Benutzer, der entfernt werden soll, und klicken Sie auf das Symbol **Benutzer entfernen** ![Symbol 'Entfernen'](../icons/icon_remove_teamuser.svg). 
2. Klicken Sie auf **Entfernen**, um das Entfernen des angegebenen Benutzers aus dem Konto zu bestätigen. 

Der Benutzer wird aus der angezeigten Liste der Teammitglieder für dieses Konto entfernt.
