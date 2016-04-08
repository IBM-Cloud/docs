---

copyright:
  years: 2015,2016

---

{:new_window: target=_"blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Einführung in {{site.data.keyword.iotrtinsights_full}}
{: #gettingstartedtemplate}
*Letzte Aktualisierung: 11. Februar 2016*

Mit {{site.data.keyword.iotrtinsights_full}} in Bluemix ({{site.data.keyword.iotrtinsights_short}}) können Sie Analysen von Echtzeitdaten Ihrer IoT-Geräte erstellen und erhalten so Informationen zu deren Status sowie zum allgemeinen Status Ihrer Operationen.
{:shortdesc}

Bevor Sie {{site.data.keyword.iotrtinsights_short}} verwenden können, müssen Sie zuerst den {{site.data.keyword.iot_full}}-Service ({{site.data.keyword.iot_short}}) einrichten, um Ihre Analyse-Engine mit Ihren Geräten zu verbinden. Sie können einen vorhandenen {{site.data.keyword.iot_short}}-Service verwenden oder einen neuen erstellen. Für einen schnellen Einstieg können Sie die IoT-Telefonanwendung und deren zugeordneten {{site.data.keyword.iot_short}}-Service für Ihre Organisation bereitstellen. 

Führen Sie die folgenden Schritte aus, damit dieser Service schnell einsatzbereit ist: 
1. Stellen Sie den {{site.data.keyword.iotrtinsights_short}}-Service für Ihre Bluemix-Organisation bereit. 
  1. Klicken Sie im Dashboard Ihres Bluemix-Kontos auf **Services oder APIs verwenden**.
  2. Lokalisieren Sie den Internet of Things-Abschnitt des Servicekatalogs und wählen Sie **{{site.data.keyword.iotrtinsights_short}}** aus.
  3. Überprüfen Sie auf der {{site.data.keyword.iotrtinsights_short}}-Seite die Auswahlen für "Service hinzufügen":   
    - Bereich - Stellen Sie sicher, dass der Service in demselben Bereich bereitgestellt wird, in dem auch der {{site.data.keyword.iot_short}}-Service bereitgestellt wurde. 
    - Anwendung - Nicht binden. 
    - Servicename - Ändern Sie optional den Servicenamen in einen Namen, den Sie sich leicht merken können. Dieser Name wird in der IoT-Kachel "{{site.data.keyword.iotrtinsights_short}}" im Bluemix-Dashboard angezeigt. 
    - Ausgewählter Plan - Wählen Sie "Kostenfrei" aus oder wählen Sie einen gebührenpflichtigen Plan aus, der Ihren Anforderungen entspricht.   
    > **Wichtig:** Mit dem kostenfreien {{site.data.keyword.iotrtinsights_short}}-Plan können Sie pro Organisation nur eine Instanz des Service bereitstellen.
  4. Klicken Sie auf **Verwenden**, um {{site.data.keyword.iotrtinsights_short}} für Ihre Bluemix-Services bereitzustellen. 
2. Optional: Verwenden Sie Ihr Telefon als IoT-Gerät mit {{site.data.keyword.iotrtinsights_short}}.
Verwenden Sie Ihre IoT-Telefonanwendung, um Ihr Smartphone schnell als IoT-Gerät einzurichten, mit dem Sie Ihre {{site.data.keyword.iotrtinsights_short}}-Umgebung überprüfen und Echtzeitanalysen der Daten definieren können. Weitere Informationen zur IoT-Telefonanwendung finden Sie im Projekt zur [Internet of Things-Telefonanwendung](https://github.com/ibm-messaging/IoT-html5-phone).  

  Gehen Sie wie folgt vor, um die Anwendung zu erstellen und Ihr Telefon mit {{site.data.keyword.iot_full}} zu verbinden: 
  1. Klicken Sie auf nachfolgende Schaltfläche, um den Bereitstellungsprozess zu starten:
  [![Symbol 'In Bluemix bereitstellen'](https://bluemix.net/deploy?repository=https://github.com/ibm-messaging/iot-html5-phone "IoT-Telefon in Bluemix bereitstellen")(images/deploy_to_bluemix.png "Symbol 'In Bluemix bereitstellen'")].   
  > **Hinweis:** Durch die Bereitstellung der IoT-Telefonanwendung wird auch ein {{site.data.keyword.iot_short}}-Service (*iot-phone-iotf-service*) bereitgestellt, der automatisch an die Telefonanwendung gebunden wird. Fügen Sie diesen {{site.data.keyword.iot_short}}-Service als Datenquelle hinzu, um die IoT-Telefonanwendung zu testen. Es wird auch ein Cloudant NoSQL DB-Service  (*iot-phone-cloudant-cloudantNoSQLDB*) erstellt, der von der Anwendung verwendet wird.
  2. Klicken Sie auf **Genehmigen**, wenn Sie aufgefordert werden, den Zugriff für IBM Single Sign On Service (OAuth Consent) selbst zu genehmigen.   
  >**Tipp:** Wenn Sie kein Bluemix-Konto haben, können Sie sich anmelden, um Ihre kostenfreie Bluemix-Testversion zu aktivieren. 
  2. Ändern Sie den Namen im Feld "Anwendungsname" in einen leicht zu merkenden Namen. In den weiteren Anweisungen wird die Bezeichnung *Telefonanwendung* verwendet. Dieser Name wird in einer Anwendungskachel in Ihrem Bluemix-Dashboard angezeigt; er ist Bestandteil der URL, die Sie verwenden, wenn Sie Ihr Telefon mit {{site.data.keyword.iot_short}} verbinden. 
  2. Klicken Sie auf **Bereitstellen**. 
  2. Kehren Sie zu dem Bluemix-Dashboard zurück, nachdem der Bereitstellungsprozess abgeschlossen ist und eine Erfolgsnachricht angezeigt wurde. Die Kacheln *Telefonanwendung* und *iot-phone-iotf-service* werden zu Ihrem Konto hinzugefügt. 
  1. Klicken Sie im Bluemix-Dashboard auf die Kachel *Telefonanwendung*. 
  2. Öffnen Sie auf Ihrem Telefon einen Browser und rufen Sie die Weiterleitungs-URL auf, die unter dem Anwendungsnamen angezeigt wird. Geben Sie bei der entsprechenden Eingabeaufforderung eine frei gewählte Geräte-ID an, mit der Sie Ihr Telefon als Gerät in den {{site.data.keyword.iot_short}}- und {{site.data.keyword.iotrtinsights_short}}-Dashboards identifizieren. 
  3. Klicken Sie auf **Verbinden**, um Ihr Telefon mit dem {{site.data.keyword.iot_short}}-Service *iot-phone-iotf-service* zu verbinden.
  Die Anzeige wird mit den Daten aktualisiert, die von Ihrem Telefon zu Ihrem {{site.data.keyword.iot_short}}-Service gesendet werden. 
2. Erstellen und konfigurieren Sie einen IoT-Service.   
> **Tipp:** Wenn Sie die IoT-Telefonanwendung bereitgestellt haben, wurde der *iot-phone-iotf-service* bereits erstellt und Sie können diesen Schritt überspringen.   

  1. Melden Sie sich bei der Bluemix-Organisation an und wählen Sie den Bereich aus, in dem {{site.data.keyword.iotrtinsights_short}} bereitgestellt werden soll. 
  2. Klicken Sie im Bluemix-Dashboard auf **Services oder APIs verwenden**. 
  3. Lokalisieren Sie den Internet of Things-Abschnitt des Servicekatalogs und wählen Sie **Internet of Things** aus. 
  4. Überprüfen Sie auf der {{site.data.keyword.iot_full}}-Seite die Auswahlen für "Service hinzufügen" und klicken Sie auf **Verwenden**, um {{site.data.keyword.iot_short}} zu Ihren Bluemix-Services hinzuzufügen.
  Nachdem der {{site.data.keyword.iot_short}}-Service bereitgestellt wurde, werden Sie zur Service-Management-Seite weitergeleitet. 
3. Lokalisieren Sie die API-Schlüssel für die Verbindung.
Wenn Sie einen neuen {{site.data.keyword.iot_short}}-Service erstellt haben, müssen Sie nun die API-Schlüssel erstellen, um die beiden Services  zu verbinden. Wenn Sie einen vorhandenen Service verwenden, können Sie die bestehenden Schlüssel nutzen.   
  1. Klicken Sie im Bluemix-Dashboard auf die Internet of Things-Kachel.   
  >**Hinweis:** Wenn Sie die IoT-Telefonanwendung verwenden, klicken Sie auf die Kachel *iot-phone-iotf-service*.   

  1. Klicken Sie auf **Dashboard starten**, um das {{site.data.keyword.iot_full}}-Dashboard zu öffnen. 
  2. Navigieren Sie zu **Zugriff > API-Schlüssel**.
  3. Klicken Sie auf **API-Schlüssel generieren**. 
  3. Notieren Sie sich den API-Schlüssel, das Authentifizierungstoken und die Organisations-ID, die am oberen Rand des {{site.data.keyword.iot_short}}-Dashboards angezeigt wird.
  Sie benötigen diese Informationen in {{site.data.keyword.iotrtinsights_short}}, um die Services zu verbinden. 
4. Verbinden Sie Ihren {{site.data.keyword.iot_short}}-Service und den {{site.data.keyword.iotrtinsights_short}}-Service. 
  1. Klicken Sie im Bluemix-Dashboard auf die Kachel für {{site.data.keyword.iotrtinsights_short}}.   
  2. Klicken Sie auf der Serviceseite auf **Datenquelle hinzufügen**. 
  2. Klicken Sie auf der Seite "Datenquellen verwalten" der {{site.data.keyword.iotrtinsights_short}}-Konsole auf **Neue Datenquelle hinzufügen**. 
  3. Geben Sie für die Datenquelle einen beschreibenden Namen an und geben Sie die folgenden Informationen an, die Sie vorher ermittelt haben. 
    - Organisations-ID
    - API-Schlüssel
    - Authentifizierungstoken
  4. Klicken Sie auf ![Symbol 'Erstellen'](images/create.png "Symbol 'Erstellen'"), um die Datenquelle zu erstellen und eine Verbindung zu ihr herzustellen. 
4. Sie können {{site.data.keyword.iotrtinsights_short}} nun verwenden.
Sie können mit der Verwendung von {{site.data.keyword.iotrtinsights_short}} beginnen, indem Sie Benutzer hinzufügen, Ihre Geräte verbinden, Dashhoards zum Anzeigen von relevanten Gerätedaten konfigurieren und Alerts einrichten. 
>**Ihre {{site.data.keyword.iotrtinsights_short}}-Instanz auswählen:** Wenn Ihnen als Operator oder Administrator Zugriff auf weitere {{site.data.keyword.iotrtinsights_short}}-Instanzen erteilt wurde, können Sie schnell zwischen diesen Instanzen wechseln. Klicken Sie in der {{site.data.keyword.iotrtinsights_short}}-Konsole auf Ihren Benutzernamen und wählen Sie die Instanz aus, auf die Sie zugreifen wollen.    

# Zugehörige Links
## Beispiele
* [Internet of Things-Telefonanwendung](https://github.com/ibm-messaging/IoT-html5-phone)
* [developerWorks - Internet of Things-Rezepte](https://developer.ibm.com/recipes/)
* [Creating apps with the Internet of Things starter application](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500)

## API
* [API-Dokumentation](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)

## Allgemein
* [Produktinformationen](iotrtinsights_overview.html)   
* [What's new in Bluemix Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category)
* [Einführung in {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html)
* [dW-Antworten in IBM developerWorks](https://developer.ibm.com/answers/topics/iot-real-time/)
