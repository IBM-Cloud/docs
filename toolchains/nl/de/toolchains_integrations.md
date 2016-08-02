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

*Letzte Aktualisierung: 17. Juni 2016*
{: .last-updated}

Sie können Toolintegrationen konfigurieren, die Entwicklungs-, Bereitstellungs- und Systemtasks unterstützen, während Sie eine Toolchain erstellen, oder Sie können Toolintegrationen hinzufügen und konfigurieren, um eine vorhandene Toolchain anzupassen.   
{:shortdesc}

**Wichtig**: Diese Funktion ist experimentell. Toolchains sind unter Umständen nicht stabil und können sich auf eine Weise ändern, die nicht mit früheren Versionen kompatibel ist. Es wird empfohlen, sie nicht in Produktionsumgebungen einzusetzen. Wenn Sie Toolchains verwenden möchten, müssen Sie eine einmalige [Zugriffsanforderung](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window} stellen. Toolchains sind nur in USA (Süden) verfügbar. 

**Tipp**: Wenn Sie beginnen möchten, mit Ihrem eigenen Code zu entwickeln, müssen Sie sicherstellen, dass Sie die GitHub- und GitHub Issues-Toolintegrationen vor der {{site.data.keyword.deliverypipeline}} konfigurieren. 

## Delivery Pipeline konfigurieren
{: #deliverypipeline}

Die {{site.data.keyword.deliverypipeline}} automatisiert die kontinuierliche Entwicklung Ihrer Projekte durch aufeinanderfolgende Stages, in denen Eingaben abgerufen und Jobs wie Builds, Tests und Bereitstellungen ausgeführt werden.  

Konfigurieren Sie die {{site.data.keyword.deliverypipeline}}, um das kontinuierliche Erstellen, Testen und Bereitstellen Ihrer Apps zu automatisieren:  

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **Delivery Pipeline**. Abhängig von der Schablone, die Sie verwenden, sind unterschiedliche Felder verfügbar. Überprüfen Sie die Standardfeldwerte und ändern Sie diese Einstellungen gegebenenfalls. 
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Registerkarte **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.  
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+). 
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf **Delivery Pipeline**. 
1. Geben Sie einen Namen für Ihre neue Pipeline an. 
1. Wenn Sie mithilfe Ihrer Pipeline eine Benutzerschnittstelle bereitstellen möchten, wählen Sie das Kontrollkästchen **Anzeigbare App** aus. Alle Apps, die Ihre Pipeline erstellt, werden in der Liste **APP ANZEIGEN** auf der Seite mit den Toolintegrationen der Toolchain angezeigt. 
1. Klicken Sie auf **Integration erstellen**, um die {{site.data.keyword.deliverypipeline}} zu Ihrer Toolchain hinzuzufügen. 
1. Klicken Sie auf die {{site.data.keyword.deliverypipeline}}-Kachel, um die Pipeline anzuzeigen und zu konfigurieren. Die Grundlagen des Konfigurierens einer Pipeline finden Sie unter [Pipelines erstellen und bereitstellen](../services/DeliveryPipeline/build_deploy.html){: new_window}. 

  **Tipp**: Falls Sie die Pipeline aktivieren möchten, wenn Sie Änderungen per Push-Operation an Ihr GitHub-Repository übertragen, müssen Sie GitHub für Ihre Toolchain konfigurieren, bevor Sie die Stages für Ihre Pipeline definieren. Die Pipeline-Stages benötigen die Git-URLs für Ihre GitHub-Repositorys. Jede Pipeline-Stage kann nur auf ein einziges GitHub-Repository verweisen, das Ihrer Toolchain zugeordnet ist. Anweisungen zum Konfigurieren von GitHub finden Sie im Abschnitt [GitHub und GitHub Issues](#github). 
  
1. Optional: Wenn Sie möchten, dass Sauce Labs Ihre App testet, konfigurieren Sie die {{site.data.keyword.deliverypipeline}}, um einen Sauce Labs-Testjob hinzuzufügen. Anweisungen zum Konfigurieren des Testjobs finden Sie im Abschnitt [Sauce Labs-Testjob in Ihrer Pipeline konfigurieren](#config_saucelabs). 

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
  
1. Konfigurieren Sie den Bereitstellungsjob. Schließen Sie im Feld **Bereitstellungsscript** diesen Befehl ein: export CF_APP_NAME="$CF_APP". Der Befehl exportiert den Namen der App als Umgebungseigenschaft. 
1. Konfigurieren Sie den Testjob. Die Werte in der folgenden Abbildung sind Beispiele. In die Felder **Serviceinstanz**, **Ziel**, **Organisation** und **Bereich** werden der Sauce Labs-Benutzername, die Region, die Organisation und der Bereich eingetragen, die Sie aktuell verwenden. ![Job konfigurieren](images/toolchain_configure_job.png)

  Wählen Sie als Testertyp **Sauce Labs** aus. 
  
  b. Wählen Sie als Serviceinstanz den Sauce Labs-Benutzernamen aus, den Sie beim Konfigurieren von Sauce Labs für Ihre Toolchain verwendet haben.  
  
   **Tipp**: Um zu sehen, welchen Benutzernamen und Zugriffsschlüssel Sie beim Konfigurieren von Sauce Labs für Ihre Toolchain verwendet haben, klicken Sie auf **Konfigurieren**.  
  
  c. Geben Sie im Feld **Testausführungsbefehl** die Befehle ein, die die für Ihre Tests erforderlichen Abhängigkeiten installieren, und führen Sie dann die Tests aus. Für eine hypothetische Node.js-App würden Sie beispielsweise Folgendes eingeben: 
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. Wenn Sie Ihre Testberichte in den Testjobprotokollen anzeigen möchten, wählen Sie das Kontrollkästchen **Testbericht aktivieren** aus und legen Sie Dateimuster für Testergebnisse auf `test/*.xml` fest. 
  
1. Klicken Sie auf **SPEICHERN**. Jetzt werden immer, wenn Ihre Pipeline aktiv ist, Sauce Labs-Tests ausgeführt. 

Weitere Informationen finden Sie unter [Delivery Pipeline](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}. 

## Bereitstellungsrisikoanalysen hinzufügen 
{: #dra}

{{site.data.keyword.DRA_full}} erfasst und analysiert die Ergebnisse von Komponententests, Funktionstests und Codeabdeckungstools, um zu bestimmen, ob Ihr Code vordefinierte Kriterien an angegebenen Punkten in Ihrem Bereitstellungsprozess erfüllt. Falls Ihr Code die Kriterien nicht erfüllt oder mehr als erfüllt, wird die Bereitstellung gestoppt, um keine Risiken einzuführen. Sie können eine Bereitstellungsrisikoanalyse als Sicherheitsnetz für Ihre kontinuierliche Bereitstellungsumgebung oder als Methode zum Implementieren und Verbessern von Qualitätsstandards einsetzen.  

 **Tipp**: Diese Toolintegration ist vorkonfiguriert. Sie erfordert keine Konfigurationsparameter und Sie können sie nicht neu konfigurieren. 
 
Fügen Sie Bereitstellungsrisikoanalysen hinzu, um die Qualität Ihres Codes in Bluemix aufrechtzuerhalten und zu verbessern, indem Sie Ihre Bereitstellungen überwachen und Risiken erkennen, bevor sie eingeführt werden: 

1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Registerkarte **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.  
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+). 
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf die Option für Bereitstellungsrisikoanalysen****.  
1. Klicken Sie auf **Integration erstellen**. 
1. Klicken Sie auf die Kachel für Bereitstellungsrisikoanalysen und führen Sie dann die anfänglichen Schritte aus: Kriterien erstellen, Kriterien mit der Pipeline verknüpfen und Pipeline ausführen. Weitere Informationen finden Sie unter [Deployment Risk Analytics](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}. 

## Eclipse Orion-{{site.data.keyword.webide}} hinzufügen
{: #webide}

Die Eclipse Orion-{{site.data.keyword.webide}} ist eine integrierte webbasierte Umgebung, in der Sie Quellcodeverwaltungstasks erstellen, bearbeiten, ausführen, debuggen und abschließen können. Sie können nahtlos von der Bearbeitung zur Ausführung, zur Übergabe und zur Bereitstellung übergehen.  

 **Tipp**: Diese Toolintegration ist vorkonfiguriert. Sie erfordert keine Konfigurationsparameter und Sie können sie nicht neu konfigurieren. 
 
Fügen Sie die Toolintegration der Eclipse Orion-{{site.data.keyword.webide}} hinzu, um Quellcodeverwaltungstasks abzuschließen: 

1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Registerkarte **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.  
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+). 
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf die Option für die Eclipse Orion-Web-IDE****.  
1. Klicken Sie auf **Integration erstellen**. 
1. Klicken Sie auf die Kachel für die neue Eclipse Orion-Web-IDE. In Ihrem Arbeitsbereich sind Ihre GitHub-Repositorys bereits aufgeführt. Die Repositorys, die Ihrer aktuellen Toolchain zugeordnet sind, sind hervorgehoben. 

Weitere Informationen finden Sie unter [Web-IDE](https://www.ibm.com/devops/method/content/code/tool_web_ide/){: new_window}. 


## GitHub und GitHub Issues konfigurieren
{: #github}

GitHub ist ein webbasierter Hosting-Service für Git-Repositorys. Sie können sowohl über lokale als auch über ferne Kopien Ihrer Repositorys verfügen, was die Zusammenarbeit sehr einfach gestaltet.  

GitHub Issues ist ein Überwachungstool, das Ihre Arbeit und Ihre Pläne an einem zentralen Ort aufbewahrt. Es ist in Ihr Entwicklungsrepository integriert, damit Sie sich auf die wichtigen Aufgaben konzentrieren können. 

Konfigurieren Sie GitHub und GitHub Issues zum Verwalten Ihres Quellcodes in der Cloud: 

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, führen Sie diese Schritte aus: 

 a. Klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **GitHub**. Wenn Sie {{site.data.keyword.Bluemix}} nicht für den Zugriff auf GitHub autorisiert haben, klicken Sie auf **Autorisieren**, um zur GitHub-Website zu wechseln. Wenn keine aktive GitHub-Sitzung existiert, werden Sie aufgefordert, sich anzumelden. Klicken Sie auf **Anwendung autorisieren**, um {{site.data.keyword.Bluemix}} den Zugriff auf Ihr GitHub-Konto zu erlauben. Falls eine aktive GitHub-Sitzung existiert, Sie Ihr Kennwort aber bereits vor einiger Zeit eingegeben haben, werden Sie möglicherweise aufgefordert, Ihr GitHub-Kennwort durch erneute Eingabe zu bestätigen. 
 
 b. Überprüfen Sie die Standardspeicherorte für die GitHub-Zielrepositorys. Diese Repositorys werden aus den Beispielrepositorys geklont. Ändern Sie gegebenenfalls die Namen der Zielrepositorys.
![Standardspeicherorte für Zielrepositorys](images/toolchain_github_config.png) 
   
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Registerkarte **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.  
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+). 
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf **GitHub**. 
1. Falls Sie über ein GitHub-Repository verfügen und es verwenden möchten, geben Sie die URL ein. Klicken Sie für den Repository-Typ auf **Link**. 
1. Falls Sie ein neues GitHub-Repository verwenden möchten, geben Sie einen Namen für das GitHub-Repository ein, das Sie klonen oder verzweigen, und wählen Sie den Repository-Typ aus:  

 a. Wählen Sie **Neu** aus, um ein leeres Repository zu erstellen.  
 
 b. Wählen Sie **Klonen** aus, um eine Kopie eines GitHub-Repository zu erstellen. 
 
 c. Wählen Sie **Verzweigen** aus, um ein GitHub-Repository zu verzweigen, sodass Sie Änderungen per Pull-Anforderungen beitragen können. 
 
1. Wenn Sie GitHub Issues zum Überwachen von Problemen verwenden möchten, wählen Sie das Kontrollkästchen **GitHub Issues aktivieren** aus. 
1. Klicken Sie auf **Integration erstellen**. 
1. Klicken Sie auf die Kachel für das GitHub-Repository, mit dem Sie arbeiten möchten, um github.com zu öffnen und die Inhalte des Repositorys anzuzeigen. 
 
  **Tipp**: Sie können die integrierten Quellcodeverwaltungstools in der Eclipse Orion-Web-IDE verwenden, um das GitHub-Repository zu bearbeiten und eine App aus Ihrem Arbeitsbereich bereitzustellen. 

1. Falls Sie GitHub Issues aktiviert haben, klicken Sie auf die Kachel für GitHub Issues, um zu GitHub Issues zu wechseln. 

Weitere Informationen finden Sie unter [GitHub](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} und [GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.     

##Dedicated {{site.data.keyword.ghe_short}} verwenden
{: #ghe}

{{site.data.keyword.ghe_long}} ist die IBM Cloud-gehostete und vollständig verwaltete Version von {{site.data.keyword.ghe_short}}, verfügbar für Bluemix Dedicated-Umgebungen. GitHub bietet das bei Entwicklern beliebte Social-Coding. [{{site.data.keyword.Bluemix_notm}} Dedicated](../dedicated/index.html#dedicated){: new_window} stellt eine Cloud-Computing-Umgebung auf physisch isolierter Hardware bereit, die in Ihr Netzwerk integriert ist. 

Dedicated {{site.data.keyword.ghe_short}} ist nur für {{site.data.keyword.Bluemix_notm}} Dedicated-Kunden verfügbar. 

### Konto einrichten 

{{site.data.keyword.ghe_short}} schließt Single Sign-on mit {{site.data.keyword.Bluemix_notm}} Dedicated ein. Um sich bei {{site.data.keyword.ghe_short}} anzumelden, fügen Sie die URL von Ihrem Regionsadministrator oder aus der Begrüßungs-E-Mail in einen Browser ein. Ihre URL sollte folgendes Muster aufweisen: `github.name-ihres-unternehmens.bluemix.net`. Melden Sie sich mit Ihrer {{site.data.keyword.Bluemix_notm}} Dedicated-Benutzer-ID und Ihrem Kennwort an. Daraufhin wird Ihr {{site.data.keyword.ghe_short}}-Konto automatisch erstellt. 

**Hinweis:** Falls Sie in einer Nachricht darauf hingewiesen werden, dass Ihre Benutzer-ID nicht existiert, bitten Sie Ihren Regionsadministrator, Ihre Benutzer-ID zur {{site.data.keyword.Bluemix_notm}} Dedicated-Benutzerregistry hinzuzufügen. Falls Sie der Regionsadministrator sind, finden Sie weitere Informationen unter [{{site.data.keyword.Bluemix_notm}} Dedicated-Benutzer und -Berechtigungen verwalten](https://new-console.stage1.ng.bluemix.net/docs/admin/index.html#oc_useradmin){: new_window}. 

In den meisten Fällen ist Ihr GitHub-Benutzername der E-Mail-Kurzname, es sei denn, Ihr Kurzname enthält Zeichen, die GitHub nicht unterstützt, z. B. Punkte. Falls Ihr Kurzname Zeichen enthält, die GitHub nicht unterstützt, werden diese Zeichen durch Gedankenstriche ersetzt.      

### E-Mail-Adresse zu Ihrem Konto hinzufügen

Sie müssen Ihre E-Mail-Adresse zu Ihren {{site.data.keyword.ghe_short}}-Kontoeinstellungen hinzufügen, um Benachrichtigungen zu erhalten. Nachdem Sie Ihre E-Mail-Adresse hinzugefügt haben, können Sie die Social-Coding-Funktionen von {{site.data.keyword.ghe_short}} nutzen.     
 
Führen Sie diese Schritte aus, um Ihre E-Mail-Adresse zu Ihrem Dedicated {{site.data.keyword.ghe_short}}-Konto hinzuzufügen:     
1. Klicken Sie in der oberen rechten Ecke einer beliebigen GitHub-Seite auf Ihr Profilsymbol und klicken Sie dann auf **Einstellungen**.     
2. Klicken Sie in der Seitenleiste auf **E-Mail**.     
3. Fügen Sie Ihre E-Mail-Adresse hinzu und klicken Sie auf **Hinzufügen**.      

{: #ghe_auth}
### Persönliches Zugriffstoken oder SSH-Schlüssel für die Authentifizierung erstellen

Um ferne Git-Operationen wie `clone` oder `push` aus Ihrem lokalen Git-Repository auszuführen, müssen Sie ein persönliches Zugriffstoken oder einen SSH-Schlüssel zur Authentifizierung bei {{site.data.keyword.ghe_short}} verwenden. Eine Authentifizierung über HTTPS wird nur mit einem Zugriffstoken unterstützt. Sie können nicht Ihre Benutzer-ID oder Ihr Kennwort verwenden, um aus einem lokalen Repository eine 'clone'- oder 'push'-Operation auszuführen. API-Anforderungen erfordern ebenfalls ein persönliches Zugriffstoken. 

**Hinweis:** Um ein persönliches Zugriffstoken bzw. einen SSH-Schlüssel zur Authentifizierung zu verwenden, müssen Sie Git lokal einrichten. Anweisungen finden Sie unter [Set Up Git](https://help.github.com/enterprise/2.6/user/articles/set-up-git/){: new_window}.     

Führen Sie die folgenden Schritte aus, um ein persönliches Zugriffstoken zu erstellen:     
   1. Klicken Sie in der oberen rechten Ecke einer beliebigen GitHub-Seite auf Ihr Profilsymbol und klicken Sie dann auf **Einstellungen**.     
   2. Klicken Sie in der Seitenleiste auf **Persönliche Zugriffstoken**.    
   3. Klicken Sie auf **Neues Token generieren**. 
   4. Fügen Sie eine Tokenbeschreibung hinzu und klicken Sie auf **Token generieren**. 
   5. Kopieren Sie das Token an einen sicheren Speicherort oder in eine Kennwortmanagement-App.
     **Hinweis:** Aus Sicherheitsgründen können Sie nach Verlassen der Seite das Token nicht erneut anzeigen.     

Verwenden Sie Ihr persönliches Zugriffstoken statt eines Kennworts für den Befehlszeilenzugriff über HTTPS.  


Führen Sie die folgenden Schritte aus, um einen SSH-Schlüssel zu erstellen: 
   1. Öffnen Sie Git Bash (Windows) oder ein neues Terminalfenster (Linux und Mac).     
   2. Fügen Sie den folgenden Text ein, wobei Sie die E-Mail-Adresse, die Sie zu Ihrem {{site.data.keyword.ghe_short}}-Konto hinzugefügt haben, ersetzen: 
   
     ``
     ssh-keygen -t rsa -b 4096 -C "ihre_e-mail@beispiel.com"
     # Creates a new ssh key, using the provided email as a
label
     Generating public/private rsa key pair.
     ``

   3. Wenn Sie aufgefordert werden, eine Datei anzugeben, in der der Schlüssel gespeichert werden soll, drücken Sie die Eingabetaste, um die Standardposition zu übernehmen. 
   4. Geben Sie bei entsprechender Aufforderung eine sichere Kennphrase ein. Weitere Informationen finden Sie unter [Working with SSH key passphrases](https://help.github.com/enterprise/2.6/user/articles/working-with-ssh-key-passphrases/){: new_window}.    

Fügen Sie Ihren SSH-Schlüssel zu ssh-agent hinzu:     
   1. Stellen Sie sicher, dass ssh-agent aktiviert ist. Geben Sie mithilfe von Git Bash diesen Befehl ein, um ssh-agent zu aktivieren:
      ``
      # start the ssh-agent in the background
      $ eval "$(ssh-agent -s)"
      Agent pid 59566
      ``    
  
   2. Fügen Sie Ihren SSH-Schlüssel zu ssh-agent hinzu, indem Sie diesen Befehl eingeben:
``
$ ssh-add ~/.ssh/id_rsa
      ``    
   3. Fügen Sie den SSH-Schlüssel zu Ihrem GitHub-Konto hinzu. Weitere Informationen finden Sie unter [Adding a new SSH key to your GitHub account](https://help.github.com/enterprise/2.6/user/articles/adding-a-new-ssh-key-to-your-github-account/){: new_window}.     
   

### GitHub-Organisationen, -Teams und -Repositorys einrichten    

Das Einrichten von GitHub-Organisationen ist nützlich, weil Sie verschiedene Gruppen von Benutzern erstellen, die an ähnlichen Projekten oder Tasks arbeiten. Das Organisieren von Teams innerhalb einer Organisation hat den zusätzlichen Vorteil, dass Sie den Zugriff auf Repositorys steuern können. Weitere Informationen finden Sie unter [Organizations and teams](https://help.github.com/enterprise/2.6/admin/guides/user-management/organizations-and-teams/){: new_window}. 

**Hinweis:** GitHub-Organisationen sind nicht dasselbe wie Bluemix-Organisationen. 

Richten Sie das Projekt Ihres Teams ein, indem Sie diese Tasks ausführen: 

   1. [Organisation erstellen](https://help.github.com/enterprise/2.6/user/articles/creating-a-new-organization-account/){: new_window}. 
   2. [Repository für Ihre Organisation erstellen](https://help.github.com/enterprise/2.6/user/articles/create-a-repo/){: new_window}. 
   3. [Benutzer einladen, Ihrer Organisation beizutreten](https://help.github.com/enterprise/2.6/user/articles/inviting-users-to-join-your-organization/){: new_window}. 
   4. [Vorsichtig mindestens ein Teammitglied auswählen, das Benutzerberechtigungen in Ihrer Organisation haben soll](https://help.github.com/enterprise/2.6/user/articles/changing-a-person-s-role-to-owner/){: new_window}.     
   
  **Hinweis:** Bevor Sie Benutzer in Ihre Organisation einladen, müssen sie sich mindestens einmal bei {{site.data.keyword.ghe_short}} anmelden, oder ihre {{site.data.keyword.ghe_short}}-Konten stehen nicht für das Einladen zur Verfügung. 
   
### Unterstützung anfordern
Um jetzt Antworten zu erhalten, übergeben Sie Fragen an [Stack Overflow](http://stackoverflow.com/questions/ask?tags=ibm-bluemix_github-enterprise){: new_window}.  

Weitere Unterstützung erhalten Sie unter den folgenden Ressourcen:     
   1. Füllen Sie das Formular unter https://ibm.biz/bluemixsupport aus.    
   2. Übergeben Sie ein neues Ticket über das Client Success Portal unter https://support.ibmcloud.com/ics/support/mylogin.asp?login=bluemix.     


## PagerDuty konfigurieren
{: #pagerduty}

PagerDuty integriert Daten aus mehreren Überwachungssystemen in einer Gesamtansicht. Wenn ein Problem auftritt, stellt PagerDuty sicher, dass das Teammitglied, das zu diesem Zeitpunkt am besten geeignet ist, das Problem zu lösen, benachrichtigt wird. Falls das Teammitglied nicht auf das Problem reagiert, können Eskalationen konfiguriert werden, um es an sekundäre Entwickler oder Betriebsleiter weiterzuleiten. 

Konfigurieren Sie PagerDuty, um Benachrichtigungen zu senden, wenn Pipeline-Stage-Fehler auftreten, damit Sie Probleme schneller beheben und Ausfallzeiten reduzieren können: 

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **PagerDuty**. 
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Registerkarte **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.  
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+). 
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf **PagerDuty**. 
1. Geben Sie den Namen der PagerDuty-Website ein, die Ihrem PagerDuty-Konto zugeordnet ist. Wenn Sie kein PagerDuty-Konto haben, [registrieren Sie sich für eines](https://signup.pagerduty.com/accounts/new){: new_window}. 
1. Geben Sie den API-Zugriffsschlüssel für Ihr PagerDuty-Konto ein. Anweisungen zum Auffinden des Schlüssels finden Sie auf der Seite für die [API-Authentifizierung](https://signup.pagerduty.com/accounts/new){: new_window}. 
1. Geben Sie den Namen Ihres PagerDuty-Service ein. 
1. Geben Sie die E-Mail-Adresse für den primären PagerDuty-Kontakt ein. 
1. Geben Sie die Telefonnummer für den primären PagerDuty-Kontakt ein. 
1. Klicken Sie auf **Integration erstellen**. 
1. Klicken Sie auf die Kachel für PagerDuty, um pagerduty.com zu öffnen. Sie können die Ereignisse anzeigen, die dem PagerDuty-Service zugeordnet sind, den Sie während der Konfiguration dieser Toolintegration für Ihre Toolchain angegeben haben.  

Weitere Informationen finden Sie unter [PagerDuty](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}. 


## Sauce Labs konfigurieren
{: #saucelabs}

Sauce Labs führt funktionelle Komponententests aus. Wenn eine Sauce Labs-Testsuite als Testjob in der {{site.data.keyword.deliverypipeline}} konfiguriert wird, kann die Testsuite Tests für Ihre Web- oder Mobil-App als Teil Ihres kontinuierlichen Bereitstellungsprozesses ausführen. Anhand dieser Tests können Sie eine reibungslose Ablaufsteuerung für Ihre Projekte realisieren, da sie verhindern, dass fehlerhafter Code bereitgestellt wird. 

Konfigurieren Sie Sauce Labs, um automatische funktionelle Tests auf mehreren Betriebssystemen und in mehreren Browsern auszuführen, sodass Sie die Art und Weise emulieren können, auf die ein Benutzer möglicherweise eine Website oder eine Anwendung nutzt. 

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **Sauce Labs**. 
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Registerkarte **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**.  
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+). 
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf **Sauce Labs**. 
1. Geben Sie den Benutzernamen ein, der Ihrem Sauce Labs-Konto zugeordnet ist. Sie können [Ihren Benutzernamen in der Begrüßungsnachricht oben auf Ihrer Sauce Labs-Kontoseite](https://saucelabs.com/account){: new_window} finden. 
1. Geben Sie den Zugriffsschlüssel für Ihr Sauce Labs-Konto ein. Sie können [den Schlüssel in der linken oberen Ecke Ihrer Sauce Labs-Kontoseite finden](https://saucelabs.com/account){: new_window}. 
1. Klicken Sie auf **Integration erstellen**. 
1. Klicken Sie auf die Kachel für Sauce Labs, um saucelabs.com zu öffnen und die Testaktivität für die Toolchain anzuzeigen. 

 **Tipp**: Wenn Sie einen Sauce Labs-Testjob zur {{site.data.keyword.deliverypipeline}} hinzugefügt haben, können Sie die Serviceinstanz auswählen. 

Weitere Informationen finden Sie unter [Sauce Labs](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}. 


## Slack konfigurieren
{: #slack}

**Wichtig**: Benachrichtigungen, die in öffentlichen Slack-Kanälen gepostet werden, sind für jeden im Team sichtbar. Denken Sie daran, dass Sie für den Inhalt, den Sie posten, verantwortlich sind. 

Slack ist ein cloudbasiertes echtzeitorientiertes Messaging- und Benachrichtigungssystem. Slack stellt persistenten Chat bereit, wobei es sich um eine interaktivere Alternative zu E-Mail für die Teamzusammenarbeit handelt. Sie können mit Ihrem Team über einen dedizierten Kanal oder über eine Reihe von Kanälen kommunizieren, die in direktem Zusammenhang mit Ihrer Arbeit stehen. Sie können außerdem Dateien und Bilder über die Kanäle oder in direkten Nachrichten zwischen zwei oder mehr Personen teilen. Die Kommunikation in direkten Nachrichten und über die Kanäle wird aufbewahrt und kann durchsucht werden.  

Konfigurieren Sie Slack, um Benachrichtigungen zu Ihrer Toolchain von den Toolintegrationen zu erhalten, z. B. Test- und Bereitstellungsaktivitäten: 

1. Wenn Sie diese Toolintegration konfigurieren, während Sie die Toolchain erstellen, klicken Sie im Abschnitt mit den konfigurierbaren Integrationen auf **Slack**. 
1. Wenn Sie eine Toolchain haben und diese Toolintegration hinzufügen, klicken Sie im DevOps-Dashboard auf der Registerkarte **Toolchains** auf die Toolchain, um die zugehörige Seite mit den Toolintegrationen zu öffnen. Alternativ können Sie auf der Übersichtsseite der App auf der Kachel 'Continuous Delivery' auf **Toolchain anzeigen** klicken. Klicken Sie dann auf **Toolintegrationen**. 
1. Klicken Sie auf die Schaltfläche zum Hinzufügen (+). 
1. Klicken Sie im Abschnitt mit den Toolintegrationen auf **Slack**. 
1. Geben Sie das API-Authentifizierungstoken für Ihr Slack-Konto ein. Sie müssen ein generiertes Token für uneingeschränkten Zugriff zur Authentifizierung bei Slack verwenden. Anweisungen zum Auffinden des Tokens finden Sie im Abschnitt zur [Slack-Authentifizierung](https://api.slack.com/web#authentication){: new_window}. 
1. Geben Sie den Namen des Slack-Kanals ein, an den die Benachrichtigungen gesendet werden sollen. Falls der Kanal, den Sie angeben, nicht existiert, wird er erstellt. Falls der Kanal archiviert wurde, wird er reaktiviert. 
1. Klicken Sie auf **Integration erstellen**. 
1. Klicken Sie auf die Kachel für Slack. Sie können alle Aktivitäten für Ihre Toolchain im konfigurierten Slack-Kanal anzeigen. 

Weitere Informationen finden Sie unter [Slack](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}. 
