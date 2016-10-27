---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Toolchains unter {{site.data.keyword.Bluemix_notm}} Dedicated verwenden
{: #toolchains-using_dedicated}

Letzte Aktualisierung: 26. August 2016
{: .last-updated}

Sie können eine Toolchain verwenden, die in Ihrer täglichen Entwicklung, Bereitstellung und Operation produktiv ist. Sie können nach der Einrichtung einer Toolchain Toolintegrationen hinzufügen, löschen oder konfigurieren sowie den Zugriff auf die Toolchain verwalten.
{: shortdesc}

**Wichtig**: Diese Funktion ist experimentell. Toolchains sind möglicherweise nicht stabil und können so geändert werden, dass sie nicht mehr mit früheren Versionen kompatibel sind. Sie sollten nicht in Produktionsumgebungen verwendet werden.   

## Toolintegrationen konfigurieren
{: #configuring_a_tool_integration_dedicated}

Wenn Sie während der Erstellung einer Toolchain die Toolintegration noch nicht konfiguriert haben, wird neben ihrer Kachel die Schaltfläche **Konfigurieren** angezeigt. Wenn Sie während der Erstellung einer Toolchain die Toolintegration bereits konfiguriert haben, können Sie die Konfigurationseinstellungen aktualisieren.

1. Klicken Sie im Dashboard in der Registerkarte **DEVOPS** auf die Toolchain, um ihre dazugehörige Seite 'Toolintegrationen' anzuzeigen. Sie können als Alternative auf der Übersichtsseite Ihrer App rechts oben auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. 
1. Wenn Sie eine Toolintegration zum ersten Mal konfigurieren müssen, klicken Sie auf der entsprechenden Kachel auf **Konfigurieren**.

  ![Schaltfläche 'Konfigurieren'](images/toolchain_tile_configure.png)

 Wenn Sie das Konfigurieren der Toolintegration abgeschlossen haben, klicken Sie auf **Integration speichern**.
 
1. Wenn Sie die Konfiguration einer Toolintegration aktualisieren müssen, klicken Sie auf der entsprechenden Kachel auf das Menü, um die Konfigurationsoptionen aufzurufen.

  ![Konfigurationsmenü](images/toolchain_tile_menu.png)
 
 Wenn Sie das Aktualisieren der Einstellungen abgeschlossen haben, klicken Sie auf **Integration speichern**.

## Eine Toolintegration hinzufügen
{: #adding_a_tool_integration_dedicated}

Sie können für Ihre Toolchain Toolintegrationen hinzufügen und konfigurieren.

1. Klicken Sie im Dashboard in der Registerkarte **DEVOPS** auf die Toolchain, um ihre dazugehörige Seite 'Toolintegrationen' anzuzeigen. Sie können als Alternative auf der Übersichtsseite Ihrer App rechts oben auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. 
1. Um eine Liste mit den hinzuzufügenden Toolintegrationen anzuzeigen, klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie auf eine Toolintegration, um sie hinzuzufügen.
1. Geben Sie alle erforderlichen Informationen ein, um die Toolintegration zu konfigurieren. 
1. Klicken Sie auf **Integration erstellen**, um Ihrer Toolchain die Toolintegration hinzuzufügen.

## Eine Toolintegration löschen
{: #deleting_a_tool_integration}

Wenn Sie aus Ihrer Toolchain eine Toolintegration löschen, kann dies nicht mehr rückgängig gemacht werden. 

1. Klicken Sie im Dashboard in der Registerkarte **DEVOPS** auf die Toolchain, um ihre dazugehörige Seite 'Toolintegrationen' anzuzeigen. Sie können als Alternative auf der Übersichtsseite Ihrer App rechts oben auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. 
1. Klicken Sie auf die Kachel für die entsprechende Toolintegration, die gelöscht werden soll, auf das Menü, um die Konfigurationsoptionen anzuzeigen.
1. Um aus Ihrer Toolchain eine Toolintegration zu löschen, klicken Sie auf **Löschen**.
1. Bestätigen Sie den Vorgang, indem Sie auf **Löschen** klicken. 

## Zugriff verwalten
{: #managing_access_dedicated}

Sie können Benutzern Zugriff auf eine Toolchain gewähren, indem Sie sie der Organisation hinzufügen, der die Toolchain zugeordnet ist. Jede Toolchain ist einer bestimmten Organisation zugeordnet und jeder Benutzer, der Mitglied dieser Organisation ist, kann auf die zugeordneten Toolchains zugreifen. Um die Organisation anzuzeigen, in der Sie zurzeit arbeiten, klicken Sie in der Menüleiste auf das **{{site.data.keyword.avatar}}**-Symbol ![Avatar-Symbol ](../icons/i-avatar-icon.svg). Um auf einen anderen Toolchain-Satz zuzugreifen, wechseln Sie in eine andere Organisation.

Wenn Sie Benutzer zu Ihrer {{site.data.keyword.Bluemix}}-Organisation und zu Bereichen hinzufügen, können sich die Benutzer mit ihrer ID und ihrem Kennwort für {{site.data.keyword.Bluemix_notm}} bei GitHub Enterprise anmelden. Wenn sich die Benutzer anmelden, werden für sie Konten erstellt. Wenn Sie Benutzer zu Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation und zu Bereichen hinzufügen, werden die Benutzer nicht automatisch dem GitHub Enterprise-Repository hinzugefügt. Das Hinzufügen zum Repository kann nur eine Person mit Admin-Berechtigung durchführen. Weitere Informationen finden Sie im Abschnitt [Dedicated GitHub Enterprise verwenden](../services/ghededicated/index.html){: new_window}.

Führen Sie die folgenden Schritte durch, um einen Benutzer hinzuzufügen: 

1. Klicken Sie im Dashboard in der Registerkarte **DEVOPS** auf die Toolchain, um ihre dazugehörige Seite 'Toolintegrationen' anzuzeigen. Klicken Sie dann auf **Verwalten**. Sie können als Alternative auf der Übersichtsseite Ihrer App rechts oben auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Verwalten**.   
1. Klicken Sie auf den Link für Ihre Organisation. 
1. Klicken Sie auf der Seite 'Organisationen verwalten' auf **Benutzer einladen** und geben Sie die E-Mail-Adresse des Benutzers ein.
1. Wenn Sie erweiterte Berechtigungen zum Verwalten von Benutzern in {{site.data.keyword.Bluemix_notm}}-Organisationen gewähren möchten, aktivieren Sie die entsprechenden Kontrollkästchen **Manager**, **Abrechnungsmanager** oder **Auditor**.
1. Klicken Sie auf **Einladen**.
1. Klicken Sie auf **Speichern**. 

## Eine Toolchain löschen
{: #deleting_a_toolchain_dedicated}

Sie können eine Toolchain löschen und angeben, welche ihrer zugeordneten Toolintegrationen gelöscht werden sollen. Das Löschen einer Toolchain kann nicht rückgängig gemacht werden.

1. Klicken Sie im Dashboard in der Registerkarte **DEVOPS** auf die Toolchain, um ihre dazugehörige Seite 'Toolintegrationen' anzuzeigen. Klicken Sie dann auf **Verwalten**. Sie können als Alternative auf der Übersichtsseite Ihrer App rechts oben auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Verwalten**. 
1. Klicken Sie auf **Toolchain löschen**. Überprüfen Sie die Toolintegrationen, die Sie löschen, oder passen Sie sie an.
1. Bestätigen Sie den Löschvorgang, indem Sie den Namen der Toolchain eingeben und auf **Löschen** klicken.

 **Tipp**: Wenn Sie eine GitHub Enterprise-Toolintegration löschen, wird das zugeordnete GitHub Enterprise-Repository nicht aus GitHub Enterprise gelöscht. Das Repository muss manuell aus GitHub Enterprise gelöscht werden.
