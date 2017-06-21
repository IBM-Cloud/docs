---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Richtlinien definieren
{: #policies}

Richtlinien steuern die Gates in Ihrer Continuous Delivery-Pipeline. Entspricht Ihr Code keiner Richtlinie oder überschreitet Ihr Code eine Richtlinie, die an einem bestimmten Gate durchgesetzt wird, wird die Bereitstellung angehalten; dadurch wird verhindert, dass sicherheitsbedenkliche Änderungen freigegeben werden. 
{:shortdesc}

Sie können Richtlinien in {{site.data.keyword.DRA_short}} festlegen. Richtlinien werden in der {{site.data.keyword.Bluemix_notm}}-Organisation erstellt, die {{site.data.keyword.DRA_short}} enthält. Alle Anwendungen, die sich in ein und derselben Organisation befinden, können die Richtlinie nutzen. 

Führen Sie zum Definieren einer Richtlinie die folgenden Schritte aus:

1. Klicken Sie in der linken Navigationsleiste auf **Einstellungen**.

2. Klicken Sie auf **Richtlinie**.

3. Klicken Sie auf **Richtlinie erstellen** und geben Sie anschließend einen Namen und eine Beschreibung für die neue Richtlinie ein.

4. Klicken Sie auf **Weiter**.

4. Fügen Sie mindestens eine Regel zur Richtlinie hinzu:
  1. Klicken Sie auf **Regel zu Richtlinie hinzufügen**.
  2. Wählen Sie den Regeltyp aus.
  3. Geben Sie Details und Bedingungen für die Regel ein.
  4. Klicken Sie auf **Speichern**.

5. Wenn Sie mit dem Hinzufügen von Regeln zu der Richtlinie fertig sind, klicken Sie auf die Option zum Abschließen des Vorgangs.

## Regeln erstellen
{: #criteria}

Mit Regeln werden die Kriterien festgelegt, anhand derer Richtlinien Erfolg oder Fehlschlagen bewerten. Sie können beispielsweise eine Richtlinie "Komponententest und Testumfang" erstellen, die eine Regel für Komponententests enthält, die eine 80-prozentige Erfolgsquote für Komponententests fordert, und eine Regel für den Testumfang, die eine 100-prozentige Codeabdeckung verlangt. Wenn Sie ein Gate hinzufügen, das sich auf diese Regel in einer Pipeline bezieht, verhindert das Gate, dass Builds, die nicht beiden Regeln entsprechen, weiter durchgeführt werden können. 

Sie können immer eine erfolgreiche Durchführung verlangen, indem Sie Tests als kritisch markieren. Wählen Sie zum Erstellen einer Regel eine Richtlinie aus und klicken Sie dann auf **Regel zu Richtlinie hinzufügen**. 

### Regeln für Funktionstests erstellen
{: #criteria_fvt}

1. Geben Sie eine Beschreibung ein und wählen Sie ein Format aus.

2. Geben Sie an (in Prozent), wie viele Testfälle bestanden haben müssen, damit sie als erfolgreich deklariert werden können.

3. Definieren Sie beliebige kritische Testfälle.

4. Wählen Sie für die Überwachung von Testfallregressionen das entsprechende Kontrollkästchen aus.

5. Klicken Sie auf **Speichern**.


### Regeln für Komponententests erstellen
{: #criteria_ut}

1. Geben Sie eine Beschreibung ein und wählen Sie ein Format aus.

2. Geben Sie an (in Prozent), wie viele Testfälle bestanden haben müssen, damit sie als erfolgreich deklariert werden können.

3. Definieren Sie beliebige kritische Testfälle.

4. Wählen Sie für die Überwachung von Testfallregressionen das entsprechende Kontrollkästchen aus.

5. Klicken Sie auf **Speichern**.


### Regeln für Codeabdeckung erstellen
{: #criteria_codecoverage}

1. Geben Sie eine Beschreibung ein und wählen Sie ein Format aus.

2. Geben Sie an (in Prozent), wie viel Codeabdeckung erforderlich ist, damit sie als erfolgreich deklariert werden kann.

3. Wählen Sie für die Überwachung von Codeabdeckungsregressionen das entsprechende Kontrollkästchen aus.

4. Klicken Sie auf **Speichern**.

### Regeln für statische Sicherheitsscans erstellen
{: #criteria_static}

1. Geben Sie eine Beschreibung ein.

2. Geben Sie jeweils die maximale Anzahl von Problemen mit hohem, mittlerem und niedrigem Schweregrad an, die gemäß der Regel zulässig sind. 

3. Klicken Sie auf **Speichern**.

### Regeln für dynamische Sicherheitsscans erstellen
{: #criteria_dynamic}

1. Geben Sie eine Beschreibung ein.

2. Geben Sie jeweils die maximale Anzahl von Problemen mit hohem, mittlerem und niedrigem Schweregrad an, die gemäß der Regel zulässig sind. 

3. Klicken Sie auf **Speichern**.

## Formate und Tools für Testergebnisse

{{site.data.keyword.DRA_short}} unterstützt die folgenden Typen von Metriken und Formaten:

* Funktionsüberprüfungstest (Mocha, xUnit)
* Komponententest (Mocha, xUnit, Karma/Mocha)
* Codeabdeckung (Istanbul als JSON-Übersichtsberichtsformat, Blanket.js)

{{site.data.keyword.DRA_short}} unterstützt auch Selenium- und Jasmine-Tests. Diese Tests müssen in den offiziell unterstützten Tools wie xUnit und Mocha integriert sein. Weitere Informationen zur gemeinsamen Verwendung von {{site.data.keyword.deliverypipeline}}, {{site.data.keyword.DRA_short}} und Selenium finden Sie unter [Running Selenium tests from the command line on a delivery pipeline](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/).

Für Elemente mit Testfällen können Sie kritische Testfälle angeben; dabei handelt es sich um Tests, die unabhängig vom zulässigen Prozentsatz bestanden werden müssen. Namen für kritische Testfälle müssen mit dem Attribut `full title` des Testfalls übereinstimmen.    
* Bei Karma/Mocha-Tests sind die Beschreibungszeichenfolgen `describe()` und `it()` durch Leerzeichen verbunden.
* Bei xUnit-Tests sind Paketname, Klassenname und Funktionsname durch Leerzeichen verbunden. Dies wird durch das folgende Beispiel veranschaulicht:
  ```
  <testsuites package="test">
    <testsuite package="otc-api" name="PUT Service Instances - Test Setup" tests="2" failures="0" errors="0">
      <testcase name="#1 Authorization passed for mock user: idsb3t1@us.ibm.com"/>
      <testcase name="#2 Authorization passed for mock user: idsb3t4@us.ibm.com"/>
    </testsuite>
  </testsuite>
  ```
  Dieses Beispiel generiert die folgenden Testfallnamen:
  ```
  test otc-api PUT Service Instances - Test Setup #1 Authorization passed for mock user: idsb3t1@us.ibm.com
  test otc-api PUT Service Instances - Test Setup #2 Authorization passed for mock user: idsb3t1@us.ibm.com
  ```

Sie können Sauce Labs mit {{site.data.keyword.DRA_short}} verwenden; fügen Sie hierfür die Sauce Labs-Toolintegration zu Ihrer Pipeline hinzu. Integrieren Sie anschließend die Umgebungsvariablen `SAUCE_USERNAME` und `SAUCE_ACCESS_KEY` als Berechtigungsnachweise in die Selenium-Tests.

Sie können die vollständigen Titel aller Tests nach einer Ausführung in den Protokollen sehen.  

**Anmerkungen:**
* {{site.data.keyword.DRA_short}} unterstützt keine kritischen Tests, die einen Bindestrich im vollständigen Titel enthalten.    
* Wenn Sie Ihren Organisationsnamen ändern, müssen Sie die Richtlinien, die dem vorherigen Namen zugeordnet waren, neu erstellen. Der Zugriff auf Entscheidungsberichte, die vor der Namensänderung generiert wurden, geht sonst verloren.

## Entscheidungsberichte anzeigen    
{: #DI_decision_reports}

Nach der Pipeline-Ausführung beginnt {{site.data.keyword.DRA_short}} für die Erstellung einer Baseline mit der Erfassung und Analyse der Testergebnisse aus der Pipeline. Es werden Daten aus allen nachfolgenden Ausführungen erfasst und mit den vorherigen Ergebnissen verglichen. In Entscheidungsgates werden diese Daten verwendet, um zu bestimmen, wann eine Bereitstellung gestoppt werden soll. 

Führen Sie die folgenden Schritte aus, um den Entscheidungsbericht für ein Gate aus der Pipeline anzuzeigen:

   1. Klicken Sie bei der Stufe mit dem zu überprüfenden Gate auf die Option zum Anzeigen von Protokollen und Verlauf.

   2. Klicken Sie im Job, der das Gate enthält, auf den Namen des Gates.

   3. Suchen Sie in der Protokollansicht nach der Nachricht `Check {{site.data.keyword.DRA_short}} report here` und klicken Sie auf den Link, um den Bericht zu öffnen.
