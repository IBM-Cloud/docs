---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.iotinsurance_short}} - Fehlerbehebung
{: #ts}

Im Folgenden finden Sie die Antworten auf allgemeine Fragen zur Fehlerbehebung bei der Verwendung von {{site.data.keyword.iotinsurance_full}} unter {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problem beim Bereitstellen von Apps
{: #deployingapps}
Sie können die Apps für {{site.data.keyword.iotinsurance_short}} möglicherweise nicht bereitstellen, wenn in Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation zu wenig freier Speicher vorhanden ist. Sie können entweder den Speicherplatz, den Ihre Apps nutzen, reduzieren, oder das Hauptspeicherkontingent für Ihr Konto vergrößern.
{:shortdesc}

Wenn Sie den Service {{site.data.keyword.iotinsurance_short}} öffnen, ist die Bereitstellungsfunktion nicht aktiviert und Sie können keine Apps bereitstellen.
{: tsSymptoms}

Es müssen mindestens 2 GB freier Speicher in Ihrer Organisation verfügbar sein, um die Bereitstellungsfunktion zu aktivieren. Testkonten haben maximal 2 GB Hauptspeicherkontingent. Wenn Sie andere Services oder Apps als {{site.data.keyword.iotinsurance_short}} erstellt haben, weist Ihre Organisation über zu wenig Hauptspeicher für die Bereitstellung der {{site.data.keyword.iotinsurance_short}}-Apps auf.
{: tsCauses}

Sie können entweder das Hauptspeicherkontingent Ihres Kontos erweitern oder den Hauptspeicher reduzieren, den Ihre Services und Apps nutzen.
- Für die Erweiterung des Hauptspeicherkontingents Ihres Kontos können Sie [Ihr Testkonto in ein gebührenpflichtiges Konto umwandeln](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).
- Für eine rasche Reduzierung des Hauptspeichers entfernen Sie alle Services und Apps mit Ausnahme von {{site.data.keyword.iotinsurance_short}}. Starten Sie den Service {{site.data.keyword.iotinsurance_short}} neu, damit die Änderungen wirksam werden.
- Bei gebührenpflichtigen Konten mit mehr als 2 GB Gesamtspeicher ist ein Entfernen weiterer Apps oder Services möglicherweise nicht erforderlich, wenn Sie die Menge an verwendetem Speicher anpassen. Informationen finden Sie unter [Für Organisation geltende Speicherbegrenzung wurde überschritten](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory).
{: tsResolve}

## Leistungsprobleme
{: #performance_issues}

In Zeiten mit hoher Systemauslastung kann es zu einer verlangsamten Verarbeitung kommen.
{:shortdesc}

Auf ausgelasteten Systemen, die häufig API-Aufrufe durchführen, können verzögerte Antwortzeiten auftreten.
{: tsSymptoms}

{{site.data.keyword.iotinsurance_short}} stellt standardmäßig eine Testversion von {{site.data.keyword.cloudantfull}} bereit. Durch diese Version wird die Anzahl der API-Aufrufe begrenzt, die pro Sekunde ausgeführt werden können.
{: tsCauses}

Führen Sie ein Upgrade auf die Standardversion von {{site.data.keyword.cloudant}} durch.
{: tsResolve}

## Hilfe und Support für {{site.data.keyword.iotinsurance_short}} anfordern
{: #gettinghelp}

Bei Problemen oder Fragen zur Verwendung von {{site.data.keyword.iotinsurance_full}} können Sie {{site.data.keyword.Bluemix_notm}} zurate ziehen oder Hilfe anfordern, indem Sie nach ensprechenden Informationen suchen oder Fragen in einem Forum stellen. Sie können aber auch ein Support-Ticket öffnen.

- Wenn Sie die [Statusseite von Bluemix ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/support/#status){:new_window} aufrufen, können Sie überprüfen, ob {{site.data.keyword.Bluemix_notm}} verfügbar ist.

- Sie können die Foren besuchen und überprüfen, ob andere Benutzer bereits dasselbe Problem hatten. Wenn Sie die Foren zum Stellen einer Frage nutzen, versehen Sie Ihre Frage mit entsprechenden Tags, damit sie von den {{site.data.keyword.Bluemix_notm}}-Entwicklungteams erkannt wird.
  <!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->
- Zu technischen Fragen zur Entwicklung oder Bereitstellung einer App mit {{site.data.keyword.iotinsurance_short}} posten Sie Ihre Frage an [StackOverflow ![Symbol für externen Link](../../icons/launch-glyph.svg)](http://stackoverflow.com/search?q=iot-insurance+ibm-bluemix){:new_window} und versehen Sie Ihre Frage mit den Tags "ibm-bluemix" und "iot-for-insurance".
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
- Fragen zum Service sowie Anweisungen zur Einführung finden Sie im Forum von [IBM developerWorks dW Answers ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/topics/iot-insurance/?smartspace=bluemix){:new_window}. Versehen Sie Ihre Frage mit den Tags "iot-for-insurance" und "bluemix".

Unter [Hilfe anfordern](https://www.{DomainName}/docs/support/index.html#getting-help) finden Sie weitere Details zur Verwendung der Foren.

- Wenn Sie das Problem dennoch nicht lösen können, können Sie ein IBM Support-Ticket öffnen. Weitere Informationen zum Öffnen eines IBM Support-Tickets oder zu den Supportebenen und Ticketprioritäten finden Sie im Abschnitt zur [Kontaktaufnahme mit dem Support](../support/index.html#contacting-support).
