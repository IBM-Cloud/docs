{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

#Einführung in {{site.data.keyword.deliverypipeline}} {: #delivery-pipeline}  

*Letzte Aktualisierung: 21. Januar 2016*

Um Ihre Builds und Bereitstellungen für {{site.data.keyword.Bluemix}} zu automatisieren, verwenden Sie IBM Continuous {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}} (Service {{site.data.keyword.deliverypipeline}}).
{: shortdesc} 

Beim Entwickeln einer App in der Cloud können Sie aus mehreren Buildtypen wählen. Sie stellen das Build-Script bereit und {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} führt es aus. Es müssen keine Buildsysteme eingerichtet werden. Anschließend können Sie mit einem einzigen Mausklick Ihre App automatisch in einem oder mehreren {{site.data.keyword.Bluemix_notm}}-Bereichen, auf öffentlichen Cloud Foundry-Servern oder Docker-Containern in IBM Containers for {{site.data.keyword.Bluemix_notm}} bereitstellen.  

Über Build-Jobs wird Ihr App-Quellcode aus Git- oder Jazz-Quellcodeverwaltungsrepositorys heraus kompiliert und paketiert. Bei den Build-Jobs werden bereitstellbare Artefakte wie WAR-Dateien oder Docker-Container für IBM Containers erstellt. Sie können außerdem innerhalb Ihres Builds automatisch Komponententests ausführen. Mit jeder Änderung am Quellcode wird ein Build ausgelöst.  

Ein Bereitstellungsjob erhält Output von einem Build-Job und stellt ihn entweder IBM Containers oder Cloud Foundry-Servern bereit, z. B. {{site.data.keyword.Bluemix_notm}}.  

Es ist eine Bereitstellung für eine oder mehrere Regionen bzw. einen oder mehrere Services möglich. Sie können beispielsweise Ihren {{site.data.keyword.deliverypipeline}}-Service so einrichten, dass Entwicklungsartefakte IBM Containers nutzen, in einer einzigen Region getestet werden und in mehreren Regionen für die Produktion bereitgestellt werden. Weitere Informationen hierzu finden Sie unter [Regionen](../../overview/index.html#ov_intro__reg).

1. Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an und wählen Sie für Ihre App eine Organisation und einen Bereich aus.
1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf die Option zum Erstellen einer App.
1. Wählen Sie eine Vorlage für eine Web-App oder eine mobile App sowie einen Starter aus und klicken Sie auf die Option zum Fortfahren. Geben Sie der App einen Namen und klicken Sie anschließend auf die Option zum Fertigstellen.  
1. Blättern Sie auf der Seite 'Coding beginnen' abwärts und klicken Sie auf **App-Übersicht anzeigen**.  
1. Erstellen Sie im {{site.data.keyword.Bluemix_notm}}-App-Dashboard ein Git-gehostetes Projekt für die App, indem Sie auf **Git hinzufügen** klicken. Stellen Sie sicher, dass das Kontrollkästchen **Das Repository mit dem Starter-App-Paket füllen und {{site.data.keyword.deliverypipeline}} aktivieren (Erstellen & Bereitstellen)** ausgewählt ist, und klicken Sie anschließend auf **Weiter**.   
1. Klicken Sie nach der Erstellung des Git-Repositorys auf **Schließen**. Der Link 'Git hinzufügen' wird durch den Link 'Code bearbeiten' und Ihre Git-URL ersetzt.  
1. Fügen Sie den {{site.data.keyword.deliverypipeline}}-Service zu dem zugehörigen Bereich bzw. den zugehörigen Bereichen hinzu. Nach dem Hinzufügen dieses Service können Sie eine mehrphasige Bereitstellungspipeline in Ihren {{site.data.keyword.Bluemix_notm}}-Bereichen erstellen, indem Sie Stages mit Build-, Test- und Bereitstellungsjobs konfigurieren und ausführen.
    1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-App-Dashboard auf **Service oder API hinzufügen**. Wählen Sie für die Kategorie das Kontrollkästchen **DevOps** aus und klicken Sie im Katalog auf **Delivery Pipeline**.
    2. Wählen Sie einen Plan aus und klicken Sie auf **Erstellen**. Das {{site.data.keyword.deliverypipeline}}-Dashboard wird geöffnet und es wird die App angezeigt, die Sie vorher erstellt haben.     
  
Im {{site.data.keyword.deliverypipeline}}-Dashboard sehen Sie Ihre {{site.data.keyword.jazzhub_short}}-Projekte
sowie die Status, in denen sie sich befinden. Sie können den Status von Builds, der bereitgestellten App und kürzlich erfolgten Bereitstellungen überprüfen oder auch die aktuellen Protokolle und Bereitstellungsdetails anzeigen.  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="de-de" id="rellinks">
<h2 class="topictitle2" id="d68e338">Zugehörige Links</h2>
<aside>
<div class="linklist" id="general"><h3 class="linklistlabel">Zugehörige Links</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(Wird auf einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">Voraussetzungen für {{site.data.keyword.Bluemix_notm}}</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">Lerntexte und Beispiele</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(Wird auf einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">Apps klonen, bearbeiten und bereitstellen</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(Wird auf einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">Node.js-App entwickeln und bereitstellen</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(Wird auf einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">Java-App entwickeln und bereitstellen</a></li>
<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(Wird auf einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">developerWorks: {{site.data.keyword.Bluemix_notm}}-Service {{site.data.keyword.deliverypipeline}}</a></li>
</ul>
</div>
</aside>
</article>
