---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Annotationen in OpenWhisk-Assets

OpenWhisk-Aktionen, -Auslöser, -Regeln und -Pakete (insgesamt als Assets bezeichnet) können mit `Annotationen` versehen werden. Annotationen werden wie Parameter mit einem `Schlüssel`, der einen Namen definiert, und mit einem `Wert`, der den Wert definiert, an Assets angehängt. Annotationen können bequem über die Befehlszeilenschnittstelle (CLI) mit dem Befehl `--annotation` oder kurz `-a` festgelegt werden.
{: shortdesc}

Zweck: Annotationen wurden in OpenWhisk hinzugefügt, um das Experimentieren ohne Änderungen an dem zugrunde liegenden Assetschema zu ermöglichen. Bis zum Zeitpunkt der Abfassung dieses Dokuments war bewusst nicht definiert worden, welche `Annotationen` zulässig sein sollen. Da inzwischen jedoch die Verwendung von Annotationen weiter ausgedehnt wird, um semantische Änderungen zu übertragen, ist es wichtig, sie ab jetzt auch zu dokumentieren. 

Die häufigste Verwendung von Annotationen bis heute dient dem Zweck, Aktionen und Pakete zu dokumentieren. Sie werden sehen, dass viele der Pakete im OpenWhisk-Katalog Annotationen haben. Diese Annotationen beschreiben zum Beispiel die Funktionalität, die durch die zugehörigen Aktionen bereitgestellt wird, oder erläutern, welche Parameter beim Binden des Pakets erforderlich sind, welche Aufrufparameter anzugeben sind oder ob ein Parameter ein "geheimer Schlüssel" (z. B. ein Kennwort) ist. Diese Annotationen wurden nach Bedarf zum Beispiel im Hinblick auf die Benutzerschnittstellenintegration (UI-Integration) entwickelt.

Das folgende Beispiel zeigt einen Satz von Annotationen für eine Aktion `echo`, der die Eingabeargumente unverändert (z. B. `function main(args) { return args }`) zurückgibt. Diese Aktion kann zur Protokollierung von Eingabeparametern zum Beispiel im Zusammenhang mit einer Sequenz oder Regel verwendet werden.

```
wsk action create echo echo.js \
    -a description 'An action which returns its input. Useful for logging input to enable debug/replay.' \
    -a parameters  '[{ "required":false, "description": "Any JSON entity" }]' \
    -a sampleInput  '{ "msg": "Five fuzzy felines"}' \
    -a sampleOutput '{ "msg": "Five fuzzy felines"}'
```
{: pre}

Die folgenden Annotationen werden zum Beschreiben von Paketen verwendet:

- `description`: eine prägnante Beschreibung des Pakets
- `parameters`: ein Array, das Parameter beschreibt, deren Gültigkeitsbereich das Paket ist (nachfolgend beschrieben)

Für Aktionen werden die folgenden Annotationen verwendet: 

- `description`: eine prägnante Beschreibung der Aktion
- `parameters`: ein Array, das Aktionen beschreibt, die zur Ausführung der Aktion erforderlich sind
- `sampleInput`: ein Beispiel für das Eingabeschema mit typischen Werten
- `sampleOutput`: ein Beispiel für das Ausgabeschema, in der Regel für die Beispieleingabe (`sampleInput`)

Die folgenden Annotationen gehören zu den Annotationen, die zur Beschreibung von Parametern verwendet werden:

- `name`: der Name des Parameters
- `description`: eine prägnante Beschreibung des Parameters
- `doclink`: ein Link zu weiterer Dokumentation für den Parameter (z. B. für OAuth-Tokens nützlich) 
- `required`: 'true' für erforderliche Parameter, 'false' für optionale Parameter
- `bindTime`: 'true', wenn der Parameter beim Binden eines Pakets angegeben werden muss
- `type`: der Typ des Parameters, einer der folgenden Werte: `password`, `array` (jedoch weiter gefasst verwendbar)

Die Annotationen werden *nicht* geprüft. Daher ist es zum Beispiel zwar denkbar, durch die Annotationen zu erschließen, ob die Zusammensetzung zweier Aktionen zu einer Sequenz gültig ist, aber das System tut dies bisher nicht.

## Annotationen für experimentelle Funktionen

Die API-Kerndefinition wurde in letzter Zeit um einige experimentelle Funktionen erweitert. Um Pakete und Aktionen an diesen Funktionen beteiligen zu können, wurden drei neue Annotationen eingeführt, die semantische Bedeutung haben. Diese Annotationen müssen explizit auf `true` gesetzt werden, um Wirkung zu haben. Durch Ändern des Werts von `true` in `false` wird das angehängte Asset von der experimentellen API ausgeschlossen. Die Annotationen haben im System ansonsten keine Bedeutung. Es handelt sich um die folgenden Annotationen:

- `final`: Gilt nur für eine Aktion. Sie macht alle Aktionsparameter, die bereits definiert sind, unveränderbar. Ein Parameter einer Aktion, die die Annotation hat, kann nicht durch Aufrufparameter überschrieben werden, wenn der Parameter einmal einen Wert hat, der durch das umschließende Paket oder die Aktionsdefinition definiert wurde.
- `web-export`: Gilt nur für eine Aktion. Wenn angegeben, macht diese Annotation die entsprechende Aktion für REST-Aufrufe *ohne* Authentifizierung zugänglich. Solche Aktionen werden als [*Webaktionen*](openwhisk_webactions.html) bezeichnet, da sie die Verwendung von OpenWhisk-Aktionen zum Beispiel in einem Browser ermöglichen. Es ist wichtig zu beachten, dass der *Eigner* der Webaktion die Kosten für die Ausführung der Webaktion im System trägt (d. h. der *Eigner* der Aktion ist auch Eigner des Aktivierungsdatensatzes).

