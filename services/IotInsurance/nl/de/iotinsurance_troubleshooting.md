---

copyright:
  years: 2016
lastupdated: "2016-10-06"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Fehlerbehebung
{: #troubleshooting}

Im Folgenden finden Sie die Antworten auf allgemeine Fragen zur Fehlerbehebung bei der Verwendung von {{site.data.keyword.iotinsurance_full}} unter {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problem beim Bereitstellen der Apps
{: #deployingapps}

Sie können die Apps für {{site.data.keyword.iotinsurance_short}} möglicherweise nicht bereitstellen, wenn in Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation zu wenig freier Speicher vorhanden ist. Sie können entweder den Speicherplatz, den Ihre Apps nutzen, reduzieren, oder das Hauptspeicherkontingent für Ihr Konto vergrößern.

### Was passiert?

Wenn Sie den Service {{site.data.keyword.iotinsurance_short}} öffnen, ist die Bereitstellungsfunktion nicht aktiviert und Sie können keine Apps bereitstellen.

### Wie kommt es dazu?

Es müssen mindestens 2 GB freier Speicher in Ihrer Organisation verfügbar sein, um die Bereitstellungsfunktion zu aktivieren. Testkonten haben maximal 2 GB Hauptspeicherkontingent. Wenn Sie andere Services oder Apps als {{site.data.keyword.iotinsurance_short}} erstellt haben, weist Ihre Organisation über zu wenig Hauptspeicher für die Bereitstellung der {{site.data.keyword.iotinsurance_short}}-Apps auf.

### Problembehebung

Sie können entweder das Hauptspeicherkontingent Ihres Kontos erweitern oder den Hauptspeicher reduzieren, den Ihre Services und Apps nutzen.

  - Für die Erweiterung des Hauptspeicherkontingents Ihres Kontos können Sie [Ihr Testkonto in ein gebührenpflichtiges Konto umwandeln](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).

  - Für eine rasche Reduzierung des Hauptspeichers entfernen Sie alle Services und Apps mit Ausnahme von {{site.data.keyword.iotinsurance_short}}. Starten Sie den Service {{site.data.keyword.iotinsurance_short}} neu, damit die Änderungen wirksam werden.

  - Bei gebührenpflichtigen Konten mit mehr als 2 GB Gesamtspeicher ist ein Entfernen weiterer Apps oder Services möglicherweise nicht erforderlich, wenn Sie die Menge an verwendetem Speicher anpassen. Informationen finden Sie unter [Für Organisation geltende Speicherbegrenzung wurde überschritten](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory).
