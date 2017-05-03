---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Neueste Aktualisierungen für das SDK for Nodejs-Buildpack
{: #latest_updates}

Eine Liste mit den neuesten Aktualisierungen im Buildpack 'sdk-for-nodejs'.

## 10. März 2017: Node.js-Buildpack v3.11 aktualisiert
Mit diesem Release des Buildpacks werden die IBM SDK for Node.js-Laufzeitversionen: 0.10.47, 0.10.48, 0.12.17, 0.12.18, 4.7.3, 4.8.0, 6.9.5 und 6.10.0 unterstützt. Die Standardversion ist jetzt 4.8.0.

Zusätzlich zu den neuen Laufzeiten enthält dieses Release Fehlerkorrekturen für einen Fehler, der beim Aktivieren des Shell-App-Management-Handlers mithilfe der Benutzerschnittstelle von devconsole aufgetreten war. Dieses Buildpack ändert ferner die Funktionsweise der automatischen Konfiguration für den Service 'Monitoring and Analytics'. Anwendungen mit dem kostenfreien Plan verfügen bei Ihren Anwendungen nicht mehr über die Protokollfunktion, die durch logmet ersetzt wurde.

## 20. Januar 2017: Node.js-Buildpack v3.10 aktualisiert
Mit diesem Release des Buildpacks werden die IBM SDK for Node.js-Laufzeitversionen: 0.10.47, 0.10.48, 0.12.17, 0.12.18, 4.7.0, 4.7.2, 6.9.2 und 6.9.4 unterstützt. Die Standardversion ist jetzt 4.7.2.

Sie enthält einen Fix für einen Fehler, bei dem "npm start" nicht immer aufgerufen wurde, um Anwendungen zu starten.

## 17. November 2016: Node.js-Buildpack v3.9 aktualisiert
Mit diesem Release des Buildpacks werden die IBM SDK for Node.js-Laufzeitversionen: 0.10.47, 0.10.48, 0.12.16, 0.12.17, 4.6.1, 4.6.2, 6.7.0 und 6.9.1 unterstützt. Die Standardversion ist jetzt 4.6.2.

Beachten Sie, dass Node.js v6 am 18. Oktober 2016 auf den LTS-Status hochgestuft wurde und bald zur Standardlaufzeit des Buildpacks wird. Node.js v0.10 hat seine Lebensdauer am 31. Oktober 2016 erreicht und ist nicht mehr im Buildpack enthalten. Weitere Details finden Sie unter [Node.js version long-term support and the SDK for Node.js buildpack](https://www.ibm.com/blogs/bluemix/2016/11/node-version-support-and-sdk-buildpack/). 

Fehler, die die App-Management-Handler für die Traceerstellung und 'inspector' betreffen, wenn diese zusammen mit Node.js v6 verwendet werden, wurden in diesem Release behoben. Weitere Informationen dazu, wie der 'inspector'-Handler sich verändert hat, nachdem nun Node.js v6 die Funktionen von 'inspector' integriert hat, finden Sie unter [Managing Liberty and Node.js apps](/docs/manageapps/app_mng.html#inspector). 

## 7. Oktober 2016: Node.js-Buildpack v3.8-20161006-1211 aktualisiert
Dieses Release des Buildpacks unterstützt die IBM SDK for Node.js-Laufzeitversionen: 0.10.46, 0.10.47, 0.12.15, 0.12.16, 4.5.0, 4.6.0, 6.6.0 und 6.7.0. Der Standardwert lautet jetzt 4.6.0.

Zusätzlich zu den neuen Laufzeiten enthält dieses Release Fehlerkorrekturen für das Buildpack. Ein Fix für das bekannte Problem bei der Verwendung von Node.js 6.x und dem Entwicklungsmodus, das in den Releaseaktualisierungen zu v3.7-20160826-1101 genannt wurde, ist eines davon. Es erfolgt ferner eine Synchronisation mit dem [Cloud Foundry Node.js Buildpack v1.5.20](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.20).

## 26. August 2016: Node.js-Buildpack v3.7-20160826-1101 aktualisiert
Mit diesem Release des Buildpacks werden die IBM SDK for Node.js-Laufzeitversionen: 0.10.45, 0.10.46, 0.12.14, 0.12.15, 4.4.7, 4.5.0, 6.2.2 und 6.4.0 hinzugefügt. Der Standardwert ist jetzt 4.5.0.

Dieses Release beinhaltet auch die Fehlerkorrekturen aus dem [Node.js-Buildpack 1.5.18 von Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.18).

Das Release entfernt die Unterstützung für den strongpm App Management-Handler entsprechend der Ankündigung in [Bluemix Node.js Buildpack v3.3 – FIPS-Modus und mehr](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/).

Beachten Sie, dass es ein bekanntes Problem bei der Verwendung von Node.js 6.x und dem [Entwicklungsmodus](/docs/manageapps/app_mng.html#devmode) gibt. Als Problemumgehung müssen Sie, nachdem Sie den Entwicklungsmodus aktiviert haben, Ihrer Anwendung vor der Verwendung erneut eine Stage zuweisen.

## 22. Juli 2016: Node.js-Buildpack v3.6-20160715-0749 aktualisiert
Mit diesem Release des Buildpacks werden die IBM SDK for Node.js-Laufzeitversionen 0.10.45, 0.10.46, 0.12.14, 0.12.15, 4.4.6, 4.4.7, 6.2.1 und 6.2.2 unterstützt. Die Standardversion ist jetzt 4.4.7.

Dieses Release enthält ein App-Management-Proxy, das eingebundene Anmeldungen unterstützt.

Fixes für die folgenden Sicherheitslücken sind enthalten:
* [CVE-2016-1669](http://www-01.ibm.com/support/docview.wss?uid=swg21986383)

## 22. Juni 2016: Node.js-Buildpack v3.5-20160609-1608 aktualisiert

Mit diesem Release des Buildpacks werden die IBM SDK for Node.js-Laufzeitversionen 4.4.5 und 6.2.0 hinzugefügt. Zur Standardversion wird 4.4.5.

Das Release entfernt die Unterstützung älterer Laufzeitversionen entsprechend der Ankündigung in [Bluemix Node.js Buildpack v3.3 – FIPS-Modus und mehr](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/). Das Buildpack unterstützt jetzt 0.10.44, 0.10.45, 0.12.13, 0.12.14, 4.4.4, 4.4.5, 6.1.0 und 6.2.0.

Dieses Release beinhaltet Fehlerkorrekturen aus dem [Node.js-Buildpack 1.5.14 von Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.14).

## 20. Mai 2016: Node.js-Buildpack v3.4-20160518-1653 aktualisiert

Mit diesem Release des Buildpacks werden die IBM SDK for Node.js-Laufzeitversionen 0.10.45, 0.12.14, 4.4.4, 6.0.0 und 6.1.0 hinzugefügt. Die Standardversion ist jetzt 4.4.4.

Fixes für die folgenden Sicherheitslücken sind enthalten:
* [CVE-2015-8855](http://www-01.ibm.com/support/docview.wss?uid=swg21982852)
* [CVE-2016-2108 CVE-2016-2107 CVE-2016-2105 CVE-2016-2106 CVE-2016-2109 CVE-2016-2176 ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://www.openssl.org/news/secadv/20160503.txt)

Beachten Sie, dass es ein bekanntes Problem mit npm Version 3 und dem Dienstprogramm 'inspector' des App-Managements gibt. npm 3.8.6 ist die Standardversion bei den Laufzeiten 6.0.0 und 6.1.0. Wenn Sie eine der 6.x-Laufzeiten und das Dienstprogramm 'inspector' verwenden möchten, sollten Sie als temporäre Fehlerumgehung in Ihrer Datei 'package.json'eine 2.x-Version von npm angeben.

## 29. April 2016: Node.js-Buildpack v3.3-20160428-1409 aktualisiert

Mit diesem Release des Buildpacks werden die IBM SDK for Node.js-Laufzeitversionen 0.10.44, 0.12.13, 4.4.0, 4.4.1, 4.4.2 und 4.4.3 hinzugefügt. Die Standardversion ist jetzt 4.4.3.
Bei
4.3.1 und höher ist es nun möglich, eine FIPS-fähige Version der Laufzeit zu verwenden. Hierfür müssen Sie die Umgebungsvariable `FIPS_MODE=true` für Ihre App festlegen.

Das aktualisierte Buildpack und die neuen Laufzeitversionen enthalten außerdem Fixes für Sicherheitslücken:
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

Das aktualisierte Buildpack enthält auch Fixes für einige Programmfehler:
* IBM SDK for Node.js-Builds werden jetzt immer verwendet, sobald einer für den Abgleich mit dem angeforderten Bereich verfügbar ist. Früher galt dies nur für 4.x-Laufzeitversionen.
* Das Dienstprogramm 'inspector' des App-Managements funktioniert nun mit 4.x-Laufzeitversionen.
* Eine Regression im Dienstprogramm 'strongpm' des App-Managements wurde behoben.

## 18. März 2016: Node.js-Buildpack v3.2-20160315-1257 aktualisiert

Mit diesem Release des Buildpacks wird die standardmäßige IBM SDK for Node.js-Laufzeit von Version 4.3.0 auf 4.3.2 verschoben. IBM SDK for Node.js in den Versionen 0.10.43, 0.12.12 und 4.3.1 ist ebenfalls enthalten. Verwenden Sie diese neuesten Node.js-Versionen, um Fixes für einige Sicherheitslücken zu übernehmen.

## 4. März 2016: Node.js-Buildpack v3.1-20160222-1123 aktualisiert

Mit diesem Release des Buildpacks wird die standardmäßige IBM SDK for Node.js-Laufzeit von Version 4.2.4 auf 4.3.0 verschoben. IBM SDK for Node.js in den Versionen 0.10.42, 0.12.10 und 4.2.6 ist ebenfalls enthalten. Verwenden Sie diese neuesten Node.js-Versionen, um Fixes für einige Sicherheitslücken zu übernehmen.

## 4. Februar 2016: Node.js-Buildpack v3.0-20160125-1224 aktualisiert

Dieses Release ist vollständig mit dem [Node.js-Buildpack der Cloud Foundry-Community](https://github.com/cloudfoundry/nodejs-buildpack) synchronisiert. Zusätzlich zu Änderungen der Community wurden Änderungen an bestimmten Standardwerten sowie Optimierungen zum Reduzieren der für das Staging erforderlichen Zeit und Aktualisierungen für das Feature 'App-Management' vorgenommen.

* Buildpack-Aktualisierungen:

  * Node.js v4.2.4 (IBM SDK for Node.js Version 4) ist nun die Standardlaufzeit in Bluemix und ersetzt v0.12.9. Diese Änderung kann dazu führen, dass Ihre Anwendung ein anderes Verhalten zeigt, wenn für Ihre Anwendung nicht eine bestimmte Version angegeben wurde. Lesen Sie die Dokumentation zur [Node.js-Laufzeit](index.html), um zu erfahren, wie für Ihre Bluemix-Anwendung eine bestimmte Version von Node.js angegeben wird.

  * Für NODE_ENV ist nun standardmäßig die Einstellung *production* festgelegt. Diese Änderung führt zu einem geänderten Verhalten einiger Knotenabhängigkeiten. Beispielsweise gibt das Express-Framework im Web-Browser für fehlerhafte Endpunkte keine Stack-Traces mehr zurück, sondern zeigt stattdessen *Internal Server Error* (Interner Serverfehler) an. Wenn für NPM_CONFIG_PRODUCTION die Einstellung *true* festgelegt ist, legt NPM für NODE_ENV die Einstellung *production* nur für Subshell-Scripts in der Installationsphase für 'npm' fest. Diese Funktion erlaubt es Benutzern, für NODE_ENV einen anderen Wert, beispielsweise *development*, als Anwendungslaufzeit festzulegen. Für die Übersichtlichkeit erkennen npm-Scripts die Nachricht **NODE_ENV=production**.

  * Eine Fehlerkorrektur für den Service 'Monitoring and Analytics' ist enthalten.

* Cacheaktualisierungen:

  * Wenn der Cache inaktiviert ist (NODE_MODULES_CACHE=false), startet das Buildpack nicht den Versuch, Module oder Komponenten in den Cache zu stellen. Zuvor hat diese Einstellung bewirkt, dass der Cache nicht abgerufen wurde, die installierten Module jedoch für zukünftige Implementierungen in den Cache gestellt wurden. Nun wird der Cache nicht abgerufen und es wird nicht versucht, einen Cache zu speichern.

  * Bower-Komponenten (bower-components) werden standardmäßig zusätzlich zu Knotenmodulen (node_modules) in den Cache gestellt.

* Andere Aktualisierungen:

  * Nützliche Warnungen für fehlende Abhängigkeiten wie 'gulp', 'bower' und 'angular' wurden hinzugefügt.

  * Das Erkennungsscript wird mit Informationen zur Buildpackversion aktualisiert.

  * Die ursprünglich von der Community eingeführte Clusteringempfehlung (WEB_CONCURRENCY) wurde entfernt, da die Speicherfeststellung für Bluemix falsch war.


## 16. Dezember 2015: Node.js-Buildpacks v2.8-20151209-1403 und v3.0beta-20151211-2041 aktualisiert

Dieses Release des Buildpacks für Node.js steht in zwei Versionen zur Verfügung: v2.8 und v3.0beta. Beide Versionen enthalten folgende Änderungen:

Eine Fehlerkorrektur für den Service 'Monitoring and Analytics'. Die Einbeziehung einer im Cache gespeicherten Laufzeit für IBM SDK for Node.js v4.2.3.0, v4.2.2.0, v1.2.0.8 und v1.2.0.7, die auf den Node.js-Versionen v4.2.3, v4.2.2, v0.12.9 und v0.12.8 der Community basieren.
Außerdem wurde in v3.0beta die Node.js-Standardlaufzeit in v4.2.3 geändert.

Das IBM Node.js-Buildpack v3.0beta wurde jetzt als nicht standardmäßiges Buildpack für Bluemix mit Node.js v4.2.3 als Standardlaufzeit freigegeben. Führen Sie für Ihre Anwendung eine Push-Operation mit der Betaversion des Buildpacks durch, um sicherzustellen, dass Ihre Apps und Services weiterhin in Bluemix ausgeführt werden. Nach mindestens 30 Tagen wird Version 3 das Standardbuildpack.

Gehen Sie wie folgt vor, um für Ihre Anwendung eine Push-Operation mit v3.0beta durchzuführen:
* Verwenden Sie in Ihrem Befehl 'cf push' die Option '-b':

```
        cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}

* Verwenden Sie alternativ die Option 'buildpack' in Ihrer Datei manifest.yml:

```
        buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

Diese Änderung der Standardlaufzeit hat keine Auswirkung auf Ihre Anwendung, wenn Sie in der Datei 'package.json' Ihrer Anwendung eine bestimmte Version von Node.js konfiguriert haben. 

**Anmerkung:** Sie können immer die zum Ausführen Ihrer Anwendung zu verwendende Node.js-Version angeben, indem Sie den Eintrag 'engines.node' in Ihrer Datei 'package.json'wie in [Verfügbare Versionen](index.html#available_versions) erläutert verwenden.

## 23. November 2015: Node.js-Buildpack v2.7-20151118-1003 aktualisiert

In 2.7 wurde Version 4.2.1.0 von IBM SDK for Node.js (basierend auf Node v4.2.1 LTS) integriert. Dies ist noch nicht die Standardeinstellung, sie kann aber für die Verwendung angegeben werden. **Anmerkung:** Diese Version ersetzt den zuvor verfügbaren Open-Source-Build. Es wurden auch einige kleinere Fehlerkorrekturen am Framework für Serviceerweiterungen vorgenommen.

## 19. Oktober 2015: Node.js-Buildpack v2.6.1-20151015-1326 aktualisiert

In Node.js v2.6.1 wird eine Fehlerkorrektur für den [StrongPM-App-Management-Handler](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/) und eine konsistentere Version von NPM eingeführt.

## 15. Oktober 2015: Node.js-Buildpack v2.6-20151006-1309 aktualisiert

Dieses Release von Node.js-Buildpack bietet die Integration von [StrongLoop Process Manager ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://strong-pm.io) für das Feature 'App-Management'. Weitere Informationen finden Sie im Blogbeitrag [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/).

## 15. Juni 2015: Node.js-Buildpack v2.0-20150608-1503 aktualisiert

In diesem Release wurde unser Node.js-Buildpack mit dem neuesten [Node.js-Buildpack der CF-Community](https://github.com/cloudfoundry/nodejs-buildpack) synchronisiert, das mit einer Reihe neuer Features der Community ausgestattet ist.
Darüber hinaus wurde das Feature 'App-Management' im Node.js-Buildpack umgestaltet, wodurch die Verwendung von Dienstprogrammen wie 'shell', 'node-inspector', 'Bluemix Live Sync' und anderen ermöglicht wird. Details finden Sie in [App-Management](/docs/manageapps/app_mng.html).

## 5. Mai 2015: Node.js-Buildpack v1.17-20150429-1033 aktualisiert

* Das Node.js-Buildpack wird nun mit [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/) geliefert.
* Wenn Ihre Anwendung in der zugehörigen Datei 'package.json' keine Laufzeit angibt, verwendet Ihre App jetzt Version 0.12.1 statt Version 0.10.x. Wenn Sie die vorherige Version verwenden müssen, geben Sie in Ihrer Datei 'package.json'wie unten gezeigt Version 0.10.x an.

```
        "engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* Bekannte Probleme mit Version 0.12.1:
   * Bei Verwendung des von Bluemix Live Sync bereitgestellten Features 'Debug Tools' (Fehlerbehebungstools) funktioniert die Funktion 'Suspend' (Vorübergehend sperren) nicht.
   * Das für den Service MQ Light verwendete Modul 'mqlight' wird in Version 0.12.x nicht unterstützt.

* Eine Reihe von Sicherheitslücken wurden behoben:
  * Sicherheitslücken in OpenSSL, die sich auf IBM SDK for Node.js auswirkten, wurden behoben. Weitere Details finden Sie im [Sicherheitsbulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21701494).
  * Sicherheitslücke in RC4 Stream Cipher, die sich auf IBM SDK for Node.js auswirkte, wurde behoben. Weitere Details finden Sie im [Sicherheitsbulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21882778).

##  2. April 2015: Node.js-Buildpack v1.15-20150331-2231 aktualisiert

* Das Node.js-Buildpack enthält nun drei neue Features, um in Bluemix ohne erneute Implementierung eine ähnlich schnelle Entwicklung wie auf einem Desktop zu erreichen.
  * Desktop Sync: Synchronisieren Sie eine beliebige Desktop-Baumstruktur (Windows) mit einem cloudbasierten Projektarbeitsbereich.
  * Live Edit: Ermöglicht Ihnen das Durchführen von Änderungen an einer in Bluemix ausgeführten Node.js-Anwendung und das sofortige Testen dieser Änderungen in Ihrem Browser.
  * Debug: Führen Sie in Ihrer Umgebung eine Shell-Operation und anschließend ein Debug durch! Mithilfe des Debuggers 'Node Inspector' können Sie unter anderem Code dynamisch bearbeiten, Unterbrechungspunkte einfügen, Code schrittweise durchgehen und die Laufzeit erneut starten
  * Weitere Informationen finden Sie in [App-Management](/docs/manageapps/app_mng.html#Utilities).
* Die neuesten Änderungen aus dem [Node.js-Buildpack von Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack) wurden einbezogen. Diese Änderungen umfassen eine Reihe von Fehlerkorrekturen und von der Community vorgenommene Verbesserungen.
* Das Node.js-Buildpack enthält nun [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/).

## 5. Januar 2015: Node.js-Buildpack v1.9.1-20141208-1221 aktualisiert

* Das Node.js-Buildpack enthält nun Unterstützung für Einstellungen dynamischer Protokolle. Mit dieser Unterstützung können Entwickler die Protokollebene Ihrer Anwendung dynamisch ändern, wenn die Anwendung für die Protokollierung das Modul 'log4js', 'bunyan' oder 'ibmbluemix' verwendet.
* Das Node.js-Buildpack enthält nun [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/). Dieses Update enthält Korrekturen für das POODLE-Problem.

## 23. Oktober 2014: Node.js-Buildpack v1.6-20141013-1736 aktualisiert

* Das Node.js-Buildpack enthält nun [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/). Dieses Update bedeutet, dass Ihnen eine vollständig unterstützte IBM Node.js-Laufzeit zur Verfügung steht, wenn Sie die letzte stabile Node.js-Laufzeit für Ihre Anwendung angeben (v0.10.32). Dieses neueste SDK umfasst einen Fix für ein Problem mit dem eingebetteten Modul 'qs', das zu einem Denial-of-Service-Fehler führte. Außerdem enthält es eine aktualisierte Version des Moduls 'npm' sowie weitere Verbesserungen in den Modulen 'http' und 'url'. Weitere Details finden Sie im [Änderungsprotokoll für v0.10.32](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog).
* Das Buildpack enthält außerdem einen Fix für einen Programmfehler, durch den während der Implementierung eine fehlerhafte Datei 'index.html' zur Kundenanwendung hinzugefügt wurde.

## 30. September 2014: Node.js-Buildpack v1.4-20140908-1746 aktualisiert

* Das Node.js-Buildpack enthält nun [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/). Dieses Update bedeutet, dass Ihnen eine vollständig unterstützte IBM Node.js-Laufzeit zur Verfügung steht, wenn Sie die letzte stabile Node.js-Laufzeit für Ihre Anwendung angeben (v0.10.31). Mit einer vollständig unterstützten Node.js-Laufzeit erhalten die Kunden ein konsistentes Unterstützungsangebot.
* Das Buildpack enthält ein verbessertes Serviceframework. Insbesondere arbeitet es besser beim Binden des Service 'Monitoring and Analytics' und stellt mehr Diagnoseinformationen bereit, wenn der Service ausfällt.

## 28. August 2014: Liberty-Buildpack v1.3-20140821-1143 aktualisiert

* Das neueste Node.js-Buildpack enthält nun IBM SDK for Node.js v1.1.0.6. Dieses Update bedeutet, dass Ihnen eine vollständig unterstützte IBM Node.js-Laufzeit zur Verfügung steht, wenn Sie die letzte stabile Node.js-Laufzeit für Ihre Anwendung angeben (v0.10.30). Diese Laufzeit korrigiert die [V8-Sicherheitslücke (Datenverlust im Hauptspeicher) ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow).
* Das Buildpack enthält auch Verbesserungen und Fehlerkorrekturen für die Erweiterung des Service 'Monitoring and Analytics', mit der Sie über den Service Leistungsprobleme und Fehlerbedingungen diagnostizieren können.

## 29. Juli 2014: Node.js-Buildpack v1.1-20140717-1447 aktualisiert

Das Node.js-Buildpack enthält nun IBM SDK for Node.js v1.1.0.5. Dieses Update bedeutet, dass Ihnen eine vollständig unterstützte IBM Node.js-Laufzeit zur Verfügung steht, wenn Sie die letzte stabile Node.js-Laufzeit für Ihre Anwendung angeben (v0.10.29). Sie finden weitere Informationen zu [IBM Node.js SDKs](https://developer.ibm.com/node/sdk/).

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [Node.js-Laufzeit](index.html)
