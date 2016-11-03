---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# Einführung in {{site.data.keyword.deliverypipeline}} {: #delivery-pipeline}  

Letzte Aktualisierung: 15. September 2016
{: .last-updated}

Um Ihre Builds und Bereitstellungen für {{site.data.keyword.Bluemix}} zu automatisieren, verwenden Sie IBM Continuous {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Diese Informationen gelten sowohl für {{site.data.keyword.deliverypipeline}} als auch für {{site.data.keyword.deliverypipeline}} Next.

Beim {{site.data.keyword.deliverypipeline}}-Service können Sie unter verschiedenen Buildtypen auswählen. Sie stellen das Build-Script bereit und {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} führt es aus. Es müssen keine Buildsysteme eingerichtet werden. Anschließend können Sie mit einem einzigen Mausklick Ihre App automatisch in einem oder mehreren {{site.data.keyword.Bluemix_notm}}-Bereichen, auf öffentlichen Cloud Foundry-Servern oder Docker-Containern in IBM Containers for {{site.data.keyword.Bluemix_notm}} bereitstellen.  

Über Build-Jobs wird Ihr App-Quellcode aus Git- oder Jazz-Quellcodeverwaltungsrepositorys heraus kompiliert und paketiert. Bei den Build-Jobs werden bereitstellbare Artefakte wie WAR-Dateien oder Docker-Container für IBM Containers erstellt. Sie können außerdem innerhalb Ihres Builds automatisch Komponententests ausführen. Mit jeder Änderung am Quellcode wird ein Build ausgelöst.

Ein Bereitstellungsjob erhält Output von einem Build-Job und stellt ihn entweder IBM Containers oder Cloud Foundry-Servern bereit, z. B. {{site.data.keyword.Bluemix_notm}}.  

Es ist eine Bereitstellung für eine oder mehrere Regionen bzw. einen oder mehrere Services möglich. Sie können beispielsweise Ihren {{site.data.keyword.deliverypipeline}}-Service so einrichten, dass Entwicklungsartefakte IBM Containers nutzen, in einer einzigen Region getestet werden und in mehreren Regionen für die Produktion bereitgestellt werden. Weitere Informationen hierzu finden Sie unter [Regionen](../../overview/index.html#ov_intro__reg).

Es gibt mehrere Möglichkeiten für die Erstellung einer Pipeline; dazu gehören das Hinzufügen einer Pipeline zu einer vorhandenen Anwendung sowie die Erstellung einer Pipeline ohne vorhandene Anwendung. Wenn Sie in Ihrer Organisation noch keinen {{site.data.keyword.deliverypipeline}}-Service haben, können Sie den Katalog aufrufen und auf {{site.data.keyword.deliverypipeline}} oder {{site.data.keyword.deliverypipeline}} Next sowie auf 'Erstellen' klicken.

Führen Sie diese Schritte aus, um eine {{site.data.keyword.deliverypipeline}} für eine vorhandene Anwendung einzurichten:    

1. Erstellen Sie im {{site.data.keyword.Bluemix_notm}}-App-Dashboard auf der Registerkarte 'Übersicht' unter **Continuous Delivery** ein Git-gehostetes Projekt für die App, indem Sie je nach Kontext auf **Pipeline und Git-Repository hinzufügen** oder auf **Git hinzufügen** klicken.
1. Stellen Sie sicher, dass das Kontrollkästchen **Füllen Sie das Repository mit dem Paket mit der Lösung für den komfortablen Schnelleinstieg und aktivieren Sie die Pipeline von Build & Deploy** ausgewählt ist und klicken Sie dann auf **Weiter**. Möglicherweise müssen Sie Ihre E-Mail-Adresse bestätigen, um fortzufahren.  
1. Klicken Sie nach der Erstellung des Git-Repositorys auf **Schließen**. Die Schaltfläche 'Git hinzufügen' wird durch die Schaltfläche 'Code bearbeiten' und Ihre Git-URL ersetzt.  
1. Klicken Sie auf **Code bearbeiten**, um die Pipeline zu öffnen, und klicken Sie anschließend auf **Build & Deploy**. Um die Pipeline das erste Mal auszuführen, führen Sie am Git-Repository eine Änderung mit der Push-Operation durch.

Nach dem Hinzufügen dieses Service können Sie eine mehrphasige Bereitstellungspipeline in Ihren {{site.data.keyword.Bluemix_notm}}-Bereichen erstellen, indem Sie Phasen mit Build-, Test- und Bereitstellungsjobs konfigurieren und ausführen. Im {{site.data.keyword.deliverypipeline}}-Dashboard sehen Sie Ihre {{site.data.keyword.jazzhub_short}}-Projekte
sowie die Status, in denen sie sich befinden. Sie können den Status von Builds, der bereitgestellten App und kürzlich erfolgten Bereitstellungen überprüfen oder auch die aktuellen Protokolle und Bereitstellungsdetails anzeigen.  

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
<h3 class="linklistlabel">Lerntexte und Beispiele</h3>
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
