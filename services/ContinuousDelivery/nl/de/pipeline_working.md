---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-28"

---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# Mit {{site.data.keyword.deliverypipeline}} arbeiten {: #pipeline-working}

Um Ihre Builds und Bereitstellungen für {{site.data.keyword.Bluemix}} zu automatisieren, verwenden Sie {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Bei {{site.data.keyword.deliverypipeline}} können Sie unter verschiedenen Buildtypen auswählen. Sie stellen das Build-Script bereit und {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} führt es aus. Es müssen keine Buildsysteme eingerichtet werden. Anschließend können Sie mit einem einzigen Mausklick Ihre App automatisch in einem oder mehreren {{site.data.keyword.Bluemix_notm}}-Bereichen, auf öffentlichen Cloud Foundry-Servern oder Docker-Containern in IBM Containers for {{site.data.keyword.Bluemix_notm}} bereitstellen.

Über Buildjobs wird Ihr App-Quellcode aus Git-Repositorys heraus kompiliert und paketiert. Bei den Buildjobs werden bereitstellbare Artefakte wie WAR-Dateien oder Docker-Container für IBM Containers erstellt. Sie können außerdem innerhalb Ihres Builds automatisch Komponententests ausführen. Sie können Ihre Buildjobs so konfigurieren, dass bei jedem mit Push-Operation übertragenen Commit ein Build ausgelöst wird.

Ein Bereitstellungsjob erhält Output von einem Buildjob und stellt ihn entweder IBM Containers oder Cloud Foundry-Servern bereit, z. B. {{site.data.keyword.Bluemix_notm}}.

Es ist eine Bereitstellung für eine oder mehrere Regionen bzw. einen oder mehrere Services möglich. Sie können Ihre {{site.data.keyword.deliverypipeline}} beispielsweise so einrichten, dass sie mindestens einen Service verwendet, in einer einzigen Region getestet oder und in mehreren Regionen für die Produktion bereitgestellt wird. Weitere Informationen hierzu finden Sie unter [Regionen](/docs/overview/whatisbluemix.html#ov_intro_reg){: new_window}.

Wenn Sie mehrere Pipelines in einer offenen Toolchain verwenden, können Sie eine Kombinationspipeline erstellen, um die Bereitstellung aller Pipelines von einem zentralen Punkt aus zu verwalten.

Es gibt mehrere Möglichkeiten für die Erstellung einer Pipeline; dazu gehören das Hinzufügen einer Pipeline zu einer vorhandenen Anwendung sowie die Erstellung einer Pipeline ohne vorhandene Anwendung. Wenn Ihre Organisation noch keinen {{site.data.keyword.deliverypipeline}}-Service hat, können Sie den Katalog aufrufen und auf '{{site.data.keyword.deliverypipeline}}' sowie auf 'Erstellen' klicken.

Führen Sie diese Schritte aus, um eine {{site.data.keyword.deliverypipeline}} für eine vorhandene Anwendung einzurichten:

1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Apps-Dashboard auf Ihre App.
1. Klicken Sie im Menü in der {{site.data.keyword.Bluemix_notm}}-Menüleiste auf **Services** und dann
auf **DevOps**. 
1. Klicken Sie auf **Pipelines** und dann auf **Pipeline erstellen**.

Führen Sie zum [Erstellen einer Pipeline![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}, die für die Bereitstellung einer Cloud Foundry-Anwendung konfiguriert ist, die folgenden Schritte aus:

1. Klicken Sie auf **Cloud Foundry**.
1. Wenn Sie einen anderen Namen für die Pipeline verwenden möchten, ändern Sie den Standardnamen.
1. Wenn Sie einen anderen Namen für die Anwendung verwenden möchten, ändern Sie den Standardnamen. Dieser Name ist der Name der Anwendung, in der die Bereitstellung durch die Pipeline erfolgt.
1. Wenn Sie über keine Toolchain verfügen, wird eine Toolchain mit einem Standardnamen erstellt. Wenn Sie einen anderen Namen für die Toolchain verwenden möchten, ändern Sie den Namen entsprechend. Durch die Integration anderer Tools und Services haben Sie mit der Toolchain die Möglichkeit, die Funktionalität Ihrer Pipeline zu erweitern. Weitere Informationen zu Toolchains enthält [Mit Toolchains arbeiten](/docs/services/ContinuousDelivery/toolchains_working.html){: new_window}.

 **Tipp**: Pipelines und Toolchains gehören zu Organisationen. Wenn Sie einer Organisation angehören, die über Toolchains verfügt, können Sie zu der Zugriffssteuerungsliste für jede der zugeordneten Toolchains hinzugefügt werden. Nachdem Sie zu der Zugriffskontrollliste für eine Toolchain hinzugefügt worden sind, können Sie diese Toolchain sowie alle zugeordneten Pipelines benutzen, selbst wenn Sie diese nicht erstellt haben. Weitere Informationen zur Zugriffssteuerung für Toolchains enthält [Zugriff verwalten](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){: new_window}.

1. Wählen Sie entweder den Namen der gewünschten Toolchain aus oder geben Sie einen Namen für die neue Toolchain ein, die Sie erstellen möchten.
1. Wählen Sie Ihren Git-Provider aus.

 **Tipp**: Falls Sie {{site.data.keyword.Bluemix_notm}} nicht für den Zugriff auf GitHub autorisiert haben, klicken Sie auf **Autorisieren**, um zur GitHub-Website zu wechseln. Wenn keine aktive GitHub-Sitzung existiert, werden Sie aufgefordert, sich anzumelden. Klicken Sie auf **Anwendung autorisieren**, um {{site.data.keyword.Bluemix_notm}} den Zugriff auf Ihr GitHub-Konto zu erlauben. Falls eine aktive GitHub-Sitzung existiert, Sie Ihr Kennwort aber bereits vor einiger Zeit eingegeben haben, werden Sie möglicherweise aufgefordert, Ihr GitHub-Kennwort durch erneute Eingabe zu bestätigen.

   * Falls Sie über ein Repository verfügen und dieses verwenden möchten, klicken Sie beim Repository-Typ auf **Verknüpfen**. Suchen Sie die Position des Repositorys oder wählen Sie das Repository aus der Liste der verfügbaren Repositorys aus.

   * Wenn Sie ein leeres Repository erstellen möchten, klicken Sie beim Repository-Typ auf **Neu**. Geben Sie einen Namen für das Repository ein.

   * Wenn Sie einen Klon eines Repositorys erstellen möchten, wählen Sie beim Repository-Typ **Kopieren** aus. Suchen Sie die Position des Repositorys oder wählen Sie das Repository aus der Liste der verfügbaren Repositorys aus.

   * Wenn Sie ein Repository verzweigen möchten, sodass Sie Änderungen über Pull-Anforderungen beitragen können, klicken Sie auf **Verzweigen**. Suchen Sie die Position des Repositorys oder wählen Sie das Repository aus der Liste der verfügbaren Repositorys aus.

1. Wählen Sie ein Repository aus oder geben Sie die URL für ein Repository ein.
1. Klicken Sie auf **Erstellen**. Die Pipeline wird erstellt, konfiguriert und auf der Übersichtsseite der Toolchain angezeigt.
 ![Karte für Pipeline](images/cd_pipeline.png)
1. Wenn Sie eine Pipeline in einer Toolchain erstellt haben, die eine Kombinationspipeline enthält, wird die neu erstellte Pipeline zu der Kombinationspipeline hinzugefügt. Nehmen Sie Änderungen am Bereitstellungsplan vor, sodass dieser Bereitstellungstasks für die neue Pipeline enthält. Näheres enthält [Delivery Pipeline-Tasks erstellen](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html#tasks_pipelineCD){: new_window}.

Führen Sie zum Erstellen einer [leeren Pipeline ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} ohne jegliche vorkonfigurierten Stages die folgenden Schritte aus:

1. Klicken Sie auf **Angepasst**.
1. Wenn Sie einen anderen Namen für die Pipeline verwenden möchten, ändern Sie den Standardnamen.
1. Wenn Sie über keine Toolchain verfügen, wird eine Toolchain mit einem Standardnamen erstellt. Wenn Sie einen anderen Namen für die Toolchain verwenden möchten, ändern Sie den Namen entsprechend. Durch die Integration anderer Tools und Services haben Sie mit der Toolchain die Möglichkeit, die Funktionalität Ihrer Pipeline zu erweitern.
1. Wählen Sie entweder den Namen der gewünschten Toolchain aus oder geben Sie einen Namen für die neue Toolchain ein, die Sie erstellen möchten.
1. Klicken Sie auf **Erstellen**. Daraufhin wird eine leere Pipeline erstellt und auf der Übersichtsseite als Karte dargestellt.

Von {{site.data.keyword.deliverypipeline}} aus können Sie Ihre Konfiguration ändern, den Status von Builds, der bereitgestellten App und von kürzlich erfolgten Bereitstellungen überprüfen, die aktuellen Protokolle und Bereitstellungsdetails anzeigen und Ihre Pipeline löschen.
