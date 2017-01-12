---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Toolchains unter {{site.data.keyword.Bluemix_notm}} Public verwenden
{: #toolchains-using}

Letzte Aktualisierung: 9. November 2016
{: .last-updated}

Mithilfe einer Toolchain können Sie Ihre täglichen Entwicklungs-, Bereitstellungs- und Systemaufgaben produktiv abwickeln. Nach dem Einrichten einer Toolchain können Sie Toolintegrationen hinzufügen, löschen oder konfigurieren sowie den Zugriff auf die Toolchain verwalten. Toolchains sind nur in den USA (Süden) verfügbar.
{: shortdesc}

## Toolintegration konfigurieren
{: #configuring_a_tool_integration}

Wenn Sie die Konfiguration einer Toolintegration beim Erstellen einer Toolchain noch nicht vorgenommen haben, wird eine Schaltfläche **Konfigurieren** auf der zugehörigen Kachel angezeigt. Wenn Sie beim Erstellen einer Toolchain eine Toolintegration konfiguriert haben, können Sie die Konfigurationseinstellungen aktualisieren.

1. Klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf eine Toolchain, um die zugehörige Übersichtsseite anzuzeigen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Übersicht** klicken.
1. Wenn Sie eine Toolintegration erstmalig konfigurieren müssen, klicken Sie auf der zugehörigen Kachel auf **Konfigurieren**.

  ![Schaltfläche 'Konfigurieren'](images/toolchain_tile_configure.png)

 Wenn Sie die Konfiguration der Toolintegration abgeschlossen haben, klicken Sie auf **Integration speichern**.
 
1. Wenn Sie die Konfiguration einer Toolintegration aktualisieren müssen, klicken Sie auf der zugehörigen Kachel auf das Menü für den Zugriff auf die Konfigurationsoptionen.

  ![Konfigurationsmenü](images/toolchain_tile_menu.png)
 
 Wenn Sie die Aktualisierung der Einstellungen abgeschlossen haben, klicken Sie auf **Integration speichern**.

## Toolintegration hinzufügen
{: #adding_a_tool_integration}

Sie können Toolintegrationen für Ihre Toolchain hinzufügen und konfigurieren.

1. Klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf eine Toolchain, um die zugehörige Übersichtsseite anzuzeigen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Übersicht** klicken.
1. Klicken Sie auf **Tool hinzufügen**, um eine Liste von hinzuzufügenden Toolintegrationen anzuzeigen.
1. Klicken Sie auf eine Toolintegration, die Sie hinzufügen möchten.
1. Geben Sie alle erforderlichen Informationen zum Konfigurieren der Toolintegration ein. 
1. Klicken Sie auf **Integration erstellen**, um die Toolintegration zu Ihrer Toolchain hinzuzufügen.

## Toolintegration löschen
{: #deleting_a_tool_integration}

Wenn Sie eine Toolintegration aus Ihrer Toolchain löschen, kann diese Löschung nicht mehr rückgängig gemacht werden. 

1. Klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf eine Toolchain, um die zugehörige Übersichtsseite anzuzeigen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Übersicht** klicken.
1. Klicken Sie auf der Kachel für die Toolintegration, die Sie löschen möchten, auf das Menü für den Zugriff auf die Konfigurationsoptionen.
1. Klicken Sie auf **Löschen**, um die Toolintegration aus Ihrer Toolchain zu löschen.
1. Bestätigen Sie dies, indem Sie nochmals auf **Löschen** klicken.  

## Zugriff verwalten
{: #managing_access}

Sie können Benutzern Zugriff auf eine Toolchain gewähren, indem Sie sie zu der Organisation hinzufügen, der die Toolchain zugeordnet ist. Jede Toolchain ist einer bestimmten Organisation zugeordnet und alle Benutzer, die Mitglied dieser Organisation sind, können auf die zugeordneten Toolchains zugreifen. Die Organisation, in der Sie gegenwärtig arbeiten, wird in der Menüleiste angezeigt. Klicken Sie auf die Organisation und wechseln Sie zu einer anderen Organisation, um auf andere Toolchains zugreifen zu können.

1. Klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die zu verwaltende Toolchain und klicken Sie dann auf **Verwalten**. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Verwalten** klicken.  
1. Klicken Sie auf den Link zu Ihrer Organisation. 
1. Klicken Sie auf der Seite 'Organisationen verwalten' auf **Benutzer einladen** und geben Sie die E-Mail-Adresse des Benutzers ein.
1. Wenn Sie erweiterte Berechtigungen zur Verwaltung von Benutzern in {{site.data.keyword.Bluemix_notm}}-Organisationen erteilen möchten, wählen Sie mindestens eines der folgenden Kontrollkästchen aus: **Manager**, **Abrechnungsmanager** und **Auditor**.
1. Klicken Sie auf **EINLADEN**.
1. Klicken Sie auf **SPEICHERN**.

## Toolchain löschen
{: #deleting_a_toolchain}

Sie können eine Toolchain löschen und angeben, welche der zugehörigen Toolintegrationen ebenfalls gelöscht werden sollen. Wenn Sie eine Toolchain löschen, kann diese Löschung nicht mehr rückgängig gemacht werden.

1. Klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die zu löschende Toolchain und klicken Sie dann auf **Verwalten**. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Verwalten** klicken.
1. Klicken Sie auf **Toolchain löschen** und überprüfen oder ändern Sie die zu löschenden Toolintegrationen.
1. Bestätigen Sie das Löschen, indem Sie den Namen der Toolchain eingeben und auf **Löschen** klicken.  

 **Tipp**: Wenn Sie eine GitHub-Toolintegration löschen, wird das zugeordnete GitHub-Repository nicht aus GitHub gelöscht. Sie müssen das Repository manuell aus GitHub entfernen.


# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}

* [Create and use your first toolchain (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Create a custom toolchain (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Create an application with three microservices (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [Create a toolchain from a template on {{site.data.keyword.Bluemix_notm}} Dedicated (Betaversion) (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Create a toolchain from an app on {{site.data.keyword.Bluemix_notm}} Dedicated (Betaversion) (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Zugehörige Links
{: #general}

* [Microservices toolchain (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method){:new_window}
