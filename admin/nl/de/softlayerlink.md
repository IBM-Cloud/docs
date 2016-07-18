---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

<!-- draft - staging only -->

#SoftLayer- und {{site.data.keyword.Bluemix_notm}}-Abrechnungskonten verknüpfen
{: #softlayerlink}
*Letzte Aktualisierung: 10. Juni 2016*
{: .last-updated}

Sie können nun die SoftLayer- und {{site.data.keyword.Bluemix_notm}}-Abrechnungskonten verknüpfen. Wenn Sie die Konten verknüpfen, erfolgt die Rechnungsstellung sowohl für SoftLayer- als auch für {{site.data.keyword.Bluemix_notm}}-Ressourcen über SoftLayer. Wenn Sie über ein bestehendes Konto verfügen, erfolgt die Rechnungsstellung für {{site.data.keyword.Bluemix_notm}} über SoftLayer ab dem neuen Abrechnungszyklus, der nach dem Verknüpfen der Konten beginnt.
{:shortdesc}

**Wichtig:** Alle verknüpften Konten in {{site.data.keyword.Bluemix_notm}} müssen nutzungsabhängige Konten sein. Sie können ein neues nutzungsabhängiges Konto erstellen oder ein bestehendes nutzungsabhängiges Konto verknüpfen. Sie können auch ein bestehendes Testkonto verknüpfen, das dann in ein nutzungsabhängiges Konto umgewandelt wird.  

Nachdem die Konten verknüpft wurden, kann die Nutzung der {{site.data.keyword.Bluemix_notm}}-Ressourcen weiterhin in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle überwacht werden. Diese Ressourcen werden nun allerdings über die SoftLayer-Rechnung abgerechnet.

Obwohl die Kontoabrechnung verknüpft ist und Sie problemlos zwischen den Konten wechseln können, benötigen Sie weiterhin separate IDs für {{site.data.keyword.Bluemix_notm}} und SoftLayer. Verwenden Sie Ihre SoftLayer-ID weiterhin für SoftLayer-Produkte und -Services und die IBM ID für {{site.data.keyword.Bluemix_notm}}-Produkte und -Services. 

**Achtung:** Das Verknüpfen der Konten kann nicht rückgängig gemacht werden.  

Wenn Sie über ein SoftLayer-Konto verfügen und die SoftLayer- und {{site.data.keyword.Bluemix_notm}}-Konten verknüpfen möchten, führen Sie die folgenden Schritte aus:
 1. Klicken Sie im {{site.data.keyword.slportal}} auf **{{site.data.keyword.Bluemix_notm}}-Konto verknüpfen**. 
 2. Lesen und akzeptieren Sie die Bedingungen für das Verknüpfen von SoftLayer- und {{site.data.keyword.Bluemix_notm}}-Konten.
 3. Geben Sie nach entsprechender Aufforderung die E-Mail-Adresse an, die Ihrem {{site.data.keyword.Bluemix_notm}}-Konto zugeordnet ist. Wenn Sie über kein {{site.data.keyword.Bluemix_notm}}-Konto verfügen, geben Sie die von Ihnen gewünschte E-Mail-Adresse an und befolgen Sie die Anweisungen für die Einladung zu {{site.data.keyword.Bluemix_notm}} und das Erstellen eines Kontos.

Sie müssen ein Masterbenutzer des SoftLayer-Kontos sein, um Konten verknüpfen zu können.

Wenn die Konten verknüpft sind, wird im globalen Header von SoftLayer der Link **Zu {{site.data.keyword.Bluemix_notm}} wechseln** angezeigt. Wenn Sie auf diesen Link klicken, wird die {{site.data.keyword.Bluemix_notm}}-Anmeldeseite geöffnet. Ferner wird nun der Link **SoftLayer** im {{site.data.keyword.Bluemix_notm}}-Header angezeigt. Wenn Sie auf diesen Link klicken, wird die Homepage von {{site.data.keyword.slportal}} in einem neuen Fenster geöffnet.


## Guthaben für {{site.data.keyword.Bluemix_notm}}-Nutzung bei Verknüpfung der Konten
{: #slcredit}

Wenn Sie die {{site.data.keyword.Bluemix_notm}}- und SoftLayer-Abrechnungskonten verknüpfen, erhalten Sie ein Guthaben von $ 200,00 für die {{site.data.keyword.Bluemix_notm}}-Nutzung. Das Guthaben muss innerhalb von 30 Tagen nach dem Verknüpfen der Konten aufgebraucht werden.

Weitere Informationen zum Anzeigen von Guthaben und deren Ablaufdatum finden Sie unter [Guthaben anzeigen](https://console.ng.bluemix.net/docs/pricing/index.html#credits).

## SoftLayer-Teammitglieder zu {{site.data.keyword.Bluemix_notm}} einladen
{: #invite_users}

Beim Verknüpfen der {{site.data.keyword.Bluemix_notm}}- und SoftLayer-Konten können Sie die SoftLayer-Teammitglieder zur Teilnahme an {{site.data.keyword.Bluemix_notm}} einladen. Sie können die SoftLayer-Teammitglieder auch später über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle einladen.
{:shortdesc}

In der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle können Sie entweder alle oder einzelne Mitglieder des SoftLayer-Kontos einladen. Bei der Einladung von Teammitgliedern müssen Sie die {{site.data.keyword.Bluemix_notm}}-Kontorolle für die eingeladenen Personen festlegen. Weitere Informationen zu den verschiedenen Rollen in {{site.data.keyword.Bluemix_notm}} finden Sie unter [Benutzerrollen](https://console.ng.bluemix.net/docs/admin/users_roles.html#userrolesinfo).

Sie müssen ein Masterbenutzer des SoftLayer-Kontos sein, um Teammitglieder zum {{site.data.keyword.Bluemix_notm}}-Konto einzuladen.

Gehen Sie wie folgt vor, um Teammitglieder über {{site.data.keyword.Bluemix_notm}} einzuladen:
 1. Klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](images/account_support.svg) > **Konten** > **Teammitglieder einladen**.
 2. Klicken Sie auf **Hinzufügen**, um sich für das SoftLayer-Konto zu authentifizieren und eine Liste der Teammitglieder aus dem SoftLayer-Konto anzuzeigen.
 3. Wählen Sie die gewünschten Teammitglieder aus und klicken Sie auf **Senden**.

Sie können diese Operation für jedes weitere Teammitglied wiederholen, das Ihrem Softlayer-Konto hinzugefügt wird.
 
Das Teammitglied empfängt eine E-Mail mit einem Link zur **Teilnahme an der Organisation**. Wenn das Mitglied über keine IBM ID verfügt, wird es zur Registrierungsseite weitergeleitet. Als Nächstes kann das Teammitglied einige Basisinformationen eingeben und ein {{site.data.keyword.Bluemix_notm}}-Konto erstellen.

Weitere Informationen zum Einladen von Teammitgliedern über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle finden Sie unter [Teammitglieder einladen](https://console.ng.bluemix.net/docs/admin/users_roles.html#inviteteammembers).

## {{site.data.keyword.Bluemix_notm}}-Services mit SoftLayer-Assets verwenden
{: #bluemix_services}

Es ist einfach, API-basierte öffentliche {{site.data.keyword.Bluemix_notm}}-Services mit den SoftLayer-Assets zu verwenden. Alle APIs sind gesichert und verschlüsselt, damit Ihre Daten geschützt sind.
{:shortdesc}

Wollten Sie vielleicht schon einmal die kognitiven Fähigkeiten von Watson in Apps einfügen, die auf Bare-Metal-Servern über SoftLayer ausgeführt werden? Sie können in vier einfachen Schritten einen Service wie {{site.data.keyword.personalityinsightsshort}} hinzufügen, um den Benutzer Ihrer App besser zu verstehen:

1. Suchen Sie den Service im {{site.data.keyword.Bluemix_notm}}-Katalog.
2. Stellen Sie eine Instanz des Service bereit. Dazu sind nur einige Klicks notwendig.
3. Konfigurieren Sie den Service für die Ausführung mit dem bereits vorhandenen Code, indem Sie die Berechtigungsnachweise des Service kopieren und diese zur Anwendung hinzufügen.
4. Nach der Aktualisierung der App können Sie die neue Version in der SoftLayer-Infrastruktur bereitstellen.

Erweitern Sie Ihr Insights- und Ihr kognitives Wissen, indem Sie Watson-APIs über Ihre Apps in SoftLayer aufrufen, um diese stärker zu personalisieren. Oder nutzen Sie die Daten- und Analyseservices, um leistungsstarke Analysen für Ihre Apps auszuführen. Sie können sich auch für Database as a Service entscheiden und das Management {{site.data.keyword.Bluemix_notm}} überlassen.

Modernisieren Sie die Anwendungsentwicklung unter Verwendung von Containern mit Services wie {{site.data.keyword.activedeployshort}} und {{site.data.keyword.deliverypipeline}}. Sie können dann mit dem {{site.data.keyword.vpn_short}}-Service per Tunnelung zu SoftLayer zurückkehren, um den Container in einem privaten Netz mit dem privaten SoftLayer-Netz zu verbinden. Alle Nutzungsgebühren für Rechenressourcen und -services werden über die SoftLayer-Rechnung abgerechnet. 

### API-basierte {{site.data.keyword.Bluemix_notm}}-Services
Mit SoftLayer können nicht alle {{site.data.keyword.Bluemix_notm}}-Services verwendet werden. Die folgenden Services können zur Ausführung mit dem Anwendungscode eingerichtet werden:
* {{site.data.keyword.alchemyapishort}}
* {{site.data.keyword.alertnotificationshort}}
* {{site.data.keyword.sparks}}
* {{site.data.keyword.appseccloudshort}}
* {{site.data.keyword.blockchain}}
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.conceptinsightsshort}}
* {{site.data.keyword.iotmapinsights_short}}
* {{site.data.keyword.dashdbshort}}
* {{site.data.keyword.dialogshort}}
* {{site.data.keyword.documentconversionshort}}
* {{site.data.keyword.twittershort}}
* {{site.data.keyword.weather_short}}
* {{site.data.keyword.iotdriverinsights_short}}
* {{site.data.keyword.geospatialshort_Geospatial}}
* {{site.data.keyword.graphshort}}
* {{site.data.keyword.iotelectronics}}
* {{site.data.keyword.languagetranslationshort}}
* {{site.data.keyword.messagehub}}
* {{site.data.keyword.mqa}}
* {{site.data.keyword.mobileappbuilder_short}}
* {{site.data.keyword.mql}}
* {{site.data.keyword.nlclassifierlshort}}
* {{site.data.keyword.objectstorageshort}}
* {{site.data.keyword.personalityinsightsshort}}
* {{site.data.keyword.presenceinsightsshort}}
* {{site.data.keyword.relationshipextractionshort}}
* {{site.data.keyword.retrieveandrankshort}}
* {{site.data.keyword.servicediscoveryshort}}
* {{site.data.keyword.speechtotextshort}}
* {{site.data.keyword.sqldb}}
* {{site.data.keyword.streaminganalyticsshort}}
* {{site.data.keyword.texttospeechshort}}
* {{site.data.keyword.toneanalyzershort}}
* {{site.data.keyword.tradeoffanalyticsshort}}
* {{site.data.keyword.visualinsightsshort}}
* {{site.data.keyword.visualrecognitionshort}}
* {{site.data.keyword.workflow}}
* {{site.data.keyword.workloadscheduler}}

**Hinweis:** Nicht alle Pläne für diese Services sind verfügbar. Für verknüpfte Konten können nur die für nutzungsabhängige Konten aktivierten Pläne verwendet werden. Wenn Sie jedoch über ein separates {{site.data.keyword.Bluemix_notm}}-Konto mit separater Rechnungsstellung verfügen, können Sie für diese Services jeden beliebigen Plan verwenden.


## Rechnungsstellung für {{site.data.keyword.Bluemix_notm}}-Nutzung bei verknüpften Konten
{: #bill_usage}

Nach der Verknüpfung Ihrer {{site.data.keyword.Bluemix_notm}}- und SoftLayer-Abrechnungskonten erfolgt die Rechnungsstellung im nächsten Abrechnungszyklus über eine einzige SoftLayer-Rechnung.
{:shortdesc}

Der {{site.data.keyword.Bluemix_notm}}-Nutzungszyklus basiert auf Kalendermonaten, sodass Rechnungen für Ihr Konto monatlich zum Monatsersten erstellt werden. Bei SoftLayer beginnt der Nutzungszyklus mit dem Beginn der SoftLayer-Nutzung, sodass die Rechnungsstellung jeden Monat an dem Tag erfolgt, an dem Sie sich für Ihr SoftLayer-Konto angemeldet haben. 

Wenn Sie Ihre Konten verknüpfen, wird die {{site.data.keyword.Bluemix_notm}}-Nutzung für den aktuellen Monat noch wie bisher abgerechnet und Sie erhalten für diesen Nutzungszeitraum eine {{site.data.keyword.Bluemix_notm}}-Rechnung. Ab dem ersten des nächsten Monats werden Ihre {{site.data.keyword.Bluemix_notm}}-Gebühren über die SoftLayer-Rechnung abgerechnet.

Wenn Sie Ihre Konten beispielsweise am 16. April verknüpft haben, erhalten Sie für die Nutzung im April eine Bluemix-Rechnung. Der Monat Mai wird dann über das SoftLayer-Konto abgerechnet.

![Verknüpfung von Bluemix- und SoftLayer-Konten - Zusammenfassung](images/BluemixSoftLayerBill.svg)

Nach dem Zusammenführen der Rechnungen ist auf der SoftLayer-Rechnung in der Zusammenfassungsansicht ein Abschnitt **{{site.data.keyword.Bluemix_notm}}** enthalten. In der detaillierten Abrechnungsansicht werden die {{site.data.keyword.Bluemix_notm}}-Gebühren als sonstige Services aufgeführt und beginnen mit *"{{site.data.keyword.Bluemix_notm}} Plan..."*.

Informationen zum Anzeigen der {{site.data.keyword.Bluemix_notm}}-Nutzung finden Sie unter [Nutzungsdetails anzeigen](https://console.ng.bluemix.net/docs/pricing/index.html#usage).


# Zugehörige Links
## Allgemein
* [Video: Link SoftLayer and Bluemix Accounts For a Single Invoice](https://www.youtube.com/watch?v=Xb01idt2NiU&index=1&list=PLzpeuWUENMK2d3L5qCITo2GQEt-7r0oqm)
