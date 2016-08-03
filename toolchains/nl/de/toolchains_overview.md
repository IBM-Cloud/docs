---

Copyright:
  Jahre: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Erste Schritte mit Toolchains
(experimentell) 
{: #toolchains_getting_started}

*Letzte Aktualisierung: 8. Juni 2016*
{: .last-updated}  

Eine Toolchain ist eine Gruppe von Toolintegrationen, die
Entwicklungs-, Bereitstellungs- und Systemtasks unterstützen. Die
kollektive Leistung einer Toolchain ist höher als die Summe der
zugehörigen einzelnen Toolintegrationen.
{: shortdesc}

Sie können eine Toolchain auf zwei Arten erstellen:
Entweder Sie verwenden eine Vorlage zum Erstellen einer Toolchain
oder Sie erstellen eine Toolchain aus einer App. Abhängig von
der verwendeten Vorlage oder Toolchain umfasst die Toolchain unter
Umständen ein GitHub-Repository, in dem ein App-Startercode und eine
vorkonfigurierte Delivery Pipeline angegeben wird. Wenn Sie
Änderungen per Push-Operation an das GitHub-Repository der Toolchain
übertragen, erstellt die Delivery Pipeline automatisch
Builds und stellt die App in {{site.data.keyword.Bluemix}}
bereit. 

Als Ausgangspunkt können Sie eine Toolchain-Vorlage verwenden,
um eine Toolchain zu erstellen, die eine bestimmte Gruppe von
Toolintegrationen enthält, oder eine leere Toolchain, zu der Sie
Toolintegrationen hinzufügen können. 

**Wichtig**: Diese Funktion ist
experimentell. Toolchains sind unter Umständen nicht stabil und
können sich auf eine Weise ändern, die nicht mit früheren Versionen
kompatibel ist. Es wird empfohlen, sie nicht in Produktionsumgebungen
einzusetzen. Wenn Sie Toolchains verwenden möchten, müssen Sie eine
einmalige
[Zugriffsanforderung](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}
stellen. Toolchains sind nur in USA (Süden) verfügbar. 


##Toolchain aus einer Vorlage erstellen   
{: #creating_a_toolchain_from_a_template}

Nachdem Ihre Anforderung nach Zugriff auf Toolchains genehmigt wurde, können Sie eine Vorlage als Ausgangspunkt zum Erstellen einer Toolchain verwenden, die eine bestimmte Gruppe von Toolintegrationen enthält. 

1. Klicken Sie im DevOps-Dashboard auf der Registerkarte **Toolchains** auf **Toolchain erstellen**, um Ihre erste Toolchain zu erstellen. Wenn Sie bereits eine Toolchain haben, klicken Sie auf die Schaltfläche zum Hinzufügen (+), um eine weitere Toolchain zu erstellen. 
1. Klicken Sie auf eine Toolchainvorlage. Klicken Sie beispielsweise auf **Microservices-Toolchain**, um ein Onlinegeschäftsmuster zum Erstellen der Toolchain zu verwenden.  
1. Überprüfen Sie auf der Seite zum Erstellen der Toolchain das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in der entsprechenden Lebenszyklusphase in der Toolchain angezeigt. Das Diagramm in der folgenden Abbildung ist ein Beispiel. Wenn Sie eine Toolchain erstellen, zeigt das Diagramm jede Toolintegration an, die Teil der Toolchain ist.
![Diagramm einer Toolchain](images/toolchain_diagram.png)

1. Überprüfen Sie die Standardinformationen für die Toolchaineinstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix}} identifizierbar. Wenn es bereits eine Toolchain mit diesem Namen gibt oder wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain.   
1. Wählen Sie im Abschnitt mit den konfigurierbaren Integrationen jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren](../toolchains/toolchains_integrations.html){: new_window}. 
1. Klicken Sie auf **Erstellen**. Es werden verschiedene Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten: 

 * Die Toolchain wird erstellt. 
 * Falls Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines aktiviert. 
 * Falls Sie die Sauce Labs-Toolintegration konfiguriert haben, wird die Sauce Labs-Integration konfiguriert, um Jobs zu Pipelines hinzuzufügen und Tests auszuführen. 
 * Falls Sie die PagerDuty-Toolintegration konfiguriert haben, wird die PagerDuty-Integration konfiguriert, um Benachrichtigungen an den in Slack konfigurierten Kanal zu senden. Diese Benachrichtigungen geben an, wenn ein Problem auftritt. 
 * Falls Sie die Slack-Toolintegration konfiguriert haben, wird die Slack-Integration konfiguriert, um Benachrichtigungen an den in Slack konfigurierten Kanal zu senden. Diese Benachrichtigungen geben den Entwicklungsfortschritt an, z. B. `Verbunden mit Projekt XYZ`, `Pipeline konfiguriert` und `Stage 'Build' gestartet`. 
 * Falls Sie die GitHub-Toolintegration konfiguriert haben, wird das GitHub-Beispielrepository in Ihr GitHub-Konto geklont. 


##Toolchain aus einer App erstellen
{: #creating_a_toolchain_from_an_app}

Nachdem Ihre Anforderung nach Zugriff auf Toolchains genehmigt wurde, können Sie eine Toolchain aus Ihrer App erstellen. Die Toolchain kann kontinuierliche Entwicklung, Bereitstellung, Überwachung und mehr unterstützen und sie ist Ihrer App zugeordnet. Jede App kann einer Toolchain zugeordnet sein. Wenn Sie Änderungen per Push-Operation an das GitHub-Repository der Toolchain übertragen, erstellt die Pipeline automatisch Builds und stellt die App bereit.   

1. Klicken Sie auf der Übersichtsseite Ihrer App auf der Kachel 'Continuous Delivery' auf **Toolchain hinzufügen**. Alternativ können Sie in der klassischen Bluemix-Oberfläche auf **GIT HINZUFÜGEN** klicken. Ihre App wird für eine kontinuierliche Bereitstellung aus einem neuen GitHub-Repository konfiguriert, in dem der App-Startercode angegeben wird. 
1. Überprüfen Sie auf der Seite zum Erstellen der Toolchain das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in der entsprechenden Lebenszyklusphase in der Toolchain angezeigt. 
1. Überprüfen Sie die Standardinformationen für die Toolchaineinstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix}} identifizierbar. Wenn es bereits eine Toolchain mit diesem Namen gibt oder wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain. 
1. Wählen Sie im Abschnitt mit den konfigurierbaren Integrationen jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren](../toolchains/toolchains_integrations.html){: new_window}. 
1. Klicken Sie auf **Erstellen**. Es werden verschiedene Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten: 

 * Die Toolchain wird erstellt. 
 * Falls Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines aktiviert. 
 * Falls Sie die Sauce Labs-Toolintegration konfiguriert haben, wird die Sauce Labs-Integration konfiguriert, um Jobs zu Pipelines hinzuzufügen und Tests auszuführen. 
 * Falls Sie die PagerDuty-Toolintegration konfiguriert haben, wird die PagerDuty-Integration konfiguriert, um Benachrichtigungen an den in Slack konfigurierten Kanal zu senden. Diese Benachrichtigungen geben an, wenn ein Problem auftritt. 
 * Falls Sie die Slack-Toolintegration konfiguriert haben, wird die Slack-Integration konfiguriert, um Benachrichtigungen an den in Slack konfigurierten Kanal zu senden. Diese Benachrichtigungen geben den Entwicklungsfortschritt an, z. B. `Verbunden mit Projekt XYZ`, `Pipeline konfiguriert` und `Stage 'Build' gestartet`. 
 * Falls Sie die GitHub-Toolintegration konfiguriert haben, wird das GitHub-Beispielrepository in Ihr GitHub-Konto geklont. 

 
##Toolchain anzeigen
{: #viewing_a_toolchain}

Nachdem die Toolchain und alle Toolintegrationen konfiguriert wurden, können Sie eine grafische Darstellung der Toolchain auf der Seite mit den Toolintegrationen anzeigen. 

1. Klicken Sie im DevOps-Dashboard auf der Registerkarte **Toolchains** auf eine Toolchain, um die zugehörige Seite mit den Toolintegrationen anzuzeigen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** und dann auf **Toolintegrationen** klicken. 
1. Suchen Sie auf der Seite nach einer grafischen Darstellung der Toolchain. 
1. Um auf eine Toolintegration in Ihrer Toolchain zuzugreifen, klicken Sie auf die entsprechende Toolkachel.  
 
 **Tipp**: Wenn Sie über mehr als ein GitHub-Repository verfügen, kann es für dieselbe Toolintegration mehrere Kacheln geben, da für jedes Repository eine eigene Pipeline erforderlich ist. 


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}

* [Create an application with three microservices](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}

## Zugehörige Links
{: #general}

* [Microservices toolchain (Experimental)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain (Experimental)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM&reg; Bluemix&reg; Garage Method](https://www.ibm.com/devops/method){:new_window}
