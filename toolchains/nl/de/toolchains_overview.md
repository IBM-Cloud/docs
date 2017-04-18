---

Copyright:
  Jahre: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Erste Schritte mit Toolchains (Beta) 
{: #toolchains_getting_started}

Letzte Aktualisierung: 7. Oktober 2016
{: .last-updated}  

Toolchains stehen in öffentlichen und dedizierten {{site.data.keyword.Bluemix}}-Umgebungen (Public bzw. Dedicated) zur Verfügung. Sie können eine Toolchain auf zwei Arten erstellen: Entweder Sie verwenden eine Vorlage zum Erstellen einer Toolchain oder Sie erstellen eine Toolchain aus einer App. Unter {{site.data.keyword.Bluemix_notm}} Public sind Toolchains nur in den USA (Süden) verfügbar.
{: shortdesc}

##Erste Schritte mit Toolchains: Public 
{: #getting_started_public}

**Anmerkung:** Vergewissern Sie sich, dass Sie in der neuen Bluemix-Version arbeiten. Dies erkennen Sie am oberen Banner.

 * Falls eine Nachricht ausgegeben wird, die Ihnen die Verwendung der neuen Bluemix-Version anbietet, arbeiten Sie mit dem klassischen Zugang von Bluemix. Klicken Sie auf den Link, um die neue Bluemix-Version zu öffnen.
 * Wenn keine entsprechende Nachricht angezeigt wird, arbeiten Sie bereits mit der neuen Bluemix-Version.

Jede Toolchain ist einer bestimmten Organisation zugeordnet und alle Benutzer, die Mitglied dieser Organisation sind, können auf die ihr zugeordneten Toolchains zugreifen. Bevor Sie eine Toolchain erstellen, müssen Sie sicherstellen, dass Sie in der Organisation arbeiten, in der Sie die Toolchain erstellen wollen. Die Organisation, in der Sie gegenwärtig arbeiten, wird in der Menüleiste angezeigt. Um zu einer anderen Organisation zu wechseln, klicken Sie in der Menüleiste auf die Organisation und wählen Sie anschließend die Organisation aus, zu der Sie wechseln möchten.

###Toolchain aus einer Vorlage erstellen   
{: #creating_a_toolchain_from_a_template}

Sie können eine Vorlage als Ausgangspunkt zum Erstellen einer Toolchain verwenden, die eine bestimmte Gruppe von Toolintegrationen enthält.

1. Wenn Sie Ihre erste Toolchain erstellen, müssen Sie sicherstellen, dass Toolchains in Ihrer Organisation aktiviert sind:
   1. Öffnen Sie das DevOps-Dashboard und klicken Sie auf die Seite **Toolchains**.
   2. Wenn die Schaltfläche **Toolchains aktivieren** angezeigt wird, klicken Sie sie an und folgen Sie den angezeigten Anweisungen, um Ihre Toolchain zu erstellen.
   3. Wenn die Schaltfläche **Toolchains aktivieren** nicht angezeigt wird, sind die Toolchains bereits aktiviert. Setzen Sie den Vorgang mit Schritt 2 fort.
1. Klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Schaltfläche zum Hinzufügen (+), um eine Toolchain zu erstellen.
1. Klicken Sie auf eine Toolchain-Vorlage. Klicken Sie beispielsweise auf **Microservices-Toolchain**, um ein Onlinegeschäftsmuster zum Erstellen der Toolchain zu verwenden. 
1. Überprüfen Sie auf der Seite zum Erstellen der Toolchain das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in ihrer aktuellen Lebenszyklusphase in der Toolchain angezeigt. Das Diagramm in der folgenden Abbildung ist ein Beispiel. Wenn Sie eine Toolchain erstellen, zeigt das Diagramm jede Toolintegration an, die Teil der Toolchain ist.
![Diagramm einer Toolchain](images/toolchain_diagram.png)

1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. Wenn es bereits eine Toolchain mit diesem Namen gibt oder wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain.  
1. Wählen Sie im Abschnitt mit den konfigurierbaren Integrationen jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Bestimmte Toolintegrationen erfordern keine Konfiguration. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren (Link wird in neuem Fenster geöffnet)](../toolchains/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**.  Es werden verschiedene Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten:

 * Die Toolchain wird erstellt.
 * Falls Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines aktiviert.
 * Falls Sie die Sauce Labs-Toolintegration konfiguriert haben, wird die Sauce Labs-Integration konfiguriert, um Jobs zu Pipelines hinzuzufügen und Tests auszuführen.
 * Falls Sie die PagerDuty-Toolintegration konfiguriert haben, wird die PagerDuty-Integration konfiguriert, um Benachrichtigungen an den in Slack konfigurierten Kanal zu senden. Diese Benachrichtigungen weisen auf Probleme hin.
 * Falls Sie die Slack-Toolintegration konfiguriert haben, wird die Slack-Integration konfiguriert, um Benachrichtigungen an den in Slack konfigurierten Kanal zu senden. Diese Benachrichtigungen geben den Entwicklungsfortschritt an, z. B. `Verbunden mit Projekt XYZ`, `Pipeline konfiguriert` und `Stage 'Build' gestartet`.
 * Falls Sie die GitHub-Toolintegration konfiguriert haben, wird das GitHub-Beispielrepository in Ihr GitHub-Konto geklont.


###Toolchain aus einer App erstellen
{: #creating_a_toolchain_from_an_app}

Sie können eine Toolchain aus Ihrer App erstellen. Die Toolchain kann kontinuierliche Entwicklung, Bereitstellung, Überwachung und mehr unterstützen und sie ist Ihrer App zugeordnet. Jede App kann einer Toolchain zugeordnet sein. Wenn Sie Änderungen per Push-Operation an das GitHub-Repository der Toolchain übertragen, erstellt die Pipeline automatisch Builds und stellt die App bereit.  

1. Wenn Sie Ihre erste Toolchain erstellen, müssen Sie sicherstellen, dass Toolchains in Ihrer Organisation aktiviert sind:
   1. Öffnen Sie das DevOps-Dashboard und klicken Sie auf die Seite **Toolchains**.
   2. Wenn die Schaltfläche **Toolchains aktivieren** angezeigt wird, klicken Sie sie an und folgen Sie den angezeigten Anweisungen, um Ihre Toolchain zu erstellen.
   3. Wenn die Schaltfläche **Toolchains aktivieren** nicht angezeigt wird, sind die Toolchains bereits aktiviert. Setzen Sie den Vorgang mit Schritt 2 fort.
1. Klicken Sie auf der Übersichtsseite Ihrer App auf der Kachel 'Continuous Delivery' auf **Aktivieren**. Alternativ können Sie beim klassischen Zugang von {{site.data.keyword.Bluemix_notm}} in der rechten oberen Ecke auf der Übersichtsseite der App auf **Toolchain hinzufügen** klicken. Ihre App wird für eine kontinuierliche Bereitstellung aus einem neuen GitHub-Repository konfiguriert, in dem der App-Starter-Code angegeben wird.
1. Überprüfen Sie auf der Seite zum Erstellen der Toolchain das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in ihrer aktuellen Lebenszyklusphase in der Toolchain angezeigt.
1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. Wenn es bereits eine Toolchain mit diesem Namen gibt oder wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain.
1. Wählen Sie im Abschnitt mit den konfigurierbaren Integrationen jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Bestimmte Toolintegrationen erfordern keine Konfiguration. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren (Link wird in neuem Fenster geöffnet)](../toolchains/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**.  Es werden verschiedene Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten:

 * Die Toolchain wird erstellt.
 * Falls Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines aktiviert.
 * Falls Sie die Sauce Labs-Toolintegration konfiguriert haben, wird die Sauce Labs-Integration konfiguriert, um Jobs zu Pipelines hinzuzufügen und Tests auszuführen.
 * Falls Sie die PagerDuty-Toolintegration konfiguriert haben, wird die PagerDuty-Integration konfiguriert, um Benachrichtigungen an den in Slack konfigurierten Kanal zu senden. Diese Benachrichtigungen weisen auf Probleme hin.
 * Falls Sie die Slack-Toolintegration konfiguriert haben, wird die Slack-Integration konfiguriert, um Benachrichtigungen an den in Slack konfigurierten Kanal zu senden. Diese Benachrichtigungen geben den Entwicklungsfortschritt an, z. B. `Verbunden mit Projekt XYZ`, `Pipeline konfiguriert` und `Stage 'Build' gestartet`.
 * Falls Sie die GitHub-Toolintegration konfiguriert haben, wird das GitHub-Beispielrepository in Ihr GitHub-Konto geklont.


##Erste Schritte mit Toolchains: Dedicated
{: #getting_started_dedicated}

Jede Toolchain ist einer bestimmten Organisation zugeordnet und alle Benutzer, die Mitglied dieser Organisation sind, können auf die ihr zugeordneten Toolchains zugreifen. Klicken Sie vor dem Erstellen einer Toolchain auf das Symbol **{{site.data.keyword.avatar}}** ![Avatar-Symbol](../icons/i-avatar-icon.svg) in der Menüleiste, um das Widget 'Konto und Unterstützung' zu öffnen und um die Organisation anzuzeigen, in der Sie arbeiten. Wenn es sich dabei nicht um die Organisation handelt, in der Sie die Toolchain erstellen wollen, müssen Sie zu einer anderen Organisation wechseln.

###Toolchain aus einer Vorlage erstellen   
{: #creating_a_toolchain_from_a_template_dedicated}

Sie können eine Vorlage als Ausgangspunkt zum Erstellen einer Toolchain verwenden, die eine bestimmte Gruppe von Toolintegrationen enthält.

1. Wenn Sie Ihre erste Toolchain erstellen, müssen Sie sicherstellen, dass Toolchains in Ihrer Organisation aktiviert sind:
   1. Öffnen Sie das DevOps-Dashboard und klicken Sie auf die Registerkarte **Toolchains**.
   2. Wenn die Schaltfläche **Toolchains aktivieren** angezeigt wird, klicken Sie sie an und folgen Sie den angezeigten Anweisungen, um Ihre Toolchain zu erstellen.
   3. Wenn die Schaltfläche **Toolchains aktivieren** nicht angezeigt wird, sind die Toolchains bereits aktiviert. Setzen Sie den Vorgang mit Schritt 2 fort.
1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf der Registerkarte **DEVOPS** auf die Schaltfläche zum Hinzufügen (+), um eine Toolchain zu erstellen.
1. Klicken Sie auf eine Toolchain-Vorlage. Um beispielsweise eine einfache Toolchain zu erstellen, um eine neue Cloud Foundry-App bereitzustellen, klicken Sie auf **Einfache Cloud Foundry-Toolchain**. 
1. Überprüfen Sie auf der Seite zum Erstellen der Toolchain das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in ihrer aktuellen Lebenszyklusphase in der Toolchain angezeigt. Das Diagramm in der folgenden Abbildung ist ein Beispiel. Wenn Sie eine Toolchain erstellen, zeigt das Diagramm jede Toolintegration an, die Teil der Toolchain ist.
![Dedicated-Toolchain-Diagramm](images/toolchain_dedicated_diagram.png)

1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. Wenn es bereits eine Toolchain mit diesem Namen gibt oder wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain.  
1. Wählen Sie im Abschnitt mit den konfigurierbaren Integrationen jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Bestimmte Toolintegrationen erfordern keine Konfiguration. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren (Link wird in neuem Fenster geöffnet)](../toolchains/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**.  Es werden verschiedene Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten:

 * Die Toolchain wird erstellt.
 * Falls Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines aktiviert.
 * Falls Sie die GitHub Enterprise-Toolintegration konfiguriert haben, wird das GitHub Enterprise-Beispielrepository in Ihr GitHub Enterprise-Konto geklont.


###Toolchain aus einer App erstellen
{: #creating_a_toolchain_from_an_app_dedicated}

Sie können eine Toolchain aus Ihrer App erstellen. Die Toolchain kann kontinuierliche Entwicklung, Bereitstellung, Überwachung und mehr unterstützen und sie ist Ihrer App zugeordnet. Jede App kann einer Toolchain zugeordnet sein. Wenn Sie Änderungen per Push-Operation an das GitHub Enterprise-Repository der Toolchain übertragen, erstellt die Pipeline automatisch Builds und stellt die App bereit.  

1. Wenn Sie Ihre erste Toolchain erstellen, müssen Sie sicherstellen, dass Toolchains in Ihrer Organisation aktiviert sind:
   1. Öffnen Sie das DevOps-Dashboard und klicken Sie auf die Registerkarte **Toolchains**.
   2. Wenn die Schaltfläche **Toolchains aktivieren** angezeigt wird, klicken Sie sie an und folgen Sie den angezeigten Anweisungen, um Ihre Toolchain zu erstellen.
   3. Wenn die Schaltfläche **Toolchains aktivieren** nicht angezeigt wird, sind die Toolchains bereits aktiviert. Setzen Sie den Vorgang mit Schritt 2 fort.
1. Klicken Sie in der rechten oberen Ecke auf der Übersichtsseite der App auf **Toolchain hinzufügen**. Ihre App wird für eine kontinuierliche Bereitstellung aus einem neuen GitHub Enterprise-Repository konfiguriert, in dem der App-Starter-Code angegeben wird.
1. Überprüfen Sie auf der Seite zum Erstellen der Toolchain das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in ihrer aktuellen Lebenszyklusphase in der Toolchain angezeigt.
1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. Wenn es bereits eine Toolchain mit diesem Namen gibt oder wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain.
1. Wählen Sie im Abschnitt mit den konfigurierbaren Integrationen jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Bestimmte Toolintegrationen erfordern keine Konfiguration. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren (Link wird in neuem Fenster geöffnet)](../toolchains/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**.  Es werden verschiedene Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten:

 * Die Toolchain wird erstellt.
 * Falls Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines aktiviert.
 * Falls Sie die GitHub Enterprise-Toolintegration konfiguriert haben, wird das GitHub Enterprise-Beispielrepository in Ihr GitHub Enterprise-Konto geklont.


##Toolchain anzeigen
{: #viewing_a_toolchain}

Nachdem Sie die Toolchain und die zugehörigen Toolintegrationen konfiguriert haben, können Sie eine grafische Darstellung der Toolchain auf der Seite mit den Toolintegrationen anzeigen.

* Klicken Sie bei Verwendung von {{site.data.keyword.Bluemix_notm}} Public im DevOps-Dashboard auf der Seite **Toolchains** auf eine Toolchain, um die zugehörige Seite mit den Toolintegrationen anzuzeigen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. 
   
* Wenn Sie {{site.data.keyword.Bluemix_notm}} Dedicated verwenden, klicken Sie im Dashboard auf der Registerkarte **DEVOPS** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie in der rechten oberen Ecke auf der Übersichtsseite der App auf **Toolchain anzeigen** klicken.

* Um auf eine Toolintegration in Ihrer Toolchain zuzugreifen, klicken Sie auf die Kachel des entsprechenden Tools. 
 
 **Tipp**: Wenn Sie über mehr als ein GitHub Enterprise-Repository verfügen, kann es für dieselbe Toolintegration mehrere Kacheln geben, da jedes Repository durch eine eigene Kachel dargestellt wird.


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}

* [Create an application with three microservices (Beta) (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}
* [Create a toolchain from a template on {{site.data.keyword.Bluemix_notm}} Dedicated (Betaversion) (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Create a toolchain from an app on {{site.data.keyword.Bluemix_notm}} Dedicated (Betaversion) (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Zugehörige Links
{: #general}

* [Microservices toolchain (Beta) (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain (Beta) (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method){:new_window}
