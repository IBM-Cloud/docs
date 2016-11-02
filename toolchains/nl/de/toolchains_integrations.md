---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Toolintegrationen konfigurieren
{: #integrations}

Letzte Aktualisierung: 13. September 2016
{: .last-updated}

Sie haben die Möglichkeit, Toolintegrationen zu konfigurieren, die Entwicklungs-, Bereitstellungs- und Operationstasks unterstützen, wenn Sie eine Toolchain erstellen. Sie können auch Toolintegrationen hinzufügen und konfigurieren, um eine vorhandene Toolchain anzupassen.  
{:shortdesc}

**Wichtig**: Diese Funktion ist experimentell. Toolchains sind möglicherweise nicht stabil und können so geändert werden, dass sie nicht mehr mit früheren Versionen kompatibel sind. Sie sollten nicht in Produktionsumgebungen verwendet werden. Unter {{site.data.keyword.Bluemix_notm}} Public sind Toolchains nur in der Region 'Vereinigte Staaten (Süden)' verfügbar.

Die Toolintegrationen, die zum Hinzufügen und Konfigurieren Ihrer Toolchain verfügbar sind, hängen davon ab, ob Sie die Toolchains unter {{site.data.keyword.Bluemix_notm}} Public oder {{site.data.keyword.Bluemix_notm}} Dedicated verwenden.

*Tabelle 1: Toolintegrationen, die für Toolchains unter {{site.data.keyword.Bluemix_notm}} Public und Dedicated verfügbar sind*

|Toolintegration |Verfügbar unter {{site.data.keyword.Bluemix_notm}} Public	|Verfügbar unter {{site.data.keyword.Bluemix_notm}} Dedicated|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.deliverypipeline}} 		|Ja	   	|Ja  		|
|{{site.data.keyword.DRA_short}} 		|Ja		|Nein			|
|Eclipse Orion {{site.data.keyword.webide}}		|Ja		|Ja			|
|GitHub		|Ja		|Nein		|
|Dedicated GitHub Enterprise			|Nein		|Ja		|
|PagerDuty			|Ja		|Nein		|
|Sauce Labs		|Ja		|Nein		|
|Slack			|Ja		|Nein		|

**Tipp**: Wenn Sie Quellcode unter {{site.data.keyword.Bluemix_notm}} Public entwickeln möchten, konfigurieren Sie die GitHub-Toolintegration, bevor Sie die {{site.data.keyword.deliverypipeline}} konfigurieren. Wenn Sie Quellcode unter {{site.data.keyword.Bluemix_notm}} Dedicated entwickeln möchten, konfigurieren Sie die {{site.data.keyword.ghe_short}}-Toolintegration, bevor Sie die {{site.data.keyword.deliverypipeline}} konfigurieren. 


## Delivery Pipeline konfigurieren
{: #deliverypipeline}

Die {{site.data.keyword.deliverypipeline}} automatisiert die unterbrechungsfreie Bereitstellung Ihrer Projekte über eine Stagefolge, die Eingabe- und Ausführungsjobs empfängt, z. B. Builds, Tests und Bereitstellungen. 

Konfigurieren Sie die {{site.data.keyword.deliverypipeline}}, um das unterbrechungsfreie Erstellen, Testen und Bereitstellen Ihrer Apps zu automatisieren: 

1. Wenn Sie während der Toolchain-Erstellung diese Toolintegration konfigurieren, klicken Sie im Abschnitt 'Konfigurierbare Integrationen' auf **Delivery Pipeline**. Je nach verwendeter Vorlage stehen unterschiedliche Felder zur Verfügung. Überprüfen Sie die Standardfeldwerte und ändern Sie ggf. diese Einstellungen.
1. Wenn Sie bei einer Toolchain unter {{site.data.keyword.Bluemix_notm}} Public diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard in der Registerkarte **Toolchains** auf die Toolchain, um die Seite 'Toolintegrationen' zu öffnen. Sie können als Alternative auf der Übersichtsseite Ihrer App in der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. Wenn Sie eine Toolchain unter {{site.data.keyword.Bluemix_notm}} Dedicated verwenden klicken Sie im Dashboard in der Registerkarte **DEVOPS** auf die Toolchain, um die Seite 'Toolintegrationen' zu öffnen. Sie können als Alternative auf der Übersichtsseite Ihrer App rechts oben auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.  
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt 'Toolintegrationen' auf **Delivery Pipeline**.
1. Geben Sie für Ihre neue Pipeline einen Namen an.
1. Wenn Ihre Pipeline zum Bereitstellen einer Benutzerschnittstelle verwendet werden soll, aktivieren Sie das Kontrollkästchen **Viewable App**. Alle Apps, die Ihre Pipeline erstellt, werden auf der Seite 'Toolintegrationen' der Toolchain in der Liste **App anzeigen** angezeigt.
1. Klicken Sie auf **Create Integration**, um Ihrer Toolchain die {{site.data.keyword.deliverypipeline}} hinzuzufügen.
1. Klicken Sie auf die Kachel für Ihre {{site.data.keyword.deliverypipeline}}, um die Pipeline anzuzeigen und zu konfigurieren. Die Grundlagen zum Konfigurieren einer Pipeline finden Sie im Abschnitt [Pipelines erstellen und bereitstellen](../services/DeliveryPipeline/build_deploy.html){: new_window}.

  **Tipp**: Wenn Sie die Pipeline auslösen möchten, wenn Sie Änderungen an Ihr GitHub oder {{site.data.keyword.ghe_short}}-Repository (repo) übertragen möchten, müssen Sie GitHub oder {{site.data.keyword.ghe_short}} für Ihre Toolchain konfigurieren, bevor Sie die Stages für Ihre Pipeline definieren. Die Pipelinestages benötigen die Git-URLs für Ihre Repositorys. Jede Pipelinestage kann nur auf ein GitHub oder {{site.data.keyword.ghe_short}}-Repository verweisen, das Ihrer Toolchain zugeordnet ist. Anweisungen zum Konfigurieren von GitHub finden Sie im Abschnitt [GitHub](#github). Anweisungen zum Konfigurieren von Dedicated GitHub Enterprise finden Sie im Abschnitt [Einführung in {{site.data.keyword.ghe_long}}](../services/ghededicated/index.html){: new_window}.
  
1. Optional: Wenn Sie eine Toolchain unter {{site.data.keyword.Bluemix_notm}} Public verwenden und mit Sauce Labs Tests für Ihre App ausführen möchten, konfigurieren Sie die {{site.data.keyword.deliverypipeline}}, um einen Sauce Labs-Testjob hinzuzufügen. Anweisungen zum Konfigurieren des Testjobs finden Sie im Abschnitt [Sauce Labs-Testjobs in Ihrer Pipeline konfigurieren](#config_saucelabs).

### Sauce Labs-Testjob in Ihrer Pipeline konfigurieren
{: #config_saucelabs}

Bevor Sie einen Sauce Labs-Testjob in Ihrer Pipeline konfigurieren können, brauchen Sie eine funktionierende Pipeline mit Stages, um Ihre App zu erstellen und bereitzustellen. Außerdem müssen Sie Sauce Labs für Ihre Toolchain konfigurieren. Anweisungen zum Konfigurieren von Sauce Labs finden Sie im Abschnitt [Sauce Labs](#saucelabs).

Konfigurieren Sie die {{site.data.keyword.deliverypipeline}}, um einen Sauce Labs-Testjob hinzuzufügen:

1. Wenn Sie keine Stage haben, die eine Testversion Ihrer App bereitstellt, erstellen Sie eine.
1. Fügen Sie in der Stage erst den Bereitstellungsjob und dann den Testjob hinzu. Wenn sich beide Jobs in derselben Stage befinden, können Sie auf dieselben Umgebungseigenschaften zugreifen.
  ![Testjob](images/toolchain_test_job.png) 

1. Konfigurieren Sie die Stage: 

  a. Erstellen Sie in der Registerkarte **ENVIRONMENT PROPERTIES** diese drei Eigenschaften: CF_APP_NAME, SAUCE_USERNAME und SAUCE_ACCESS_KEY.
  
  b. Geben Sie Ihren Benutzernamen und den Zugriffsschlüssel für Sauce Labs ein. So lagern Sie diese Werte aus, damit Sie sie in Ihren Tests verwenden können.
  
1. Konfigurieren Sie den Bereitstellungsjob. Schließen Sie im Feld **Deploy Script** diesen Befehl ein: `export CF_APP_NAME="$CF_APP"`. Mit diesem Befehl wird der App-Name als Umgebungseigenschaft exportiert.
1. Konfigurieren Sie den Testjob. Die Werte in den folgenden Abbildungen sind Beispiele. Die Felder **Serviceinstanz**, **Ziel**, **Organisation** und **Bereich** werden mit dem Benutzernamen, der Region, der Organisation und dem Bereich für Sauce Labs gefüllt.
![Job konfigurieren](images/toolchain_configure_job.png)

  a. Wählen Sie für den Testertyp **Sauce Labs** aus.
  
  b. Wählen Sie für die Serviceinstanz den Benutzernamen für Sauce Labs aus, den Sie zum Konfigurieren von Sauce Labs für Ihre Toolchain verwendet haben. 
  
   **Tipp**: Um den Benutzernamen und den Zugriffsschlüssel anzuzeigen, den Sie für die Konfiguration von Sauce Labs für Ihre Toolchain verwendet haben, klicken Sie auf **Konfigurieren**. 
  
  c. Geben Sie im Feld **Test Execution Command** die Befehle ein, mit denen die Abhängigkeiten installiert werden, die von Ihren Tests sowie zur Testausführung benötigt werden. Sie können zum Beispiel für die App 'Node.js' folgende Befehle eingeben:
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. Wenn Sie Ihre Testberichte in den Testjobprotokollen anzeigen möchten, aktivieren Sie das Kontrollkästchen **Enable Test Report** und legen Sie das Dateimuster für das Testergebnis auf `test/*.xml` fest.
  
1. Klicken Sie auf **Speichern**. Jedes Mal, wenn Ihre Pipeline ausgeführt wird, werden Ihre Sauce Labs-Test ausgeführt.

Weitere Informationen finden Sie im Abschnitt [Delivery Pipeline](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}.


## {{site.data.keyword.DRA_short}} hinzufügen
{: #dra}

{{site.data.keyword.DRA_full}} erfasst und analysiert die Ergebnisse aus den Komponententest, Funktionstests und Codeabdeckungstools, um zu bestimmten, ob Ihr Code den vordefinierten Kriterien bei bestimmten Gates in Ihrem Entwicklungsprozess entspricht. Wenn Ihr Code die Kriterien nicht erfüllt oder überschreitet, wird die Bereitstellung gestoppt, um Risiken zu vermeiden. Sie können {{site.data.keyword.DRA_short}} als Sicherheitsnetz für Ihre kontinuierliche Bereitstellungsumgebung oder zur Implementierung und Verbesserung von Qualitätsstandards verwenden. 

 **Hinweis**: Diese Toolintegration ist vordefiniert. Es sind keine Konfigurationsparameter erforderlich und sie kann auch nicht erneut konfiguriert werden.
 
Fügen Sie {{site.data.keyword.DRA_short}} hinzu, um die Qualität Ihres Codes in {{site.data.keyword.Bluemix_notm}} zu pflegen und zu verbessern, indem Ihre Bereitstellung überwacht wird, um Risiken vor der Veröffentlichung zu identifizieren.

1. Wenn Sie bei einer Toolchain diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard in der Registerkarte **Toolchains** auf die Toolchain, um die Seite 'Toolintegrationen' zu öffnen. Sie können als Alternative auf der Übersichtsseite der App in der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.  
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt 'Toolintegrationen' auf **Deployment Risk Analytics**. 
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Kachel für {{site.data.keyword.DRA_short}} und führen Sie die ersten Schritte aus: Kriterien erstellen, die Kriterien mit der Pipeline verbinden und die Pipeline ausführen. Weitere Informationen finden Sie unter [{{site.data.keyword.DRA_short}}](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}.


## Die Eclipse Orion {{site.data.keyword.webide}} hinzufügen
{: #webide}

Die Eclipse Orion {{site.data.keyword.webide}} ist eine integrierte, webbasierte Umgebung, in der Sie Tasks zur Quellcodeverwaltung erstellen, bearbeiten, ausführen, debuggen und abschließen können. Sie können das Bearbeiten, das Ausführen, das Einreichen und Bereitstellen nahtlos durchführen. 

 **Hinweis**: Diese Toolintegration ist vordefiniert. Es sind keine Konfigurationsparameter erforderlich und sie kann auch nicht erneut konfiguriert werden.
 
Um die Tasks zur Quellcodeverwaltung durchzuführen, fügen Sie die Toolintegration für die Eclipse Orion {{site.data.keyword.webide}} hinzu:

1. Wenn Sie bei einer Toolchain unter {{site.data.keyword.Bluemix_notm}} Public diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard in der Registerkarte **Toolchains** auf die Toolchain, um die Seite 'Toolintegrationen' zu öffnen. Sie können als Alternative auf der Übersichtsseite der App in der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. Wenn Sie eine Toolchain unter {{site.data.keyword.Bluemix_notm}} Dedicated verwenden klicken Sie im Dashboard in der Registerkarte **DEVOPS** auf die Toolchain, um die Seite 'Toolintegrationen' zu öffnen. Sie können als Alternative auf der Übersichtsseite Ihrer App rechts oben auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. 
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt 'Toolintegrationen' auf **Web-IDE für Eclipse Orion**. 
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Kachel für die Eclipse Orion {{site.data.keyword.webide}}. Ihr Arbeitsbereich wird mit Ihrem GitHub oder {{site.data.keyword.ghe_short}}-Repository vorab gefüllt. Die Repositorys, die Ihrer aktuellen Toolchain zugeordnet sind, werden hervorgehoben.

Weitere Informationen finden Sie im Abschnitt [Code mit der Eclipse Orion {{site.data.keyword.webide}} bearbeiten](../toolchains/web_ide.html){: new_window}.


## GitHub konfigurieren
{: #github}

GitHub ist ein webbasierter Hosting-Service für Git-Repositorys. Sie können sowohl lokale als auch ferne Kopien Ihrer Repositorys haben. Dadurch vereinfacht sich die Zusammenarbeit. 

GitHub Issues ist ein Trackingtool, mit dem Sie Ihre Arbeit und Pläne an einer zentralen Stelle aufbewahren können. Es ist in Ihrem Entwicklungs-Respository integriert, sodass Sie sich auf wichtige Tasks konzentrieren können.

Konfigurieren Sie GitHub, um Ihren Quellcode in der Cloud zu verwalten:

1. Wenn Sie während der Toolchain-Erstellung diese Toolintegration konfigurieren, führen Sie die folgenden Schritte aus:

 a. Klicken Sie im Abschnitt 'Konfigurierbare Integrationen' auf **GitHub**. Wenn {{site.data.keyword.Bluemix_notm}} keine Berechtigung hat, auf GitHub zuzugreifen, klicken Sie auf **Berechtigen**, um zur GitHub-Website zu gehen. Wenn Sie keine aktive GitHub-Sitzung haben, werden Sie aufgefordert, sich anzumelden. Klicken Sie auf die Option****, mit der die Anwendung berechtigt wird, {{site.data.keyword.Bluemix_notm}} auf Ihr GitHub-Konto zuzugreifen. Wenn Sie bei einer aktiven GitHub-Sitzung vor längerer Zeit Ihr Kennwort eingegeben haben, werden Sie möglicherweise aufgefordert, Ihr GitHub-Kennwort zur Bestätigung einzugeben.
 
 b. Überprüfen Sie die Standardzielposition für die GitHub-Repositorys. Diese Repositorys werden vom Beispiel-Repository geklont. Ändern Sie bei Bedarf die Namen der Ziel-Repositorys.
 ![Standardzielposition für Repositorys](images/toolchain_github_config.png)
   
1. Wenn Sie bei einer Toolchain diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard in der Registerkarte **Toolchains** auf die Toolchain, um die Seite 'Toolintegrationen' zu öffnen. Sie können als Alternative auf der Übersichtsseite der App in der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.  
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt 'Toolintegrationen' auf **GitHub**.
1. Wenn Sie ein vorhandenes GitHub-Repository verwenden möchten, geben Sie die URL ein. Klicken Sie für den Repository-Typ auf **Verknüpfen**.
1. Wenn Sie ein neues GitHub-Repository verwenden möchten, geben Sie für das GitHub-Repository einen Namen und die URL des Repositorys ein, von dem Sie klonen oder aufspalten, und wählen Sie den Repository-Typ aus: 

 a. Um ein leeres Repository zu erstellen, klicken Sie auf **Neu**. 
 
 b. Um eine Kopie eines GitHub-Repository zu erstellen, klicken Sie auf **Klonen**.
 
 c. Um ein GitHub-Repository aufzuspalten, sodass Sie Änderungen über Pull-Anforderungen beisteuern können, klicken Sie auf **Verzweigen**.
 
1. Wenn Sie GitHubs Issues für die Problemverfolgung verwenden möchten, aktivieren Sie das Kontrollkästchen **GitHub Issues aktivieren**.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Kachel für das GitHub-Repository, mit dem Sie arbeiten möchten. Die GitHub-Website wird geöffnet, auf der Sie die Inhalte des Repositorys sehen können.
 
  **Tipp**: Sie können in der Eclipse Orion {{site.data.keyword.webide}} die Management-Tools für den Quellcode verwenden, um das GitHub-Repository zu bearbeiten und eine App aus Ihrem Arbeitsbereich bereitzustellen.

1. Wenn Sie GitHub Issues aktiviert haben, klicken Sie zum Öffnen auf die Kachel für GitHub Issues.

Weitere Informationen finden Sie im Abschnitt [GitHub](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} und [GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.


## Dedicated GitHub Enterprise konfigurieren
{: #configghe}

{{site.data.keyword.ghe_long}} ist ein lokaler, webbasierter Hosting-Service für Git-Repositorys. Dedicated GitHub Enterprise eignet sich nur für Kunden von {{site.data.keyword.Bluemix_notm}} Dedicated. GitHub Issues ist ein Trackingtool, mit dem Sie Ihre Arbeit und Pläne an einer zentralen Stelle aufbewahren können. Es ist in Ihrem Entwicklungs-Respository integriert, sodass Sie sich auf wichtige Tasks konzentrieren können. Weitere Informationen zu Dedicated GitHub Enterprise und GitHub Issues finden Sie im Abschnitt [Dedicated GitHub Enterprise verwenden](../services/ghededicated/index.html){: new_window} und [GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.

Sie können {{site.data.keyword.ghe_short}} als eine Toolintegration in Ihrer Toolchain konfigurieren, sodass Sie den Quellcode in der [{{site.data.keyword.Bluemix_notm}} Dedicated](../dedicated/index.html#dedicated){: new_window}-Unternehmensinstanz verwalten können.

1. Wenn Sie während der Toolchain-Erstellung diese Toolintegration konfigurieren, führen Sie die folgenden Schritte aus:

 a. Bevor Sie sich zum ersten Mal bei Dedicated GitHub Enterprise anmelden, bitten Sie den Bereichsadministrator Ihres Unternehmens, Ihre Benutzer-ID zur {{site.data.keyword.Bluemix_notm}} Dedicated-Instanz aus der Benutzerregistry des Unternehmens mit LDAP hinzuzufügen. Weitere Informationen zu Einrichten Ihres {{site.data.keyword.ghe_short}}-Kontos finden Sie im Abschnitt [Dedicated GitHub Enterprise verwenden](../services/ghededicated/index.html){: new_window}.
 
 b. Klicken Sie im Abschnitt 'Konfigurierbare Integrationen' auf **{{site.data.keyword.ghe_short}}**.    
 
 c. Überprüfen Sie den Standardnamen für das neue {{site.data.keyword.ghe_short}}-Repository. Ändern Sie bei Bedarf die Namen des neuen Repositorys. In der folgenden Abbildung wird ein Repository dargestellt, das von einem Beispiel-Repository geklont wurde. Sie können ein vorhandenes oder neues Repository verwenden. Um ein neues Repository zu verwenden, können Sie ein leeres Repository erstellen, ein Repository klonen oder aufspalten.
 ![Standardposition für Repositorys](images/toolchain_ghe_config.png)
   
1. Wenn Sie bei einer Toolchain unter {{site.data.keyword.Bluemix_notm}} Public diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard in der Registerkarte **Toolchains** auf die Toolchain, um die Seite 'Toolintegrationen' zu öffnen. Sie können als Alternative auf der Übersichtsseite Ihrer App in der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. Wenn Sie eine Toolchain unter {{site.data.keyword.Bluemix_notm}} Dedicated verwenden klicken Sie im Dashboard in der Registerkarte **DEVOPS** auf die Toolchain, um die Seite 'Toolintegrationen' zu öffnen. Sie können als Alternative auf der Übersichtsseite Ihrer App rechts oben auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. 
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt 'Toolintegrationen' auf **{{site.data.keyword.ghe_short}}**.
1. Wenn Sie ein vorhandenes {{site.data.keyword.ghe_short}}-Repository verwenden möchten, geben Sie die URL des Repositorys ein. Klicken Sie für den Repository-Typ auf **Vorhanden**.
1. Wenn Sie ein neues {{site.data.keyword.ghe_short}}-Repository verwenden möchten, geben Sie für das Repository einen Namen und die URL des Repositorys ein, von dem Sie klonen oder aufspalten, und wählen Sie den Repository-Typ aus: 

 a. Um ein leeres Repository zu erstellen, klicken Sie auf **Neu**. 
 
 b. Um eine Kopie eines Repository zu erstellen, klicken Sie auf **Klonen**.
 
 c. Um ein Repository aufzuspalten, sodass Sie Änderungen über Pull-Anforderungen beisteuern können, klicken Sie auf **Verzweigen**.
 
1. Um GitHubs Issues für die Problemverfolgung zu verwenden, aktivieren Sie das Kontrollkästchen **GitHub Issues aktivieren**.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Kachel für das {{site.data.keyword.ghe_short}}-Repository, mit dem Sie arbeiten möchten. Die [{{site.data.keyword.Bluemix_notm}} Dedicated](../dedicated/index.html#dedicated){: new_window}-Instanz Ihres Unternehmens wird geöffnet, auf der Sie die Inhalte des Repositorys sehen können.
 
  **Tipp**: Sie können in der Eclipse Orion {{site.data.keyword.webide}} die Management-Tools für den Quellcode verwenden, um das {{site.data.keyword.ghe_short}}-Repository zu bearbeiten und eine App aus Ihrem Arbeitsbereich bereitzustellen.

1. Wenn Sie GitHub Issues aktiviert haben, klicken Sie auf die Kachel für GitHub Issues.

<!-- 8/23/2016: The GHE Dedicated content has been moved to docs-staging/services/ghededicated/index.md -->

## PagerDuty konfigurieren
{: #pagerduty}

PagerDuty integriert Daten aus mehreren Überwachungssystemen in eine Gesamtansicht. Wenn ein Problem auftritt, stellt PagerDuty sicher, dass das Teammitglied, das am geeignetsten erscheint, das Problem zu beheben, benachrichtigt wird. Wenn das Teammitglied nicht auf die Problembenachrichtigung reagiert, kann das Problem mit konfigurierten Eskalationen an andere Mitarbeiter oder Operationsmanager weitergeleitet werden.

Konfigurieren Sie PagerDuty, damit Benachrichtigungen gesendet werden, wenn Pipelinestage-Fehler auftreten und diese für geringere Ausfallzeiten schneller behoben werden können:

1. Wenn Sie während der Toolchain-Erstellung diese Toolintegration konfigurieren, klicken Sie im Abschnitt 'Konfigurierbare Integrationen' auf **PagerDuty**. 
1. Wenn Sie bei einer Toolchain diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard in der Registerkarte **Toolchains** auf die Toolchain, um die Seite 'Toolintegrationen' zu öffnen. Sie können als Alternative auf der Übersichtsseite der App in der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.  
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt 'Toolintegrationen' auf **PagerDuty**
1. Geben Sie den Namen der PagerDuty-Site ein, die Ihrem PagerDuty-Konto zugeordnet ist. Wenn Sie kein PagerDuty-Konto besitzen, [registrieren Sie sich für ein Konto](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Geben Sie den API-Zugriffsschlüssel für Ihr PagerDuty-Konto ein. Anweisungen zum Finden des Schlüssels finden Sie im Abschnitt [API-Authentifizierung](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Geben Sie den Namen Ihres PagerDuty-Service ein.
1. Geben Sie die E-Mail-Adresse des PagerDuty-Hauptansprechpartners ein.
1. Geben Sie die Telefonnummer des PagerDuty-Hauptansprechpartners ein.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Kachel für PagerDuty, um 'pagerduty.com' aufzurufen. Sie können die Ereignisse anzeigen, die dem PagerDuty-Service zugeordnet sind, den Sie beim Konfigurieren dieser Toolintegration für Ihre Toolchain angegeben haben. 

Weitere Informationen finden Sie im Abschnitt [PagerDuty](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Sauce Labs konfigurieren
{: #saucelabs}

Sauce Labs führt funktionale Komponententests aus. Wenn eine Sauce Labs-Testsuite als Testjob in der {{site.data.keyword.deliverypipeline}} konfiguriert wird, kann die Testsuite für Ihre Web- oder mobile App als Teil des kontinuierlichen Bereitstellungsprozesses ausgeführt werden. Diese Tests können eine wertvolle Ablaufsteuerung für Ihre Projekte bereitstellen und als Gates fungieren, um die Entwicklung von fehlerhaftem Code zu verhindern.

Konfigurieren Sie Sauce Labs, um automatisierte Funktionstests unter mehreren Betriebssystemen und Browsern auszuführen, um zu emulieren, wie ein Benutzer eine Website oder Anwendung verwendet: 

1. Wenn Sie während der Toolchain-Erstellung diese Toolintegration konfigurieren, klicken Sie im Abschnitt 'Konfigurierbare Integrationen' auf **Sauce Labs**. 
1. Wenn Sie bei einer Toolchain diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard in der Registerkarte **Toolchains** auf die Toolchain, um die Seite 'Toolintegrationen' zu öffnen. Sie können als Alternative auf der Übersichtsseite der App in der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.  
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt 'Toolintegrationen' auf **Sauce Labs**.
1. Geben Sie den Benutzernamen ein, die Ihrem Sauce Labs-Konto zugeordnet ist. Sie finden [Ihren Benutzernamen in der Willkommensnachricht oben auf Ihrer Sauce Labs-Kontoseite](https://saucelabs.com/account){: new_window}.
1. Geben Sie den Zugriffsschlüssel für Ihren Sauce Labs-Account ein.Sie finden [den Zugriffsschlüssel links unten auf Ihrer Sauce Labs-Kontoseite](https://saucelabs.com/account){: new_window}.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Kachel für Sauce Labs, um 'saucelabs.com' aufzurufen und zeigen Sie die Testaktivität für die Toolchain an.

 **Tipp**: Wenn Sie der {{site.data.keyword.deliverypipeline}} den Sauce Labs-Testjob hinzugefügt haben, können Sie die Serviceinstanz auswählen.

Weitere Informationen finden Sie im Abschnitt [Sauce Labs](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}.


## Slack konfigurieren
{: #slack}

**Wichtig**: Benachrichtigungen, die in öffentlichen Slack-Kanälen veröffentlicht werden, sind für alle Teammitglieder sichtbar. Denken Sie daran, dass Sie für den Inhalt Ihrer Beiträge verantwortlich sind.

Slack ist ein cloudbasiertes Messaging- und Benachrichtigungssystem in Echtzeit. Slack stellt einen persistenten Chat bereit und ist für eine interaktive Zusammenarbeit im Team eine bessere Alternative als die E-Mail. Sie können über einen dedizierten Kanal oder über mehrere Kanäle mit direktem Bezug zu Ihrer Arbeit mit Ihrem Team kommunizieren. Sie können auch Dateien und Bilder gemeinsam nutzen sowie direkte Nachrichten an zwei oder mehrere Benutzer senden. Die Kommunikation über Kanäle und Direktnachrichten wird aufbewahrt, sodass Sie sie durchsuchen können. 

Konfigurieren Sie Slack, um Nachrichten über Ihre Toolchain aus den Toolintegrationen (z. B. Test- oder Bereitstellungsaktivitäten) zu empfangen:

1. Wenn Sie während der Toolchain-Erstellung diese Toolintegration konfigurieren, klicken Sie im Abschnitt 'Konfigurierbare Integrationen' auf **Slack**. 
1. Wenn Sie bei einer Toolchain diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard in der Registerkarte **Toolchains** auf die Toolchain, um die Seite 'Toolintegrationen' zu öffnen. Sie können als Alternative auf der Übersichtsseite der App in der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. 
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt 'Toolintegrationen' auf **Slack**.
1. Geben Sie Ihr API-Authentifizierungstoken für Ihr Slack-Konto ein. Für die Authentifizierung mit Slack ist ein generierter Token mit uneingeschränktem Zugriff erforderlich. Anweisungen zum Finden des Tokens finden Sie im Abschnitt [Slack-Authentifizierung](https://api.slack.com/web#authentication){: new_window}.
1. Geben Sie den Namen des Slack-Kanals ein, an den Sie Benachrichtigungen senden möchten. Wenn der angegebene Kanal nicht existiert, wird er erstellt. Wenn der Kanal archiviert wurde, wird er wieder aktiviert.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Kachel für Slack. Sie können jede Aktivität für Ihre Toolchain im konfigurierten Slack-Kanal anzeigen.

eitere Informationen finden Sie im Abschnitt [Slack](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.
