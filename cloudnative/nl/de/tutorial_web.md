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

# Umfassendes Lernprogramm zum Web-Basis-Starter (Web Basic Starter)
{: #tutorial}

Das folgende umfassende Lernprogramm führt Sie durch die Schritte zur Erstellung eines Projekts aus dem Web-Basis-Starter, inklusive der Tools, die Sie installiert haben müssen, sowie durch die Schritte zum Ausführen des Projektcodes. 

## Entwicklertools installieren
{: #dev_tools}

Stellen Sie sicher, dass die [vorausgesetzten Entwicklertools ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](get_code.html#prereq-dev-tools){: new_window} installiert sind.


## Projekt mit der {{site.data.keyword.dev_console}} erstellen
{: #create-devex}

1. Erstellen Sie ein Projekt in der {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}. 

	1. Klicken Sie auf der Seite **Einführung** in der {{site.data.keyword.dev_console}} auf **Projekt erstellen**.

		Alternativ können Sie auf der Seite **Projekte** auf **Projekt erstellen** klicken.

	2. Wählen Sie **Web-App** aus und klicken Sie auf **Weiter**. 

	3. Wählen Sie **Basic Web** aus und klicken Sie auf **Weiter**. 

	4. Geben Sie Ihren Projektnamen ein. Verwenden Sie für dieses Lernprogramm `WebBasicProject`.    

	5. Geben Sie einen Hostnamen ein. Verwenden Sie für dieses Lernprogramm `devhost`.  

	6. Wählen Sie Ihre Sprachplattform aus. Verwenden Sie für dieses Lernprogramm `Swift`.
   
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

	* Wählen Sie ein Muster aus: 1 (für Web)
	* Wählen Sie einen Starter aus: 1 (für Basic Web)
	* Wählen Sie eine Sprache aus: 2 (für Swift)
	* Geben Sie einen Namen für Ihr Projekt ein: `WebBasicProjectCLI`
	* Geben Sie einen Hostnamen für Ihr Projekt ein: `myhost`

4. Wenn Sie Services zu Ihrem Projekt hinzufügen möchten, geben Sie `y` ein, wenn Sie in der Eingabeaufforderung danach gefragt werden, und beantworten Sie die restlichen Fragen. 

5. Navigieren Sie nach dem erfolgreichen Speichern des Projekts `WebBasicProjectCLI` zum Ordner `WebBasicProjectCLI`. 

6. Fügen Sie eigenen Code hinzu, erstellen Sie das Projekt und führen Sie es aus. 
 
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


## Ein Webprojekt ausführen
{: #run}

### Lokal
{: #local notoc}

1. Installieren Sie Ihre Knotenabhängigkeiten: 

  ```
  npm install
  ```
  {: codeblock}

2. Bündeln Sie den Front-End-Code in einem Modul: 

  ```
  node_modules/.bin/gulp
  ```
  {: codeblock}

3. Kompilieren Sie den Server: 

  ```
  swift build
  ```
  {: codeblock}

4. Führen Sie die Anwendung aus: 

  ```
  .build/debug/WebBasicProjectCLI
  ```
  {: codeblock}

5. Öffnen Sie im Browser `http://localhost:8080`. 


### {{site.data.keyword.dev_cli_short}} verwenden
{: #dev notoc}

1. Installieren Sie die Knotenabhängigkeiten: 

  ```
  npm install
  ```
  {: codeblock}

2. Bündeln Sie den Front-End-Code in einem Modul: 

  ```
  gulp
  ```
  {: codeblock}

3. Führen Sie die Kompilierung aus: 

  ```
  bx dev run
  ```
  {: codeblock}

4. Öffnen Sie im Browser `http://localhost:8080`. 


## Eigenes Projekt in Xcode ausführen
{: #Xcode}

1. Erstellen Sie ein Xcode-Projekt. 

	Damit Sie mit der Entwicklung in Xcode beginnen können, müssen Sie mit dem Paketmanager für Swift ein Xcode-Projekt erstellen. 
	
	```
	swift project generate-xcodeproj
	```
	{: codeblock}

2. Ändern Sie das aktive Ziel in die ausführbare Datei: 

	Öffnen Sie anschließend das Projekt in Xcode und stellen Sie sicher, dass das aktuelle Ziel die ausführbare Datei ist. Sie können die Optionstaste gedrückt halten, während Sie auf das Dropdown-Menü klicken, um die gewünschte ausführbare Datei auszuwählen. 

3. Klicken Sie auf **Ausführen**. 

4. Öffnen Sie im Browser `http://localhost:8080`. 

