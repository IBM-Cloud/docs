{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Letzte Aktualisierung: 18. Januar 2016*

# Neueste Aktualisierungen für das Node.js-Buildpack
{: #latest_updates}

Es folgt eine Liste mit den neuesten Aktualisierungen für das Node.js-Buildpack.

## 16. Dezember 2015: Node.js-Buildpack v2.8-20151209-1403 und v3.0beta-20151211-2041 aktualisiert

Dieses Release des Node.js-Buildpacks enthält zwei Versionen: Version 2.8 und Version 3.0 Beta. Beide Versionen beinhalten die folgenden Änderungen:

Eine Fehlerkorrektur für den Service 'Monitoring and Analytics'
Die Einbeziehung einer im Cache gespeicherten Laufzeit für IBM SDK für Node.js Version 4.2.3.0, Version 4.2.2.0,
Version 1.2.0.8 und Version 1.2.0.7 (basierend auf den Node.js-Community-Versionen 4.2.3, 4.2.2, 0.12.9 bzw. 0.12.8)

Das IBM Node.js-Buildpack Version 3.0 Beta wurde als nicht standardmäßiges Buildpack für Bluemix mit Node.js Version 4.2.3 als Standardlaufzeit veröffentlicht. Führen Sie für Ihre Anwendung mit der Betaversion des Buildpacks eine Push-Operation durch, um sicherzustellen, dass Ihre Apps und Services weiterhin mit Bluemix funktionieren. Nach einer Dauer von mindestens 30 Tagen wird Version 3 zum Standardbuildpack.

Gehen Sie wie folgt vor, um mit Version 3.0 Beta eine Push-Operation für Ihre Anwendung durchzuführen:
* Verwenden Sie die Option '-b' im Befehl 'cf push':
```
 cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}
* Sie können auch die Option 'buildpack' in der Datei 'manifest.yml' verwenden:
```
buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

Diese Änderung an der Standardlaufzeit hat keine Auswirkungen auf Ihre Anwendung, wenn Sie in der Datei 'package.json' Ihrer Anwendung eine bestimmte Version von Node.js konfiguriert haben. Beachten Sie, dass Sie die zum Ausführen Ihrer Anwendung zu verwendende Version von Node.js immer mithilfe des Eintrags 'engines.node' in der Datei 'package.json' angeben können. Dieser Vorgang wird unter [Verfügbare Versionen](index.html#available_versions) beschrieben.

## 23. November 2015: Node.js-Buildpack v2.7-20151118-1003 aktualisiert

In Version 2.7 haben wir Version 4.2.1.0 von IBM SDK for Node.js (basierend auf Node Version 4.2.1 LTS) einbezogen. Sie ist noch nicht als Standard festgelegt, kann aber für die Verwendung festgelegt werden. Beachten Sie, dass dadurch das zuvor verfügbare Open-Source-Build ersetzt wird. Es wurden auch einige kleine Fehlerkorrekturen am Service-Erweiterungs-Framework vorgenommen.

## 19. Oktober 2015: Node.js-Buildpack v2.6.1-20151015-1326 aktualisiert

Node.js Version 2.6.1 enthält eine Fehlerkorrektur für den [App-Verwaltungs-Handler StrongPM](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/) und eine konsistentere NPM-Version.

## 15. Oktober 2015: Node.js-Buildpack v2.6-20151006-1309 aktualisiert

Dieses Release des Node.js-Buildpacks umfasst die Integration von [StrongLoop Process Manager](https://strong-pm.io) in die App-Verwaltungsfunktion. Weitere Informationen finden Sie im Blogbeitrag [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/). 

## 15. Juni 2015: Node.js-Buildpack v2.0-20150608-1503 aktualisiert

In diesem Release wurde das Node.js-Buildpack mit dem neuesten [Node.js-Buildpack der CF-Community](https://github.com/cloudfoundry/nodejs-buildpack) synchronisiert. Dadurch wird eine Reihe neuer Features von der Community bereitgestellt. Zudem wurde das Feature für die App-Verwaltung im Node.js-Buildpack umgestaltet. Damit werden Dienstprogramme wie z. B. 'shell', 'node-inspector' und Bluemix Live Sync aktiviert. Details hierzu finden Sie unter [App-Management](../../manageapps/app_mng.html).

## 5. Mai 2015: Node.js-Buildpack v1.17-20150429-1033 aktualisiert

* Das Node.js-Buildpack umfasst nun [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/).
* Wenn in Ihrer Anwendung in der Datei 'package.json' keine Laufzeit angegeben ist, wird die App nun mit Version 0.12.1 statt Version 0.10.x gestartet. Wenn Sie die Vorgängerversion verwenden müssen, müssen Sie, wie nachstehend gezeigt, in der Datei 'package.json' Version 0.10.x angeben:```
   "engines": {
        "node": "0.10.x"
    }
```
{: codeblock}
* Bei Version 0.12.1 gibt es bekannte Probleme:
   * Bei der Verwendung des Debug Tools-Features, das mit Bluemix Live Sync ausgeliefert wird, ist das Feature zum Aussetzen beschädigt.
   * Das für den Service MQ Light verwendete Modul 'mqlight' wird bei Version 0.12.x nicht unterstützt.

* Mehrere Sicherheitslücken wurden behoben:
  * Es wurden Sicherheitslücken in OpenSSL behoben, die sich auf IBM SDK for Node.js auswirken. Nähere Informationen finden Sie im [Sicherheitsbulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21701494).
  * Es wurde eine Sicherheitslücke in RC4 Stream Cipher behoben, die sich auf IBM SDK for Node.js auswirkt. Nähere Informationen finden Sie im [Sicherheitsbulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21882778).

##  2. April 2015: Node.js-Buildpack v1.15-20150331-2231 aktualisiert

* Das Node.js-Buildpack enthält nun drei neue Features, mit denen Sie ohne erneutes Bereitstellen wie am Desktop-PC schnell in Bluemix entwickeln können.
  * Desktop Sync: Zum Synchronisieren einer beliebigen (Windows-) Desktop-Baumstruktur mit einem cloudbasierten Projektarbeitsbereich.
  * Live Edit: Sie können an einer in Bluemix ausgeführten Node.js-Anwendung Änderungen vornehmen und sie direkt in Ihrem Browser testen.
  * Debug: Einfach mit der Shell in Ihre Umgebung einbinden und mit dem Debuggen beginnen! Mit dem Node Inspector-Debugger können Sie unter anderem Code dynamisch bearbeiten, Unterbrechungspunkte einfügen, Code schrittweise durchgehen und die Laufzeit erneut starten.
  * Weitere Informationen hierzu finden Sie unter [App-Management](../../manageapps/app_mng.html#Utilities).
* Wir haben die neuesten Änderungen aus dem [Node.js-Buildpack von Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack) herangezogen. Dazu wurden von der Community einige Fehler behoben und Verbesserungen vorgenommen.
* Das Node.js-Buildpack umfasst nun [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/).

## 5. Januar 2015: Node.js-Buildpack v1.9.1-20141208-1221 aktualisiert

* Das Node.js-Buildpack unterstützt nun Einstellungen für die dynamische Protokollierung. Dadurch können Entwickler die Protokollierungsebene ihrer Anwendung während des Betriebs ändern, wenn die Anwendung die Module 'log4js', 'bunyan' oder 'ibmbluemix' für die Protokollierung verwendet.
* Das Node.js-Buildpack umfasst nun [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/). Dies schließt Korrekturen für das POODLE-Problem ein.

## 23. Oktober 2014: Node.js-Buildpack v1.6-20141013-1736 aktualisiert

* Das Node.js-Buildpack umfasst nun [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/). Dies bedeutet, dass Sie eine vollständig unterstützte IBM Node.js-Laufzeit erhalten, wenn Sie die neueste stabile Node.js-Laufzeit (v0.10.32) für Ihre Anwendung angeben. Dieses neue SDK enthält eine Korrektur für ein Problem mit dem eingebetteten qs-Modul, das zu einer Serviceverweigerung (Denial-of-Service) geführt hat. Ferner enthält es eine aktualisierte Version des npm-Moduls und andere Verbesserungen im http- und url-Modul. Weitere Details finden Sie im [Änderungsprotokoll für v0.10.32](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog).
* Das Buildpack enthält ferner eine Korrektur für einen Fehler, der während der Implementierung eine falsche Datei 'index.html' in die Kundenanwendung eingefügt hat.

## 30. September 2014: Node.js-Buildpack v1.4-20140908-1746 aktualisiert

* Das Node.js-Buildpack umfasst nun [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/). Dies bedeutet, dass Sie eine vollständig unterstützte IBM Node.js-Laufzeit erhalten, wenn Sie die neueste stabile Node.js-Laufzeit (v0.10.31) für Ihre Anwendung angeben. Kunden können auf diese vollständig unterstützte Node.js-Laufzeit aufbauen und darauf vertrauen, dass die Unterstützung genauso umfassend und zuverlässig ist wie bei allen anderen IBM Produkten.
* Das Buildpack enthält ein verbessertes Servicegerüst. Die Funktionsweise wurde insbesondere hinsichtlich der Bindung des Monitoring and Analytics-Service verbessert; im Fehlerfall werden zusätzliche Diagnoseinformationen bereitgestellt.

## 28. August 2014: Node.js-Buildpack v1.3-20140821-1143 aktualisiert

* Im Lieferumfang des neuesten Node.js-Buildpacks ist nun IBM SDK for Node.js v1.1.0.6 enthalten. Dies bedeutet, dass Sie eine vollständig unterstützte IBM Node.js-Laufzeit erhalten, wenn Sie die neueste stabile Node.js-Laufzeit (v0.10.30) für Ihre Anwendung angeben. Diese Laufzeit korrigiert die Anfälligkeit für Datenverluste im Hauptspeicher (siehe [V8 Memory Corruption and Stack Overflow](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow)).
* Ferner enthält das Buildpack Verbesserungen und Fehlerkorrekturen für die Monitoring and Analytics-Serviceerweiterung, die das Diagnostizieren von Leistungsproblemen und Fehlerbedingungen über den Service ermöglicht.

## 29. Juli 2014: Node.js Buildpack v1.1-20140717-1447 aktualisiert

Im Lieferumfang des Node.js-Buildpacks ist nun IBM SDK for Node.js v1.1.0.5 enthalten. Dies bedeutet, dass Sie eine vollständig unterstützte IBM Node.js-Laufzeit erhalten, wenn Sie die neueste stabile Node.js-Laufzeit (v0.10.29) für Ihre Anwendung angeben. Weitere Informationen zu den IBM Node.js-SDKs finden Sie [hier](https://developer.ibm.com/node/sdk/).
