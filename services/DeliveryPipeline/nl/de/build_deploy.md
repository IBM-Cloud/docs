---

copyright:
  years: 2016

---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Builderstellung und Bereitstellung von Pipelines
{: #deliverypipeline_build_deploy}
Letzte Aktualisierung: 29. August 2016
{: .last-updated}

Der IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}}-Service ermöglicht es Ihnen, einen reproduzierbaren, kontinuierlichen Integrationsprozess und einen Continuous Delivery-Prozess zu implementieren.
{:shortdesc}

Führen Sie die folgenden Aufgaben aus, um eine Pipeline zu erstellen und zu konfigurieren.

## Eine Phase hinzufügen
{: #deliverypipeline_add_stage}

1. In der Pipeline: Klicken Sie auf der Seite 'Alle Phasen' auf **Phase hinzufügen**. Die Seite 'Phasekonfiguration' wird angezeigt.
2. Konfigurieren Sie die Phase.
  1. Wählen Sie auf der Registerkarte **EINGABE** eine Eingabe für die Phase aus.
  2. Fügen Sie auf der Registerkarte **JOBS** mindestens einen Job hinzu und konfigurieren Sie diesen. Die erste Phase verfügt in der Regel mindestens über einen Buildjob.
3. Klicken Sie auf **Speichern**.

## Einen Job zu einer Phase hinzufügen
{: #deliverypipeline_add_job}

1. Klicken Sie in der Phase auf das Symbol **Phasenkonfiguration** und dann auf **Phase konfigurieren**.
2. Klicken Sie auf die Registerkarte **JOBS**.
3. Klicken Sie auf **Job hinzufügen**. Wählen Sie den Typ von Job aus, der hinzugefügt werden soll.
4. Konfigurieren Sie den Job.
5. Klicken Sie auf **Speichern**.

![Einen Job zu einer Phase hinzufügen](./images/AddJob.png)

## Eine Phase ausführen
{: #deliverypipeline_run_stage}

Sie können eine Phase manuell ausführen, indem Sie auf das Symbol **Phase ausführen** in der Pipeline auf der Seite 'Alle Phasen' klicken.

![Auf das Symbol für die Ausführung der Phase in der Phase klicken](./images/RunStage.png)

Sie können über eine von zwei Möglichkeiten auch bedarfsgerechte Builds und Bereitstellungen von der Seite für Buildprotokolle anfordern.
* Ziehen Sie einen Build auf die Box, die sich unter einer konfigurierten Phase befindet.
* Klicken Sie neben einem Build auf das Symbol **Senden an** und wählen Sie dann einen Bereich aus, in dem die Bereitstellung erfolgen soll.
  ![Die Phase für die Ausführung mit diesem Buildsymbol](./images/deploy_to.png)

Klicken Sie in der Phase auf **Protokolle und Verlauf anzeigen**, um eine aktive Phase abzubrechen. Klicken Sie in der Liste der Jobs auf die Nummer des aktiven Jobs und anschließend auf **ABBRECHEN**. Sie können Jobs auch einzeln abbrechen, indem Sie auf einen Job und anschließend auf das Symbol **Abbrechen** klicken, oder indem Sie auf das Symbol **Stopp** neben einem Job in seiner Phase klicken.

## Eine App bereitstellen
{: #deliverypipeline_deploy}

Ein ordnungsgemäß konfigurierter Bereitstellungsjob stellt Ihre App immer dann in Ihrem Ziel bereit, wenn der Job ausgeführt wird. Um einen Bereitstellungsjob manuell auszuführen, klicken Sie auf das Symbol **Phase ausführen** der Phase, in der sich der Job befindet.

###Eingabeüberarbeitungen
Wenn Sie eine Phase manuell ausführen, oder wenn sie ausgeführt wird, weil eine Phase vor ihr abgeschlossen wurde, wählt die aktive Phase ihre Eingabeüberarbeitung aus. In der Regel ist die Eingabeüberarbeitung eine Buildnummer. Zur Auswahl der Eingabeüberarbeitung führt die Phase den folgenden Prozess aus:

1. Falls eine bestimmte Überarbeitung ausgewählt ist, wird diese verwendet.
2. Falls keine bestimmte Überarbeitung ausgewählt ist, werden vorherige Phasen durchsucht, bis eine Phase gefunden wurde, die dieselbe Eingabe verwendet. Die letzte erfolgreich ausgeführte Überarbeitung dieser Eingabe wird gesucht und verwendet.
3. Falls keine bestimmte Überarbeitung angegeben ist und keine anderen Phasen die angegebene Quelle als Eingabe verwenden, wird die letzte Überarbeitung der Eingabe verwendet.

**Tipp:** Sie können einen vorherigen Build bereitstellen. Klicken Sie in der Phase, die den Build enthält, auf **Protokolle und Verlauf anzeigen**. Klicken Sie auf der Seite, die geöffnet wird, um die Ausführungsnummer zu erweitern, und klicken Sie anschließend auf den Buildjob. Klicken Sie auf **Senden an** und wählen Sie ein Ziel aus.

###Services zu Apps hinzufügen
Sie können Services zu Ihren Apps hinzufügen und diese Services von Ihrem Bluemix Dashboard oder von der Cloud Foundry-CLI (CLI = Befehlszeilenschnittstelle) verwalten. Sie können für DevOps Services-Pipelinejobs auch Cloud Foundry-CLI-Befehle in Scripts ausgeben. Sie können zum Beispiel einen Service zu einer App im Script eines Bereitstellungsjobs hinzufügen. Weitere Informationen zum Hinzufügen von Services finden Sie unter [Hinzufügen eines Service zur Anwendung](https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service).

## Protokolle anzeigen
{: #deliverypipeline_view_logs}

Sie können die Protokolle für Jobs anzeigen und Sie können auf der Seite mit dem Phasenverlaufsprotokoll Phasen anzeigen, die gerade ausgeführt werden.

Um das Protokoll eines Jobs anzuzeigen, klicken Sie auf den Job. Alternativ können Sie in einer Phase auf **Protokolle und Verlauf anzeigen** klicken.

Um das Laufzeitprotokoll einer bereitgestellten Anwendung anzuzeigen, klicken Sie auf **Laufzeitprotokoll anzeigen**.

![Bereiche in einer Phasekachel, auf die Sie klicken können, um relevante Protokolle zu öffnen](./images/view_logs_and_history.png)

Zusätzlich zu den Jobprotokollen können Sie Komponententestergebnisse, generierte Artefakte und Codeänderungen für beliebige Buildjobs anzeigen.

Sie können ferner eine Phase auf der Seite mit dem Phasenverlaufsprotokoll ausführen, abbrechen oder konfigurieren. Klicken Sie im oberen Teil der Seite auf **Ausführen**, um eine Phase auszuführen, oder auf **KONFIGURIEREN**, um eine Phase zu konfigurieren. Während der Ausführung einer Phase können Sie diese abbrechen, indem Sie auf die Ausführungsnummer klicken und anschließend auf 'ABBRECHEN'.

![Auf eine Ausführungsnummer einer Phase klicken, um diesen auf der Protokollseite der Phasen auszuwählen. ](./images/click_stage_run_number.png)

<!--
[1]: https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest
[2]: https://www.ng.bluemix.net/docs/#services/DeliveryPipeline/index.html#getstartwithCD
[3]: http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push
[4]: https://console.ng.bluemix.net/?ace_base=true/#/pricing/cloudOEPaneId=pricing
[5]: ./images/open_logs.png
[6]: #manifests
[7]: ./images/runbar-annotated-dark.png
[8]: ./images/input_tab_only_execute.png
[9]: ./images/deploy_to.png
[10]: ./images/view_logs_and_history.png
[11]: ./images/play_button.png
[12]: ./images/basicAnimate.gif
[13]: ./images/AddStage.png
[14]: ./images/AddJob.png
[15]: ./images/jobs.png
[16]: ./images/RunStage.png
[17]: https://www.ng.bluemix.net/docs/starters/container_pipeline.html#container_pipeline
[18]: ../../../tutorials/basicbuild
[19]: #add_stage
[20]: #add_job
[21]: ../deploy_ext
[22]: ./images/pipeline_settings_icon.png
[23]: https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service
[24]: ../deploy_var
[25]: ./images/click_stage_run_number.png
[26]: ./images/diagram.jpg

-->
