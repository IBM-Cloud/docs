---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

*Letzte Aktualisierung: 23. März 2016*

Die Liberty for Java-Anwendungen in {{site.data.keyword.Bluemix}} basieren auf dem Buildpack 'liberty-for-java'. Mit dem Buildpack 'liberty-for-java' wird eine vollständige Laufzeitumgebung zum Ausführen von Java EE 7- und OSGi-Anwendungen auf einem Liberty-Profil bereitgestellt. Es unterstützt gängige Frameworks wie Spring und umfasst die IBM JRE. WebSphere Liberty ermöglicht eine zeiteffiziente Anwendungsentwicklung, die optimal an die Cloud angepasst ist.
{: shortdesc}

## Erkennung
{: #detection}
Das Liberty-Buildpack wird verwendet, wenn folgende Anwendungsarten bereitgestellt werden:
* [WAR-Dateien](optionsForPushing.html#stand_alone_apps)
* [EAR-Dateien](optionsForPushing.html#stand_alone_apps)
* [Liberty-Serververzeichnis](optionsForPushing.html#server_directory)
* [Paketierter Liberty-Server](optionsForPushing.html#packaged_server)
* Main-Methode von Java
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## Starteranwendung
{: #starter_application}
{{site.data.keyword.Bluemix}} stellt mehrere Liberty-Starteranwendungen bereit.  Die Liberty-Starteranwendungen sind einfache Liberty-Apps, die Sie als Schablone verwenden können. Sie können mit den Starter-Apps experimentieren, Änderungen an der Bluemix-Umgebung vornehmen und diese mit einer Push-Operation übertragen.  Hilfe zur Verwendung der Starteranwendungen finden Sie in [Starteranwendungen verwenden](../../cfapps/starter_app_usage.html).

# Zugehörige Links
## Allgemein
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
* [Liberty-Apps verwalten](../../manageapps/app_mng.html#Utilities)
* [Bereitstellung von Apps mit IBM Eclipse Tools for Bluemix](../../manageapps/eclipsetools/eclipsetools.html#eclipsetools)
* [Erste Schritte mit dem Service IBM Monitoring and Analytics für Bluemix](../../services/monana/index.html#monana_oview)
## Beispiele
* [Cloud Foundry Architecture Labs](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/)
