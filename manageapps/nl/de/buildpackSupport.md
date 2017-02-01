---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Buildpack-Support-Anweisung
{: #buildpack_support_statement}


## Integrierte IBM-Buildpacks
{: #built-in_ibm_buildpacks}

Für [Liberty for Java](/docs/runtimes/liberty/index.html), [SDK for Node.js](/docs/runtimes/nodejs/index.html) und [ASP.NET Core](/docs/runtimes/dotnet/index.html) unterstützt IBM zwei Versionen (n & n - 1), z. B. IBM Liberty Buildpack Version 1.22 & IBM Liberty Buildpack Version 1.21. Jedes Buildpack bietet und unterstützt eine oder mehrere Hauptversionen der entsprechenden Laufzeit, z. B. IBM SDK, Java Technology Edition Version 7 Release 1 und Version 8. Buildpacks werden normalerweise einmal im Monat mit der neuesten verfügbaren Nebenversion aktualisiert.

Für [IBM Bluemix Runtime for Swift](/docs/runtimes/swift/index.html) unterstützt IBM den Buildpack für die aktuelle Version von Swift, verfügbar unter [Swift.org](http://swift.org). Aktualisierungen des Buildpacks werden mit der neuesten verfügbaren freigegebenen Version von Swift synchronisiert sein.

Probleme können für jede Version des integrierten IBM Buildpacks, das unter {{site.data.keyword.Bluemix_notm}} unterstützt wird, gemeldet werden. Sie müssen jedoch mit der neuesten Version abgeglichen werden. Wenn ein Fehler gefunden wird, stellt IBM ein Fix in der nächsten Version der Laufzeit und des entsprechenden Buildpacks bereit. IBM stellt keine Fixes für ältere Hauptversionen oder für Nebenversionen (N-1, n-1) bereit. IBM stellt keinen Support für Community-Laufzeiten bereit, auch wenn IBM Buildpacks verwendet werden, z. B. Open JDK mit dem Liberty-Buildpack. Diese Community-Laufzeiten halten dieselbe Support-Richtlinie ein, siehe dazu auch "Integrierte Community-Buildpacks".

## Integrierte Community-Buildpacks
{: #built-in_community_buildpacks}

Die folgenden integrierten Community-Buildpacks werden von der Cloud Foundry-Community bereitgestellt:

* [Java](/docs/runtimes/tomcat/index.html)
* [Node.js](https://github.com/cloudfoundry/nodejs-buildpack)
* [PHP](/docs/runtimes/php/index.html)
* [Ruby](/docs/runtimes/ruby/index.html)
* [Python](/docs/runtimes/python/index.html)
* [Go](/docs/runtimes/go/index.html)

Aktualisierungen an diesen Buildpacks erfolgen, wenn {{site.data.keyword.Bluemix_notm}} auf eine neue Version von Cloud Foundry aktualisiert wird. Probleme mit diesen Laufzeiten unter {{site.data.keyword.Bluemix_notm}} können IBM gemeldet werden. IBM bietet Unterstützung an, um festzustellen, ob {{site.data.keyword.Bluemix_notm}} die Ursache des Problems ist. Bei Problemen im Zusammenhang mit {{site.data.keyword.Bluemix_notm}} stellt IBM einen Fix bereit. Bei Fehlern im Buildpack oder in der Laufzeit selbst bietet IBM Unterstützung an, um die Fehler in der entsprechenden Community zu melden. IBM stellt keine Fixes für diese Buildpacks und Laufzeiten bereit.

## Externe Buildpacks
{: #external_buildpacks}


IBM bietet keinen Support für externe Buildpacks an. Wenden Sie sich an die Cloud Foundry-Community, um Unterstützung zu erhalten.
