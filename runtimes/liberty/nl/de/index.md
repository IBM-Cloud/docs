---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

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
{{site.data.keyword.Bluemix}} stellt mehrere Liberty-Starteranwendungen bereit.  Die Liberty-Starteranwendungen sind einfache Liberty-Apps, die Sie als Schablone verwenden können. Sie können mit den Starter-Apps experimentieren, Änderungen an der Bluemix-Umgebung vornehmen und diese mit einer Push-Operation übertragen.  Hilfe zur Verwendung der Starteranwendungen finden Sie in [Starteranwendungen verwenden](/docs/cfapps/starter_app_usage.html).

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
* [Liberty-Apps verwalten](/docs/manageapps/app_mng.html#Utilities)
* [Bereitstellung von Apps mit IBM Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools)
* [Erste Schritte mit dem Service IBM Monitoring and Analytics für Bluemix](/docs/services/monana/index.html#monana_oview)

