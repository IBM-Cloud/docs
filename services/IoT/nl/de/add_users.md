---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Benutzerzugriff verwalten

Über das Zugriffsdashboard können Sie den Zugriff auf Ihre {{site.data.keyword.iot_full}}-Organisation steuern und verwalten. Sie können Benutzer hinzufügen, indem Sie sie hinzufügen, einladen, registrieren oder importieren. Durch die Zuweisung von Rollen können Sie Ihren Benutzern unterschiedliche Zugriffsebenen zuordnen.
{:shortdesc}

- [Neue Benutzer hinzufügen](#adding-new-users)
- [Benutzer bearbeiten](#editing-users)
- [Benutzerzugriff sperren](#blocking-users)
- [Benutzer entfernen](#removing-users)

## Neue Benutzer hinzufügen
{: #adding-new-users}

Über die Registerkarte **Zugriff** im Dashboard können Sie einzelne Mitglieder mithilfe der Funktionen zum Hinzufügen, Einladen oder Registrieren hinzufügen. Sie können auch mithilfe der Importfunktion mehrere Mitglieder gleichzeitig hinzufügen, einladen oder registrieren.

Mitgliederkonten haben standardmäßig kein Ablaufdatum. Wenn Sie Ihrer {{site.data.keyword.iot_short_notm}}-Organisation Mitglieder hinzufügen, können Sie für deren Konto optional ein Ablaufdatum festlegen.

### Mitglieder zur {{site.data.keyword.iot_short_notm}}-Organisation hinzufügen

Zum Hinzufügen von Mitgliedern zu Ihrer Organisation benötigen Sie die IBM ID des Mitglieds. Eine Bestätigung des Mitglieds benötigen Sie zum Hinzufügen des Mitglieds nicht.

Gehen Sie wie folgt vor, um Ihrer {{site.data.keyword.iot_short_notm}}-Organisation ein einzelnes Mitglied hinzuzufügen:
1. Wechseln Sie im {{site.data.keyword.iot_short_notm}}-Dashboard zu **Zugriff**.
2. Klicken Sie auf **Mitglied hinzufügen** und wählen Sie **Hinzufügen** aus.
3. Geben Sie die IBM ID des Mitglieds ein.
4. Wählen Sie eine Rolle für das Mitglied aus.
5. Optional: Legen Sie ein Ablaufdatum für das Mitglied fest.
6. Klicken Sie auf **Mitglied hinzufügen**.

Zum gleichzeitigen Hinzufügen mehrerer Mitglieder müssen Sie eine CSV-Datei (`.csv`) hochladen, die für jedes Mitglied die IBM ID, die Rolle und das optionale Ablaufdatum enthält.
1. Wechseln Sie im {{site.data.keyword.iot_short_notm}}-Dashboard zu **Zugriff**.
2. Klicken Sie auf **Mitglied hinzufügen** und wählen Sie **Importieren** aus.
3. Klicken Sie auf **Hinzufügen per Massenoperation**.
4. Wählen Sie eine Standardrolle aus und stellen Sie sicher, dass die Spaltennummern in Ihrer CSV-Datei (`.csv`) mit den Spaltennummern in den CSV-Einstellungen übereinstimmen.
5. Stellen Sie sicher, dass das Spaltentrennzeichen in Ihrer CSV-Datei (`.csv`) mit dem Spaltentrennzeichen in den CSV-Einstellungen übereinstimmt.
6. Klicken Sie auf die Option zum Durchsuchen oder ziehen Sie die CSV-Datei (`.csv`) in das Fenster **CSV-Upload**.

### Mitglieder in die {{site.data.keyword.iot_short_notm}}-Organisation einladen

Wenn Sie einen Benutzer einladen, Mitglied Ihrer {{site.data.keyword.iot_short_notm}}-Organisation zu werden, empfängt der Benutzer eine E-Mail, die einen Einladungslink enthält. Einladungslinks laufen 48 Stunden nach dem Versenden ab. Wenn ein Einladungslink nicht innerhalb von 48 Stunden verwendet wird, muss der Benutzer erneut eingeladen werden, damit er einen neuen Einladungslink erhält.

Gehen Sie wie folgt vor, um ein Mitglied in Ihre {{site.data.keyword.iot_short_notm}}-Organisation einzuladen:
1. Wechseln Sie im {{site.data.keyword.iot_short_notm}}-Dashboard zu **Zugriff**.
2. Klicken Sie auf **Mitglied hinzufügen** und wählen Sie **Einladen** aus.
3. Geben Sie die E-Mail-Adresse des Mitglieds ein.
4. Wählen Sie eine Rolle für dieses Mitglied aus.
5. Optional: Legen Sie ein Ablaufdatum für das Mitglied fest.
6. Klicken Sie auf **Mitglied einladen**.

Zum gleichzeitigen Einladen mehrerer Mitglieder müssen Sie eine CSV-Datei (`.csv`) hochladen, die für jedes Mitglied die E-Mail-Adresse, die Rolle und das optionale Ablaufdatum enthält.
1. Wechseln Sie im {{site.data.keyword.iot_short_notm}}-Dashboard zu **Zugriff**.
2. Klicken Sie auf **Mitglied hinzufügen** und wählen Sie **Importieren** aus.
3. Klicken Sie auf **Einladen per Massenoperation**.
4. Wählen Sie eine Standardrolle aus und stellen Sie sicher, dass die Spaltennummern in Ihrer CSV-Datei (`.csv`) mit den Spaltennummern in den CSV-Einstellungen übereinstimmen.
5. Stellen Sie sicher, dass das Spaltentrennzeichen in Ihrer CSV-Datei (`.csv`) mit dem Spaltentrennzeichen in den CSV-Einstellungen übereinstimmt.
6. Klicken Sie auf die Option zum Durchsuchen oder ziehen Sie die CSV-Datei (`.csv`) in das Fenster **CSV-Upload**.

### Mitglied in der {{site.data.keyword.iot_short_notm}}-Organisation registrieren

Wenn in Ihrer Organisation {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}} nicht verwendet wird, können Sie Ihrer Organisation einzelne Mitglieder hinzufügen, indem Sie sie registrieren (hierfür ist keine IBM ID erforderlich).

Gehen Sie wie folgt vor, um ein Mitglied in Ihrer {{site.data.keyword.iot_short_notm}}-Organisation zu registrieren:
1. Wechseln Sie im {{site.data.keyword.iot_short_notm}}-Dashboard zu **Zugriff**.
2. Klicken Sie auf **Mitglied hinzufügen** und wählen Sie **Einladen** aus.
3. Geben Sie die E-Mail-Adresse des Mitglieds ein.
4. Wählen Sie eine Rolle für dieses Mitglied aus.
5. Geben Sie den Betreff, den Realmnamen und den Aussteller ein.
   **Wichtig:** Stellen Sie sicher, dass die Felder für den Betreff (`Subject`), den Realmnamen (`Realm Name`) und den Aussteller (`Issuer`) die Empfehlungen und Standards von OpenID Connect einhalten. Weitere Informationen finden Sie auf der Website von [OpenID Connect ![Symbol für externen Link](../../icons/launch-glyph.svg)](http://openid.net/connect/){: new_window}.
6. Optional: Legen Sie ein Ablaufdatum für das Mitglied fest.
7. Klicken Sie auf **Benutzer registrieren**.

Zum gleichzeitigen Registrieren mehrerer Mitglieder müssen Sie eine CSV-Datei (`.csv`) hochladen, die für jedes Mitglied die E-Mail-Adresse, die Rolle, den Betreff, den Realmnamen, den Aussteller und das optionale Ablaufdatum enthält.
1. Wechseln Sie im {{site.data.keyword.iot_short_notm}}-Dashboard zu **Zugriff**.
2. Klicken Sie auf **Mitglied hinzufügen** und wählen Sie **Importieren** aus.
3. Klicken Sie auf **Registrierung per Massenoperation**.
4. Wählen Sie eine Standardrolle aus und stellen Sie sicher, dass die Spaltennummern in Ihrer CSV-Datei mit den Spaltennummern in den CSV-Einstellungen übereinstimmen.
5. Stellen Sie sicher, dass das Spaltentrennzeichen in Ihrer CSV-Datei mit dem Spaltentrennzeichen in den CSV-Einstellungen übereinstimmt.
6. Klicken Sie auf die Option zum Durchsuchen oder ziehen Sie die CSV-Datei in das Fenster **CSV-Upload**.

### CSV-Datei erstellen

Beim Erstellen einer CSV-Datei für den Import von Mitgliedern in Ihre Organisation müssen Sie sicherstellen, dass Sie für die von Ihnen verwendete Methode die erforderlichen Informationen einschließen. Verwenden Sie zum Trennen von Spalten entweder Kommas oder Semikola. Stellen Sie beim Hochladen der CSV-Datei sicher, dass Sie unter **CSV-Einstellungen** das richtige Spaltentrennzeichen auswählen.

## Benutzer bearbeiten
{: #editing-users}

Beim Bearbeiten eines Benutzer können Sie die Benutzerrolle ändern, ein Ablaufdatum hinzufügen, entfernen oder ändern sowie Zugriff auf eine Organisation hinzufügen oder entfernen.

1. Klicken Sie in Ihrem {{site.data.keyword.iot_short_notm}}-Dashboard links in der Navigationsleiste auf **Mitglieder**.
2. Klicken Sie auf das Bearbeitungssymbol **** ![Bearbeiten](/docs/images/edit_32.svg) neben dem Benutzer, den Sie bearbeiten möchten.
3. Nehmen Sie die gewünschten Änderungen für den Benutzer vor.
4. Klicken Sie auf **Speichern**.

## Benutzerzugriff sperren
{: #blocking-users}

Sie können den Zugriff von Benutzern auf die {{site.data.keyword.iot_short_notm}}-Organisation sperren, ohne die Zugehörigkeit zu der Organisation zu ändern.

1. Klicken Sie in Ihrem {{site.data.keyword.iot_short_notm}}-Dashboard links in der Navigationsleiste auf **Mitglieder**.
2. Klicken Sie auf den Schalter neben dem Benutzer, für den der Zugriff auf die {{site.data.keyword.iot_short_notm}}-Organisation gesperrt werden soll.


## Benutzer entfernen
{: #removing-users}

Sie können Benutzer vollständig aus der {{site.data.keyword.iot_short_notm}}-Organisation entfernen. Das Entfernen von Benutzern kann nicht rückgängig gemacht werden, d. h. die betreffenden Benutzer müssen erneut [zur Plattform hinzugefügt werden](#adding-new-users), um den Zugriff wiederherzustellen.

1. Klicken Sie in Ihrem {{site.data.keyword.iot_short_notm}}-Dashboard links in der Navigationsleiste auf **Mitglieder**.
2. Klicken Sie auf das Löschsymbol**** ![Löschen](/docs/images/trash_32.svg) neben dem Benutzer, den Sie entfernen möchten.
3. Klicken Sie im Bestätigungsdialog auf **Löschen**.
