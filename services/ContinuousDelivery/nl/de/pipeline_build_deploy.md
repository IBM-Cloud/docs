---

copyright:
  years: 2016, 2017
lastupdated: "2017-3-16"
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

# Builderstellung und Bereitstellung
{: #deliverypipeline_build_deploy}

Der IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}}-Service ermöglicht es Ihnen, einen reproduzierbaren, kontinuierlichen Integrationsprozess und einen Continuous Delivery-Prozess zu implementieren.
{:shortdesc}

Führen Sie die folgenden Aufgaben aus, um eine Pipeline zu erstellen und zu konfigurieren.

## Eine Stage hinzufügen
{: #deliverypipeline_add_stage}

1. Klicken Sie auf der Seite 'Pipeline' auf **Stage hinzufügen**. Die Seite 'Stagekonfiguration' wird angezeigt.
2. Konfigurieren Sie die Stage.
  1. Wählen Sie auf der Registerkarte **EINGABE** eine Eingabe für die Stage aus.
  2. Fügen Sie auf der Registerkarte **JOBS** mindestens einen Job hinzu und konfigurieren Sie diesen. Die erste Stage verfügt in der Regel mindestens über einen Buildjob.
3. Klicken Sie auf **Speichern**.

## Einen Job zu einer Stage hinzufügen
{: #deliverypipeline_add_job}

1. Klicken Sie in der Stage auf das Symbol **Stagekonfiguration** und dann auf **Stage konfigurieren**.
2. Klicken Sie auf die Registerkarte **JOBS**.
3. Klicken Sie auf **Job hinzufügen**. Wählen Sie den Typ von Job aus, der hinzugefügt werden soll.
4. Konfigurieren Sie den Job.
5. Klicken Sie auf **Speichern**.

![Einen Job zu einer Stage hinzufügen](images/AddJob2.png)

## Eine Stage ausführen
{: #deliverypipeline_run_stage}

Sie können eine Stage manuell ausführen, indem Sie auf das Symbol **Stage ausführen** auf der Seite 'Pipeline' klicken.

![Auf das Symbol für die Ausführung der Stage in der Stage klicken](images/RunStage.png)

Sie können über eine von zwei Möglichkeiten auch bedarfsgerechte Builds und Bereitstellungen von der Seite für Buildprotokolle anfordern.
* Ziehen Sie einen Build auf die Box, die sich unter einer konfigurierten Stage befindet.
* Klicken Sie neben einem Build auf das Symbol **Senden an** und wählen Sie dann einen Bereich aus, in dem die Bereitstellung erfolgen soll.
  ![Die Stage für die Ausführung mit diesem Buildsymbol](images/deploy_to.png)

Klicken Sie in der Stage auf **Protokolle und Verlauf anzeigen**, um eine aktive Stage abzubrechen. Klicken Sie in der Liste der Jobs auf die Nummer des aktiven Jobs und anschließend auf **ABBRECHEN**. Sie können Jobs auch einzeln abbrechen, indem Sie auf einen Job und anschließend auf das Symbol **Abbrechen** klicken, oder indem Sie auf das Symbol **Stopp** neben einem Job in seiner Stage klicken.

## Eine App bereitstellen
{: #deliverypipeline_deploy}

Ein ordnungsgemäß konfigurierter Bereitstellungsjob stellt Ihre App immer dann in Ihrem Ziel bereit, wenn der Job ausgeführt wird. Um einen Bereitstellungsjob manuell auszuführen, klicken Sie auf das Symbol **Stage ausführen** der Stage, in der sich der Job befindet.

###Eingabeüberarbeitungen
Wenn Sie eine Stage manuell ausführen, oder wenn sie ausgeführt wird, weil eine Stage vor ihr abgeschlossen wurde, wählt die aktive Stage ihre Eingabeüberarbeitung aus. In der Regel ist die Eingabeüberarbeitung eine Buildnummer. Zur Auswahl der Eingabeüberarbeitung erfüllt die Stage die folgenden Bedingungen:

* Falls eine bestimmte Überarbeitung ausgewählt ist, wird diese verwendet.
* Falls keine bestimmte Überarbeitung ausgewählt ist, werden vorherige Stages durchsucht, bis eine Stage gefunden wurde, die dieselbe Eingabe verwendet. Die letzte erfolgreich ausgeführte Überarbeitung dieser Eingabe wird gesucht und verwendet.
* Falls keine bestimmte Überarbeitung angegeben ist und keine anderen Stages die angegebene Quelle als Eingabe verwenden, wird die letzte Überarbeitung der Eingabe verwendet.

**Tipp:** Sie können einen vorherigen Build bereitstellen. Klicken Sie in der Stage, die den Build enthält, auf **Protokolle und Verlauf anzeigen**. Klicken Sie auf der Seite, die geöffnet wird, um die Ausführungsnummer zu erweitern, und klicken Sie anschließend auf den Buildjob. Klicken Sie auf **Senden an** und wählen Sie ein Ziel aus.

###Services zu Apps hinzufügen
Sie können Services zu Ihren Apps hinzufügen und diese Services von Ihrem Bluemix-Dashboard aus oder über die Cloud Foundry-CLI (CLI = Befehlszeilenschnittstelle) verwalten. Sie können für Pipeline-Jobs auch Cloud Foundry-CLI-Befehle in Scripts ausgeben. Sie können zum Beispiel einen Service zu einer App im Script eines Bereitstellungsjobs hinzufügen. Weitere Informationen zum Hinzufügen von Services finden Sie unter [Hinzufügen eines Service zur Anwendung](/docs/services/reqnsi.html#add_service).

## Protokolle anzeigen
{: #deliverypipeline_view_logs}

Sie können die Protokolle für Jobs anzeigen und Stages, die gerade ausgeführt werden, auf der Seite mit dem Stageverlaufsprotokoll anzeigen.

Um das Protokoll eines Jobs anzuzeigen, klicken Sie auf den Job. Alternativ können Sie in einer Stage auf **Protokolle und Verlauf anzeigen** klicken.

Um das Laufzeitprotokoll einer bereitgestellten Anwendung anzuzeigen, klicken Sie auf **Laufzeitprotokoll anzeigen**.

![Bereiche in einer Stagekachel, auf die Sie klicken können, um relevante Protokolle zu öffnen](images/view_logs_and_history.png)

Zusätzlich zu den Jobprotokollen können Sie Komponententestergebnisse, generierte Artefakte und Codeänderungen für beliebige Buildjobs anzeigen.

Sie können ferner eine Stage auf der Seite mit dem Stageverlaufsprotokoll ausführen, abbrechen oder konfigurieren. Klicken Sie auf **Ausführen**, um eine Stage auszuführen, oder klicken Sie auf **Konfigurieren**, um eine Stage zu konfigurieren. Während der Ausführung einer Stage können Sie diese abbrechen, indem Sie auf die Ausführungsnummer und anschließend auf **Abbrechen** klicken.
