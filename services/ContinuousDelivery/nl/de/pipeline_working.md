---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# Mit {{site.data.keyword.deliverypipeline}} arbeiten{: #pipeline-working}  

Letzte Aktualisierung: 18. November 2016
{: .last-updated}

Um Ihre Builds und Bereitstellungen für {{site.data.keyword.Bluemix}} zu automatisieren, verwenden Sie {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Bei {{site.data.keyword.deliverypipeline}} können Sie unter verschiedenen Buildtypen auswählen. Sie stellen das Build-Script bereit und {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} führt es aus. Es müssen keine Buildsysteme eingerichtet werden. Anschließend können Sie mit einem einzigen Mausklick Ihre App automatisch in einem oder mehreren {{site.data.keyword.Bluemix_notm}}-Bereichen, auf öffentlichen Cloud Foundry-Servern oder Docker-Containern in IBM Containers for {{site.data.keyword.Bluemix_notm}} bereitstellen.  

Über Build-Jobs wird Ihr App-Quellcode aus Git-Repositorys heraus kompiliert und paketiert. Bei den Build-Jobs werden bereitstellbare Artefakte wie WAR-Dateien oder Docker-Container für IBM Containers erstellt. Sie können außerdem innerhalb Ihres Builds automatisch Komponententests ausführen. Sie können Ihre Buildjobs so konfigurieren, dass bei jedem mit Push-Operation übertragenen Commit ein Build ausgelöst wird.

Ein Bereitstellungsjob erhält Output von einem Build-Job und stellt ihn entweder IBM Containers oder Cloud Foundry-Servern bereit, z. B. {{site.data.keyword.Bluemix_notm}}.  

Es ist eine Bereitstellung für eine oder mehrere Regionen bzw. einen oder mehrere Services möglich. Sie können Ihre {{site.data.keyword.deliverypipeline}} beispielsweise so einrichten, dass sie mindestens einen Service verwendet, in einer einzigen Region getestet oder und in mehreren Regionen für die Produktion bereitgestellt wird. Weitere Informationen hierzu finden Sie unter [Regionen](/docs/overview/whatisbluemix.html#ov_intro_reg).

Es gibt mehrere Möglichkeiten für die Erstellung einer Pipeline; dazu gehören das Hinzufügen einer Pipeline zu einer vorhandenen Anwendung sowie die Erstellung einer Pipeline ohne vorhandene Anwendung. Wenn Ihre Organisation noch keinen {{site.data.keyword.deliverypipeline}}-Service hat, können Sie den Katalog aufrufen und auf '{{site.data.keyword.deliverypipeline}}' sowie auf 'Erstellen' klicken.

Führen Sie diese Schritte aus, um eine {{site.data.keyword.deliverypipeline}} für eine vorhandene Anwendung einzurichten:    

1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Apps-Dashboard auf Ihre App.
1. Klicken Sie im 'Hamburger'-Menü in der {{site.data.keyword.Bluemix_notm}}-Menüleiste auf **Services** und dann auf **DevOps**.
1. Klicken Sie auf **Pipelines** und dann auf **Pipeline erstellen**.

Führen Sie zum [Erstellen einer Pipeline (Link wird in neuem Fenster geöffnet)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}, die für die Bereitstellung einer Cloud Foundry-Anwendung konfiguriert ist, die folgenden Schritte aus:    

1. Klicken Sie auf **Cloud Foundry**.  
1. Wenn Sie einen anderen Namen für die Pipeline verwenden möchten, ändern Sie den Standardnamen.  
1. Wenn Sie einen anderen Namen für die Anwendung verwenden möchten, ändern Sie den Standardnamen. Dieser Name ist der Name der Anwendung, in der die Bereitstellung durch die Pipeline erfolgt. 
1. Wenn Sie über keine Toolchain verfügen, wird eine Toolchain mit einem Standardnamen erstellt. Wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain. Durch die Integration anderer Tools und Services haben Sie mit der Toolchain die Möglichkeit, die Funktionalität Ihrer Pipeline zu erweitern.

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
1. Wenn Sie einen anderen Namen für die Pipeline verwenden möchten, ändern Sie den Standardnamen.  
1. Wenn Sie über keine Toolchain verfügen, wird eine Toolchain mit einem Standardnamen erstellt. Wenn Sie einen anderen Namen verwenden möchten, ändern Sie den Namen der Toolchain. Durch die Integration anderer Tools und Services haben Sie mit der Toolchain die Möglichkeit, die Funktionalität Ihrer Pipeline zu erweitern.
1. Wählen Sie entweder den Namen der gewünschten Toolchain aus oder geben Sie einen Namen für die neue Toolchain ein, die Sie erstellen möchten.
1. Klicken Sie auf **Erstellen**. Daraufhin wird eine leere Pipeline erstellt und auf der Übersichtsseite als Kachel dargestellt.

Auf der Kachel für {{site.data.keyword.deliverypipeline}} können Sie Ihre Konfiguration ändern, den Status von Builds, der bereitgestellten App und von kürzlich erfolgten Bereitstellungen überprüfen, die aktuellen Protokolle und Bereitstellungsdetails anzeigen und Ihre Pipeline löschen.  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks" role="article">
<h2 class="topictitle2" id="d68e338">Zugehörige Links</h2>
<aside role="complementary" aria-labelledby="related_links">
<div class="linklist" id="general"><h3 class="linklistlabel" id="related_links">Zugehörige Links</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(Wird auf einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">Voraussetzungen für {{site.data.keyword.Bluemix_notm}}</a></li>
<li><img src="./sout.gif" alt=""><a href="https://www.ibm.com/devops/method/content/deliver/practice_delivery_pipeline/" rel="external" title="(Wird auf einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">IBM Bluemix Garage-Methode: Delivery Pipeline</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">Lernprogramme und Beispiele</h3>
<ul>

<!--
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(Opens in a new tab or window)">Clone, edit, and deploy an app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Node.js app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Java app</a></li>
-->

<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(Wird auf einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">developerWorks: {{site.data.keyword.Bluemix_notm}}-Service {{site.data.keyword.deliverypipeline}}</a></li>
</ul>
</div>
</aside>
</article>
