---

copyright:
  years: 2016
lastupdated: "2016-10-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Projekt mit einem Benutzerschnittstellenstarter erstellen
{: #projects_ui}

Letzte Aktualisierung: 13. Oktober 2016
{: .last-updated}

Sie können einen Benutzerschnittstellenstarter in einem {{site.data.keyword.Bluemix}} Mobile-Dashboard verwenden, um ein Projekt in der {{site.data.keyword.Bluemix_notm}}-Umgebung zu erstellen. Dieses Verfahren ist nicht auf Projekte anwendbar, die Code-Starter verwenden. Anweisungen zu Code-Startern finden Sie unter [Projekt mit einem Code-Starter erstellen](projects_code.html).
{:shortdesc}

Führen Sie die folgenden Schritte aus, um ein Projekt mit einem Benutzerschnittstellenstarter zu erstellen:

1. Erstellen Sie ein neues Mobile-Dashboard-Projekt in {{site.data.keyword.Bluemix_notm}}.

 Nachdem Sie den Mobile-Katalog ausgewählt haben, starten Sie mit der Registerkarte *Einführung*. Diese enthält Beschreibungen von ausgewählten Startern, die Sie verwenden können, sowie unterschiedliche Methoden zur Erstellung von Projekten, je nachdem, wie viel Hilfe Sie benötigen. Wenn Sie mit minimaler Hilfestellung einfach anfangen wollen, wählen Sie **Projekt erstellen** aus.

 Wenn Sie bereits über Projekte verfügen, können Sie die Registerkarte *Projekte* öffnen, während Sie sich in der Registerkarte *Einführung* befinden. Im {{site.data.keyword.Bluemix_notm}} Mobile-Dashboard können Sie in der Ansicht **Projekte** ein Projekt auswählen, mit dem Sie arbeiten möchten, über *Aktionen* ein Projekt löschen oder den Code dafür herunterladen oder ein neues Projekt erstellen. Wenn das Projekt über einen Benutzerschnittstellenstarter gestartet wurde, können Sie das Projekt im Benutzerschnittstellenbuilder direkt über das Menü *Aktionen* öffnen. 

	1. Wählen Sie in der {{site.data.keyword.Bluemix_notm}}-Konsole **Mobile** aus, nachdem Sie das Menü mit den drei Zeilen neben dem {{site.data.keyword.Bluemix_notm}}-Logo erweitert haben. 
	
	2. Wählen Sie **Projekt erstellen** aus. 

	  Alternativ können Sie die Registerkarte **Projekte** auswählen, um die Projekte anzuzeigen, die bereits in Ihrer mobilen Umgebung vorhanden sind, und neue Projekte erstellen, indem Sie auf **Projekt erstellen** klicken. 

	3. Wählen Sie den Starter aus, der dem Typ der Anwendung, die Sie erstellen möchten, am meisten entspricht, und wählen Sie **Projekt erstellen** aus. Es gibt **Benutzerschnittstellenstarter** und **Code-Starter**. Unter [Starter](starters.html) finden Sie weitere Informationen zu Startern und ihrer Verwendung. 
	
	4. Geben Sie einen Namen für Ihr Projekt ein und wählen Sie **Erstellen** aus.
	
2. Treffen Sie Ihre Auswahlen in der Anzeige **Projektübersicht**. In der Anzeige **Projektübersicht** werden Informationen zu Ihrem Projekt und den optionalen Leistungsmerkmalen angezeigt, die Sie Ihrem Projekt hinzufügen können, z. B. Push Notifications.  

	1. Optional: Wählen Sie **Hinzufügen** aus, um Ihrem Projekt eins der aufgelisteten Leistungsmerkmale hinzuzufügen. Bearbeiten Sie **Servicename** für Ihren Service und klicken Sie auf **Erstellen**.
	
	2. Optional: Wiederholen Sie Schritt *a* für alle zusätzlichen Leistungsmerkmale, die Sie Ihrem Projekt hinzufügen möchten. 

3. Entwerfen Sie Ihre Benutzerschnittstelle mithilfe des Benutzerschnittstellenbuilders.

   Hinweis: Da die Code-Starter nicht über eine anpassbare Benutzerschnittstelle verfügen, steht die Registerkarte *Design* nicht zur Verfügung.

    1. Wählen Sie im Navigationsmenü die Option **Benutzerschnittstellenbuilder** aus, um das Design Ihrer App anzupassen.<!--Most of the design screens have sections that begin with a navigation on the left of the screen, and the sections more specific as it moves to the right side preview of your app. Note: Not all design screens in the starters have the same sections.--> 
	
	2. Passen Sie das Layout Ihrer App über die Registerkarte **Anzeigen** an.
	
	3. Fügen Sie neue Anzeigen hinzu, indem Sie **Anzeige erstellen** auswählen. Benennen Sie neue Anzeigen, um sie in Ihrer App besser referenzieren zu können. Sie können aus folgenden Anzeigetypen auswählen: 
	    * Menü
		* Liste
		* Karte
		* Angepasst 
		* Diagramm
		
	4. Sie können den Menütitel Ihrer App ändern, indem Sie das Textfeld *Menü* im Abschnitt **Layout** Ihrer Schnittstelle auswählen und den Inhalt des Feldes **Anzuzeigende Daten** ersetzen. Zeigen Sie Ihre Aktualisierungen im Abschnitt für simulierte Geräte an.
	
		Aktualisieren Sie die Designelemente, indem Sie sie einzeln auswählen und gegebenenfalls die Informationen aktualisieren. Diese Elemente werden im Baumstrukturformat angezeigt. Sie können die Reihenfolge oder die Position der Menüelemente ändern, indem Sie ein Element an eine neue Position ziehen. Alle untergeordneten Elemente des Elements werden zusammen mit dem übergeordneten Element verschoben. Die Textinformationen in den Baumstrukturelementen, die in den Feldern **Anzuzeigende Daten** angezeigt werden, verweisen auf Inhalt des Datenquellen-Spreadsheets. *Ändern Sie diese Elemente nicht in der Ansicht **Design**, da sie vom Inhalt in den Datenquellen überschrieben werden, die in der Ansicht **Daten** angegeben sind.* 
		
		Ein Element, das in der Baumstruktur als *Formular* angegeben ist, ist unabhängig und kann integriert geändert werden. Es referenziert keine Informationen aus einer Datenquelle.
	
	5. Wählen Sie in der Navigation die Option **Daten** aus, um die von der App verwendeten Daten anzuzeigen. Die Vorlage enthält Standardinformationen; Sie können die Quelle der Daten jedoch ändern, indem Sie **Neue erstellen** auswählen. Da Sie mehr als eine Datenquelle referenzieren können, geben Sie für jede Datenquelle, die Sie verwenden, einen Namen an. Sie können aus den folgenden Optionen für Datenquellen auswählen:
		* Cloud
		* Local
		* Cloudant
		* Google Sheet
		* Excel Online
		* Google Drive
	
	Sie können auch in der Tabelle vorhandenen Inhalt importieren, exportieren oder ändern, wenn sie lokal ist, indem Sie die Schaltflächen verwenden und den Inhalt in der Tabelle auswählen.
	     
		 Hinweis: Wenn Sie Daten importieren, die nicht mit der Struktur der Standarddaten übereinstimmen, aktivieren Sie die Schiebeleiste zum Ersetzen des Schemas. Ein Beispiel hierfür ist eine CSV-Datei, die weniger Spalten besitzt als die Daten, die mit Ihrem Starter bereitgestellt werden.
		 
	6. Wählen Sie in der Navigation die Option **Benutzerzugriff** aus, um die Zugangsvoraussetzungen Ihres Projekts zu ändern. Mit dem Switch können Sie den Benutzerzugriff ein- und ausschalten. Wenn der Benutzerzugriff eingeschaltet ist, können Sie das Zeitlimit für inaktive Benutzer sowie die Berechtigungsnachweise für Benutzer festlegen, die auf die App zugreifen.
	
	7. Wählen Sie im Navigationsmenü die Option **Einstellungen** aus, um die Gesamtinformationen zu Ihrem Projekt und die farbliche Darstellung zu ändern. In dieser Anzeige geben Sie Ihren Google-API-Schlüssel ein, wenn dieser für die Leistungsmerkmale, die Sie Ihrem Projekt hinzugefügt haben, erforderlich ist. In dieser Anzeige geben Sie auch Ihre eindeutige Bundle-ID ein, die im Apple Store oder Google Play Store registriert ist.
	
		Wenn Sie Ihrem Projekt das IBM MobileFirst Foundation-SDK hinzufügen wollen, schalten Sie den Switch ein.
		
	8. Wenn Sie den Switch umgeschaltet haben, um Ihrem Projekt in der Anzeige *Einstellungen* IBM MobileFirst Platform Foundation hinzuzufügen, wird in der Navigation die Auswahl **Foundation** angezeigt. Wählen Sie **Foundation** aus und füllen Sie die für IBM MobileFirst Platform Foundation spezifischen erforderlichen Informationen aus.
	
	9. Wählen Sie im Navigationsmenü die Option **Veröffentlichen** aus, um die endgültigen Informationen für die Erstellung Ihrer mobilen App einzugeben. Sie können Ihre Bundle-ID für iOS und die Anwendungs-ID für Android eingeben.
	
	Wenn Sie eine iOS-App erstellen, müssen Sie Ihre Bundle-ID, Ihr Verteilungszertifikat in Form einer *.p12*-Datei und Ihr Bereitstellungsprofil in Form einer *.mobileprovision*-Datei aus dem Apple-Bereitstellungsportal abrufen. Diese drei sollten zum selben Zeitpunkt und mit demselben Computer erstellt werden, der auch zum Posten Ihrer App im Apple-Store verwendet werden soll. Das Verteilungszertifikat und das Bereitstellungsprofil müssen auf der Bundle-ID basieren. 	

4.  Kehren Sie zurück zur Anzeige *Projektübersicht*, um den Code für Ihre App abzurufen, und testen Sie die App. Sie können den Code direkt für das iOS- oder Android-Betriebssystem herunterladen oder einen QR-Code für das Android-Betriebssystem scannen. 


