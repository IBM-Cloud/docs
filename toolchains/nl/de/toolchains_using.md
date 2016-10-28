---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Toolchains unter {{site.data.keyword.Bluemix_notm}} Public verwenden
{: #toolchains-using}

*Letzte Aktualisierung: 12. August 2016*
{: .last-updated}

Sie können eine Toolchain verwenden, die in Ihrer täglichen Entwicklung, Bereitstellung und Operation produktiv ist. Sie können nach der Einrichtung einer Toolchain Toolintegrationen hinzufügen, löschen oder konfigurieren sowie den Zugriff auf die Toolchain verwalten.
{: shortdesc}

**Wichtig**: Diese Funktion ist experimentell. Toolchains sind möglicherweise nicht stabil und können so geändert werden, dass sie nicht mehr mit früheren Versionen kompatibel sind. Sie sollten nicht in Produktionsumgebungen verwendet werden. Toolchains nur in der Region 'Vereinigte Staaten (Süden)' verfügbar.

## Toolintegrationen konfigurieren
{: #configuring_a_tool_integration}

Wenn Sie während der Erstellung einer Toolchain die Toolintegration noch nicht konfiguriert haben, wird neben ihrer Kachel die Schaltfläche **Konfigurieren** angezeigt. Wenn Sie während der Erstellung einer Toolchain die Toolintegration bereits konfiguriert haben, können Sie die Konfigurationseinstellungen aktualisieren.

1. Klicken Sie im DevOps-Dashboard in der Registerkarte **Toolchains** auf die Toolchain, um ihre dazugehörige Seite 'Toolintegrationen' anzuzeigen. Sie können als Alternative auf der Übersichtsseite der App in der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Toolintegrationen** klicken. 
1. Wenn Sie eine Toolintegration zum ersten Mal konfigurieren müssen, klicken Sie auf der entsprechenden Kachel auf **Konfigurieren**.

  ![Schaltfläche 'Konfigurieren'](images/toolchain_tile_configure.png)

 Wenn Sie das Konfigurieren der Toolintegration abgeschlossen haben, klicken Sie auf **Integration speichern**.
 
1. Wenn Sie die Konfiguration einer Toolintegration aktualisieren müssen, klicken Sie auf der entsprechenden Kachel auf das Menü, um die Konfigurationsoptionen aufzurufen.

  ![Konfigurationsmenü](images/toolchain_tile_menu.png)
 
 Wenn Sie das Aktualisieren der Einstellungen abgeschlossen haben, klicken Sie auf **Integration speichern**.

## Eine Toolintegration hinzufügen
{: #adding_a_tool_integration}

Sie können für Ihre Toolchain Toolintegrationen hinzufügen und konfigurieren.

1. Klicken Sie im DevOps-Dashboard in der Registerkarte **Toolchains** auf die Toolchain, um ihre dazugehörige Seite 'Toolintegrationen' anzuzeigen. Sie können als Alternative auf der Übersichtsseite der App in der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Toolintegrationen** klicken. 
1. Um eine Liste mit den hinzuzufügenden Toolintegrationen anzuzeigen, klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie auf eine Toolintegration, die Sie hinzufügen möchten.
1. Geben Sie alle erforderlichen Informationen ein, um die Toolintegration zu konfigurieren. 
1. Klicken Sie auf **Integration erstellen**, um Ihrer Toolchain die Toolintegration hinzuzufügen.

## Eine Toolintegration löschen
{: #deleting_a_tool_integration}

Wenn Sie aus Ihrer Toolchain eine Toolintegration löschen, kann dies nicht mehr rückgängig gemacht werden. 

1. Klicken Sie im DevOps-Dashboard in der Registerkarte **Toolchains** auf die Toolchain, um ihre dazugehörige Seite 'Toolintegrationen' anzuzeigen. Sie können als Alternative auf der Übersichtsseite der App in der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Toolintegrationen** klicken. 
1. Klicken Sie auf die Kachel für die entsprechende Toolintegration, die gelöscht werden soll, auf das Menü, um die Konfigurationsoptionen anzuzeigen.
1. Um aus Ihrer Toolchain eine Toolintegration zu löschen, klicken Sie auf **Löschen**.
1. Bestätigen Sie den Vorgang, indem Sie auf **Löschen** klicken.  

## Zugriff verwalten
{: #managing_access}

Sie können Benutzern Zugriff auf eine Toolchain gewähren, indem Sie sie der Organisation hinzufügen, der die Toolchain zugeordnet ist. Jede Toolchain ist einer bestimmten Organisation zugeordnet und jeder Benutzer, der Mitglied dieser Organisation ist, kann auf die zugeordneten Toolchains zugreifen. Klicken Sie in der Menüliste auf das **{{site.data.keyword.avatar}}**-Symbol ![Avatar-Symbol](../icons/i-avatar-icon.svg), um das Widget 'Konto und Unterstützung' zu öffnen und die Organisation zu öffnen, in der Sie arbeiten. Um auf einen anderen Toolchain-Satz zuzugreifen, wechseln Sie in eine andere Organisation.

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. Klicken Sie im DevOps-Dashboard in der Registerkarte **Toolchains** auf die Toolchain, die verwaltet werden soll, und dann auf **Verwalten**. Sie können als Alternative auf der Übersichtsseite der App in der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Verwalten** klicken.   
1. Klicken Sie auf den Link für Ihre Organisation. 
1. Klicken Sie auf der Seite 'Organisationen verwalten' auf **Benutzer einladen** und geben Sie die E-Mail-Adresse des Benutzers ein.
1. Wenn Sie erweiterte Berechtigungen zum Verwalten von Benutzern in {{site.data.keyword.Bluemix_notm}}-Organisationen gewähren möchten, aktivieren Sie die entsprechenden Kontrollkästchen **Manager**, **Abrechnungsmanager** oder **Auditor**.
1. Klicken Sie auf **Einladen**.
1. Klicken Sie auf **Speichern**. 

## Eine Toolchain löschen
{: #deleting_a_toolchain}

Sie können eine Toolchain löschen und angeben, welche ihrer zugeordneten Toolintegrationen gelöscht werden sollen. Das Löschen einer Toolchain kann nicht rückgängig gemacht werden.

1. Klicken Sie im DevOps-Dashboard in der Registerkarte **Toolchains** auf die Toolchain, die gelöscht werden soll, und dann auf **Verwalten**. Sie können als Alternative auf der Übersichtsseite der App in der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Verwalten** klicken. 
1. Klicken Sie auf **Toolchain löschen**. Überprüfen Sie die Toolintegrationen, die Sie löschen, oder passen Sie sie an.
1. Bestätigen Sie den Löschvorgang, indem Sie den Namen der Toolchain eingeben und auf **Löschen** klicken.  

 **Tipp**: Wenn Sie eine GitHub-Toolintegration löschen, wird das zugeordnete GitHub-Repository nicht aus GitHub Enterprise gelöscht. Das Repository muss manuell aus GitHub gelöscht werden.
