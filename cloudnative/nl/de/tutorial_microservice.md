---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Umfassendes Lernprogramm zum Microservice-Basis-Starter (Microservice Basic Starter)
{: #tutorial}

Das folgende umfassende Lernprogramm führt Sie durch die Schritte zur Erstellung eines Projekts aus dem Microservice-Basis-Starter, inklusive der Tools, die Sie installiert haben müssen, sowie durch die Schritte zum Ausführen des Projektcodes. 

## Entwicklertools installieren
{: #dev_tools}

Stellen Sie sicher, dass die [vorausgesetzten Entwicklertools ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](get_code.html#prereq-dev-tools){: new_window} installiert sind.


## Projekt mit der {{site.data.keyword.dev_console}} erstellen
{: #create-devex}

1. Erstellen Sie ein Projekt in der {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}. 

	1. Klicken Sie auf der Seite **Einführung** in der {{site.data.keyword.dev_console}} auf **Projekt erstellen**.

		Alternativ können Sie auf der Seite **Projekte** auf **Projekt erstellen** klicken.

	2. Wählen Sie **Microservice** aus und klicken Sie auf **Weiter**. 

	3. Wählen Sie **Basis** aus und klicken Sie auf **Weiter**. 

	4. Geben Sie Ihren Projektnamen ein. Verwenden Sie für dieses Lernprogramm `MicroserviceProject`.   

	5. Geben Sie einen Hostnamen ein. Verwenden Sie für dieses Lernprogramm `devhost`.  
   
	6. Klicken Sie auf **Erstellen**.

2. Optional: Fügen Sie die Data-Funktion hinzu.

	1. Klicken Sie auf der Seite **Projektübersicht** für **Data** auf **Anzeigen**.

      Alternativ können Sie **Erstellen** oder **Vorhandenen hinzufügen** auf der Seite **Funktionen > Data** aus. 

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.

3. Generieren Sie den Projektcode.

	1. Klicken Sie auf der Seite **Projektübersicht** auf **Code abrufen**, um Ihre Sprache auszuwählen. 
   
		Alternativ können Sie auf die Seite **Code** klicken.
      
	2. Klicken Sie auf **Code generieren**. 
   
	3. Wenn die Projektcodegenerierung fertig ist, klicken Sie auf **Code herunterladen**, um Ihr Projektarchiv herunterzuladen.

4. Optional: [Aktualisieren Sie das Projekt](project_overview_page.html#update_language), um eine neue Sprache zu generieren. 


## Projekt mit dem {{site.data.keyword.dev_cli_notm}} erstellen
{: #create-cli}

1. Stellen Sie sicher, dass das [{{site.data.keyword.dev_cli_short}}](dev_cli.html) installiert ist. 

2. Navigieren Sie in der Eingabeaufforderung des Terminals zu einem lokalen Verzeichnis Ihrer Wahl und führen Sie den folgenden Befehl aus. 
  
	```
	bx dev create
	```
	{: codeblock}

3. Geben Sie bei Aufforderung die folgenden Werte an: 

	* Wählen Sie ein Muster aus: 4 (für Microservices)
	* Wählen Sie einen Starter aus: 1 (für Basis)
	* Wählen Sie eine Plattform aus: 3 (für Java)
	* Geben Sie einen Namen für Ihr Projekt ein: `MicroserviceProjectCLI`

4. Wenn Sie Services zu Ihrem Projekt hinzufügen möchten, geben Sie `y` ein, wenn Sie in der Eingabeaufforderung danach gefragt werden, und beantworten Sie die restlichen Fragen. 

5. Navigieren Sie nach dem erfolgreichen Speichern des Projekts `MicroserviceProjectCLI` zum Ordner `MicroserviceProjectCLI`. 

6. Zu diesem Zeitpunkt können Sie eigenen Code zum Projekt hinzufügen oder das Projekt erstellen bzw. ausführen. 
 
 
## Projekt mit dem {{site.data.keyword.dev_cli_notm}} ausführen
{: #running-dev-plugin}

1. Geben Sie zum Erstellen des Projekts im aktuellen Projektverzeichnis den folgenden Befehl ein: 

	```
	bx dev build
	```     
	{: codeblock}

2. Geben Sie zum Erstellen und Ausführen des Projekts im aktuellen Projektverzeichnis den folgenden Befehl ein: 

	```
	bx dev run
	```
	{: codeblock}	

3. Sie können mithilfe von curl auf die Anwendung auf dem Server zugreifen: 

	```
	curl http://localhost:8080	
	```
	{: codeblock}
