---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Neueste Aktualisierungen für das Buildpack 'sdk-for-nodejs'
{: #latest_updates}

*Letzte Aktualisierung: 22. März 2016*

Eine Liste mit den neuesten Aktualisierungen im Buildpack 'sdk-for-nodejs'.
## 29. April 2016: Node.js Buildpack v3.3-20160418-1749 aktualisiert

Mit diesem Release des Buildpacks werden die IBM SDK for Node.js-Laufzeitversionen 0.10.44, 0.12.13, 4.4.1 und 4.4.2 hinzugefügt. Die Standardversion ist jetzt 4.4.2. Es wurden außerdem mehrere ältere Versionen der IBM SDK for Node.js-Laufzeit entfernt. Das Buildpack enthält nun die beiden neuesten Versionen von 0.10.x, 0.12.x und 4.x; momentan sind dies 0.10.43, 0.10.44, 0.12.12, 0.12.13, 4.4.1 und 4.4.2.

Bei 4.4.1 und 4.4.2 ist es nun möglich, eine FIPS-kompatible Version der Laufzeit zu verwenden; hierfür müssen Sie die Umgebungsvariable `FIPS_MODE=true` für Ihre App festlegen. Suchen Sie dann in der Staging-Ausgabe nach `FIPS_MODE`, um die Erkennung durch das Buildpack zu bestätigen.

Das aktualisierte Buildpack und die neuen Laufzeitversionen enthalten außerdem Fixes für Sicherheitslücken:
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

Das aktualisierte Buildpack enthält auch Fixes für zwei Programmfehler:
* IBM SDK for Node.js-Builds werden jetzt immer verwendet, sobald einer für den Abgleich mit dem angeforderten Bereich verfügbar ist. Früher galt dies nur für 4.x-Laufzeitversionen.
* Das Dienstprogramm 'Inspector' von App Management funktioniert nun mit 4.x-Laufzeitversionen.

## 18. März 2016: Node.js-Buildpack v3.2-20160315-1257 aktualisiert

Mit diesem Release des Buildpacks wird die standardmäßige IBM SDK for Node.js-Laufzeit von Version 4.3.0 in 4.3.2 verschoben. IBM SDK for Node.js in den Versionen 0.10.43, 0.12.12 und 4.3.1 ist ebenfalls enthalten. Benutzer sollten diese letzten Node.js-Versionen verwenden, um ihnen Fixes für einige Sicherheitslücken zu entnehmen.

## 4. März 2016: Node.js-Buildpack v3.1-20160222-1123 aktualisiert

Mit diesem Release des Buildpacks wird die standardmäßige IBM SDK for Node.js-Laufzeit von Version 4.2.4 in 4.3.0 verschoben. IBM SDK for Node.js in den Versionen 0.10.42, 0.12.10 und 4.2.6 ist ebenfalls enthalten. Benutzer sollten diese letzten Node.js-Versionen verwenden, um ihnen Fixes für einige Sicherheitslücken zu entnehmen.

## 4. Februar 2016: Node.js-Buildpack v3.0-20160125-1224 aktualisiert

Dieses Release ist vollständig mit dem [Node.js-Buildpack der Cloud Foundry-Community](https://github.com/cloudfoundry/nodejs-buildpack) synchronisiert. Zusätzlich zu Änderungen der Community gibt es Änderungen an bestimmten Standardwerten, Optimierungen zum Reduzieren der für das Staging erforderlichen Zeit und Aktualisierungen für das Feature 'App-Management'.

* Buildpack-Aktualisierungen:

  * Node.js v4.2.4 (IBM SDK for Node.js Version 4) ist nun die Standardlaufzeit in Bluemix und ersetzt v0.12.9. Dies kann dazu führen, dass Ihre Anwendung ein anderes Verhalten zeigt, wenn Sie für Ihre Anwendung nicht eine bestimmte Version angegeben haben. Lesen Sie die Dokumentation zur [Node.js-Laufzeit](index.html), um zu erfahren, wie für Ihre Bluemix-Anwendung eine bestimmte Version von Node.js angegeben wird.

  * Für NODE_ENV ist nun standardmäßig die Einstellung *production* festgelegt. Dies führt zu einem geänderten Verhalten einiger Knotenabhängigkeiten. Beispielsweise gibt das Express-Framework im Web-Browser für fehlerhafte Endpunkte keine Stack-Traces mehr zurück, sondern zeigt stattdessen nur *Internal Server Error* (Interner Serverfehler) an. Wenn für NPM_CONFIG_PRODUCTION die Einstellung *true* festgelegt ist, legt NPM für NODE_ENV die Einstellung *production* nur für Subshell-Scripts in der Installationsphase für 'npm' fest. Dadurch können Benutzer für NODE_ENV einen anderen Wert wie beispielsweise *development* als Anwendungslaufzeit festlegen. Für die Übersichtlichkeit erkennen npm-Scripts die Nachricht **NODE_ENV=production**.

  * Eine Fehlerkorrektur für den Service 'Monitoring and Analytics' ist enthalten.

* Cacheaktualisierungen:

  * Wenn der Cache inaktiviert ist (NODE_MODULES_CACHE=false), startet das Buildpack nicht den Versuch, Module oder Komponenten in den Cache zu stellen. Zuvor hat diese Einstellung bewirkt, dass der Cache nicht abgerufen wurde, die installierten Module jedoch für zukünftige Implementierungen in den Cache gestellt wurden. Nun wird der Cache nicht abgerufen und es wird auch nicht mehr versucht, einen Cache zu speichern.

  * Bower-Komponenten (bower-components) werden standardmäßig zusätzlich zu Knotenmodulen (node_modules) in den Cache gestellt.

* Andere Aktualisierungen:

  * Für fehlende Abhängigkeiten wurden hilfreiche Warnungen wie beispielsweise 'gulp', 'bower' und 'angular' hinzugefügt.

  * Das Erkennungsscript wird mit Informationen zur Buildpackversion aktualisiert.

  * Die ursprünglich von der Community eingeführte Clusteringempfehlung (WEB_CONCURRENCY) wurde entfernt, da die Speicherfeststellung für Bluemix falsch war.


## 16. Dezember 2015: Node.js-Buildpack v2.8-20151209-1403 und v3.0beta-20151211-2041 aktualisiert

Dieses Release des Buildpacks für Node.js steht in zwei Versionen zur Verfügung: v2.8 und v3.0beta. Beide Versionen enthalten folgende Änderungen:

Eine Fehlerkorrektur für den Service 'Monitoring and Analytics'. Die Einbeziehung einer im Cache gespeicherten Laufzeit für IBM SDK for Node.js v4.2.3.0, v4.2.2.0, v1.2.0.8 und v1.2.0.7 (auf der Basis der entsprechenden Node.js-Versionen v4.2.3, v4.2.2, v0.12.9 und v0.12.8 der Community). Zusätzlich wurde in v3.0beta die Node.js-Standardlaufzeit in v4.2.3 geändert.

Das Buildpack für IBM Node.js v3.0beta wurde als nicht standardmäßiges Buildpack für Bluemix mit Node.js v4.2.3 als Standardlaufzeit freigegeben. Führen Sie für Ihre Anwendung eine Push-Operation mit der Betaversion des Buildpacks durch, um sicherzustellen, dass Ihre Apps und Services weiterhin in Bluemix ausgeführt werden. Nach mindestens 30 Tagen wird Version 3 das Standardbuildpack.

Gehen Sie wie folgt vor, um für Ihre Anwendung eine Push-Operation mit v3.0beta durchzuführen:
* Verwenden Sie in Ihrem Befehl 'cf push' die Option '-b':

```
        cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}

* Verwenden Sie alternativ die Option 'buildpack' in Ihrer Datei 'manifest.yml':

```
        buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

Diese Änderung der Standardlaufzeit hat keine Auswirkung auf Ihre Anwendung, wenn Sie in Ihrem Anwendungspaket eine bestimmte Version von Node.js konfiguriert haben. Beachten Sie, dass Sie stets die zum Ausführen Ihrer Anwendung verwendete Node.js-Version angeben können, indem Sie den Eintrag 'engines.node' in Ihrer Datei 'package.json' wie in [Verfügbare Versionen](index.html#available_versions) erläutert verwenden.

## 23. November 2015: Node.js-Buildpack v2.7-20151118-1003 aktualisiert

In 2.7 wurde Version 4.2.1.0 von IBM SDK for Node.js (basiert auf Node v4.2.1 LTS) integriert. Dies ist noch nicht die Standardeinstellung, sie kann aber für die Verwendung angegeben werden. Beachten Sie, dass dadurch die zuvor verfügbare Open-Source-Erstellung ersetzt wird. Es wurden auch einige kleinere Fehlerkorrekturen am Framework für Serviceerweiterungen vorgenommen.

## 19. Oktober 2015: Node.js-Buildpack v2.6.1-20151015-1326 aktualisiert

In Node.js v2.6.1 wird eine Fehlerkorrektur für den [StrongPM-App-Management-Handler](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/) und eine konsistentere Version von NPM eingeführt.

## 15. Oktober 2015: Node.js-Buildpack v2.6-20151006-1309 aktualisiert

In diesem Release des Node.js-Buildpacks wurde [StrongLoop Process Manager](https://strong-pm.io) in das Feature 'App-Management' integriert. Weitere Informationen finden Sie im Blogbeitrag [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/).

## 15. Juni 2015: Node.js-Buildpack v2.0-20150608-1503 aktualisiert

In diesem Release wurde das Node.js-Buildpack mit dem neuesten [Node.js-Buildpack der CF-Community](https://github.com/cloudfoundry/nodejs-buildpack) synchronisiert, das mit einer Reihe neuer Features der Community ausgestattet ist.
Darüber hinaus wurde das Feature 'App-Management' im Node.js-Buildpack umgestaltet, wodurch die Verwendung von Dienstprogrammen wie 'shell', 'node-inspector', 'Bluemix Live Sync' und weiteren ermöglicht wurde. Details finden Sie in [App-Management](../../manageapps/app_mng.html).

## 5. Mai 2015: Node.js-Buildpack v1.17-20150429-1033 aktualisiert

* Das Node.js-Buildpack wird nun mit [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/) geliefert.
* Wenn Ihre Anwendung in der zugehörigen Datei 'package.json' keine Laufzeit angibt, verwendet Ihre App ab sofort Version 0.12.1 statt Version 0.10.x. Wenn Sie die vorherige Version verwenden müssen, geben Sie in der zugehörigen Datei 'package.json' wie unten gezeigt 'v0.10.x' an.

```
        "engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* Es gibt mit Version 0.12.1 bekannte Probleme:
   * Bei Verwendung des von Bluemix Live Sync bereitgestellten Features 'Debug Tool' funktioniert die Funktion 'Suspend' nicht.
   * Das für den Service MQ Light verwendete Modul 'mqlight' wird in Version 0.12.x nicht unterstützt.

* Eine Reihe von Sicherheitslücken wurden behoben:
  * Sicherheitslücken in OpenSSL, die sich auf IBM SDK for Node.js auswirkten, wurden behoben. Weitere Details finden Sie im [Sicherheitsbulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21701494).
  * Sicherheitslücke in RC4 Stream Cipher, die sich auf IBM SDK for Node.js auswirkte, wurde behoben. Weitere Details finden Sie im [Sicherheitsbulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21882778).

##  2. April 2015: Node.js-Buildpack v1.15-20150331-2231 aktualisiert

* Das Node.js-Buildpack enthält nun drei neue Features, um in Bluemix ohne erneute Implementierung eine ähnlich schnelle Entwicklung wie auf einem Desktop zu erreichen.
  * Desktop Sync: Synchronisieren Sie eine beliebige Desktop-Baumstruktur (Windows) mit einem cloudbasierten Projektarbeitsbereich.
  * Live Edit: Sie können Änderungen an einer in Bluemix ausgeführten Node.js-Anwendung vornehmen und sie sofort in Ihrem Browser testen.
  * Debug: Führen Sie in Ihrer Umgebung eine Shell-Operation und anschließend ein Debug durch! Mithilfe des Debuggers 'Node Inspector' können Sie Code dynamisch bearbeiten, Unterbrechungspunkte einfügen, Code schrittweise durchgehen, die Laufzeit erneut starten und mehr.
  * Weitere Informationen finden Sie in [App-Management](../../manageapps/app_mng.html#Utilities).
* Die neuesten Änderungen aus dem [Node.js-Buildpack von Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack) wurden einbezogen. Dieses Buildpack enthält eine Reihe von Fehlerkorrekturen und von der Community vorgenommenen Verbesserungen.
* Das Node.js-Buildpack enthält nun [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/).

## 5. Januar 2015: Node.js-Buildpack v1.9.1-20141208-1221 aktualisiert

* Das Node.js-Buildpack enthält nun Unterstützung für Einstellungen dynamischer Protokolle. Damit können Entwickler die Protokollebene Ihrer Anwendung während des Betriebs ändern, wenn die Anwendung für die Protokollierung das Modul 'log4js', 'bunyan' oder 'ibmbluemix' verwendet.
* Das Node.js-Buildpack enthält nun [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/). Hier sind Korrekturen für das POODLE-Problem enthalten.

## 23. Oktober 2014: Node.js-Buildpack v1.6-20141013-1736 aktualisiert

* Das Node.js-Buildpack enthält nun [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/). Dies bedeutet, dass Ihnen eine vollständig unterstützte IBM Node.js-Laufzeit zur Verfügung steht, wenn Sie die letzte stabile Node.js-Laufzeit für Ihre Anwendung (v0.10.32) angeben. Dieses neueste SDK umfasst einen Fix für ein Problem mit dem eingebetteten Modul 'qs', das zu einem Denial-of-Service-Fehler führte. Außerdem enthält es eine aktualisierte Version des Moduls 'npm' sowie weitere Verbesserungen in den Modulen 'http' und 'url'. Weiterführende Details finden Sie im [Änderungsprotokoll für v0.10.32](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog).
* Das Buildpack enthält außerdem einen Fix für einen Programmfehler, durch den während der Implementierung eine fehlerhafte Datei index.html zur Kundenanwendung hinzugefügt wurde.

## 30. September 2014: Node.js-Buildpack v1.4-20140908-1746 aktualisiert

* Das Node.js-Buildpack enthält nun [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/). Dies bedeutet, dass Ihnen eine vollständig unterstützte IBM Node.js-Laufzeit zur Verfügung steht, wenn Sie die letzte stabile Node.js-Laufzeit für Ihre Anwendung (v0.10.31) angeben. Kunden können mit dem Wissen, dass Sie sich auf die für IBM Produkte gewohnte, umfassende Unterstützung verlassen können, auf diese vollständig unterstützte Node.js-Laufzeit aufbauen.
* Das Buildpack enthält ein verbessertes Serviceframework. Insbesondere hat sich die Funktion zum Binden des Service 'Monitoring and Analytics' verbessert und es werden für Störfälle zusätzliche Diagnoseinformationen bereitgestellt.

## 18. August 2014: Node.js-Buildpack v1.3-20140821-1143 aktualisiert

* Das neueste Node.js-Buildpack enthält nun IBM SDK for Node.js v1.1.0.6. Dies bedeutet, dass Ihnen eine vollständig unterstützte IBM Node.js-Laufzeit zur Verfügung steht, wenn Sie die letzte stabile Node.js-Laufzeit (v0.10.30) für Ihre Anwendung angeben. Diese Laufzeit behebt die [V8-Sicherheitslücke (Datenverlust im Hauptspeicher)](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow).
* Das Buildpack enthält auch Verbesserungen und Fehlerkorrekturen für die Erweiterung des Service 'Monitoring and Analytics', mit der Sie über den Service Leistungsprobleme und Fehlerbedingungen diagnostizieren können.

## 29. Juli 2014: Node.js-Buildpack v1.1-20140717-1447 aktualisiert

Das Node.js-Buildpack enthält nun IBM SDK for Node.js v1.1.0.5. Dies bedeutet, dass Ihnen eine vollständig unterstützte IBM Node.js-Laufzeit zur Verfügung steht, wenn Sie die letzte stabile Node.js-Laufzeit für Ihre Anwendung (v0.10.29) angeben. Weitere Informationen zu SDKs von IBM Node.js finden Sie [hier](https://developer.ibm.com/node/sdk/).

# Zugehörige Links
## Allgemein
* [Node.js-Laufzeit](index.html)
