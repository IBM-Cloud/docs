---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.streaminganalyticsshort}} - Fehlerbehebung
{: #ts_StreamingAnalytics}

Hier finden Sie Antworten auf häufig gestellte Fragen zur Verwendung von {{site.data.keyword.streaminganalyticsshort}} unter {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

##Wenn ich den Service starte, werde ich zur Eingabe von Berechtigungsnachweisen aufgefordert, um mich an der Konsole anmelden zu können.
{: #log_in_console}

Wenn Sie {{site.data.keyword.streaminganalyticsshort}} starten, werden Sie aufgefordert, Berechtigungsnachweise für die Anmeldung an der Servicekonsole einzugeben.
{:shortdesc}

Sie starten einen {{site.data.keyword.streaminganalyticsshort}}-Service, den Sie zuvor erstellt haben, und anstatt direkt Zugriff auf die Servicekonsole zu erhalten, wird eine Anmeldeseite angezeigt, auf der Sie zur Eingabe der Berechtigungsnachweise aufgefordert werden.
{: tsSymptoms}

Die Serviceinfrastruktur wurde aktualisiert und Ihr Browser-Cache verhindert, dass der Service die Aktualisierung aufgreift.
{: tsCauses}

Löschen Sie Ihren Browser-Cache, um sicherzustellen, dass Sie die aktuelle Version der Servicekonsole erhalten.
{: tsResolve}

##Meine Anwendung weist einen nicht einwandfreien Zustand auf
{: #app_unhealthy}

Sie können Ihre Anwendung nicht korrekt ausführen und der Allgemeinzustand ist `nicht einwandfrei`.
{:shortdesc}

Sie übergeben eine Anwendung an die Serviceinstanz, die Anwendung startet, schlägt dann aber sofort fehl und der Allgemeinzustand ist `nicht einwandfrei`. Der folgende Fehler ist in der Protokolldatei dokumentiert: `/lib64/libc.so.6: Version GLIBC_2.14 nicht gefunden`.
{: tsSymptoms}

Sie haben die Anwendung nicht mithilfe eines RHEL 6.5-Betriebssystems oder einer entsprechenden CentOS-Version kompiliert.
{: tsCauses}

Sie müssen Ihre Anwendung unter einem Red Hat Enterprise Linux (RHEL) 6.5-Betriebssystem oder einer entsprechenden CentOS-Version mit Intel-Prozessoren erneut kompilieren. Übergeben Sie Ihre Anwendung erneut an die Serviceinstanz.
{: tsResolve}
