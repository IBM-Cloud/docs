---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-21"

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Upgrade Ihres {{site.data.keyword.jazzhub_short}}-Projekts zu einer Toolchain durchführen
{: #upgrade_projects}

Aus {{site.data.keyword.jazzhub}} wird künftig {{site.data.keyword.contdelivery_full}}. Als Teil dieser Änderungen wird für Projekte ein Upgrade zu Toolchains durchgeführt.  

Sie können ein Upgrade für Ihr Projekt durchführen oder warten, bis das Upgrade automatisch vorgenommen wird. Die optimale Benutzererfahrung ergibt sich, wenn Sie für Ihr Projekt so bald wie möglich das Upgrade durchführen, damit Sie steuern können, wie der Name Ihrer Toolchain lautet und in welcher Organisation sie erstellt wird.   
{: shortdesc}

## Toolchains
{: #compare_toolchains}

Toolchains ähneln Projekten, weisen jedoch einige wichtige Unterschiede auf: 

- Projekte können nur über ein Repository (repo) und eine Pipeline verfügen. Toolchains können so viele Repositorys und Pipelines besitzen wie nötig. 
- Toolchains können Tools enthalten, die in Projekten nicht verfügbar sind, wie zum Beispiel Slack, Sauce Labs, PagerDuty und {{site.data.keyword.DRA_full}}. 
- Der Zugriff auf Toolchains wird über standardmäßige Bluemix-Organisationen verwaltet. Die Mitgliedschaft wird auf Organisationsebene gepflegt, wohingegen bei Projekten die Pflege von Mitgliedschaften auf Projektebene erfolgt. 

Mehr zu Toolchains erfahren Sie in [YouTube![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://youtu.be/2SIPE1e7NJ4){: new_window} oder in der [Einführung in {{site.data.keyword.contdelivery_short}}](/docs/services/ContinuousDelivery/index.html).
[![Externer Link zu YouTube](images/CD_video.png)](https://youtu.be/2SIPE1e7NJ4){: new_window}    

## Voraussetzungen
{: #upgrade_prereqs}    

- Für den Zugriff auf die Toolchain Ihres aktualisierten Projekts benötigen Sie eine Bluemix-ID. Vor der Durchführung des Upgrades müssen Sie daher sicherstellen, dass Sie über eine aktive Bluemix-ID verfügen. Sollte das nicht der Fall sein, müssen Sie sich [anmelden](https://console.ng.bluemix.net/registration/). 
- Stellen Sie sicher, dass die Angabe für Ihren DevOps Services-Projekteigner korrekt ist. Die Toolchain, die auf der Grundlage Ihres Projekts erstellt wird, ist künftig Teil der Bluemix-Organisation dieses Eigners. 

**Wichtig:** Die Eclipse Orion-{{site.data.keyword.webide}} in der Toolchain funktioniert gesondert von der {{site.data.keyword.webide}}, die Ihrem Projekt zugeordnet ist. Wenn Sie die {{site.data.keyword.webide}} verwenden und nicht festgeschriebene Änderungen vorliegen, führen Sie einen Commit für diese Änderungen aus, bevor Sie das Upgrade durchführen.   


## Upgrade eines Projekts zu einer Toolchain durchführen
{: #project_to_toolchain}

Wenn Ihr Projekt bereit für das Upgrade ist, wird eine Nachricht auf der Karte des Projekts und auf seiner Übersichtsseite angezeigt. 

![Abbildung der Karte mit Bezeichnung 'Bereit für Upgrade'](images/card-project-to-upgrade.png)

![Nachricht 'Es ist an der Zeit für das Upgrade'](images/banner-ready-to-upgrade.png)

**Tipp:** Im Menü auf der Seite 'Meine Projekte' finden Sie Projekte, die bereit für das Upgrade sind:  

![Abbildung des Menüelements 'Projekte für Upgrade'](images/menu-projects-to-upgrade.png)

## Upgradeprozess starten
{: #start_upgrade}

Bevor Sie den Upgradeprozess starten, können Sie ihn sich auf [YouTube![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://youtu.be/oaZVGveVxBg){: new_window} in Aktion ansehen.
[![Externer Link zu YouTube](images/migration-video2.png)](https://youtu.be/oaZVGveVxBg){: new_window}    
Führen Sie die folgenden Schritte aus, um für Ihr Projekt das Upgrade zu einer Toolchain durchzuführen: 

1. Starten Sie den Upgradeprozess. Klicken Sie dazu in der Bannernachricht auf **Jetzt Upgrade durchführen**. Die Seite für das Upgrade des Projekts zu einer Toolchain wird angezeigt.  

   ![Beispiel für eine Upgradeseite](images/project-upgrade-toolchain.png)

   Einen Überblick über den Upgradeprozess können Sie sich verschaffen, indem Sie die Beschreibung auf dieser Seite lesen. Da das Projekt ein Repository bei GitHub.com verwendet, wird die Toolchain im vorliegenden Fall mit demselben GitHub-Repository verbunden. Die Toolchain wird eine neue Pipeline enthalten, die dieselben Stages und Jobs wie die Pipeline des Projekts enthält. Außerdem enthält die Toolchain einen Verweis auf die Eclipse Orion-{{site.data.keyword.webide}}, die in {{site.data.keyword.contdelivery_short}} ausgeführt wird. 

2. Durch Konfigurieren einiger Einstellungen können Sie die Toolchain anpassen: 

   - Wenn Sie den Namen der Toolchain ändern wollen, bearbeiten Sie das Feld **Name**. 

      ![Feld 'Name'](images/name-change.png)

   - Wenn Sie ändern wollen, in welcher {{site.data.keyword.Bluemix_notm}}-Organisation die Toolchain erstellt wird, wählen Sie die gewünschte Organisation im Menü Ihres Kontos aus: 

      ![Auswahlfunktion für Bluemix-Organisation](images/bluemix-organization-chooser.png)

   Da die Verwaltung von Toolchains auf Organisationsebene erfolgt, müssen Sie unbedingt eine Organisation auswählen, bei der die Projektmitglieder, die Zugriff auf die Toolchain benötigen, entweder bereits vorhanden sind oder aber hinzugefügt werden können.  
  
3. Klicken Sie auf **Erstellen**. Die neue Toolchain wird erstellt und ihre Übersichtsseite wird angezeigt. 

   ![Übersicht über die Toolchain, für die das Upgrade durchgeführt wurde](images/new-toolchain-page.png)

   - Wenn Sie auf Ihr GitHub-Repository oder den Tracker für zugehörige Probleme zugreifen wollen, klicken Sie auf **GitHub** oder auf **Probleme**. 
   
   - Wenn Sie auf die Pipeline zugreifen wollen, klicken Sie auf **Delivery Pipeline**.   
   
   - Wenn Sie auf die {{site.data.keyword.webide}} zugreifen wollen, die diejenigen Inhalte Ihres Repositorys enthält, die in den Arbeitsbereich ausgecheckt waren, klicken Sie auf **Eclipse Orion {{site.data.keyword.webide}}**.  

## Projekt nochmals bearbeiten
{: #revisit_projects}

Sie können jetzt Ihre neue Toolchain verwenden. Ihr Projekt ist jetzt mit der Bezeichnung 'Upgrade durchgeführt' versehen und auf der Übersichtsseite wird eine Bestätigungsnachricht angezeigt. 

![Abbildung der Karte mit Bezeichnung 'Upgrade durchgeführt'](images/card-upgraded-project.png)

![Projekt mit erfolgtem Upgrade](images/banner-upgraded.png)

Durch Auswahl der Option **Projekte mit erfolgtem Upgrade** im Menü auf der Seite 'Meine Projekte' können Sie anzeigen, für welche Projekte das Upgrade bereits durchgeführt wurde: 

![Abbildung des Menüelements 'Projekte mit erfolgtem Upgrade'](images/menu-upgraded-projects.png)

Falls es erforderlich ist, das Upgrade zurückzusetzen, löschen Sie die Toolchain. Wenn Sie danach zur Übersichtsseite des betreffenden Projekts zurückkehren, wird wieder die Upgradenachricht angezeigt und Sie können das Upgrade erneut durchführen, wenn Sie dazu bereit sind. 

## Nächste Schritte
{: #upgrade_next_steps}   

1. Bestätigen Sie, dass das Upgrade vollständig durchgeführt wurde. Überprüfen Sie dazu auf die Übersichtsseite des Projekts, ob die entsprechende Nachricht angezeigt wird:     

   ![Projekt mit erfolgtem Upgrade](images/banner-upgraded.png)    

2. Erteilen Sie den Mitgliedern Ihres Teams Zugriff auf die Toolchain.     
    - Jedes Teammitglied muss über ein gültiges Bluemix-Konto verfügen. Teammitglieder, die kein solches Konto besitzen, müssen sich entsprechend [anmelden ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/registration){:new_window}. 
    - Fügen Sie Teammitglieder zu der Organisation (org) hinzu, zu der die Toolchain gehört. 
3. Verwenden Sie anstatt der Tools aus Ihrem {{site.data.keyword.jazzhub_short}}-Projekt die Tools aus Ihrer Toolchain. Verwenden Sie zum Bearbeiten von Code über einen Browser zum Beispiel die Web-IDE aus Ihrer Toolchain.     

## Fehlerbehebung
{: #upgrade_troubleshoot}    

Falls Sie Fragen haben oder Probleme ansprechen möchten, senden Sie eine entsprechende E-Mail-Nachricht an [hub@jazz.net](mailto:hub@jazz.net). Geben Sie in der E-Mail-Nachricht die URLs zu Ihrem {{site.data.keyword.jazzhub_short}}-Projekt und zu Ihrer {{site.data.keyword.contdelivery_short}}-Toolchain an. 

