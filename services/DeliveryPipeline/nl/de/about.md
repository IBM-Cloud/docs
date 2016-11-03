---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Informationen zu {{site.data.keyword.deliverypipeline}}
{: #deliverypipeline_about}
Letzte Aktualisierung: 29. August 2016
{: .last-updated}

Der IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} Service, der auch als Pipeline bezeichnet wird, automatisiert die kontinuierliche Bereitstellung Ihrer Bluemix-Projekte. In einer Pipeline rufen Abfolgen von Phasen Eingabe- und Ausgabejobs wie Builds, Tests und Bereitstellungen ab.
{:shortdesc}

Die folgenden Abschnitte beschreiben die Konzeptionsdetails von Pipelines.

## Phasen
{: #deliverypipeline_stages}

Phasen organisieren Eingabe- und Ausgabejobs während ein Build für den Code erstellt, dieser implementiert und getestet wird. Phasen akzeptieren Eingaben von den Quellcodeverwaltungsrepositorys oder von Buildjobs in anderen Phasen. Wenn Sie Ihre erste Phase erstellen, werden die Einstellungen für Sie auf der Registerkarte **EINGABE** festgelegt.

Die Eingabe einer Phase wird an die darin enthaltenen Jobs übergeben und jeder Job wird in einem bereinigten Container ausgeführt. Die Jobs in einer Phase können einander keine Artefakte übergeben.

Sie können Umgebungseigenschaften für eine Phase definieren, die in allen Jobs verwendet werden können. Sie könnten zum Beispiel die Eigenschaft `TEST_URL` definieren, die eine einzelne URL übergibt, um Jobs in einer einzelnen Phase bereitzustellen und zu testen. Der Bereitstellungsjob würde an dieser URL implementiert und der Testjob würde die App testen, die an dieser URL ausgeführt wird.

In einer Phase werden Builds und Bereitstellungen automatisch ausgelöst, sobald Änderungen an ein Quellcodeverwaltungsrepository des Projekts übermittelt werden. Phasen und Jobs werden seriell ausgeführt. Sie ermöglichen die Ablaufsteuerung für Ihre Arbeit. Sie können zum Beispiel eine Phase für den Test vor einer Phase für die Bereitstellung anordnen. Falls die Tests in der Phase für den Test fehlschlagen, wird die Phase für die Bereitstellung nicht ausgeführt.

Möglicherweise wünschen Sie eine engere Steuerung einer bestimmten Phase. Wenn Sie nicht möchten, dass eine Phase immer dann ausgeführt wird, wenn eine Änderung bei ihrer Eingabe auftritt, können Sie diese Funktion inaktivieren. Klicken Sie auf der Registerkarte **EINGABE** im Abschnitt für Auslöser von Phasen auf **Jobs nur ausführen, wenn diese Phase manuell ausgeführt wird**.

![Die Registerkarte EINGABE](./images/input_tab_only_execute.png)

## Jobs
{: #deliverypipeline_jobs}

Ein Job ist eine Ausführungseinheit innerhalb einer Phase. Eine Phase kann mehrere Jobs enthalten und die Jobs in einer Phase werden nacheinander ausgeführt. Falls ein Job fehlschlägt, werden nachfolgende Jobs in der Phase nicht ausgeführt.

![Build- und Testjobs innerhalb einer Phase](./images/jobs.png)

Jobs werden in diskreten Arbeitsverzeichnissen innerhalb von Docker-Containern ausgeführt, die für jede Pipelineausführung erstellt werden. Vor der Ausführung eines Jobs wird sein Arbeitsverzeichnis mit Eingaben gefüllt, die auf der Ebene der Phase definiert wurden. Sie haben beispielsweise eine Phase, die einen Testjob und einen Bereitstellungsjob enthält. Wenn Sie Abhängigkeiten in einem Job installieren, so sind diese für den anderen Job nicht verfügbar. Falls Sie die Abhängigkeiten in der Eingabe der Phase verfügbar machen, stehen Sie beiden Jobs zur Verfügung.

Wenn Sie einen Job konfigurieren, können Sie mit Ausnahme von Buildjobs vom einfachen Typ (Simple), UNIX-Shell-Scripts einbeziehen, die Build-, Test- oder Bereitstellungsbefehle einschießen. Da Jobs in Ad-hoc-Containern ausgeführt werden, können die Aktionen eines Jobs nicht die Ausführungsumgebungen anderer Jobs beeinflussen, selbst wenn diese Jobs Teil derselben Phase sind.

Nachdem ein Job ausgeführt wurde, wird der Container, der für ihn erstellt worden ist, gelöscht. Die Ergebnisse eines Jobs können erhalten bleiben, die Umgebung, in der der Job ausgeführt wurde, kann jedoch nicht erhalten bleiben.

**Hinweis**: Jobs können für eine Dauer von bis zu 60 Minuten ausgeführt werden. Wenn Jobs diesen Grenzwert überschreiten, schlagen sie fehl. Falls ein Job den Grenzwert überschreitet, teilen Sie ihn in mehrere Jobs auf. Wenn ein Job zum Beispiel drei Aufgaben ausführt, können Sie ihn möglicherweise in drei Jobs aufteilen: Ein Job für jede Aufgabe.

Informationen dazu, wie Sie einen Job zu einer Phase hinzufügen, finden Sie unter dem Thema [Job zu einer Phase hinzufügen](./build_deploy.html#deliverypipeline_add_job).

### Buildjobs

Buildjobs kompilieren Ihr Projekt in Vorbereitung auf die Bereitstellung. Sie generieren Artefakte, die an ein Buildarchivverzeichnis gesendet werden können, obwohl die Artefakte standardmäßig in das Stammverzeichnis des Projekts gestellt werden.

Jobs, die Eingaben von Buildjobs erhalten, müssen Buildartefakte in derselben Struktur referenzieren, in der sie erstellt wurden. Wenn ein Buildjob zum Beispiel Buildartefakte in das Verzeichnis `output` archiviert, würde ein Bereitstellungsscript auf das Verzeichnis `output` und nicht auf das Projektstammverzeichnis verweisen, um das kompilierte Projekt zu implementieren.

**Hinweis**: Wenn Sie den Erstellungsprogrammtyp **Simple** für einen Buildjob auswählen, überspringen Sie den Erstellungsprozess. In diesem Fall wird Ihr Code nicht kompiliert, sondern unverändert an die Phase für die Bereitstellung gesendet. Wählen Sie daher für Build und Bereitstellung einen anderen Buildertyp als **Simple** aus.

#### Umgebungseigenschaften für Erstellungsscripts
Sie können Umgebungseigenschaften innerhalb der Buildshellbefehle eines Buildjobs einschließen. Die Eigenschaften bieten Zugriff auf Informationen über die Ausführungsumgebung des Jobs. Weitere Informationen finden Sie unter [Umgebungseigenschaften und Ressourcen für den {{site.data.keyword.deliverypipeline}}-Service](./deploy_var.html).

### Bereitstellungsjobs

Bereitstellungsjobs laden Ihr Projekt als eine App in Bluemix hoch und sind über eine URL zugänglich. Nach der Bereitstellung eines Projekts, finden Sie die bereitgestellte App in Ihrem Bluemix-Dashboard. Sie können die Build- und Bereitstellungsjobs als separate Phasen konfigurieren oder Sie können sie zu derselben Phase hinzufügen, damit Sie automatisch ausgeführt werden.

Bereitstellungsjobs können neue Apps bereitstellen oder vorhandene Apps aktualisieren. Auch wenn Sie eine App zuerst mit einer anderen Methode wie beispielsweise über die Cloud Foundry-Befehlszeilenschnittstelle oder die Ausführungsleiste in der Web IDE bereitgestellt haben, können Sie die App mithilfe eines Bereitstellungsjobs aktualisieren. Verwenden Sie den Namen der App, um eine App in einem Bereitstellungsjob zu aktualisieren.

Es ist eine Bereitstellung für eine oder mehrere Regionen bzw. einen oder mehrere Services möglich. Sie können beispielsweise Ihren {{site.data.keyword.deliverypipeline}}-Service so einrichten, dass Entwicklungsartefakte IBM Containers nutzen, in einer einzigen Region getestet werden und in mehreren Regionen für die Produktion bereitgestellt werden. Weitere Informationen hierzu finden Sie unter [Regionen](../../overview/index.html#ov_intro__reg).

#### Umgebungseigenschaften für Bereitstellungsscripts

Sie können Umgebungseigenschaften innerhalb eines Bereitstellungsscripts eines Bereitstellungsjobs einbeziehen. Diese Eigenschaften bieten Zugriff auf Informationen über die Ausführungsumgebung des Jobs. Weitere Informationen finden Sie unter [Umgebungseigenschaften und Ressourcen für den {{site.data.keyword.deliverypipeline}}-Service](./deploy_var.html).

### Testjobs
Wenn Bedingungen eingehalten werden sollen, schließen Sie Testjobs vor oder nach Ihren Build- und Bereitstellungsjobs ein. Sie können Testjobs anpassen, damit diese so einfach oder so komplex wie erforderlich sind. Möglicherweise erwarten Sie eine bestimmte Antwort auf die Ausgabe eine cURL-Befehls. Möglicherweise möchten Sie eine Reihe von Komponententests ausführen oder Funktionstests mit Testservices Dritter wie beispielsweise Sauce Labs auslösen.

Wenn Ihre Tests Ergebnisdateien im JUnit XML-Format erzeugen, wird ein Bericht auf Grundlage der Ergebnisdateien auf der Registerkarte **Tests** jeder Seite mit Testergebnissen angezeigt. Wenn ein Test fehlschlägt, schlägt der Job ebenfalls fehl.

#### Umgebungseigenschaften für Testscripts

Sie können Umgebungseigenschaften in das Script eines Testjobs einschließen. Die Eigenschaften bieten Zugriff auf Informationen zur Ausführungsumgebung des Jobs. Weitere Informationen finden Sie unter [Umgebungseigenschaften und Ressourcen für den {{site.data.keyword.deliverypipeline}}-Service](./deploy_var.html).

## Manifestdateien
{: #deliverypipeline_manifest}

Manifestdateien, die den Namen `manifest.yml` tragen und in einem Projektstammverzeichnis gespeichert sind, steuern, wie Ihr Projekt in Bluemix implementiert ist. Informationen zur Erstellung von Manifestdateien für ein Projekt finden Sie in der [Bluemix-Dokumentation über Anwendungsmanifeste](https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest). Für die Integration in Bluemix muss Ihr Projekt über eine Manifestdatei im Stammverzeichnis verfügen. Es ist jedoch nicht erforderlich, dass Sie eine Bereitstellung auf Grundlage der Informationen in der Datei vornehmen.

Sie können in der Pipeline alles angeben, was eine Manifestdatei bei `cf push`-Befehlsargumenten verwenden kann. Die `cf push`-Befehlsargumente sind bei Projekten hilfreich, die über mehrere Bereitstellungsziele verfügen. Falls mehrere Implementierungsjobs versuchen, die Route zu verwenden, die in der Manifestdatei des Projekts angegeben ist, tritt ein Konflikt auf.

Um Konflikte zu vermeiden, können Sie eine Route mithilfe von `cf push` gefolgt vom Hostnamenargument, `-n` und einem Routennamen angeben. Bei der Änderungen des Bereitstellungsscripts für einzelne Phasen können Sie Weiterleitungskonflikte vermeiden, wenn Sie mehrere Ziele implementieren.

Öffnen Sie die Konfigurationseinstellungen für einen Bereitstellungsjob und ändern Sie das Feld **Bereitstellungsscript**, um `cf push`-Befehlsargumente zu verwenden. Weitere Informationen finden Sie in der [Dokumentation zur Push-Operation von Cloud Foundry](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push).

## Eine Beispielpipeline
{: #deliverypipeline_example}

Eine einfache Pipeline enthält vielleicht drei Phasen:

1. Eine Phase für den Build, der Erstellungsprozesse auf einer App kompiliert und einen Build ausführt.
2. Eine Phase für den Test, der eine Instanz der App bereitstellt und auf dieser Tests ausführt.
3. Eine Phase für die Produktion, der eine Produktionsinstanz der getesteten App bereitstellt.

Diese Pipeline wird im folgenden Konzeptionsdiagramm dargestellt:

![Ein Konzeptionsdiagramm der Phasen und Jobs in einer Pipeline](./images/diagram.jpg)

*Ein konzeptionelles Modell einer Pipeline mit drei Phasen*

Phasen bekommen Ihre Eingaben von Repositorys und Buildjobs. Jobs innerhalb einer Phase werden nacheinander und unabhängig voneinander ausgeführt. In der Beispielpipeline werden die Phasen nacheinander ausgeführt, obwohl die Phasen für den Test und die Produktion beide die Ausgabe des Phase für den Build als Eingabe verwenden.

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
