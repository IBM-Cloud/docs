---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Einführung in Continuous Delivery
{: #cd_getting_started}

Nutzen Sie DevOps-Verfahren durch Verwendung von {{site.data.keyword.contdelivery_full}}, das offene Toolchains zur Automatisierung der Erstellung und Bereitstellung von Anwendungen enthält. Beginnen Sie mit der Erstellung einer einfachen Toolchain für die Bereitstellung, die Entwicklungs-, Bereitstellungs- und Operationstasks unterstützt.
{: shortdesc}

Nachdem Sie eine Instanz von {{site.data.keyword.contdelivery_short}} erstellt haben, indem Sie das Element im {{site.data.keyword.Bluemix_notm}}-Katalog ausgewählt haben, können Sie entscheiden, welches die ersten Schritte sind, die Sie mit dem Service ausführen wollen.
 ![Einführungsseite für Continuous Delivery](images/cd_landing_page.png)

 * Klicken Sie für einen schnellen Start durch Bereitstellung Ihrer Anwendung mithilfe einer automatisierten Pipeline im Abschnitt für den Start mit einer Pipeline auf **[Hier beginnen](#starting_with_a_pipeline)**. Sie können später weitere Tools hinzufügen.
 * Klicken Sie zum Erstellen und Konfigurieren einer Continuous Delivery-Toolchain anhand einer Vorlage im Abschnitt für den Start mit einer Toolchain-Vorlage auf **[Hier beginnen](#starting_from_a_toolchain_template)**. Die Toolchain integriert Tools für Planung, Entwicklung und Bereitstellung von Pipelines sowie für die Verwaltung Ihrer Anwendungen. Tools können jederzeit in eine Toolchain eingefügt oder daraus entfernt werden.
 * Wenn Sie bereits über Toolchains verfügen, klicken Sie im Abschnitt 'Mit einer Toolchain-Vorlage beginnen' auf **Zeigen Sie Ihre Toolchains an**. Weitere Informationen zum Arbeiten mit Toolchains enthält [Toolchains verwenden](/docs/services/ContinuousDelivery/toolchains_using.html){: new_window}. 

**Tipp**: Pipelines werden von Toolchains verwaltet. Sie können eine Pipeline zu einer vorhandenen Toolchain hinzufügen. Wenn Sie eine Pipeline erstellen, nicht aber über bereits vorhandene Toolchains verfügen, so wird eine Toolchain mit einem Standardnamen für Sie erstellt. Mit der Toolchain können Sie die Funktionalität Ihrer Pipeline durch Integrieren mit anderen Tools und Services erweitern. 

##Mit einer Pipeline beginnen
{: #starting_with_a_pipeline}

Mit Pipelines können beispielsweise Builds und Bereitstellungen automatisiert werden. Wählen Sie eine Vorlage aus und geben Sie die Position des GitHub-Repositorys an, um mit einer automatisierten Pipeline zu beginnen.

Führen Sie zum [Erstellen einer Pipeline![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){:new_window}, die für die Bereitstellung einer Cloud Foundry-Anwendung konfiguriert ist, die folgenden Schritte aus: 

1. Klicken Sie auf **Cloud Foundry**.
1. Wenn Sie einen anderen Namen für die Pipeline verwenden möchten, ändern Sie den Standardnamen. Der Name der Pipeline macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar.
1. Wenn Sie einen anderen Namen für die Anwendung verwenden möchten, ändern Sie den Standardnamen. Der Name der Anwendung macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. Dieser Name ist der Name der Anwendung, in der die Bereitstellung durch die Pipeline erfolgt.
1. Wenn Sie über keine Toolchain verfügen, wird eine Toolchain mit einem Standardnamen erstellt. Wenn Sie einen anderen Namen für die Toolchain verwenden möchten, ändern Sie den Namen entsprechend. Pipelines werden von Toolchains verwaltet. Durch die Integration anderer Tools und Services haben Sie mit der Toolchain die Möglichkeit, die Funktionalität Ihrer Pipeline zu erweitern.

 **Tipp**: Pipelines und Toolchains gehören zu Organisationen. Wenn Sie zu einer Organisation gehören, die über Toolchains verfügt, können Sie diese Toolchains verwenden, auch wenn Sie diese nicht erstellt haben.

1. Wählen Sie entweder den Namen der gewünschten Toolchain aus oder geben Sie einen Namen für die neue Toolchain ein, die Sie erstellen möchten.
1. Wählen Sie Ihren Git-Provider aus. 

 **Tipp**: Falls Sie {{site.data.keyword.Bluemix_notm}} nicht für den Zugriff auf GitHub autorisiert haben, klicken Sie auf **Autorisieren**, um zur GitHub-Website zu wechseln. Wenn keine aktive GitHub-Sitzung existiert, werden Sie aufgefordert, sich anzumelden. Klicken Sie auf **Anwendung autorisieren**, um {{site.data.keyword.Bluemix_notm}} den Zugriff auf Ihr GitHub-Konto zu erlauben. Falls eine aktive GitHub-Sitzung existiert, Sie Ihr Kennwort aber bereits vor einiger Zeit eingegeben haben, werden Sie möglicherweise aufgefordert, Ihr GitHub-Kennwort durch erneute Eingabe zu bestätigen.

 Wenn Sie nicht autorisiert sind, auf das {{site.data.keyword.ghe_short}}-Repository zuzugreifen, muss Sie jemand hinzufügen, der über Administratorberechtigungen für das Repository verfügt. Anweisungen zum Autorisieren bei {{site.data.keyword.Bluemix_notm}} Dedicated für {{site.data.keyword.ghe_short}} enthält [Einführung in {{site.data.keyword.Bluemix_notm}} Dedicated für {{site.data.keyword.ghe_short}}](/docs/services/ghededicated/index.html){: new_window}. Wenn Sie sich bei Ihrer eigenen verwalteten Version von {{site.data.keyword.ghe_short}} autorisieren müssen, gehen Sie gemäß Ihren eigenen internen Prozeduren vor. 

   * Falls Sie über ein Repository verfügen und dieses verwenden möchten, klicken Sie beim Repository-Typ auf **Verknüpfen**. Suchen Sie die Position des Repositorys oder wählen Sie das Repository aus der Liste der verfügbaren Repositorys aus.

   * Wenn Sie ein leeres Repository erstellen möchten, klicken Sie beim Repository-Typ auf **Neu**. Geben Sie einen Namen für das Repository ein.

   * Wenn Sie einen Klon eines Repositorys erstellen möchten, wählen Sie beim Repository-Typ **Kopieren** aus. Suchen Sie die Position des Repositorys oder wählen Sie das Repository aus der Liste der verfügbaren Repositorys aus.

   * Wenn Sie ein Repository verzweigen möchten, sodass Sie Änderungen über Pull-Anforderungen beitragen können, klicken Sie auf **Verzweigen**. Suchen Sie die Position des Repositorys oder wählen Sie das Repository aus der Liste der verfügbaren Repositorys aus.

1. Wählen Sie ein Repository aus oder geben Sie die URL für ein Repository ein. 
1. Klicken Sie auf **Erstellen**. Die Pipeline wird erstellt, konfiguriert und auf der Übersichtsseite der Toolchain angezeigt.
 ![Karte für Pipeline](images/cd_pipeline.png)

Führen Sie zum Erstellen einer [leeren Pipeline ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} ohne jegliche vorkonfigurierten Stages die folgenden Schritte aus: 

1. Klicken Sie auf **Angepasst**.
1. Wenn Sie einen anderen Namen für die Pipeline verwenden möchten, ändern Sie den Standardnamen. Der Name der Pipeline macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar.
1. Wenn Sie über keine Toolchain verfügen, wird eine Toolchain mit einem Standardnamen erstellt. Wenn Sie einen anderen Namen für die Toolchain verwenden möchten, ändern Sie den Namen entsprechend. Pipelines werden von Toolchains verwaltet. Durch die Integration anderer Tools und Services haben Sie mit der Toolchain die Möglichkeit, die Funktionalität Ihrer Pipeline zu erweitern.
1. Wählen Sie entweder den Namen der gewünschten Toolchain aus oder geben Sie einen Namen für die neue Toolchain ein, die Sie erstellen möchten.
1. Klicken Sie auf **Erstellen**. Daraufhin wird eine leere Pipeline erstellt und auf der Übersichtsseite als Karte dargestellt. 

##Mit einer Toolchain-Vorlage beginnen
{: #starting_from_a_toolchain_template}

Gehen Sie zum Erstellen und Konfigurieren einer Continuous Delivery-Toolchain anhand einer [Vorlage ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/create){: new_window} wie folgt vor: 

1. Klicken Sie auf der Seite **Toolchain erstellen** auf eine Toolchain-Vorlage.  
1. Überprüfen Sie das Diagramm der Toolchain, die Sie gerade erstellen. In dem Diagramm wird jede Toolintegration in ihrer aktuellen Lebenszyklusphase in der Toolchain angezeigt.

 **Tipp**: Für einige der Toolchain-Vorlagen sind mehrere Instanzen einer Toolintegration vorhanden. Die Vorlage für die Microservice-Toolchain unter {{site.data.keyword.Bluemix_notm}} Public enthält beispielsweise drei Instanzen von GitHub und drei Instanzen von Delivery Pipeline - jeweils eine Instanz für jeden der drei Microservices. 

 Das Diagramm in der folgenden Abbildung ist ein Beispiel. Wenn Sie eine Toolchain erstellen, zeigt das Diagramm jede Toolintegration an, die Teil der Toolchain ist.
 ![Toolchain-Diagramm](images/toolchain_diagram.png)
1. Überprüfen Sie die Standardinformationen für die Toolchain-Einstellungen. Der Name der Toolchain macht sie in {{site.data.keyword.Bluemix_notm}} identifizierbar. Wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain.
1. Wählen Sie im Abschnitt mit den Toolintegrationen jede Toolintegration aus, die Sie für Ihre Toolchain konfigurieren möchten. Einige Toolintegrationen erfordern keine Konfiguration. Informationen zum Konfigurieren der Toolintegrationen finden Sie unter [Toolintegrationen konfigurieren](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Klicken Sie auf **Erstellen**. Zum Einrichten Ihrer Toolchain werden mehrere verschiedene Schritte automatisch ausgeführt. Die Toolintegrationen, die eingerichtet werden, unterscheiden sich voneinander, je nachdem, welche Toolchain-Vorlage Sie ausgewählt haben und ob Sie {{site.data.keyword.Bluemix_notm}} Public oder {{site.data.keyword.Bluemix_notm}} Dedicated verwenden. Wenn Sie eine Microservice-Toolchain unter {{site.data.keyword.Bluemix_notm}} Public erstellen, werden zum Beispiel die folgenden Schritte ausgeführt: 

 * Die Toolchain wird erstellt.
 * Wenn Sie Delivery Pipeline konfiguriert haben, werden die Pipelines erstellt und ausgeführt. 
 * Wenn Sie Sauce Labs konfiguriert haben, wird die Toolchain so eingerichtet, dass Sauce Labs-Testjobs zu den Pipelines hinzugefügt werden. 
 * Wenn Sie PagerDuty konfiguriert haben, wird die Toolchain so eingerichtet, dass sie Alertbenachrichtigungen an den von Ihnen angegebenen PagerDuty-Service sendet. 
 * Wenn Sie Slack konfiguriert haben, wird die Toolchain so konfiguriert, dass sie Benachrichtigungen zum Bereitstellungsstatus an den von Ihnen angegebenen Kanal sendet. 
 * Wenn Sie eine Quellcode-Toolintegration wie GitHub konfiguriert haben, wird das GitHub-Beispielrepository in Ihr GitHub-Konto geklont. 
