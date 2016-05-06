---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Sandboxmodus und Produktionsmodus

{: #push-sandboxandproduction-modes}

Sie können die Push-Benachrichtigungen in einem der folgenden Modi ausführen: Sandbox oder Produktion. Sandbox ist eine eigenständige Testumgebung für die Entwicklung und das Testen der Integration der Push-API mit dem Push-Service der Serveranwendung. Sie konfigurieren zuerst Sandbox- und Produktionsmodi über das Push-Dashboard. Sie können beim Betriebsmodus des Push-Service zwischen Sandboxmodus und Produktionsmodus mithilfe der [Push-REST-API](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window} wechseln. Standardmäßig ist der Sandboxmodus aktiviert. Auch wenn Sie zwischen den Modi wechseln können, werden die Tags, Geräte und Subskriptionen nicht von den Modi gemeinsam genutzt.


Wenn Sie bereit sind für die Bereitstellung der Anwendung in einer Liveumgebung, wählen Sie mit der Push-REST-API den Produktionsmodus aus. Informationen zur REST-API finden Sie in der REST-API-Referenz.

Führen Sie die folgenden Schritte durch, um beim Betriebsmodus des Push-Service vom Sandboxmodus in den Produktionsmodus zu wechseln:

1. Verwenden Sie den REST-API-Aufruf 'PUT' zum Festlegen der Einstellungen für die Anwendungs-ID (ApplicationID).
2. Überprüfen Sie im JSON-Hauptteil, dass der Modus gewechselt wurde, indem Sie den REST-API-Aufruf ['GET' zum Abrufen der Einstellungen der Anwendungs-ID (ApplicationID)](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window} verwenden. Die erwartete Antwort ist "mode": "PRODUCTION".
 
 ```
 { 
 "mode": "PRODUCTION"
 }
 ```
1. Nachdem der Umgebungsmodus gewechselt wurde, führen Sie den Client-Code erneut aus, um Ihr Gerät für den Produktionsmodus zu registrieren.

Informationen zur REST-API finden Sie in der REST-API-Referenz.
