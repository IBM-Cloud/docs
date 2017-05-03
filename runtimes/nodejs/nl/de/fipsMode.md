---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# FIPS-Modus
{: #fips_mode}

Die Node.js-Buildpackversionen v3.2-20160315-1257 sowie höhere Versionen unterstützen [FIPS ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards).  
{: shortdesc}

Setzen Sie die Umgebungsvariable FIPS_MODE auf 'true', wenn Sie eine FIPS-fähige Knotenengine verwenden möchten.
Beispiel:

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

Beachten Sie, dass einige Knotenmodule möglicherweise nicht funktionieren, wenn FIPS_MODE auf 'true' gesetzt ist.  Zum Beispiel werden **Knotenmodule fehlschlagen, die [MD5 ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://en.wikipedia.org/wiki/MD5) verwenden,** wie beispielsweise [Express ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](http://expressjs.com/). Im Falle von Express können Sie dieses Problem möglicherweise umgehen, indem Sie [etag ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](http://expressjs.com/en/api.html) in Ihrer
Expess-App auf 'false' setzen. Sie können Ihren Code beispielsweise wie folgt bearbeiten:
```
    app.set('etag', false);
```
{: codeblock}
Weitere Informationen dazu finden Sie in diesem [stackoverflow-Post ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js).

**ANMERKUNG** [App-Management](/docs/manageapps/app_mng.html) und FIPS_MODE werden *NICHT* gleichzeitig unterstützt.  Wenn die Umgebungsvariable BLUEMIX_APP_MGMT_ENABLE eingestellt ist und die Umgebungsvariable FIPS_MODE auf 'true' gesetzt ist, kann für die App kein Staging durchgeführt werden.

Es gibt mehrere Möglichkeiten, den FIPS_MODE-Status zu überprüfen:
<ul>
<li> Sie können in den Protokollen zu Ihrer Anwendung nach einer Nachricht ähnlich der folgenden suchen:     

  <pre>
  Installing FIPS-enabled IBM SDK for Node.js (4.4.3) from cache
  </pre>
  {: codeblock}

Diese Nachricht teilt mit, dass eine FIPS-fähige node.js-Engine ausgeführt wird, aber nicht unbedingt, dass FIPS ausgeführt wird
</li>

<li> Sie können den Wert von **process.versions.openssl** prüfen. Beispiel:

  <pre>
  console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

Wenn die SSL-Version 'fips' enthält, unterstützt die verwendete SSL-Version FIPS.  
</li>

<li> Bei node.js Version 6 und höher können Sie den von crypto.fips zurückgegebenen Wert in Code wie dem folgenden prüfen:

  <pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

Wenn der zurückgegebene Wert '1' ist, wird FIPS verwendet. Beachten Sie, dass crypto.fips für node.js-Versionen vor Version 6 den Wert *undefined* (nicht definiert) zurückgibt.
</li>
</ul>

## Nodejs Version 4
{: #nodejs_v4_fips}

Die folgende Tabelle erläutert das Verhalten von node.js Version 4 bezüglich FIPS:

|                 | Ergebnis        |
| :-------------- | :------------ |
|FIPS_MODE=true   |Erfolg (1)    |
|FIPS_MODE !=true |Erfolg (2)    |

* Erfolg (1)
  * FIPS wird verwendet.
  * Die Protokolle enthalten die Nachricht *Installing FIPS-enabled IBM SDK for Node.js*.
  * Der von process.versions.openssl zurückgegebene Wert enthält 'fips'.
* Erfolg (2)
  * FIPS wird *NICHT* verwendet.
  * Die Protokolle enthalten *NICHT* die Nachricht *Installing FIPS-enabled IBM SDK for Node.js*.
  * Der von process.versions.openssl zurückgegebene Wert enthält *NICHT* 'fips'.

## Nodejs Version 6
{: #nodejs_v6_fips}

Für die Ausführung im FIPS-Modus müssen Sie bei Node.js Version 6 neben der Einstellung von **FIPS_MODE=true** in Ihrem Startbefehl **--enable-fips** angeben, entsprechend dem folgenden Beispiel:
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

Die folgende Tabelle erläutert das Verhalten von node.js Version 6 bezüglich FIPS.

|                 |--enable-fips  |KEIN --enable-fips |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |Erfolg (1)    |Erfolg (2)      |
|FIPS_MODE !=true |Fehler (3)    |Erfolg (4)      |

* Erfolg (1)
  * FIPS wird verwendet.
  * Die Protokolle enthalten die Nachricht *Installing FIPS-enabled IBM SDK for Node.js*.
  * Der von process.versions.openssl zurückgegebene Wert enthält 'fips'
  * crypto.fips gibt '1' zurück, was bedeutet, dass FIPS verwendet wird
* Erfolg (2)
  * FIPS wird *NICHT* verwendet.
  * Die Protokolle enthalten die Nachricht *Installing FIPS-enabled IBM SDK for Node.js*.
  * Der von process.versions.openssl zurückgegebene Wert enthält 'fips'
  * crypto.fips gibt '0' zurück, was bedeutet, dass FIPS *NICHT* verwendet wird
* Fehler (3)
  * FIPS wird *NICHT* verwendet.
  * Die Protokolle enthalten *NICHT* die Nachricht *Installing FIPS-enabled IBM SDK for Node.js*.
  * Das Staging schlägt mit der Nachricht 'ERR node: bad option: --enable-fips' fehl
* Erfolg (4)
  * FIPS wird *NICHT* verwendet.
  * Die Protokolle enthalten *NICHT* die Nachricht *Installing FIPS-enabled IBM SDK for Node.js*.
  * Der von process.versions.openssl zurückgegebene Wert enthält *NICHT* 'fips'
  * crypto.fips gibt '0' zurück, was bedeutet, dass FIPS *NICHT* verwendet wird
