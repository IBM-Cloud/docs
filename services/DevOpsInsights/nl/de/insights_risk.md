---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Deployment Risk
{: #gettingstarted}

{{site.data.keyword.DRA_short}} stellt eine Fülle von Informationen zu Ihren Bereitstellungen, insbesondere zu Risiken, bereit. Mit dieser Komponente können Sie den Qualitätsschutz in Ihrer Delivery Pipeline mithilfe von Richtlinien und Gates automatisieren. 
{:shortdesc}

Klicken Sie nach dem Öffnen von {{site.data.keyword.DRA_short}} über die Toolchain auf **Deployment Risk**. Dort erhalten Sie einen Überblick über die Anwendungen in Ihren Staging- und Produktionsumgebungen. Außerdem können Sie Drilldowns durchführen, um mehr zu Codeabdeckung, Testleistung und Sicherheitsberichten zu erfahren. Die Dashboards werden automatisch mit den aktuellen Informationen aus den {{site.data.keyword.DRA_short}}-Tests der Pipelines gefüllt.

## Informationen zu Deployment Risk
{: #about}

Mit Deployment Risk können Sie Qualitätsstandards in Ihrer Toolchain mithilfe von Richtlinien und Gates durchsetzen. Richtlinien umfassen Regeln; Gates setzen Richtlinien um. Sie können beispielsweise eine Richtlinie "Komponententest und Testumfang" erstellen, die verlangt, dass Builds Standards für Komponententests und Testumfang einhalten. Sie fügen dann ein Gate hinzu, das die Richtlinie zu Ihrem Continuous Delivery-Prozess referenziert. Builds, die nicht der Richtlinie entsprechen, werden am Gate gestoppt. 

Deployment Risk kann in Verbindung mit {{site.data.keyword.deliverypipeline}} verwendet werden, was wiederum Teil von {{site.data.keyword.contdelivery_full}} ist, sowie mit Jenkins-Projekten. Auf einer höheren Ebene ähneln sich die Anweisungen zur Verwendung beider Optionen.  

Wenn Sie {{site.data.keyword.deliverypipeline}} verwenden, führen Sie die folgenden Schritte aus:

1. [Erstellen Sie Richtlinien und Regeln](#policies_and_rules) für die {{site.data.keyword.DRA_short}}-Verwaltung.
2. [Bereiten Sie die Pipelinestufen vor](#integrate_pipeline), um sie mit {{site.data.keyword.DRA_short}} zu integrieren.

3. [Erstellen oder bearbeiten Sie Testjobs](#configure_pipeline_jobs) in der Pipeline, mit denen Ergebnisse nach {{site.data.keyword.DRA_short}} hochgeladen werden.
4. [Fügen Sie Gates zu der Pipeline hinzu](#configure_pipeline_gates), die basierend auf diesen Ergebnissen und Ihren Richtlinien Entscheidungen zu Hochstufungen fällen.
5. Führen Sie die Pipeline aus und [zeigen Sie die Ergebnisse an](#view_results).

Wenn Sie Jenkins verwenden, führen Sie die folgenden Schritte aus:

1. [Erstellen Sie Richtlinien und Regeln](#policies_and_rules) für die {{site.data.keyword.DRA_short}}-Verwaltung.
2. [Installieren Sie das Jenkins-Plug-in und konfigurieren Sie es](#integrate_jenkins).
3. [Erstellen Sie Testjobs und Gates gemäß den Anweisungen in der Plug-in-Anleitung](#integrate_jenkins). Die Tests laden Ergebnisse zum Analysieren nach {{site.data.keyword.DRA_short}} hoch und die Gates verwenden diese Ergebnisse für Hochstufungsentscheidungen.
4. Führen Sie das Projekt aus und [zeigen Sie die Ergebnisse an](#view_results). 

Unabhängig davon, wie Sie Ihren Code erstellen und bereitstellen, sind die Ergebnisse gleich: Die Builds, die Standards entsprechen, passieren die Deployment Risk-Gates; Builds, die nicht den angegebenen Standards entsprechen, werden gestoppt. 

## Voraussetzungen
{: #prerequisites}

Für Deployment Risk sind neben der in [Einführung in {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html) beschriebenen Konfiguration einige zusätzliche Konfigurationsschritte erforderlich.

Für die Verwendung von Deployment Risk benötigen Sie zwei Dinge:

* Eine Instanz von {{site.data.keyword.deliverypipeline}} oder ein Jenkins-Projekt
* Tests, mit denen Sie Ihr Projekt bewerten möchten

## Richtlinien und Regeln erstellen
{: #policies_and_rules}

Richtlinien sind Gruppen von Regeln, die die Gates in Ihrer Delivery Pipeline steuern. Entspricht Ihr Code keiner Richtlinie oder überschreitet Ihr Code eine Richtlinie, die an einem bestimmten Gate durchgesetzt wird, wird die Bereitstellung angehalten; dadurch wird verhindert, dass sicherheitsbedenkliche Änderungen freigegeben werden.

Sie können Richtlinien in {{site.data.keyword.DRA_short}} festlegen. Richtlinien werden in der {{site.data.keyword.Bluemix_notm}}-Organisation erstellt, die {{site.data.keyword.DRA_short}} enthält. Alle Anwendungen, die sich in ein und derselben Organisation befinden, können die Richtlinie nutzen. 

### Richtlinien erstellen
{: #create_policies}

Führen Sie zum Erstellen einer Richtlinie die folgenden Schritte aus:

1. Klicken Sie in der linken Navigationsleiste auf **Einstellungen**.

2. Klicken Sie auf **Richtlinien**.

3. Klicken Sie auf **Richtlinie erstellen** und geben Sie anschließend einen Namen und eine Beschreibung für die neue Richtlinie ein.

4. Klicken Sie auf **Weiter**.

4. Fügen Sie mindestens eine Regel zur Richtlinie hinzu:
  1. Klicken Sie auf **Regel zu Richtlinie hinzufügen**.
  2. Wählen Sie den Regeltyp aus.
  3. Geben Sie Details und Bedingungen für die Regel ein.
  4. Klicken Sie auf **Speichern**.

5. Wenn Sie mit dem Hinzufügen von Regeln zu der Richtlinie fertig sind, klicken Sie auf die Option zum Abschließen des Vorgangs.

### Regeln erstellen
{: #creating_rules}

Mit Regeln werden die Kriterien festgelegt, anhand derer Richtlinien Erfolg oder Fehlschlagen bewerten. Sie können beispielsweise eine Richtlinie "Komponententest und Testumfang" erstellen, die eine Regel für Komponententests enthält, die eine 80-prozentige Erfolgsquote für Komponententests fordert, und eine Regel für den Testumfang, die eine 100-prozentige Codeabdeckung verlangt. Wenn Sie ein Gate hinzufügen, das sich auf diese Regel in einer Pipeline bezieht, verhindert das Gate, dass Builds, die nicht beiden Regeln entsprechen, weiter durchgeführt werden können. 

Sie können immer eine erfolgreiche Durchführung verlangen, indem Sie Tests als kritisch markieren. Wählen Sie zum Erstellen einer Regel eine Richtlinie aus und klicken Sie dann auf **Regel zu Richtlinie hinzufügen**. 

#### Regeln für Funktionsüberprüfungstests erstellen
{: #criteria_fvt}

1. Geben Sie eine Beschreibung ein und wählen Sie ein Format aus.

2. Geben Sie an (in Prozent), wie viele Testfälle bestanden haben müssen, damit sie als erfolgreich deklariert werden können.

3. Definieren Sie beliebige kritische Testfälle.

4. Wählen Sie für die Überwachung von Testfallregressionen das entsprechende Kontrollkästchen aus.

5. Klicken Sie auf **Speichern**.


#### Regeln für Komponententests erstellen
{: #criteria_ut}

1. Geben Sie eine Beschreibung ein und wählen Sie ein Format aus.

2. Geben Sie an (in Prozent), wie viele Testfälle bestanden haben müssen, damit sie als erfolgreich deklariert werden können.

3. Definieren Sie beliebige kritische Testfälle.

4. Wählen Sie für die Überwachung von Testfallregressionen das entsprechende Kontrollkästchen aus.

5. Klicken Sie auf **Speichern**.


#### Regeln für Codeabdeckung erstellen
{: #criteria_codecoverage}

1. Geben Sie eine Beschreibung ein und wählen Sie ein Format aus.

2. Geben Sie an (in Prozent), wie viel Codeabdeckung erforderlich ist, damit sie als erfolgreich deklariert werden kann.

3. Wählen Sie für die Überwachung von Codeabdeckungsregressionen das entsprechende Kontrollkästchen aus.

4. Klicken Sie auf **Speichern**.

#### Regeln für statische Sicherheitsscans erstellen
{: #criteria_static}

Sie können {{site.data.keyword.DRA_short}} mit IBM Application Security on Cloud integrieren, um statische Code-Scans und dynamische App-Scans durchzuführen. Weitere Informationen zu Application Security on Cloud finden Sie in der [offiziellen Dokumentation](/docs/services/ApplicationSecurityonCloud/index.html) zu diesem Produkt.

1. Geben Sie eine Beschreibung ein.

2. Geben Sie jeweils die maximale Anzahl von Problemen mit hohem, mittlerem und niedrigem Schweregrad an, die gemäß der Regel zulässig sind. 

3. Klicken Sie auf **Speichern**.

#### Regeln für dynamsische Sicherheitsscans erstellen
{: #criteria_dynamic}

Sie können {{site.data.keyword.DRA_short}} mit {{site.data.keyword.appseccloudfull}} integrieren, um dynamische App-Scans durchzuführen. Weitere Informationen zu Application Security on Cloud finden Sie in der [offiziellen Dokumentation](/docs/services/ApplicationSecurityonCloud/index.html) zu diesem Produkt.

1. Geben Sie eine Beschreibung ein.

2. Geben Sie jeweils die maximale Anzahl von Problemen mit hohem, mittlerem und niedrigem Schweregrad an, die gemäß der Regel zulässig sind. 

3. Klicken Sie auf **Speichern**.

## {{site.data.keyword.deliverypipeline}} konfiguieren 
{: #configuration}

Nach dem Hinzufügen von {{site.data.keyword.DRA_short}} zu einer Toolchain und dem Definieren der von dieser Komponente überwachten Richtlinien müssen Sie sie mit {{site.data.keyword.deliverypipeline}} integrieren. Weitere Informationen zu Pipelines finden Sie in der [offiziellen Dokumentation](/docs/services/ContinuousDelivery/pipeline_working.html).

### Pipelinestufen vorbereiten
{: #integrate_pipeline}

Damit Sie Ihr Projekt mit Deployment Risk analysieren können, müssen Sie Staging- und Produktionstufen in der Pipeline festlegen. Sie definieren diese Stufen mithilfe von Umgebungsvariablen für Text, die sich im jeweiligen Konfigurationsmenü der einzelnen Stufen ![Symbol für Konfiguration der Pipelinestufe](images/pipeline-stage-configuration-icon.png) unter **Umgebungseigenschaften** befinden.

1. Legen Sie für die Staging-Stufe die Eigenschaft `LOGICAL_ENV_NAME` auf `STAGING` fest. 

2. Legen Sie für die Produktionsstufe die Eigenschaft `LOGICAL_ENV_NAME` auf `PRODUCTION` fest. 

Sie können auch die folgenden Eigenschaften zu Stufen hinzufügen, mit denen Ihre App erstellt oder bereitgestellt wird:

* `LOGICAL_APP_NAME`: Definiert den Namen der App im Dashboard.
* `BUILD_PREFIX`: Definiert Text, der den Builds der Stufe als Präfix hinzugefügt wird. Dieser Text erscheint auch im Dashboard. 

### Testjobs hinzufügen
{: #configure_pipeline_jobs}

Sie integrieren {{site.data.keyword.DRA_short}} mithilfe von zwei Arten von Testjobs mit der Pipeline: Mit dem einen Testjob werden Ergebnisse zum Analysieren nach {{site.data.keyword.DRA_short}} hochgeladen. Der andere Testjob sind Gates, mit denen auf die Analyse reagiert wird. 

Zunächst fügen Sie Jobs des Typs 'Erweiterter Tester' zur Pipeline hinzu, um Tests durchzuführen und die Ergebnisse hochzuladen. 

**Hinweis:** Wenn Sie einen Testjob so aktualisieren möchten, dass Ergebnisse nach {{site.data.keyword.DRA_short}} hochgeladen werden, speichern Sie seine Konfigurationen an einer gut zugänglichen Position, bevor Sie fortfahren. Öffnen Sie dann das Konfigurationsmenü des Testjobs und fahren Sie mit Schritt 3 fort. 

1. Klicken Sie für die Stufe, für die Sie den Job zum Hochladen von Ergebnissen hinzufügen möchten, auf das Symbol für die Stufenkonfiguration ![Symbol für Konfiguration der Pipelinestufe](images/pipeline-stage-configuration-icon.png). Klicken Sie auf die Option zum Konfigurieren der Stufe.
2. Erstellen Sie einen Testjob und geben Sie einen Namen für den Job ein. 
3. Wählen Sie als Jobtyp **Erweiterter Tester** aus.
4. Füllen Sie die Felder für den Testbefehl und das Arbeitsverzeichnis so aus, wie Sie es für einen normalen Testjob für eine Pipeline tun würden. 
5. Füllen Sie die übrigen Felder aus, um die Testergebnisse für einen bestimmten Testtyp hochzuladen. 

 1. Wählen Sie den Metriktyp aus, der dem entspricht, was Sie in der {{site.data.keyword.DRA_short}}-Richtlinie definiert haben, die Sie verwenden möchten.
 2. Geben Sie eine Speicherposition für die Ergebnisdatei ein. Diese Position ist relativ zum Arbeitsverzeichnis. 

6. Wenn Sie Ergebnisse für einen zweiten Testtyp im selben Job hochladen möchten, müssen Sie die Felder ausfüllen, die mit *Additional* markiert sind.
7. Klicken Sie auf **Speichern**, um zu der Pipeline zurückzukehren.

Die Werte für die Felder mit dem Typ von Metrik und der Position der Ergebnisdatei müssen dem richtigen Format entsprechen:

<table><thead>
<tr>
<th>Metriktyp</th>
<th>Unterstützte Formate</th>
</tr>
</thead><tbody>
<tr>
<td>Funktionsüberprüfungstest</td>
<td>Mocha, xUnit</td>
</tr>
<tr>
<td>Komponententest</td>
<td>Mocha, xUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Codeabdeckung</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

Abbildung 1 zeigt einen Testjob, der für die Ausführung von Komponententests, für das Hochladen der Ergebnisse im Mocha-Format sowie für das Hochladen der Codeabdeckungsergebnisse im Istanbul-Format konfiguriert ist.

![DevOps Insights - Upload-Job](images/insights_upload_job.png)
*Abbildung 1. Ergebnisse nach DevOps Insights hochladen*

### Gates definieren
{: #configure_pipeline_gates}

Mit {{site.data.keyword.DRA_short}}-Gates wird überprüft, ob Ihre Testergebnisse eine definierte Richtlinie einhalten. Wird die Richtlinie nicht erfüllt, schlägt das {{site.data.keyword.DRA_short}}-Gate standardmäßig fehl. Sie können Gates auch so konfigurieren, dass sie eine beratenden Funktion einnehmen, damit selbst nach einem Ausfall die Pipeline fortgeführt werden kann.

Das Deployment Risk-Dashboard ist nach einem Staging-Bereitstellungsjob auf das Vorhandensein eines Gates angewiesen. Wenn Sie das Dashboard verwenden möchten, stellen Sie sicher, dass nach der Bereitstellung für eine Staging-Umgebung (jedoch vor der Bereitstellung für eine Produktionsumgebung) ein Gate vorhanden ist.

Normalerweise werden Gates vor der Hochstufung von Builds in der Pipeline platziert. Diese Positionen sind für die Überprüfung der Qualität des Builds auf Basis Ihrer Richtlinien ideal, um sicherzustellen, dass die Hochstufung von einer Umgebung zu einer anderen sicher ist. Sie können Gates jedoch an einer beliebigen Stelle in der Pipeline platzieren, für die ein bestimmtes Kriterium überprüft werden soll. Gates, die vor der Bereitstellung in einer Staging-Umgebung liegen, setzen Richtlinien zwar weiter durch, erscheinen jedoch nicht im Deployment Risk-Dashboard.

1. Klicken Sie auf einer Stufe auf das Symbol für die Stufenkonfiguration ![Symbol für Konfiguration der Pipelinestufe](images/pipeline-stage-configuration-icon.png) und klicken Sie auf die Option zum Konfigurieren der Stufe.
2. Klicken Sie auf **Job hinzufügen**. Wählen Sie als Jobtyp **Test** aus.
3. Wählen Sie als Testertyp **{{site.data.keyword.DRA_short}}-Gate** aus.
4. Geben Sie den Umgebungsnamen an. Stellen Sie sicher, dass dieser Wert mit der Definition in Ihren [Umgebungseigenschaften](#toolchain_pipeline_props) übereinstimmt.
5. Geben Sie den Richtlinienname ein, der an diesem Gate überprüft werden soll.

 Dieser Name muss genau mit einem der von Ihnen definierten Richtliniennamen übereinstimmen. Sie können nur Richtlinien angeben, die in derselben {{site.data.keyword.Bluemix_notm}}-Organisation wie Ihre Toolchain definiert sind.

6. Optional: Damit ein Gate im Empfehlungsmodus funktioniert, müssen Sie die Auswahl des Kontrollkästchens zum Stoppen dieser Stufe beim Fehlschlagen dieses Jobs zurücknehmen. Im Empfehlungsmodus führt {{site.data.keyword.DRA_short}} dieselbe Richtlinienanalyse für das Gate durch und generiert Berichte; doch wenn ein Fehler auftrittt, wird die Pipeline nicht gestoppt.
7. Klicken Sie auf **Speichern**, um zu der Pipeline zurückzukehren.
8. Richten Sie für all Ihre {{site.data.keyword.DRA_short}}-Richtlinien Gates ein; wiederholen Sie dafür dieser Schritte.

![Deployment Risk - Mocha-Job](images/insights_gate_job.png)
*Abbildung 2. DevOps Insights-Gate*

Beginnen Sie nach der Konfiguration der Pipeline mit der Verwendung von {{site.data.keyword.DRA_short}}. Anweisungen hierzu finden Sie im Abschnitt zur [Ausführung der Delivery Pipeline](/docs/services/DevOpsInsights/pipeline_decision_reports.html#toolchain_reports).

## Ein Jenkins-Projekt konfigurieren
{: #integrate_jenkins}

Nach dem Hinzufügen von {{site.data.keyword.DRA_full}} zu einer offenen Toolchain und dem Definieren der von dieser Komponente überwachten Richtlinien können Sie sie mit Ihrem Jenkins-Projekt integrieren. 

Das IBM Cloud DevOps-Plug-in für Jenkins integriert Jenkins-Projekte mit Toolchains. Eine *Toolchain* ist eine Gruppe von Toolintegrationen, die Entwicklungs-, Bereitstellungs- und Operationsaufgaben unterstützen. Das Gesamtpotenzial einer Toolchain ist größer als die Summe ihrer einzelnen Toolintegrationen. Offene Toolchains sind Teil des {{site.data.keyword.contdelivery_full}}-Service. Weitere Informationen zum {{site.data.keyword.contdelivery_short}}-Service finden Sie in der [entsprechenden Dokumentation](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html).

Nach der Installation des IBM Cloud DevOps-Plug-ins können Sie Testergebnisse in {{site.data.keyword.DRA_short}} publizieren, automatisierte Qualitätsgates hinzufügen und Ihre Bereitstellungsrisiken verfolgen. Außerdem können Sie Jobbenachrichtigungen an andere Tools, wie Slack und PagerDuty, in Ihrer Toolchain senden. Damit Sie Ihre Bereitstellungen besser überwachen können, können über die Toolchain Bereitstellungsnachrichten zu Git-Commits und deren zugehörige Git- oder JIRA-Probleme hinzugefügt werden. Zudem können Sie Ihre Bereitstellungen auf der Verbindungsseite der Toolchain anzeigen. 

Das Plug-in stellt Aktionen für den Buildabschluss sowie Befehlszeilenschnittstellen für die Unterstützung der Integration zur Verfügung. {{site.data.keyword.DRA_short}} aggregiert und analysiert die Ergebnisse aus Komponententests, Funktionstests, Codeabdeckungstools und dynamischen Sicherheitsscans, um zu bestimmen, ob Ihr Code den vordefinierten Richtlinien an Gates in Ihrem Bereitstellungsprozess entspricht. Entspricht Ihr Code keiner Richtlinie oder überschreitet Ihr Code eine Richtlinie, wird die Bereitstellung angehalten; dadurch wird verhindert, dass sicherheitsbedenkliche Änderungen freigegeben werden. Sie können {{site.data.keyword.DRA_short}} als Sicherheitsnetz für Ihre Continuous Delivery-Umgebung, als Möglichkeit der Implementierung und Verbesserung der Qualitätsstandards über einen Zeitraum hinweg sowie als Datenvisualisierungstool für Informationen zum Projektstatus verwenden.

### Voraussetzungen
{: #jenkins_prerequisites}

Sie müssen über Zugriff auf den Server verfügen, auf dem das Jenkins-Projekt ausgeführt wird.

### Eine Toolchain erstellen
{: #jenkins_create}

Bevor Sie {{site.data.keyword.DRA_short}} mit einem Jenkins-Projekt integrieren können, müssen Sie eine Toolchain erstellen. 

1. Rufen Sie zum Erstellen einer Toolchain die [Seite zum Erstellen einer Toolchain](https://console.ng.bluemix.net/devops/create) auf und befolgen Sie die Anweisungen auf dieser Seite. 

2. Nachdem Sie die Toolchain erstellt haben, fügen Sie {{site.data.keyword.DRA_short}} zu dieser Toolchain hinzu. Anweisungen hierzu finden Sie in der [{{site.data.keyword.DRA_short}}-Dokumentation](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html). 

### Plug-in installieren
{: #jenkins_install}

Laden Sie zunächst das Plug-in von {{site.data.keyword.DRA_short}} herunter.  

1. Klicken Sie auf der Übersichtsseite der Toolchain auf **DevOps Insights**.
2. Klicken Sie auf **Settings** und anschließend auf **Jenkins Plugin Setup**.
3. Befolgen Sie die Anweisungen auf der Seite zum Herunterladen des Plug-ins.

Installieren Sie das Plug-in auf dem Jenkins-Server.

1. Klicken Sie auf **Manage Jenkins &gt; Manage Plugins** und dann auf die Registerkarte **Advanced**.
2. Klicken Sie auf **Choose File** und wählen Sie die Installationsdatei für das IBM Cloud DevOps-Plug-in aus. 
3. Klicken Sie auf **Upload**.
4. Starten Sie Jenkins erneut und prüfen Sie, ob das Plug-in installiert wurde.

### Jenkins-Jobs für das Deployment Risk-Dashboard konfigurieren
{: #jenkins_configure}

Nachdem das Plug-in installiert wurde, können Sie {{site.data.keyword.DRA_short}} in Ihr Jenkins-Projekt integrieren. 

Führen Sie die folgenden Schritte aus, um Deployment Risk-Gates und das Deployment Risk-Dashboard mit Ihrem Projekt verwenden zu können.

1. Öffnen Sie die Konfiguration eines vorhandenen Jobs (z. B. Build, Test oder Bereitstellung).

2. Fügen Sie eine Buildabschlussaktion für den entsprechenden Typ hinzu:

   * Verwenden Sie für Build-Jobs den Typ **Publish build information to IBM Cloud DevOps**.
   
   * Verwenden Sie für Testjobs den Typ **Publish test result to IBM Cloud DevOps**.
   
   * Verwenden Sie für Bereitstellungsjobs den Typ **Publish deployment information to IBM Cloud DevOps**.
   
3. Füllen Sie die erforderlichen Felder aus. Diese können je nach Jobtyp anders sein. 

   * Wählen Sie aus der Liste **Credentials** Ihre {{site.data.keyword.Bluemix_notm}}-ID und Ihr Kennwort aus. Sind diese nicht in Jenkins gespeichert, klicken Sie auf die Option zum Hinzufügen, um sie hinzuzufügen und zu speichern. Testen Sie die Verbindung mit {{site.data.keyword.Bluemix_notm}}, indem Sie auf **Test Connection** klicken.
   
   * Geben Sie im Feld für den Namen des Build-Jobs den Namen Ihres Build-Jobs genau wie in Jenkins an. Lassen Sie dieses Feld leer, wenn der Build-Job zeitlich mit dem Testjob zusammenfällt. Wenn es außerhalb von Jenkins zu dem Build-Job kommt, aktivieren Sie das Kontrollkästchen **Builds are being done outside of Jenkins** und geben Sie die Buildnummer und die Build-URL an.
   
   * Wenn die Tests in der Umgebung in der Buildstufe ausgeführt werden, wählen Sie nur die Buildumgebung aus. Wenn die Tests in der Bereitstellungsstufe ausgeführt werden, wählen Sie die Bereitstellungsumgebung aus und geben Sie den Umgebungsnamen an. Es werden zwei Werte unterstützt: `STAGING` und `PRODUCTION`.
   
   * Geben Sie den Speicherort der Ergebnisdatei im entsprechenden Feld an. Wenn durch den Test keine Ergebnisdatei generiert wird, lassen Sie dieses Feld leer. Durch das Plug-in wird eine auf dem Status des aktuellen Testjobs basierende Standardergebnisdatei hochgeladen.

   Die nachfolgenden Abbildungen zeigen Beispielkonfigurationen:
   
   ![Buildinformationen hochladen](images/Upload-Build-Info.png "Buildinformationen in DRA publizieren")
   *Buildinformationen publizieren*
   
   ![Testergebnis hochladen](images/Upload-Test-Result.png "Testergebnis in DRA publizieren")
   *Testergebnis publizieren*
   
   ![Bereitstellungsinformationen hochladen](images/Upload-Deployment-Info.png "Bereitstellungsinformationen in DRA publizieren")
   *Bereitstellungsinformationen publizieren*

4. Wenn Sie {{site.data.keyword.DRA_short}}-Richtliniengates zum Steuern eines nachfolgenden Bereitstellungsjobs verwenden möchten, fügen Sie eine Buildabschlussaktion des Typs **IBM Cloud DevOps Gate** hinzu. Wählen Sie eine Richtlinie aus und geben Sie den Gültigkeitsbereich der Testergebnisse an. Damit Richtliniengates nachfolgende Bereitstellungen verhindern können, aktivieren Sie das Kontrollkästchen **Fail the build based on the policy rules**. Die folgende Abbildung zeigt eine Beispielkonfiguration:

    ![DevOps Insights-Gate](images/DRA-Gate.png "DevOps Insights-Gate")

5. Führen Sie den Jenkins-Build-Job aus.

6. Zeigen Sie das Deployment Risk-Dashboard, indem Sie [IBM Bluemix DevOps](https://console.ng.bluemix.net/devops) aufrufen, Ihre Toolchain auswählen und auf **DevOps Insights** klicken.

Das Deployment Risk-Dashboard ist nach einem Staging-Bereitstellungsjob auf das Vorhandensein eines Gates angewiesen. Wenn Sie das Dashboard verwenden möchten, stellen Sie sicher, dass nach der Bereitstellung für eine Staging-Umgebung (jedoch vor der Bereitstellung für eine Produktionsumgebung) ein Gate vorhanden ist.
    
### Benachrichtigungen konfigurieren
{: #jenkins_notifications}

Sie können die Jenkins-Jobs so konfigurieren, dass Benachrichtigungen an Tools wie Slack oder PagerDuty gesendet werden, indem Sie die Anweisungen in der entsprechenden [Bluemix-Dokumentation](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins) befolgen.

Das nachfolgende Beispiel zeigt, wie Sie `ICD_WEBHOOK_URL` für Jobkonfigurationen konfigurieren:
![Parameter 'ICD_WEBHOOK_URL festlegen](images/Set-Parameterized-Webhook.png "Parametrisierten WebHook festlegen")

Dieses Beispiel veranschaulicht, wie Sie Buildabschlussaktionen für Jobbenachrichtigungen konfigurieren können:
![Buildabschlussaktionen für WebHook-Benachrichtigung](images/PostBuild-WebHookNotification.png "WebHook-Benachrichtigung in Buildabschlussaktionen konfigurieren")

## Ergebnisse anzeigen
{: #view_results}

Nach der Pipeline-Ausführung beginnt {{site.data.keyword.DRA_short}} für die Erstellung einer Baseline mit der Erfassung und Analyse der Testergebnisse aus der Pipeline. Es werden Daten aus allen nachfolgenden Ausführungen erfasst und mit den vorherigen Ergebnissen verglichen. In Entscheidungsgates werden diese Daten verwendet, um zu bestimmen, wann eine Bereitstellung gestoppt werden soll. 

Sie können sich Ihre Bereitstellung und Gatebewertungsdaten im Deployment Risk-Dashboard ansehen. Öffnen Sie zum Aufrufen des Dashboards {{site.data.keyword.DRA_short}} und klicken Sie im seitlichen Menü auf **Deployment Risk**.

Wenn Sie eine {{site.data.keyword.contdelivery_short}}-Pipeline verwenden, können Sie einzelne Berichte zur Gateausführung über die Pipeline selbst anzeigen. Führen Sie die folgenden Schritte aus, um den Entscheidungsbericht für ein Gate aus der Pipeline anzuzeigen:

1. Klicken Sie bei der Stufe mit dem zu überprüfenden Gate auf die Option zum Anzeigen von Protokollen und Verlauf.

2. Klicken Sie im Job, der das Gate enthält, auf den Namen des Gates.

3. Suchen Sie in der Protokollansicht nach der Nachricht `Check {{site.data.keyword.DRA_short}} report here` und klicken Sie auf den Link, um den Bericht zu öffnen.






