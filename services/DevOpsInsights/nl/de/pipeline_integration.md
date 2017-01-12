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

# {{site.data.keyword.DRA_short}} mit {{site.data.keyword.deliverypipeline}} integrieren
{: #toolchain_configure_pipeline}

Nach dem Hinzufügen von {{site.data.keyword.DRA_full}} zu einer Toolchain und der Definition der von dieser Komponente überwachten Richtlinien müssen Sie {{site.data.keyword.DRA_short}} mit Ihrer Pipeline integrieren.
{:shortdesc}

<!--##Configuring the {{site.data.keyword.deliverypipeline}}

{: #toolchain_integration}
To use {{site.data.keyword.DRA_short}}, add it to any toolchain that uses the {{site.data.keyword.deliverypipeline}}.

1. In {{site.data.keyword.Bluemix_notm}}, on the **Toolchains** tab, open a toolchain.

2. On the toolchain's Overview page, click the add (+) button.

3. In the Tool Integrations section, select **{{site.data.keyword.DRA_short}}**.

4. Click **Create Integration**.

5. In your toolchain, click the {{site.data.keyword.deliverypipeline}} tile. You can configure {{site.data.keyword.DRA_short}} in any number of pipelines.-->

## Pipelinestufen für {{site.data.keyword.DRA_short}} vorbereiten
{: #toolchain_pipeline_props}

Sie müssen mehrere Umgebungseigenschaften in den einzelnen Pipelinestufen erstellen, die Build- oder Bereitstellungsjobs enthalten:

1. Klicken Sie auf die Option für die Stufenkonfiguration und anschließend auf die Option zum Konfigurieren der Stufe.

2. Klicken Sie auf **UMGEBUNGSEIGENSCHAFTEN**.

3. Fügen Sie die drei folgenden Texteigenschaften hinzu und speichern Sie anschließend die Änderungen für die Stufe:

<table><thead>
<tr>
<th>Umgebungseigenschaft</th>
<th>Beschreibung</th>
</tr>
</thead><tbody>
<tr>
<td><code>LOGICAL_APP_NAME</code></td>
<td>Der Name der App wie er in den {{site.data.keyword.DRA_short}}-Dashboards angezeigt wird. </td>
</tr>
<tr>
<td><code>LOGICAL_ENV_NAME</code></td>
<td>Der Name der Umgebung, in der die App ausgeführt wird. Diese Eigenschaft wird für die Kategorisierung der App in {{site.data.keyword.DRA_short}}-Dashboards verwendet.</td>
</tr>
<tr>
<td><code>BUILD_PREFIX</code></td>
<td>Ein Präfix, das zu Builds hinzugefügt wird, die in {{site.data.keyword.DRA_short}}-Dashboards zu sehen sind.</td>
</tr>
</tbody></table>


## Testjobs für {{site.data.keyword.DRA_short}} aktualisieren
{: #toolchain_pipeline_upload}

Rufen Sie zur Einführung die Setup-Informationen eines Testjobs ab.

1. Klicken Sie auf der Stufe, die einen Testjob enthält, auf das Symbol für die Stufenkonfiguration ![Symbol für Konfiguration der Pipelinestufe](images/pipeline-stage-configuration-icon.png). Klicken Sie auf die Option zum Konfigurieren der Stufe.
2. Erstellen Sie einen Job. Wählen Sie als Jobtyp **Test** aus.
3. Wählen Sie einen Testjob mit dem Testertyp 'Einfach' (Simple) aus und kopieren Sie die Informationen, die sich in den Feldern für Testbefehl und Arbeitsverzeichnis befinden, in einen Editor. Diese Informationen benötigen Sie zu einem späteren Zeitpunkt.
4. Ändern Sie im selben Testjob des Typs 'Einfach' (Simple) den Testertyp durch Auswahl von **Erweiterter Tester**.
5. Fügen Sie in das Feld für den Testbefehl die Befehle ein, die Sie aus dem Feld für den Testbefehl des Testjobs 'Einfach' (Simple) kopiert haben.
6. Fügen Sie in das Feld für das Arbeitsverzeichnis den Pfad ein, den Sie aus dem Feld für das Arbeitsverzeichnis des Testjobs 'Einfach' (Simple) kopiert haben.
7. Füllen Sie die übrigen Felder aus, um die Testergebnisse für einen bestimmten Testtyp hochzuladen. Wenn Sie Ergebnisse für einen zweiten Testtyp im selben Job hochladen möchten, müssen Sie auch die Felder ausfüllen, die mit *Additional* markiert sind.

 * Metriktyp
 * Format
 * Position der Ergebnisdatei
8. Klicken Sie auf **Speichern**, um zu der Pipeline zurückzukehren.

Die Werte für die Felder mit dem Typ von Metrik und der Position der Ergebnisdatei müssen dem richtigen Format entsprechen:

<table><thead>
<tr>
<th>Metriktyp</th>
<th>Unterstützte Formate</th>
</tr>
</thead><tbody>
<tr>
<td>Funktionsüberprüfungstest</td>
<td>Mocha, JUnit</td>
</tr>
<tr>
<td>Komponententest</td>
<td>Mocha, JUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Codeabdeckung</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

*Abbildung 1* zeigt einen Testjob, der für die Ausführung von Komponententests, für das Hochladen der Ergebnisse im Mocha-Format sowie für das Hochladen der Codeabdeckungsergebnisse im Istanbul-Format konfiguriert ist.

![Deployment Risk Analytics - Upload-Job](images/DRA_upload_job.png)
*Abbildung 1. Ergebnisse nach DevOps Analytics hochladen*

## {{site.data.keyword.DRA_short}}-Gates in der Pipeline definieren
{: #toolchain_pipeline_gates}

Mit {{site.data.keyword.DRA_short}}-Gates wird überprüft, ob Ihre Testergebnisse die definierte Richtlinie einhalten. Wird die Richtlinie nicht erfüllt, schlägt das {{site.data.keyword.DRA_short}}-Gate fehl. Normalerweise werden Gates am Ende jeder Stufe Ihrer Pipeline platziert. Diese Position ist für die Überprüfung der Qualität des Builds auf Basis Ihrer Richtlinie ideal, um sicherzustellen, dass die Hochstufung von einer Umgebung zu einer anderen sicher ist. Sie können Gates jedoch an einer beliebigen Stelle in der Pipeline platzieren, für die ein bestimmtes Kriterium überprüft werden soll.

1. Klicken Sie auf einer Stufe auf das Symbol für die Stufenkonfiguration ![Symbol für Konfiguration der Pipelinestufe](images/pipeline-stage-configuration-icon.png) und klicken Sie auf die Option zum Konfigurieren der Stufe.
2. Klicken Sie auf **Job hinzufügen**. Wählen Sie als Jobtyp **Test** aus.
3. Geben Sie einen Namen für den neuen Job ein, z. B. *Gate (Komponententest)*.
4. Wählen Sie als Testertyp **{{site.data.keyword.DRA_short}}-Gate** aus.
5. Geben Sie den Umgebungsnamen an. Stellen Sie sicher, dass dieser Wert mit der Definition in Ihren [Umgebungseigenschaften](#toolchain_pipeline_props) übereinstimmt.
6. Definieren Sie den Richtliniennamen, der bei diesem Gate überprüft werden soll.

 Dieser Name muss genau mit einem der von Ihnen definierten Richtliniennamen übereinstimmen. Sie können nur Richtlinien angeben, die in derselben {{site.data.keyword.Bluemix_notm}}-Organisation wie Ihre Toolchain definiert sind.

7. Optional: Damit ein Gate im Empfehlungsmodus funktioniert, müssen Sie die Auswahl des Kontrollkästchens zum Stoppen dieser Stufe beim Fehlschlagen dieses Jobs zurücknehmen. Im Empfehlungsmodus führt {{site.data.keyword.DRA_short}} dieselbe Richtlinienanalyse für das Gate durch und generiert Berichte; doch wenn ein Fehler auftrittt, wird die Pipeline nicht gestoppt.
8. Klicken Sie auf **Speichern**, um zu der Pipeline zurückzukehren.
9. Richten Sie für all Ihre {{site.data.keyword.DRA_short}}-Richtlinien Gates ein; wiederholen Sie dafür dieser Schritte.

![Deployment Risk Analytics-Mocha-Job](images/DRA_gate_job.png)
*Abbildung 2. DevOps Analytics-Gate*

Beginnen Sie nach der Konfiguration der Pipeline mit der Verwendung von {{site.data.keyword.DRA_short}}. Anweisungen hierzu finden Sie im Abschnitt zur [Ausführung der Delivery Pipeline](./pipeline_decision_reports.html#toolchain_reports).
