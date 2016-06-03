---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:new_window: target="_blank"}

#Anwendungen entwickeln 
{: #develop-apps-IDS}

*Letzte Aktualisierung: 7. Dezember 2015*  

Sie können Anwendungen in einer integrierten Entwicklungsumgebung (Integrated Development Environment, IDE) oder einem Texteditor entwickeln oder auch {{site.data.keyword.jazzhub}} verwenden. 
{: shortdesc}

##Anwendungen mit Bluemix DevOps Services entwickeln
{: #dev_ops}

Mit {{site.data.keyword.jazzhub_short}} können Sie eine Anwendung in der Cloud entwickeln, verfolgen und planen und diese dann in {{site.data.keyword.Bluemix_notm}} bereitstellen. Sie können innerhalb von Minuten aus einem Quellcode eine aktive Anwendung erhalten.  

{{site.data.keyword.jazzhub_short}} stellt zwei Services bereit: {{site.data.keyword.trackplan}} und {{site.data.keyword.deliverypipeline}}. Der {{site.data.keyword.trackplan}}-Service
wird für agiles Planen verwendet. Mit dem {{site.data.keyword.deliverypipeline}}-Service werden Builds und Bereitstellungen automatisiert. Diese Services finden Sie im {{site.data.keyword.Bluemix_notm}}-Katalog. Weitere Informationen zur Verwendung dieser Services finden Sie unter [Einführung in Track & Plan](../services/TrackPlan/index.html#gettingstartedtemplate) und [Einführung in Delivery Pipeline](../services/DeliveryPipeline/index.html#getstartwithCD). 

{{site.data.keyword.jazzhub_short}} stellt außerdem Git-Hosting für die Quellcodeverwaltung sowie eine Web-IDE zur Verfügung, in der Sie den Code bearbeiten, verwalten und bereitstellen können. In einer App aktivieren Sie Git-Hosting durch Klicken auf den Link **Git hinzufügen**, der sich in der rechten oberen Ecke der Übersichtsseite der App befindet. Sie können dann den Code der App in der Web-IDE bearbeiten, indem Sie auf **Code bearbeiten** klicken. Über die
Web-IDE-Shell können Sie 'cf'-Befehle mit Content-Assist
ausführen. Sie können beispielsweise eine Liste aller Cloud Foundry-Befehle abrufen, indem Sie den folgenden
Befehl eingeben:  
```
help cfo
```
{:pre}
