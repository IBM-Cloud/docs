---

copyright:
  years: 2015, 2017
lastupdated: "2017-5-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Upgrade Ihres {{site.data.keyword.jazzhub_short}}-Projekts zu einer Toolchain durchführen
{: #upgrade_projects}

Aus {{site.data.keyword.jazzhub}} wird künftig {{site.data.keyword.contdelivery_full}}. Als Teil dieser Änderungen wird für Projekte ein Upgrade zu Toolchains durchgeführt.

Sie können ein Upgrade für Ihr Projekt durchführen oder warten, bis das Upgrade automatisch vorgenommen wird. Die optimale Benutzererfahrung ergibt sich, wenn Sie sicherstellen, dass die [Voraussetzungen](#upgrade_prereqs) erfüllt sind und Sie für Ihr Projekt so bald wie möglich das Upgrade durchführen, damit Sie steuern können, wie der Name Ihrer Toolchain lautet und in welcher Organisation sie erstellt wird. {: shortdesc}

## Toolchains
{: #compare_toolchains}

Toolchains ähneln Projekten, weisen jedoch einige wichtige Unterschiede auf:

- Projekte können nur über ein Repository (repo) und eine Pipeline verfügen. Toolchains können so viele Repositorys und Pipelines besitzen wie nötig.
- Toolchains können Tools enthalten, die in Projekten nicht verfügbar sind, wie zum Beispiel Slack, Sauce Labs, PagerDuty und {{site.data.keyword.DRA_full}}.
- Der Zugriff auf Toolchains wird über standardmäßige {{site.data.keyword.Bluemix_notm}}-Organisationen verwaltet. Die Mitgliedschaft wird auf Organisationsebene gepflegt, wohingegen bei Projekten die Pflege von Mitgliedschaften auf Projektebene erfolgt.

Mehr zu Toolchains erfahren Sie in [YouTube![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://youtu.be/2SIPE1e7NJ4){: new_window} oder in der [Einführung in {{site.data.keyword.contdelivery_short}}](/docs/services/ContinuousDelivery/index.html).
[![Externer Link zu YouTube](images/CD_video.png)](https://youtu.be/2SIPE1e7NJ4){: new_window}

## Voraussetzungen
{: #upgrade_prereqs}

- Für den Zugriff auf die Toolchain Ihres aktualisierten Projekts benötigen Sie eine {{site.data.keyword.Bluemix_notm}}-ID. Vor der Durchführung des Upgrades müssen Sie daher sicherstellen, dass Sie über eine aktive {{site.data.keyword.Bluemix_notm}}-ID verfügen. Sollte das nicht der Fall sein, müssen Sie sich [anmelden](https://console.ng.bluemix.net/registration/).
- Stellen Sie sicher, dass die Angabe für Ihren {{site.data.keyword.jazzhub_short}}-Projekteigner richtig ist. Die Toolchain, die auf der Grundlage Ihres Projekts erstellt wird, ist künftig Teil der {{site.data.keyword.Bluemix_notm}}-Organisation dieses Eigners. 
- Stellen Sie bei der Planung für den Start des Upgrades sicher, dass Sie in jeder Organisation und jedem Bereich, in dem die Bereitstellung durch die Pipeline erfolgt, Mitglied sind. Die Durchführung des Upgrades kann von einem beliebigen Projektadministrator gestartet werden. Wenn jedoch der Administrator, der die Durchführung des Upgrades startet, nicht Mitglied aller Organisationen und Bereiche ist, in denen die Bereitstellung durch die Pipeline erfolgt, kann die Pipeline nicht erstellt werden. Die Person, die die Durchführung des Upgrades startet, wird Eigner des Repositorys in der Toolchain. 
- Die Eclipse Orion-Web-IDE in der Toolchain funktioniert gesondert von der Web-IDE, die Ihrem Projekt zugeordnet ist. Wenn Sie die {{site.data.keyword.webide}} verwenden und nicht festgeschriebene Änderungen vorliegen, führen Sie einen Commit für diese Änderungen aus, bevor Sie das Upgrade durchführen.


## Upgrade eines Projekts zu einer Toolchain durchführen
{: #project_to_toolchain}

**Wichtig:** Projekte unter hub.jazz.net und Toolchains werden in den Südstaaten der USA gehostet. Wenn Ihr Projekt für die Bereitstellung von Apps in anderen Regionen konfiguriert wurde, wird es auch nach dem Upgrade auf eine Toolchain weiterhin Apps in diesen Regionen bereitstellen. 

Wenn Ihr Projekt bereit für das Upgrade ist, wird eine Nachricht auf der Karte des Projekts und auf seiner Übersichtsseite angezeigt.

![Abbildung der Karte mit Bezeichnung 'Bereit für Upgrade'](images/card-project-to-upgrade.png)

![Nachricht 'Es ist an der Zeit für das Upgrade'](images/banner-ready-to-upgrade.png)

**Tipp:** Im Menü auf der Seite 'Meine Projekte' finden Sie Projekte, die bereit für das Upgrade sind:

![Abbildung des Menüelements 'Projekte für Upgrade'](images/menu-projects-to-upgrade.png)

Wenn Sie die Durchführung des Upgrades starten, sind die Pipeline-Stages in Ihrem Projekt gesperrt. Sie können sie weder ausführen noch ändern. Wenn Sie das Upgrade durch Löschen der Toolchain zurücksetzen, wird die Pipeline entsperrt. 

Wenn in Ihrem Projekt ein Git-Repository verwendet wird, das unter JazzHub gehostet wird, wird das Repository nach dem Start des Upgrades gesperrt, um die Integrität der Daten sicherzustellen, die in die Toolchain verschoben werden. Wenn Sie das Upgrade durch Löschen der Toolchain zurücksetzen, wird das Repository unter JazzHub entsperrt. 

## Upgradeprozess starten
{: #start_upgrade}

Bevor Sie den Upgradeprozess starten, können Sie ihn sich auf [YouTube![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://youtu.be/LSr2e3uvyLs){: new_window} in Aktion ansehen.
[![Externer Link zu YouTube](images/migration-video2.png)](https://youtu.be/LSr2e3uvyLs){: new_window}

Führen Sie die folgenden Schritte aus, um für Ihr Projekt das Upgrade zu einer Toolchain durchzuführen:

1. Starten Sie den Upgradeprozess. Klicken Sie dazu in der Bannernachricht auf **Jetzt Upgrade durchführen**. Die Seite für das Upgrade des Projekts zu einer Toolchain wird angezeigt.

   ![Beispiel für eine Upgradeseite](images/project-upgrade-toolchain.png)

   Einen Überblick über den Upgradeprozess können Sie sich verschaffen, indem Sie die Beschreibung auf dieser Seite lesen. Die Toolchain wird eine neue Pipeline enthalten, die dieselben Stages und Jobs wie die Pipeline des Projekts enthält. Außerdem enthält die Toolchain einen Verweis auf die Eclipse Orion-{{site.data.keyword.webide}}, die in {{site.data.keyword.contdelivery_short}} ausgeführt wird.

   Da das Projekt ein öffentliches Repository unter github.com verwendet, wird für die Toolchain in diesem Beispiel eine Verbindung zum selben GitHub-Repository hergestellt. Wenn Ihr Projekt ein Git-Repository verwendet, das unter JazzHub gehostet wird, werden die Inhalte dieses Repositorys durch Klonen in einem neuen Repository in {{site.data.keyword.gitrepos}} bereitgestellt, das Teil von
{{site.data.keyword.contdelivery_short}} ist. Vollständige Details zur Handhabung der einzelnen Repositorytypen finden Sie in der folgenden Tabelle. 

|Projektrepository |Projekttyp	|Toolchain-Repository |
|:----------|:------------------------------|:------------------|
|github.com 		|Privat oder öffentlich 		|Dasselbe github.com-Repository mit {{site.data.keyword.Bluemix_notm}} Public.	|
|hub.jazz.net/git		|Privat oder öffentlich 		|Ein neues Repository in {{site.data.keyword.gitrepos}} mit {{site.data.keyword.Bluemix_notm}} Public. 	|
{: caption="Tabelle 1. Zuordnung von Projektrepositorys zu Toolchain-Repositorys" caption-side="top"}

2. Durch Konfigurieren einiger Einstellungen können Sie die Toolchain anpassen:

   - Wenn Sie den Namen der Toolchain ändern wollen, bearbeiten Sie das Feld **Name**.

      ![Feld 'Name'](images/name-change.png)

   - Wenn Sie ändern wollen, in welcher {{site.data.keyword.Bluemix_notm}}-Organisation die Toolchain erstellt wird, wählen Sie die gewünschte Organisation im Menü Ihres Kontos aus:

      ![Auswahlfunktion für Bluemix-Organisation](images/bluemix-organization-chooser.png)

   Da die Verwaltung von Toolchains auf Organisationsebene erfolgt, müssen Sie unbedingt eine Organisation auswählen, bei der die Projektmitglieder, die Zugriff auf die Toolchain benötigen, entweder bereits vorhanden sind oder aber hinzugefügt werden können.

3. Falls Sie in Ihrem Projekt Track & Plan verwendet haben, können Sie Ihre Track & Plan-Daten an GitHub Issues übertragen. 

   ![Track and Plan - Optionen](images/upgrade-tutorial-track-and-plan.png)

   - Geben Sie an, ob Sie Ihre Track & Plan-Daten migrieren möchten. 
   - Standardmäßig werden alle Ihre Track & Plan-Daten migriert. Wenn Sie es vorziehen, nur die Arbeitselemente zu migrieren, die Teil einer bestimmten Abfrage sind, müssen Sie diese Abfrage angeben. 
   - Wählen Sie alle Arbeitselementattribute aus, die Sie Bezeichnungen in GitHub Issues zuordnen wollen. 

4. Klicken Sie auf **Erstellen**. Die neue Toolchain wird erstellt und ihre Übersichtsseite wird angezeigt.

   ![Übersicht über die Toolchain, für die das Upgrade durchgeführt wurde](images/new-toolchain-page.png)

   - Wenn Sie auf Ihr GitHub-Repository oder den Tracker für zugehörige Probleme zugreifen wollen, klicken Sie auf **GitHub** oder auf **Probleme**.
   - Wenn Sie auf die Pipeline zugreifen wollen, klicken Sie auf **Delivery Pipeline**.
   - Wenn Sie auf die {{site.data.keyword.webide}} zugreifen wollen, die diejenigen Inhalte Ihres Repositorys enthält, die in den Arbeitsbereich ausgecheckt waren, klicken Sie auf **Eclipse Orion {{site.data.keyword.webide}}**.

   Wenn Sie während der Durchführung des Upgrades zu Ihrem Projekt zurückkehren, wird in der Bannernachricht möglicherweise angezeigt, dass das Upgrade in Bearbeitung ist, insbesondere, wenn der Upgradeprozess das Importieren von Quellcode in ein neues Repository oder das Importieren von Track &amp; Plan-Arbeitselementen als Arbeitsschritte umfasst. 

   ![Nachricht, dass für ein Projekt ein Upgrade auf eine Toolchain durchgeführt wird](images/project-being-upgraded-banner.png)

## Projekt nochmals bearbeiten
{: #revisit_projects}

Sie können jetzt Ihre neue Toolchain verwenden. Ihr Projekt ist jetzt mit der Bezeichnung 'Upgrade durchgeführt' versehen und auf der Übersichtsseite wird eine Bestätigungsnachricht angezeigt.

![Abbildung der Karte mit Bezeichnung 'Upgrade durchgeführt'](images/card-upgraded-project.png)

![Projekt mit erfolgtem Upgrade](images/banner-upgraded.png)

Durch Auswahl der Option **Projekte mit erfolgtem Upgrade** im Menü auf der Seite 'Meine Projekte' können Sie anzeigen, für welche Projekte das Upgrade bereits durchgeführt wurde:

![Abbildung des Menüelements 'Projekte mit erfolgtem Upgrade'](images/menu-upgraded-projects.png)

Falls es erforderlich ist, das Upgrade zurückzusetzen, löschen Sie die Toolchain. Sie können Ihre Toolchain im Menü **Weitere Aktionen** auf der Toolchain-Seite 'Übersicht' löschen: 

![Abbildung für die Löschaktion im Menü 'Weitere Aktionen'](images/upgrade-tutorial-delete-toolchain.png)

Wenn Sie zu Ihrem Projekt zurückkehren, wird die Upgradenachricht erneut angezeigt, und Sie können erneut ein Upgrade durchführen, wenn
Sie bereit sind. 

## Nächste Schritte
{: #upgrade_next_steps}

1. Bestätigen Sie, dass das Upgrade vollständig durchgeführt wurde. Aktualisieren Sie dazu Ihren Browser und überprüfen Sie auf der Übersichtsseite des Projekts, ob die entsprechende Nachricht, dass für Ihr Projekt ein Upgrade auf diese Toolchain durchgeführt wurde, angezeigt wird:


   ![Nachricht im Banner, dass das Upgrade für das Projekt durchgeführt wurde](images/banner-upgraded.png)

   **Hinweis:** Wenn in der Nachricht 'Jetzt Upgrade durchführen' steht, ist das Durchführen des Upgrades fehlgeschlagen. Klicken Sie auf den Link **Jetzt Upgrade durchführen**, um es erneut zu versuchen. 

   ![Nachricht im Banner, die angibt, dass das Projekt für die Durchführung eines Upgrades
bereit ist](images/banner-ready-to-upgrade.png)

2. Erteilen Sie den Mitgliedern Ihres Teams Zugriff auf die Toolchain.
    - Jedes Teammitglied muss über ein gültiges {{site.data.keyword.Bluemix_notm}}-Konto verfügen. Teammitglieder, die kein solches Konto besitzen, müssen sich entsprechend [anmelden ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/registration){:new_window}.
    - Erteilen Sie Mitgliedern der Organisation (org) Zugriff auf die Toolchain über die Toolchain-Seite 'Verwalten'. Weitere
Informationen zur Zugriffssteuerung für Toolchains finden Sie in
[Zugriff verwalten
![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){:new_window}. 
    - Wenn ein Benutzer nicht Mitglied der Organisation ist, zu der die Toolchain gehört, fügen Sie ihn über die Seite 'Organisationen
verwalten' der Organisation hinzu.
Weitere Informationen zum Verwalten von Organisationen finden Sie in
[Organisationen und Bereiche verwalten
![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](/docs/admin/orgs_spaces.html#orgsspacesusers){:new_window}. 

3. Verwenden Sie anstatt der Tools aus Ihrem {{site.data.keyword.jazzhub_short}}-Projekt die Tools aus Ihrer Toolchain. Verwenden Sie zum Bearbeiten von Code über einen Browser zum Beispiel die Web-IDE aus Ihrer Toolchain.

4. Wenn Sie {{site.data.keyword.gitrepos}} verwenden, führen Sie die Authentifizierung mithilfe eines persönlichen
Zugriffstokens oder
eines SSH-Schlüssels durch. Weitere Informationen zu SSH-Schlüsseln finden Sie in
[Persönliches Zugriffstoken oder SSH-Schlüssel für die
Authentifizierung erstellen](/docs/services/ContinuousDelivery/git_working.html#git_authentication). Um eine Authentifizierung von einem externen Git-Client über HTTPS durchzuführen, führen Sie folgende
Schritte aus: 
    1. Wechseln Sie zur [Seite 'Zugriffstoken'
![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://git.ng.bluemix.net/profile/personal_access_tokens){:new_window} in Ihren
{{site.data.keyword.gitrepos}}-Benutzereinstellungen. 
    2. Erstellen Sie ein persönliches Zugriffstoken, in dem als Bereich **api** verwendet wird. 
    3. Rufen Sie die [Seite mit dem Account
![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://git.ng.bluemix.net/profile/account){:new_window} auf und suchen
Sie Ihren für {{site.data.keyword.gitrepos}} geltenden Benutzernamen. Ihr Benutzername wird im Abschnitt für Änderungen des
Benutzernamens aufgelistet und er wird bei allen persönlichen Repositorys, die Sie erstellen, auf der ersten Seite der URL angezeigt. 
    4. Für die Authentifizierung mit {{site.data.keyword.gitrepos}} von einem externen Git-Client aus über HTTPS
verwenden Sie Ihren Benutzernamen und Ihr persönliches Zugriffstoken. 
    5. Wenn Sie das lokale Repository Ihres JazzHub Git-Repositorys wiederverwenden wollen, verweisen Sie von diesem Repository aus auf
das neue Repository in {{site.data.keyword.gitrepos}}. Wechseln Sie von einer Shell in einem Terminal aus in das Verzeichnis, in
dem das JazzHub Git-Repository geklont wird. Geben Sie den Befehl `git remote set-url` wie folgt ein:
`git remote set-url origin https://git.ng.bluemix.net/<Benutzer-ID>/<Name_des_neuen_Repositorys>` 

        **Tipp:** Verwenden Sie den Befehl `git remote -v`, um zu überprüfen, welche fernen Namen
für welche fernen URLs festgelegt sind. Der standardmäßige ferne Name lautet `origin`. Wenn Sie eine erweiterte Konfiguration
haben, lautet das Format des Befehls wie folgt: `git remote set-url <ferner_Name_der_JazzHub_Repo_verwendet>
https://git.ng.bluemix.net/<Benutzer-ID>/<Name_des_neuen_Repositorys>` 

5. Überlegen Sie nach dem Einrichten und der anfänglichen Verwendung Ihrer Toolchain, ob Sie folgende Schritte ausführen wollen,
damit sichergestellt ist, dass Ihr Projekt ausschließlich von Ihnen verwendet wird: 
    - Fügen Sie Ihrem Projektnamen ein Suffix hinzu, um anzugeben, dass es nicht verwendet werden darf. Sie können beispielsweise
`_DO_NOT_USE` (nicht verwenden) an das Ende des Projektnamens anfügen. 
    - Aktualisieren Sie die Beschreibung des Projekts, um deutlich zu machen, dass es nicht mehr verwendet wird, und fügen Sie der
Toolchain einen Verweis hinzu. 
    - Entfernen Sie die Mitglieder aus dem Projekt. 
    - Löschen Sie das Projekt, wenn Sie es nicht mehr benötigen. 

6. Optional: Um die Entwicklungsreife Ihres Projekts, die von Ihrem Team verwendeten Verfahren und die Qualität Ihrer Codebasis zu
untersuchen, fügen Sie Ihrer Toolchain IBM Cloud {{site.data.keyword.DRA_short}} hinzu. {{site.data.keyword.DRA_short}} wendet
auf DevOps-Projekte Verfahren für die
Analyse der Entwickler, des Teams und der Bereitstellung an. Weitere Informationen finden Sie in
[Einführung in {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html). 


## Fehlerbehebung
{: #upgrade_troubleshoot}

Wenn Sie Fragen oder Probleme haben, wenden Sie sich an das
[Unterstützungsforum](https://developer.ibm.com/answers/questions/ask/?smartspace=devops-services). Schließen Sie in Ihren
Forumpost die URLs für Ihr {{site.data.keyword.jazzhub_short}}-Projekt sowie Ihre
{{site.data.keyword.contdelivery_short}}-Toolchain ein und taggen Sie Ihren Post
mit dem Tag `devops-services`. 
