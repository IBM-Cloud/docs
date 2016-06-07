---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Teammitglieder und Rollen verwalten
{: #userroles}
*Letzte Aktualisierung: 16. Mai 2016*

Auf der Seite **Teamverzeichnis** für Ihr Konto können Sie vorhanden Teammitglieder und deren Rollen in Ihrer Organisation und in Bereichen verwalten sowie neue Teammitglieder einladen. Um auf das Teamverzeichnis für Ihr Konto zuzugreifen, klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../admin/images/account_support.svg) &gt; **Konto** &gt; *ihr_kontoname* &gt; **Teamverzeichnis**.
{:shortdesc}

Kontoeigner führen alle Operationen für Organisationen und Bereiche einschließlich der Verwaltung der Teammitglieder und der ihnen zugeordneten Rollen aus. Organisationsmanager können Teammitglieder einladen und Rollen verwalten. Bereichsmanager können die Seite **Organisationen verwalten** verwenden, um vorhandene Kontomitglieder zum Bereich hinzuzufügen und deren Rollen anzupassen. Lesen Sie die folgenden Informationen, um mehr über Rollen zu erfahren. 

## Rollen
{: #userrolesinfo}

Auf Kontoebene gibt es zwei Rollen, die den Zugriff auf andere Kontoverwaltungsfunktionen ermöglichen: 

*Tabelle 1. Kontorollen und Berechtigungen*

| Kontorolle | Berechtigungen |    
|----------------|---------|
|Eigner | Ein Eigner für das Konto verfügt über Zugriff auf sein Profil, das Teamverzeichnis, die Rechnungsinformationen, die Informationen zu Ausgaben und das Nutzungsdashboard. Auf der Seite 'Teamverzeichnis' kann der Eigner neue Teammitglieder einladen und deren Rollen anpassen. Der Eigner kann auch Werbeguthaben hinzufügen, das Abrechnungslimit festlegen oder ändern, den Servicezugriff festlegen und Organisationen und Bereiche verwalten.  |
|Mitglied | Ein Mitglied hat Zugriff auf sein Profil, das Teamverzeichnis und auf Limits für Kontoguthaben und Abrechnung im {{site.data.keyword.Bluemix_notm}}-Header. Ein Mitglied kann auf der Seite 'Teamverzeichnis' jedoch nur die Teammitglieder innerhalb des Kontos anzeigen.  |

 Alle neuen Teammitglieder werden als Mitglied des Kontos hinzugefügt. Sie können Organisations- und Bereichsrollen für eingeladene Personen zuordnen, um bestimmte Ansichten und Berechtigungen in {{site.data.keyword.Bluemix_notm}} zu aktivieren. Neue Teammitglieder, die zu einer Organisation hinzugefügt wurden, erhalten standardmäßig die Rolle des Organisationsauditors. Für einen bestimmten Bereich können Sie eingeladenen Personen die Rollen 'Entwickler' oder 'Auditor' zuordnen. Sobald die eingeladenen Personen die Einladung annehmen und bei {{site.data.keyword.Bluemix_notm}} teilnehmen, können Sie deren Rollen auf der Seite **Teamverzeichnis** bearbeiten. 

Die folgenden Rollen können auf Organisationsebene hinzugefügt werden: 

*Tabelle 2. Organisationsrollen und Berechtigungen*

| Organisationsrolle | Berechtigungen |    
|-------------------|-------------|
|Manager | Organisationsmanager können Bereiche innerhalb der Organisation erstellen, anzeigen, bearbeiten oder löschen, die Nutzung und das Kontingent der Organisation anzeigen, Teammitglieder zur Organisation einladen, steuern, wer Zugriff auf die Organisation und die Rollen in der Organisation hat und die angepassten Domänen für die Organisation verwalten.  |
|Abrechnungsmanager | Abrechnungsmanager können Informationen zur Laufzeit- und Servicenutzung für die Organisation auf der Seite 'Nutzungsdashboard' anzeigen.   |
|Auditor | Organisationsauditoren können Anwendungs- und Serviceinhalte in der Organisation anzeigen. Auditoren können Teammitglieder in der Organisation und deren zugeordnete Rollen sowie das Kontingent für die Organisation auch anzeigen. Diese Rolle ist standardmäßig allen eingeladenen Personen zugeordnet. |

Die folgenden Rollen können auf Bereichsebene zugeordnet werden: 

*Tabelle 3. Bereichsrollen und Berechtigungen*

| Bereichsrolle | Berechtigungen |    
|------------|-------------|
|Manager | Bereichsmanager können vorhandene Teammitglieder hinzufügen und Rollen innerhalb des Bereichs verwalten. Der Bereichsmanager kann auch die Anzahl der Instanzen, die Servicebindungen und die Nutzung der Ressource für jede Anwendung im Bereich anzeigen.  |
|Entwickler | Bereichsentwickler können Anwendungen und Services innerhalb des Bereichs erstellen, löschen und verwalten. Einige der Verwaltungstasks umfassen das Implementieren, Starten oder Stoppen von Apps, das Umbenennen oder Löschen von Apps, das Umbenennen eines Bereichs, das Binden oder Aufheben der Bindung eines Service an eine Anwendung, das Anzeigen der Anzahl der Instanzen, Servicebindungen und der Ressourcennutzung für jede Anwendung im Bereich. Zusätzlich kann der Bereichsentwickler eine interne oder externe URL zu einer Anwendung im Bereich zuordnen.    |
|Auditor | Bereichsauditoren haben Lesezugriff auf alle Informationen zu Bereichen, beispielsweise auf Informationen zur Anzahl der Instanzen, zu Servicebindungen und zur Ressourcennutzung für jede Anwendung im Bereich.  |

**Hinweis**: Teammitglieder, denen eine Bereichsmanager- oder Bereichsentwicklerrolle zugeordnet wurde, können auf die Umgebungsvariable VCAP_SERVICES zugreifen. Ein Teammitglied, dem die Auditorrolle zugeordnet wurde, kann nicht auf VCAP_SERVICES zugreifen.

## Teammitglieder einladen
{: #inviteteammembers}

Kontoeigner und Organisationsmanager können Teammitglieder von der Seite 'Teammitglieder einladen' zu Organisationen einladen. Wenn Sie neue Teammitglieder hinzufügen, werden diesen automatisch Auditorrollen zugewiesen. Sie können die Rollen später auf der Seite 'Teamverzeichnis' ändern. Führen Sie die folgenden Schritte aus, um ein Teammitglied einzuladen: 

<ol>
<li>Klicken Sie auf das Symbol **Konto und Unterstützung** ![Symbol 'Konto und Unterstützung'](../admin/images/account_support.svg) &gt; **Konto** &gt; *ihr_kontoname* &gt; **Teammitglied einladen**.</li>
<li>Wählen Sie die Organisation aus, zu der Sie Teammitglieder einladen möchten. </li>
<li>Klicken Sie auf **Weiter**.</li>
<li>Wählen Sie die Bereiche aus, für die Sie Ihren Teammitgliedern Zugriff ermöglichen möchten. </li>
<li>Wählen Sie die Rolle aus, die den ausgewählten Bereichen in der Organisation zugewiesen werden soll. </li>
<li>Wählen Sie die Option zum Bestätigen aus, um zu bestätigen, dass Sie die finanzielle Verantwortung für alle Gebühren übernehmen, die auf dem Konto aufgelaufen sind. </li>
<li>Geben Sie die E-Mail-Adresse für ein einzelnes Teammitglied oder die Adressen mehrerer Teammitglieder an:
<ul>
<li>Um ein einzelnes Teammitglied hinzuzufügen, geben Sie die E-Mail-Adresse ein und klicken auf **Senden**.</li>
<li>Um mehr als ein Teammitglied hinzuzufügen, klicken Sie auf **Laden Sie alle Mitglieder auf einmal ein**. Geben Sie die E-Mail-Adressen mithilfe eine durch Kommas, Leerzeichen oder Zeilenumbrüche getrennten Liste ein. Klicken Sie anschließend auf **Weiter**, um die E-Mail-Adressen zu überprüfen; um die Einladungen zu senden, klicken Sie auf **Senden**.</li>
</ul>
</li>
</ol>

Klicken Sie auf **Anstehendes anzeigen**, um zu prüfen, ob die Einladungen anstehend sind oder akzeptiert wurden. Sie können auswählen, die Einladungs-E-Mail erneut zu senden oder die Einladung für eine anstehende Einladung jederzeit stornieren. 

## Rollen bearbeiten
{: #editinguserroles}

Kontoeigner und Organisationsmanager können Organisationen und Bereichsrollen für vorhandene Teammitglieder auf der Seite **Teamverzeichnis** bearbeiten.  

1. Klicken Sie auf das Symbol **Konto und Unterstützung** ![Symbol 'Konto und Unterstützung'](../admin/images/account_support.svg) &gt; **Konto** &gt; *ihr_kontoname* &gt; **Teamverzeichnis**.
2. Suchen Sie die Teammitglieder, deren Rollen Sie bearbeiten möchten.
3. Klicken Sie auf **Rollen anzeigen**.
4. Wählen Sie die Organisationsrolle aus oder löschen Sie die Auswahl der Organisationsrolle, um den Organisationszugriff für das Teammitglied zu ändern. 
5. Klicken Sie auf **Bereiche anzeigen**, um die Bereichsrollen hinzuzufügen oder zu entfernen. 
6. Wählen Sie die Bereichsrolle aus oder löschen Sie die Auswahl der Bereichsrolle, um den Bereichszugriff für das Teammitglied zu ändern. 
7. Klicken Sie auf **Bereiche schließen**.
8. Klicken Sie auf **Speichern** am Ende der Seite. 

Bereichsmanager können Rollen für die Teammitglieder in ihren Bereichen auf der Seite **Organisation verwalten** bearbeiten. 

1. Klicken Sie auf das Symbol **Konto und Unterstützung** ![Symbol 'Konto und Unterstützung'](../admin/images/account_support.svg) &gt; **Konto** &gt; *ihr_kontoname* &gt; **Organisationen verwalten**.
2. Suchen Sie die Organisation, in der sich Ihr Bereich befindet. 
3. Klicken Sie auf **Details anzeigen**.
4. Suchen Sie Ihren Bereich und klicken Sie auf **Bereich bearbeiten**.
5. Wählen Sie die Registerkarte **Benutzer** aus.
6. Wählen Sie die Option für die Bereichsrolle aus oder löschen Sie die Auswahl für die Option der Bereichsrolle, die Sie für das Teammitglied hinzufügen oder entfernen möchten. 
7. Klicken Sie auf **Speichern**.
