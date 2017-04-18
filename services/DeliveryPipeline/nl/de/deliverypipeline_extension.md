---

copyright:
  years: 2015, 2016

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

# {{site.data.keyword.deliverypipeline}}-Service erweitern
{: #deliverypipeline_extending}
Letzte Aktualisierung: 29. August 2016
{: .last-updated}

Sie können die Funktionalität des {{site.data.keyword.deliverypipeline}}-Service erweitern, indem Sie Ihre Jobs für die Verwendung unterstützter Services konfigurieren. Testjobs können zum Beispiel statische Codescans ausführen und Buildjobs können Zeichenfolgen globalisieren.
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->

Die folgenden Tasks beschreiben, wie ausgewählte Tools in eine Delivery Pipeline integriert werden.

## Die Ausführung von statischen Codescans durch die Verwendung der Pipeline

{: #deliverypipeline_scan}

Sie möchten Sicherheitsprobleme in Ihrem Code finden, bevor Sie diesen bereitstellen? Wenn Sie IBM® Static Analyzer for Bluemix™ als Teil Ihrer Pipeline verwenden, können Sie automatisierte Abgleiche mit den statischen Binärdateien für den Build Ihrer Java™ App mit den Endungen `.war`, `.ear`, `.jar` oder `.class` durchführen.

Eine Pipeline, die den Service Static Analyzer verwendet, umfasst die folgenden Phasen:

+ Eine Phase für den Build der Quellendateien
+ Eine Phase für die Verarbeitung mit den folgenden Jobs:
  + Ein Buildjob für die Ausführung des Service Static Analyzer
  + Ein Buildjob für die Ausführung eines Containerbuilds
+ Eine Phase für die Bereitstellung des Containers


### Einen statischen Codescan erstellen

Lesen Sie zunächst die [Nutzungsbedingungen für den Service](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-6814-01), bevor Sie mit den nächsten Schritten beginnen.

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. Erstellen Sie eine Phase für die Verarbeitung.

  a. Klicken Sie auf **Phase hinzufügen**.

  b. Benennen Sie die Phase. Zum Beispiel: `Verarbeitung`.

  c. Wählen Sie für den Eingabetyp **Buildartefakte** aus.

  d. Überprüfen Sie die Werte für die Phase und den Job und aktualisieren Sie diese bei Bedarf.

2. Fügen Sie in der Phase für die Verarbeitung einen Buildjob hinzu, um den Codescan auszuführen.

  a. Klicken Sie auf der Registerkarte **Jobs** auf **Job hinzufügen**.

  b. Wählen Sie als Jobtyp **Test** aus.

  c. Wählen Sie als Testtyp **IBM Security Static Analyzer** aus.

  d. Überprüfen Sie die Werte für die Organisation und den Bereich und aktualisieren Sie diese bei Bedarf.

  e. Markieren Sie das Kontrollkästchen **Service und Bereich für mich einrichten** oder heben Sie die Markierung bei Bedarf auf.

    * Wenn Sie möchten, dass die Pipeline Ihren Bluemix-Bereich auf den Service und eine App überprüft, die den Service an den Container bindet, wählen Sie das Kontrollkästchen aus. Wenn der Service oder die gebundene App nicht vorhanden sind, fügt die Pipeline den freien Plan des Service zu Ihrem Bereich hinzu. Die gebundene App, die erstellt wird, hat den Namen `pipeline_bridge_app`. Anschließend verwendet die Pipeline die Berechtigungsnachweise von der Datei 'pipeline_bridge_app', um auf die gebundenen Services zuzugreifen.

    * Wenn Sie den Service und die gebundene App bereits in Ihrem Bluemix-Bereich konfiguriert haben, oder wenn Sie [diese Anforderungen manuell konfigurieren](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline) möchten, heben Sie die Markierung für das Kontrollkästchen auf.

  f. Geben Sie im Feld **Anzahl der Minuten für die Durchführung der Analyse** einen Wert zwischen 0 und 59 Minuten ein. Der Standardwert beträgt 5 Minuten. Eine URL zu dem Dashboard von Static Analyzer befindet sich in den Konsolenprotokollen am Ende des Jobs.

     Wenn der Static Analyzer-Scan nicht vor dem von Ihnen angegebenen Zeitpunkt vollständig ist, schlägt der Job fehl. Der Scananalyse wird jedoch weiter ausgeführt und Sie können sie im Dashboard von Static Analyzer anzeigen. Nachdem der Static Analyzer-Scan abgeschlossen ist, wird die Scananforderung nicht wiederholt, wenn Sie den Job erneut ausführen, und der Pipelinejob kann abgeschlossen werden. Sie können die Pipeline stattdessen auch so konfigurieren, dass sie bei einem erfolgreichen Scan nicht blockiert wird. Erläuterungen hierzu folgen beim nächsten Schritt.

  g. Wählen Sie das Kontrollkästchen **Ausführen dieser Phase beenden, wenn dieser Job fehlschlägt** abhängig davon aus bzw. ab, was passieren soll, wenn dieser Job fehlschlägt oder das Zeitlimit überschreitet. Jobs können fehlschlagen, wenn die Anfälligkeit hoch ist.

    * Wenn Sie dieses Kontrollkästchen auswählen und der Job fehlschlägt, werden nachfolgende Jobs in dieser Phase und in folgenden Phasen nicht ausgeführt.

    * Wenn Sie das Kontrollkästchen abwählen und der Job fehlschlägt, wird die Phase fortgesetzt ohne nachfolgende Jobs oder Phasen zu blockieren. Wenn Sie zum Beispiel wissen, dass der Bericht viele Sicherheitsprobleme enthält, die bearbeitet werden müssen, empfiehlt es sich, die Phase für eine Fortsetzung zu konfigurieren, da der Scan sehr zeitaufwändig sein kann. Bei diesem Szenario ist es möglicherweise ungünstig, wenn die übrigen Jobs und Phasen nur beendet werden, weil der Scan zu viel Zeit beansprucht.

  h. Klicken Sie auf **Speichern**.

3. Wenn der Job fertig gestellt ist, überprüfen Sie die Ergebnisse, indem Sie auf **Protokolle und Verlauf anzeigen** klicken. Wenn die Analyse erfolgreich war oder das Zeitlimit überschreitet, wird in den Scanergebnissen eine URL angezeigt. Wenn der Scanstatus anstehend ist, warten Sie, bis der Scan abgeschlossen ist, um die vollständigen Ergebnisse anzuzeigen.

4. Wenn Sie die Phase für die Verarbeitung erneut ausführen müssen, bevor die Analyse abgeschlossen ist, können Sie das tun. In den folgenden Situationen wird eine neue Analyse jedoch nicht erneut übergeben und die vorherigen Ergebnisse werden verwendet:
  * Die Phase für die Verarbeitung wird noch immer ausgeführt, wenn Sie eine neue Analyse gestartet haben.
  * Ein Scan wurde bereits für den Build übergeben.
  * Ein neuer Quellenbuild wurde noch nicht ausgeführt.

5. Führen Sie einen der folgenden Schritte aus, um eine neue Analyse zu starten:
  * Führen Sie die Phase für den Build aus, die Eingaben für die verarbeitende Phase liefert, und führen Sie dann die Phase für die Verarbeitung erneut aus.
  * Öffnen Sie die URL für die Scanergebnisse und klicken Sie auf das Symbol **Papierkorb**. Führen Sie anschließend die Phase für die Verarbeitung erneut aus.

Beispiele für die Konsolenausgabe:

**Erfolgreicher Scan**
![Beispiel für erfolgreichen Scan](images/analyzer_success.png)

**Anstehender Scan**
![Beispiel für anstehenden Scan](images/analyzer_pending.png)

Weitere Informationen zur Verwendung des Service Static Analyzer finden Sie in der [Dokumentation zum Service Static Analyzer](https://console.ng.bluemix.net/docs/services/ApplicationSecurityonCloud/index.html).

<!--

## Globalizing strings by using the pipeline
{: #deliverypipeline_globalize}

You can translate strings automatically into other languages when you use the IBM Globalization Pipeline service with your pipeline. IBM Globalization Pipeline uses machine translation to translate your source files as part of the pipeline's build and deployment process.

You can also update the machine-translated strings within the globalization project. A translator or native speaker of the language can then review the machine-translated strings to ensure that they are of a high quality.

To see an example of a typical pipeline that uses the Globalization Pipeline service, watch this video:

<iframe width="640" height="360" src="https://www.youtube.com/embed/UToj7FIomCg?feature=player_embedded" frameborder="0" allowfullscreen></iframe>

### Creating a globalization stage and job
Before you begin:

1. All English-translatable strings should be included in one or more `filename_en.properties` or `filename_en.json` files that all use the same name. For example: `messages_en.properties`.

2. If your messages are in `.json` files, remove the depth from the structure by removing any subkeys. To remove the subkeys, change instances of `{key: {subkey: value, subkey:value}}` to `{key:value, key:value}`.

To create the globalization stage and job:

1. Create a globalization stage.

  a. Click **ADD STAGE**.

  b. Name the stage; for example, `Globalization`.

  c. For the input type, select **SCM repository**.

2. In the globalization stage, add a job to translate the source files.

  a. On the **JOBS** tab, click **ADD JOB**.

  b. For the job type, select **Build**.

  c. For the builder type, select **IBM Globalization Pipeline**.

  d. For the organization and space, verify the values and update them if needed.

  e. In the **Source file name** field, type the name and extension of the `.properties` or `.json` input file. If you have files in different subdirectories, but they all have the same name, you need to type the file name once only. For example, if you have a `messages_en.properties` file in three directories, type `messages_en.properties` for the source file name, and all files with that name will be translated.

  f. Determine whether to select the **Set up service and space for me** check box.

    * If you want the pipeline to check your Bluemix space for the service and an app that binds the service to the container, select this check box. If the service or bound app does not exist, the pipeline adds the free plan of the service to your space for you. The bound app that is created is named `pipeline_bridge_app`. Then, the pipeline uses the credentials from pipeline_bridge_app to access the bound services.

    * If you configured the service and bound app in your Bluemix space already or if you want to [configure these requirements manually](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline), leave this check box cleared.

  g. For the Globalization bundle prefix, enter a prefix for the bundle name, which is structured in this format: `<globalization_bundle_prefix>.path.to.source.file`. The pipeline job creates this Globalization bundle for you in the Globalization Pipeline service.

    **Tip:** Use the DevOps Services project name in the prefix so that the project can be identified easily in the Globalization Pipeline service.

  h. Click **SAVE**.

3. Create another stage to package your app. For the input of the job in this stage, use the IBM Globalization Pipeline job from the previous stage. Do not use the source as the input. The Globalization Pipeline job augments the source files with the machine-translated strings.

4. To ensure that the machine-translated content is included in the packaged app, create another stage to package the app in. For the input to that stage, include the Globalization Pipeline job.

The machine translated files are placed in the same directory as the source `.properties` or `.json` file. To view the files, click **Job > Artifacts**.

After the stage is completed, you can review the translated files from the console output. You can also direct translators to the files so that they can review the machine-translation output and provide revisions to improve quality. The revisions are stored in a Cloudant™ database and take precedence over any future machine translations of the same strings.

For more information about using the Globalization Pipeline service from the Bluemix Dashboard, [see the Globalization Pipeline service documentation](https://www.ng.bluemix.net/docs/services/GlobalizationPipeline/index.html).

-->

## Pufferbenachrichtigungen für Builds in der Pipeline erstellen
{: #deliverypipeline_slack}

Sie können Benachrichtigungen über Buildergebnisse von IBM Container Service, IBM Security Static Analyzer und IBM Globalization von Ihrer Delivery Pipeline an Ihre Pufferkanäle senden.

Bevor Sie damit beginnen, erstellen oder kopieren Sie eine Puffer-WebHook-URL:

1. Öffnen Sie die Seite für die Pufferintegration für Ihr Team: `https://_project_name_.slack.com/services`
2. Suchen Sie in der Liste der Integrationen **Eingehende WebHooks** und klicken Sie auf **Hinzufügen**.
3. Wählen Sie einen Kanal aus und klicken Sie auf **Integration eingehender WebHooks hinzufügen**.
4. Fügen Sie eine **WebHook-URL** hinzu oder kopieren Sie eine vorhandene.

Weitere Informationen finden Sie in der [Pufferdokumentation zu eingehenden WebHooks](https://api.slack.com/incoming-webhooks).

Gehen Sie wie folgt vor, um Pufferbenachrichtigungen zu erstellen:

1. Öffnen Sie in der Pipeline die Konfiguration für eine Phase.
2. Klicken Sie auf der Registerkarte **UMGEBUNGSEIGENSCHAFTEN** auf **EIGENSCHAFT HINZUFÜGEN**.
3. Wählen Sie den Eintrag **Texteigenschaft** aus.
4. Geben Sie den Namen und einen Wert für die Umgebungseigenschaft ein. Wiederholen Sie dies, um mehrere Umgebungseigenschaften zu erstellen.

  *Tabelle 1. Umgebungseigenschaften für die Konfiguration von Pufferbenachrichtigungen*

  <table>
  <tr>
  <th>Name</th>
  <th>Wert</th>
  <th>Beschreibung</th>
  <tr/>
  <tr>
    <td><code>SLACK_WEBHOOK_PATH</code></td>
    <td>Eine URL</td>
    <td>Erforderlich. Die WebHook-URL, die in den Einstellungen für Ihr Pufferprojekt gespeichert ist.</td>
  </tr>
  <tr>
    <td><code>SLACK_COLOR</code></td>
    <td>Sie können einen der folgenden Werte eingeben:
      <ul><li><code>good</code></li>
      <li><code>warning</code></li>
      <li><code>danger</code></li>
      <li>Jede hexadezimale Farbe wie zum Beispiel #439FEO</li></ul></td>
    <td>Optional. Die Farbe der Begrenzung, die an der Seite der Nachricht im Puffer angezeigt wird. Die Standardfarben sind grün für gute Nachrichten, rot für schlechte Nachrichten und grau für Informationsnachrichten.</td>
  </tr>
  <tr>
    <td><code>NOTIFY_FILTER</code></td>
    <td>Geben Sie einen der folgenden Werte ein, um nur eine Teilmenge der Nachrichtentypen zu empfangen:
      <ul>
      <li><code>good</code>: Nur unbekannte, gute und Informationsnachrichten abrufen. Schlechte Nachrichten werden nicht gesendet.</li>
      <li><code>bad</code>: Alle Nachrichten abrufen.</li>
      <li><code>info</code>: Nur Informationsnachrichten abrufen. Gute, schlechte und unbekannte Nachrichten werden nicht gesendet.</li>
      <li><code>unknown</code>: Alle Nachrichten abrufen.</li></ul>
      Beispiel: Wenn Sie <code>NOTIFY_FILTER = bad</code> festlegen, werden Fehlerbenachrichtigung nur im Pufferkanal (Slack Channel) angezeigt.</td>
    <td>Optional. Entscheiden Sie, für welchen Nachrichtentyp Benachrichtigungen gesendet werden sollen. Standardmäßig werden gute und schlechte Nachrichten, jedoch keine Informationsnachrichten gesendet.
      <ul><li><code>good</code>: Erfolgreiche Buildergebnisse.</li>
      <li><code>bad</code>: Nicht erfolgreiche Buildergebnisse.</li>
      <li><code>info</code>: Informationsnachrichten über den Erstellungsprozess.</li>
      <li><code>unknown</code>: Unbekannte Nachrichten sind keinem Typ zugeordnet.</li></ul></td>
   </table>

5. Klicken Sie auf **Speichern**.

6. Wiederholen Sie diese Schritte und senden Sie Pufferbenachrichtigungen für andere Phasen, die Jobs von IBM Container Service, IBM Security Analyzer und IBM Globalization umfassen.

Die Buildbenachrichtigung, die im Puffer angezeigt wird, enthält einen Link zum Projekt der DevOps Services und gelegentlich einen Link zum Dashboard des Projekts. Damit Pufferbenutzer diesen Link öffnen können, müssen Sie bei DevOps Services registriert und Mitglied des Projekts sein, in dem die Pipeline konfiguriert ist.

## HipChat-Benachrichtigungen für Builds in der Pipeline erstellen
{: #deliverypipeline_hipchat}

Sie können Benachrichtigungen über Buildergebnisse von IBM Container Service, IBM Security Static Analyzer und IBM Globalization von Ihrer Delivery Pipeline an Ihre HipChat-Rooms senden.

Bevor Sie damit beginnen, erstellen oder kopieren Sie ein vorhandenes HipChat-Token:

1. Wechseln Sie auf die Seite mit dem HipChat-Account für Ihr Team: `https://_project_name_.hipchat.com/account/api`
2. Erstellen Sie ein neues Token oder verwenden Sie ein vorhandenes Token.

Gehen Sie wie folgt vor, um HipChat-Benachrichtigungen zu erstellen:

1. Öffnen Sie in der Pipeline die Konfiguration für eine Phase.
2. Klicken Sie auf der Registerkarte **UMGEBUNGSEIGENSCHAFTEN** auf **EIGENSCHAFT HINZUFÜGEN**.
3. Wählen Sie **Texteigenschaft** aus.
4. Geben Sie den Namen und einen Wert für die Umgebungseigenschaft ein. Wiederholen Sie dies, um mehrere Umgebungseigenschaften zu erstellen.

  *Tabelle 2. Umgebungseigenschaften für die Konfiguration von HipChat-Benachrichtigungen*

  <table>
  <tr>
  <th>Name</th>
  <th>Wert</th>
  <th>Beschreibung</th>
  </tr>
  <tr>
    <td><code>HIP_CHAT_TOKEN</code></td>
    <td>Alphanumerische Zeichenfolge</td>
    <td>Erforderlich. Lesen Sie im Abschnitt "Vorbemerkungen" die Anweisungen zum Erstellen oder Kopieren eines vorhandenen HipChat-Tokens.</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_ROOM_NAME</code></td>
    <td>Raumname</td>
    <td>Erforderlich.</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_COLOR</code></td>
    <td>Geben Sie einen der folgenden Werte ein:
      <ul><li><code>yellow</code></li>
      <li><code>red</code></li>
      <li><code>green</code></li>
      <li><code>purple</code></li>
      <li><code>gray</code></li>
      <li><code>random</code></li></ul>
    </td>
    <td>Optional: Geben Sie eine Hintergrundfarbe und eine Umrandungsfarbe für HipChat-Benachrichtigungen ein. Wenn Sie <code>HIP_CHAT_COLOR</code> festlegen, müssen Sie die Farbe nicht angeben, wenn Sie das Script aufrufen.
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_COLOR</code></td>
    <td>Geben Sie einen der folgenden Werte ein:
      <ul><li><code>good</code></li>
      <li><code>danger</code></li>
      <li><code>info</code></li></ul>
    Diese Variable gilt sowohl für HipChat- als auch für Pufferhinweisfarben. Wenn Sie <code>NOTIFICATION_COLOR</code> angeben, müssen Sie weder <code>HIP_CHAT_COLOR</code> noch <code>SLACK_COLOR</code> angeben.</td>
    <td>Optional: Geben Sie die Hintergrundfarbe und die Umrandungsfarbe sowohl für HipChat- als auch für Pufferbenachrichtigungen an. Wenn Sie <code>NOTIFICATION_COLOR</code> festlegen, müssen Sie die Farbe nicht angeben, wenn Sie das Script aufrufen.
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_LEVEL</code></td>
    <td>Geben Sie einen der folgenden Werte ein:
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul></td>
    <td>Optional: Geben Sie die Benachrichtigungsstufe an. Weitere Einzelheiten über Auslöser der Benachrichtigung finden Sie unter <code>NOTIFICATION_FILTER</code>.</td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_FILTER</code></td>
    <td>Geben Sie einen der folgenden Werte ein:
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul>
    <td>Optional: Geben Sie die Ebene des Benachrichtigungsfilters an. Benachrichtigungen werden gesendet, wenn die folgenden Parameter übereinstimmen:
      <ul><li><code>NOTIFICATION_FILTER = good</code> und <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code> oder <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = info</code> und <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code>, <code>info</code> oder <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = bad</code> und <code>NOTIFICATION_LEVEL = bad</code> oder <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = unknown</code> und <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code> oder <code>unknown</code></li></ul></td>
    </tr>
  </table>

5. Klicken Sie auf **Speichern**.

6. Wiederholen Sie diese Schritte, um HipChat-Benachrichtigungen für andere Phasen zu senden, die Jobs von IBM Container Service, IBM Security Static Analyzer und IBM Globalization enthalten.

## Active Deploy für Bereitstellungen ohne Ausfallzeit in der Pipeline verwenden
{: #deliverypipeline_activedeploy}

Sie können die kontinuierliche Bereitstellung von Ihren Apps oder Containergruppen durch die Verwendung des Service IBM® Active Deploy in der Bluemix® DevOps Services Delivery-Pipeline automatisieren. Weitere Informationen zu ersten Schritten finden Sie in der [Dokumentation zu Active Deploy](https://new-console.ng.bluemix.net/docs/services/ActiveDeploy/updatingapps.html#adpipeline).

## Containerimages mit der Pipeline erstellen und bereitstellen
{: #deliverypipeline_containers}

Sie können Ihre App-Builds und Containerbereitstellungen in Bluemix® mithilfe der IBM® Continuous Delivery Pipeline for Bluemix automatisieren. Der Service Delivery Pipeline in den DevOps-Srvices unterstützt:
  - Erstellen von Docker-Images
  - Bereitstellen von Images in Containern für Bluemix

Weitere Informationen zu den ersten Schritten finden Sie in der [Übersicht über Delivery Pipeline und Container](https://new-console.ng.bluemix.net/docs/containers/container_pipeline_ov.html#container_pipeline_ov).
