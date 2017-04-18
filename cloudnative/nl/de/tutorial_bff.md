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

# Umfassendes Lernprogramm zum BFF-Basis-Starter (BFF Basic Starter)
{: #tutorial}

Das folgende umfassende Lernprogramm führt Sie durch die Schritte zur Erstellung eines Projekts aus dem BFF-Basis-Starter, inklusive der Tools, die Sie installiert haben müssen, sowie durch die Schritte zum Ausführen des Projektcodes. 

## Entwicklertools installieren
{: #dev_tools}

Stellen Sie sicher, dass die [vorausgesetzten Entwicklertools ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](get_code.html#prereq-dev-tools){: new_window} installiert sind.


## Projekt mit der {{site.data.keyword.dev_console}} erstellen
{: #create-devex}

1. Erstellen Sie ein Projekt in der {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}. 

	1. Klicken Sie auf der Seite **Einführung** in der {{site.data.keyword.dev_console}} auf **Projekt erstellen**.

		Alternativ können Sie auf der Seite **Projekte** auf **Projekt erstellen** klicken.

	2. Wählen Sie **Backend for Frontend** aus und klicken Sie auf **Weiter**. 

	3. Wählen Sie die Auswahlmöglichkeit für ein Basis-Backend**** aus und klicken Sie auf **Weiter**. 

	4. Geben Sie Ihren Projektnamen ein. Verwenden Sie für dieses Lernprogramm `BFFProject`.    

	5. Geben Sie einen Hostnamen ein. Verwenden Sie für dieses Lernprogramm `devhost`.  

	6. Wählen Sie Ihre Sprachplattform aus. Verwenden Sie für dieses Lernprogramm `Node`. 
   
	7. Klicken Sie auf **Erstellen**.

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

	* Wählen Sie ein Muster aus: 3 (für Backend for Frontend)
	* Wählen Sie einen Starter aus: 1 (für Basis-Backend)
	* Wählen Sie eine Sprache aus: 1 (für Node)
	* Geben Sie einen Namen für Ihr Projekt ein: `BFFProjectCLI`
	* Geben Sie einen Hostnamen für Ihr Projekt ein: `myhost`

4. Wenn Sie Services zu Ihrem Projekt hinzufügen möchten, geben Sie `y` ein, wenn Sie in der Eingabeaufforderung danach gefragt werden, und beantworten Sie die restlichen Fragen. 

5. Navigieren Sie nach dem erfolgreichen Speichern des Projekts `BFFProjectCLI` zum Ordner `BFFProjectCLI`. 

6. Zu diesem Zeitpunkt können Sie eigenen Code zum Projekt hinzufügen oder das Projekt erstellen bzw. ausführen. 
 
	1. Erstellen Sie das Projekt mit dem folgenden Befehl: 
   
		```
		bx dev build
		```     
		{: codeblock}
  
	2. Führen Sie das Projekt mit dem folgenden Befehl aus: 

 		```
		bx dev run
		```
		{: codeblock}


## Ein BFF-Projekt ausführen
{: #running-bff}

### Lokal
{: #bff-local}

1. Kompilieren Sie den Server: 

  ```
  swift build
  ```
  {: codeblock}

2. Führen Sie die Anwendung aus. Beispiel: Die Anwendung weist den Namen `MyServer` auf: 

  ```
  .build/debug/MyServer
  ```
  {: codeblock}

3. Sie können curl auf dem Server mit `curl http://localhost:8080` ausführen. 


### Bluemix Plug-in verwenden
{: #using-blumix}

1. Führen Sie die Kompilierung aus. 

	```
	bx dev run
	```
	{: codeblock}

2. Sie können curl auf dem Server mit dem folgenden Befehl ausführen:  
  
	```
	curl http://localhost:8080
	```
	{: codeblock}
