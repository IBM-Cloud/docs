---

copyright:
  years: 2015, 2016

---

# Einführung
{: #getting-started}
Für den Einstieg in die Verwendung von {{site.data.keyword.amashort}} können Sie entweder den {{site.data.keyword.amashort}}-Service einer vorhandenen {{site.data.keyword.Bluemix}}-Anwendung hinzufügen oder Sie können eine neue App mit der Boilerplate erstellen.  

## Instanz des {{site.data.keyword.amashort}}-Service erstellen
{: #service-instance}

Sie können eine neue Instanz eines {{site.data.keyword.amashort}}-Service über den {{site.data.keyword.Bluemix}}-Katalog erstellen.  Wenn Sie nicht die Boilerplate zum Erstellen eines neuen mobilen Back-Ends verwenden, müssen Sie das Server-SDK auf Ihrem vorhandenen Back-End konfigurieren.


  * **Neue App**: Die Anweisungen in den folgenden Abschnitten beschreiben die Erstellung einer neuen App, die ein mobiles Back-End erstellt und dieses mit dem {{site.data.keyword.amashort}}-Server-SDK schützt. Klicken Sie auf die Boilerplate **MobileFirst Services Starter**, um eine neue Anwendung mit dem {{site.data.keyword.amashort}}-Service zu erstellen.
  * **Vorhandene App**: Klicken Sie auf das Symbol für {{site.data.keyword.amashort}} und erstellen Sie eine neue Serviceinstanz, die an eine vorhandene Anwendung gebunden ist. Informationen zur Konfiguration des Server-SDK für Ihre vorhandene App finden Sie in [Cloudressourcen schützen](protecting-resources.html).


## Mobiles Back-End mit der Boilerplate 'MobileFirst Services Starter' erstellen
{: #create-backend}
Wenn Sie 'MobileFirst Services Starter' verwenden, erhalten Sie eine Instanz einer Node.js-Laufzeit, die auf IBM {{site.data.keyword.Bluemix_notm}} aktiv ist, um Ihre angepasste Back-End-Logik zu implementieren. Ein Satz von mobilen Kernservices, die Sicherheits-, Daten-, Push- und Überwachungsfunktionen bereitstellen, wird an diese Node.js-App gebunden. Nach dem Erstellen der Node.js-App in {{site.data.keyword.Bluemix_notm}} können Sie Ihre Entwicklungsumgebung einrichten und mit der Verwendung der {{site.data.keyword.Bluemix_notm}} Mobile Services-SDKs beginnen. Sie können die SDKs verwenden, um mit einfachen API-Aufrufen auf die Services zuzugreifen, die an Ihre Cloud-App gebunden sind.

1. Wechseln Sie im {{site.data.keyword.Bluemix_notm}}-Katalog zum Abschnitt **Boilerplates** und klicken Sie auf **MobileFirst Services Starter**.
1. Fügen Sie Informationen zu Ihrem mobilen Back-End hinzu, wie Bereich, Name, Host und Serviceplan.
1. Klicken Sie auf **CREATE** (Erstellen).



## Nächste Schritte
{: #next-steps}
Mehrere Endpunkte der Node.js-Anwendung, die Sie mit der Boilerplate erstellt haben, werden mit {{site.data.keyword.amashort}} geschützt. Weitere Informationen zur Standardanwendung für das mobile Back-End finden Sie in [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop).

Sie können Ihre mobile App so einrichten, das sie das {{site.data.keyword.amashort}}-SDK verwendet.  Nach der Einrichtung des SDK können Sie mit der Einrichtung der Authentifizierung und Überwachung für Ihre App beginnen.  Befolgen Sie die Anweisungen für Ihre Entwicklungsplattform für mobile Apps:

* [Android](getting-started-android.html)
* [iOS (Swift-SDK)](getting-started-ios.html)
* [iOS (Objective-C-SDK)](getting-started-ios.html)
* [Cordova](getting-started-cordova.html)
