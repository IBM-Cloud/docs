---

copyright:
  years: 2017
lastupdated: "2017-03-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Integration von DevOps Insights mit IBM UrbanCode Deploy - Überblick
{: #uc_insights_overview}

Mit Delivery Insights, einer Komponente von {{site.data.keyword.DRA_short}}, können Sie Bereitstellungsstatistiken, Metriken und weitere Informationen zu Ihrer IBM UrbanCode Deploy-Installation anzeigen. Beispielsweise können Diagramme über den Bereitstellungszeitraum, über erfolgreiche und fehlgeschlagene Bereitstellungen angezeigt werden, die alle nach logisch gruppierten Umgebungen sortiert sind. {:shortdesc}

Wenn Sie über keine Toolchain oder keine {{site.data.keyword.DRA_short}}-Instanz verfügen, müssen Sie zunächst {{site.data.keyword.DRA_short}} einrichten:
1. Klicken Sie im {{site.data.keyword.Bluemix}}-Katalog auf **{{site.data.keyword.DRA_short}}**, wählen Sie einen Preistarif und klicken Sie auf **Erstellen**. 
1. Klicken Sie auf die Registerkarte **Verwalten** und anschließend unter **Mit Delivery Insights for UrbanCode beginnen** auf **Hier starten**. Delivery Insights erstellt im Hintergrund eine Toolchain für Ihre Organisation. Offene Toolchains sind Sammlungen von Toolintegrationen und im vorliegenden Fall sind IBM UrbanCode Deploy und {{site.data.keyword.DRA_short}} Teile der Toolchain. Weitere Informationen zu Toolchains finden Sie in [Arbeiten mit Toolchains](../ContinuousDelivery/toolchains_working.html). 
1. Führen Sie auf der Seite für die Einrichtung von Delivery Insights die Schritte zum Einrichten von DevOps Connect durch und verbinden Sie die IBM UrbanCode Deploy-Server. 
<!--  1. Set up a system to run DevOps Connect. See [prerequisites](uc_insights_prereqs.html).
  1. Download DevOps Connect, which is provided in a runnable JAR file.
  1. Copy the script from the **Delivery Insights Setup** page and run it. This command starts DevOps Connect with a token that allows it to connect to your organization on {{site.data.keyword.Bluemix}}.
  1. Connect your IBM UrbanCode Deploy servers to DevOps connect. See [Connecting IBM UrbanCode Deploy servers to Delivery Insights](uc_insights_connect_ucd.html). -->


Wenn Sie bereits über eine Toolchain verfügen, befolgen Sie die folgenden Schritte zum Hinzufügen von Delivery Insights:
1. Falls Sie das Tool {{site.data.keyword.DRA_short}} noch nicht haben, fügen Sie es zur Toolchain hinzu. 
1. Klicken Sie in der Toolchain auf das Tool {{site.data.keyword.DRA_short}}. 
1. Führen Sie auf der Seite für die Einrichtung von Delivery Insights die Schritte zum Einrichten von DevOps Connect durch und verbinden Sie die IBM UrbanCode Deploy-Server. 

Nachdem Sie Delivery Insights und DevOps Connect eingerichtet haben, können Sie Daten von IBM UrbanCode Deploy-Servern in Delivery Insights anzeigen. Weitere Informationen finden Sie in [IBM UrbanCode Deploy-Server mit Delivery Insights verbinden](uc_insights_connect_ucd.html). 

<!-- 
For questions or issues, see the [questions forum](https://developer.ibm.com/answers/?community=urbancode).
--> 

![Zwei Diagramme aus UrbanCode Insights-Demodaten](images/uc_insights_demo_data.gif)

Zu den in Delivery Insights angezeigten Informationen zählen unter anderem:

- Statistikdaten zur Bereitstellung, einschließlich Bereitstellungszeitraum und Bereitstellungsumfang im Zeitverlauf. 
- Statistikdaten zur Fehlerrate bei der Bereitstellung nach Anwendung und Umgebung. 
- Statistikdaten zur Komponentenbereitstellung, einschließlich Fehlerrate, Bereitstellungszeit und -zeitraum. 

## Systeme - Überblick

Die Topologie für Delivery Insights umfasst mindestens eine lokale Installation von IBM UrbanCode Deploy <!-- (and optionally IBM UrbanCode Release) --> und das Dienstprogramm DevOps Connect. 

Das folgende Diagramm zeigt eine typische Installation dieser Systeme. 

![Übersichtstopologie für UrbanCode Insights, einschließlich lokaler Systeme und IBM Cloud-Services](images/uc_insights_overview_topology_multi_ucd.png)

- Eine Installation von **IBM UrbanCode Deploy** stellt die Informationen zu erfolgreichen und fehlgeschlagenen Bereitstellungen für die Metriken bereit. Für IBM UrbanCode Deploy ist für die Kommunikation mit IBM Bluemix DevOps Connect ein Patch erforderlich. 

<!--
- **IBM UrbanCode Release** is an optional part of the topology. You can use the environment mappings in IBM UrbanCode Release to set logical environments for reports.

-->

- **IBM Bluemix DevOps Connect** (früher das Dienstprogramm IBM UrbanCode Sync) koordiniert die Kommunikation zwischen lokalen Installationen von IBM UrbanCode Deploy <!-- and IBM UrbanCode Release --> und von IBM gehosteten Services wie UrbanCode Insights. DevOps Connect verwendet die sichere HTTPS-Kommunikation mit den lokalen Servern und die Tokenauthentifizierung für die Bereitstellung von Daten für UrbanCode Insights. 

  DevOps Connect benötigt Plug-ins, um eine Verbindung zu den anderen Systemen in der Topologie herzustellen. 

- Als Komponente von {{site.data.keyword.DRA_short}} stellt **Delivery Insights** Metriken zur Bereitstellungsaktivität in IBM UrbanCode Deploy bereit, einschließlich Bereitstellungszeiten und Fehlerraten basierend auf verschiedenen Umgebungsgruppen. Die Autorisierung wird über {{site.data.keyword.Bluemix}}-Konten gesteuert. 
