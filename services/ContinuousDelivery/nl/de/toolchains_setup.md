---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Einführung in Toolchains
{: #toolchains-setup}

Letzte Aktualisierung: 28. April 2016
{: .last-updated}  

Sie können eine Toolchain auf zwei Arten erstellen: Entweder Sie verwenden eine Vorlage zum Erstellen einer Toolchain oder Sie fügen eine Toolchain einer App hinzu. Abhängig von der verwendeten Vorlage oder Toolchain umfasst die Toolchain unter Umständen ein GitHub-Repository, in dem ein App-Starter-Code und eine vorkonfigurierte Delivery Pipeline angegeben wird. Wenn Sie Änderungen per Push-Operation an das GitHub-Repository der Toolchain übertragen, erstellt die Delivery Pipeline automatisch Builds und stellt die App in {{site.data.keyword.Bluemix}} bereit. 
{: shortdesc}  

**Wichtig**: Diese Funktionalität ist experimentell. Toolchains können instabil und Änderungen unterworfen sein, die nicht mit früheren Versionen kompatibel sind. Der Einsatz in Produktionsumgebungen wird nicht empfohlen. Zur Verwendung von Toolchains muss eine einmalige [Zugriffsanforderung](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window} ausgeführt werden. Toolchains sind nur in den USA (Region Dallas) verfügbar.

## Toolchain aus einer Vorlage erstellen   
{: #creating_a_toolchain_from_a_template}

Nachdem Ihre Anforderung für den Zugriff auf Toolchains genehmigt wurde, können Sie eine Vorlage als Ausgangspunkt zum Erstellen einer Toolchain verwenden, die eine bestimmte Gruppe von Toolintegrationen enthält.

1. Klicken Sie im DevOps-Dashboard auf der Registerkarte **Toolchains** auf **Toolchain erstellen**, um Ihre erste Toolchain zu erstellen. Wenn Sie bereits über eine Toolchain verfügen, klicken Sie auf die Schaltfläche zum Hinzufügen (+), um eine weitere Toolchain zu erstellen.
1. Klicken Sie auf eine Toolchain-Vorlage. Klicken Sie beispielsweise auf **Cloud-native Toolchain für Microservices**, um ein Onlinegeschäftsmuster zum Erstellen der Toolchain zu verwenden. 
1. Überprüfen Sie auf der Seite zum Erstellen der Toolchain das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in ihrer aktuellen Lebenszyklusphase in der Toolchain angezeigt. Das Diagramm in der folgenden Abbildung ist ein Beispiel. Wenn Sie eine Toolchain erstellen, zeigt das Diagramm jede Toolintegration an, die Teil der Toolchain ist.
![Diagramm einer Toolchain](images/toolchain_diagram.png)

1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix}} identifizierbar. Wenn es bereits eine Toolchain mit diesem Namen gibt oder wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain.  
1. Wenn Sie die Toolchain vor der Konfiguration von Toolintegrationen erstellen möchten, klicken Sie auf **Erstellen** und bestätigen Sie, dass Sie die Toolchain ohne Toolintegrationen erstellen möchten. Fahren Sie mit dem Abschnitt zum [Erstellen einer Toolchain](#creating_a_toolchain) fort, in dem die Schritte zur automatischen Konfiguration der Toolchain beschrieben werden.  
1. Wenn Sie die Toolintegrationen vor der Erstellung der Toolchain konfigurieren möchten, wählen Sie im Abschnitt mit den konfigurierbaren Integrationen die Toolintegrationen aus, die Sie konfigurieren möchten. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren](../toolchains/toolchains_integrations.html){: new_window}. 

## Toolchain aus einer App erstellen
{: #creating_a_toolchain_from_an_app}

Nachdem Ihre Anforderung für den Zugriff auf Toolchains genehmigt wurde, können Sie eine Toolchains aus Ihrer App erstellen. Die Toolchain kann kontinuierliche Entwicklung, Bereitstellung, Überwachung und mehr unterstützen und sie ist Ihrer App zugeordnet. Jede App kann einer Toolchain zugeordnet sein. Wenn Sie Änderungen per Push-Operation an das GitHub-Repository der Toolchain übertragen, erstellt die Pipeline automatisch Builds und stellt die App bereit.  

1. Klicken Sie auf der Übersichtsseite Ihrer App auf der Kachel 'Continuous Delivery' auf **Toolchain hinzufügen**. Alternativ können Sie in Bluemix Classic Experience auf **Git hinzufügen** klicken. Ihre App wird für eine kontinuierliche Bereitstellung aus einem neuen GitHub-Repository konfiguriert, in dem der App-Starter-Code angegeben wird.
1. Überprüfen Sie auf der Seite zum Erstellen der Toolchain das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in ihrer aktuellen Lebenszyklusphase in der Toolchain angezeigt.
1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix}} identifizierbar. Wenn es bereits eine Toolchain mit diesem Namen gibt oder wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain.
1. Wählen Sie im Abschnitt mit den konfigurierbaren Integrationen jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren](../toolchains/toolchains_integrations.html){: new_window}.

## Toolchain konfigurieren
{: #setting_up_a_toolchain}

Wenn Sie Ihre Toolchain noch nicht erstellt haben, klicken Sie auf **Erstellen**. Es werden verschiedene Schritte automatisch ausgeführt, um Ihre Toolchain einzurichten:

 * Die Toolchain wird erstellt.
 * Falls Sie die Delivery Pipeline-Toolintegration konfiguriert haben, werden die Pipelines aktiviert.
 * Falls Sie die Sauce Labs-Toolintegration konfiguriert haben, wird die Sauce Labs-Integration konfiguriert, um Jobs zu Pipelines hinzuzufügen und Tests auszuführen.
 * Falls Sie die PagerDuty-Toolintegration konfiguriert haben, wird die PagerDuty-Integration konfiguriert, um Benachrichtigungen an den in Slack konfigurierten Kanal zu senden. Diese Benachrichtigungen weisen auf Probleme hin.
 * Falls Sie die Slack-Toolintegration konfiguriert haben, wird die Slack-Integration konfiguriert, um Benachrichtigungen an den in Slack konfigurierten Kanal zu senden. Diese Benachrichtigungen geben den Entwicklungsfortschritt an, z. B. `Verbunden mit Projekt XYZ`, `Pipeline konfiguriert` und `Stage 'Build' gestartet`.
 * Falls Sie die GitHub-Toolintegration konfiguriert haben, wird das GitHub-Beispielrepository in Ihr GitHub-Konto geklont.  
 
## Toolchain anzeigen
{: #viewing_a_toolchain}

Nach dem Konfigurieren der Toolchain und aller Toolintegrationen wird die Seite für Toolintegrationen geöffnet.

1. Überprüfen Sie die Seite, um eine grafische Darstellung der Toolchain für Ihre App anzuzeigen.
1. Um auf eine Toolintegration in Ihrer Toolchain zuzugreifen, klicken Sie auf die Kachel des entsprechenden Tools. 
 
 **Tipp**: Wenn Sie über mehr als ein GitHub-Repository verfügen, kann es für dieselbe Toolintegration mehrere Kacheln geben, da jedes Repository eine eigene Pipeline benötigt.
