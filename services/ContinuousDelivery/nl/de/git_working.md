---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:screen:.screen}
{:codeblock:.codeblock}

# Mit Git Repos and Issue Tracking arbeiten (Experimentell)
{: #git_working}

Arbeiten Sie mit Ihrem Team zusammen und verwalten Sie Ihren Quellcode mit einem Git-Repository- und Problemtracker, der von IBM gehostet wird und auf [GitLab Community Edition ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://about.gitlab.com/){:new_window} basiert.
{: shortdesc}

Die Git Repos and Issue Tracking-Toolintegration unterstützt Teams auf zahlreiche verschiedene Arten bei der Verwaltung von Code und der Zusammenarbeit: 
   * Verwalten Sie Git-Repositorys mittels differenzierter Zugriffssteuerungsmechanismen, durch die der Code geschützt bleibt
   * Überprüfen Sie den Code und verbessern Sie die Zusammenarbeit durch Zusammenführungsanforderungen (Merge)
   * Verfolgen Sie Probleme und teilen Sie Ihre Ideen durch den Tracker für Probleme mit anderen 
   * Dokumentieren Sie Projekte auf dem Wiki-System

**Hinweis:** Da diese Toolintegration auf GitLab Community Edition basiert und von IBM auf Bluemix gehostet wird, sind einige wenige GitLab-Optionen nicht verfügbar. Delivery Pipeline stellt zum Beispiel die kontinuierliche Integration und Continuous Delivery für Bluemix bereit. Aus diesem Grund werden die Features für die kontinuierliche Integration in GitLab nicht unterstützt. Außerdem stehen die Administratorfunktionen nicht zur Verfügung, denn ihre Verwaltung erfolgt durch IBM.

## Größenbegrenzung für Dateien und Repositorys
{: #git_limits}

Dateien sind grundsätzlich auf 100 MB begrenzt. Für Repositorys gilt eine Größenbegrenzung von 1 GB. Wenn Ihr Repository die Größe von 1 GB überschreitet, erhalten Sie unter Umständen eine E-Mail-Nachricht mit der Aufforderung, die Größe des Repositorys entsprechend zu reduzieren. 

## Persönliches Zugriffstoken oder SSH-Schlüssel für die Authentifizierung erstellen    
{: #git_authentication}

Zum Ausführen ferner Git-Operationen wie etwa `Klonen` oder `Push`-Operationen von Ihrem lokalen Git-Repository aus müssen Sie ein persönliches Zugriffstoken oder einen SSH-Schlüssel für die Authentifizierung bei GitLab verwenden. 

* Wie Sie ein persönliches Zugriffstoken einrichten, erfahren Sie in [Persönliche Zugriffstoken ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://git.ng.bluemix.net/help/api/README.html#personal-access-tokens){:new_window}.
* Wie Sie einen SSH-Schlüssel einrichten, können Sie in [SSH ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://git.ng.bluemix.net/help/ssh/README){:new_window} oder [Vorgehensweise zum Erstellen Ihrer SSH-Schlüssel ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://git.ng.bluemix.net/help/gitlab-basics/create-your-ssh-keys){:new_window} nachlesen. Wenn Sie mit SSH-Authentifizierung auf Ihre Repositorys zugreifen, sind gegebenenfalls weitere Konfigurationsschritte für Proxys und Firewalls erforderlich.

**Hinweis:** Damit Sie ein persönliches Zugriffstoken oder einen SSH-Schlüssel für die Authentifizierung verwenden können, müssen Sie Git lokal einrichten. Entsprechende Anweisungen enthält [Mit der Verwendung von Git in der Befehlszeile beginnen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://git.ng.bluemix.net/help/gitlab-basics/start-using-git){:new_window}. 
