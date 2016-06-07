---

copyright:
  years: 2015, 2016

---


{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


#Services
{: #services}
*Letzte Aktualisierung: 20. Januar 2016*

Verfügbare Services finden Sie im **Katalog** unter **Services** in der
{{site.data.keyword.Bluemix}}-Benutzerschnittstelle.
{:shortdesc}


{{site.data.keyword.Bluemix_notm}} stellt vordefinierte Services für mobile Anwendungen bereit. So
erleichtert {{site.data.keyword.Bluemix_notm}} Ihnen das Implementieren, Betreiben und Skalieren dieser
mobilen Services für Ihre mobilen Anwendungen. Somit können Sie sich auf Ihre Anwendungslogik und den Anwendungsentwurf konzentrieren.

{{site.data.keyword.Bluemix_notm}} betreibt und verwaltet Middleware-Services für Webanwendungen. Anwendungsentwickler haben die Möglichkeit, die für sie erforderlichen Middleware-Services anzugeben. {{site.data.keyword.Bluemix_notm}} stellt daraufhin automatisch neue Instanzen der angegebenen Middleware-Services bereit und bindet die Serviceinstanzen an die Anwendung.

{{site.data.keyword.Bluemix_notm}}
zeigt Services auf zwei Arten an: nach Servicekategorie und nach Serviceunterstützungstyp.



<dl>
<dt><strong>Kategorie</strong></dt>
<dd>{{site.data.keyword.Bluemix_notm}}-Services
werden in unterschiedlichen Kategorien zusammengefasst. In jeder Servicekategorie
werden zuerst die von IBM erstellten Services, anschließend die Services anderer Anbieter und
danach die Community-Services aufgeführt.</dd>
<dt><strong>Support</strong></dt>
<dd>Für {{site.data.keyword.Bluemix_notm}}-Services stehen mehrere Unterstützungsstufen bereit. In der folgenden Tabelle werden allgemeine Supportinformationen für
{{site.data.keyword.Bluemix_notm}}-Services beschrieben:

</dd>
</dl>



|Typ	|Beschreibung	|Details zu Unterstützung|
|:------|:--------------|:--------------|
|IBM	|Ein Service, der von IBM bereitgestellt wird und zur allgemeinen Verfügung bereitsteht.	|Für Probleme, die sich als Mängel eines von IBM bereitgestellten, allgemein verfügbaren Service
erweisen, steht Support zur Verfügung. Die Art des Supports beruht auf der von Ihnen festgelegten Prioritätsstufe. Weitere Informationen zu Prioritätsstufen von Tickets finden Sie unter [Support kontaktieren](../support/index.html#contacting-bluemix-support){: new_window}.|
|Drittanbieter	|Ein Service, der von einem anderen Unternehmen als IBM bereitgestellt wird.	|Support für Services von Drittanbietern wird durch den Service-Provider bereitgestellt. Wenn ein Problem von IBM untersucht wird und sich als Mangel im Service eines Drittanbieters herausstellt, ist IBM nicht verpflichtet, einen Fix zur Verfügung zu stellen. IBM teilt die Analyse mit dem anderen Service-Provider auf, sofern erforderlich.|
|Community	|Ein Service, der von einer Open-Source-Community bereitgestellt wird.	|Support für Community-Services wird von der {{site.data.keyword.Bluemix_notm}} Developers Community bereitgestellt. Wenn ein Problem von IBM untersucht wird und sich als Mangel im Community-Service herausstellt, ist IBM nicht verpflichtet, einen Fix zur Verfügung zu stellen.|
|Beta	|Ein Service, der für die Produktionsumgebung noch nicht einsatzfähig ist und sich in einer Versuchsphase der
Entwicklungsstufe befindet. Ein Betaservice kann den Entwicklungs- und Marketingteams dabei helfen, den Wert der Services einzuschätzen, bevor sie den Service der Allgemeinheit zur Verfügung stellen.	|Probleme, die sich als Mängel in einem von IBM bereitgestellten Betaservice erweisen, werden unterstützt; jedoch ist IBM nicht verpflichtet, einen Fix zur Verfügung zu stellen. Zusätzlich wird dem Problemticket eine Prioritätsstufe von 3 oder 4 zugeordnet, soweit zutreffend. Informationen zu Prioritätsstufen von Tickets finden Sie unter [Support kontaktieren](../support/index.html#contacting-bluemix-support){: new_window}.|
*Tabelle 1. Supportinformationen für {{site.data.keyword.Bluemix_notm}}*




{{site.data.keyword.Bluemix_notm}}
stellt darüber hinaus experimentelle Services bereit, die Sie testen können. Um alle verfügbaren experimentellen Services, Boilerplates und Laufzeiten anzuzeigen, melden Sie sich an {{site.data.keyword.Bluemix_notm}} an, blättern Sie zum Ende des Katalogs und klicken Sie anschließend auf **{{site.data.keyword.Bluemix_notm}} Labs-Katalog**.

Experimentelle Services sind möglicherweise
nicht ganz stabil in der Ausführung und können Änderungen aufweisen, die nicht mit früheren
Versionen kompatibel sind. Diese Services sollten nicht in Produktionsumgebungen verwendet werden. Support für experimentelle Services wird von der {{site.data.keyword.Bluemix_notm}} Developers Community bereitgestellt. Wenn ein Problem von IBM untersucht wird und sich als Mangel eines experimentellen Service herausstellt,
ist IBM nicht verpflichtet, einen Fix zur Verfügung zu stellen.

Um einen Service in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle, der Befehlszeilenschnittstelle 'cf', IBM {{site.data.keyword.Bluemix_notm}} DevOps Service oder in sonstigen unterstützten Tools nutzen zu können, führen Sie die folgenden Schritte durch:

1. Erstellen Sie eine Instanz des Service. In den meisten Fällen kann die Serviceinstanz im Zuge der Anwendungserstellung eingerichtet werden.

2. Geben Sie die Anwendung an, von der die neue Serviceinstanz verwendet werden soll. Bei Webanwendungen können Sie mehr als eine Anwendung für die Nutzung derselben Serviceinstanz angeben, was gewöhnlich zu Zwecken der gemeinsamen Datennutzung geschieht.

3. Schreiben Sie für die Interaktion mit dem Service Ihren eigenen Code in Ihre Anwendung.

##Services nach Region

Nicht alle
Services sind für jede {{site.data.keyword.Bluemix_notm}}-Region verfügbar. In der folgenden Tabelle sind die Services aufgeführt, die von IBM zur Verfügung gestellt werden.



|Service	|Verfügbar in Region 'US South'	|Verfügbar in Region 'Europe United Kingdom' |Verfügbar in Region 'Australia Sydney'|
|:----------|:------------------------------|:------------------|:------------------|
|{{site.data.keyword.activedeployshort}}	|Ja		|Ja		|Nein|
|{{site.data.keyword.alchemyapishort}} 		|Ja	   	|Ja  		|Ja|
|{{site.data.keyword.appsecshort}}		|Ja		|Nein		|Nein|
|{{site.data.keyword.alertnotificationshort}}|Ja		|Nein			|Nein		|
|{{site.data.keyword.APS_DA}}			|Ja		|Nein		|Nein|
|{{site.data.keyword.APS_MA}}			|Ja		|Nein		|Nein|
|{{site.data.keyword.amashort}}			|Ja		|Ja		|Ja|
|{{site.data.keyword.hadoopst}}			|Ja		|Nein		|Nein|
|{{site.data.keyword.APIM}}			|Ja		|Ja		|Nein|
|{{site.data.keyword.autoscaling}}		|Ja		|Ja		|Ja|
|{{site.data.keyword.bigicloudst}}		|Ja		|Nein		|Nein|
|{{site.data.keyword.rules_short}}		|Ja		|Ja		|Nein|
|{{site.data.keyword.cloudint}}			|Ja		|Ja		|Nein|
|{{site.data.keyword.cloudant}}			|Ja		|Ja		|Nein|
|{{site.data.keyword.conceptexpansionshort}}	|Ja		|Ja		|Ja|
|{{site.data.keyword.conceptinsightsshort}}	|Ja		|Ja		|Ja|
|{{site.data.keyword.dashdbshort}}		|Ja		|Ja		|Nein|
|{{site.data.keyword.datacshort}}		|Ja		|Ja		|Ja|
|{{site.data.keyword.DB2OnCloud_short}}		|Ja		|Ja		|Ja|
|{{site.data.keyword.deliverypipeline}}		|Ja		|Ja		|Nein|
|{{site.data.keyword.dialogshort}}		|Ja		|Ja		|Ja|
|{{site.data.keyword.documentconversionshort}}	|Ja		|Ja		|Ja|
|{{site.data.keyword.creshort}}			|Ja		|Nein		|Nein|
|{{site.data.keyword.game}}			|Ja		|Ja		|Ja|
|{{site.data.keyword.geospatialshort_Geospatial}}	|Ja	|Ja		|Nein|
|{{site.data.keyword.globalizationshort}}	|Ja		|Nein		|Nein|
|{{site.data.keyword.dataworks_short}}		|Ja		|Ja		|Nein|
|{{site.data.keyword.twittershort}}		|Ja		|Ja		|Ja|
|{{site.data.keyword.weather_short}}		|Ja		|Ja		|Ja|
|{{site.data.keyword.IntegrationTestingshort}}	|Ja		|Ja		|Nein|
|{{site.data.keyword.iot_short}}		|Ja		|Nein		|Nein|
|{{site.data.keyword.keymanagementserviceshort}}|Nein		|Ja		|Nein|
|{{site.data.keyword.languagetranslationshort}}	|Ja		|Ja		|Nein|
|{{site.data.keyword.messagehub}}		|Ja		|Ja		|Nein|
|{{site.data.keyword.messageresonanceshort}}	|Ja		|Ja		|Nein|
|{{site.data.keyword.APS_MAiOS}} 		|Ja		|Nein		|Nein|
|{{site.data.keyword.macm_short}}		|Ja		|Ja		|Ja|
|{{site.data.keyword.mobilemam}}		|Ja		|Ja		|Nein|
|{{site.data.keyword.mobiledata}}		|Ja		|Ja		|Nein|
|{{site.data.keyword.manda}}			|Ja		|Ja		|Nein|
|{{site.data.keyword.mqa}}			|Ja		|Ja		|Nein|
|{{site.data.keyword.mql}}			|Ja		|Ja		|Nein|
|{{site.data.keyword.nlclassifierlshort}} 	|Ja 		|Ja 		|Ja|
|{{site.data.keyword.objectstorageshort}}	|Ja		|Nein		|Nein|
|{{site.data.keyword.personalityinsightsshort}}	|Ja		|Ja		|Ja|
|{{site.data.keyword.mobilepush}}Push		|Ja		|Ja		|Nein|
|Push für iOS 8					|Ja		|Ja		|Nein|
|{{site.data.keyword.questionandanswershort}}	|Ja		|Ja		|Ja|
|{{site.data.keyword.rapidApps}}		|Ja		|Ja		|Nein|
|{{site.data.keyword.relationshipextractionshort}}	|Ja	|Ja		|Ja|
|{{site.data.keyword.retrieveandrankshort}}	|Ja 		|Ja 		|Ja|
|{{site.data.keyword.SecureGateway}}		|Ja		|Ja		|Nein|
|{{site.data.keyword.servicediscoveryshort}}	|Ja		|Nein		|Nein|
|{{site.data.keyword.sescashort}}		|Ja		|Ja		|Ja|
|{{site.data.keyword.ssofull}}			|Ja		|Nein		|Nein|
|{{site.data.keyword.speechtotextshort}}	|Ja 		|Ja	 	|Ja|
|{{site.data.keyword.sqldb}}			|Ja		|Ja		|Nein|
|{{site.data.keyword.staticanalyzershort}}	|Ja		|Ja		|Nein|
|{{site.data.keyword.streaminganalyticsshort}}	|Ja		|Nein		|Nein|
|{{site.data.keyword.texttospeechshort}} 	|Ja 		|Ja	 	|Ja|
|{{site.data.keyword.times}}			|Ja		|Ja		|Nein|
|{{site.data.keyword.toneanalyzershort}} 	|Ja 		|Ja 		|Ja|
|{{site.data.keyword.trackplan}}		|Ja		|Ja		|Nein|
|{{site.data.keyword.tradeoffanalyticsshort}}	|Ja		|Ja		|Ja|
|{{site.data.keyword.visualinsightsshort}}	|Ja		|Ja		|Ja|
|{{site.data.keyword.visualizationrenderingshort}} |Ja		|Ja		|Nein|
|{{site.data.keyword.workflow}}			|Ja		|Ja		|Nein|
|{{site.data.keyword.workloadscheduler}}	|Ja		|Ja		|Nein|
|{{site.data.keyword.xpagesservice_short}}	|Ja		|Ja		|Nein|
*Tabelle 2. Serviceverfügbarkeit*


# Service zur Anwendung hinzufügen
{: #add_service}
*Letzte Aktualisierung: 8 March 2016*

{{site.data.keyword.Bluemix}} bietet eine Liste von Services an, die im Auftrag des Entwicklers verwaltet werden. Um einen Service hinzuzufügen, den Ihre Anwendung verwenden kann, müssen Sie eine Instanz dieses Service anfordern und die Anwendung für die Interaktion mit dem Service konfigurieren.

Sie haben die folgenden Möglichkeiten, alle in {{site.data.keyword.Bluemix_notm}} verfügbaren Services anzuzeigen:

* Über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle. Zeigen Sie den {{site.data.keyword.Bluemix_notm}}-Katalog an.
* Über die Befehlszeilenschnittstelle 'cf'. Verwenden Sie hier den Befehl **cf marketplace**.
* Über Ihre eigene Anwendung. Verwenden Sie die [Services-API GET /v2/services](http://apidocs.cloudfoundry.org/197/services/list_all_services.html){: new_window}.

Zum Entwickeln einer Anwendung wählen Sie den benötigten Service aus. Auf Ihre Auswahl hin interagiert {{site.data.keyword.Bluemix_notm}} mit dem Service und unternimmt die notwendigen Schritte zur Bereitstellung von Ressourcen dieses Service. Dieser Bereitstellungsprozess kann für die verschiedenen Servicetypen unterschiedlich ablaufen. Ein Datenbankservice richtet beispielsweise eine Datenbank ein, während ein Push-Benachrichtigungsservice für mobile Anwendungen Konfigurationsinformationen erstellt.

{{site.data.keyword.Bluemix_notm}} stellt Ihrer Anwendung mittels einer Serviceinstanz die Ressourcen eines Service zur Verfügung. Eine Serviceinstanz kann von mehreren Webanwendungen gemeinsam
genutzt werden.

Sie können auch Services verwenden, die in anderen Regionen gehostet werden, sofern diese Services in diesen Regionen verfügbar sind. Diese Services müssen im Internet
zugänglich gemacht werden und müssen über API-Endpunkte verfügen. Sie müssen Ihre Anwendung für die Verwendung dieser
Services manuell codieren, wie Sie auch externe Anwendungen oder Tools von anderen Anbietern
zur Verwendung von {{site.data.keyword.Bluemix_notm}}-Services codieren. Weitere Informationen finden Sie in [Externen Anwendungen und Tools von anderen Herstellern die Verwendung von {{site.data.keyword.Bluemix_notm}}-Services ermöglichen](#accser_external).



## Neue Serviceinstanz anfordern
{: #req_instance}

Um eine neue Serviceinstanz anzufordern, müssen Sie die
{{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle
oder die Befehlszeilenschnittstelle 'cf' verwenden.

**Hinweis:** Bei der Angabe des Servicenamens sollten Sie nur alphabetische oder numerische Zeichen verwenden, da es sonst zu unvorhersehbaren
Ergebnissen kommen kann.

Wenn Sie zum Anfordern einer Serviceinstanz die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle verwenden, führen Sie die folgenden Schritte durch:

1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-**Katalog** auf die Kachel für den Service, der hinzugefügt werden soll. Die Seite mit den Servicedetails wird geöffnet.

2. Wählen Sie im Bereich zum Hinzufügen eines Service in der Liste **Apps** eine Anwendung aus, an die Sie diese Serviceinstanz binden möchten.

3. Geben Sie in das Feld **Servicename** einen Namen ein. Es wird ein Standardservicename zur Verfügung gestellt. Sie können den Namen
in dem Feld ändern oder ihn unverändert übernehmen.

4. Füllen Sie ggf. weitere Felder aus bzw. treffen Sie weitere Auswahlen und klicken Sie
anschließend auf **Erstellen**.

Wenn Sie zum Anfordern einer Serviceinstanz die Befehlszeilenschnittstelle 'cf' verwenden,
führen Sie die folgenden Schritte durch:

1. Verwenden Sie den Befehl **cf marketplace**, um den Namen und den Plan des benötigten Service zu suchen.

2. Verwenden Sie den folgenden Befehl, um eine Serviceinstanz zu erstellen. Dabei ist 'service_name' der Name des Service, 'service_plan' der Plan
des Service und 'service_instance' der Name, den Sie für diese Serviceinstanz verwenden möchten.

    ```
    cf create-service service_name service_plan service_instance
    ```

3. Verwenden Sie den folgenden Befehl, um die Serviceinstanz an eine Anwendung zu binden. Dabei ist 'appname' der Name der Anwendung und 'service_instance' der Name
der Serviceinstanz.

    ```
    cf bind-service appname service_instance
    ```

Sie können eine Serviceinstanz nur an die App-Instanzen binden, die sich im selben Bereich bzw. in derselben Organisation befinden. Sie können allerdings Serviceinstanzen aus anderen Bereichen oder Organisationen auf dieselbe Weise wie eine externe App verwenden. Anstatt eine Bindung zu erstellen, verwenden Sie die Berechtigungsnachweise, um Ihre App-Instanz direkt zu konfigurieren. Weitere Informationen dazu, wie externe Apps {{site.data.keyword.Bluemix_notm}}-Services verwenden, finden Sie unter [Externen Apps die Verwendung von {{site.data.keyword.Bluemix_notm}}-Services ermöglichen](#accser_external){: new_window}.


## Die eigene Anwendung für die Interaktion mit einem Service konfigurieren 
{: #config}

Nachdem Sie eine Serviceinstanz an Ihre Anwendung gebunden haben, müssen Sie Ihre Anwendung für die Interaktion mit dem Service konfigurieren.

Für die Kommunikation mit Anwendungen kann unter Umständen jeder Service einen anderen Mechanismus erfordern. Wenn Sie Anwendungen entwickeln, werden diese Mechanismen zu Informationszwecken als Teil der Servicedefinition dokumentiert. Aus Konsistenzgründen sind diese Mechanismen für die Interaktion Ihrer Anwendung mit dem Service erforderlich.

* Um mit Datenbankservice zu interagieren, verwenden Sie die Informationen, die {{site.data.keyword.Bluemix_notm}} zur Verfügung stellt, z. B. die Benutzer-ID, das Kennwort und den Zugriffs-URI für die Anwendung.
* Um mit mobilen Back-End-Services zu interagieren, verwenden Sie die Informationen, die {{site.data.keyword.Bluemix_notm}} zur Verfügung stellt, z. B. die Anwendungskennung (app ID), die clientspezifischen Sicherheitsinformationen und den Zugriffs-URI für die Anwendung. Die mobilen Services arbeiten üblicherweise in Kontexten miteinander, sodass Kontextinformationen wie z. B. der Name des Anwendungsentwicklers oder des Benutzers, der die Anwendung verwendet, in der gesamten Servicegruppe genutzt werden kann.
* Für die Interaktion mit Webanwendungen oder serverseitigem Cloud-Code für mobile Anwendungen verwenden Sie die Informationen, die {{site.data.keyword.Bluemix_notm}} bereitstellt, wie z. B. die Laufzeitberechtigungsnachweise in der Umgebungsvariablen *VCAP_SERVICES* der Anwendung. Der Wert für die Umgebungsvariable *VCAP_SERVICES* ist die Serialisierung eines JSON-Objekts. Die Variable enthält die erforderlichen Laufzeitdaten für die Interaktion mit den Services, an die die Anwendung gebunden ist. Das Format der Daten ist für die verschiedenen Services unterschiedlich. Um zu erfahren, was Sie zu erwarten haben und wie die einzelnen Informationen einzuordnen sind, sollte möglicherweise die Servicedokumentation zu Rate gezogen werden.

Wenn ein Service, den Sie an eine Anwendung binden, ausfällt, wird die Ausführung der Anwendung möglicherweise gestoppt oder die Anwendung weist Fehler auf. {{site.data.keyword.Bluemix_notm}} führt keinen automatischen Neustart für die Anwendung durch, um die Probleme zu beheben. Sie sollten in Erwägung ziehen, Ihre Anwendung zu codieren, damit eine Erkennung der Fehler möglich ist und der Systembetrieb nach einer Störung, nach Ausnahmebedingungen oder Verbindungsfehlern wiederhergestellt werden kann. Weitere Informationen finden Sie im Abschnitt, in dem beschrieben wird, dass [Apps nicht automatisch neu gestartet werden](../troubleshoot/index.html#ts_topmenubar).

## Externen Apps die Verwendung von {{site.data.keyword.Bluemix_notm}}-Services ermöglichen
{: #accser_external}

Möglicherweise verfügen Sie über Anwendungen, die außerhalb von {{site.data.keyword.Bluemix_notm}} eingerichtet und in Betrieb genommen wurden, oder Sie verwenden Tools anderer Hersteller. Sofern ein {{site.data.keyword.Bluemix_notm}}-Service Endpunkte zur Verfügung stellt, die über das Internet zugänglich sind, können Sie diese Services mit Ihren lokalen Anwendungen oder Tools anderer Hersteller verwenden.

Um einer externen App oder einem Tool eines anderen Herstellers die Verwendung eines {{site.data.keyword.Bluemix_notm}}-Service zu ermöglichen, führen Sie die folgenden Schritte durch:

1. Fordern Sie eine Instanz des Service an.
    1. Klicken Sie auf dem Dashboard in der Benutzerschnittstelle von {{site.data.keyword.Bluemix_notm}} auf **Services oder APIs verwenden**. Daraufhin wird der Katalog angezeigt.
    2. Wählen Sie im Katalog den gewünschten Service aus, indem Sie auf die Kachel für den Service klicken. Die Seite mit den Servicedetails wird geöffnet.
    3. Lassen Sie im Fenster 'Service hinzufügen' für die Liste **App**: die Option **Nicht binden** ausgewählt. Diese Auswahl bedeutet, dass keine Verbindung zwischen dem Service und einer {{site.data.keyword.Bluemix_notm}}-App hergestellt wird.
    4. Wählen Sie die anderen Optionen je nach Bedarf entsprechend aus. Klicken Sie anschließend auf **Erstellen**. Es wird eine Serviceinstanz erstellt und das Service-Dashboard wird angezeigt.
2. Im linken Navigationsbereich des Service-Dashboards können Sie die Option **Serviceberechtigungsnachweise** auswählen, um Berechtigungsnachweise im JSON-Format anzuzeigen oder hinzuzufügen. Verwenden Sie den angezeigten API-Schlüssel als Berechtigungsnachweise zur Herstellung einer Verbindung zu der Serviceinstanz.

Ihre Anwendung, die außerhalb von {{site.data.keyword.Bluemix_notm}} ausgeführt wird, kann nun auf den {{site.data.keyword.Bluemix_notm}}-Service zugreifen.

**Hinweis:** Wenn Sie Serviceinstanzen löschen oder die Rechnungsangaben überprüfen möchten, müssen Sie zu Ihrem Dashboard in der Benutzerschnittstelle zurückkehren, um die Serviceinstanzen zu verwalten.

## Vom Benutzer zur Verfügung gestellte Serviceinstanz erstellen
{: #user_provide_services}

Sie verfügen möglicherweise über Ressourcen, die außerhalb von {{site.data.keyword.Bluemix_notm}} verwaltet werden. Wenn Sie über Berechtigungsnachweise für den Zugriff auf solche externen Ressourcen über das Internet verfügen, können Sie vom Benutzer zur Verfügung gestellte {{site.data.keyword.Bluemix_notm}}-Serviceinstanzen erstellen, die Ihre externen Ressourcen darstellen und die Kommunikation mit diesen Ressourcen ermöglichen.

Führen Sie die folgenden Schritte aus, um eine vom Benutzer zur Verfügung gestellte Serviceinstanz zu erstellen und an eine Anwendung zu binden:

1. Erstellen Sie eine vom Benutzer zur Verfügung gestellte Serviceinstanz entweder mit dem Befehl **cf create-user-provided-service** oder mit dem Befehl **cf cups**:
    * Verwenden Sie zum Erstellen einer allgemeinen, vom Benutzer zur Verfügung gestellten Serviceinstanz die Option **-p** und trennen Sie die Parameternamen durch Kommas. Die cf-Befehlszeilenschnittstelle fordert Sie dann nacheinander zum Angeben der einzelnen Parameter auf. Beispiel:
        ```
        cf cups testups1 -p "host, port, dbname, username, password"
        host> pubsub01.example.com
        port> 1234
        dbname> sampledb01
        username> pubsubuser
        password> p@$$w0rd
        Creating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * Um eine Serviceinstanz zu erstellen, die Informationen an eine Protokollmanagementsoftware eines Drittanbieters weitergibt, verwenden Sie die Option **-l** und geben Sie das von der Protokollmanagementsoftware des Drittanbieters bereitgestellte Ziel an. Beispiel:

        ```
        cf cups testups2 -l syslog://example.com
        Creating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

    Wenn Sie einen oder mehrere Parameter der vom Benutzer zur Verfügung gestellten Serviceinstanz aktualisieren möchten, verwenden Sie entweder den Befehl **cf update-user-provided-service** oder den Befehl **cf uups**.

    * Verwenden Sie zum Aktualisieren einer allgemeinen, vom Benutzer zur Verfügung gestellten Serviceinstanz die Option **-p** und geben Sie die Parameterschlüssel und -werte in einem JSON-Objekt an. Beispiel:

        ```
        cf uups testups1 -p "{\"username\":\"pubsubuser2\",\"password\":\"p@$$w0rd2\"}"
        Updating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * Um eine Serviceinstanz zu erstellen, die Informationen an eine Protokoll-Management-Software eines Drittanbieters weitergibt, verwenden Sie die Option -l. Beispiel:

        ```
        cf uups testups2 -l syslog://example2.com
        Updating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

2. Binden Sie die Serviceinstanz mit dem Befehl 'cf bind-service' an Ihre Anwendung. Beispiel:

	```
	cf bind-service myapp testups1
	Binding service testups1 to app myapp in org my-org / space dev as user@sample.com...
	OK
	```

Sie können Ihre Anwendung nun für die Verwendung der externen Ressourcen konfigurieren. Informationen zum Konfigurieren Ihrer Anwendung für die Interaktion mit einem Service finden Sie unter [Anwendung für die Interaktion mit einem Service konfigurieren](#config){: new_window}.

## Services in einer anderen Region verwenden
{: #cross_region_service}

Wenn Sie über eine Serviceinstanz verfügen, die erstellt und an Apps in einer einzigen Region gebunden wurde, können Sie diese Serviceinstanz mit einer der folgenden Methoden in einer anderen Region verwenden:

  * Verwenden Sie die Serviceberechtigungsnachweise, um Ihre App-Instanz direkt zu konfigurieren. Details finden Sie unter [Externen Apps die Verwendung von {{site.data.keyword.Bluemix_notm}}-Services ermöglichen](#accser_external){: new_window}.
  * Erstellen Sie einen vom Benutzer bereitgestellten Service als Bridge.
    
	Angenommen, Sie beginnen in der Region, in der Sie die Serviceinstanz verwenden möchten. Führen Sie die folgenden Schritte aus, um eine Serviceinstanz zu verwenden, die in einer anderen Region existiert:

      1. Wechseln Sie in die Region, in der die Serviceinstanz existiert. Erweitern Sie in der oberen Menüleiste von {{site.data.keyword.Bluemix_notm}} die Option **Region** oder klicken Sie auf das Symbol für **Region** und wählen Sie anschließend die Region aus, in der sich die Serviceinstanz befindet.

      2. Rufen Sie die Berechtigungsnachweise und Verbindungsparameter aus der Umgebungsvariablen VCAP_SERVICES der Serviceinstanz in der Region ab, in der sich der Service befindet. Führen Sie die folgenden Schritte aus:

	       1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf die Anwendungskachel. Die Übersichtsseite wird angezeigt.
	       2. Klicken Sie im linken Navigationsbereich auf **Umgebungsvariablen**. Die Details zur Umgebungsvariablen *VCAP_SERVICES* werden im rechten Fensterbereich angezeigt. Dokumentieren Sie den JSON-Inhalt für die Serviceinstanz.

      3. Wechseln Sie zu der Region, in der Sie die Serviceinstanz verwenden möchten. Erweitern Sie in der oberen Menüleiste von {{site.data.keyword.Bluemix_notm}} die Option **Region** oder klicken Sie auf das Symbol für **Region** und wählen Sie anschließend die Region aus, in der Sie die Serviceinstanz verwenden möchten.

      4. Erstellen Sie eine vom Benutzer zur Verfügung gestellte Serviceinstanz, indem Sie die Berechtigungsnachweise und Verbindungsparameter verwenden, die Sie aus der Umgebungsvariablen *VCAP_SERVICES* aufgezeichnet haben. Informationen zur Erstellung einer vom Benutzer bereitgestellten Serviceinstanz finden Sie im Abschnitt zur [Erstellung einer vom Benutzer bereitgestellten Serviceinstanz](#user_provide_services){: new_window}.

      5. Binden Sie die vom Benutzer bereitgestellte Serviceinstanz mit dem folgenden Befehl an Ihre App:

	     ```
	     cf bind-service myapp user-provided_service_instance
	     ```






## Services in einem anderen Service verwenden
{: #s2s_binding}

Mit der Berechtigung für den Servicezugriff kann ein Service direkt auf einen anderen zugreifen. Sie können den Zugriff einer Serviceinstanz auf andere Serviceinstanzen über das {{site.data.keyword.Bluemix_notm}}-Dashboard autorisieren und konfigurieren.

Führen Sie die folgenden Schritte aus, um eine Serviceinstanz von einem anderen Service zu verwenden:

1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf die Kachel für den Service, auf den Sie zugreifen möchten. Das Dashboard für den Service wird angezeigt.
2. Klicken Sie im linken Navigationsbereich auf *Verwalten von*, um das Binden von anderen Serviceinstanzen unter Verwendung der Konsole der Serviceinstanz zu autorisieren.
3. Wenn Sie den Zugriff weiterer Services auf die Serviceinstanz verhindern möchten, klicken Sie im linken Navigationsfenster auf *Berechtigung für Servicezugriff* und entfernen Sie die Servicebindung anschließend mithilfe von *Widerrufen*. 

# Zugehörige Links
{: #rellinks}

## Allgemein
{: #general}

* [Service mithilfe der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle binden](../cfapps/ee.html#ee_bindui)
* [VCAP_SERVICES abrufen](../cli/vcapsvc.html#retrieving)


