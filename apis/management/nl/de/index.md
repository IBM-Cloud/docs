---

copyright:
  years: 2017
lastupdated: "2017-04-12"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Übersicht
{: #index}

APIs können nativ in {{site.data.keyword.Bluemix}} verwaltet werden. Dabei spielt es keine Rolle, ob sie einer {{site.data.keyword.openwhisk_short}}-Aktion oder einer wachsenden Liste integrierter {{site.data.keyword.Bluemix_notm}}-Services, wie beispielsweise dem {{site.data.keyword.appconserviceshort}}-Service, zugeordnet sind. Durch das Verwalten der APIs kann die Nutzung gesteuert und die Akzeptanz erhöht werden. Ferner ist es möglich,Statistiken zu überwachen.

Das folgende Diagramm zeigt, wie die API-Verwaltung durch Einfügen eines schnellen und einfachen Gateways funktioniert. Das Gateway, das im Diagramm als API-Gateway bezeichnet wird, antwortet auf eingehende API-Aufrufe von Anwendungen. Das API-Gateway stellt eine umfassende Reihe von API-Richtlinien für Sicherheit, Datenverkehrsmanagement, Mediation, Beschleunigung und Nicht-HTTP-Protokoll-Unterstützung bereit.

![API-Gateway - Ablauf](images/bluemix-native-apim-flow_ow.png "API-Verwaltung - Ablauf")

Wenn Sie eine API verfügbar machen, kann diese API von anderen Benutzern verwendet werden. Dabei erhalten die Benutzer der API häufig eingeschränkten Zugriff auf die Informationen, die sich auf den verwalteten Servern befinden. Dies führt zu einer höheren Benutzerfreundlichkeit für den Endbenutzer, da der Zugriff auf die Informationen direkt über die aktuelle Schnittstelle erfolgt.

Manchmal kann es notwendig sein, gewisse Aktivitäten auf den Servern zu steuern. Wenn auf einem Server beispielsweise zu viele API-Anforderungen in einem kurzen Zeitraum erfolgen, kann es zu einer Überlastung des Servers kommen, der daraufhin beendet wird. Um Situationen wie diese zu vermeiden, kann die Rate der API-Aufrufe über die API-Verwaltung gesteuert werden. Das der API zugeordnete einfache Gateway überwacht die Anzahl der API-Aufrufe und schränkt die Anzahl der akzeptierten Aufrufe ein. Ferner kann mithilfe der API-Verwaltung die Menge der API-Aufrufe einer bestimmten Quelle durch Aufzeichnung des zugehörigen API-Schlüssels überwacht werden. Der API-Schlüssel ist eine eindeutige Zeichenfolge, die das API-Entwicklerteam dem API-Verbraucherteam zur Verfügung stellt und dem API-Entwickler die Überwachung von Statistiken zu den Aufrufen ermöglicht, die von den Anforderungen des Verbraucherteams generiert werden.  

Die API-Verwaltung von {{site.data.keyword.Bluemix_notm}} bietet die folgenden Funktionen:
## API-Analyse
{: #basic_analytics notoc}

Sollen APIs gewinnbringend genutzt werden, können Sie mithilfe der Analysefunktion die Aufrufnutzung überwachen. Ferner erhalten Sie Aufschluss über die Art der API-Nutzung, um fundierte Entscheidungen hinsichtlich der Frage zu treffen, wie die APIs für eine höhere Akzeptanz aktualisiert werden sollten.

Die folgenden Statistiken zu APIs können angezeigt werden:
* Die Anzahl der Antworten und die durchschnittliche Antwortzeit in der letzten Stunde oder im angegebenen Zeitintervall.
* Die Anzahl der API-Aufrufe pro Minute.
* Die letzten 100 Antworten.

## Ratenbegrenzung durch Subskription (API-Schlüssel)
{: #rate_limit notoc}

Sie können eine Ratenbegrenzung festlegen, um die Anzahl der API-Aufrufe durch Anwendungen zu steuern. Im Falle einer Ratenbegrenzung kann nur eine bestimmte Anzahl von Aufrufen pro Sekunde, Minute oder Stunde erfolgen, sodass Ihr Back-End nicht überlastet wird. Sie können diese Begrenzung entweder für alle APIs oder pro API-Schlüssel festlegen.

## OAuth
{: #oauth notoc}

Um eine unzulässige Nutzung der bereitgestellten Daten zu verhindern, können Sie sicherstellen, dass nur Benutzer mit einer korrekten Authentifizierung auf die APIs zugreifen können. Der API-Zugriff kann über den OAuth-Autorisierungsstandard gesteuert werden. OAuth ist ein tokenbasiertes Berechtigungsprotokoll, das Websites anderer Anbieter oder Anwendungen den Zugriff auf Benutzerdaten ermöglicht, ohne dass der Benutzer persönliche Daten preisgeben muss.

## CORS
{: #cors notoc}

CORS ermöglicht den in einer Webseite eingebetteten Scripts domänenübergreifende API-Aufrufe. Der Vorteil für den API-Benutzer besteht darin, dass die API die Informationen aus einer anderen Domäne abrufen kann, wenn diese von der API aufgerufen wird. Ohne die Aktivierung von CORS ist das Abrufen von Inhalten auf die Domäne der ursprünglichen Anforderung begrenzt. Weitere Informationen zu CORS sowie zur Implementierung finden Sie in [HTTP access control (CORS) ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS.html){: new_window}.

## Weitere API-Verwaltungsoptionen
{: #add_mgt_options notoc}

Diese Funktionen für die API-Verwaltung können über die Registerkarte 'API-Verwaltung' des {{site.data.keyword.openwhisk_short}}- oder App Connect-Dashboards aufgerufen werden. Für komplexere Verwaltungslösungen ist ein Upgrade auf den vollständigen {{site.data.keyword.apiconnect_full}}-Service möglich. Weitere Informationen zum {{site.data.keyword.apiconnect_full}}-Service finden Sie in
[Getting started with API Connect](https://console.ng.bluemix.net/docs/services/apiconnect/index.html){: new_window}.

Weitere Informationen zum Upgrade der in {{site.data.keyword.Bluemix_notm}} verwalteten APIs auf den {{site.data.keyword.apiconnect_short}}-Service finden Sie in [Auf weitere Funktionen der API-Verwaltung zugreifen](upgrade.html).

