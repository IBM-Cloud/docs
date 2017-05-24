---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-10"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Informationen zu angepassten Rollen
{: #custom_roles}

Neben den vordefinierten Rollen, die im Detail in der [Dokumentation zu Benutzer-, Anwendungs- und Gatewayrollen](roles_index.html) beschrieben werden, können Benutzer angepasste Rollen erstellen, die jeweils über eigene spezielle Berechtigungen verfügen. Anhand von Rollen haben Benutzer Zugriff auf bestimmte Operationen. Durch das Erstellen einer angepassten Rolle können Sie die Berechtigungen, die für vordefinierte Rollen verfügbar sind, beliebig kombinieren.
{:shortdesc}

Weitere Informationen zu den API-Operationen, die für Benutzerrollen verfügbar sind, finden Sie in der [Dokumentation zu Benutzer-, Anwendungs- und Gatewayrollen](roles_index.html).

## Angepasste Rolle erstellen
{: #custom-role-create}

Gehen Sie wie folgt vor, um eine angepasste Rolle zu erstellen:

1. Öffnen Sie im {{site.data.keyword.iot_short_notm}}-Dashboard in der Navigationsleiste das Teilfenster **Mitglieder**.
2. Wählen Sie die Registerkarte **Rollen** aus und klicken Sie auf **Neue Rolle**.
3. Geben Sie einen Namen für die angepasste Rolle ein.
4. Optional: Geben Sie eine Beschreibung für die angepasste Rolle ein.
5. Optional: Angepasste Rollen können eine vorhandene Rolle als Vorlage verwenden. Um eine vorhandene Benutzerrolle als Basis für die angepasste Rolle zu nehmen, wählen Sie die Rolle aus der Liste aus.
6. Klicken Sie auf **Weiter**.
7. Erweitern Sie in der Berechtigungsliste die Berechtigungskategorien und wählen Sie die Operationen aus, die im Rahmen der angepassten Rolle möglich sein sollen.
8. Klicken Sie auf **Rolle hinzufügen**.

Die angepasste Rolle wird in die Liste der verfügbaren Rollen aufgenommen.

## Angepasste Rolle bearbeiten oder löschen
{: #custom-role-edit}

Gehen Sie wie folgt vor, um eine angepasste Rolle zu bearbeiten oder zu löschen:

1. Öffnen Sie im {{site.data.keyword.iot_short_notm}}-Dashboard in der Navigationsleiste das Teilfenster **Mitglieder**.
2. Wählen Sie die Registerkarte **Rollen** aus.
3. Suchen Sie nach der Spalte, die der angepassten Rolle entspricht, die bearbeitet werden soll.
3. Klicken Sie für den Namen der angepassten Rolle auf das Bearbeitungssymbol.
4. Nehmen Sie alle erforderlichen Änderungen an der Rollenbeschreibung und den Berechtigungen vor.
5. Um die Rolle zu löschen, blättern Sie an das Ende der Liste mit den Berechtigungskategorien und klicken Sie auf **Rolle löschen**.
5. Wenn Sie Änderungen vorgenommen haben, klicken Sie auf **Speichern**, um die Rolle zu aktualisieren.

Die Rolle wird aktualisiert.
