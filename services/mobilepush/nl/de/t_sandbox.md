---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Sandboxmodus und Produktionsmodus
{: #push-sandboxandproduction-modes}
Letzte Aktualisierung: 11. Januar 2017
{: .last-updated}

Sie können {{site.data.keyword.mobilepushshort}} in jedem der beiden folgenden Modi ausführen: 'Sandbox' oder 'Produktion'. 'Sandbox' ist eine eigenständige Testumgebung für die Entwicklung und das Testen der Integration der Push-API mit dem Push-Service der Serveranwendung. 

Konfigurieren Sie die Modi 'Sandbox' und 'Produktion' über das Push-Dashboard. Sie können bei der Betriebsart des Push-Service mithilfe der [Push-REST-API](https://mobile.{DomainName}/imfpush/){: new_window} zwischen dem Sandbox- und dem Produktionsmodus wechseln. Standardmäßig ist der Sandboxmodus aktiviert. Auch wenn Sie zwischen den Modi wechseln können, werden die Tags, Geräte und Subskriptionen nicht von den Modi gemeinsam genutzt.

Wenn Sie für die Bereitstellung der Anwendung in einer Liveumgebung bereit sind, wählen Sie mit der [Push-REST-API](https://mobile.{DomainName}/imfpush/){: new_window} den Produktionsmodus aus. 

Führen Sie die folgenden Schritte durch, um beim Betriebsmodus des Push-Service vom Sandboxmodus in den Produktionsmodus zu wechseln:

1. Verwenden Sie den REST-API-Aufruf 'PUT' zum Festlegen der Einstellungen für die Anwendungs-ID (ApplicationID).
2. Überprüfen Sie im JSON-Hauptteil, dass der Modus gewechselt wurde, indem Sie den REST-API-Aufruf ['GET' zum Abrufen der Einstellungen der Anwendungs-ID (ApplicationID)](https://mobile.{DomainName}/imfpush/){: new_window} verwenden. Die erwartete Antwort ist "mode": "PRODUCTION".
```{ 
    "mode": "PRODUCTION"
 }
```
	{: codeblock}
1. Nachdem der Umgebungsmodus gewechselt wurde, führen Sie den Client-Code erneut aus, um Ihr Gerät für den Produktionsmodus zu registrieren.

Informationen zur REST-API finden Sie in [REST-APIs verwenden](t_restapi.html).
