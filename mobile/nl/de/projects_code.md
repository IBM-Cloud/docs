---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Code-Starter zur Erstellung eines Projekts verwenden
{: #projects_code}

Sie können einen [Code-Starter](starters.html#Code_Starter) in einem {{site.data.keyword.Bluemix}} Mobile-Dashboard verwenden, um ein Projekt in der {{site.data.keyword.Bluemix_notm}}-Umgebung zu erstellen. Dieses Verfahren ist nicht auf Projekte anwendbar, die Benutzerschnittstellenstarter verwenden. Anweisungen zu Benutzerschnittstellenstartern finden Sie unter [Projekt mit einem Benutzerschnittstellenstarter erstellen](projects_ui.html). 
{:shortdesc}

Führen Sie die folgenden Schritte aus, um ein Projekt mit einem Code-Starter zu erstellen:

1. Erstellen Sie ein neues Mobile-Dashboard-Projekt in {{site.data.keyword.Bluemix_notm}}.

 Nachdem Sie den Mobile-Katalog ausgewählt haben, starten Sie mit der Registerkarte *Einführung*. Diese enthält Beschreibungen von ausgewählten Startern, die Sie verwenden können, sowie unterschiedliche Methoden zur Erstellung von Projekten, je nachdem, wie viel Hilfe Sie benötigen. Wenn Sie einfach anfangen wollen, wählen Sie **Projekt erstellen** aus.

 Wenn Sie bereits über Projekte verfügen, können Sie auch mit der ausgewählten Registerkarte *Projekte* anfangen. Im {{site.data.keyword.Bluemix_notm}} Mobile-Dashboard können Sie in der Ansicht **Projekte** ein Projekt auswählen, mit dem Sie arbeiten möchten, über *Aktionen* ein Projekt löschen oder den Code dafür herunterladen oder ein neues Projekt erstellen.

	1. Wählen Sie in der {{site.data.keyword.Bluemix_notm}}-Konsole **Mobile** aus, nachdem Sie das Menü mit den drei Zeilen neben dem {{site.data.keyword.Bluemix_notm}}-Logo erweitert haben. 
	
	2. Wählen Sie **Projekt erstellen** aus. 

	  Alternativ können Sie die Registerkarte **Projekte** auswählen, um die Projekte anzuzeigen, die bereits in Ihrer mobilen Umgebung vorhanden sind, und neue Projekte erstellen, indem Sie auf **Projekt erstellen** klicken.

	3. Klicken Sie auf **Code-Starter**.  

	4. Wählen Sie den Starter aus, der dem Typ der Anwendung, die Sie erstellen möchten, am meisten entspricht, und wählen Sie **Projekt erstellen** aus. Es gibt **Benutzerschnittstellenstarter** und **Code-Starter**. Unter [Starter](starters.html) finden Sie weitere Informationen zu Startern und ihrer Verwendung. 
	
	5. Geben Sie einen Namen für Ihr Projekt ein und wählen Sie **Erstellen** aus.
	
2. Treffen Sie Ihre Auswahlen in der Anzeige **Projektübersicht**.  In der Anzeige **Projektübersicht** werden Informationen zu Ihrem Projekt und den optionalen Services angezeigt, die Sie Ihrem Projekt hinzufügen können, z. B. {{site.data.keyword.mobilepushshort}} und Authentication.  

	1. Optional: Wählen Sie **Hinzufügen** aus, um Ihrem Projekt einen der aufgelisteten Services hinzuzufügen. Bearbeiten Sie **Servicename** für Ihren Service und klicken Sie auf **Erstellen**. Wenn Sie Ihrem Projekt Services hinzufügen, erstellen Sie eine Verknüpfung mit der {{site.data.keyword.Bluemix_notm}}-Seite für diesen Service. Konfigurieren Sie den Service durch Bereitstellen der Informationen, die für den Service erforderlich sind.
	
	2. Optional: Wiederholen Sie Schritt *a* für alle zusätzlichen Leistungsmerkmale, die Sie Ihrem Projekt hinzufügen möchten.

3. Optional: Wählen Sie **Daten** aus, um eine Cloudant NoSQL-Datenbank oder einen Object Storage-Service zu verbinden.
	1. Klicken Sie auf **Erstellen**, um eine neue Cloudant NoSQL-Datenbank oder einen Object Storage-Service zu konfigurieren.
	
	Hinweis: Wenn Sie eine Instanz des Object Storage-Service erstellen, werden Sie außerhalb des Projekts durch den Erstellungsvorgang und durch das Hinzufügen der erforderlichen Berechtigungsnachweise geführt. Navigieren Sie nach dem Erstellen zurück zum Projekt und wählen Sie **Vorhandenen hinzufügen** aus, um den Service mit dem Projekt zu verbinden.
	
	Wenn bereits eine Instanz vorhanden ist, die nicht mit einem anderen Projekt verbunden ist, und die Sie mit diesem Projekt verbinden möchten, wählen Sie **Vorhandene hinzufügen** aus. 
	
	2. Vergewissern Sie sich, dass die Kachel der Cloudant NoSQL-Datenbank oder des Object Storage-Service, zu der bzw. dem Sie eine Verbindung hergestellt haben, auf der Datenregisterkarte Ihres Projekts angezeigt wird.

4.  Laden Sie Ihr Projekt herunter und vervollständigen Sie die Einrichtung.

    1. Klicken Sie auf **Code herunterladen** und wählen Sie Ihre bevorzugte Sprache aus.
   
    2. Extrahieren Sie das Archiv und zeigen Sie die `README.md`-Datei in einem Markdown-Viewer an, um die Einrichtung zu beenden.

5.  Testen Sie Ihre App. 


