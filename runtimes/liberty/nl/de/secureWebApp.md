---

copyright:
  years: 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Sichere Java-Webanwendungen schreiben
{: #secure_java_web_app}

Alle Webanwendungen müssen unter Berücksichtigung von Sicherheitsaspekten gestaltet und codiert werden, um das Auftreten schwerwiegender Sicherheitslücken zu vermeiden.
{: shortdesc}

{{site.data.keyword.Bluemix}} bietet eine sichere Starteranwendung, damit Sie sichereren Liberty Java-Code schreiben können und die meisten der XSS-Probleme (XSS, Cross-Site Scripting) vermeiden. Sie können diese [sichere Starteranwendung](https://github.com/IBM-Bluemix/java-secure-app) herunterladen, einen Build erstellen und das Ergebnis lokal und unter {{site.data.keyword.Bluemix_notm}} bereitstellen.

## Warum sollen sichere Web-Apps geschrieben werden?
{: #why}

Eine Sicherheitslücke kann durch unterschiedliche Attacken ausgenutzt werden. Eine Attacke kann Berechtigungsnachweise stehlen, zu Daten- und Funktionsverlust führen, Services unterbrechen und der Reputation und dem Umsatz des Unternehmens schaden. Cross-Site Scripting (XSS) ist eine der bekannten Sicherheitslücken in den meisten Webanwendungen, die vermieden werden muss. 

Anstatt die Theorie von XSS-Attacken und Techniken zu deren Vermeidung vor dem Beginn der Webanwendungsentwicklung zu erlernen, können Sie diese [sichere Starteranwendung](https://github.com/IBM-Bluemix/java-secure-app) verwenden. Die sichere Starteranwendung enthält Codebeispiele aus der Programmierpraxis für Schlüsselsicherheit, die XSS vermeiden, so dass Sie mit der Entwicklung beginnen können, während Sie Techniken zur Vermeidung von XSS erlernen und anwenden.

## So verwenden Sie die Beispielapp für Sicherheit
{: #how}

Sie können die [sichere Starteranwendung](https://github.com/IBM-Bluemix/java-secure-app) als Startpunkt für die neue Liberty-Anwendungsentwicklung verwenden. Beginnen Sie damit, den Code für die XSS-Gegenmaßnahmen in der App nachzuvollziehen und wenden Sie diesen dann auf die Operationen der Anwendungs-API an. Die Gegenmaßnahmen in der sicheren Starteranwendung verhindern, dass böswillige Benutzereingaben Ihre Anwendung auf dem Server und auf dem Browser beschädigen. Dies erfolgt durch die Migration oder Verhinderung von XSS-Attacken. 

Laden Sie zunächst die sichere Starteranwendung herunter, dann erstellen Sie einen Build und stellen das Ergebnis unter Bluemix oder lokal auf dieselbe Weise bereit, wie Sie dies mit der Beispielanwendung [getting-started-java](https://github.com/IBM-Bluemix/get-started-java) getan haben. Wechseln Sie zu [Erste Schritte mit Liberty unter Bluemix](getting-started.html), um mehr über die Builderstellung und Bereitstellung von Anwendungen unter Bluemix zu erfahren. Für den Anfang können Sie diese Schritte verwenden, um die App zu klonen, einen Build zu erstellen und sie auszuführen. 

```
git clone https://github.com/IBM-Bluemix/java-secure-app
cd java-secure-app
mvn install liberty:run-server
```
Die App finden Sie unter http://localhost:9080/GetStartedSecureJava/

## Weitere Informationen
{: more}
Die sichere Starteranwendung enthält **BadServlet.java**. Diese Anwendung zeigt ein Beispiel für unsicheren Code, den Anwendungsentwickler möglicherweise versehentlich schreiben.

Die sichere Starteranwendung enthält außerdem **GoodServlet.java** mit einer Reihe guter und sicherer Beispiele aus der Programmierpraxis wie Eingabevalidierung, Ausgabeverschlüsselung, sichere Einstellungen für HTTP-Header und Sicherheitsrichtlinien für Inhalte (Content Security Policy). Diese Verfahren sind wichtige Maßnahmen gegen XSS. Ihre Anwendung kann auch andere Sicherheitslücken verringern, die durch Injektion und Directory-Traversal-Techniken ausgenutzt werden könnten. 

Weitere Informationen über XSS und Gegenmaßnahmen finden Sie unter [XSS Prevention Cheat Sheet ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://www.owasp.org/index.php/XSS){: new_window}.
