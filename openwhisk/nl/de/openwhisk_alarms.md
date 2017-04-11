---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Paket für Alarme verwenden
{: #openwhisk_catalog_alarm}

Das Paket `/whisk.system/alarms` kann verwendet werden, um einen Auslöser in einer angegebenen Häufigkeit zu aktivieren. Dies ist nützlich, um sich wiederholende Jobs oder Tasks einzurichten, wie zum Beispiel das stündliche Aufrufen einer Systemsicherungsaktion.

Das Paket enthält den folgenden Feed.

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | Paket | - | Dienstprogramm für Alarme und periodisch wiederkehrende Aktionen |
| `/whisk.system/alarms/alarm` | Feed | cron, trigger_payload, maxTriggers | Auslöserereignis regelmäßig aktivieren |


## Auslöserereignis regelmäßig aktivieren
{: #openwhisk_catalog_alarm_fire}

Der Feed `/whisk.system/alarms/alarm` konfiguriert den Alarm-Service so, dass er ein Auslöserereignis mit einer angegebenen Häufigkeit aktiviert. Die folgenden Parameter sind verfügbar:

- `cron`: Eine Zeichenfolge auf der Basis der UNIX-Syntax 'crontab', die angibt, wann der Auslöser zu aktivieren ist (angegeben in koordinierter Weltzeit, UTC). Die Zeichenfolge besteht aus einer Reihe von fünf durch Leerzeichen getrennten Feldern: `X X X X X`.
Weitere Informationen zur Verwendung der cron-Syntax finden Sie unter 'http://crontab.org'. Beispiele für die von der Zeichenfolge angegebene Häufigkeit:

  - `* * * * *`: zu Beginn jeder Minute.
  - `0 * * * *`: zu Beginn jeder Stunde.
  - `0 */2 * * *`: alle zwei Stunden (z. B. 02:00:00, 04:00:00, ...).
  - `0 9 8 * *`: um 9:00:00 (UTC) am achten Tag jeden Monats.

- `trigger_payload`: Der Wert dieses Parameters wird jedes Mal zum Inhalt des Auslösers, wenn der Auslöser aktiviert wird.

- `maxTriggers`: Stoppt die Aktivierung von Auslösern, wenn dieser Grenzwert erreicht wird. Standardwert: 1.000.000. Der Wert -1 (unbegrenzt) kann verwendet werden.

Das folgende Beispiel zeigt, wie ein Auslöser erstellt wird, der einmal alle 2 Minuten aktiviert wird, wobei das Auslöserereignis die Werte für `name` und `place` enthält.

  ```
  wsk trigger create periodic \
    --feed /whisk.system/alarms/alarm \
    --param cron "*/2 * * * *" \
    --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

Jedes generierte Ereignis enthält die im Wert von `trigger_payload` angegebenen Eigenschaften als Parameter. In diesem Fall erhält jedes Auslöserereignis die Parameter `name=Odin` und `place=Asgard`.

**Hinweis:** Der Parameter `cron` bietet auch Unterstützung für eine angepasste Syntax mit sechs Feldern, wobei das erste Feld für Sekunden steht. 
Weitere Informationen zur Verwendung dieser angepassten cron-Syntax finden Sie unter 'https://github.com/ncb000gt/node-cron'. 
Im Folgenden ist ein Beispiel für die Notation mit sechs Feldern aufgeführt:
  - `*/30 * * * * *`: alle 30 Sekunden.

