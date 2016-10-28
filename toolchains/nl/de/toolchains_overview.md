---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Einführung in Toolchains (Experimentell)
{: #toolchains_getting_started}

Letzte Aktualisierung: 17. August 2016
{: .last-updated}  

Toolchains sind in den Public- und Dedicated-Umgebungen unter {{site.data.keyword.Bluemix}} verfügbar. Sie haben zwei Möglichkeiten, eine Toolchain zu erstellen: entweder mithilfe einer Schablone oder mithilfe einer App.
{: shortdesc}

**Wichtig**: Diese Funktion ist experimentell. Toolchains sind möglicherweise nicht stabil und können so geändert werden, dass sie nicht mehr mit früheren Versionen kompatibel sind. Sie sollten nicht in Produktionsumgebungen verwendet werden. Unter {{site.data.keyword.Bluemix_notm}} Public sind Toolchains nur in der Region 'Vereinigte Staaten (Süden)' verfügbar.


##Einführung in Toolchains: Öffentlich
{: #getting_started_public}

Jede Toolchain wird einer bestimmten Organisation zugeordnet und jeder Benutzer, der Mitglied dieser Organisation ist, kann auf die zugeordneten Toolchains zugreifen. Bevor Sie eine Toolchain erstellen können, müssen Sie sicherstellen, dass Sie in der Organisation arbeiten, in der Sie die Toolchain erstellen möchten. Um zu einer anderen Organisation zu wechseln, klicken Sie auf das **{{site.data.keyword.avatar}}**-Symbol ![Avatar-Symbol](../icons/i-avatar-icon.svg) in der Menüleiste, um das Widget 'Konto und Unterstützung' zu öffnen.

###Eine Toolchain mithilfe einer Schablone erstellen   
{: #creating_a_toolchain_from_a_template}

Sie können eine Schablone als Ausgangspunkt verwenden, um eine Toolchain zu erstellen, die einen bestimmten Satz an Toolintegrationen einbezieht.

1. Wenn Sie Ihre erste Toolchain erstellen, stellen Sie sicher, dass die Toolchains in Ihrer Organisation aktiviert sind:
   1. Öffnen Sie das DevOps-Dashboard und klicken Sie auf die Registerkarte **Toolchains**.
   2. Wenn die Schaltfläche **Toolchains aktivieren** angezeigt wird, klicken Sie darauf. Folgen Sie dann den Eingabeaufforderungen, um Ihre Toolchain zu erstellen.
   3. Wenn die Schaltfläche **Toolchains aktivieren** nicht angezeigt wird, wurden die Toolchains bereits aktiviert. Fahren Sie mit Schritt 2 fort.
1. Klicken Sie im DevOps-Dashboard in der Registerkarte **Toolchains** auf die Schaltfläche zu Hinzufügen (+), um eine Toolchain zu erstellen.
1. Klicken Sie auf eine Toolchain-Schablone. Wenn Sie beispielsweise ein Beispiel für ein Onlinegeschäft verwenden möchten, um die Toolchain zu erstellen, klicken Sie auf **Microservices-Toolchain**. 
1. Prüfen Sie auf der Seite zur Toolchain-Erstellung das Diagramm der Toolchain, die Sie erstellen möchten. Im Diagramm wird jede Toolintegration in seiner Lebenszyklusphase in der Toolchain angezeigt. Das Diagramm in der folgenden Abbildung ist ein Beispiel. Wenn Sie eine Toolchain erstellen, wird jede Toolintegration, die Teil der Toolchain ist, im Diagramm angezeigt.
![Toolchain-Diagramm](images/toolchain_diagram.png)

1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain identifiziert sie in {{site.data.keyword.Bluemix_notm}}. Wenn bereits eine Toolchain mit diesem Namen vorhanden ist oder Sie einen anderen Namen verwenden möchten, ändern Sie den Toolchain-Namen.  
1. Wählen Sie im Abschnitt 'Konfigurierbare Integrationen' jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Einige Toolintegrationen benötigen keine Konfiguration. Weitere Informationen zum Konfigurieren von Toolintegrationen finden Sie im Abschnitt [Toolintegrationen konfigurieren](../toolchains/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**.  Es werden mehrere Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten:

 * Die Toolchain wird erstellt.
 * Wenn Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines ausgelöst.
 * Wenn Sie die Sauce Labs-Toolintegration konfiguriert haben, wird die Sauce Labs-Integration so konfiguriert, dass den Pipelines Jobs hinzugefügt und Tests ausgeführt werden.
 * Wenn Sie die PagerDuty-Toolintegration konfiguriert haben, wird die PagerDuty-Integration so konfiguriert, dass Benachrichtigungen an den in Slack konfigurierten Kanal gesendet werden. Diese Benachrichtigungen verweisen auf ein Problem.
 * Wenn Sie die Slack-Toolintegration konfiguriert haben, wird die Slack-Integration so konfiguriert, dass Benachrichtigungen an den in Slack konfigurierten Kanal gesendet werden. Diese Benachrichtigungen geben den Bereitstellungsprozess an. Beispiel: `Verbunden mit Project XYZ`, `Pipeline konfiguriert` und `Stage 'build' gestartet`.
 * Wenn Sie die GitHub-Toolintegration konfiguriert haben, wird das GitHub-Beispiel-Repository in Ihrem GitHub-Konto geklont.


###Eine Toolchain mithilfe einer App erstellen
{: #creating_a_toolchain_from_an_app}

Sie können mithilfe Ihrer App eine Toolchain erstellen. Eine Toolchain kann eine kontinuierliche Entwicklung, Bereitstellung, Überwachung u.v.m. unterstützen und ist Ihrer App zugeordnet. Jede App kann einer Toolchain zugeordnet sein. Wenn Sie Änderungen mit Push-Operation an Ihr GitHub-Repository Ihrer Toolchain übertragen, erstellt die Pipeline die App automatisch und stellt sie bereit.  

1. Wenn Sie Ihre erste Toolchain erstellen, stellen Sie sicher, dass die Toolchains in Ihrer Organisation aktiviert sind:
   1. Öffnen Sie das DevOps-Dashboard und klicken Sie auf die Registerkarte **Toolchains**.
   2. Wenn die Schaltfläche **Toolchains aktivieren** angezeigt wird, klicken Sie darauf. Folgen Sie dann den Eingabeaufforderungen, um Ihre Toolchain zu erstellen.
   3. Wenn die Schaltfläche **Toolchains aktivieren** nicht angezeigt wird, wurden die Toolchains bereits aktiviert. Fahren Sie mit Schritt 2 fort.
1. Sie können als Alternative auf der Übersichtsseite Ihrer App in der Kachel 'Continuous Delivery' auf **Toolchain hinzufügen** klicken. Sie können auch in der klassischen {{site.data.keyword.Bluemix_notm}}-Ansicht oben rechts auf der Übersichtsseite Ihrer App auf **Toolchain hinzufügen** klicken. Ihre App ist für eine kontinuierliche Bereitstellung für ein neues GitHub-Repository konfiguriert, das mit dem App-Startercode gefüllt wird.
1. Prüfen Sie auf der Seite zur Toolchain-Erstellung das Diagramm der Toolchain, die Sie erstellen möchten. Im Diagramm wird jede Toolintegration in seiner Lebenszyklusphase in der Toolchain angezeigt. 
1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain identifiziert sie in {{site.data.keyword.Bluemix_notm}}. Wenn bereits eine Toolchain mit diesem Namen vorhanden ist oder Sie einen anderen Namen verwenden möchten, ändern Sie den Toolchain-Namen.
1. Wählen Sie im Abschnitt 'Konfigurierbare Integrationen' jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Einige Toolintegrationen benötigen keine Konfiguration. Weitere Informationen zum Konfigurieren von Toolintegrationen finden Sie im Abschnitt [Toolintegrationen konfigurieren](../toolchains/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**.  Es werden mehrere Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten:

 * Die Toolchain wird erstellt.
 * Wenn Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines ausgelöst.
 * Wenn Sie die Sauce Labs-Toolintegration konfiguriert haben, wird die Sauce Labs-Integration so konfiguriert, dass den Pipelines Jobs hinzugefügt und Tests ausgeführt werden.
 * Wenn Sie die PagerDuty-Toolintegration konfiguriert haben, wird die PagerDuty-Integration so konfiguriert, dass Benachrichtigungen an den in Slack konfigurierten Kanal gesendet werden. Diese Benachrichtigungen verweisen auf ein Problem.
 * Wenn Sie die Slack-Toolintegration konfiguriert haben, wird die Slack-Integration so konfiguriert, dass Benachrichtigungen an den in Slack konfigurierten Kanal gesendet werden. Diese Benachrichtigungen geben den Bereitstellungsprozess an. Beispiel: `Verbunden mit Project XYZ`, `Pipeline konfiguriert` und `Stage 'build' gestartet`.
 * Wenn Sie die GitHub-Toolintegration konfiguriert haben, wird das GitHub-Beispiel-Repository in Ihrem GitHub-Konto geklont.


##Einführung in Toolchains: Dedicated
{: #getting_started_dedicated}

Jede Toolchain wird einer bestimmten Organisation zugeordnet und jeder Benutzer, der Mitglied dieser Organisation ist, kann auf die zugeordneten Toolchains zugreifen. Bevor Sie eine Toolchain erstellen, klicken Sie auf das **{{site.data.keyword.avatar}}**-Symbol ![Avatar-Symbol](../icons/i-avatar-icon.svg) in der Menüleiste, um das Widget 'Konto und Unterstützung' zu öffnen und die Organisation zu öffnen, in der Sie arbeiten. Wenn es sich dabei nicht um die Organisation handelt, in der Sie die Toolchain erstellen möchten, wechseln Sie zu einer anderen Organisation.

###Eine Toolchain mithilfe einer Schablone erstellen   
{: #creating_a_toolchain_from_a_template_dedicated}

Sie können eine Schablone als Ausgangspunkt verwenden, um eine Toolchain zu erstellen, die einen bestimmten Satz an Toolintegrationen einbezieht.

1. Wenn Sie Ihre erste Toolchain erstellen, stellen Sie sicher, dass die Toolchains in Ihrer Organisation aktiviert sind:
   1. Öffnen Sie das DevOps-Dashboard und klicken Sie auf die Registerkarte **Toolchains**.
   2. Wenn die Schaltfläche **Toolchains aktivieren** angezeigt wird, klicken Sie darauf. Folgen Sie dann den Eingabeaufforderungen, um Ihre Toolchain zu erstellen.
   3. Wenn die Schaltfläche **Toolchains aktivieren** nicht angezeigt wird, wurden die Toolchains bereits aktiviert. Fahren Sie mit Schritt 2 fort.
1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard in der Registerkarte **DEVOPS** auf die Schaltfläche zu Hinzufügen (+), um eine Toolchain zu erstellen.
1. Klicken Sie auf eine Toolchain-Schablone. Um beispielsweise eine einfache Toolchain zu erstellen, die eine neue Cloud Foundry-App bereitstellt, klicken Sie auf **Einfache Cloud Foundry-Toolchain**. 
1. Prüfen Sie auf der Seite zur Toolchain-Erstellung das Diagramm der Toolchain, die Sie erstellen möchten. Im Diagramm wird jede Toolintegration in seiner Lebenszyklusphase in der Toolchain angezeigt. Das Diagramm in der folgenden Abbildung ist ein Beispiel. Wenn Sie eine Toolchain erstellen, wird jede Toolintegration, die Teil der Toolchain ist, im Diagramm angezeigt.
![Diagramm für eine Dedicated-Toolchain](images/toolchain_dedicated_diagram.png)

1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain identifiziert sie in {{site.data.keyword.Bluemix_notm}}. Wenn bereits eine Toolchain mit diesem Namen vorhanden ist oder Sie einen anderen Namen verwenden möchten, ändern Sie den Toolchain-Namen.  
1. Wählen Sie im Abschnitt 'Konfigurierbare Integrationen' jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Einige Toolintegrationen benötigen keine Konfiguration. Weitere Informationen zum Konfigurieren von Toolintegrationen finden Sie im Abschnitt [Toolintegrationen konfigurieren](../toolchains/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**.  Es werden mehrere Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten:

 * Die Toolchain wird erstellt.
 * Wenn Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines ausgelöst.
 * Wenn Sie die GitHub Enterprise-Toolintegration konfiguriert haben, wird das GitHub Enterprise-Beispiel-Repository in Ihrem GitHub Enterprise-Konto geklont.


###Eine Toolchain mithilfe einer App erstellen
{: #creating_a_toolchain_from_an_app_dedicated}

Sie können mithilfe Ihrer App eine Toolchain erstellen. Eine Toolchain kann eine kontinuierliche Entwicklung, Bereitstellung, Überwachung u.v.m. unterstützen und ist Ihrer App zugeordnet. Jede App kann einer Toolchain zugeordnet sein. Wenn Sie Änderungen mit Push-Operation an Ihr GitHub Enterprise-Repository Ihrer Toolchain übertragen, erstellt die Pipeline die App automatisch und stellt sie bereit.  

1. Wenn Sie Ihre erste Toolchain erstellen, stellen Sie sicher, dass die Toolchains in Ihrer Organisation aktiviert sind:
   1. Öffnen Sie das DevOps-Dashboard und klicken Sie auf die Registerkarte **Toolchains**.
   2. Wenn die Schaltfläche **Toolchains aktivieren** angezeigt wird, klicken Sie darauf. Folgen Sie dann den Eingabeaufforderungen, um Ihre Toolchain zu erstellen.
   3. Wenn die Schaltfläche **Toolchains aktivieren** nicht angezeigt wird, wurden die Toolchains bereits aktiviert. Fahren Sie mit Schritt 2 fort.
1. Sie können auf der Übersichtsseite Ihrer App rechts oben auf **Toolchain anzeigen** klicken. Ihre App ist für eine kontinuierliche Bereitstellung für ein neues GitHub Enterprise-Repository konfiguriert, das mit dem App-Startercode gefüllt wird.
1. Prüfen Sie auf der Seite zur Toolchain-Erstellung das Diagramm der Toolchain, die Sie erstellen möchten. Im Diagramm wird jede Toolintegration in seiner Lebenszyklusphase in der Toolchain angezeigt. 
1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain identifiziert sie in {{site.data.keyword.Bluemix_notm}}. Wenn bereits eine Toolchain mit diesem Namen vorhanden ist oder Sie einen anderen Namen verwenden möchten, ändern Sie den Toolchain-Namen.
1. Wählen Sie im Abschnitt 'Konfigurierbare Integrationen' jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Einige Toolintegrationen benötigen keine Konfiguration. Weitere Informationen zum Konfigurieren von Toolintegrationen finden Sie im Abschnitt [Toolintegrationen konfigurieren](../toolchains/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**.  Es werden mehrere Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten:

 * Die Toolchain wird erstellt.
 * Wenn Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines ausgelöst.
 * Wenn Sie die GitHub Enterprise-Toolintegration konfiguriert haben, wird das GitHub Enterprise-Beispiel-Repository in Ihrem GitHub Enterprise-Konto geklont.


##Eine Toolchain anzeigen
{: #viewing_a_toolchain}

Nachdem Sie die Toolchain und ihre Toolintegrationen konfiguriert haben, können Sie eine visuelle Darstellung der Toolchain auf der Seite 'Toolintegrationen' anzeigen.

* Wenn Sie {{site.data.keyword.Bluemix_notm}} Public verwenden, klicken Sie im DevOps-Dashboard in der Registerkarte **Toolchains** auf eine Toolchain, um ihre dazugehörige Seite 'Toolintegrationen' zu öffnen. Sie können als Alternative auf der Übersichtsseite der App in der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.  
   
* Wenn Sie {{site.data.keyword.Bluemix_notm}} Dedicated verwenden, klicken Sie im Dashboard in der Registerkarte **DEVOPS** auf eine Toolchain, um ihre dazugehörige Seite 'Toolintegrationen' zu öffnen. Sie können als Alternative auf der Übersichtsseite Ihrer App rechts oben auf **Toolchain anzeigen** klicken. 

* Um auf eine Toolintegration zuzugreifen, die sich in Ihrer Toolchain befindet, klicken Sie auf die Kachel für das entsprechende Tool. 
 
 **Tipp**: Wenn Sie mehr als ein GitHub- oder GitHub Enterprise-Repository besitzen, werden mehrere Kacheln für dieselbe Toolintegration angezeigt, da jedes Repository mit einer eigenen Kachel dargestellt wird.


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}

* [Eine Anwendung mit drei Microservices erstellen](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}
* [Eine Toolchain mithilfe einer Schablone unter {{site.data.keyword.Bluemix_notm}} Dedicated (Experimentell) erstellen](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Eine Toolchain mithilfe einer App unter {{site.data.keyword.Bluemix_notm}} Dedicated (Experimentell) erstellen](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Zugehörige Links
{: #general}

* [Microservices-Toolchain (Experimentell)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Einfache Toolchain (Experimentell)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method](https://www.ibm.com/devops/method){:new_window}
