---

Copyright:
  Jahre: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Toolintegrationen konfigurieren
{: #integrations}

Letzte Aktualisierung: 18. Oktober 2016
{: .last-updated}

Sie können Toolintegrationen konfigurieren, die Entwicklungs-, Bereitstellungs- und Systemtasks unterstützen, während Sie eine Toolchain erstellen, oder Sie können Toolintegrationen hinzufügen und konfigurieren, um eine vorhandene Toolchain anzupassen.  
{:shortdesc}

**Wichtig**: Unter {{site.data.keyword.Bluemix_notm}} Public sind Toolchains nur in den USA (Süden) verfügbar.

Die Toolintegrationen, die zum Hinzufügen und Konfigurieren für Ihre Toolchain zur Verfügung stehen, sind unterschiedlich, abhängig davon, ob Sie Toolchains unter {{site.data.keyword.Bluemix_notm}} Public oder {{site.data.keyword.Bluemix_notm}} Dedicated verwenden. Falls Sie Toolchains bei {{site.data.keyword.Bluemix_notm}} Dedicated verwenden, variieren die für Sie verfügbaren Toolintegrationen abhängig davon, wie {{site.data.keyword.jazzhub_title}} in Ihrer speziellen Umgebung konfiguriert wurde.

*Tabelle 1. Toolintegrationen, die für Toolchains unter {{site.data.keyword.Bluemix_notm}} Public und Dedicated verfügbar sind*

|Toolintegration |Verfügbar unter {{site.data.keyword.Bluemix_notm}} Public	|Verfügbar unter {{site.data.keyword.Bluemix_notm}} Dedicated (umgebungsabhängig)|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.deliverypipeline}} 		|Ja	   	|Ja  		|
|{{site.data.keyword.DRA_short}} 		|Ja		|Nein			|
|Eclipse Orion {{site.data.keyword.webide}}		|Ja		|Ja			|
|GitHub		|Ja		|Ja		|
|Dedicated GitHub Enterprise			|Nein		|Ja		|
|Anderes Tool			|Ja		|Ja		|
|PagerDuty			|Ja		|Ja		|
|Sauce Labs		|Ja		|Nein		|
|Slack			|Ja		|Ja		|

**Tipp**: Wenn Sie beginnen möchten, mit Ihrem eigenen Code unter {{site.data.keyword.Bluemix_notm}} Public zu entwickeln, müssen Sie die GitHub-Toolintegration konfigurieren, bevor Sie die {{site.data.keyword.deliverypipeline}} konfigurieren. Wenn Sie beginnen möchten, mit Ihrem eigenen Code unter {{site.data.keyword.Bluemix_notm}} Dedicated zu entwickeln, müssen Sie die {{site.data.keyword.ghe_short}}-Toolintegration oder die GitHub-Toolintegration vor der {{site.data.keyword.deliverypipeline}} konfigurieren. 


## Delivery Pipeline konfigurieren
{: #deliverypipeline}

Die {{site.data.keyword.deliverypipeline}} automatisiert die kontinuierliche Entwicklung Ihrer Projekte durch aufeinanderfolgende Stages, in denen Eingaben abgerufen und Jobs wie Builds, Tests und Bereitstellungen ausgeführt werden. 

Konfigurieren Sie die {{site.data.keyword.deliverypipeline}}, um das kontinuierliche Erstellen, Testen und Bereitstellen Ihrer Apps zu automatisieren: 

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **Delivery Pipeline**. Abhängig von der Vorlage, die Sie verwenden, sind unterschiedliche Felder verfügbar. Überprüfen Sie die Standardfeldwerte und ändern Sie diese Einstellungen gegebenenfalls.
1. Wenn Sie unter {{site.data.keyword.Bluemix_notm}} Public eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite Ihrer App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. Wenn Sie unter {{site.data.keyword.Bluemix_notm}} Dedicated eine Toolchain verwenden, klicken Sie im Dashboard auf der Registerkarte **DEVOPS** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie in der rechten oberen Ecke auf der Übersichtsseite der App auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. 
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf **Delivery Pipeline**.
1. Geben Sie einen Namen für Ihre neue Pipeline an.
1. Wenn Sie mithilfe Ihrer Pipeline eine Benutzerschnittstelle bereitstellen möchten, wählen Sie das Kontrollkästchen **Anzeigbare App** aus. Alle Apps, die Ihre Pipeline erstellt, werden in der Liste **APP ANZEIGEN** auf der Seite mit den Toolintegrationen der Toolchain angezeigt.
1. Klicken Sie auf **Integration erstellen**, um die {{site.data.keyword.deliverypipeline}} zu Ihrer Toolchain hinzuzufügen.
1. Klicken Sie auf die {{site.data.keyword.deliverypipeline}}-Kachel, um die Pipeline anzuzeigen und zu konfigurieren. Die Grundlagen des Konfigurierens einer Pipeline finden Sie unter [Pipelines erstellen und bereitstellen (Link wird in neuem Fenster geöffnet)](../services/DeliveryPipeline/build_deploy.html){: new_window}.

  **Tipp**: Falls Sie die Pipeline aktivieren möchten, wenn Sie Änderungen per Push-Operation an Ihr GitHub- oder {{site.data.keyword.ghe_short}}-Repository übertragen, müssen Sie GitHub oder {{site.data.keyword.ghe_short}} für Ihre Toolchain konfigurieren, bevor Sie die Stages für Ihre Pipeline definieren. Die Pipeline-Stages benötigen die Git-URLs für Ihre Repositorys. Jede Pipeline-Stage kann nur auf eines der GitHub- oder {{site.data.keyword.ghe_short}}-Repositorys verweisen, das Ihrer Toolchain zugeordnet ist. Anweisungen zum Konfigurieren von GitHub finden Sie im Abschnitt [GitHub](#github). Anweisungen zum Konfigurieren von Dedicated GitHub Enterprise finden Sie unter [Einführung in {{site.data.keyword.ghe_long}} (Link wird in neuem Fenster geöffnet)](../services/ghededicated/index.html){: new_window}.
  
1. Optional: Wenn Sie eine Toolchain unter {{site.data.keyword.Bluemix_notm}} Public verwenden und Sie möchten, dass Sauce Labs Ihre App testet, konfigurieren Sie die {{site.data.keyword.deliverypipeline}}, um einen Sauce Labs-Testjob hinzuzufügen. Anweisungen zum Konfigurieren des Testjobs finden Sie im Abschnitt [Sauce Labs-Testjob in Ihrer Pipeline konfigurieren](#config_saucelabs).

### Sauce Labs-Testjob in Ihrer Pipeline konfigurieren
{: #config_saucelabs}

Bevor Sie einen Sauce Labs-Testjob in Ihrer Pipeline konfigurieren, brauchen Sie eine funktionstüchtige Pipeline, die Stages zum Erstellen und Bereitstellen Ihrer App umfasst, und Sie müssen Sauce Labs für Ihre Toolchain konfigurieren. Anweisungen zum Konfigurieren von Sauce Labs finden Sie im Abschnitt [Sauce Labs](#saucelabs).

Konfigurieren Sie die {{site.data.keyword.deliverypipeline}}, um einen Sauce Labs-Testjob hinzuzufügen:

1. Wenn keine Stage vorhanden ist, die eine Testversion Ihrer App bereitstellt, erstellen Sie eine.
1. Fügen Sie in der Stage einen Testjob nach dem Bereitstellungsjob hinzu. Indem Sie diese Jobs in derselben Stage platzieren, können sie auf dieselbe Gruppe von Umgebungseigenschaften zugreifen.   
  ![Testjob](images/toolchain_test_job.png) 

1. Konfigurieren Sie die Stage: 

  a. Erstellen Sie auf der Registerkarte **UMGEBUNGSEIGENSCHAFTEN** drei Eigenschaften: CF_APP_NAME, SAUCE_USERNAME und SAUCE_ACCESS_KEY.
  
  b. Geben Sie Ihren Sauce Labs-Benutzernamen und -Zugriffsschlüssel ein. Dadurch stellen Sie diese Werte extern bereit und können sie in Ihren Tests verwenden.
  
1. Konfigurieren Sie den Bereitstellungsjob. Schließen Sie im Feld **Bereitstellungsscript** diesen Befehl ein: `export CF_APP_NAME="$CF_APP"`. Der Befehl exportiert den Namen der App als Umgebungseigenschaft.
1. Konfigurieren Sie den Testjob. Die Werte in der folgenden Abbildung sind Beispiele. In die Felder **Serviceinstanz**, **Ziel**, **Organisation** und **Bereich** werden der Sauce Labs-Benutzername, die Region, die Organisation und der Bereich eingetragen, die Sie verwenden.  
![Job konfigurieren](images/toolchain_configure_job.png)

  Wählen Sie als Testertyp **Sauce Labs** aus.
  
  b. Wählen Sie als Serviceinstanz den Sauce Labs-Benutzernamen aus, den Sie beim Konfigurieren von Sauce Labs für Ihre Toolchain verwendet haben. 
  
   **Tipp**: Um zu sehen, welchen Benutzernamen und Zugriffsschlüssel Sie beim Konfigurieren von Sauce Labs für Ihre Toolchain verwendet haben, klicken Sie auf **Konfigurieren**. 
  
  c. Geben Sie im Feld **Befehl für die Testausführung** die Befehle ein, die die für Ihre Tests erforderlichen Abhängigkeiten installieren, und führen Sie dann die Tests aus. Für eine Node.js-App würden Sie beispielsweise folgende Befehle eingeben:
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. Wenn Sie Ihre Testberichte in den Testjobprotokollen anzeigen möchten, wählen Sie das Kontrollkästchen **Testbericht aktivieren** aus und legen Sie Dateimuster für Testergebnisse auf `test/*.xml` fest.
  
1. Klicken Sie auf **SPEICHERN**. Immer, wenn Ihre Pipeline aktiv ist, werden Sauce Labs-Tests ausgeführt.

Weitere Informationen finden Sie unter [Delivery Pipeline (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}.


## {{site.data.keyword.DRA_short}} hinzufügen
{: #dra}

{{site.data.keyword.DRA_full}} erfasst und analysiert die Ergebnisse von Komponententests, Funktionstests und Codeabdeckungstools, um zu bestimmen, ob Ihr Code vordefinierte Kriterien an angegebenen Punkten in Ihrem Bereitstellungsprozess erfüllt. Falls Ihr Code die Kriterien nicht erfüllt oder mehr als erfüllt, wird die Bereitstellung gestoppt, um keine Risiken einzuführen. Sie können {{site.data.keyword.DRA_short}} als Sicherheitsnetz für Ihre kontinuierliche Bereitstellungsumgebung oder als Methode zum Implementieren und Verbessern von Qualitätsstandards einsetzen. 

 **Hinweis**: Diese Toolintegration ist vorkonfiguriert. Sie erfordert keine Konfigurationsparameter und Sie können sie nicht neu konfigurieren.
 
Fügen Sie {{site.data.keyword.DRA_short}} hinzu, um die Qualität Ihres Codes in {{site.data.keyword.Bluemix_notm}} aufrechtzuerhalten und zu verbessern, indem Sie Ihre Bereitstellungen überwachen und Risiken erkennen, bevor sie eingeführt werden.

1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. 
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf die Option für Bereitstellungsrisikoanalysen****. 
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Kachel für {{site.data.keyword.DRA_short}} und führen Sie dann die anfänglichen Schritte aus: Kriterien erstellen, Kriterien mit der Pipeline verknüpfen und Pipeline ausführen. Weitere Informationen finden Sie unter [{{site.data.keyword.DRA_short}} (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}.


## Eclipse Orion-{{site.data.keyword.webide}} hinzufügen
{: #webide}

Die Eclipse Orion-{{site.data.keyword.webide}} ist eine integrierte webbasierte Umgebung, in der Sie Quellcodeverwaltungstasks erstellen, bearbeiten, ausführen, debuggen und abschließen können. Sie können nahtlos von der Bearbeitung zur Ausführung, zur Übergabe und zur Bereitstellung übergehen. 

 **Hinweis**: Diese Toolintegration ist vorkonfiguriert. Sie erfordert keine Konfigurationsparameter und Sie können sie nicht neu konfigurieren.
 
Fügen Sie die Toolintegration der Eclipse Orion-{{site.data.keyword.webide}} hinzu, um Quellcodeverwaltungstasks auszuführen:

1. Wenn Sie unter {{site.data.keyword.Bluemix_notm}} Public eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. Wenn Sie unter {{site.data.keyword.Bluemix_notm}} Dedicated eine Toolchain verwenden, klicken Sie im Dashboard auf der Registerkarte **DEVOPS** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie in der rechten oberen Ecke auf der Übersichtsseite der App auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf die Option für die Eclipse Orion-Web-IDE****. 
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Kachel für die neue Eclipse Orion-{{site.data.keyword.webide}}. In Ihrem Arbeitsbereich sind Ihre GitHub- oder {{site.data.keyword.ghe_short}}-Repositorys bereits aufgeführt. Die Repositorys, die Ihrer aktuellen Toolchain zugeordnet sind, sind hervorgehoben.

Weitere Informationen finden Sie unter [Code mit Eclipse Orion-{{site.data.keyword.webide}} bearbeiten (Link wird in neuem Fenster geöffnet)](../toolchains/web_ide.html){: new_window}.


## GitHub konfigurieren
{: #github}

GitHub ist ein webbasierter Hosting-Service für Git-Repositorys. Sie können sowohl über lokale als auch über ferne Kopien Ihrer Repositorys verfügen, was die Zusammenarbeit sehr einfach gestaltet. 

GitHub Issues ist ein Überwachungstool, das Ihre Arbeit und Ihre Pläne an einem zentralen Ort aufbewahrt. Es ist in Ihr Entwicklungsrepository integriert, damit Sie sich auf die wichtigen Aufgaben konzentrieren können.

Konfigurieren Sie GitHub zum Verwalten Ihres Quellcodes in der Cloud:

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, führen Sie diese Schritte aus:

 a. Klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **GitHub**. Wenn Sie die Toolchain unter {{site.data.keyword.Bluemix_notm}} Public erstellen und {{site.data.keyword.Bluemix_notm}} nicht für den Zugriff auf GitHub autorisiert haben, klicken Sie auf **Autorisieren**, um zur GitHub-Website zu wechseln. Wenn keine aktive GitHub-Sitzung existiert, werden Sie aufgefordert, sich anzumelden. Klicken Sie auf **Anwendung autorisieren**, um {{site.data.keyword.Bluemix_notm}} den Zugriff auf Ihr GitHub-Konto zu erlauben. Falls eine aktive GitHub-Sitzung existiert, Sie Ihr Kennwort aber bereits vor einiger Zeit eingegeben haben, werden Sie möglicherweise aufgefordert, Ihr GitHub-Kennwort durch erneute Eingabe zu bestätigen.
 
 b. Überprüfen Sie die Standardspeicherorte für die GitHub-Zielrepositorys. Diese Repositorys werden aus den Beispielrepositorys geklont. Ändern Sie gegebenenfalls die Namen der Zielrepositorys.
 ![Standardspeicherorte für Zielrepositorys](images/toolchain_github_config.png)
   
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. 
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf **GitHub**.
1. Falls Sie über ein GitHub-Repository verfügen und es verwenden möchten, geben Sie die URL ein. Klicken Sie für den Repository-Typ auf **Link**.
1. Falls Sie ein neues GitHub-Repository verwenden möchten, geben Sie einen Namen für das GitHub-Repository ein, das Sie klonen oder verzweigen, und wählen Sie den Repository-Typ aus: 

 a. Klicken Sie auf **Neu**, um ein leeres Repository zu erstellen. 
 
 b. Klicken Sie auf **Klonen**, um eine Kopie eines GitHub-Repositorys zu erstellen.
 
 c. Klicken Sie auf **Verzweigen**, um ein GitHub-Repository zu verzweigen, sodass Sie Änderungen per Pull-Anforderungen beitragen können.
 
1. Wenn Sie GitHub Issues zum Überwachen von Problemen verwenden möchten, wählen Sie das Kontrollkästchen **GitHub Issues aktivieren** aus.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Kachel für das GitHub-Repository, mit dem Sie arbeiten möchten. Daraufhin wird die GitHub-Website geöffnet, auf der Sie die Inhalte des Repositorys anzeigen können.
 
  **Tipp**: Sie können die integrierten Quellcodeverwaltungstools in der Eclipse Orion-{{site.data.keyword.webide}} verwenden, um das GitHub-Repository zu bearbeiten und eine App aus Ihrem Arbeitsbereich bereitzustellen.

1. Falls Sie GitHub Issues aktiviert haben, klicken Sie auf die Kachel für GitHub Issues, um GitHub Issues zu öffnen.

Weitere Informationen finden Sie unter [GitHub (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} und [GitHub Issues (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.


## Dedicated GitHub Enterprise konfigurieren
{: #configghe}

{{site.data.keyword.ghe_long}} ist ein lokaler webbasierter Hosting-Service für Git-Repositorys. Dedicated GitHub Enterprise ist nur für {{site.data.keyword.Bluemix_notm}} Dedicated-Kunden verfügbar. GitHub Issues ist ein Überwachungstool, das Ihre Arbeit und Ihre Pläne an einem zentralen Ort aufbewahrt. Es ist in Ihr Entwicklungsrepository integriert, damit Sie sich auf die wichtigen Aufgaben konzentrieren können. Weitere Informationen zu Dedicated GitHub Enterprise und GitHub Issues finden Sie im Abschnitt zur [Verwendung von Dedicated GitHub Enterprise (Link wird in neuem Fenster geöffnet)](../services/ghededicated/index.html){: new_window} bzw. unter [GitHub Issues (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.

Sie können {{site.data.keyword.ghe_short}} als Toolintegration in Ihrer Toolchain konfigurieren, sodass Sie Quellcode
in der Instanz von [{{site.data.keyword.Bluemix_notm}} Dedicated (Link wird in neuem Fenster geöffnet)](../dedicated/index.html#dedicated){: new_window}
Ihres Unternehmens verwalten können.

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, führen Sie diese Schritte aus:

 a. Bevor Sie sich zum ersten Mal bei Dedicated GitHub Enterprise anmelden, bitten Sie den Regionsadministrator Ihres Unternehmens, der {{site.data.keyword.Bluemix_notm}} Dedicated-Instanz Ihre Benutzer-ID aus dem Benutzerregistry Ihres Unternehmens unter Verwendung von LDAP hinzuzufügen. Informationen zum Einrichten Ihres {{site.data.keyword.ghe_short}}-Kontos finden Sie im Abschnitt zur Verwendung von [Dedicated GitHub Enterprise (Link wird in neuem Fenster geöffnet)](../services/ghededicated/index.html){: new_window}.
 
 b. Klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **{{site.data.keyword.ghe_short}}**.    
 
 c. Prüfen Sie den Standardnamen für das neue {{site.data.keyword.ghe_short}}-Repository. Ändern Sie gegebenenfalls den Namen des neuen Repositorys. Die folgende Abbildung zeigt ein Beispiel für ein Repository, das aus einem Beispielrepository geklont ist. Sie können ein vorhandenes oder ein neues Repository verwenden. Um ein neues Repository zu verwenden, können Sie ein leeres Repository erstellen oder Sie können ein Repository klonen oder verzweigen. 
 ![Standardspeicherorte für Repositorys](images/toolchain_ghe_config.png)
   
1. Wenn Sie unter {{site.data.keyword.Bluemix_notm}} Public eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite Ihrer App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. Wenn Sie unter {{site.data.keyword.Bluemix_notm}} Dedicated eine Toolchain verwenden, klicken Sie im Dashboard auf der Registerkarte **DEVOPS** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie in der rechten oberen Ecke auf der Übersichtsseite der App auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf **{{site.data.keyword.ghe_short}}**.
1. Falls Sie über ein {{site.data.keyword.ghe_short}}-Repository verfügen, das Sie verwenden wollen, geben Sie die URL für das Repository ein. Klicken Sie für den Repository-Typ auf **Vorhanden**.
1. Falls Sie ein neues {{site.data.keyword.ghe_short}}-Repository verwenden möchten, geben Sie einen Namen für das Repository ein, das Sie klonen oder verzweigen, und wählen Sie den Repository-Typ aus: 

 a. Klicken Sie auf **Neu**, um ein leeres Repository zu erstellen. 
 
 b. Klicken Sie auf **Klonen**, um eine Kopie eines Repositorys zu erstellen.
 
 c. Klicken Sie auf **Verzweigen**, um ein Repository zu verzweigen, sodass Sie Änderungen per Pull-Anforderungen beitragen können.
 
1. Wenn Sie GitHub Issues zum Überwachen von Problemen verwenden möchten, wählen Sie das Kontrollkästchen **GitHub Issues aktivieren** aus.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Kachel für das {{site.data.keyword.ghe_short}}-Repository, mit dem Sie arbeiten möchten. Die Instanz von [{{site.data.keyword.Bluemix_notm}} Dedicated (Link wird in neuem Fenster geöffnet)](../dedicated/index.html#dedicated){: new_window} Ihres Unternehmens wird geöffnet, in der Sie die Inhalte des Repositorys anzeigen können.
 
  **Tipp**: Sie können die integrierten Quellcodeverwaltungstools in der Eclipse Orion-{{site.data.keyword.webide}} verwenden, um das {{site.data.keyword.ghe_short}}-Repository zu bearbeiten und eine App aus Ihrem Arbeitsbereich bereitzustellen.

1. Falls Sie GitHub Issues aktiviert haben, klicken Sie auf die Kachel für GitHub Issues.

<!-- 8/23/2016: The GHE Dedicated content has been moved to docs-staging/services/ghededicated/index.md -->

## Angepasstes Tool konfigurieren (Option 'Other Tool')
{: #othertool}

Falls Ihr Team ein Tool verwendet, das nicht in der Liste der Toolchainintegrationen enthalten ist, können Sie ein angepasstes Tool integrieren. 

So konfigurieren Sie ein angepasstes Tool, damit es mit anderen Tools in Ihrer Toolchain zusammenarbeitet und für Ihr Team verfügbar ist:
1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **Other Tool**.

1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf **Other Tool**.
1. Geben Sie den Namen des Tools ein.
1. Wählen Sie eine Lebenszyklusphase aus, die dem Tool am genauesten entspricht. Die Auswahl der Lebenszyklusphase bestimmt die Kategorie, unter der Ihr Tool auf der Seite mit den Toolintegrationen angezeigt wird.
1. Fügen Sie eine URL für ein Symbol hinzu. Das Symbol wird auf der Karte für die Integration Ihres Tools angezeigt.
1. Fügen Sie eine URL für die Dokumentation hinzu.
1. Geben Sie einen Instanznamen für das Tool an. Beispiel: Tool für mein Team.
1. Fügen Sie eine URL für die Toolinstanz hinzu. Beim Klicken auf die Karte für die Toolintegration werden Sie zu der URL geführt, die Sie für die Toolinstanz angeben.
1. Fügen Sie eine Beschreibung des Tools hinzu. 
1. (Erweitert) Fügen Sie bei Bedarf zusätzliche Eigenschaften hinzu. Listen Sie beispielsweise alle Informationen oder Attribute auf, die gegebenenfalls für die Integration Ihres Tools bei anderen Tools in Ihrer Toolchain erforderlich sind.  
1. Klicken Sie auf **Integration erstellen**.

## PagerDuty konfigurieren
{: #pagerduty}

PagerDuty integriert Daten aus mehreren Überwachungssystemen in einer Gesamtansicht. Wenn ein Problem auftritt, stellt PagerDuty sicher, dass das Teammitglied, das zu diesem Zeitpunkt am besten geeignet ist, das Problem zu lösen, benachrichtigt wird. Falls das Teammitglied nicht auf das Problem reagiert, können Eskalationen konfiguriert werden, um es an sekundäre Entwickler oder Betriebsleiter weiterzuleiten.

Konfigurieren Sie PagerDuty, um Benachrichtigungen zu senden, wenn Pipeline-Stage-Fehler auftreten, damit Sie Probleme schneller beheben und Ausfallzeiten reduzieren können:

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **PagerDuty**.
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. 
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf **PagerDuty**.
1. Geben Sie den Namen der PagerDuty-Website ein, die Ihrem PagerDuty-Konto zugeordnet ist. Wenn Sie kein PagerDuty-Konto haben, [registrieren Sie sich für ein solches Konto (Link wird in neuem Fenster geöffnet)](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Geben Sie den API-Zugriffsschlüssel für Ihr PagerDuty-Konto ein. Anweisungen zum Auffinden des Schlüssels finden Sie auf der Seite für die [API-Authentifizierung (Link wird in neuem Fenster geöffnet)](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Geben Sie den Namen Ihres PagerDuty-Service ein.
1. Geben Sie die E-Mail-Adresse für den primären PagerDuty-Kontakt ein.
1. Geben Sie die Telefonnummer für den primären PagerDuty-Kontakt ein.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Kachel für PagerDuty, um pagerduty.com zu öffnen. Sie können die Ereignisse anzeigen, die dem PagerDuty-Service zugeordnet sind, den Sie während der Konfiguration dieser Toolintegration für Ihre Toolchain angegeben haben. 

Weitere Informationen finden Sie unter [PagerDuty (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Sauce Labs konfigurieren
{: #saucelabs}

Sauce Labs führt funktionelle Komponententests aus. Wenn eine Sauce Labs-Testsuite als Testjob in der {{site.data.keyword.deliverypipeline}} konfiguriert wird, kann die Testsuite Tests für Ihre Web- oder Mobil-App als Teil Ihres kontinuierlichen Bereitstellungsprozesses ausführen. Anhand dieser Tests können Sie eine reibungslose Ablaufsteuerung für Ihre Projekte erzielen, da die Bereitstellung von fehlerhaftem Code verhindert wird.

Konfigurieren Sie Sauce Labs, um automatische Funktionstests auf mehreren Betriebssystemen und in mehreren Browsern auszuführen, sodass Sie die Art und Weise emulieren können, auf die ein Benutzer möglicherweise eine Website oder eine Anwendung nutzt.

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **Sauce Labs**.
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. 
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf **Sauce Labs**.
1. Geben Sie den Benutzernamen ein, der Ihrem Sauce Labs-Konto zugeordnet ist. Sie finden [Ihren Benutzernamen in der Begrüßungsnachricht oben auf Ihrer Sauce Labs-Kontoseite (Link wird in neuem Fenster geöffnet)](https://saucelabs.com/account){: new_window}.
1. Geben Sie den Zugriffsschlüssel für Ihr Sauce Labs-Konto ein. Sie finden [den Schlüssel auf der Sauce Labs-Kontoseite (Link wird in neuem Fenster geöffnet)](https://saucelabs.com/account){: new_window}.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Kachel für Sauce Labs, um saucelabs.com zu öffnen und die Testaktivität für die Toolchain anzuzeigen.

 **Tipp**: Wenn Sie einen Sauce Labs-Testjob zur {{site.data.keyword.deliverypipeline}} hinzugefügt haben, können Sie die Serviceinstanz auswählen.

Weitere Informationen finden Sie unter [Sauce Labs (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}.


## Slack konfigurieren
{: #slack}

**Wichtig**: Benachrichtigungen, die in öffentlichen Slack-Kanälen gepostet werden, sind für jeden im Team sichtbar. Denken Sie daran, dass Sie für den Inhalt, den Sie posten, verantwortlich sind.

Slack ist ein cloudbasiertes echtzeitorientiertes Messaging- und Benachrichtigungssystem. Slack stellt persistenten Chat bereit, wobei es sich um eine interaktivere Alternative zu E-Mail für die Teamzusammenarbeit handelt. Sie können mit Ihrem Team über einen dedizierten Kanal oder über eine Reihe von Kanälen kommunizieren, die in direktem Zusammenhang mit Ihrer Arbeit stehen. Sie können außerdem Dateien und Bilder über die Kanäle oder in direkten Nachrichten zwischen zwei oder mehr Personen teilen. Die Kommunikation in direkten Nachrichten und über die Kanäle wird aufbewahrt und kann durchsucht werden. 

Konfigurieren Sie Slack, um Benachrichtigungen zu Ihrer Toolchain von den Toolintegrationen zu erhalten, z. B. Test- und Bereitstellungsaktivitäten:

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **Slack**.
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Seite **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+).
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf **Slack**.
1. Geben Sie das API-Authentifizierungstoken für Ihr Slack-Konto ein. Sie müssen ein generiertes Token für uneingeschränkten Zugriff zur Authentifizierung bei Slack verwenden. Anweisungen zum Auffinden des Tokens finden Sie im Abschnitt zur [Slack-Authentifizierung (Link wird in neuem Fenster geöffnet)](https://api.slack.com/web#authentication){: new_window}.
1. Geben Sie den Namen des Slack-Kanals ein, an den die Benachrichtigungen gesendet werden sollen. Falls der Kanal, den Sie angeben, nicht existiert, wird er erstellt. Falls der Kanal archiviert wurde, wird er reaktiviert.
1. Klicken Sie auf **Integration erstellen**.
1. Klicken Sie auf die Kachel für Slack. Sie können alle Aktivitäten für Ihre Toolchain im konfigurierten Slack-Kanal anzeigen.

Weitere Informationen finden Sie unter [Slack (Link wird in neuem Fenster geöffnet)](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.








