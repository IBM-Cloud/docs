---

copyright:
  years: 2017
lastupdated: "2017-04-11"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Auf weitere Funktionen der API-Verwaltung zugreifen
{: #upgrade}

Über die API-Verwaltung können Anrufraten und die OAuth-Autorisierung gesteuert sowie Analysen angezeigt werden. Durch ein Upgrade auf den {{site.data.keyword.apiconnect_full}}-Service kann die API-Verwaltung erweitert werden. Der {{site.data.keyword.apiconnect_short}}-Service bietet mehr Auswahlmöglichkeiten bei Sicherheitsrichtlinien und eine bessere Steuerung der Ratenbegrenzungen. Darüber hinaus haben Sie die Möglichkeit, ein vollständig anpassbares Entwicklerportal zu konfigurieren, um API-Inhalte zu teilen und mit der Entwickler-Community zu kommunizieren. Weitere Vorteile:
* Lebenszyklusmanagement
* Zusammengesetzte APIs
* Web-Service-Integration
* Protokollmediation
* API-Generierung aus Schemas
* Micro-Service-Entwicklung

Die Migration auf den {{site.data.keyword.apiconnect_short}}-Service ist einfach. Die APIs, die über die API-Verwaltung gesteuert werden, müssen Sie nicht erneut erstellen.

## APIs auf {{site.data.keyword.apiconnect_short}} migrieren
{: #migrate_api}

Wenn Sie ein Upgrade auf {{site.data.keyword.apiconnect_full}} durchführen möchten, müssen Sie die APIs von der API-Verwaltung auf den {{site.data.keyword.apiconnect_short}}-Service migrieren. Führen Sie dazu für jede API die folgenden Schritte aus: 

1. Laden Sie das Swagger-Dokument für die API aus der API-Verwaltung herunter.
    1. Öffnen Sie Ihre App und wählen Sie **API-Verwaltung** aus.
	2. Wählen Sie die Registerkarte **API-Explorer** aus. Daraufhin wird eine Liste der APIs angezeigt, die sich auf das jeweilige Projekt beziehen.
    2. Laden Sie das Swagger-Dokument für die API herunter, indem Sie das Symbol neben dem Namen der API auswählen.
2. Erstellen Sie die {{site.data.keyword.apiconnect_short}}-Instanz und bereiten Sie diese vor. 
    1. Erstellen Sie eine Instanz des {{site.data.keyword.apiconnect_short}}-Service aus dem {{site.data.keyword.Bluemix_notm}}-Katalog.
	2. Wählen Sie Ihren Plan aus.
	3. Wählen Sie **+Hinzufügen** aus, um einen Katalog zu erstellen.
	4. Geben Sie einen Anzeigenamen und einen Namen für den Katalog ein und wählen Sie **Hinzufügen** aus.
	5. Wählen Sie den erstellten Katalog aus.
3. Importieren Sie das Swagger-Dokument in die {{site.data.keyword.apiconnect_short}}-Instanz. Führen Sie dazu die folgenden Schritte aus:
	1. Wählen Sie im Dashboard für den {{site.data.keyword.apiconnect_short}}-Service **Navigieren zu... (>>)** > **Entwürfe** im Menü aus.
	2. Wählen Sie Sie die API-Registerkarte aus.
	3. Wählen Sie **+Hinzufügen** > **API aus Datei oder URL importieren** aus.
	4. Suchen Sie die Swagger-Datei, die Sie aus der API-Verwaltung heruntergeladen haben, und wählen Sie sie aus. Wählen Sie **Öffnen** aus.
	5. Wählen Sie **Importieren** aus, um die API in den {{site.data.keyword.apiconnect_short}}-Service zu importieren.
4. Geben Sie Einstellungen für die API an.
    1. Wählen Sie **Produkt erstellen** aus.
	2. Wählen Sie das erstellte Produkt aus, um die zugehörigen Einstellungen anzuzeigen.
	3. Legen Sie die Ratenbegrenzung für die API fest.
	4. Legen Sie die Stufe für die API fest.
5. Fügen Sie gegebenenfalls den Endpunkt für die API hinzu.
    1. Wählen Sie die API aus.
	2. Wählen Sie die Registerkarte 'Assembly' aus.
	3. Fügen Sie den Endpunkt hinzu, sofern dieser noch nicht angegeben wurde.
	
 Nach der Migration der APIs können Sie durch Öffnen der Kachel für den {{site.data.keyword.apiconnect_short}}-Service und über das {{site.data.keyword.Bluemix_notm}}-Dashboard auf sämtliche Funktionen der API-Verwaltung zugreifen. 

 
