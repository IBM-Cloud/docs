---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Einführung in {{site.data.keyword.contdelivery_short}}
{: #cd_getting_started}

Letzte Aktualisierung: 18. November 2016
{: .last-updated}  

Nutzen Sie DevOps-Verfahren durch Verwendung von {{site.data.keyword.contdelivery_full}}, das Toolchains zur Automatisierung der Erstellung und Bereitstellung von Anwendungen enthält. Beginnen Sie mit der Erstellung einer einfachen Toolchain für die Bereitstellung, die Entwicklungs-, Bereitstellungs- und Operationstasks unterstützt.
{: shortdesc}

Nach der Erstellung einer {{site.data.keyword.contdelivery_short}}-Instanz durch Auswahl der entsprechenden Servicekachel im {{site.data.keyword.Bluemix_notm}}-Katalog können Sie auswählen, wie Sie mit dem Service beginnen möchten.
 ![Einführungsseite für Continuous Delivery](images/cd_landing_page.png)

 * Klicken Sie für einen schnellen Start durch Bereitstellung Ihrer Anwendung mithilfe einer automatisierten Pipeline im Abschnitt für den Start mit einer Pipeline auf **[Hier beginnen](#starting_with_a_pipeline)**. Sie können später weitere Tools hinzufügen. 
 * Klicken Sie zum Erstellen und Konfigurieren einer Continuous Delivery-Toolchain anhand einer Vorlage im Abschnitt für den Start mit einer Toolchain-Vorlage auf **[Hier beginnen](#starting_from_a_toolchain_template)**. Die Toolchain integriert Tools für Planung, Entwicklung und Bereitstellung von Pipelinees sowie für die Verwaltung Ihrer Anwendungen. Tools können jederzeit in eine Toolchain eingefügt oder daraus entfernt werden.
 * Wenn Sie bereits über Toolchains verfügen, klicken Sie im Abschnitt 'Mit einer Toolchain-Vorlage beginnen' auf **Zeigen Sie Ihre Toolchains an**. Weitere Informationen zum Arbeiten mit Toolchains finden Sie unter [Toolchains unter Bluemix Public verwenden](/docs/services/ContinuousDelivery/toolchains_using.html){: new_window}.

##Mit einer Pipeline beginnen
{: #starting_with_a_pipeline}

Mit Pipelines können beispielsweise Builds und Bereitstellungen automatisiert werden. Wählen Sie eine Vorlage aus und geben Sie die Position des GitHub-Repositorys an, um mit einer automatisierten Pipeline zu beginnen.

Führen Sie zum [Erstellen einer Pipeline (Link wird in neuem Fenster geöffnet)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}, die für die Bereitstellung einer Cloud Foundry-Anwendung konfiguriert ist, die folgenden Schritte aus:

1. Klicken Sie auf **Cloud Foundry**.
1. Wenn Sie einen anderen Namen für die Pipeline verwenden möchten, ändern Sie den Standardnamen. Der Name der Pipeline macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. 
1. Wenn Sie einen anderen Namen für die Anwendung verwenden möchten, ändern Sie den Standardnamen. Der Name der Anwendung macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. Dieser Name ist der Name der Anwendung, in der die Bereitstellung durch die Pipeline erfolgt. 
1. Wenn Sie über keine Toolchain verfügen, wird eine Toolchain mit einem Standardnamen erstellt. Wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain. Pipelines werden von Toolchains verwaltet. Durch die Integration anderer Tools und Services haben Sie mit der Toolchain die Möglichkeit, die Funktionalität Ihrer Pipeline zu erweitern. 

 **Tipp**: Pipelines und Toolchains gehören zu Organisationen. Wenn Sie zu einer Organisation gehören, die über Toolchains verfügt, können Sie diese Toolchains verwenden, auch wenn Sie diese nicht erstellt haben.
 
1. Wählen Sie entweder den Namen der gewünschten Toolchain aus oder geben Sie einen Namen für die neue Toolchain ein, die Sie erstellen möchten.
1. Geben Sie die Position des GitHub-Repositorys an.

 **Tipp**: Falls Sie {{site.data.keyword.Bluemix_notm}} nicht für den Zugriff auf GitHub autorisiert haben, klicken Sie auf **Autorisieren**, um zur GitHub-Website zu wechseln. Wenn keine aktive GitHub-Sitzung existiert, werden Sie aufgefordert, sich anzumelden. Klicken Sie auf **Anwendung autorisieren**, um {{site.data.keyword.Bluemix_notm}} den Zugriff auf Ihr GitHub-Konto zu erlauben. Falls eine aktive GitHub-Sitzung existiert, Sie Ihr Kennwort aber bereits vor einiger Zeit eingegeben haben, werden Sie möglicherweise aufgefordert, Ihr GitHub-Kennwort durch erneute Eingabe zu bestätigen.

   * Wenn Sie über ein GitHub-Repository verfügen und es verwenden möchten, wählen Sie **Link** aus. Suchen Sie die Position des Repositorys oder wählen Sie das Repository aus der Liste der verfügbaren Repositorys aus.
   
   * Wenn Sie ein leeres GitHub-Repository erstellen möchten, wählen Sie für den Repository-Typ **Neu** aus. Geben Sie einen Namen für das Repository ein.
   
   * Wenn Sie einen Klon eines GitHub-Repositorys erstellen möchten, wählen Sie **Kopieren** aus. Suchen Sie die Position des Repositorys oder wählen Sie das Repository aus der Liste der verfügbaren Repositorys aus.
   
   * Wenn Sie ein GitHub-Repository verzweigen möchten, sodass Sie Änderungen über Pull-Anforderungen beitragen können, wählen Sie **Verzweigen** aus. Suchen Sie die Position des Repositorys oder wählen Sie das Repository aus der Liste der verfügbaren Repositorys aus.
 
1. Klicken Sie auf **Erstellen**. Die Pipeline wird erstellt, konfiguriert und auf der Übersichtsseite der Toolchain angezeigt. ![Kachel für Pipeline](images/cd_pipeline.png)
 
Gehen Sie wie folgt vor, um eine [leere Pipeline (Link wird in neuem Fenster geöffnet)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} ohne vorkonfigurierte Phasen zu erstellen:

1. Klicken Sie auf **Angepasst**.
1. Wenn Sie einen anderen Namen für die Pipeline verwenden möchten, ändern Sie den Standardnamen. Der Name der Pipeline macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. 
1. Wenn Sie über keine Toolchain verfügen, wird eine Toolchain mit einem Standardnamen erstellt. Wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain. Pipelines werden von Toolchains verwaltet. Durch die Integration anderer Tools und Services haben Sie mit der Toolchain die Möglichkeit, die Funktionalität Ihrer Pipeline zu erweitern.
1. Wählen Sie entweder den Namen der gewünschten Toolchain aus oder geben Sie einen Namen für die neue Toolchain ein, die Sie erstellen möchten.
1. Klicken Sie auf **Erstellen**. Daraufhin wird eine leere Pipeline erstellt und auf der Übersichtsseite als Kachel dargestellt.

##Mit einer Toolchain-Vorlage beginnen
{: #starting_from_a_toolchain_template}

Gehen Sie wie folgt vor, um eine Continuous Delivery-Toolchain anhand einer [Vorlage (Link wird in neuem Fenster geöffnet)](https://console.ng.bluemix.net/devops/create){: new_window} zu erstellen und zu konfigurieren:

1. Klicken Sie auf der Seite **Toolchain erstellen** auf eine Toolchain-Vorlage.  
1. Überprüfen Sie das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in ihrer aktuellen Lebenszyklusphase in der Toolchain angezeigt. Das Diagramm in der folgenden Abbildung ist ein Beispiel. Wenn Sie eine Toolchain erstellen, zeigt das Diagramm jede Toolintegration an, die Teil der Toolchain ist.
 ![Toolchain-Diagramm](images/toolchain_diagram.png)
1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. Wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain.
1. Wählen Sie im Abschnitt mit den konfigurierbaren Integrationen jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Einige Toolintegrationen erfordern keine Konfiguration. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**. Es werden verschiedene Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten:

 * Die Toolchain wird erstellt.
 * Falls Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines erstellt und aktiviert.
 * Falls Sie die Sauce Labs-Toolintegration konfiguriert haben, wird Sauce Labs konfiguriert, um Jobs zu Pipelines hinzuzufügen und Tests auszuführen.
 * Falls Sie die PagerDuty-Toolintegration konfiguriert haben, wird PagerDuty konfiguriert, um Alertbenachrichtigungen an den angegebenen Service zu senden.  
 * Falls Sie die Slack-Toolintegration konfiguriert haben, wird Slack konfiguriert, um Benachrichtigungen zum Bereitstellungsstatus an den angegebenen Kanal zu senden.  
 * Falls Sie die GitHub-Toolintegration konfiguriert haben, wird das GitHub-Beispielrepository in Ihr GitHub-Konto geklont. 

# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}

* [Create and use your first toolchain (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Create a custom toolchain (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Create an application with three microservices (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}

## Zugehörige Links
{: #general}

* [Microservices toolchain (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method){:new_window}
