---

copyright:
  years: 2015, 2016
  
---

# Anwendungsüberwachung
{: #app-monitoring}

Neben Sicherheitseinrichtungen stellt {{site.data.keyword.amafull}} auch Überwachungs- und Analysefunktionen für Ihre mobilen Anwendungen bereit. Mit dem {{site.data.keyword.amashort}}-Client-SDK können Sie Clientprotokolle und Überwachungsdaten aufzeichnen. Entwickler können steuern, wann diese Daten an den {{site.data.keyword.amashort}}-Service gesendet werden sollen. Alle Sicherheitsereignisse, wie zum Beispiel erfolgreiche oder fehlgeschlagene Authentifizierungen, die im {{site.data.keyword.amashort}}-Service auftreten, werden automatisch protokolliert.

Wenn Daten an {{site.data.keyword.amashort}} übergeben werden, können Sie das {{site.data.keyword.amashort}}-Überwachungsdashboard verwenden, um Analyseerkenntnisse zu Ihren mobilen Anwendungen, Geräten und Clientprotokollen zu erhalten. Informationen zu Anforderungen, die Ihre Anwendung an Ressourcen sendet, die von {{site.data.keyword.amashort}} geschützt werden, werden standardmäßig aufgezeichnet.

Zu den automatisch aufgezeichneten Daten gehören Informationen wie die Anzahl der Authentifizierungen, der neuen Geräte und der neuen Benutzer. Darüber hinaus können Sie das {{site.data.keyword.amashort}}-Client-SDK so konfigurieren, dass es die folgenden Informationen zurückmeldet:

### Nutzungsstatistikdaten der mobilen Anwendungen
{: #usage-stats}

Sie können Ihre mobilen Anwendungen so konfigurieren, dass sie mit einigen einfachen API-Aufrufen Anwendungslebenzyklusereignisse aufzeichnen und die aufgezeichneten Daten an den {{site.data.keyword.amashort}}-Service senden. Sie können die Anzahl der Öffnungsvorgänge für Apps, der empfangenen Push-Benachrichtigungen usw. aufzeichnen.

### Clientseitige Protokollerfassung
{: #client-side-logcapture}

Bei Anwendungen in diesem Bereich kommt es ab und zu zu Problemen, die von einem Entwickler behoben werden müssen. Es ist häufig schwer, diese Probleme zu reproduzieren. <!--in R&D.--> Entwickler, die an dem Code gearbeitet haben, verfügen möglicherweise nicht über die Umgebung oder das richtige Gerät, um die entsprechenden Tests durchzuführen. In diesen Situationen ist es hilfreich, die Debugprotokolle von den Clientgeräten abrufen zu können, da die Probleme in der Umgebung auftreten, in der die Ereignisse stattfinden.

## Erfasste Daten aufbewahren
{: #preserve-captureddata}

Es gibt keine Möglichkeit sicherzustellen, dass alle erfassten Daten auf der Clientseite erhalten bleiben. Benutzer können die mobile Anwendung offline verwenden und gleichzeitig erfasste Analyse- und Protokolldaten kumulieren. Da der Client offline begrenzten Dateisystemspeicherbereich hat, müssen ältere protokollierte Ereignisse gelöscht werden, um neuere protokollierte Ereignisse behalten zu können. Der Entwickler muss entscheiden, wann erfasste Daten über die bereitgestellten APIs an den {{site.data.keyword.amashort}}-Service gesendet werden sollen.

## {{site.data.keyword.amashort}}-Überwachungsdashboard verwenden
{: #monitoring-dashboard}

1. Öffnen Sie das {{site.data.keyword.Bluemix}}-Dashboard und klicken Sie auf Ihre {{site.data.keyword.Bluemix_notm}}-Anwendung.

2. Wenn Ihr {{site.data.keyword.Bluemix_notm}}-Anwendungsdashboard geöffnet ist, klicken Sie auf eine {{site.data.keyword.amashort}}-Kachel.

3. Klicken Sie im {{site.data.keyword.amashort}}-Dashboard auf den Link `Überwachung` im Menü auf der linken Seite.

## Nächste Schritte
{: #next-steps}
* [Protokollfunktion aktivieren, konfigurieren und verwenden](app-monitoring-logger.html)
* [Nutzungsanalysedaten erfassen](app-monitoring-gathering-analytics.html)
