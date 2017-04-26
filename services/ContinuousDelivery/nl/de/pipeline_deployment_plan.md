---

copyright:
  years: 2017
lastupdated: "2017-3-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Bereitstellungspläne für Kombinationspipelines anpassen
{: #tasks_overview}

In einem Bereitstellungsplan für eine Kombinationspipeline stellt eine Task eine unternehmensrelevante Aktivität dar, die mit einer Softwarebereitstellung verbunden ist. Tasks werden in Bereitstellungsplänen definiert. 

{:shortdesc}

Die meisten Tasks verfügen über einen Ausgangspunkt, einen Endpunkt und eine messbare Dauer. Eine Task kann einem der folgenden Typen angehören: 

<ul>
<li>Manuelle Tasks können jede Aktivität darstellen, die mit einer Software-Bereitstellung verbunden ist, wie z. B. das Offlineschalten eines Servers oder das Aktualisieren einer Datenbank.</li>
<li>UrbanCode Deploy-Tasks stellen IBM&reg; UrbanCode&reg; Deploy-Apps dar. Sie können IBM UrbanCode Deploy-Apps mit Tasks vom Typ IBM UrbanCode Deploy ausführen. </li>
<li>Continuous Delivery Pipeline-Tasks stellen Instanzen von {{site.data.keyword.deliverypipeline}} dar, das Teil von {{site.data.keyword.contdelivery_full}} ist. Mit diesem Tasktyp können Sie Ihre Instanzen von {{site.data.keyword.deliverypipeline}} verwalten. </li>
<li>Verzögerte Tasks stellen kritische Ereignisse dar, die zu einem bestimmten Zeitpunkt eintreten. </li>
<li>Header-Tasks sind Organisationselemente. Sie könnten zum Beispiel eine Header-Task verwenden, um eine Taskgruppe anzugeben. </li>
</ul>

<!-- You can add tasks to deployment plans by creating tasks or you can import tasks from CSV files that are created by IBM UrbanCode Release or another application. You can also copy tasks from other deployment plans. See [Importing tasks](/docs/services/UCCR/UCCR_deployPlan.html#plan_importTasks) for information about the format of the CSV file. -->

## Tasks erstellen
{: #tasks_create}

Wenn Sie eine Task erstellen, wählen Sie den Bereitstellungsplan aus, zu dem die Task hinzugefügt werden soll. Neue Tasks werden standardmäßig am Ende des Bereitstellungsplans eingefügt. Nach der Erstellung einer Task können Sie sie verschieben oder kopieren und in einen anderen Bereitstellungsplan einfügen. Außerdem können Sie Abhängigkeiten zu anderen [Tasks](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html#tasks_dependencies) erstellen.

Nach dem Speichern einer Task werden für diese Task Aktionssymbole angezeigt. Anhand dieser Aktionssymbole können Sie den Status der Task im Verlauf einer Bereitstellung ändern. Alle Tasks besitzen das Symbol für die Aktion **Überspringen**. Andere Symbole wie etwa das für die Aktion **Starten** werden angezeigt, wenn ihnen der jeweilige Kontext entspricht.

![](../UCCR/images/deploy-plan-intro.png "Typischer Bereitstellungsplan")

*Abbildung 1. Einfacher Bereitstellungsplan mit Tasks und Aktionssymbolen*

Jede Task in einem Bereitstellungsplan ist in einer separaten Zeile enthalten. Welche Informationen für die einzelnen Tasks angezeigt werden, ist in der nachfolgenden Tabelle beschrieben. 

### Tabelle 1. Taskeigenschaften

| Eigenschaft        | Beschreibung  |
| ------------------ | ------------------ |
| Name               |Name der Task       |
| Typ                |Typ von Task: Manuell, Continuous Delivery Pipeline, Verzögert, E-Mail, Header/Hinweis, UrbanCode Deploy|             
| Status             |Taskstatus: Nicht gestartet, Abgeschlossen, Fehlgeschlagen, Übersprungen, Nicht zutreffend |
| Eigner             |Person, der die Task zugewiesen ist                                                        |
| Startzeit          |Startzeit oder erwartete Startzeit basierend auf dem geplanten Start oder aber geschätzte Dauer anderer Tasks        |
| Endzeit            |Zeit, zu der die Task aufgelöst wurde        |
| Dauer              |Zeitraum (in Minuten) vom Start der Task bis zu ihrer Auflösung        |
| Abhängigkeiten     |Anzahl der Tasks, die als Voraussetzungen für diese Task fungieren bzw. die von dieser Task abhängig sind        |

---
Nachdem Tasks zu Bereitstellungsplänen hinzugefügt worden sind, können Sie sie auf verschiedene Arten verwalten:
   * Wenn Sie eine Task verschieben wollen, ziehen Sie sie an die gewünschte neue Position.

   * Wenn Sie eine Task oder Gruppe kopieren wollen, klicken Sie auf die entsprechende Task, klicken Sie dann auf das Symbol für die Aktion **Kopieren** <img class="inline" src="../UCCR/images/copy-group.png"  alt="Symbol für Aktion 'Kopieren'">, platzieren Sie den Cursor an die Stelle, an der Sie die kopierte Task einfügen möchten, und klicken Sie dann auf das Symbol für die Aktion **Einfügen** <img class="inline" src="../UCCR/images/paste-group.png"  alt="Symbol für Aktion 'Einfügen'">.

   * Wenn Sie eine Task oder Gruppe aus einem Bereitstellungsplan ausschneiden wollen, klicken Sie auf die betreffende Task und klicken Sie anschließend auf das Symbol für die Aktion **Ausschneiden** <img class="inline" src="../UCCR/images/cut-group.png"  alt="Symbol für Aktion 'Ausschneiden'">.

   * Wenn Sie eine Task löschen wollen, klicken Sie auf die zu löschende Task und klicken Sie dann auf das Symbol für die Aktion **Löschen** <img class="inline" src="../UCCR/images/trash-group.png"  alt="Symbol für Aktion Löschen'">. Dann wird die Task aus dem Implementierungsplan entfernt.

<!-- ## Creating UrbanCode Deploy tasks
{: #tasks_UDTasks}

UrbanCode Deploy tasks manage UrbanCode Deploy applications. When you run an UrbanCode Deploy task, the associated UrbanCode Deploy application runs by using the process, version, and environment specified by the task. You can set the version and environment at design time or wait and select them at run time.

During deployments, UrbanCode Deploy tasks start automatically when they become eligible to run.   

**Important** Applications become available after {{site.data.keyword.uccr_short}} is integrated with UrbanCode Deploy. The applications that are available to a deployment plan depend on the team that is assigned to the plan. The applications that are managed by the team in UrbanCode Deploy are also available in {{site.data.keyword.uccr_short}}.

Complete the following tasks to create an UrbanCode Deploy task.

1. On the Deployment Plan Details page, click **Create Task**. If you want to insert a task at a specific position in the plan, select a task before using the **Create Task**. The new task is inserted above the selected task.

1. On the Create Task dialog box, in the **Type** list, select **UrbanCode Deploy**.

1. In the **Name** field, enter a name for the task.

3. In the **Duration (minutes)** field, enter the number of minutes that you expect the task to run until it is completed. The estimated duration is used to calculate expected deployment times.

3. In the **Tags** list, attach a tag to the task. You can select multiple tags. To create a tag, type the tag name in list's text field.

3. In the **Application Name** list, select an application.

3. In the **Process** list, select an application process. Processes that belong to the selected UrbanCode Deploy application are available.

3. In the **Environment** list, select an application environment. Environments that belong to the selected UrbanCode Deploy application are available.  To postpone selecting an environment until you are ready to run the deployment, select **Use Version Tab**.

3. In the **Version** list, select an application version. Versions refer to IBM UrbanCode Deploy application snapshots. Versions that belong to the selected application are available.  To postpone selecting a version, select **Use Version Tab**. If the application process does not require a version, select **No Version**. You might select this last option if you are running a configuration-type process that does not require components.

3. In the **Assigned groups and users** list, assign the task to a user or group. The assigned user runs the task during deployment.

3. In the **Owner** list, select the task owner. The default owner is the user who created the task. The **Owner** list is displayed after the task is assigned to a user or group.    

5. Click **Save**. The task is inserted into the deployment plan.

After the task is created, the plan's **Version** tab is updated with information about the application assigned to the task. If you selected **Use Version Tab** for the application environment and version, use the Version tab to set those options before running the deployment. -->

## Manuelle Tasks erstellen
{: #tasks_manual}

Normalerweise stellen manuelle Tasks eine Aktivität dar, die einem Software-Release zugeordnet ist und einen Startpunkt, einen Endpunkt sowie eine messbare Dauer besitzt. 

Führen Sie die folgenden Schritte aus, um eine manuelle Task zu erstellen: 

1. Klicken Sie auf der Seite mit den Bereitstellungsplandetails auf **Task erstellen**. Wenn Sie eine Task an einer bestimmten Position in den Plan einfügen wollen, wählen Sie zuerst eine Task aus und klicken Sie dann auf **Task erstellen**. Die neue Task wird über der ausgewählten Task eingefügt. 

1. Wählen Sie im Fenster 'Task erstellen' in der Liste **Typ** den Typ **Manuell** aus.

1. Geben Sie im Feld **Name** einen Namen für die Task ein. 

3. Geben Sie im Feld **Dauer (Minuten)** in Minuten die erwartete Ausführungsdauer der Task bis zu ihrem Abschluss ein. Die geschätzte Dauer wird zum Berechnen der erwarteten Bereitstellungszeiten verwendet. 

3. Versehen Sie die Task in der Liste **Tags** mit einem Tag. Sie können mehrere Tags auswählen. Wenn Sie einen Tag erstellen möchten, geben Sie den Namen für den Tag in das Textfeld der Liste ein. 

3. Weisen Sie die Task in der Liste **Zugewiesene Gruppen und Benutzer** einem Benutzer oder einer Gruppe zu. Der zugewiesene Benutzer führt die Task bei der Bereitstellung aus. 

3. Wählen Sie in der Liste **Eigner** den Taskeigner aus. Der Standardeigner ist der Benutzer, der die Task erstellt hat. Die Liste **Eigner** wird angezeigt, nachdem die Task einem Benutzer oder einer Gruppe zugewiesen wurde.     

5. Klicken Sie auf **Speichern**. Die Task wird in den Bereitstellungsplan eingefügt. 

## Verzögerte Tasks erstellen
{: #tasks_delayed}

Tasks vom Typ 'Verzögert' stellen Meilensteine oder kritische Ereignisse bei einer Bereitstellung dar. Mit verzögerten Tasks können Sie sicherstellen, dass wichtige Tasks zum erwarteten Zeitpunkt starten. Normalerweise fungieren verzögerte Tasks als Voraussetzungen für andere wichtige Tasks. 

Eine verzögerte Task startet, sobald sie ausführungsberechtigt ist, und sie endet zu einer benutzerdefinierten Zeit. Eine gestartete verzögerte Task weist so lange den Status 'In Bearbeitung' auf, bis sie die vorgesehene Zeit erreicht und ihr Status in 'Abgeschlossen' wechselt. Nachdem eine verzögerte Task abgeschlossen worden ist, wird die Ausführung der von ihr abhängigen Tasks gestartet. 

Führen Sie die folgenden Schritte aus, um eine verzögerte Task zu erstellen: 

1. Klicken Sie auf der Seite mit den Bereitstellungsplandetails auf **Task erstellen**. Wenn Sie eine Task an einer bestimmten Position in den Plan einfügen wollen, wählen Sie zuerst eine Task aus und klicken Sie dann auf **Task erstellen**. Die neue Task wird über der ausgewählten Task eingefügt. 

1. Wählen Sie im Fenster 'Task erstellen' in der Liste **Typ** den Typ **Verzögert** (Delayed) aus.

1. Geben Sie im Feld **Name** einen Namen für die Task ein. 

3. Geben Sie im Feld **Zeit** die Uhrzeit aus, zu der die Task abgeschlossen sein wird, oder wählen Sie eine entsprechende Uhrzeit aus. 

3. Wählen Sie in der Liste **Zeitzone** die Zeitzone für die im Feld **Zeit** eingegebene Zeitangabe aus.     

5. Klicken Sie auf **Speichern**. Die Task wird in den Bereitstellungsplan eingefügt. 

## Header-Tasks erstellen
{: #tasks_header}

Header-Tasks stellen Organisationselemente dar, die Sie zu Bereitstellungsplänen hinzufügen können. Wenn Sie eine Taskgruppe erstellen, ist es gegebenenfalls ratsam, die Gruppe mit einer Header-Task zu versehen. Header-Tasks können wie beliebige andere Tasks auch Abhängigkeiten besitzen. 

<!-- When you import a deployment plan from IBM UrbanCode Release, segment tasks are bracketed by note-type Start Segment and End Segment tasks. Segment dependencies are represented by dependencies to End Segment tasks. -->

Führen Sie die folgenden Schritte aus, um eine Header-Task zu erstellen: 

1. Klicken Sie auf der Seite mit den Bereitstellungsplandetails auf **Task erstellen**. Wenn Sie eine Task an einer bestimmten Position in den Plan einfügen wollen, wählen Sie zuerst eine Task aus und klicken Sie dann auf **Task erstellen**. Die neue Task wird über der ausgewählten Task eingefügt. 

1. Wählen Sie im Fenster 'Task erstellen' in der Liste **Typ** den Typ **Header** aus.

1. Geben Sie im Feld **Name** einen Namen für die Task ein. Dieser Name kann eine Taskgruppe bezeichnen. 

3. Geben Sie im Feld **Beschreibung** eine Beschreibung ein oder fügen Sie eine solche ein. Sie könnten beispielsweise einen Hinweis, eine Erinnerung oder sonstige Anweisungen eingeben. 

5. Klicken Sie auf **Speichern**. Die Task wird in den Bereitstellungsplan eingefügt. 

## Delivery Pipeline-Tasks erstellen
{: #tasks_pipelineCD}

{{site.data.keyword.deliverypipeline}} bewirkt im {{site.data.keyword.contdelivery_short}}-Service die Automatisierung Ihrer DevOps-Workflows. Mit Pipeline-Tasks können Sie Ihre Instanzen von {{site.data.keyword.deliverypipeline}} verwalten. 

Führen Sie die folgenden Schritte aus, um eine Delivery Pipeline-Task zu erstellen: 

1. Klicken Sie auf der Seite mit den Bereitstellungsplandetails auf **Task erstellen**. Wenn Sie eine Task an einer bestimmten Position in den Plan einfügen wollen, wählen Sie zuerst eine Task aus und klicken Sie dann auf **Task erstellen**. Die neue Task wird über der ausgewählten Task eingefügt. 

1. Wählen Sie im Fenster 'Task erstellen' in der Liste **Typ** den Typ **Continuous Delivery Pipeline** aus.

1. Geben Sie im Feld **Name** einen Namen für die Task ein. Dieser Name kann eine Taskgruppe bezeichnen. 

3. Geben Sie im Feld **Beschreibung** eine Beschreibung ein oder fügen Sie eine solche ein. Sie könnten beispielsweise einen Hinweis, eine Erinnerung oder sonstige Anweisungen eingeben. 

3. Geben Sie im Feld **Pipeline-ID** die Pipeline-ID ein oder fügen Sie sie ein. 

3. Geben Sie im Feld **Stagename** den Namen für die Stage ein oder fügen Sie ihn ein. 

5. Klicken Sie auf **Speichern**. Die Task wird in den Bereitstellungsplan eingefügt. 

## Taskgruppen verwalten
{: #tasks_groups}

Sie können zwei oder mehr Tasks in einer Taskgruppe kombinieren. Wenn Sie eine Gruppe erstellen, legen Sie das gewünschte Ausführungsmuster der Gruppe fest - nacheinander (sequenziell) oder zeitgleich (parallel). Die Tasks in einer Gruppe mit parallelem Ausführungsmuster können in jeder beliebigen Reihenfolge ausgeführt werden. Außerdem können Sie solche Tasks gleichzeitig ausführen, sofern keine Abhängigkeiten vorhanden sind. Die Ausführung von Tasks in Gruppen mit sequenziellem Ausführungsmuster erfolgt gemäß ihrer Listenreihenfolge angefangen bei der ersten bzw. obersten Task. 

Es ist möglich, Gruppen in andere Gruppen einzubetten. Sie können beispielsweise eine Gruppe mit sequenziellem Ausführungsmuster in eine Gruppe mit parallelem Ausführungsmuster einbetten oder umgekehrt. Die Einbettung einer Gruppe mit sequenziellem Ausführungsmuster in eine andere sequenzielle Gruppe oder einer Gruppe mit parallelem Ausführungsmuster in eine andere parallele Gruppe ist jedoch nicht möglich.   

Führen Sie die folgenden Schritte aus, um eine Taskgruppe zu erstellen: 

1. Wählen Sie auf der Seite mit den Bereitstellungsplandetails mindestens zwei Tasks aus. 

1. Führen Sie einen der folgenden Schritte aus, je nachdem, welchen Typ von Gruppe Sie erstellen wollen: 

  <ul>
  <li>Wenn Sie eine Gruppe mit parallelem Ausführungsmuster erstellen wollen, klicken Sie auf das Symbol **Parallel** <img class="inline" src="../UCCR/images/para-icon.png"  alt="Symbol 'Parallele Gruppe'">. Fall die Erstellung einer parallelen Gruppe mit den ausgewählten Tasks nicht möglich ist, ist dieses Symbol inaktiviert. Es könnte zum Beispiel sein, dass Sie eine parallele Gruppe nicht erstellen können, wenn sich alle für diese Gruppe ausgewählten Tasks bereits in einer parallelen Gruppe befinden. </li>
  <li>Wenn Sie eine Gruppe mit sequenziellem Ausführungsmuster erstellen wollen, klicken Sie auf das Symbol **Sequenziell** <img class="inline" src="../UCCR/images/seq-icon.png"  alt="Symbol 'Sequenzielle Gruppe'">. </li>
  </ul>

Die Gruppe wird gebildet und es wird eine Leiste für die Gruppenauswahl zum Bereitstellungsplan hinzugefügt. Wenn Sie nicht zusammenhängende Tasks ausgewählt haben, so bilden die Tasks eine fortlaufenden Liste, die mit der obersten ausgewählten Task beginnt. 

Die folgende Abbildung stellt eine parallele Gruppe dar. An der Leiste für die Gruppenauswahl ist erkennbar, um welche Art von Gruppe es sich handelt - um eine Gruppe mit parallelem Ausführungsmuster <img class="inline" src="../UCCR/images/para-select.png"  alt="Auswahl von paralleler Gruppe"> oder um eine Gruppe mit sequenziellem Ausführungsmuster <img class="inline" src="../UCCR/images/seq-select.png"  alt="Auswahl von sequenzieller Gruppe">.

(![](../UCCR/images/group-select.png "Typischer Bereitstellungsplan"))

*Abbildung 2. Parallele Gruppe*

Wenn Sie eine Gruppe verschieben wollen, klicken Sie auf die **Gruppenauswahlleiste** oder klicken Sie auf eine beliebige Stelle in der Gruppen und ziehen Sie diese dann an eine neue Position. 

Wenn Sie eine Gruppe kopieren möchten, klicken Sie auf das Symbol für die Aktion **Kopieren** <img class="inline" src="../UCCR/images/copy-group.png"  alt="Symbol für Aktion 'Kopieren'">, platzieren Sie den Cursor an die Stelle, an der Sie die kopierte Gruppe einfügen möchten, und klicken Sie auf das Symbol für die Aktion **Einfügen** <img class="inline" src="../UCCR/images/paste-group.png"  alt="Symbol für Aktion 'Einfügen'">.

Wenn Sie eine Gruppe ausschneiden wollen, wählen Sie die betreffende Gruppe aus und klicken Sie auf das Symbol für die Aktion **Ausschneiden** <img class="inline" src="../UCCR/images/cut-group.png"  alt="Symbol für Aktion 'Ausschneiden'">.

Wenn Sie eine Gruppe auflösen wollen, wählen Sie die entsprechende Gruppe aus und klicken Sie dann in der Leiste für die Gruppenauswahl auf das Symbol für die Aktion **Gruppe auflösen** <img class="inline" src="../UCCR/images/ungroup-icon.png"  alt="Symbol für Aktion 'Gruppen auflösen'">.

Wenn Sie die in einer Gruppe enthaltenen Tasks löschen wollen, wählen Sie die betreffende Gruppe aus und klicken Sie auf das Symbol für die Aktion **Löschen** <img class="inline" src="../UCCR/images/trash-group.png"  alt="Symbol für Aktion 'Löschen'">. Die Tasks werden aus dem Bereitstellungsplan entfernt. 

## Task-Tags verwalten
{: #tasks_tags}

Tags stellen Organisationselemente dar, die Sie zu Tasks hinzufügen können. Sie können Bereitstellungspläne nach Tags filtern. Bei einer Bereitstellung in einer Produktionsumgebung könnten Sie beispielsweise Tasks inaktivieren, die den Tag `DEV_only` enthalten, denn dieser gibt an, dass diese Tasks nur für die Entwicklungsumgebung konzipiert sind. 

Führen Sie die folgenden Schritte aus, um einen Tag zu einer Task hinzuzufügen: 

1. Wählen Sie auf der Seite mit den Bereitstellungsplandetails eine Task oder Taskgruppe aus und klicken Sie auf **Tags verwalten** <img class="inline" src="../UCCR/images/task-tag.png"  alt="Tags verwalten">. Sie können mehrere Tasks und Gruppen auswählen. 

1. Wählen Sie im Fenster 'Tags für ausgewählte Tasks verwalten' in der Liste **Allgemeine Tags** Tags aus. Sie können einen Tag erstellen, indem Sie in der Liste einen Namen in das Textfeld eingeben. 

1. Klicken Sie auf **Speichern**.

Tags werden in den Taskzeilen der Seite mit den Bereitstellungsplandetails angezeigt. Der Task 'Deploy WAR' zum Implementieren einer WAR-Datei in der folgenden Abbildung sind zwei Tags zugewiesen: `Bereitstellung` (Deployment) und `Kritisch` (Critical).

Die Tags, die ein Bereitstellungsplan verwendet, werden auf der Seite mit den Bereitstellungsplandetails auf der Registerkarte **Versionen** angezeigt. Wenn Sie eine Task als nicht anwendbar für eine Bereitstellung definieren wollen, sie also für diese Bereitstellung nicht bereitstehen soll, entfernen Sie die Tags für die betreffende Task. Tasks mit dem Status 'Nicht zutreffend' können nicht gestartet werden.   

![](../UCCR/images/task-tag-labels.png "Typischer Bereitstellungsplan")

*Abbildung 3. Task-Tags*

## Taskabhängigkeiten erstellen
{: #tasks_dependencies}

Sie können eine Task als Voraussetzung für andere Tasks definieren. Wenn eine Task als Voraussetzung fungiert, können die von ihr abhängigen Task erst gestartet werden, nachdem die vorausgesetzte Task aufgelöst wurde, selbst wenn die abhängigen Tasks ansonsten startberechtigt sind. 

Eine Task kann über mehrere abhängige Tasks und über mehrere vorausgesetzte Tasks verfügen. Sie können mit jeder anderen Task im Bereitstellungsplan Abhängigkeiten für eine Task definieren. Die Erstellung von Schleifenabhängigkeiten ist jedoch nicht zulässig. So ist es zum Beispiel nicht möglich, eine Task als abhängig von einer weiteren anderen Task zu definieren, die ihrerseits wiederum eine Abhängigkeit von der ersten Task aufweist. 

Durch die Steuerung von Taskabhängigkeiten können Sie sicherstellen, dass Ereignisse in der erwarteten Reihenfolge eintreten. 

Führen Sie die folgenden Schritte aus, um eine Task als Voraussetzung für andere Tasks zu definieren: 

1. Wählen Sie auf der Seite mit den Bereitstellungsplandetails eine Task oder Taskgruppe aus und klicken Sie auf **Voraussetzungen verwalten** <img class="inline" src="../UCCR/images/task-depend.png"  alt="Voraussetzung für Task">. Sie können mehrere Tasks und Gruppen auswählen. 

1. Wählen Sie im Fenster 'Voraussetzungen verwalten for Selected Tasks' in der Liste **Für ausgewählte Tasks vorausgesetzte Tasks** die Task aus, die als Voraussetzung fungieren soll. 

1. Klicken Sie auf **Speichern**.

Taskabhängigkeiten werden auf der Seite mit den Bereitstellungsplandetails in der Spalte für Abhängigkeiten angezeigt. Aufwärtspfeile kennzeichnen vorausgesetzte Tasks, während Abwärtspfeile auf abhängige Tasks hinweisen. 

Für die erste Task in der folgenden Abbildung sind keine Voraussetzungen festgelegt, doch sie weist zwei von ihr abhängige Tasks auf. Die zweite Task verfügt über eine vorausgesetzte Task, während sie keine abhängigen Tasks besitzt. 

(![](../UCCR/images/plan-w-depend.png "Typischer Bereitstellungsplan"))

*Abbildung 4. Taskabhängigkeiten*

Wenn Sie Abhängigkeiten überprüfen oder ändern wollen, wählen Sie die betreffende Task aus und klicken Sie auf **Voraussetzungen verwalten** <img class="inline" src="../UCCR/images/task-depend.png"  alt="Voraussetzung für Task">.
