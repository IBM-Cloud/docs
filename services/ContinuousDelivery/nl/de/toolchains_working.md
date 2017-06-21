---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Toolchains erstellen
{: #toolchains_getting_started}

Eine *Toolchain* ist eine Gruppe von Toolintegrationen, die Entwicklungs-, Bereitstellungs- und Systemtasks unterstützen. Die kollektive Leistung einer Toolchain ist höher als die Summe der zugehörigen einzelnen Toolintegrationen.
{: shortdesc}

Offene Toolchains stehen in den öffentlichen und den dedizierten Umgebungen von {{site.data.keyword.Bluemix}} (Public bzw. Dedicated) zur Verfügung. Sie können eine Toolchain auf zwei Arten erstellen: Entweder Sie verwenden eine Vorlage zum Erstellen einer Toolchain oder Sie erstellen eine Toolchain aus einer App.

Jede Toolchain ist einer bestimmten Organisation (org) zugeordnet und jeder Benutzer, der Mitglied dieser Organisation ist, kann für jede der ihr zugeordneten Toolchains zu der Zugriffssteuerungsliste hinzugefügt werden. Weitere Informationen zur Zugriffssteuerung für Toolchains enthält [Zugriff verwalten](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){: new_window}. Bevor Sie eine Toolchain erstellen, müssen Sie sicherstellen, dass Sie in der Organisation arbeiten, in der Sie die Toolchain erstellen wollen. Die Organisation, in der Sie gerade arbeiten, wird auf der Menüleiste angezeigt. Um zu einer anderen Organisation zu wechseln, klicken Sie in der Menüleiste auf die Organisation und wählen Sie dann die Organisation aus, zu der Sie wechseln möchten.


##Toolchain aus einer Vorlage erstellen   
{: #creating_a_toolchain_from_a_template}

Sie können eine Vorlage als Ausgangspunkt zum [Erstellen einer Toolchain ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/create){: new_window} verwenden, die eine bestimmte Gruppe von Toolintegrationen enthält. Weitere Informationen zur Verwendung von Vorlagen enthält [IBM Cloud Garage Method ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/category/tools){:new_window}.

1. Wenn Sie {{site.data.keyword.Bluemix_notm}} Public verwenden, melden Sie sich bei [{{site.data.keyword.Bluemix_notm}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://console.ng.bluemix.net){:new_window} an.
1. Wenn Sie {{site.data.keyword.Bluemix_notm}} Dedicated verwenden, melden Sie sich bei Ihrer dedizierten Umgebung auf {{site.data.keyword.Bluemix_notm}} an.
1. Klicken Sie im Menü in der {{site.data.keyword.Bluemix_notm}}-Menüleiste auf **Services** und dann auf
**DevOps**. 
1. Klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf **Toolchain erstellen**.
1. Klicken Sie auf der Seite **Toolchain erstellen** auf eine Toolchain-Vorlage.
1. Überprüfen Sie das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in ihrer aktuellen Lebenszyklusphase in der Toolchain angezeigt.

 **Tipp**: Für einige der Toolchain-Vorlagen sind mehrere Instanzen einer Toolintegration vorhanden. Die Vorlage für die Microservice-Toolchain unter {{site.data.keyword.Bluemix_notm}} Public enthält beispielsweise drei Instanzen von GitHub und drei Instanzen von Delivery Pipeline - jeweils eine Instanz für jeden der drei Microservices.

 Das Diagramm in der folgenden Abbildung ist ein Beispiel. Wenn Sie eine Toolchain erstellen, zeigt das Diagramm jede Toolintegration an, die Teil der Toolchain ist.
![Diagramm einer Toolchain](images/toolchain_diagram.png)

1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. Wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain.  
1. Wählen Sie im Abschnitt mit den Toolintegrationen jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Einige Toolintegrationen erfordern keine Konfiguration. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**. Zum Einrichten Ihrer Toolchain werden mehrere verschiedene Schritte automatisch ausgeführt. Die Toolintegrationen, die eingerichtet werden, unterscheiden sich voneinander, je nachdem, welche Toolchain-Vorlage Sie ausgewählt haben und ob Sie {{site.data.keyword.Bluemix_notm}} Public oder {{site.data.keyword.Bluemix_notm}} Dedicated verwenden. Wenn Sie eine Microservice-Toolchain unter {{site.data.keyword.Bluemix_notm}} Public erstellen, werden zum Beispiel die folgenden Schritte ausgeführt:

 * Die Toolchain wird erstellt.
 * Wenn Sie Delivery Pipeline konfiguriert haben, werden die Pipelines erstellt und aktiviert.
 * Wenn Sie Sauce Labs konfiguriert haben, wird die Toolchain so eingerichtet, dass Sauce Labs-Testjobs zu den Pipelines hinzugefügt werden.
 * Wenn Sie PagerDuty konfiguriert haben, wird die Toolchain so eingerichtet, dass sie Alertbenachrichtigungen an den von Ihnen angegebenen PagerDuty-Service sendet.
 * Wenn Sie Slack konfiguriert haben, wird die Toolchain so konfiguriert, dass sie Benachrichtigungen zum Bereitstellungsstatus an den von Ihnen angegebenen Kanal sendet.
 * Wenn Sie eine Quellcode-Toolintegration wie GitHub konfiguriert haben, wird das GitHub-Beispielrepository in Ihr GitHub-Konto geklont.


##Toolchain aus einer App erstellen
{: #creating_a_toolchain_from_an_app}

Sie können eine Toolchain aus Ihrer App erstellen. Die Toolchain kann kontinuierliche Entwicklung, Bereitstellung, Überwachung und mehr unterstützen und sie ist Ihrer App zugeordnet. Jede App kann einer Toolchain zugeordnet sein. Wenn Sie Änderungen per Push-Operation an das GitHub- oder das {{site.data.keyword.ghe_short}}-Repository der Toolchain übertragen, erstellt die Pipeline automatisch Builds der App und stellt die App bereit.  

1. Klicken Sie auf der Übersichtsseite Ihrer App auf der Karte für Continuous Delivery auf **Aktivieren**. Wenn Sie {{site.data.keyword.Bluemix_notm}} Public verwenden, wird Ihre App für die kontinuierliche Bereitstellung aus einem neuen GitHub-Repository konfiguriert, das den Startcode für die App enthält. Wenn Sie {{site.data.keyword.Bluemix_notm}} Dedicated verwenden, wird Ihre App für die kontinuierliche Bereitstellung aus einem neuen GitHub- oder {{site.data.keyword.ghe_short}}-Repository konfiguriert, das den Startcode für die App enthält.
1. Überprüfen Sie auf der Seite zum Erstellen der Toolchain das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in ihrer aktuellen Lebenszyklusphase in der Toolchain angezeigt.
1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. Wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain.
1. Wählen Sie im Abschnitt mit den Toolintegrationen jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Einige Toolintegrationen erfordern keine Konfiguration. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**.  Zum Einrichten Ihrer Toolchain werden mehrere verschiedene Schritte automatisch ausgeführt. Die Toolintegrationen, die eingerichtet werden, unterscheiden sich voneinander, je nachdem, ob Sie Toolchains unter {{site.data.keyword.Bluemix_notm}} Public oder unter {{site.data.keyword.Bluemix_notm}} Dedicated verwenden. Wenn Sie eine Toolchain aus einer App unter {{site.data.keyword.Bluemix_notm}} Public erstellen, werden zum Beispiel die folgenden Schritte ausgeführt:

 * Die Toolchain wird erstellt.
 * Wenn Sie Delivery Pipeline konfiguriert haben, werden die Pipelines erstellt und aktiviert.
 * Wenn Sie GitHub konfiguriert haben, wird das GitHub-Beispielrepository in Ihr GitHub-Konto geklont.


##Toolchain anzeigen
{: #viewing_a_toolchain}

Nachdem Sie die Toolchain und die zugehörigen Toolintegrationen konfiguriert haben, können Sie eine grafische Darstellung der Toolchain anzeigen.

1. Klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** klicken. Klicken Sie anschließend auf **Übersicht**.
2. Um auf eine Toolintegration in Ihrer Toolchain zuzugreifen, klicken Sie auf das entsprechende Tool.

 **Tipp**: Wenn Sie über mehr als ein GitHub-, {{site.data.keyword.ghe_short}}- oder Git-Repository verfügen, sind möglicherweise mehrere Karten für dieselbe Toolintegration vorhanden, da jedes Repository durch eine eigene Karte dargestellt wird. Wenn Sie über mehrere Pipelines verfügen, sind gegebenenfalls mehrere Karten für dieselbe Toolintegration vorhanden, da jede Pipeline durch ihre eigene Karte dargestellt wird. Wenn Sie eine Microservice-Toolchain erstellen, besitzt jeder dieser drei Microservices sein eigenes GitHub-, {{site.data.keyword.ghe_short}}- oder Git-Repository und seine eigene Pipeline.
