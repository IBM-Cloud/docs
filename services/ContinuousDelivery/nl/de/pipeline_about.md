---

copyright:
  years: 2016, 2017
lastupdated: "2017-4-4"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Informationen zu Delivery Pipeline
{: #deliverypipeline_about}

Der IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} Service, der auch als Pipeline bezeichnet wird, automatisiert die kontinuierliche Bereitstellung Ihrer Bluemix-Projekte. In einer Pipeline rufen Abfolgen von Stages Eingabe- und Ausgabejobs wie Builds, Tests und Bereitstellungen ab.
{:shortdesc}

Die folgenden Abschnitte beschreiben die Konzeptionsdetails von Pipelines.

## Stages
{: #deliverypipeline_stages}

Stages organisieren Eingabe- und Ausgabejobs während ein Build für den Code erstellt, dieser implementiert und getestet wird. Stages akzeptieren Eingaben von den Quellcodeverwaltungsrepositorys (SCM-Repositorys) oder von Buildjobs (Buildartefakte) in anderen Stages. Wenn Sie Ihre erste Stage erstellen, werden die Einstellungen für Sie auf der Registerkarte **EINGABE** festgelegt.

Die Eingabe einer Stage wird an die darin enthaltenen Jobs übergeben und jeder Job wird in einem bereinigten Container ausgeführt. Die Jobs in einer Stage können einander keine Artefakte übergeben.

Sie können Umgebungseigenschaften für eine Stage definieren, die in allen Jobs verwendet werden können. Sie könnten zum Beispiel die Eigenschaft `TEST_URL` definieren, die eine einzelne URL übergibt, um Jobs in einer einzelnen Stage bereitzustellen und zu testen. Der Bereitstellungsjob würde an dieser URL implementiert und der Testjob würde die App testen, die an dieser URL ausgeführt wird.

In einer Stage werden standardmäßig Builds und Bereitstellungen automatisch ausgeführt, sobald Änderungen an ein SCM-Repository des Projekts übermittelt werden. Stages und Jobs werden seriell ausgeführt. Sie ermöglichen die Ablaufsteuerung für Ihre Arbeit. Sie können zum Beispiel eine Teststage vor einer Bereitstellungsstage anordnen. Falls die Tests in der Teststage fehlschlagen, wird die Bereitstellungsstage nicht ausgeführt.

Möglicherweise wünschen Sie eine engere Steuerung einer bestimmten Stage. Wenn Sie nicht möchten, dass eine Stage immer dann ausgeführt wird, wenn eine Änderung bei ihrer Eingabe auftritt, können Sie diese Funktion inaktivieren. Klicken Sie auf der Registerkarte **EINGABE** im Abschnitt für Auslöser von Stages auf **Jobs nur ausführen, wenn diese Stage manuell ausgeführt wird**.

![Die Registerkarte EINGABE](images/input_tab_only_execute.png)

## Jobs
{: #deliverypipeline_jobs}

Ein Job ist eine Ausführungseinheit innerhalb einer Stage. Eine Stage kann mehrere Jobs enthalten und die Jobs in einer Stage werden nacheinander ausgeführt. Falls ein Job fehlschlägt, werden nachfolgende Jobs in der Stage nicht ausgeführt.

![Build- und Testjobs innerhalb einer Stage](images/jobs.png)

Jobs werden in diskreten Arbeitsverzeichnissen innerhalb von Docker-Containern ausgeführt, die für jede Pipelineausführung erstellt werden. Vor der Ausführung eines Jobs wird sein Arbeitsverzeichnis mit Eingaben gefüllt, die auf der Ebene der Stage definiert wurden. Sie haben beispielsweise eine Stage, die einen Testjob und einen Bereitstellungsjob enthält. Wenn Sie Abhängigkeiten in einem Job installieren, so sind diese für den anderen Job nicht verfügbar. Falls Sie die Abhängigkeiten in der Eingabe der Stage verfügbar machen, stehen Sie beiden Jobs zur Verfügung.

Wenn Sie einen Job konfigurieren, können Sie mit Ausnahme von Buildjobs vom einfachen Typ (Simple), UNIX-Shell-Scripts einbeziehen, die Build-, Test- oder Bereitstellungsbefehle einschießen. Da Jobs in Ad-hoc-Containern ausgeführt werden, können die Aktionen eines Jobs nicht die Ausführungsumgebungen anderer Jobs beeinflussen, selbst wenn diese Jobs Teil derselben Stage sind.

Darüber hinaus können Pipeline-Jobs nur die folgenden Befehle als `sudo` ausführen:
  * `/usr/sbin/service`
  * `/usr/bin/apt-get`
  * `/usr/bin/apt-key`
  * `/usr/bin/dpkg`
  * `/usr/bin/add-apt-repository`
  * `/opt/IBM/node-v0.10.40-linux-x64/npm`
  * `/opt/IBM/node-v0.12.7-linux-x64/npm`
  * `/opt/IBM/node-v4.2.2-linux-x64/npm`
  * `/usr/bin/Xvfb`
  * `/usr/bin/pip`


Nachdem ein Job ausgeführt wurde, wird der Container, der für ihn erstellt worden ist, gelöscht. Die Ergebnisse eines Jobs können erhalten bleiben, die Umgebung, in der der Job ausgeführt wurde, kann jedoch nicht erhalten bleiben.

**Hinweis**: Jobs können für eine Dauer von bis zu 60 Minuten ausgeführt werden. Wenn Jobs diesen Grenzwert überschreiten, schlagen sie fehl. Falls ein Job den Grenzwert überschreitet, teilen Sie ihn in mehrere Jobs auf. Wenn ein Job zum Beispiel drei Aufgaben ausführt, können Sie ihn möglicherweise in drei Jobs aufteilen: Ein Job für jede Aufgabe.

Informationen dazu, wie Sie einen Job zu einer Stage hinzufügen, enthält das Thema [Einen Job zu einer Stage hinzufügen](/docs/services/ContinuousDelivery/pipeline_build_deploy.html#deliverypipeline_add_job){: new_window}.

### Buildjobs

Buildjobs kompilieren Ihr Projekt in Vorbereitung auf die Bereitstellung. Sie generieren Artefakte, die an ein Buildarchivverzeichnis gesendet werden können, obwohl die Artefakte standardmäßig in das Stammverzeichnis des Projekts gestellt werden.

Jobs, die Eingaben von Buildjobs erhalten, müssen Buildartefakte in derselben Struktur referenzieren, in der sie erstellt wurden. Wenn ein Buildjob zum Beispiel Buildartefakte in das Verzeichnis `output` archiviert, würde ein Bereitstellungsscript auf das Verzeichnis `output` und nicht auf das Projektstammverzeichnis verweisen, um das kompilierte Projekt zu implementieren. Sie können das zu archivierende Verzeichnis angeben, indem Sie den Verzeichnisnamen in das Feld **Archivverzeichnis erstellen** eingeben. Wenn Sie das Feld leer lassen, wird das Stammverzeichnis archiviert.

**Hinweis**: Wenn Sie den Erstellungsprogrammtyp **Simple** für einen Buildjob auswählen, überspringen Sie den Erstellungsprozess. In diesem Fall wird Ihr Code nicht kompiliert, sondern unverändert an die Stage für die Bereitstellung gesendet. Wählen Sie daher für Build und Bereitstellung einen anderen Buildertyp als **Simple** aus.

#### Umgebungseigenschaften für Erstellungsscripts
Sie können Umgebungseigenschaften innerhalb der Buildshellbefehle eines Buildjobs einschließen. Die Eigenschaften bieten Zugriff auf Informationen über die Ausführungsumgebung des Jobs. Weitere Informationen finden Sie unter [Umgebungseigenschaften und Ressourcen für den {{site.data.keyword.deliverypipeline}}-Service](/docs/services/ContinuousDelivery/pipeline_deploy_var.html).

### Bereitstellungsjobs

Bereitstellungsjobs laden Ihr Projekt als eine App in Bluemix hoch und sind über eine URL zugänglich. Nach der Bereitstellung eines Projekts finden Sie die bereitgestellte App in Ihrem Bluemix-Dashboard.

Bereitstellungsjobs können neue Apps bereitstellen oder vorhandene Apps aktualisieren. Auch wenn Sie eine App zuerst mit einer anderen Methode wie beispielsweise über die Cloud Foundry-Befehlszeilenschnittstelle oder die Ausführungsleiste in der Web IDE bereitgestellt haben, können Sie die App mithilfe eines Bereitstellungsjobs aktualisieren. Verwenden Sie den Namen der App, um eine App in einem Bereitstellungsjob zu aktualisieren.

Es ist eine Bereitstellung für eine oder mehrere Regionen bzw. einen oder mehrere Services möglich. Sie können Ihre {{site.data.keyword.deliverypipeline}} beispielsweise so einrichten, dass sie mindestens einen Service verwendet, in einer einzigen Region getestet oder und in mehreren Regionen für die Produktion bereitgestellt wird. Weitere Informationen hierzu finden Sie unter [Regionen](/docs/overview/whatisbluemix.html#ov_intro_reg){: new_window}.

#### Umgebungseigenschaften für Bereitstellungsscripts

Sie können Umgebungseigenschaften innerhalb eines Bereitstellungsscripts eines Bereitstellungsjobs einbeziehen. Diese Eigenschaften bieten Zugriff auf Informationen über die Ausführungsumgebung des Jobs. Weitere Informationen finden Sie unter [Umgebungseigenschaften und Ressourcen für den {{site.data.keyword.deliverypipeline}}-Service](/docs/services/ContinuousDelivery/pipeline_deploy_var.html).

### Testjobs
Wenn Bedingungen eingehalten werden sollen, schließen Sie Testjobs vor oder nach Ihren Build- und Bereitstellungsjobs ein. Sie können Testjobs anpassen, damit diese so einfach oder so komplex wie erforderlich sind. Möglicherweise erwarten Sie eine bestimmte Antwort auf die Ausgabe eine cURL-Befehls. Möglicherweise möchten Sie eine Reihe von Komponententests ausführen oder Funktionstests mit Testservices Dritter wie beispielsweise Sauce Labs ausführen.

Wenn Ihre Tests Ergebnisdateien im JUnit XML-Format erzeugen, wird ein Bericht auf Grundlage der Ergebnisdateien auf der Registerkarte **Tests** jeder Seite mit Testergebnissen angezeigt. Wenn ein Test fehlschlägt, schlägt der Job ebenfalls fehl.

#### Umgebungseigenschaften für Testscripts

Sie können Umgebungseigenschaften in das Script eines Testjobs einschließen. Die Eigenschaften bieten Zugriff auf Informationen zur Ausführungsumgebung des Jobs. Weitere Informationen finden Sie unter [Umgebungseigenschaften und Ressourcen für den {{site.data.keyword.deliverypipeline}}-Service](/docs/services/ContinuousDelivery/pipeline_deploy_var.html).

## Manifestdateien
{: #deliverypipeline_manifest}

Manifestdateien, die den Namen `manifest.yml` tragen und in einem Projektstammverzeichnis gespeichert sind, steuern, wie Ihr Projekt in Bluemix implementiert ist. Informationen zur Erstellung von Manifestdateien für ein Projekt enthält die [Bluemix-Dokumentation über Anwendungsmanifeste](/docs/manageapps/depapps.html#appmanifest). Für die Integration in Bluemix muss Ihr Projekt über eine Manifestdatei im Stammverzeichnis verfügen. Es ist jedoch nicht erforderlich, dass Sie eine Bereitstellung auf Grundlage der Informationen in der Datei vornehmen.

Sie können in der Pipeline alles angeben, was eine Manifestdatei bei `cf push`-Befehlsargumenten verwenden kann. Die `cf push`-Befehlsargumente sind bei Projekten hilfreich, die über mehrere Bereitstellungsziele verfügen. Falls mehrere Implementierungsjobs versuchen, die Route zu verwenden, die in der Manifestdatei des Projekts angegeben ist, tritt ein Konflikt auf.

Um Konflikte zu vermeiden, können Sie eine Route mithilfe von `cf push` gefolgt vom Hostnamenargument, `-n` und einem Routennamen angeben. Bei der Änderungen des Bereitstellungsscripts für einzelne Stages können Sie Weiterleitungskonflikte vermeiden, wenn Sie mehrere Ziele implementieren.

Öffnen Sie die Konfigurationseinstellungen für einen Bereitstellungsjob und ändern Sie das Feld **Bereitstellungsscript**, um `cf push`-Befehlsargumente zu verwenden. Weitere Informationen enthält die [Dokumentation zur Push-Operation von Cloud Foundry![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push){: new_window}.

## Eine Beispielpipeline
{: #deliverypipeline_example}

Eine einfache Pipeline kann drei Stages enthalten: 

1. Eine Stage für den Build, die Erstellungsprozesse auf einer App kompiliert und einen Build ausführt. 
2. Eine Stage für den Test, die eine Instanz der App bereitstellt und in dieser Instanz anschließend Tests ausführt. 
3. Eine Stage für die Produktion, die eine Produktionsinstanz der getesteten App bereitstellt. 

Diese Pipeline wird im folgenden Konzeptionsdiagramm dargestellt:

![Ein Konzeptionsdiagramm der Stages und Jobs in einer Pipeline](images/diagram.jpg)

*Ein konzeptionelles Modell einer Pipeline mit drei Stages*

Stages bekommen Ihre Eingaben von Repositorys und Buildjobs. Jobs innerhalb einer Stage werden nacheinander und unabhängig voneinander ausgeführt. In der Beispielpipeline werden die Stages nacheinander ausgeführt, obwohl die Stages für den Test und die Produktion beide die Ausgabe
der Stage für den Build als Eingabe verwenden. 
