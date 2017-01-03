---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Mit Toolchains arbeiten
{: #toolchains_getting_started}

Letzte Aktualisierung: 17. November 2016
{: .last-updated}  

Eine *Toolchain* ist eine Gruppe von Toolintegrationen, die Entwicklungs-, Bereitstellungs- und Systemtasks unterstützen. Die kollektive Leistung einer Toolchain ist höher als die Summe der zugehörigen einzelnen Toolintegrationen.
{: shortdesc}

Toolchains stehen in öffentlichen und dedizierten {{site.data.keyword.Bluemix}}-Umgebungen (Public bzw. Dedicated) zur Verfügung. Sie können eine Toolchain auf zwei Arten erstellen: Entweder Sie verwenden eine Vorlage zum Erstellen einer Toolchain oder Sie erstellen eine Toolchain aus einer App. Unter {{site.data.keyword.Bluemix_notm}} Public sind Toolchains nur in den USA (Süden) verfügbar.

##Einführung in Toolchains: Public
{: #getting_started_public}

Jede Toolchain ist einer bestimmten Organisation zugeordnet und alle Benutzer, die Mitglied dieser Organisation sind, können auf die ihr zugeordneten Toolchains zugreifen. Bevor Sie eine Toolchain erstellen, müssen Sie sicherstellen, dass Sie in der Organisation arbeiten, in der Sie die Toolchain erstellen wollen. Die Organisation, in der Sie gegenwärtig arbeiten, wird in der Menüleiste angezeigt. Um zu einer anderen Organisation zu wechseln, klicken Sie in der Menüleiste auf die Organisation und wählen Sie anschließend die Organisation aus, zu der Sie wechseln möchten.

###Toolchain aus einer Vorlage erstellen   
{: #creating_a_toolchain_from_a_template}

ie können eine Vorlage als Ausgangspunkt zum [Erstellen einer Toolchain (Link wird in neuem Fenster geöffnet)](https://console.ng.bluemix.net/devops/create){: new_window} verwenden, die eine bestimmte Gruppe von Toolintegrationen enthält. Weitere Informationen zur Verwendung von Vorlagen finden Sie in [IBM Bluemix Garage Method (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/category/tools){:new_window}.

1. Melden Sie sich an [{{site.data.keyword.Bluemix_notm}} (Link wird in neuem Fenster geöffnet)](http://console.ng.bluemix.net){:new_window} an. Das {{site.data.keyword.Bluemix_notm}}-Dashboard wird geöffnet, das eine Übersicht über den aktiven {{site.data.keyword.Bluemix_notm}}-Bereich für Ihre Organisation enthält.
1. Klicken Sie im 'Hamburger'-Menü auf **Services** und dann auf **DevOps**.
1. Klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf **Toolchain erstellen**.
1. Klicken Sie auf der Seite **Toolchain erstellen** auf eine Toolchain-Vorlage.
1. Überprüfen Sie das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in ihrer aktuellen Lebenszyklusphase in der Toolchain angezeigt. Das Diagramm in der folgenden Abbildung ist ein Beispiel. Wenn Sie eine Toolchain erstellen, zeigt das Diagramm jede Toolintegration an, die Teil der Toolchain ist.
![Diagramm einer Toolchain](images/toolchain_diagram.png)

1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. Wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain.  
1. Wählen Sie im Abschnitt mit den konfigurierbaren Integrationen jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Einige Toolintegrationen erfordern keine Konfiguration. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**.  Es werden verschiedene Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten:

 * Die Toolchain wird erstellt.
 * Falls Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines erstellt und aktiviert.
 * Falls Sie die Sauce Labs-Toolintegration konfiguriert haben, wird Sauce Labs konfiguriert, um Jobs zu Pipelines hinzuzufügen und Tests auszuführen.
 * Falls Sie die PagerDuty-Toolintegration konfiguriert haben, wird PagerDuty konfiguriert, um Alertbenachrichtigungen an den angegebenen Service zu senden. 
 * Falls Sie die Slack-Toolintegration konfiguriert haben, wird Slack konfiguriert, um Benachrichtigungen zum Bereitstellungsstatus an den angegebenen Kanal zu senden. 
 * Falls Sie die GitHub-Toolintegration konfiguriert haben, wird das GitHub-Beispielrepository in Ihr GitHub-Konto geklont.


###Toolchain aus einer App erstellen
{: #creating_a_toolchain_from_an_app}

Sie können eine Toolchain aus Ihrer App erstellen. Die Toolchain kann kontinuierliche Entwicklung, Bereitstellung, Überwachung und mehr unterstützen und sie ist Ihrer App zugeordnet. Jede App kann einer Toolchain zugeordnet sein. Wenn Sie Änderungen per Push-Operation an das GitHub-Repository der Toolchain übertragen, erstellt die Pipeline automatisch Builds und stellt die App bereit.  

1. Klicken Sie auf der Übersichtsseite Ihrer App auf der Kachel 'Continuous Delivery' auf **Aktivieren**. Ihre App wird für eine kontinuierliche Bereitstellung aus einem neuen GitHub-Repository konfiguriert, in dem der App-Starter-Code angegeben wird.
1. Überprüfen Sie auf der Seite zum Erstellen der Toolchain das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in ihrer aktuellen Lebenszyklusphase in der Toolchain angezeigt.
1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. Wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain.
1. Wählen Sie im Abschnitt mit den konfigurierbaren Integrationen jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Einige Toolintegrationen erfordern keine Konfiguration. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**. Es werden verschiedene Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten:

 * Die Toolchain wird erstellt.
 * Falls Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines erstellt und aktiviert.
 * Falls Sie die Sauce Labs-Toolintegration konfiguriert haben, wird Sauce Labs konfiguriert, um Jobs zu Pipelines hinzuzufügen und Tests auszuführen.
 * Falls Sie die PagerDuty-Toolintegration konfiguriert haben, wird PagerDuty konfiguriert, um Alertbenachrichtigungen an den angegebenen Service zu senden. 
 * Falls Sie die Slack-Toolintegration konfiguriert haben, wird Slack konfiguriert, um Benachrichtigungen zum Bereitstellungsstatus an den angegebenen Kanal zu senden. 
 * Falls Sie die GitHub-Toolintegration konfiguriert haben, wird das GitHub-Beispielrepository in Ihr GitHub-Konto geklont.


##Einführung in Toolchains: Dedicated
{: #getting_started_dedicated}

Jede Toolchain ist einer bestimmten Organisation zugeordnet und alle Benutzer, die Mitglieder dieser Organisation sind, können auf die zugeordneten Toolchains zugreifen. Klicken Sie vor dem Erstellen einer Toolchain auf das Symbol **{{site.data.keyword.avatar}}** in der Menüleiste, um das Widget 'Konto und Unterstützung' zu öffnen und um die Organisation anzuzeigen, in der Sie arbeiten. Wenn es sich dabei nicht um die Organisation handelt, in der Sie die Toolchain erstellen wollen, müssen Sie zu einer anderen Organisation wechseln.

###Toolchain aus einer Vorlage erstellen   
{: #creating_a_toolchain_from_a_template_dedicated}

Sie können eine Vorlage als Ausgangspunkt zum Erstellen einer Toolchain verwenden, die eine bestimmte Gruppe von Toolintegrationen enthält.

1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf der Registerkarte **DEVOPS** auf die Schaltfläche zum Hinzufügen (+), um eine Toolchain zu erstellen.
1. Klicken Sie auf der Seite **Toolchain erstellen** auf eine Toolchain-Vorlage. 
1. Überprüfen Sie das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in ihrer aktuellen Lebenszyklusphase in der Toolchain angezeigt. Das Diagramm in der folgenden Abbildung ist ein Beispiel. Wenn Sie eine Toolchain erstellen, zeigt das Diagramm jede Toolintegration an, die Teil der Toolchain ist.
![Dedicated-Toolchain-Diagramm](images/toolchain_dedicated_diagram.png)

1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. Wenn es bereits eine Toolchain mit diesem Namen gibt oder wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain.  
1. Wählen Sie im Abschnitt mit den konfigurierbaren Integrationen jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Einige Toolintegrationen erfordern keine Konfiguration. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**. Es werden verschiedene Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten:

 * Die Toolchain wird erstellt.
 * Falls Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines erstellt und aktiviert.
 * Falls Sie die PagerDuty-Toolintegration konfiguriert haben, wird PagerDuty konfiguriert, um Alertbenachrichtigungen an den angegebenen Service zu senden.
 * Falls Sie die Slack-Toolintegration konfiguriert haben, wird Slack konfiguriert, um Benachrichtigungen zum Bereitstellungsstatus an den angegebenen Kanal zu senden.
 * Falls Sie die GitHub Enterprise-Toolintegration konfiguriert haben, wird das GitHub Enterprise-Beispielrepository in Ihr GitHub Enterprise-Konto geklont.


###Toolchain aus einer App erstellen
{: #creating_a_toolchain_from_an_app_dedicated}

Sie können eine Toolchain aus Ihrer App erstellen. Die Toolchain kann kontinuierliche Entwicklung, Bereitstellung, Überwachung und mehr unterstützen und sie ist Ihrer App zugeordnet. Jede App kann einer Toolchain zugeordnet sein. Wenn Sie Änderungen per Push-Operation an das GitHub Enterprise-Repository der Toolchain übertragen, erstellt die Pipeline automatisch Builds und stellt die App bereit.  

1. Klicken Sie in der rechten oberen Ecke auf der Übersichtsseite der App auf **Toolchain hinzufügen**. Ihre App wird für eine kontinuierliche Bereitstellung aus einem neuen GitHub Enterprise-Repository konfiguriert, in dem der App-Starter-Code angegeben wird.
1. Überprüfen Sie auf der Seite zum Erstellen der Toolchain das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in ihrer aktuellen Lebenszyklusphase in der Toolchain angezeigt.
1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. Wenn es bereits eine Toolchain mit diesem Namen gibt oder wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain.
1. Wählen Sie im Abschnitt mit den konfigurierbaren Integrationen jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Einige Toolintegrationen erfordern keine Konfiguration. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**.  Es werden verschiedene Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten:

 * Die Toolchain wird erstellt.
 * Falls Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines erstellt und aktiviert.
 * Falls Sie die PagerDuty-Toolintegration konfiguriert haben, wird PagerDuty konfiguriert, um Alertbenachrichtigungen an den angegebenen Service zu senden.
 * Falls Sie die Slack-Toolintegration konfiguriert haben, wird Slack konfiguriert, um Benachrichtigungen zum Bereitstellungsstatus an den angegebenen Kanal zu senden.
 * Falls Sie die GitHub Enterprise-Toolintegration konfiguriert haben, wird das GitHub Enterprise-Beispielrepository in Ihr GitHub Enterprise-Konto geklont.


##Toolchain anzeigen
{: #viewing_a_toolchain}

Nachdem Sie die Toolchain und die zugehörigen Toolintegrationen konfiguriert haben, können Sie eine grafische Darstellung der Toolchain anzeigen.

* Klicken Sie bei Verwendung von {{site.data.keyword.Bluemix_notm}} Public im DevOps-Dashboard auf der Seite **Toolchains** auf eine Toolchain, um die zugehörige Übersichtsseite anzuzeigen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie anschließend auf **Übersicht**. 
   
* Wenn Sie {{site.data.keyword.Bluemix_notm}} Dedicated verwenden, klicken Sie im Dashboard auf der Registerkarte **DEVOPS** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie in der rechten oberen Ecke auf der Übersichtsseite der App auf **Toolchain anzeigen** klicken.

* Um auf eine Toolintegration in Ihrer Toolchain zuzugreifen, klicken Sie auf die Kachel des entsprechenden Tools. 
 
 **Tipp**: Wenn Sie über mehr als ein GitHub Enterprise-Repository verfügen, kann es für dieselbe Toolintegration mehrere Kacheln geben, da jedes Repository durch eine eigene Kachel dargestellt wird.


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
