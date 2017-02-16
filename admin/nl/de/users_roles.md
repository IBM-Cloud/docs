---



copyright:

  years: 2015, 2016
lastupdated: "2016-12-05"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}


# Teammitglieder und Rollen verwalten
{: #userroles}

Auf der Seite **Teamverzeichnis** für Ihr Konto können Sie vorhanden Teammitglieder und deren Rollen in Ihrer Organisation und in Bereichen verwalten sowie neue Teammitglieder einladen. Um auf das Teamverzeichnis für Ihr Konto zuzugreifen, klicken Sie auf das Symbol **Konto** > **Teamverzeichnis**. 
{:shortdesc}

Kontoeigner führen alle Operationen für Organisationen und Bereiche einschließlich der Verwaltung der Teammitglieder und der ihnen zugeordneten Rollen aus. Organisationsmanager können Teammitglieder einladen und Rollen verwalten. Bereichsmanager können die Seite **Organisationen verwalten** verwenden, um vorhandene Kontomitglieder zum Bereich hinzuzufügen und deren Rollen anzupassen. Lesen Sie die folgenden Informationen, um mehr über Rollen zu erfahren.

## Rollen
{: #userrolesinfo}

Auf Kontoebene gibt es zwei Rollen, die den Zugriff auf andere Kontoverwaltungsfunktionen ermöglichen:

| Kontorolle | Berechtigungen |
|----------------|---------|
|Eigner | Ein Eigner für das Konto verfügt über Zugriff auf sein Profil, das Teamverzeichnis, die Rechnungsinformationen, die Informationen zu Ausgaben und das Nutzungsdashboard. Auf der Seite 'Teamverzeichnis' kann der Eigner neue Teammitglieder einladen und deren Rollen anpassen. Der Eigner kann auch Werbeguthaben hinzufügen, das Abrechnungslimit festlegen oder ändern, den Servicezugriff festlegen und Organisationen und Bereiche verwalten. |
|Mitglied | Ein Mitglied hat Zugriff auf sein Profil, das Teamverzeichnis und auf Limits für Kontoguthaben und Abrechnung im {{site.data.keyword.Bluemix_notm}}-Header. Ein Mitglied kann auf der Seite 'Teamverzeichnis' jedoch nur die Teammitglieder innerhalb des Kontos anzeigen. |
{:caption="Table 1. Account roles and permissions" caption-side="top"}

 Alle neuen Teammitglieder werden als Mitglied des Kontos hinzugefügt. Sie können Organisations- und Bereichsrollen für eingeladene Personen zuordnen, um bestimmte Ansichten und Berechtigungen in {{site.data.keyword.Bluemix_notm}} zu aktivieren. Neue Teammitglieder, die einer Organisation hinzugefügt wurden (lokale oder dedizierte Umgebungen ausgenommen), erhalten standardmäßig die Rolle des Organisationsauditors. Für einen bestimmten Bereich können Sie eingeladenen Personen die Rollen 'Entwickler' oder 'Auditor' zuordnen. Sobald die eingeladenen Personen die Einladung annehmen und bei {{site.data.keyword.Bluemix_notm}} teilnehmen, können Sie deren Rollen auf der Seite **Teamverzeichnis** bearbeiten.

Die folgenden Rollen können auf Organisationsebene hinzugefügt werden:

| Organisationsrolle | Berechtigungen |
|-------------------|-------------|
|Manager | Organisationsmanager können Bereiche innerhalb der Organisation erstellen, anzeigen, bearbeiten oder löschen, die Nutzung und das Kontingent der Organisation anzeigen, Teammitglieder zur Organisation einladen, steuern, wer Zugriff auf die Organisation und die Rollen in der Organisation hat und die angepassten Domänen für die Organisation verwalten. |
|Abrechnungsmanager | Abrechnungsmanager können Informationen zur Laufzeit- und Servicenutzung für die Organisation auf der Seite 'Nutzungsdashboard' anzeigen.  |
|Auditor | Organisationsauditoren können Anwendungs- und Serviceinhalte in der Organisation anzeigen. Auditoren können Teammitglieder in der Organisation und deren zugeordnete Rollen sowie das Kontingent für die Organisation auch anzeigen. Außer in lokalen oder dedizierten Umgebungen ist diese Rolle standardmäßig allen eingeladenen Personen zugeordnet. |
{:caption="Table 2. Organization roles and permissions" caption-side="top"}

Die folgenden Rollen können auf Bereichsebene zugeordnet werden:

| Bereichsrolle | Berechtigungen |
|------------|-------------|
|Manager | Bereichsmanager können vorhandene Teammitglieder hinzufügen und Rollen innerhalb des Bereichs verwalten. Der Bereichsmanager kann auch die Anzahl der Instanzen, die Servicebindungen und die Nutzung der Ressource für jede Anwendung im Bereich anzeigen. |
|Entwickler | Bereichsentwickler können Anwendungen und Services innerhalb des Bereichs erstellen, löschen und verwalten. Einige der Verwaltungstasks umfassen das Bereitstellen, Starten oder Stoppen von Apps, das Umbenennen oder Löschen von Apps, das Umbenennen eines Bereichs, das Binden oder Aufheben der Bindung eines Service an eine Anwendung, das Anzeigen der Anzahl der Instanzen, Servicebindungen und der Ressourcennutzung für jede Anwendung im Bereich. Zusätzlich kann der Bereichsentwickler eine interne oder externe URL zu einer Anwendung im Bereich zuordnen.   |
|Auditor | Bereichsauditoren haben Lesezugriff auf alle Informationen zu Bereichen, beispielsweise auf Informationen zur Anzahl der Instanzen, zu Servicebindungen und zur Ressourcennutzung für jede Anwendung im Bereich. |
{:caption="Table 3. Space roles and permissions" caption-side="top"}

**Hinweis:** Teammitglieder, denen eine Bereichsmanager- oder Bereichsentwicklerrolle zugeordnet wurde, können auf die Umgebungsvariable VCAP_SERVICES zugreifen. Ein Teammitglied, dem die Auditorrolle zugeordnet wurde, kann nicht auf VCAP_SERVICES zugreifen.

## Sichtbarkeit des Teamverzeichnisses anpassen
{: #teamdirectoryvisibility}

Abhängig von der Konfiguration der {{site.data.keyword.Bluemix_notm}}-Konten und -Organisationen kann es sinnvoll sein, die Sichtbarkeit des Teamverzeichnisses der Teamverzeichnisseite zu ändern. Standardmäßig können alle Teammitglieder die gesamte Liste der Kontoteammitglieder anzeigen, einschließlich aller Mitglieder aller Organisationen in diesem Konto. Es kann sein, dass die Sichtbarkeit der Teamverzeichnisseite aus Datenschutz- oder Sicherheitsgründen angepasst werden muss. Es gibt zwei Optionen zum Einstellen der Sichtbarkeit der Teamverzeichnisseite: alle Teammitglieder oder nur Sie als Kontoeigner.

Führen Sie die folgenden Schritte aus, um die Sichtbarkeit der Teamverzeichnisseite zu ändern:

1. Klicken Sie auf **Konto** &gt; **Teamverzeichnis**.
2. Klicken Sie zur Verwendung der Option **Sichtbarkeit für** auf die aktuelle Auswahl zum Anzeigen der Optionen.
3. Wählen Sie anschließend abhängig von den aktuellen Anforderungen an das Konto **Alle** oder **Nur für mich** aus.
4. Anschließend klicken Sie auf **Speichern**.

## Teammitglieder einladen
{: #inviteteammembers}

Kontoeigner und Organisationsmanager können Teammitglieder von der Seite 'Teammitglieder einladen' zu Organisationen einladen. Wenn Sie neue Teammitglieder hinzufügen (lokale oder dedizierte Umgebungen ausgenommen), werden diesen automatisch Auditorrollen zugewiesen. Sie können die Rollen später auf der Seite 'Teamverzeichnis' ändern. Führen Sie die folgenden Schritte aus, um ein Teammitglied einzuladen:

<ol>
<li>Klicken Sie auf **Konto** &gt; **Teammitglieder einladen**.</li>
<li>Wählen Sie die Organisation aus, zu der Sie Teammitglieder einladen möchten.</li>
<li>Klicken Sie auf **Weiter**.</li>
<li>Wählen Sie die Bereiche aus, für die Sie Ihren Teammitgliedern Zugriff ermöglichen möchten.</li>
<li>Wählen Sie die Rolle aus, die den ausgewählten Bereichen in der Organisation zugewiesen werden soll.</li>
<li>Wählen Sie die Option zum Bestätigen aus, um zu bestätigen, dass Sie die finanzielle Verantwortung für alle Gebühren übernehmen, die auf dem Konto aufgelaufen sind.</li>
<li>Geben Sie die E-Mail-Adresse für ein einzelnes Teammitglied oder die Adressen mehrerer Teammitglieder an:
<ul>
<li>Um ein einzelnes Teammitglied hinzuzufügen, geben Sie die E-Mail-Adresse ein und klicken auf **Senden**.</li>
<li>Um mehr als ein Teammitglied hinzuzufügen, klicken Sie auf **Laden Sie alle Mitglieder auf einmal ein**. Geben Sie die E-Mail-Adressen mithilfe eine durch Kommas, Leerzeichen oder Zeilenumbrüche getrennten Liste ein. Klicken Sie anschließend auf **Weiter**, um die E-Mail-Adressen zu überprüfen; um die Einladungen zu senden, klicken Sie auf **Senden**.</li>
</ul>
</li>
</ol>

Klicken Sie auf **Anstehende anzeigen**, um zu prüfen, ob die Einladungen anstehend sind oder akzeptiert wurden. Sie können auswählen, die Einladungs-E-Mail erneut zu senden oder die Einladung für eine anstehende Einladung jederzeit stornieren.


### SoftLayer-Teammitglieder hinzufügen

Wenn ein SoftLayer-Konto mit Ihrem Bluemix-Konto verknüpft ist, können Sie die SoftLayer-Teammitglieder hinzufügen.

1. Wechseln Sie zu **Konto** > **Teammitglieder einladen**.  
2. Klicken Sie im Abschnitt **SoftLayer-Teammitglieder hinzufügen** auf **Hinzufügen**, um sich für Ihr SoftLayer-Konto zu authentifizieren und eine Liste der Teammitglieder aus Ihrem Softlayer-Konto anzuzeigen.

Das Hinzufügen von Teammitgliedern zu Ihrem Bluemix-Konto bedeutet nicht gleichzeitig die Erteilung von Zugriff auf die Bluemix-Infrastruktur. Um Benutzern Zugriff auf das Infrastruktur-Dashboard zu erteilen, wechseln Sie zu **Infrastruktur** > **Konto** > **Benutzer** und klicken Sie auf den Link **Benutzer hinzufügen**. Sie müssen über die Berechtigung zum Hinzufügen von Benutzern verfügen.

Weitere Informationen zum Hinzufügen von Teammitgliedern aus dem SoftLayer-Konto finden Sie in [SoftLayer-Teammitglieder zu Bluemix einladen](https://console.ng.bluemix.net/docs/admin/softlayerlink.html#invite_users).


## Rollen bearbeiten
{: #editinguserroles}

Kontoeigner und Organisationsmanager können Organisationen und Bereichsrollen für vorhandene Teammitglieder auf der Seite **Teamverzeichnis** bearbeiten.

1. Klicken Sie auf **Konto** &gt; **Teamverzeichnis**.
2. Suchen Sie die Teammitglieder, deren Rollen Sie bearbeiten möchten.
3. Klicken Sie auf **Rollen anzeigen**.
4. Wählen Sie die Organisationsrolle aus oder löschen Sie die Auswahl der Organisationsrolle, um den Organisationszugriff für das Teammitglied zu ändern.
5. Klicken Sie auf **Bereiche anzeigen**, um die Bereichsrollen hinzuzufügen oder zu entfernen.
6. Wählen Sie die Bereichsrolle aus oder löschen Sie die Auswahl der Bereichsrolle, um den Bereichszugriff für das Teammitglied zu ändern.
7. Klicken Sie auf **Bereiche schließen**.
8. Klicken Sie auf **Speichern** am Ende der Seite.

Bereichsmanager können Rollen für die Teammitglieder in ihren Bereichen auf der Seite **Organisation verwalten** bearbeiten.

1. Klicken Sie auf **Konto** &gt; **Organisationen verwalten**.
2. Suchen Sie die Organisation, in der sich Ihr Bereich befindet.
3. Klicken Sie auf **Details anzeigen**.
4. Suchen Sie Ihren Bereich und klicken Sie auf **Bereich bearbeiten**.
5. Wählen Sie die Registerkarte **Benutzer** aus.
6. Wählen Sie die Option für die Bereichsrolle aus oder löschen Sie die Auswahl für die Option der Bereichsrolle, die Sie für das Teammitglied hinzufügen oder entfernen möchten.
7. Anschließend klicken Sie auf **Speichern**.

## Teammitglieder entfernen
{: #removingteammembers}

Kontoeigner und Organisationsmanager können Teammitglieder über die Seite **Teamverzeichnis** aus einem Konto entfernen. Führen Sie die folgenden Schritte aus, um ein Teammitglied zu entfernen:

1. Klicken Sie auf **Konto** &gt; **Teamverzeichnis**.
3. Suchen Sie den Benutzer, der aus dem Konto entfernt werden soll, und klicken Sie auf das Symbol **Entfernen** ![Symbol 'Entfernen'](../icons/icon_remove_teamuser.svg).
4. Klicken Sie im Fenster **Benutzer entfernen** auf **Entfernen**, um die Entfernung des angegebenen Benutzers aus dem Konto zu bestätigen.

Der Benutzer wird aus der angezeigten Liste der Teammitglieder für dieses Konto entfernt.
