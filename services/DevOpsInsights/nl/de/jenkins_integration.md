---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.DRA_short}} mit Jenkins integrieren
{: #toolchain_configure_jenkins}

Der nächste Schritt nach der Definition der Richtlinien für die {{site.data.keyword.DRA_full}}-Überwachung ist das Hinzufügen von {{site.data.keyword.DRA_short}} zu einer Toolchain; anschließend wird eine Continuous Delivery-Pipeline konfiguriert.
{:shortdesc}

<!--##Configuring a Jenkins project-->

Sie können {{site.data.keyword.DRA_short}} in ein Jenkins-Projekt oder in mehrere zugehörige Jenkins-Projekte integrieren. Dies ermöglicht Ihnen das Festlegen von Qualitätsgates sowie das Empfangen von Buildqualitätsdaten im {{site.data.keyword.DRA_short}}-Dashboard.

##Voraussetzungen    
{: #DI_jenkins_prereqs}

* Sie müssen über Zugriff auf ein lokales Jenkins-Projekt oder auf den Server, auf dem das Jenkins-Projekt ausgeführt wird, verfügen.

##{{site.data.keyword.DRA_short}}-Plug-in installieren
{: #DI_jenkins_install}

Führen Sie zur Installation des {{site.data.keyword.DRA_short}}-Plug-ins in Ihrem Jenkins-Projekt die folgenden Schritte aus:

  1. [Laden Sie die Installationsdatei für das IBM DevOps Insight-Plug-in (.hpi)](https://github.ibm.com/oneibmcloud/DRA-Jenkins/blob/hpi-release/target/dra.hpi) aus dem GitHub-Repository des Plug-ins herunter.
  2. Klicken Sie in Ihrer Jenkins-Installation auf **Manage Jenkins**, wählen Sie **Manage Plugins** aus und klicken Sie auf die Registerkarte **Advanced**.
  3. Klicken Sie auf **Choose File** und wählen Sie die Installationsdatei für das DevOps Insight-Plug-in aus.
  4. Klicken Sie auf **Upload**.
  5. Starten Sie Jenkins erneut und prüfen Sie, ob das Plug-in installiert wurde.

##{{site.data.keyword.DRA_short}} mit Jenkins integrieren    
{: #DI_jenkins_integrate}

Rufen Sie nach der Plug-in-Installation, aber vor der Integration von {{site.data.keyword.DRA_short}} in Ihre Jenkins-Installation das [Control Center](https://control-center.stage1.ng.bluemix.net/) auf und erstellen Sie mindestens eine Richtlinie.

Gehen Sie für Ihre bereits vorhandenen Jobs, in denen Sie {{site.data.keyword.DRA_short}} nutzen möchten, wie folgt vor:

1. Fügen Sie eine Buildabschlussaktion des Typs **Publish build information to {{site.data.keyword.DRA_short}}**, **Publish deployment information to {{site.data.keyword.DRA_short}}** oder **Publish test result to {{site.data.keyword.DRA_short}}** hinzu. Der jeweilige Typ muss mit dem Jobtyp übereinstimmen (erstellen, bereitstellen oder testen). Füllen Sie die erforderlichen Felder aus.
  * Wählen Sie im Feld mit den Berechtigungsnachweisen Ihre Bluemix-ID und das zugehörige Kennwort aus. Sind diese nicht in Jenkins gespeichert, klicken Sie auf die Option zum Hinzufügen, um sie hinzuzufügen und zu speichern.
  * Geben Sie im Feld für den Namen des Build-Jobs den Namen Ihres Build-Jobs genau wie in Jenkins an. Lassen Sie dieses Feld leer, wenn der Build-Job zeitlich mit dem Testjob zusammenfällt. Wenn es außerhalb von Jenkins zu dem Build-Job kommt, wählen Sie die Option **Builds are being done outside of Jenkins** aus und geben Sie die Buildnummer und die Build-URL an.
  * Geben Sie den Speicherort der Ergebnisdatei im entsprechenden Feld an. Wenn durch den Test keine Ergebnisdatei generiert wird, lassen Sie dieses Feld leer. Durch das Plug-in wird eine auf dem Status des aktuellen Testjobs basierende Standardergebnisdatei hochgeladen.
3. *Optional*: Wenn Sie möchten, dass die DRA-Richtliniengates im Testjob den nachfolgenden Bereitstellungsjob steuern, fügen Sie eine weitere Buildabschlussaktion des Typs **DevOps Risk Analytics Gate** hinzu und füllen Sie die erforderlichen Felder aus. Das Gate verhindert, dass der nachfolgende Job ausgeführt wird, wenn der Testjob die zugeordneten Richtlinien nicht erfüllen kann.
4. Klicken Sie auf die Option zum Anwenden und anschließend auf die Option zum Speichern.

Sie können auf der Projektseite auf die Option zum unmittelbaren Erstellen klicken, um das Projekt auszuführen.

Rufen Sie nach der Buildausführung das [Control Center](https://control-center.stage1.ng.bluemix.net/) auf, um Ihren Buildstatus im Dashboard zu überprüfen. Haben Sie Richtliniengates konfiguriert, können Sie auf der Statusseite des aktuellen Builds auch {{site.data.keyword.DRA_short}}-Ergebnisse sehen.
