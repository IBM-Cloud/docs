---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Toolchains verwenden
{: #toolchains-using}

*Letzte Aktualisierung: 4. Mai 2016*
{: .last-updated}

Mithilfe einer Toolchain können Sie Ihre täglichen Entwicklungs-, Bereitstellungs- und Systemaufgaben produktiv abwickeln. Nach dem Einrichten einer Toolchain können Sie Toolintegrationen hinzufügen, löschen oder konfigurieren sowie den Zugriff auf die Toolchain verwalten.
{: shortdesc}

**Wichtig**: Diese Funktion ist experimentell. Toolchains sind unter Umständen nicht stabil und können sich auf eine Weise ändern, die nicht mit früheren Versionen kompatibel ist. Es wird empfohlen, sie nicht in Produktionsumgebungen einzusetzen. Wenn Sie Toolchains verwenden möchten, müssen Sie eine einmalige [Zugriffsanforderung](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window} stellen. Toolchains sind nur in USA (Süden) verfügbar. 

## Toolintegration konfigurieren
{: #configuring_a_tool_integration}

Sie können eine Toolintegration erstmalig konfigurieren oder die Konfigurationseinstellungen für eine Toolintegration aktualisieren, die bereits Teil Ihrer Toolchain ist. 

1. Klicken Sie im DevOps-Dashboard auf der Registerkarte **Toolchains** auf eine Toolchain, um die zugehörige Seite mit den Toolintegrationen anzuzeigen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Toolintegrationen** klicken. 
1. Wenn Sie eine Toolintegration erstmalig konfigurieren müssen, klicken Sie auf der zugehörigen Kachel auf **Konfigurieren**. 

  ![Schaltfläche 'Konfigurieren'](images/toolchain_tile_configure.png)

 Wenn Sie die Konfiguration der Toolintegration abgeschlossen haben, klicken Sie auf **Integration speichern**. 
 
1. Wenn Sie die Konfiguration einer Toolintegration aktualisieren müssen, klicken Sie auf der zugehörigen Kachel auf das Menü für den Zugriff auf die Konfigurationsoptionen. 

  ![Konfigurationsmenü](images/toolchain_tile_menu.png)
 
 Wenn Sie die Aktualisierung der Einstellungen abgeschlossen haben, klicken Sie auf **Integration speichern**. 

 **Hinweis**: Nachdem Sie das Repository für eine GitHub-Toolintegration konfiguriert haben, kann zwar die URL des Repositorys aktualisiert werden, aber das Repository selbst kann nicht geändert werden. Um ein anderes Repository zu verwenden, löschen Sie die aktuelle GitHub-Toolintegration aus Ihrer Toolchain, fügen Sie eine GitHub-Toolintegration zu Ihrer Toolchain hinzu und konfigurieren Sie diese Toolintegration für die Verwendung des neuen Repositorys. 

## Toolintegration hinzufügen
{: #adding_a_tool_integration}

Sie können Toolintegrationen für Ihre Toolchain hinzufügen und konfigurieren. 

1. Klicken Sie im DevOps-Dashboard auf der Registerkarte **Toolchains** auf eine Toolchain, um die zugehörige Seite mit den Toolintegrationen anzuzeigen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Toolintegrationen** klicken. 
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+), um eine Liste von hinzuzufügenden Toolintegrationen anzuzeigen. 
1. Klicken Sie auf eine Toolintegration, die Sie hinzufügen möchten. 
1. Geben Sie alle erforderlichen Informationen zum Konfigurieren der Toolintegration ein.  
1. Klicken Sie auf **Integration erstellen**, um die Toolintegration zu Ihrer Toolchain hinzuzufügen. 

## Toolintegration löschen
{: #deleting_a_tool_integration}

Sie können eine Toolintegration aus Ihrer Toolchain löschen.  

1. Klicken Sie im DevOps-Dashboard auf der Registerkarte **Toolchains** auf eine Toolchain, um die zugehörige Seite mit den Toolintegrationen anzuzeigen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Toolintegrationen** klicken. 
1. Klicken Sie auf der Kachel für die Toolintegration, die Sie löschen möchten, auf das Menü für den Zugriff auf die Konfigurationsoptionen. 
1. Klicken Sie auf **Löschen**, um die Toolintegration aus Ihrer Toolchain zu löschen. 
1. Bestätigen Sie, indem Sie erneut auf **Löschen** klicken. 

## Zugriff verwalten
{: #managing_access}

Sie können Benutzern Zugriff auf eine Toolchain gewähren, indem Sie sie zu der Organisation hinzufügen, der die Toolchain zugeordnet ist. Jede Toolchain ist einer bestimmten Organisation zugeordnet und alle Benutzer, die Mitglied dieser Organisation sind, können auf die zugeordneten Toolchains zugreifen. Wenn Sie zu einer anderen Organisation wechseln, können Sie auf eine andere Gruppe von Toolchains zugreifen. 

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. Klicken Sie im DevOps-Dashboard auf der Registerkarte **Toolchains** auf die zu verwaltende Toolchain und klicken Sie dann auf **Verwalten**. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Verwalten** klicken.   
1. Klicken Sie auf den Link zu Ihrer Organisation.  
1. Klicken Sie auf der Seite 'Organisationen verwalten' auf **Benutzer einladen** und geben Sie die E-Mail-Adresse des Benutzers ein. 
1. Wenn Sie dem Benutzer erweiterte Berechtigungen erteilen möchten, wählen Sie mindestens eines der folgenden Kontrollkästchen aus: **Manager**, **Abrechnungsmanager** und **Auditor**. 
1. Klicken Sie auf **EINLADEN**.
1. Klicken Sie auf **SPEICHERN**. 

## Toolchain löschen
{: #deleting_a_toolchain}

Sie können eine Toolchain löschen und angeben, welche der zugehörigen Toolintegrationen ebenfalls gelöscht werden sollen. 

1. Klicken Sie im DevOps-Dashboard auf der Registerkarte **Toolchains** auf die zu löschende Toolchain und klicken Sie dann auf **Verwalten**. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Verwalten** klicken. 
1. Klicken Sie auf **Toolchain löschen** und überprüfen Sie, welche Toolintegrationen Sie löschen. 
1. Bestätigen Sie das Löschen, indem Sie den Namen der Toolchain eingeben und auf **Löschen** klicken. 

 **Tipp**: Wenn Sie eine GitHub-Toolintegration löschen, wird das zugeordnete GitHub-Repository nicht aus GitHub gelöscht. Sie müssen das Repository manuell aus GitHub entfernen. 
