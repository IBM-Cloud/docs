---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-15"

---
{:new_window: target="_blank"}

# Lernprogramm - Benutzerschnittstellenstarter für Store Catalog
{: #tutorial_store_catalog}

Der Benutzerschnittstellenstarter für {{site.data.keyword.Bluemix}} Store Catalog bietet eine grundlegende, anpassbare Struktur für Verkaufs-Apps sowie Integrationspunkte für jeden der {{site.data.keyword.Bluemix_notm}} Mobile-Services.


## Voraussetzungen
{: #tutorial_requirements}

* Ein [Bluemix ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net "Symbol für externen Link")-Konto


## Einführung
{: #tutorial_gs}

Zur schnellen Einrichtung und Ausführung mit dem Benutzerschnittstellenstarter für Store Catalog befolgen Sie diese Schritte:

1. Erstellen Sie ein Mobile-Dashboard-Projekt in {{site.data.keyword.Bluemix_notm}}.

   1. Klicken Sie auf der Seite **Einführung** des Mobile-Dashboards auf **Projekt erstellen**.

      Alternativ können Sie auf der Seite **Projekte** auf **Projekt erstellen** klicken.

   2. Wählen Sie **Benutzerschnittstellenstarter** aus, sofern noch nicht geschehen.

   3. Wählen Sie **Store Catalog** aus und klicken Sie auf **Projekt erstellen**.

   4. Geben Sie Ihren Projektnamen ein und klicken Sie auf **Erstellen**.

2. Optional: Fügen Sie die {{site.data.keyword.mobilepushshort}}-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **{{site.data.keyword.mobilepushshort}}** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **{{site.data.keyword.mobilepushshort}}** auf **Erstellen** klicken.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.

   3. Für iOS: [Apple Push Notification Service konfigurieren ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobilepush/t_push_provider_ios.html "Symbol für externen Link"){: new_window}.

   4. Für Android: [Google Cloud Messaging konfigurieren ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobilepush/t_push_provider_android.html "Symbol für externen Link"){: new_window}.

3. Optional: Fügen Sie andere Funktionen hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für die Funktion auf **Hinzufügen**.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.

   3. Befolgen Sie die Anweisungen, die im Lieferumfang des Service enthalten sind, um ihn einzurichten.

4. Entwerfen Sie Ihre App.

   1. Wählen Sie im Navigationsmenü die Option **Benutzerschnittstellenbuilder** aus, um das Design Ihrer App anzupassen.
   
		**Tipp:** Für eine Schnellansicht des Benutzerschnittstellenbuilders müssen Sie nach der Auswahl des Benutzerschnittstellenbuilders in der Navigation die Option zum Anzeigen der Funktion auswählen.

   2. Wählen Sie in der Navigation die Registerkarte **Design** aus.

      Es gibt einen Arbeitsbereich für das Design Ihrer App und eine simulierte Ansicht für die Gestaltung Ihrer App.

   3. Optional fügen Sie neue Anzeigen hinzu, indem Sie **Anzeige erstellen** auswählen. Benennen Sie neue Anzeigen, um sie in Ihrer App besser referenzieren zu können. Neue Anzeigen werden ungeachtet der Auswahl in der Baumstruktur auf derselben Ebene wie die Hauptanzeige erstellt. Sie können aus folgenden Anzeigetypen auswählen:
      * Menü
      * Liste
      * Karte
      * Angepasst
      * Diagramm	   

   4. Sie können den Menütitel Ihrer App ändern, indem Sie das Textfeld *Menü* im Abschnitt **Layout** Ihrer Schnittstelle auswählen und den Inhalt des Feldes **Anzuzeigende Daten** ersetzen. Zeigen Sie Ihre Aktualisierungen im Abschnitt für simulierte Geräte an.

      Aktualisieren Sie die Designelemente, indem Sie sie einzeln auswählen und gegebenenfalls die Informationen aktualisieren. Diese Elemente werden im Baumstrukturformat angezeigt. Sie können die Reihenfolge oder die Position der Menüelemente ändern, indem Sie ein Element an eine neue Position ziehen. Alle untergeordneten Elemente des Elements werden zusammen mit dem übergeordneten Element verschoben. Die Textinformationen in den Baumstrukturelementen, die in den Feldern **Anzuzeigende Daten** angezeigt werden, verweisen auf Inhalt des Datenquellen-Spreadsheets. *Ändern Sie diese Elemente nicht in der Ansicht **Design**, da sie vom Inhalt in den Datenquellen überschrieben werden, die in der Ansicht **Daten** angegeben sind.*

		Ein Element, das in der Baumstruktur als *Formular* angegeben ist, ist unabhängig und kann integriert geändert werden. Es referenziert keine Informationen aus einer Datenquelle.

   5. Wählen Sie in der Navigation die Option **Daten** aus, um die von der App verwendeten Daten anzuzeigen. Die Vorlage enthält Standardinformationen. Sie können die Quelle der Daten jedoch ändern, indem Sie **Neue erstellen** auswählen. Da Sie mehr als eine Datenquelle referenzieren können, geben Sie für jede Datenquelle, die Sie verwenden, einen Namen an. Sie können aus den folgenden Optionen für Datenquellen auswählen:
      * Cloud
      * Local
      * Cloudant
      * Google Sheet
      * Excel Online
      * Google Drive

      Sie können auch in der Tabelle vorhandenen Inhalt importieren, exportieren oder ändern, wenn sie lokal ist, indem Sie die Schaltflächen verwenden und den Inhalt in der Tabelle auswählen.

	  Hinweis: Wenn Sie Daten importieren, die nicht mit der Struktur der Standarddaten übereinstimmen, aktivieren Sie die Schiebeleiste zum Ersetzen des Schemas. Ein Beispiel hierfür ist eine CSV-Datei, die weniger Spalten besitzt als die Daten, die mit Ihrem Starter bereitgestellt werden.
	  
   6. Wählen Sie **Navigation** aus, um die Navigationsaktionen in Ihrer App anzupassen. Dieser Vorgang ist optional, da die Navigationsaktionen für viele der Anzeigen entsprechend den Beziehungen zwischen den Anzeigen automatisch erstellt werden. Sie können die Zielanzeige ändern, indem Sie in der Liste der Menüelemente zuerst die Anzeige bzw. das Feld auswählen, *von* der bzw. dem die Navigation ausgehen soll. Wählen Sie anschließend im Zielanzeigefeld die Anzeige aus, *zu* der navigiert werden soll. 

   7. Wählen Sie in der Navigation die Option **Benutzerzugriff** aus, um die Zugangsvoraussetzungen Ihres Projekts zu ändern. Mit dem Switch können Sie den Benutzerzugriff ein- und ausschalten. Wenn der Benutzerzugriff eingeschaltet ist, können Sie das Zeitlimit für inaktive Benutzer sowie die Berechtigungsnachweise für Benutzer festlegen, die auf die App zugreifen.

   8. Wählen Sie im Navigationsmenü die Option **Einstellungen** aus, um die Gesamtinformationen zu Ihrem Projekt und die farbliche Darstellung zu ändern. In dieser Anzeige geben Sie Ihren Google-API-Schlüssel ein, wenn dieser für die Services, die Sie Ihrem Projekt hinzugefügt haben, erforderlich ist. In dieser Anzeige geben Sie auch Ihre eindeutige Bundle-ID ein, die im Apple Store oder Google Play Store registriert ist.

      Wenn Sie Ihrem Projekt das IBM MobileFirst Foundation-SDK hinzufügen wollen, schalten Sie den Switch ein.

   9. Wenn Sie den Switch umgeschaltet haben, um Ihrem Projekt in der Anzeige *Einstellungen* IBM MobileFirst Platform Foundation hinzuzufügen, wird in der Navigation die Auswahl **Foundation** angezeigt. Wählen Sie **Foundation** aus und füllen Sie die für IBM MobileFirst Platform Foundation spezifischen erforderlichen Informationen aus.

   10. Wählen Sie im Navigationsmenü die Option **Veröffentlichen** aus, um die endgültigen für die Erstellung Ihrer mobilen App erforderlichen Informationen einzugeben. Sie können Ihre Bundle-ID für iOS und die Anwendungs-ID für Android eingeben.

       Wenn Sie eine iOS-App erstellen, müssen Sie Ihre Bundle-ID, Ihr Verteilungszertifikat in Form einer *.p12*-Datei und Ihr Bereitstellungsprofil in Form einer *.mobileprovision*-Datei aus dem Apple-Bereitstellungsportal abrufen. Diese drei sollten zum selben Zeitpunkt und mit demselben Computer erstellt werden, der auch zum Posten Ihrer App im Apple-Store verwendet werden soll. Das Verteilungszertifikat und das Bereitstellungsprofil müssen auf der Bundle-ID basieren. 	

5. Laden Sie Ihr Projekt herunter.

   1. Klicken Sie auf **Code** und wählen Sie Ihre bevorzugte Plattform oder Programmiersprache aus.

   2. Unter Android können Sie nach der Code-Generierung aus folgenden Optionen auswählen:

      * Code herunterladen

      * APK herunterladen

      * Mit QR-Code herunterladen

   3. Für iOS können Sie nach der Generierung des Codes die folgende Option auswählen:

      * Code herunterladen

6. Führen Sie Ihre App auf Ihrem Gerät oder Simulator aus.


## Nächste Schritte
{: #tutorial_next}

[Testen Sie Ihre App! ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://console.{DomainName}/mobile/create-project?starter=fb5e31a9-1186-4d46-939e-2f620f35b83b "Symbol für externen Link"){: new_window}


### Lernprogramme zu Benutzerschnittstellenstartern
{: #tutorials_UI}

* [Lernprogramm - Store Catalog](tutorial_store_catalog.html)


### Lernprogramme zu Code-Startern
{: #tutorials_Code}

* [Lernprogramm - Basic](tutorial.html)
* [Lernprogramm - Cloudant Sync](tutorial_cloudant_synd.html)
* [Lernprogramm - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Lernprogramm - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Lernprogramm - Watson Language](tutorial_watson_language.html)
* [Lernprogramm - Weather](tutorial_weather.html)

