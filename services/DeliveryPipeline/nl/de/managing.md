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

# Pipelines verwalten
{: #deliverypipeline_managing}
Letzte Aktualisierung: 30. August 2016
{: .last-updated}

Sie können Integrationen von IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} verwalten, konfigurieren und erweitern.
{:shortdesc}

Führen Sie die folgenden Aufgaben aus, um eine Pipeline zu verwalten, zu konfigurieren und zu erweitern.

## Zugriff steuern
{: #deliverypipeline_access}

Sie können beschränken, wer die Phase ausführen oder eine Pipeline ändern darf. Wechseln Sie dazu auf die Seite mit den Einstellungen für die Pipeline, indem Sie auf das Symbol **Phasenkonfiguration** auf der Seite 'Pipeline: Alle Phasen' klicken.

![Das Zahnradsymbol für die Einstellungen der Pipeline](./images/pipeline_settings.png)

## Umgebungseigenschaften und Ressourcen
{: #deliverypipeline_envprop}

Sie können Umgebungseigenschaften und vorinstallierte Ressourcen verwenden, um mit den {{site.data.keyword.deliverypipeline}}-Services zu interagieren. Möglicherweise integrieren Sie diese in ein Job-Script oder einen Testbefehl. Weitere Informationen finden Sie unter [Umgebungseigenschaften und Ressourcen für den {{site.data.keyword.deliverypipeline}}-Service](./deploy_var.html).

Sie können auf der Registerkarte **Umgebungseigenschaften** Ihre eigenen Umgebungseigenschaften zu einer Phase hinzufügen. Umgebungseigenschaften stehen für jeden Job in einer Phase zur Verfügung.

Sie können vier Typen von Eigenschaften von der Registerkarte 'Umgebungseigenschaften' hinzufügen:
* **Text** (Text): Ein Eigenschaftsschlüssel mit einem einzeiligen Wert.
* **Text Area** (Textbereich): Ein Eigenschaftsschlüssel mit einem mehrzeiligen Wert.
* **Secure** (Sicher): Ein Eigenschaftsschlüssel mit einem einzeiligen Wert. Der Wert wird in Form von Sternen angezeigt.
* **Properties** (Eigenschaften): Eine Datei im Projektrepository. Diese Datei kann mehrere Eigenschaften enthalten. Jede Eigenschaft muss in einer eigenen Zeile stehen. Verwenden Sie Gleichheitszeichen (=), um Schlüssel und Werte der Paare zu trennen.

## Die Funktionalität Ihrer Pipeline erweitern
{: #deliverypipeline_extend}

Sie können die Funktionalität Ihrer Build & Deploy Pipeline erweitern, indem Sie Ihre Jobs für die Verwendung unterstützter Services konfigurieren. Testjobs können zum Beispiel statische Codescans ausführen und Buildjobs können Zeichenfolgen globalisieren.

Weitere Informationen zum Erweitern von Pipelinefunktionen finden Sie unter [Funktionalität des {{site.data.keyword.deliverypipeline}}-Services erweitern](./deliverypipeline_extension.html).

<!-- [1]: https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest
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
[23]: ./images/pipeline_settings.png
[24]: https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service
[25]: ../deploy_var
[26]: ./images/click_stage_run_number.png
[27]: ./images/diagram.jpg -->
