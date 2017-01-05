---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Richtlinien definieren
{: #criteria}

Mit {{site.data.keyword.DRA_short}} ist die Definition der Richtlinien für Ihre Anwendung eine einfache Aufgabe. Führen Sie zur Einführung die folgenden Schritte aus:
{:shortdesc}

1. Klicken Sie im seitlichen Menü auf **Richtlinie**.

2. Klicken Sie auf **Richtlinie erstellen (+)** und geben Sie anschließend einen Namen und eine Beschreibung für die neue Richtlinie ein.

3. Klicken Sie auf **Weiter**.

4. Fügen Sie mindestens eine Regel zur Richtlinie hinzu:
  1. Klicken Sie auf **Regel erstellen (+)**.
  2. Wählen Sie den Regeltyp aus.
  3. Geben Sie Details und Bedingungen für die Regel ein.
  4. Klicken Sie auf **Speichern**.

5. Wenn Sie mit dem Hinzufügen von Regeln zu der Richtlinie fertig sind, klicken Sie auf die Option zum Abschließen des Vorgangs.

Richtlinien werden in der {{site.data.keyword.Bluemix_notm}}-Organisation erstellt, zu der {{site.data.keyword.DRA_short}} hinzugefügt wurde. Alle Anwendungen, die sich in ein und derselben Organisation befinden, können die Richtlinie nutzen.

{{site.data.keyword.DRA_short}} unterstützt die folgenden Typen von Metriken und Formaten:

* Funktionsüberprüfungstest (Mocha, JUnit)
* Komponententest (Mocha, JUnit, Karma/Mocha)
* Codeabdeckung (Istanbul als JSON-Übersichtsberichtsformat, Blanket.js)

{{site.data.keyword.DRA_short}} unterstützt auch Selenium- und Jasmine-Tests. Diese Tests müssen in den offiziell unterstützten Tools wie JUnit, xUnit und Mocha integriert sein. Weitere Informationen zur gemeinsamen Verwendung von {{site.data.keyword.deliverypipeline}}, {{site.data.keyword.DRA_short}} und Selenium finden Sie unter [Running Selenium tests from the command line on a delivery pipeline](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/).

Für Elemente mit Testfällen können Sie kritische Testfälle angeben; dabei handelt es sich um Tests, die unabhängig vom zulässigen Prozentsatz bestanden werden müssen. Namen für kritische Testfälle müssen mit dem Attribut `full title` des Testfalls übereinstimmen:    
* Bei Karma/Mocha-Tests sind die Beschreibungszeichenfolgen `describe()` und `it()` durch Leerzeichen verbunden
* Bei JUnit-Tests sind Paketname, Klassenname und Funktionsname durch Leerzeichen verbunden    

Sie können Sauce Labs mit {{site.data.keyword.DRA_short}} verwenden; fügen Sie hierfür die Sauce Labs-Integration zu Ihrer Pipeline hinzu. Integrieren Sie anschließend die Umgebungsvariablen `SAUCE_USERNAME` und `SAUCE_ACCESS_KEY` als Berechtigungsnachweise in die Selenium-Tests.

Sie können die vollständigen Titel aller Tests nach einer Ausführung in den Protokollen sehen.  

Anmerkungen:
* {{site.data.keyword.DRA_short}} unterstützt keine kritischen Tests, die einen Bindestrich im vollständigen Titel enthalten.    
* Wenn Sie Ihren Organisationsnamen ändern, müssen Sie die Richtlinien, die dem vorherigen Namen zugeordnet waren, neu erstellen. Der Zugriff auf Entscheidungsberichte, die vor der Namensänderung generiert wurden, geht sonst verloren.

## Regeln für Funktionsüberprüfungstests erstellen
{: #criteria_fvt}

1. Geben Sie eine Beschreibung ein und wählen Sie ein Format aus.

2. Geben Sie an (in Prozent), wie viele Testfälle bestanden haben müssen, damit sie als erfolgreich deklariert werden können.

3. Definieren Sie beliebige kritische Testfälle.

4. Wählen Sie für die Überwachung von Testfallregressionen das entsprechende Kontrollkästchen aus.

5. Klicken Sie auf **Speichern**.


## Regeln für Komponententests erstellen
{: #criteria_ut}

1. Geben Sie eine Beschreibung ein und wählen Sie ein Format aus.

2. Geben Sie an (in Prozent), wie viele Testfälle bestanden haben müssen, damit sie als erfolgreich deklariert werden können.

3. Definieren Sie beliebige kritische Testfälle.

4. Wählen Sie für die Überwachung von Testfallregressionen das entsprechende Kontrollkästchen aus.

5. Klicken Sie auf **Speichern**.


## Regeln für Codeabdeckung erstellen
{: #criteria_codecoverage}

1. Geben Sie eine Beschreibung ein und wählen Sie ein Format aus.

2. Geben Sie an (in Prozent), wie viel Codeabdeckung erforderlich ist, damit sie als erfolgreich deklariert werden kann.

3. Wählen Sie für die Überwachung von Codeabdeckungsregressionen das entsprechende Kontrollkästchen aus.

4. Klicken Sie auf **Speichern**.
