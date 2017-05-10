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

# Auf weitere API-Managementfunktionen zugreifen
{: #upgrade}

Das API-Management bietet die Möglichkeit, Aufrufraten und OAuth zu steuern und Analysen anzuzeigen. Sie verfügen über eine umfassendere Steuerung von APIs, wenn Sie ein Upgrade auf den {{site.data.keyword.apiconnect_full}}-Service durchführen. Der {{site.data.keyword.apiconnect_short}}-Service stellt mehr Auswahlmöglichkeiten an Sicherheitsrichtlinien und eine präzisere Steuerung der Ratenbegrenzungen bereit. Darüber hinaus haben Sie die Möglichkeit, ein vollständig anpassbares Entwicklerportal zu konfigurieren, sodass Sie APIs teilen und sich mit der Entwicklercommunity austauschen können. Weitere Vorteile sind folgende: 
* Lebenszyklusmanagement
* Zusammengesetzte APIs
* Web-Service-Integration
* Protokollmediation
* API-Generierung aus dem Schema
* Entwicklung von Microservices

Die Migration auf den {{site.data.keyword.apiconnect_short}}-Service ist einfach und Sie brauchen keine der APIs, die Sie über das API-Management verwalten, neu zu erstellen. 

## APIs auf {{site.data.keyword.apiconnect_short}} migrieren
{: #migrate_api}

Wenn Sie sich entschließen, ein Upgrade auf {{site.data.keyword.apiconnect_full}} durchzuführen, müssen Sie Ihre APIs aus dem API-Management auf den {{site.data.keyword.apiconnect_short}}-Service migrieren, indem Sie die folgenden Schritte für jede Ihrer APIs ausführen:  

1. Laden Sie das Swagger-Dokument für die API aus dem API-Management herunter. 
    1. Öffnen Sie Ihre App und wählen Sie **API Management** aus. 
	2. Wählen Sie die Registerkarte **API-Explorer** aus. Eine Liste Ihrer APIs, die zu dem entsprechenden Projekt gehören, wird angezeigt. 
    2. Laden Sie das Swagger-Dokument für Ihre API herunter, indem Sie das Symbol neben dem Namen der API auswählen. 
2. Erstellen Sie die {{site.data.keyword.apiconnect_short}}-Instanz und bereiten Sie sie vor.  
    1. Erstellen Sie eine Instanz des {{site.data.keyword.apiconnect_short}}-Service aus dem {{site.data.keyword.Bluemix_notm}}-Katalog. 
	2. Wählen Sie Ihren Plan aus. 
	3. Wählen Sie **+Hinzufügen** aus, um einen Katalog zu erstellen. 
	4. Geben Sie einen Anzeigenamen für Ihren Katalog ein und wählen Sie **Hinzufügen** aus. 
	5. Wählen Sie den Katalog aus, den Sie erstellt haben. 
3. Importieren Sie das Swagger-Dokument in Ihre {{site.data.keyword.apiconnect_short}}-Instanz, indem Sie die folgenden Schritte ausführen: 
	1. Wählen Sie im Dashboard des {{site.data.keyword.apiconnect_short}}-Service die Option **Navigieren zu... (>>)** > **Entwürfe** im Menü aus. 
	2. Wählen Sie die Registerkarte 'APIs' aus. 
	3. Wählen Sie **+Hinzufügen** > **API aus Datei oder URL importieren** aus. 
	4. Suchen Sie die Swagger-Datei, die Sie aus dem API-Management heruntergeladen haben, und wählen Sie sie aus. Wählen Sie **Öffnen** aus. 
	5. Wählen Sie **Importieren** aus, um Ihre API in den {{site.data.keyword.apiconnect_short}}-Service zu importieren. 
4. Geben Sie Einstellungen für Ihre API an. 
    1. Wählen Sie **Produkt erstellen** aus. 
	2. Wählen Sie das Produkt aus, das Sie zum Anzeigen der zugehörigen Einstellungen erstellt haben. 
	3. Legen Sie die Ratenbegrenzung für die API fest. 
	4. Legen Sie die Stufe (Tier) für die API fest. 
5. Fügen Sie den Endpunkt für die API hinzu, falls erforderlich. 
    1. Wählen Sie die API aus. 
	2. Wählen Sie die Registerkarte 'Assemblierung' aus. 
	3. Fügen Sie den Endpunkt hinzu, wenn er noch nicht angegeben ist. 
	
 Nach der Migration Ihrer APIs können Sie auf alle API-Management-Funktionen zugreifen, indem Sie die Kachel für den {{site.data.keyword.apiconnect_short}}-Service öffnen. Darüber hinaus ist der Zugriff über das {{site.data.keyword.Bluemix_notm}}-Dashboard möglich.  

 
