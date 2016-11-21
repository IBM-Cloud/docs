---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Buildpack-Support-Anweisung
{: #buildpack_support_statement}

Letzte Aktualisierung: 8. September 2016
{: .last-updated}

## Integrierte IBM-Buildpacks
{: #built-in_ibm_buildpacks}

* [Liberty for Java](../runtimes/liberty/index.html)
* [SDK for Node.js](../runtimes/nodejs/index.html)
* [ASP.NET Core](../runtimes/dotnet/index.html)

IBM unterstützt zwei Versionen (n & n - 1) jedes Laufzeit-Buildpacks, das für Bluemix bereitgestellt wird (d. h. IBM Liberty Buildpack v1.22 & IBM Liberty Buildpack v1.21). Jedes Buildpack bietet und unterstützt eine oder mehrere Hauptversionen der entsprechenden Laufzeit (d. h. IBM SDK, Java Technology Edition Version 7 Release 1 und Version 8). Buildpacks werden in der Regel alle zwei Wochen mit der aktuellen Nebenversion der verfügbaren Laufzeit aktualisiert. Die oben genannte Richtlinie stellt sicher, dass jede bereitgestellte Laufzeitversion mindestens 1 Monat ab Bereitstellungdatum unterstützt wird.

Probleme können für jede Version des integrierten IBM Buildpacks, das unter Bluemix unterstützt wird, gemeldet werden. Sie müssen jedoch mit der neuesten Version verglichen werden. Wenn ein Fehler gefunden wird, stellt IBM ein Fix in der nächsten Version der Laufzeit und des entsprechenden Buildpacks bereit. IBM stellt keine Fixes für ältere Hauptversionen oder für Nebenversionen (N-1, n-1) bereit. IBM stellt keinen Support für Community-Laufzeiten bereit, auch wenn IBM Buildpacks verwendet werden, z. B. Open JDK mit dem Liberty-Buildpack. Diese Community-Laufzeiten halten dieselbe Support-Richtlinie ein, siehe dazu auch "Integrierte Community-Buildpacks".

## Integrierte Community-Buildpacks
{: #built-in_community_buildpacks}

Die folgenden integrierten Community-Buildpacks werden von der Cloud Foundry-Community bereitgestellt:

* [Java](../runtimes/tomcat/index.html)
* [Node.js](https://github.com/cloudfoundry/nodejs-buildpack)
* [PHP](../runtimes/php/index.html)
* [Ruby](../runtimes/ruby/index.html)
* [Python](../runtimes/python/index.html)
* [Go](../runtimes/go/index.html)

Updates dieser Buildpack erfolgen, wenn Bluemix auf eine neue Version von Cloud Foundry aktualisiert wird. Probleme mit diesen Laufzeiten unter Bluemix können IBM gemeldet werden. IBM bietet Unterstützung an, um festzustellen, ob Bluemix die Ursache des Problems ist. Bei Problemen in Bezug auf Bluemix stellt IBM einen Fix bereit. Bei Fehler im Buildpack oder in der Laufzeit selbst bietet IBM Unterstützung an, die Fehler in der entsprechenden Community zu melden. IBM stellt keine Fixes für diese Buildpacks und Laufzeiten bereit.

## Externe Buildpacks
{: #external_buildpacks}


IBM bietet keinen Support für externe Buildpacks an. Wenden Sie sich an die Cloud Foundry-Community, um Unterstützung zu erhalten. 


