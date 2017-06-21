---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}    

# Toolintegrationen konfigurieren
{: #integrations}

Sie können Toolintegrationen konfigurieren, die Entwicklungs-, Bereitstellungs- und Systemtasks unterstützen, während Sie eine offene Toolchain erstellen, oder Sie können Toolintegrationen hinzufügen und konfigurieren, um eine vorhandene Toolchain anzupassen.  
{:shortdesc}

Die Toolintegrationen, die zum Hinzufügen und Konfigurieren für Ihre Toolchain zur Verfügung stehen, sind unterschiedlich, abhängig davon, ob Sie Toolchains unter {{site.data.keyword.Bluemix_notm}} Public oder {{site.data.keyword.Bluemix_notm}} Dedicated verwenden. Falls Sie Toolchains bei {{site.data.keyword.Bluemix_notm}} Dedicated verwenden, variieren die für Sie verfügbaren Toolintegrationen abhängig davon, wie {{site.data.keyword.contdelivery_full}} in Ihrer speziellen Umgebung konfiguriert wurde.

|Toolintegration |Verfügbar unter {{site.data.keyword.Bluemix_notm}} Public	|Verfügbar unter {{site.data.keyword.Bluemix_notm}} Dedicated (umgebungsabhängig)|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.alertnotificationshort}}		|Ja		|Nein		|
|Artifactory		|Ja		|Nein		|
|Availability Monitoring		|Ja		|Nein		|
|Cloud Event Management		|Ja		|Nein		|
|{{site.data.keyword.deliverypipeline}} 		|Ja	   	|Ja  		|
|{{site.data.keyword.DRA_short}} 		|Ja		|Nein			|
|Eclipse Orion {{site.data.keyword.webide}}		|Ja		|Ja			|
|Git Repos and Issue Tracking	|Ja		|Nein		|
|GitHub Issues		|Ja		|Ja		|
|Dedicated {{site.data.keyword.ghe_short}} und Issues			|Nein		|Ja		|
|Jenkins		|Ja		|Nein		|
|JIRA		|Ja		|Nein		|
|Nexus			|Ja		|Nein		|
|Anderes Tool			|Ja		|Ja		|
|PagerDuty			|Ja		|Ja		|
|Sauce Labs		|Ja		|Nein		|
|Slack			|Ja		|Ja		|
|SonarQube			|Ja		|Nein		|
{: caption="Tabelle 1. Toolintegrationen, die für Toolchains unter Bluemix Public und Bluemix Dedicated verfügbar sind" caption-side="top"}

**Tipp:** Wenn Sie beginnen möchten, mit Ihrem eigenen Quellcode unter {{site.data.keyword.Bluemix_notm}} Public
zu entwickeln, müssen Sie vor dem Konfigurieren von {{site.data.keyword.deliverypipeline}} zuerst die GitHub-Toolintegration oder die
Git Repos and Issue Tracking-Toolintegration konfigurieren. Wenn Sie beginnen möchten, mit Ihrem eigenen Code unter {{site.data.keyword.Bluemix_notm}} Dedicated zu entwickeln, müssen Sie die {{site.data.keyword.ghe_short}}-Toolintegration oder die GitHub-Toolintegration vor der {{site.data.keyword.deliverypipeline}} konfigurieren.


## Alert Notification konfigurieren (Experimentell)
{: #alertnotification}

{{site.data.keyword.alertnotificationfull}} ist eine cloudbasierte Hybridlösung, mit der Sie Ihre Benachrichtigungsstrategie zentralisieren und vereinfachen können. Sie arbeitet mit anderen cloudbasierten und lokalen Anwendungen zusammen. Alerts werden anhand einer sicheren REST-konformen API an {{site.data.keyword.alertnotificationshort}} weitergeleitet.

Konfigurieren Sie {{site.data.keyword.alertnotificationshort}}, um bei Problemen während Ihres DevOps-Prozesses Benachrichtigungen zu erhalten.

### Voraussetzungen

1. Falls Sie nicht bereits über ein {{site.data.keyword.alertnotificationshort}}-Konto verfügen, melden Sie sich wie folgt für ein solches Konto an:

 a. Öffnen Sie die Seite für [IBM {{site.data.keyword.alertnotificationshort}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/us-en/marketplace/alert-notification){: new_window} in IBM Marketplace.

 b. Erwerben Sie entweder ein Abonnement oder melden Sie sich für die kostenlose 90-Tage-Testversion an.

1. Nachdem Ihr {{site.data.keyword.alertnotificationshort}}-Konto eingerichtet ist, öffnen Sie [My IBM Dashboard ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://myibm.ibm.com/dashboard/){: new_window}.
1. Klicken Sie neben IBM {{site.data.keyword.alertnotificationshort}} auf **Starten**.
1. Klicken Sie auf **API-Schlüssel verwalten** und dann auf **API-Schlüssel erstellen**.
1. Geben Sie im Feld **API-Schlüssel erstellen** eine Beschreibung ein.
1. Klicken Sie auf **Generieren**. Die Informationen für den neuen API-Schlüssel einschließlich Name und Kennwort werden angezeigt. Da Sie diese Informationen für die Konfiguration der Toolintegration benötigen, schließen Sie das Fenster 'Neuer API-Schlüssel' nicht. Aus Sicherheitsgründen kann das Kennwort für den API-Schlüssel später nicht mehr abgerufen werden.

### Alert Notification konfigurieren

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **{{site.data.keyword.alertnotificationshort}}**.
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite Ihrer App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** klicken. Klicken Sie anschließend auf **Übersicht**.  

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf **{{site.data.keyword.alertnotificationshort}}**.

1. Geben Sie die URL für die {{site.data.keyword.alertnotificationshort}}-API ein, die Sie verwenden wollen. Sie finden die entsprechende URL auf der Seite 'API-Schlüssel verwalten' des {{site.data.keyword.alertnotificationshort}}-Service, wie zum Beispiel `https://ibmnotifybm.mybluemix.net/api/alerts/v1`.
1. Geben Sie den Namen des API-Schlüssels für {{site.data.keyword.alertnotificationshort}} ein. Den Namen des API-Schlüssels finden Sie im Fenster 'Neuer API-Schlüssel'.
1. Geben Sie das Kennwort ein, das {{site.data.keyword.alertnotificationshort}} für den API-Schlüssel generiert hat. Das Kennwort für den API-Schlüssel finden Sie im Fenster 'Neuer API-Schlüssel'.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie von Ihrer Toolchain aus auf **{{site.data.keyword.alertnotificationshort}}**.

Weitere Informationen finden Sie unter [IBM {{site.data.keyword.alertnotificationshort}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/manage/tool_alert_notification/){: new_window}.


## Artifactory konfigurieren
{: #artifactory}

Konfigurieren Sie den Repository-Manager von Artifactory zum Speichern von Buildartefakten in Ihrem Artifactory-Repository (Repo). Gehen Sie dazu wie folgt vor:

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **Artifactory**.
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite Ihrer App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** klicken. Klicken Sie anschließend auf **Übersicht**.  

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf **Artifactory**.

1. Geben Sie die URL für das Artifactory-Repository (Repo) ein, das geöffnet werden soll, wenn Sie auf die Karte für Artifactory klicken.
1. Wählen Sie den Repository-Typ aus, zu dem eine Verbindung hergestellt werden soll.
1. Wenn Sie eine Artifactory-npm-Registry verwenden, führen Sie die folgenden Schritte aus:

 a. Geben Sie die E-Mail-Adresse ein, die Ihrer Registry zugeordnet ist.

 b. Geben Sie das Authentifizierungstoken ein, das Ihrer Registry zugeordnet ist.

 c. Geben Sie die URL für Ihr Artifactory-Release-Repository ein. Dieses Repository ist Ihre private Registry auf dem Artifactory-Server.

 d. Geben Sie die URL für die Spiegelregistry oder die öffentliche Registry ein, die Sie verwenden, um mehrere öffentliche und private npm-Registrys miteinander zu kombinieren. Bei dieser URL kann es sich beispielsweise um die URL der virtuellen Registry auf Ihrem Artifactory-Server handeln, die sowohl auf Ihre private Registry als auch auf einen Cachespeicher der globalen npm-Registry Zugriff hat.

1. Wenn Sie eine Artifactory-Maven-Registry verwenden, führen Sie die folgenden Schritte aus:

 a. Geben Sie die Benutzer-ID ein, die Ihrem Repository zugeordnet ist.

 b. Geben Sie das Kennwort ein, das Ihrem Repository zugeordnet ist.

 c. Geben Sie die URL für Ihr Artifactory-Release-Repository ein. Dieses Repository ist Ihr privates Release-Repository auf dem Artifactory-Server.

 d. Geben Sie die URL für Ihr Artifactory-Snapshot-Repository ein. Dieses Repository ist Ihr privates Snapshot-Repository auf dem Artifactory-Server.

 e. Geben Sie die URL für das Spiegelrepository oder das öffentliche Repository ein, das Sie verwenden, um mehrere öffentliche und private Maven-Repositorys miteinander zu kombinieren. Bei dieser URL kann es sich beispielsweise um die URL des virtuellen Repositorys auf Ihrem Artifactory-Server handeln, das sowohl auf Ihre privaten Repositorys als auch auf einen Cachespeicher des zentralen Maven-Repositorys Zugriff hat.

1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Karte für das Artifactory-Repository, mit dem Sie arbeiten möchten. Daraufhin wird die Artifactory-Website geöffnet, auf der Sie den Inhalt des Repositorys anzeigen können.
1. Optional: Wenn Sie eine Toolchain unter {{site.data.keyword.Bluemix_notm}} Public verwenden und Sie Ihre App unter Verwendung von Artifactory mit npm erstellen wollen, konfigurieren Sie Ihre Pipeline durch Hinzufügen eines npm-Buildjobs. Anweisungen zum Konfigurieren des Buildjobs enthält der Abschnitt [Artifactory-npm-Buildjob in Ihrer Pipeline konfigurieren](#config_artifactory_npm).
1. Optional: Wenn Sie eine Toolchain unter {{site.data.keyword.Bluemix_notm}} Public verwenden und Sie Ihre App unter Verwendung von Artifactory mit Maven erstellen wollen, konfigurieren Sie Ihre Pipeline durch Hinzufügen eines Maven-Buildjobs. Anweisungen zum Konfigurieren des Buildjobs enthält der Abschnitt [Artifactory-Maven-Buildjob in Ihrer Pipeline konfigurieren](#config_artifactory_maven).

### Artifactory-npm-Buildjob in Ihrer Pipeline konfigurieren
{: #config_artifactory_npm}

Bevor Sie einen npm-Buildjob in Ihrer Pipeline konfigurieren, müssen Sie über eine funktionstüchtige Pipeline verfügen, die Ihr SCM-Build-Repository als Eingabe verwenden kann. Außerdem müssen Sie Artifactory für Ihre Toolchain konfigurieren. Anweisungen zum Konfigurieren von Artifactory enthält der Abschnitt [Artifactory](#artifactory).

Konfigurieren Sie {{site.data.keyword.deliverypipeline}} durch Hinzufügen eines npm-Buildjobs. Gehen Sie dazu wie folgt vor:

1. Erstellen Sie eine Stage und geben Sie das entsprechende SCM-Repository für die Eingabe an.
1. Fügen Sie in der Stage einen Buildjob hinzu.
1. Konfigurieren Sie den Buildjob wie folgt:
  ![npm-Build-Job](images/artifactory_npm_job.png)

  a. Wählen Sie als Buildertyp den Typ **NPM-Build** aus.

  b. Falls Sie mehrere Instanzen der Artifactory-Toolintegration konfiguriert haben, geben Sie den Namen der Artifactory-Toolintegration ein, für die Sie den npm-Buildjob konfigurieren wollen.

  c. Wählen Sie als Toolintegrationtyp den Typ **Artifactory** aus.

  d. Geben Sie beim Buildbefehl die Befehle zum Erstellen Ihres npm-Moduls ein oder die Befehle zum Veröffentlichen des Moduls in Ihrer Registry. Das nachfolgende Beispiel zeigt die Befehle zum Erstellen (Builden) des Moduls bzw. zum Veröffentlichen.
     ```
     npm install
     # oder
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **Tipp:** Sie finden die URL und die Benutzerberechtigungsnachweise, die Sie für die Verbindungsherstellung mit Ihrer
Registry verwendet haben, in den Konfigurationseinstellungen für die Artifactory-Toolintegration.
  e. Wenn Ihr Buildjob in der Artifactory-Registry veröffentlicht wird und die Version Ihres Knotenmoduls das Format `x.y.z-SNAPSHOT.w` aufweist, wählen Sie das Kontrollkästchen **Versionsangabe für Snapshot-Modul inkrementieren** aus. Der Buildjob aktualisiert die Modulversion automatisch, bevor er die Veröffentlichung in der Artifactory-Registry ausführt. Der Job wählt die höchste Version des Moduls aus der npm-Registry und der lokalen `package.json`-Datei aus und erhöht den Wert für die Modulversion unter Verwendung von SemVer (Semantic Versioning). Der Buildjob übermittelt die Änderungen nicht an das SCM-Repository.

1. Klicken Sie auf **SPEICHERN**. Wann immer Ihre Pipeline ausgeführt wird, verwendet dieser Buildjob die Konfigurationsinformationen aus der Artifactory-Toolintegration, um eine Verbindung zu Ihrer npm-Registry herzustellen.

### Artifactory-Maven-Buildjob in Ihrer Pipeline konfigurieren
{: #config_artifactory_maven}

Bevor Sie einen Maven-Buildjob in Ihrer Pipeline konfigurieren, müssen Sie über eine funktionstüchtige Pipeline verfügen, die Ihr SCM-Build-Repository als Eingabe verwenden kann. Außerdem müssen Sie Artifactory für Ihre Toolchain konfigurieren. Anweisungen zum Konfigurieren von Artifactory enthält der Abschnitt [Artifactory](#artifactory).

Konfigurieren Sie {{site.data.keyword.deliverypipeline}} durch Hinzufügen eines Maven-Buildjobs. Gehen Sie dazu wie folgt vor:

1. Erstellen Sie eine Stage und geben Sie das entsprechende SCM-Repository für die Eingabe an.
1. Fügen Sie in der Stage einen Buildjob hinzu.
1. Konfigurieren Sie den Buildjob wie folgt:
  ![Maven-Build-Job](images/artifactory_maven_job.png)

  a. Wählen Sie als Buildertyp den Typ **Maven-Build** aus.

  b. Falls Sie mehrere Instanzen der Artifactory-Toolintegration konfiguriert haben, geben Sie den Namen der Artifactory-Toolintegration ein, für die Sie den Maven-Buildjob konfigurieren wollen.

  c. Wählen Sie als Toolintegrationtyp den Typ **Artifactory** aus.

  d. Geben Sie beim Buildbefehl die Befehle zum Erstellen Ihres Maven-Moduls ein oder die Befehle zum Veröffentlichen des Moduls in Ihrer Registry. Das nachfolgende Beispiel zeigt die Befehle zum Erstellen (Builden) bzw. zum Veröffentlichen des Moduls in einer Snapshot-Registry.
     ```
     mvn -B clean package
     # oder
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **Tipp:** Sie finden die URL und die Benutzerberechtigungsnachweise, die Sie für die Verbindungsherstellung mit Ihrer
Registry verwendet haben, in den Konfigurationseinstellungen für die Artifactory-Toolintegration.
1. Klicken Sie auf **SPEICHERN**. Wann immer Ihre Pipeline ausgeführt wird, verwendet dieser Buildjob die Konfigurationsinformationen aus der Artifactory-Toolintegration, um eine Verbindung zu Ihrem Maven-Repository herzustellen.

Weitere Informationen enthält [Artifactory ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/deliver/tool_artifactory/){: new_window}.


## Availability Monitoring hinzufügen
{: #availabilitymonitoring}

{{site.data.keyword.prf_hublong}} isoliert Probleme, identifiziert Muster und verbessert die Leistung, bevor Benutzer Beinträchtigungen erfahren. Sie können Ihre App von Standorten auf der ganzen Welt testen, mit Delivery Pipelines integrieren und Erkenntnisse dazu erlangen, wie Sie Ihren Code fortlaufend optimieren können.

**Hinweis:** Diese Toolintegration ist vorkonfiguriert und erfordert keine Konfigurationsparameter. Sie können diese Toolkonfiguration nicht neu konfigurieren.

Fügen Sie die {{site.data.keyword.prf_hubshort}}-Toolintegration hinzu, um den Zustand Ihrer App während des eigentlichen Buildvorgangs zu testen, zu überwachen und zu verbessern. Gehen Sie dazu wie folgt vor:

1. Klicken Sie im DevOps-Dashboard auf der Seite 'Toolchains' auf die Toolchain, zu der Sie
{{site.data.keyword.prf_hubshort}} hinzufügen wollen. Alternativ können Sie auf der Übersichtsseite der App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** und dann auf **Übersicht** klicken.

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf **{{site.data.keyword.prf_hubshort}}**.

1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf **{{site.data.keyword.prf_hubshort}}**, um das {{site.data.keyword.prf_hubshort}}-Dashboard zu öffnen, wählen Sie eine App aus und konfigurieren Sie die Überwachung für diese App.

Weitere Informationen enthält [{{site.data.keyword.prf_hublong}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/manage/tool_bluemix_availability_monitoring/){: new_window}.


## Cloud Event Management hinzufügen (Experimentell)
{: #cloudeventmanagement}

{{site.data.keyword.evtmgt_full}} stellt eine konsolidierte Ansicht der Probleme bereit, die in Verbindung mit Ihren Services, Ihren Anwendungen und Ihrer Infrastruktur auftreten. Zur effizienteren Behebung von Problemen können Sie echtzeitorientiertes Vorfallmanagement einrichten.

**Hinweis:** Diese Toolintegration ist vorkonfiguriert und erfordert keine Konfigurationsparameter. Sie können sie nicht neu konfigurieren.

Fügen Sie Cloud Event Management zu Ihrer Toolchain hinzu, um Ihrem DevOps-Team bei der Umsetzung seiner Ziele in Form von zuverlässigem Betriebszustand, hoher Servicequalität und kontinuierlicher Verbesserung zu helfen. Gehen Sie dazu wie folgt vor:

1. Klicken Sie im DevOps-Dashboard auf **Toolchains**. Klicken Sie auf die Toolchain, zu der Sie Cloud Event
Management hinzufügen möchten. Alternativ können Sie auf der Übersichtsseite Ihrer App auf der Karte für Continuous Delivery
auf **Toolchain anzeigen** und dann auf **Übersicht** klicken. 

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf **Cloud Event Management**.

1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie von Ihrer Toolchain aus auf eine Karte der folgenden Tools:

 * **Cloud Event Management**, um mit der Verwendung von Cloud Event Management zu beginnen.

 * **{{site.data.keyword.alertnotificationshort}}**, um Richtlinien zu erstellen, die bestimmen, wann Benutzer Benachrichtigungen zu Vorfällen erhalten.

 * **Runbook Automation**, um Ihren Katalog von Runbooks in Cloud Event Management zu verwalten.

Weitere Informationen finden Sie in [Cloud Event
Management ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/manage/tool_cloud_event_mgt/){: new_window}. 


## Delivery Pipeline konfigurieren
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}} automatisiert die kontinuierliche Entwicklung Ihrer Projekte durch aufeinanderfolgende Stages, in denen Eingaben abgerufen und Jobs wie Builds, Tests und Bereitstellungen ausgeführt werden.

Konfigurieren Sie {{site.data.keyword.deliverypipeline}}, um das kontinuierliche Erstellen, Testen und Bereitstellen Ihrer Apps zu automatisieren. Gehen Sie dazu wie folgt vor:

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **{{site.data.keyword.deliverypipeline}}**. Abhängig von der Vorlage, die Sie verwenden, sind unterschiedliche Felder verfügbar. Überprüfen Sie die Standardfeldwerte und ändern Sie diese Einstellungen gegebenenfalls.
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite Ihrer der App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** und dann auf **Übersicht** klicken.

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf **{{site.data.keyword.deliverypipeline}}**.

1. Geben Sie einen Namen für Ihre neue Pipeline an.
1. Wenn Sie mithilfe Ihrer Pipeline eine Benutzerschnittstelle bereitstellen möchten, wählen Sie das Kontrollkästchen **Apps im Menü 'App anzeigen' anzeigen** aus. Alle Apps, die Ihre Pipeline erstellt, werden in der Liste **App anzeigen** auf der Übersichtsseite der Toolchain angezeigt.
1. Klicken Sie auf **Integration erstellen**, um die {{site.data.keyword.deliverypipeline}} zu Ihrer Toolchain hinzuzufügen.
1. Klicken Sie auf **{{site.data.keyword.deliverypipeline}}**, um die Pipeline anzuzeigen und zu konfigurieren. Die Grundlagen des Konfigurierens einer Pipeline finden Sie unter [Pipelines erstellen und bereitstellen](/docs/services/ContinuousDelivery/pipeline_build_deploy.html){: new_window}.

  **Tipp:** Wenn Sie die Pipeline automatisch ausführen möchten, wenn Sie Commitoperationen per Push-Operation an
ein GitHub-, {{site.data.keyword.ghe_short}}- oder Git-Repository (Repo) übertragen, führen Sie folgende Schritte aus: 

   a. Konfigurieren Sie GitHub, {{site.data.keyword.ghe_short}} oder Git Repos and Issue Tracking für Ihre Toolchain, bevor
Sie die Stages für Ihre Pipeline definieren. Die Pipeline-Stages benötigen die Git-URLs für Ihre Repositorys. Jede Pipeline-Stage kann nur auf eines der GitHub-, {{site.data.keyword.ghe_short}}- oder Git-Repositorys verweisen, die Ihrer Toolchain zugeordnet sind. Anweisungen zum Konfigurieren von GitHub finden Sie im Abschnitt [GitHub](#github). Anweisungen zum Konfigurieren von Dedicated {{site.data.keyword.ghe_short}} enthält die [Einführung in {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window}. Anweisungen zum Konfigurieren von Git Repos and Issue Tracking enthält der Abschnitt [Git Repos and Issue Tracking](##gitbluemix).

   b. Verwenden Sie einen Web-Hook. Ohne Web-Hook können Sie Pipelines nur manuell ausführen. Damit Sie einen Web-Hook verwenden
können, wenn Sie eine Verbindung zu einem GitHub- oder {{site.data.keyword.ghe_short}}-Repository herstellen, benötigen Sie
Administratorberechtigungen. Zum Herstellen einer Verbindung zu einem Git Repos and Issue Tracking-Repository benötigen Sie Berechtigungen
als Master oder Eigner. 

1. Optional: Wenn Sie eine Toolchain unter {{site.data.keyword.Bluemix_notm}} Public verwenden und Sie möchten, dass Sauce Labs Ihre App testet, konfigurieren Sie die {{site.data.keyword.deliverypipeline}}, um einen Sauce Labs-Testjob hinzuzufügen. Anweisungen zum Konfigurieren des Testjobs finden Sie im Abschnitt [Sauce Labs-Testjob in Ihrer Pipeline konfigurieren](#config_saucelabs).

### Sauce Labs-Testjob in Ihrer Pipeline konfigurieren
{: #config_saucelabs}

Bevor Sie einen Sauce Labs-Testjob in Ihrer Pipeline konfigurieren, brauchen Sie eine funktionstüchtige Pipeline, die Stages zum Erstellen und Bereitstellen Ihrer App umfasst, und Sie müssen Sauce Labs für Ihre Toolchain konfigurieren. Anweisungen zum Konfigurieren von Sauce Labs finden Sie im Abschnitt [Sauce Labs](#saucelabs).

Konfigurieren Sie die {{site.data.keyword.deliverypipeline}}, um einen Sauce Labs-Testjob hinzuzufügen:

1. Wenn keine Stage vorhanden ist, die eine Testversion Ihrer App bereitstellt, erstellen Sie eine.
1. Fügen Sie in der Stage nach dem Bereitstellungsjob einen Testjob hinzu. Indem Sie diese Jobs in derselben Stage platzieren, können sie auf dieselbe Gruppe von Umgebungseigenschaften zugreifen.   
  ![Testjob](images/toolchain_test_job.png)

1. Konfigurieren Sie die Stage:

  a. Erstellen Sie auf der Registerkarte **UMGEBUNGSEIGENSCHAFTEN** drei Eigenschaften: CF_APP_NAME, SAUCE_USERNAME und SAUCE_ACCESS_KEY.

  b. Geben Sie Ihren Sauce Labs-Benutzernamen und -Zugriffsschlüssel ein. Dadurch stellen Sie diese Werte extern bereit und können sie in Ihren Tests verwenden.

1. Konfigurieren Sie den Bereitstellungsjob. Schließen Sie im Feld **Bereitstellungsscript** diesen Befehl ein: `export CF_APP_NAME="$CF_APP"`. Der Befehl exportiert den Namen der App als Umgebungseigenschaft.
1. Konfigurieren Sie den Testjob. Die Werte in der folgenden Abbildung sind Beispiele. In die Felder **Serviceinstanz**, **Ziel**, **Organisation** und **Bereich** werden der Sauce Labs-Benutzername, die Region, die Organisation und der Bereich eingetragen, die Sie verwenden.  
![Job konfigurieren](images/toolchain_configure_job.png)

  Wählen Sie als Testertyp **Sauce Labs** aus.

  b. Wählen Sie als Serviceinstanz den Sauce Labs-Benutzernamen aus, den Sie beim Konfigurieren von Sauce Labs für Ihre Toolchain verwendet haben.

   **Tipp:** Um zu sehen, welchen Benutzernamen und Zugriffsschlüssel Sie beim Konfigurieren von Sauce Labs für Ihre
Toolchain verwendet haben, klicken Sie auf **Konfigurieren**. 

  c. Geben Sie im Feld **Befehl für die Testausführung** die Befehle ein, die die für Ihre Tests erforderlichen Abhängigkeiten installieren, und führen Sie dann die Tests aus. Für eine Node.js-App würden Sie beispielsweise folgende Befehle eingeben:
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```

    d. Wenn Sie Ihre Testberichte in den Testjobprotokollen anzeigen möchten, wählen Sie das Kontrollkästchen **Testbericht aktivieren** aus und legen Sie Dateimuster für Testergebnisse auf `test/*.xml` fest.

1. Klicken Sie auf **SPEICHERN**. Immer, wenn Ihre Pipeline aktiv ist, werden Sauce Labs-Tests ausgeführt.

Weitere Informationen enthält [Delivery Pipeline ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/deliver/tool_delivery_pipeline/){: new_window}.


## DevOps Insights hinzufügen (Beta)
{: #dra}

{{site.data.keyword.DRA_full}} erfasst und analysiert die Ergebnisse von Komponententests, Funktionstests und Codeabdeckungstools, um zu bestimmen, ob Ihr Code vordefinierte Kriterien an angegebenen Punkten in Ihrem Bereitstellungsprozess erfüllt. Falls Ihr Code die Kriterien nicht erfüllt oder mehr als erfüllt, wird die Bereitstellung gestoppt, um keine Risiken einzuführen. Sie können {{site.data.keyword.DRA_short}} als Sicherheitsnetz für Ihre kontinuierliche Bereitstellungsumgebung oder als Methode zum Implementieren und Verbessern von Qualitätsstandards einsetzen.

 **Hinweis:** Diese Toolintegration ist nur in {{site.data.keyword.Bluemix_notm}} Public verfügbar. Sie ist vorkonfiguriert und erfordert keine Konfigurationsparameter. Sie können diese Toolkonfiguration nicht neu konfigurieren.

Fügen Sie {{site.data.keyword.DRA_short}} hinzu, um die Qualität Ihres Codes in {{site.data.keyword.Bluemix_notm}} aufrechtzuerhalten und zu verbessern, indem Sie Ihre Bereitstellungen überwachen und Risiken erkennen, bevor sie eingeführt werden.

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **{{site.data.keyword.DRA_short}}**.
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** und dann auf **Übersicht** klicken.

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf **{{site.data.keyword.DRA_short}}**.

1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf **{{site.data.keyword.DRA_short}}** und führen Sie dann die anfänglichen Schritte aus: Kriterien erstellen, Kriterien mit der Pipeline verknüpfen und Pipeline ausführen.

Weitere Informationen enthält [{{site.data.keyword.DRA_short}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/learn/tool_devops_insights/){: new_window}.


## Eclipse Orion-Web-IDE hinzufügen
{: #webide}

Die Eclipse Orion-{{site.data.keyword.webide}} ist eine integrierte webbasierte Umgebung, in der Sie Quellcodeverwaltungstasks erstellen, bearbeiten, ausführen, debuggen und abschließen können. Sie können nahtlos von der Bearbeitung zur Ausführung, zur Übergabe und zur Bereitstellung übergehen.

 **Hinweis:** Diese Toolintegration ist vorkonfiguriert. Sie erfordert keine Konfigurationsparameter und Sie können sie nicht neu konfigurieren.

Fügen Sie die Toolintegration der Eclipse Orion-{{site.data.keyword.webide}} hinzu, um Quellcodeverwaltungstasks auszuführen:

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren
Integrationen auf **Eclipse Orion-Web-IDE**. 
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** und dann auf **Übersicht** klicken.

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf die Option für die **Eclipse Orion-Web-IDE**. 

1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf **Eclipse Orion-Web-IDE**. In Ihrem Arbeitsbereich sind Ihre GitHub- oder {{site.data.keyword.ghe_short}}-Repositorys bereits aufgeführt. Die Repositorys, die Ihrer aktuellen Toolchain zugeordnet sind, sind hervorgehoben.

Weitere Informationen enthalten [Code mit der {{site.data.keyword.webide}} für Eclipse Orion bearbeiten](/docs/services/ContinuousDelivery/web_ide.html){: new_window} und [Eclipse Orion-{{site.data.keyword.webide}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/code/tool_eclipse_orion_web_ide/){: new_window}.


## Git Repos and Issue Tracking (Beta) konfigurieren 
{: #gitbluemix}

Die Git Repos and Issue Tracking-Toolintegration basiert auf GitLab Community Edition, einem webbasierten Hosting-Service für Git-Repositorys. Sie können sowohl über lokale als auch über ferne Kopien Ihrer Repositorys verfügen. Weitere
Informationen enthält [Git Repos and Issue Tracking
![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://git.ng.bluemix.net/help){:new_window}. 

Wenn Sie Git Repos and Issue Tracking konfigurieren, während Sie die Toolchain erstellen, führen Sie diese Schritte aus:    

1. a. Klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **Git Repos and Issue Tracking**.
1. Überprüfen Sie die Standardzielspeicherorte für die Git-Repositorys. Diese Repositorys werden aus den Beispielrepositorys geklont. Ändern Sie gegebenenfalls die Namen der Zielrepositorys.

Wenn Sie Git Repos and Issue Tracking zu einer bereits vorhandenen Toolchain hinzufügen, führen Sie diese Schritte aus:    

1. Klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** und dann auf **Übersicht** klicken.
1. Klicken Sie auf **Tool hinzufügen**.
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf **Git Repos and Issue Tracking**.
1. Wählen Sie einen Repository-Typ aus. Gehen Sie dazu wie folgt vor:     

  a. Um ein leeres Repository zu erstellen, klicken Sie für den Repository-Typ auf **Neu** und geben Sie einen Repository-Namen ein.    
  b. Um ein Git-Repository zu verzweigen, sodass Sie Änderungen über Zusammenführungsanforderungen (Merge) beitragen können, klicken Sie auf **Verzweigen**. Geben Sie die URL für das Quellenrepository ein.    
  c. Um eine Kopie eines Git-Repositorys zu erstellen, klicken Sie auf **Klonen**. Geben Sie einen neuen Repository-Namen und die URL für das Quellenrepository ein.     
  d. Falls Sie über ein Git-Repository verfügen und dieses verwenden möchten, klicken Sie beim Repository-Typ auf **Vorhanden**. Geben Sie die URL ein.    

1. Wenn Sie Issues für die Verfolgung von Problemen verwenden möchten, wählen Sie das Kontrollkästchen **Issues aktivieren** aus.
1. Wenn Sie die Bereitstellung von Codeänderungen bei Commits durch Erstellen von Tags und Kommentaren und bei Problemen, die über die Commits referenziert werden, mit Bezeichnungen und Kommentaren verfolgen wollen, wählen Sie das Kontrollkästchen **Bereitstellung von Codeänderungen verfolgen** aus. Weitere Informationen enthält der Bluemix-Blog im Abschnitt [Mit Toolchains verfolgen, wo Ihr Code bereitgestellt wird ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window}.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Karte für das Git-Repository, mit dem Sie arbeiten möchten. Die Übersichtsseite für Ihr Projekt wird geöffnet.    

**Hinweis:** Falls Sie nicht über Master- oder Eignerberechtigungen für das Repository verfügen, zu dem Sie einen
Link herstellen, ist Ihre Integration eingeschränkt, da Sie keine Web-Hooks verwenden können. Web-Hooks sind erforderlich, um eine Pipeline
automatisch auszuführen, wenn ein Commit per Push-Operation an das Repository übertragen wird. Ohne Web-Hook müssen Sie Ihre Pipelines manuell
starten. 


## GitHub und GitHub Issues konfigurieren
{: #github}

GitHub ist ein webbasierter Hosting-Service für Git-Repositorys. Sie können sowohl über lokale als auch über ferne Kopien Ihrer Repositorys verfügen, was die Zusammenarbeit sehr einfach gestaltet.

GitHub Issues ist ein Überwachungstool, das Ihre Arbeit und Ihre Pläne an einem einzigen zentralen Ort aufbewahrt. Es ist in Ihr Entwicklungsrepository integriert, damit Sie sich auf die wichtigen Aufgaben konzentrieren können.

Konfigurieren Sie GitHub zum Verwalten Ihres Quellcodes in der Cloud:

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, führen Sie diese Schritte aus:

 a. Klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **GitHub**. Wenn Sie die Toolchain unter {{site.data.keyword.Bluemix_notm}} Public erstellen und {{site.data.keyword.Bluemix_notm}} nicht für den Zugriff auf GitHub autorisiert haben, klicken Sie auf **Autorisieren**, um zur GitHub-Website zu wechseln. Wenn keine aktive GitHub-Sitzung existiert, werden Sie aufgefordert, sich anzumelden. Klicken Sie auf **Anwendung autorisieren**, um {{site.data.keyword.Bluemix_notm}} den Zugriff auf Ihr GitHub-Konto zu erlauben. Falls eine aktive GitHub-Sitzung existiert, Sie Ihr Kennwort aber bereits vor einiger Zeit eingegeben haben, werden Sie möglicherweise aufgefordert, Ihr GitHub-Kennwort durch erneute Eingabe zu bestätigen.

 b. Überprüfen Sie die Standardspeicherorte für die GitHub-Zielrepositorys. Diese Repositorys werden aus den Beispielrepositorys geklont. Ändern Sie gegebenenfalls die Namen der Zielrepositorys.
 ![Standardspeicherorte für Zielrepositorys](images/toolchain_github_config.png)

1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** und dann auf **Übersicht** klicken.

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf **GitHub**.

1. Falls Sie über ein GitHub-Repository verfügen und dieses verwenden möchten, klicken Sie beim Repository-Typ auf **Vorhanden** und geben Sie die URL ein.
1. Falls Sie ein neues GitHub-Repository verwenden möchten, geben Sie einen Namen für das GitHub-Repository ein, das Sie klonen oder verzweigen, und wählen Sie den Repository-Typ aus:

 a. Klicken Sie auf **Neu**, um ein leeres Repository zu erstellen.

 b. Klicken Sie auf **Klonen**, um eine Kopie eines GitHub-Repositorys zu erstellen.

 c. Klicken Sie auf **Verzweigen**, um ein GitHub-Repository zu verzweigen, sodass Sie Änderungen per Pull-Anforderungen beitragen können.

1. Wenn Sie GitHub Issues für die Verfolgung von Problemen verwenden möchten, wählen Sie das Kontrollkästchen **GitHub Issues aktivieren** aus.
1. Wenn Sie die Bereitstellung von Codeänderungen bei Commits durch Erstellen von Tags und Kommentaren und bei Problemen, die über die Commits referenziert werden, mit Bezeichnungen und Kommentaren verfolgen wollen, wählen Sie das Kontrollkästchen **Bereitstellung von Codeänderungen verfolgen** aus. Weitere Informationen enthält der Bluemix-Blog im Abschnitt [Mit Toolchains verfolgen, wo Ihr Code bereitgestellt wird ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window}.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Karte für das GitHub-Repository, mit dem Sie arbeiten möchten. Daraufhin wird die GitHub-Website geöffnet, auf der Sie den Inhalt des Repositorys anzeigen können.

  **Tipp:** Sie können die integrierten Quellcodeverwaltungstools in der Eclipse Orion-Web-IDE verwenden, um das
GitHub-Repository zu bearbeiten und eine App aus Ihrem Arbeitsbereich bereitzustellen. 

1. Falls Sie GitHub Issues aktiviert haben, klicken Sie auf **GitHub Issues**, um GitHub Issues zu öffnen. Sie können diese Instanz von GitHub Issues für Ihre gesamte Toolchain verwenden, selbst wenn die Toolchain mehr als nur ein GitHub-Repository enthält.    

**Hinweis:** Falls Sie nicht über Master- oder Eignerberechtigungen für das Repository verfügen, zu dem Sie einen Link
herstellen, ist Ihre Integration eingeschränkt, da Sie keine Web-Hooks verwenden können. Web-Hooks sind erforderlich, um eine Pipeline
automatisch auszuführen, wenn ein Commit per Push-Operation an das Repository übertragen wird. Ohne Web-Hook müssen Sie Ihre Pipelines manuell
starten.

Weitere Informationen enthält [GitHub ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} und [GitHub Issues ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.


## GitHub Enterprise und GitHub Issues unter Bluemix Dedicated konfigurieren
{: #configghe}

 **Hinweis:** Diese Anweisungen gelten für {{site.data.keyword.Bluemix_notm}} Dedicated for {{site.data.keyword.ghe_short}}. Wenn Sie Ihre eigene verwaltete Version von {{site.data.keyword.ghe_short}} verwenden, kann es sein, dass sich die Vorgehensweise abhängig von Ihren internen Prozeduren in einigen Schritten unterscheidet.

{{site.data.keyword.ghe_long}} ist ein lokaler webbasierter Hosting-Service für Git-Repositorys. Dedicated {{site.data.keyword.ghe_short}} ist nur für {{site.data.keyword.Bluemix_notm}} Dedicated-Kunden verfügbar. GitHub Issues ist ein Überwachungstool, das Ihre Arbeit und Ihre Pläne an einem zentralen Ort aufbewahrt. Es ist in Ihr Entwicklungsrepository integriert, damit Sie sich auf die wichtigen Aufgaben konzentrieren können. Weitere Informationen zu Dedicated {{site.data.keyword.ghe_short}} und GitHub Issues finden Sie in der [Einführung in {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window} und im Artikel [GitHub Issues ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.

Sie können {{site.data.keyword.ghe_short}} als Toolintegration in Ihrer Toolchain konfigurieren, sodass Sie Quellcode in der Instanz von [{{site.data.keyword.Bluemix_notm}} Dedicated](/docs/dedicated/index.html#dedicated){: new_window} Ihres Unternehmens verwalten können.

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, führen Sie diese Schritte aus:

 a. Bevor Sie sich zum ersten Mal bei Dedicated {{site.data.keyword.ghe_short}} anmelden, bitten Sie den Regionsadministrator Ihres Unternehmens, Ihre Benutzer-ID aus dem Benutzerregistry Ihres Unternehmens unter Verwendung von LDAP zu der {{site.data.keyword.Bluemix_notm}} Dedicated-Instanz hinzuzufügen. Informationen zum Einrichten Ihres {{site.data.keyword.ghe_short}}-Kontos finden Sie unter [Einführung in {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window}.

 b. Klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **{{site.data.keyword.ghe_short}}**.    

 c. Prüfen Sie den Standardnamen für das neue {{site.data.keyword.ghe_short}}-Repository. Ändern Sie gegebenenfalls den Namen des neuen Repositorys. Die folgende Abbildung zeigt ein Beispiel für ein Repository, das aus einem Beispielrepository geklont ist. Sie können ein vorhandenes oder ein neues Repository verwenden. Um ein neues Repository zu verwenden, können Sie ein leeres Repository erstellen oder Sie können ein Repository klonen oder verzweigen.
 ![Standardspeicherorte für Repositorys](images/toolchain_ghe_config.png)

1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite Ihrer der App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** und dann auf **Übersicht** klicken.

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf **{{site.data.keyword.ghe_short}}**.

1. Falls Sie über ein {{site.data.keyword.ghe_short}}-Repository verfügen, das Sie verwenden wollen, geben Sie die URL für das Repository ein. Klicken Sie für den Repository-Typ auf **Vorhanden**.
1. Falls Sie ein neues {{site.data.keyword.ghe_short}}-Repository verwenden möchten, geben Sie einen Namen für das Repository ein, geben Sie die URL für das Repository ein, das Sie klonen oder verzweigen, und wählen Sie den Repository-Typ aus:

 a. Klicken Sie auf **Neu**, um ein leeres Repository zu erstellen.

 b. Klicken Sie auf **Klonen**, um eine Kopie eines Repositorys zu erstellen.

 c. Klicken Sie auf **Verzweigen**, um ein Repository zu verzweigen, sodass Sie Änderungen per Pull-Anforderungen beitragen können.

1. Wenn Sie GitHub Issues zum Überwachen von Problemen verwenden möchten, wählen Sie das Kontrollkästchen **GitHub Issues aktivieren** aus.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Karte für das {{site.data.keyword.ghe_short}}-Repository, mit dem Sie arbeiten möchten. Das {{site.data.keyword.ghe_short}}-Repository Ihres Unternehmens wird geöffnet.

  **Tipp:** Sie können die integrierten Quellcodeverwaltungstools in der Eclipse Orion-Web-IDE verwenden, um das
{{site.data.keyword.ghe_short}}-Repository zu bearbeiten und eine App aus Ihrem Arbeitsbereich bereitzustellen. 

1. Falls Sie GitHub Issues aktiviert haben, klicken Sie auf **GitHub Issues**. Sie können diese Instanz von GitHub Issues für Ihre gesamte Toolchain verwenden, selbst wenn die Toolchain mehr als nur ein GitHub-Repository enthält.    

**Hinweis:** Falls Sie nicht über Administratorberechtigungen für das Repository verfügen, zu dem Sie einen Link
herstellen, ist Ihre Integration eingeschränkt, da Sie keine Web-Hooks verwenden können. Web-Hooks sind erforderlich, um eine Pipeline
automatisch auszuführen, wenn ein Commit per Push-Operation an das Repository übertragen wird. Ohne Web-Hook müssen Sie Ihre Pipelines manuell
starten. 


## Jenkins konfigurieren
{: #jenkins}

Jenkins ist ein serverbasiertes Open-Source-Tool, das Software fortlaufend erstellt und testet und dabei die Verfahren von kontinuierlicher Integration und Continuous Delivery unterstützt.

**Wichtig:** Sie müssen über einen Jenkins-Server verfügen, bevor Sie eine Jenkins-Toolintegration erstellen können. 

Mit der Jenkins-Toolintegration können Sie Ihre Jenkins-Jobbenachrichtigungen an andere Tools in Ihrer Toolchain senden, wie zum Beispiel an Slack und PagerDuty. Wenn Sie Code in Bereitstellungen verfolgen möchten, können Sie Bereitstellungsnachrichten zu Ihren Git-Commits und den zugehörigen Git- oder JIRA-Problemen hinzufügen. Außerdem können Sie Ihre Bereitstellungen auf der Seite für Toolchain-Verbindungen anzeigen. Sie können {{site.data.keyword.DRA_short}} Testergebnisse zuführen, automatisierte Qualitätsberichte hinzufügen und Ihr Bereitstellungsrisiko verfolgen.

Konfigurieren Sie Jenkins, um das kontinuierliche Erstellen, Testen und Bereitstellen Ihrer Apps zu automatisieren. Gehen Sie dazu wie folgt vor:

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **Jenkins**.
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite Ihrer App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** klicken. Klicken Sie anschließend auf **Übersicht**.  

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf **Jenkins**.

1. Geben Sie den Namen ein, der für diese Toolintegration in Ihrer Toolchain auf der Karte für Jenkins angezeigt werden soll.
1. Geben Sie die URL für den Jenkins-Server ein, der geöffnet werden soll, wenn Sie in Ihrer Toolchain auf die Karte für Jenkins klicken.
1. Kopieren Sie den generierten Web-Hook der Toolchain. 
1. Führen Sie in Ihrem Jenkins-Server die folgenden Schritte aus:

 a. Installieren Sie die [Cloud Foundry-CLI ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window}.

 b. Installieren Sie das Cloud Foundry-Plug-in von IBM Cloud DevOps, indem Sie einen der folgenden Befehle eingeben: 

  * Mac OS: `cf install-plugin https://icd.ng.bluemix.net/icd_darwin_amd64`

  * Linux oder Docker: `cf install-plugin https://icd.ng.bluemix.net/icd_linux_amd64`

 c. Installieren und konfigurieren Sie das Jenkins-Plug-in von IBM Cloud DevOps für DevOps Insights und Notifications. Weitere Informationen enthält [Plug-in installieren und konfigurieren](/docs/services/DevOpsInsights/insights_risk.html#integrate_jenkins){: new_window}. 

 d. Führen Sie in jedem Job, für den Sie Benachrichtigungen an Ihre Toolchain senden wollen, die folgenden Schritte aus:

  * Wählen Sie das Kontrollkästchen **Dieses Projekt besitzt Parameterangaben** aus.

  * Fügen Sie den Zeichenfolgeparameter `ICD_WEBHOOK_URL` hinzu.

  * Fügen Sie den generierten Web-Hook der Toolchain ein.
 ![URL des Web-Hooks](images/jenkins_webhook_url.png)

  * Fügen Sie für 'IBM Cloud DevOps - Web-Hook-Benachrichtigung' eine Aktion nach Buildabschluss hinzu und wählen Sie das Kontrollkästchen **Job abgeschlossen** aus.
 ![Aktion nach Buildabschluss](images/jenkins_postbuild_action.png)  

 e. Führen Sie in Ihren Bereitstellungsjobs die folgenden Schritte aus:

  * Fügen Sie die Zeichenfolgeparameter `ICD_WEBHOOK_URL`, `CF_API`, `CF_ORG`, `CF_SPACE` und `CF_APP` hinzu. Die Beispiele veranschaulichen, wie Sie die einzelnen Zeichenfolgeparameter hinzufügen.
 ![Web-Hook-URL-Zeichenfolgeparameter](images/jenkins_set_webhook_url.png)
 ![CFI-API-Zeichenfolgeparameter](images/jenkins_set_cfapi.png)
 ![CFI-ORG-Zeichenfolgeparameter](images/jenkins_set_cforg.png)
 ![CFI-SPACE-Zeichenfolgeparameter](images/jenkins_set_cfspace.png)
 ![CFI-APP-Zeichenfolgeparameter](images/jenkins_set_cfapp.png)

  * Konfigurieren Sie die Bindungen für die Cloud Foundry-CLI mit der Variablen `CF_CREDS_USR` für den Benutzernamen und der Kennwortvariablen `CF_CREDS_PSW`.
 ![Cloud Foundry-CLI-Bindungen](images/jenkins_config_bindings.png)  

  * Geben Sie im Feld **Build** diese Befehle ein, um sich anzumelden, und senden Sie mithilfe des Cloud Foundry-Plug-ins
für IBM Cloud DevOps die durch die Anwendung bereitstellbaren Zuordnungen mit Git-Commit-Verfolgbarkeit an Ihre Toolchain:
 ![Build-Befehle](images/jenkins_build_commands.png)     

  * Geben Sie im Feld **Build** den Befehl `cf icd --create-connection $ICD_WEBHOOK_URL $CF_APP` ein, um die durch die Anwendung bereitstellbaren Zuordnungen an die Toolchain zu senden.    

 f. Speichern Sie Ihre Änderungen und kehren Sie für die Jenkins-Toolintegration zu der Seite zum Konfigurieren der Integration zurück.

1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie von Ihrer Toolchain aus auf **Jenkins**, um den Jenkins-Server anzuzeigen.  

Weitere Informationen enthält [Jenkins ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/deliver/tool_jenkins/){: new_window}.


## JIRA konfigurieren
{: #jira}

JIRA ist ein Tool, das Probleme und Bugs verfolgt, die mit Ihrer Software zusammenhängen. Die JIRA-Toolintegration führt eine Aktualisierung der projektbezogenen Probleme durch, wann immer Jenkins oder {{site.data.keyword.deliverypipeline}} eine Bereitstellung ausführen. Damit die JIRA-Toolintegration Ihre Probleme verfolgen kann, müssen Sie in Ihren Commit-Nachrichten Smart Commits von JIRA verwenden. Weitere Informationen zu Smart Commits von JIRA finden Sie in [Verwenden von Smart Commits ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://confluence.atlassian.com/fisheye/using-smart-commits-298976812.html){: new_window}.

Konfigurieren Sie JIRA für die Planung, Verfolgung und Übermittlung von Qualitätscode. Gehen Sie dazu wie folgt vor:

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **JIRA**.
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite Ihrer App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** klicken. Klicken Sie anschließend auf **Übersicht**.  

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf **JIRA**.

1. Wenn Sie bereits über ein JIRA-Projekt verfügen und eine Verbindung zu ihm herstellen möchten, klicken Sie beim JIRA-Typ auf **Vorhanden**:

 a. Geben Sie den JIRA-Projektschlüssel für das JIRA-Projekt ein. Den Projektschlüssel können Sie der URL des JIRA-Projekts entnehmen.

 b. Geben Sie die API-Basis-URL für Ihre JIRA-Instanz ein. Die API-URL können Sie dem Header Ihrer JIRA-Instanz entnehmen. Klicken Sie auf das Symbol für **Administration** und klicken Sie dann auf **System**.

 c. Optional: Geben Sie Ihren JIRA-Benutzernamen ein. Ihr Benutzername ist nur erforderlich, wenn Sie eine Verbindung zu einer privaten JIRA-Instanz herstellen oder wenn Sie eine Verbindung zu einer öffentlichen Instanz herstellen und Verfolgbarkeitsinformationen erhalten möchten.

 d. Optional: Geben Sie Ihr JIRA-Kennwort ein. Ihr Kennwort ist nur erforderlich, wenn Sie eine Verbindung zu einer privaten JIRA-Instanz herstellen oder wenn Sie eine Verbindung zu einer öffentlichen Instanz herstellen und Verfolgbarkeitsinformationen erhalten möchten.

 e. Wenn Sie die Bereitstellung von Codeänderungen für das Projekt durch Erstellen von Bezeichnungen und Kommentaren für referenzierte Problemen verfolgen wollen, wählen Sie das Kontrollkästchen **Bereitstellung von Codeänderungen verfolgen** aus. Stellen Sie sicher, dass Sie JIRA Smart Commit beim Referenzieren der JIRA-Probleme in Ihren GitHub-Commits verwenden. Wenn Sie diese Option nicht auswählen, ignoriert die JIRA-Toolintegration alle Commits.

1. Wenn Sie ein JIRA-Projekt erstellen möchten, klicken Sie beim JIRA-Typ auf **Neu** und gehen Sie wie folgt vor:

 a. Geben Sie einen JIRA-Projektschlüssel ein, der für das neue Projekt verwendet werden soll. Dieser Schlüssel fungiert als eindeutige ID in der Projekt-URL.

 b. Geben Sie einen Namen für das JIRA-Projekt ein.

 c. Geben Sie die API-Basis-URL für Ihre JIRA-Instanz ein. Die API-URL können Sie dem Header Ihrer JIRA-Instanz entnehmen. Klicken Sie auf das Symbol für **Administration** und klicken Sie dann auf **System**.

 d. Geben Sie den Benutzernamen für den JIRA-Projektleiter ein, den Sie für dieses Projekt einsetzen möchten. Um eine Person als JIRA-Projektleiter angeben zu können, muss diese in JIRA über die Projektleitungsgenehmigung verfügen.

 e. Geben Sie den Administratorbenutzernamen für diese JIRA-Instanz ein.

 f. Geben Sie das Administratorkennwort für diese JIRA-Instanz ein.

 g. Wenn Sie die Bereitstellung von Codeänderungen für das Projekt durch Erstellen von Bezeichnungen und Kommentaren für referenzierte Problemen verfolgen wollen, wählen Sie das Kontrollkästchen **Bereitstellung von Codeänderungen verfolgen** aus. Stellen Sie sicher, dass Sie JIRA Smart Commit beim Referenzieren der JIRA-Probleme in Ihren GitHub-Commits verwenden. Wenn Sie diese Option nicht auswählen, ignoriert die JIRA-Toolintegration alle Commits.

1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie von Ihrer Toolchain aus auf **JIRA**, um das Dashboard für das JIRA-Projekt anzuzeigen, mit dem Sie verbunden sind.

Weitere Informationen enthält [JIRA ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/code/tool_jira/){: new_window}.


## Nexus konfigurieren
{: #nexus}

Konfigurieren Sie den Repository-Manager von Nexus zum Speichern von Buildartefakten in Ihrem Nexus-Repository (Repo). Gehen Sie dazu wie folgt vor:

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **Nexus**.
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite Ihrer App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** klicken. Klicken Sie anschließend auf **Übersicht**.  

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf **Nexus**.

1. Geben Sie einen Namen für diese Instanz der Nexus-Toolintegration ein.
1. Geben Sie die URL für das Nexus-Repository ein, das geöffnet werden soll, wenn Sie in Ihrer Toolchain auf die Karte für Nexus klicken.
1. Wählen Sie den Repository-Typ aus, zu dem eine Verbindung hergestellt werden soll.
1. Wenn Sie **npm-Registry** ausgewählt haben, führen Sie die folgenden Schritte aus:

 a. Geben Sie die E-Mail-Adresse ein, die Ihrer Registry zugeordnet ist.

 b. Geben Sie das Authentifizierungstoken ein, das Ihrer Registry zugeordnet ist.

 c. Geben Sie die URL für Ihr Nexus-Release-Repository ein. Dieses Repository ist Ihre private Registry auf dem Nexus-Server.

 d. Geben Sie die URL für die Spiegelregistry oder die öffentliche Registry ein, die Sie verwenden, um mehrere öffentliche und private npm-Registrys miteinander zu kombinieren. Bei dieser URL kann es sich beispielsweise um die URL der virtuellen Registry auf Ihrem Nexus-Server handeln, die sowohl auf Ihre private Registry als auch auf einen Cachespeicher der globalen npm-Registry Zugriff hat.

1. Wenn Sie **Maven-Repository** ausgewählt haben, führen Sie die folgenden Schritte aus:

 a. Geben Sie die Benutzer-ID ein, die Ihrem Repository zugeordnet ist.

 b. Geben Sie das Kennwort ein, das Ihrem Repository zugeordnet ist.

 c. Geben Sie die URL für Ihr Nexus-Release-Repository ein. Dieses Repository ist Ihr privates Release-Repository auf dem Nexus-Server.

 d. Geben Sie die URL für Ihr Nexus-Snapshot-Repository ein. Dieses Repository ist Ihr privates Snapshot-Repository auf dem Nexus-Server.

 e. Geben Sie die URL für das Spiegelrepository oder das öffentliche Repository ein, das Sie verwenden, um mehrere öffentliche und private Maven-Repositorys miteinander zu kombinieren. Bei dieser URL kann es sich beispielsweise um die URL des virtuellen Repositorys auf Ihrem Nexus-Server handeln, das sowohl auf Ihre privaten Repositorys als auch auf einen Cachespeicher des zentralen Maven-Repositorys Zugriff hat.

1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie von Ihrer Toolchain aus auf die Karte für das Nexus-Repository, mit dem Sie arbeiten möchten. Daraufhin wird die Nexus-Website geöffnet, auf der Sie den Inhalt des Repositorys anzeigen können.
1. Optional: Wenn Sie eine Toolchain unter {{site.data.keyword.Bluemix_notm}} Public verwenden und Sie Ihre App unter Verwendung von Nexus mit npm erstellen wollen, konfigurieren Sie Ihre Pipeline durch Hinzufügen eines npm-Buildjobs. Anweisungen zum Konfigurieren des Buildjobs enthält der Abschnitt [Nexus-npm-Buildjob in Ihrer Pipeline konfigurieren](#config_nexus_npm).
1. Optional: Wenn Sie eine Toolchain unter {{site.data.keyword.Bluemix_notm}} Public verwenden und Sie Ihre App unter Verwendung von Nexus mit Maven erstellen wollen, konfigurieren Sie Ihre Pipeline durch Hinzufügen eines Maven-Buildjobs. Anweisungen zum Konfigurieren des Buildjobs enthält der Abschnitt [Nexus-Maven-Buildjob in Ihrer Pipeline konfigurieren](#config_nexus_maven).

### Nexus-npm-Buildjob in Ihrer Pipeline konfigurieren
{: #config_nexus_npm}

Bevor Sie einen npm-Buildjob in Ihrer Pipeline konfigurieren, müssen Sie über eine funktionstüchtige Pipeline verfügen, die Ihr SCM-Build-Repository als Eingabe verwenden kann. Außerdem müssen Sie Nexus für Ihre Toolchain konfigurieren. Anweisungen zum Konfigurieren von Nexus enthält der Abschnitt [Nexus](#nexus).

Konfigurieren Sie {{site.data.keyword.deliverypipeline}} durch Hinzufügen eines npm-Build-Jobs. Gehen Sie dazu wie folgt vor:

1. Erstellen Sie eine Stage und geben Sie das entsprechende SCM-Repository für die Eingabe an.
1. Fügen Sie in der Stage einen Buildjob hinzu.
1. Konfigurieren Sie den Buildjob wie folgt:
  ![npm-Build-Job](images/nexus_npm_job.png)

  a. Wählen Sie als Buildertyp den Typ **NPM-Build** aus.

  b. Falls Sie mehrere Instanzen der Nexus-Toolintegration konfiguriert haben, geben Sie den Namen der Nexus-Toolintegration ein, für die Sie den npm-Buildjob konfigurieren wollen.

  c. Wählen Sie als Toolintegrationtyp den Typ **Nexus** aus.

  d. Geben Sie beim Buildbefehl die Befehle zum Erstellen Ihres npm-Moduls ein oder die Befehle zum Veröffentlichen des Moduls in Ihrer Registry. Das nachfolgende Beispiel zeigt die Befehle zum Erstellen (Builden) des Moduls bzw. zum Veröffentlichen.
     ```
     npm install
     # oder
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **Tipp:** Sie finden die URL und die Benutzerberechtigungsnachweise, die Sie für die Verbindungsherstellung mit Ihrer
Registry verwendet haben, in den Konfigurationseinstellungen für die Nexus-Toolintegration.
  e. Wenn Ihr Buildjob in der Nexus-Registry veröffentlicht wird und die Version Ihres Knotenmoduls das Format `x.y.z-SNAPSHOT.w` aufweist, wählen Sie das Kontrollkästchen **Versionsangabe für Snapshot-Modul inkrementieren** aus. Der Buildjob aktualisiert die Modulversion automatisch, bevor er die Veröffentlichung in der Nexus-Registry ausführt. Der Buildjob wählt die höchste Version des Moduls aus der npm-Registry und der lokalen `package.json`-Datei aus und erhöht den Wert für die Modulversion unter Verwendung von SemVer (Semantic Versioning). Der Buildjob übermittelt die Änderungen nicht an das SCM-Repository.

1. Klicken Sie auf **SPEICHERN**. Wann immer Ihre Pipeline ausgeführt wird, verwendet dieser Buildjob die Konfigurationsinformationen aus der Nexus-Toolintegration, um eine Verbindung zu Ihrer npm-Registry herzustellen.

### Nexus-Maven-Buildjob in Ihrer Pipeline konfigurieren
{: #config_nexus_maven}

Bevor Sie einen Maven-Buildjob in Ihrer Pipeline konfigurieren, müssen Sie über eine funktionstüchtige Pipeline verfügen, die Ihr SCM-Build-Repository als Eingabe verwenden kann. Außerdem müssen Sie Nexus für Ihre Toolchain konfigurieren. Anweisungen zum Konfigurieren von Nexus enthält der Abschnitt [Nexus](#nexus).

Konfigurieren Sie {{site.data.keyword.deliverypipeline}} durch Hinzufügen eines Maven-Buildjobs. Gehen Sie dazu wie folgt vor:

1. Erstellen Sie eine Stage und geben Sie das entsprechende SCM-Repository für die Eingabe an.
1. Fügen Sie in der Stage einen Buildjob hinzu.
1. Konfigurieren Sie den Buildjob wie folgt:
  ![Maven-Build-Job](images/nexus_maven_job.png)

  a. Wählen Sie als Buildertyp den Typ **Maven-Build** aus.

  b. Falls Sie mehrere Instanzen der Nexus-Toolintegration konfiguriert haben, geben Sie den Namen der Nexus-Toolintegration ein, für die Sie den Maven-Buildjob konfigurieren wollen.

  c. Wählen Sie als Toolintegrationtyp den Typ **Nexus** aus.

  d. Geben Sie beim Buildbefehl die Befehle zum Erstellen Ihres Maven-Moduls ein oder die Befehle zum Veröffentlichen des Moduls in Ihrer Registry. Das nachfolgende Beispiel zeigt die Befehle zum Erstellen (Builden) des Moduls bzw. zum Veröffentlichen.
     ```
     mvn -B clean package
     # oder
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **Tipp:** Sie finden die URL und die Benutzerberechtigungsnachweise, die Sie für die Verbindungsherstellung mit Ihrer
Registry verwendet haben, in den Konfigurationseinstellungen für die Nexus-Toolintegration.
1. Klicken Sie auf **SPEICHERN**. Wann immer Ihre Pipeline ausgeführt wird, verwendet dieser Buildjob die Konfigurationsinformationen aus der Nexus-Toolintegration, um eine Verbindung zu Ihrem Maven-Repository herzustellen.

Weitere Informationen enthält [Nexus ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/deliver/tool_nexus/){: new_window}.


## Angepasstes Tool konfigurieren (Option 'Other Tool')
{: #othertool}

Falls Ihr Team ein Tool verwendet, das nicht in der Liste der Toolchainintegrationen enthalten ist, können Sie ein angepasstes Tool integrieren.

So konfigurieren Sie ein angepasstes Tool, damit es mit anderen Tools in Ihrer Toolchain zusammenarbeitet und für Ihr Team verfügbar ist:

1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite Ihrer der App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** und dann auf **Übersicht** klicken.

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf **Anderes Tool**.

1. Geben Sie den Namen des Tools ein.
1. Wählen Sie eine Lebenszyklusphase aus, die dem Tool am genauesten entspricht. Die getroffene Auswahl bestimmt, unter welcher Kategorie Ihr Tool auf der Übersichtsseite angezeigt wird.
1. Fügen Sie eine URL für ein Symbol hinzu. Dieses Symbol wird auf der Karte für Ihre Toolintegration angezeigt. 
1. Fügen Sie eine URL für die Dokumentation hinzu.
1. Geben Sie einen Instanznamen für das Tool an. Beispiel: Tool für mein Team.
1. Fügen Sie eine URL für die Toolinstanz hinzu. Diese URL wird immer dann geöffnet, wenn auf die Karte der Toolintegration geklickt wird.
1. Fügen Sie eine Beschreibung des Tools hinzu.
1. (Erweitert) Fügen Sie weitere Eigenschaften nach Bedarf hinzu. Listen Sie beispielsweise alle Informationen oder Attribute auf, die gegebenenfalls für die Integration Ihres Tools bei anderen Tools in der Toolchain erforderlich sind.  
1. Klicken Sie auf **Integration erstellen**.

Weitere Informationen enthält der Bluemix-Blog im Abschnitt [Einführung in die angepasste Toolintegration für {{site.data.keyword.Bluemix_notm}}-Toolchains ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2016/10/custom-tool-integration-with-bluemix-toolchains/){: new_window}.


## PagerDuty konfigurieren
{: #pagerduty}

PagerDuty integriert Daten aus mehreren Überwachungssystemen in einer Gesamtansicht. Wenn ein Problem auftritt, stellt PagerDuty sicher, dass das Teammitglied, das zu diesem Zeitpunkt am besten geeignet ist, das Problem zu lösen, benachrichtigt wird. Falls das Teammitglied nicht auf das Problem reagiert, können Eskalationen konfiguriert werden, um es an sekundäre Entwickler oder Betriebsleiter weiterzuleiten.

Konfigurieren Sie PagerDuty, um Benachrichtigungen zu senden, wenn Pipeline-Stage-Fehler auftreten, damit Sie Probleme schneller beheben und Ausfallzeiten reduzieren können:

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **PagerDuty**.
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite Ihrer der App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** und dann auf **Übersicht** klicken.

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf **PagerDuty**.

1. Geben Sie den API-Zugriffsschlüssel für Ihr PagerDuty-Konto ein. Wenn Sie kein PagerDuty-Konto haben, [registrieren Sie sich für ein solches Konto (Link wird in neuem Fenster geöffnet) ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://signup.pagerduty.com/accounts/new){: new_window}. Anweisungen zum Auffinden des Schlüssels finden Sie in [Generieren eines API-Schlüssels ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://support.pagerduty.com/hc/en-us/articles/202829310-Generating-an-API-Key){: new_window}.
1. Geben Sie den Namen Ihres PagerDuty-Service ein.
1. Geben Sie die E-Mail-Adresse für den primären PagerDuty-Kontakt ein.
1. Geben Sie die Telefonnummer für den primären PagerDuty-Kontakt ein.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf **PagerDuty**, um zu pagerduty.com zu gelangen. Sie können die Ereignisse anzeigen, die dem PagerDuty-Service zugeordnet sind, den Sie während der Konfiguration dieser Toolintegration für Ihre Toolchain angegeben haben.

Weitere Informationen enthält [PagerDuty ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Sauce Labs konfigurieren
{: #saucelabs}

Sauce Labs führt funktionelle Komponententests aus. Wenn eine Sauce Labs-Testsuite als Testjob in der {{site.data.keyword.deliverypipeline}} konfiguriert wird, kann die Testsuite Tests für Ihre Web- oder Mobil-App als Teil Ihres kontinuierlichen Bereitstellungsprozesses ausführen. Anhand dieser Tests können Sie eine reibungslose Ablaufsteuerung für Ihre Projekte erzielen, da die Bereitstellung von fehlerhaftem Code verhindert wird.

 **Hinweis:** Diese Toolintegration ist nur in {{site.data.keyword.Bluemix_notm}} Public verfügbar. 

Konfigurieren Sie Sauce Labs, um automatische Funktionstests auf mehreren Betriebssystemen und in mehreren Browsern auszuführen, sodass Sie die Art und Weise emulieren können, auf die ein Benutzer möglicherweise eine Website oder eine Anwendung nutzt.

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **Sauce Labs**.
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** und dann auf **Übersicht** klicken.

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf **Sauce Labs**.

1. Geben Sie den Benutzernamen ein, der Ihrem Sauce Labs-Konto zugeordnet ist. Sie finden [Ihren Benutzernamen in der Begrüßungsnachricht oben auf Ihrer Sauce Labs-Kontoseite ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://saucelabs.com/account){: new_window}.
1. Geben Sie den Zugriffsschlüssel für Ihr Sauce Labs-Konto ein. Sie finden [den Schlüssel auf der Sauce Labs-Kontoseite ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://saucelabs.com/account){: new_window}.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf **Sauce Labs**, um saucelabs.com zu öffnen und die Testaktivität für die Toolchain anzuzeigen.

 **Tipp:**: Wenn Sie einen Sauce Labs-Testjob zu {{site.data.keyword.deliverypipeline}} hinzugefügt haben,
können Sie die Serviceinstanz auswählen. 

Weitere Informationen enthält [Sauce Labs ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/deliver/tool_sauce_labs/){: new_window}.


## Slack konfigurieren
{: #slack}

**Wichtig:** Benachrichtigungen, die in öffentlichen Slack-Kanälen gepostet werden, sind für jeden im Team sichtbar. Denken Sie daran, dass Sie für den Inhalt, den Sie posten, verantwortlich sind.

Slack ist ein cloudbasiertes echtzeitorientiertes Messaging- und Benachrichtigungssystem. Slack stellt persistenten Chat bereit, wobei es sich um eine interaktionsintensivere Alternative zu E-Mail für die Teamzusammenarbeit handelt. Sie können mit Ihrem Team über einen dedizierten Kanal oder über eine Reihe von Kanälen kommunizieren, die in direktem Zusammenhang mit Ihrer Arbeit stehen. Sie können außerdem Dateien und Bilder über die Kanäle oder in direkten Nachrichten zwischen zwei oder mehr Personen teilen. Die Kommunikation in direkten Nachrichten und über die Kanäle wird aufbewahrt und kann durchsucht werden.

Konfigurieren Sie Slack, um Benachrichtigungen zu Ihrer Toolchain von den Toolintegrationen zu erhalten, z. B. Test- und Bereitstellungsaktivitäten:

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **Slack**.
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Übersichtsseite zu öffnen. Alternativ können Sie auf der Übersichtsseite Ihrer der App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** und dann auf **Übersicht** klicken.

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt mit den Toolintegrationen auf **Slack**.

1. Geben Sie die Web-Hook-URL für Slack an, die von Slack als eingehender Web-Hook generiert wird. Sie benötigen eine Web-Hook-URL für Slack, damit ein Slack-Kanal von den Toolintegrationen Benachrichtigungen über Ihre Toolchain empfangen kann. Anweisungen zum Erstellen oder Auffinden Ihres Web-Hooks finden Sie in [Eingehende Web-Hooks ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://api.slack.com/incoming-webhooks){: new_window}.

 **Tipp:** Wenn Sie einen API-Schlüssel für Ihren Slack-Kanal verwendet haben, um von den Toolintegrationen
Benachrichtigungen über Ihre Toolchain zu erhalten, müssen Sie Ihre Konfiguration so aktualisieren, dass sie stattdessen einen Web-Hook verwendet. 

1. Geben Sie den Namen des Slack-Kanals ein, an den die Benachrichtigungen gesendet werden sollen. Der Kanal muss in Ihrem Slack-Team
vorhanden und aktiv sein. 
1. Geben Sie den URL-Hostnamen für Ihr Slack-Team ein, d. h. das Wort oder die Wortfolge vor `.slack.com` in Ihrer Team-URL. Wenn Ihre Team-URL zum Beispiel `https://team.slack.com` ist, dann lautet der Hostname `team`.
1. Klicken Sie auf **Integration erstellen**.

 **Tipp:** Wenn der von Ihnen angegebene Slack-Kanal und das entsprechende Team nicht erreicht werden können, wird
auf der Karte für Slack der Fehler `Einrichtung fehlgeschlagen` angezeigt. Bewegen Sie den Mauszeiger über die Nachricht `Einrichtung fehlgeschlagen` und klicken Sie auf **Neu konfigurieren**. Stellen Sie sicher, dass Sie gültige Konfigurationsparameter für die Slack-Web-Hook-URL, den Slack-Kanal und den URL-Hostnamen für Ihr Slack-Team verwenden. Aktualisieren Sie die Einstellungen nach Bedarf und klicken Sie auf **Integration speichern**.

1. Klicken Sie auf **Slack**. Sie können alle Aktivitäten für Ihre Toolchain im konfigurierten Slack-Kanal anzeigen.

Weitere Informationen enthält [Slack ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.


## SonarQube konfigurieren 
{: #sonarqube}

SonarQube bietet eine Übersicht über den Gesamtzustand und die Qualität Ihres Quellcodes und markiert Probleme, die in neuem Code
gefunden werden. Die Analysefunktionen für Code erkennen schwierige Fehler wie Dereferenzen mit Nullzeigern, logische Fehler oder
Ressourcenlecks für über 20 Codiersprachen. 

Gehen Sie wie folgt vor, um SonarQube so zu konfigurieren, dass die Qualität Ihres Quellcodes fortlaufend analysiert und gemessen wird: 

1. Klicken Sie im DevOps-Dashboard auf **Toolchains**. Klicken Sie auf die Toolchain, der Sie SonarQube hinzufügen
wollen. Alternativ können Sie auf der Übersichtsseite Ihrer App auf der Karte für Continuous Delivery auf **Toolchain anzeigen** klicken. Klicken Sie anschließend auf **Übersicht**.  

 a. Klicken Sie auf **Tool hinzufügen**.

 b. Klicken Sie im Abschnitt 'Toolintegrationen' auf **SonarQube**. 

1. Geben Sie einen Namen für diese Instanz der SonarQube-Toolintegration ein. 
1. Geben Sie die URL für die SonarQube-Instanz ein, die geöffnet werden soll, wenn Sie in Ihrer Toolchain auf die Karte für SonarQube
klicken. 
1. Optional: Geben Sie den Benutzernamen ein, den Sie zum Herstellen einer Verbindung zum SonarQube-Server verwenden. 

 **Tipp:** Sie müssen einen Benutzernamen nur angeben, wenn Sie zum Herstellen einer Verbindung zum SonarQube-Server
ein Kennwort verwenden. Wenn Sie zum Herstellen einer Verbindung ein Authentifizierungstoken verwenden, lassen Sie dieses Feld leer. 

1. Geben Sie das Kennwort oder das Authentifizierungstoken ein, das Sie zum Herstellen einer Verbindung zum SonarQube-Server verwenden. 
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie in Ihrer Toolchain auf **SonarQube**, um das Dashboard für die SonarQube-Instanz anzuzeigen, zu der
Sie eine Verbindung hergestellt haben. 

Weitere Informationen finden Sie in [SonarQube
![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/devops/method/content/learn/tool_sonarqube/){: new_window}. 
