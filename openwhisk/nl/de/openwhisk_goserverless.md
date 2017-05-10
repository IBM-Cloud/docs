---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# OpenWhisk-Integration in Serverless Framework
{: #openwhisk_goserverless}

[Serverless Framework](https://serverless.com/) ist ein quelloffenes Framework zur Erstellung von serverunabhängigen Anwendungen. Mit einer einfachen Manifestdatei können Entwickler serverunabhängige Funktionen definieren, diese mit Ereignisquellen verbinden und Cloud-Services deklarieren, die von ihrer Anwendung benötigt werden. Das Framework sorgt für die Bereitstellung dieser serverunabhängigen Anwendungen für Cloud-Provider. Es bietet Entwicklern die Möglichkeit, Services in der Produktion zu überwachen, Aktualisierungen zu implementieren und das Debugging von Problemen zu unterstützen. Es verfügt darüber hinaus über ein sehr aktives Drittanbieterumfeld, das den Funktionsumfang des Frameworks durch Plug-ins erweitert. An diesem Punkt kommt OpenWhisk ins Spiel. 
{:shortdesc}

OpenWhisk besitzt ein [eigenes Provider-Plug-in für Serverless Framework](https://github.com/serverless/serverless-openwhisk). Entwickler, die Serverless Framework nutzen, können ihre Anwendungen auf einer beliebigen OpenWhisk-Plattforminstanz (in Bluemix gehostete Instanz, Cloud-Instanz oder private Instanz) bereitstellen. Die Unterstützung durch unterschiedliche Provider (Multi-Provider-Support) bedeutet zudem, dass das Verlagern von Anwendungen zwischen Plattformen wesentlich leichter ist und dass Entwickler serverunabhängige Multi-Cloud-Anwendungen entwickeln können.

## Einführung
{: #openwhisk_goserverless_starting}

Die offizielle Einführung in Serverless Framework finden Sie in folgender Veröffentlichung: [Einführung für OpenWhisk](https://serverless.com/framework/docs/providers/openwhisk/guide/intro/) (in englischer Sprache). Diese Einführung behandelt die Installation, den Entwicklungsworkflow und bewährte Verfahren und bietet u. a. eine schrittweise Anleitung zur Erstellung und Bereitstellung einer funktionierenden OpenWhisk-Anwendung.

[Dieses Video](https://youtu.be/GJY10W98Itc) erläutert die Verwendung von Serverless Framework mit dem OpenWhisk-Provider-Plug-in.
## Dokumentation
{: #openwhisk_goserverless_docs}

Die aktuellste Dokumentation zur Verwendung von OpenWhisk mit Serverless Framework [finden Sie hier](https://serverless.com/framework/docs/providers/openwhisk/).
## Beispiele
{: #openwhisk_goserverless_samples}
[Im GitHub-Repository für Serverless Framework-Beispiele](https://github.com/serverless/examples) finden Sie jetzt OpenWhisk mit Anleitungen zum Erstellen von HTTP-APIs, Cron-basierten Schedulern, Verkettungsfunktionen und vieles mehr.
