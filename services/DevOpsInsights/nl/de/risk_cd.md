---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integration mit der Continuous Delivery-Pipeline

Nach dem Hinzufügen von {{site.data.keyword.DRA_short}} zu einer Toolchain und dem Definieren der von dieser Komponente überwachten Richtlinien müssen Sie sie mit {{site.data.keyword.deliverypipeline}} integrieren. Weitere Informationen zu Pipelines finden Sie in der [offiziellen Dokumentation](/docs/services/ContinuousDelivery/pipeline_working.html).

## Pipelinestufen vorbereiten
{: #integrate_pipeline}

Damit Sie Ihr Projekt mit Deployment Risk analysieren können, müssen Sie Staging- und Produktionsstufen in der Pipeline festlegen. Sie definieren diese Stufen mithilfe von Umgebungsvariablen für Text, die sich im jeweiligen Konfigurationsmenü der einzelnen Stufen ![Symbol für Konfiguration der Pipelinestufe](images/pipeline-stage-configuration-icon.png) unter **Umgebungseigenschaften** befinden.

1. Legen Sie für die Staging-Stufe die Eigenschaft `LOGICAL_ENV_NAME` auf `STAGING` fest. 

2. Legen Sie für die Produktionsstufe die Eigenschaft `LOGICAL_ENV_NAME` auf `PRODUCTION` fest. 

Sie können auch die folgenden Eigenschaften zu Stufen hinzufügen, mit denen Ihre App erstellt oder bereitgestellt wird:

* `LOGICAL_APP_NAME`: Definiert den Namen der App im Dashboard.
* `BUILD_PREFIX`: Definiert Text, der den Builds der Stufe als Präfix hinzugefügt wird. Dieser Text erscheint auch im Dashboard. 

## Testjobs hinzufügen
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

## Gates definieren
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

Beginnen Sie nach der Konfiguration der Pipeline mit der Verwendung von {{site.data.keyword.DRA_short}}. 
