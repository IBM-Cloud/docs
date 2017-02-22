---

 

copyright:

  years: 2016, 2017
lastupdated: "2017-01-11"
 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Abrechnungskonten für {{site.data.keyword.Bluemix_notm}} und SoftLayer aktualisieren und zusammenführen
{: #softlayerlink}

Wenn Sie über ein {{site.data.keyword.Bluemix_notm}}-Testkonto verfügen und auf das Infrastruktur-Dashboard zugreifen möchten, müssen Sie Ihr Konto auf ein nutzungsabhängiges {{site.data.keyword.Bluemix_notm}}-Konto aktualisieren. Ein Upgrade ist auch dann erforderlich, wenn Sie weitere gebührenpflichtige Ressourcen nutzen wollen, die nicht im Rahmen eines Testkontos verfügbar sind, oder wenn Ihr Testkonto endet. 

Sie können Ihre bestehenden {{site.data.keyword.Bluemix_notm}}- und SoftLayer-Abrechnungskonten zusammenführen, indem Sie die Konten verknüpfen. Wenn Sie die Konten verknüpfen, werden sowohl die {{site.data.keyword.Bluemix_notm}}- als auch die SoftLayer-Ressourcen über {{site.data.keyword.Bluemix_notm}} in Rechnung gestellt.

**Achtung:** Ein {{site.data.keyword.Bluemix_notm}}-Abonnementkonto kann nicht mit einem SoftLayer-Konto verknüpft werden. Um auf das Infrastruktur-Dashboard zuzugreifen, müssen Sie ein nutzungsabhängiges Konto erstellen. Dabei handelt es sich um ein zweites Konto, das automatisch mit einem SoftLayer-Konto verknüpft wird. Daraufhin erhalten Sie zwei separate Rechnungen für die beiden {{site.data.keyword.Bluemix_notm}}-Konten. Obwohl die Rechnungsstellung für Ihre Infrastrukturressourcen in einem separaten nutzungsabhängigen Konto erfolgt, können die Ressourcen mit Apps und Services in Ihrem Abonnementkonto verwendet werden. Wenn Sie beispielsweise einen Watson-Service in Ihrem Abonnementkonto aktivieren, dann können Sie die Serviceberechtigungsnachweise kopieren und die Berechtigungsnachweise dann zu Ihrer Bare-Metal-Anwendung hinzufügen, die aus dem nutzungsabhängigen Konto abgeleitet wird. 
{:shortdesc}

## Aktualisierung auf ein nutzungsabhängiges {{site.data.keyword.Bluemix_notm}}-Konto
{: #upgradetopayg}

Wenn Sie sich mit einem Testkonto bei {{site.data.keyword.Bluemix_notm}} anmelden, können Sie nicht auf das {{site.data.keyword.Bluemix_notm}}-Infrastruktur-Dashboard zugreifen. Wenn Ihre Apps die Infrastrukturressourcen nutzen sollen, müssen Sie Ihr Konto auf ein nutzungsabhängiges Konto aktualisieren.

Zum Aktualisieren Ihres Testkontos auf ein nutzungsabhängiges {{site.data.keyword.Bluemix_notm}}-Konto gehen Sie folgendermaßen vor:

 1. Klicken Sie auf **Konto** &gt; **Abrechnung**.
 2. Anschließend klicken Sie auf **Kreditkarte hinzufügen**.
 3. Geben Sie die erforderlichen Abrechnungsdetails ein. 
 4. Lesen und akzeptieren Sie die Vertragsbedingungen für das nutzungsabhängige Konto. 
 5. Wenn Sie damit fertig sind, klicken Sie auf **Konto aktualisieren**. 
 
Nachdem Sie die Aktualisierung auf ein nutzungsabhängiges Konto durchgeführt haben, werden die **Infrastruktur**-Optionen im {{site.data.keyword.Bluemix_notm}}-**Katalog** aufgelistet. Wenn Sie in Ihrer Nutzung über die gebührenfreien Leistungen hinausgehen, erhalten Sie eine {{site.data.keyword.Bluemix_notm}}-Rechnung für den Monat. Die Rechnung wird in USD ausgestellt und enthält die Details zu Ihren Ressourcengebühren. 

## Konten für {{site.data.keyword.Bluemix_notm}} und SoftLayer zusammenführen
{: #unifyingaccounts}

Sie können Ihr {{site.data.keyword.Bluemix_notm}}- und Ihr SoftLayer-Konto zusammenführen, um die Ressourcen beider Konten zu nutzen. Wenn Sie Ihr {{site.data.keyword.Bluemix_notm}}- und Ihr Softlayer-Konto miteinander verknüpfen, erhalten Sie nur eine {{site.data.keyword.Bluemix_notm}}-Abrechnung. Wenn Sie über ein bestehendes {{site.data.keyword.Bluemix_notm}}-Konto verfügen, erfolgt die Rechnungsstellung über {{site.data.keyword.Bluemix_notm}} ab dem neuen Abrechnungszyklus, der nach dem Verknüpfen der Konten beginnt.

**Wichtig:** Alle verknüpften Konten in {{site.data.keyword.Bluemix_notm}} müssen nutzungsabhängige Konten sein. Sie können ein neues nutzungsabhängiges Konto erstellen oder ein bestehendes nutzungsabhängiges Konto verknüpfen. Sie können auch ein bestehendes Testkonto verknüpfen, das dann in ein nutzungsabhängiges Konto umgewandelt wird. {{site.data.keyword.Bluemix_notm}}-Abonnementkonten können nicht verknüpft werden.  

Nach dem Verknüpfen Ihrer Konten gilt Folgendes:

* Für den Zugriff sowohl auf das SoftLayer- als auch auf das {{site.data.keyword.Bluemix_notm}}-Konto müssen Sie Ihre IBMid-Berechtigungsnachweise verwenden.
* Alle bestehenden SoftLayer-Rabatte werden auf alle {{site.data.keyword.Bluemix_notm}}-Gebühren angewandt. 
* Sie erhalten nur eine Rechnung; diese ist in USD ausgestellt.
* Sie können die Nutzung der {{site.data.keyword.BluSoftlayer}}-Ressourcen in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle überwachen. 

**Achtung:** Das Verknüpfen der Konten kann nicht rückgängig gemacht werden. 

Wenn Sie über ein SoftLayer-Konto verfügen und die SoftLayer- und {{site.data.keyword.Bluemix_notm}}-Konten verknüpfen möchten, führen Sie die folgenden Schritte aus:

 1. Klicken Sie im {{site.data.keyword.slportal}} auf **{{site.data.keyword.Bluemix_notm}}-Konto verknüpfen**.
 2. Lesen und akzeptieren Sie die Bedingungen für das Verknüpfen von SoftLayer- und {{site.data.keyword.Bluemix_notm}}-Konten.
 3. Geben Sie nach entsprechender Aufforderung die E-Mail-Adresse an, die Ihrem {{site.data.keyword.Bluemix_notm}}-Konto zugeordnet ist. Wenn Sie über kein {{site.data.keyword.Bluemix_notm}}-Konto verfügen, geben Sie die von Ihnen gewünschte E-Mail-Adresse an und befolgen Sie die Anweisungen für die Einladung zu {{site.data.keyword.Bluemix_notm}} und das Erstellen eines Kontos.

Sie müssen ein Masterbenutzer des SoftLayer-Kontos sein, um Konten verknüpfen zu können.

Wenn die Konten verknüpft sind, wird im globalen Header von Softlayer der Link **Zu {{site.data.keyword.Bluemix_notm}} wechseln** angezeigt. Wenn Sie auf diesen Link klicken, wird die {{site.data.keyword.Bluemix_notm}}-Anmeldeseite geöffnet. Zusätzlich wird nun der Link **SoftLayer** im {{site.data.keyword.Bluemix_notm}}-Header angezeigt. Wenn Sie auf diesen Link klicken, wird die Homepage von {{site.data.keyword.slportal}} in einem neuen Fenster geöffnet.

Die Angebote der {{site.data.keyword.Bluemix_notm}}-Infrastruktur sind mit einem dreischichtigen Netz verbunden, das den Datenverkehr in öffentlichen, privaten und Managementdatenverkehr segmentiert. Infrastrukturangebote für ein {{site.data.keyword.Bluemix_notm}}-Kundenkonto übertragen im privaten Netz möglicherweise Daten kostenfrei untereinander. Infrastrukturangebote, z. B. Bare-Metal-Server, virtuelle Server und Cloudspeicherung, stellen Verbindungen zu anderen Anwendungen und Services im {{site.data.keyword.Bluemix_notm}}-Katalog her, z. B. Watson-Services, Container oder Laufzeiten im ganzen öffentlichen Netz. Die Datenübertragung zwischen diesen zwei Angebotstypen wird gemessen und zu Standardpreisen für die öffentliche Netzbandbreite berechnet.

## SoftLayer-Teammitglieder zu {{site.data.keyword.Bluemix_notm}} einladen
{: #invite_users}

Beim Verknüpfen der {{site.data.keyword.Bluemix_notm}}- und SoftLayer-Konten können Sie die SoftLayer-Teammitglieder zur Teilnahme an {{site.data.keyword.Bluemix_notm}} einladen. Sie können die SoftLayer-Teammitglieder auch später über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle einladen.
{:shortdesc}

In der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle können Sie entweder alle oder einzelne Mitglieder des SoftLayer-Kontos einladen. Bei der Einladung von Teammitgliedern müssen Sie die {{site.data.keyword.Bluemix_notm}}-Kontorolle für die eingeladenen Personen festlegen. Weitere Informationen zu den verschiedenen Rollen in {{site.data.keyword.Bluemix_notm}} finden Sie unter [Benutzerrollen](https://console.ng.bluemix.net/docs/admin/users_roles.html#userrolesinfo).

Sie müssen ein Masterbenutzer des SoftLayer-Kontos sein, um Teammitglieder zum {{site.data.keyword.Bluemix_notm}}-Konto einzuladen.

Führen Sie die folgenden Schritte aus, um Teammitglieder über {{site.data.keyword.Bluemix_notm}} einzuladen:

 1. Klicken Sie auf **Konto** &gt; **Teammitglieder einladen**.
 2. Klicken Sie auf **Hinzufügen**, um sich für das SoftLayer-Konto zu authentifizieren und eine Liste der Teammitglieder aus Ihrem {{site.data.keyword.BluSoftlayer}}-Konto anzuzeigen.
 3. Wählen Sie die gewünschten Teammitglieder aus und klicken Sie auf **Senden**.
 
Das Teammitglied empfängt eine E-Mail mit einem Link zur **Teilnahme an der Organisation**. Wenn das Teammitglied über keine IBMid verfügt, wird es zur Registrierungsseite weitergeleitet. Danach kann das Teammitglied einige Basisinformationen eingeben und ein eigenes {{site.data.keyword.Bluemix_notm}}-Konto erstellen.

Weitere Informationen zum Einladen von Teammitgliedern über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle finden Sie unter [Teammitglieder einladen](https://console.ng.bluemix.net/docs/admin/users_roles.html#inviteteammembers).

## Zur IBMid wechseln
{: #ibmid_switch}

Für die Authentifizierung in SoftLayer wird jetzt eine IBMid verwendet, die eine einzige Anmeldung bei allen {{site.data.keyword.Bluemix_notm}}-Komponenten ermöglicht. Es wird ein Wechsel für vorhandene SoftLayer-Konten zur IBMid-Authentifizierung ermöglicht und Sie werden von einem Migrationsassistenten durch diesen Wechsel geführt. 
{:shortdesc}

Wenn Sie Masterbenutzer sind und keine Aufforderung zum Wechsel zur IBMid im {{site.data.keyword.slportal}} angezeigt wird, [wenden Sie sich an den IBM Support](https://console.ng.bluemix.net/docs/support/index.html#contacting-support), um Hilfe zum Aktivieren dieser Funktion zu erhalten.

Sie können diesen Wechsel zur IBMid jederzeit abbrechen, solange der Prozess noch nicht abgeschlossen ist. Sie werden dann jedoch weiterhin aufgefordert, bei Ihrer nächsten Anmeldung zur IBMid zu wechseln. Jedes Konto, das mit einem {{site.data.keyword.Bluemix_notm}}-Konto verknüpft werden soll, muss zu einer eindeutigen IBMid mit einer eindeutigen E-Mail-Adresse gehören.

Führen Sie folgende Schritte aus, um von Ihrem bisherigen SoftLayer-Benutzernamen zu einer IBMid zu wechseln:

 1. Wenn Sie bei der ersten Eingabeaufforderung nach der Anmeldung **Später** ausgewählt, sich aber dann dazu entschlossen haben, den Wechsel zur IBMid-Authentifizierung in der aktuellen Sitzung zu beginnen, navigieren Sie zur Seite zum Bearbeiten des Benutzerprofils und klicken Sie auf **Zu IBMid wechseln**.
 2. Befolgen Sie die Anweisungen im Assistenten, um Ihre IBMid zu erstellen. Ihre IBMid ist eine eindeutige E-Mail-Adresse und kann nach der Erstellung nicht mehr geändert werden. Sie können die E-Mail-Adresse, die Ihrem Profil zugeordnet ist, später aktualisieren, aber die Standard-E-Mail-Adresse ist auf Ihre IBMid festgelegt. Sie erhalten eine E-Mail mit Ihrem Registrierungscode, sobald Sie den Migrationsassistenten abgeschlossen haben. 
 3. Wenn Sie die E-Mail erhalten, folgen Sie dem Link oder kopieren Sie die URL in einen Browser und geben Sie Ihren Registrierungscode ein. Der Code ist 7 Tage lang gültig und kann nur einmal verwendet werden.
 
 
Nachdem Sie zur IBMid-Authentifizierung gewechselt haben, können Sie sich nur noch mit Ihrer IBMid bei Ihrem Konto anmelden. Klicken Sie im Anmeldedialog auf **Mit IBMid anmelden**, anstatt Ihren SoftLayer-Benutzernamen und das Kennwort einzugeben.
 
Wenn Sie Ihre Bestellung als neuer Kunde auschecken, werden Sie zur Angabe einer E-Mail-Adresse für Ihr bestehendes IBMid-Konto oder zur Erstellung eines neuen IBMid-Kontos aufgefordert. Wenn Sie eine neue IBMid erstellen, geben Sie die E-Mail-Adresse für Ihre neue IBMid ein. An diese E-Mail-Adresse wird die Einladungs-E-Mail gesendet und sie ist außerdem der Benutzername für Ihre neue IBMid.

### Benutzern den Wechsel zur IBMid ermöglichen
{: #link_accounts_resellers}

In einigen Fällen muss ein Reseller oder Distributor aktivieren, dass die IBMid-Authentifizierung für ein Konto verwendet werden kann, bevor ein Benutzer zu einer IBMid wechseln kann. 

 * Um ein vorhandenes Konto mit den bisherigen SoftLayer-Berechtigungsnachweisen für die Verwendung der IBMid-Authentifizierung zu aktivieren, [wenden Sie sich an den IBM Support](https://console.ng.bluemix.net/docs/support/index.html#contacting-support), um die IBMid-Migration zu aktivieren. Diese Aktivierung ist für jedes vorhandene Endbenutzerkonto erforderlich, das mit einem {{site.data.keyword.Bluemix_notm}}-Konto verknüpft werden soll.
 
 * Um sicherzustellen, dass neue Benutzerkonten mit einer IBMid erstellt werden, muss das Attribut `CREATE_NEW_ACCOUNT_WITH_IBMid_AUTHENTICATION` auf das direkte Masterbenutzerkonto festgelegt werden. [Wenden Sie sich an den IBM Support](https://console.ng.bluemix.net/docs/support/index.html#contacting-support) oder Ihren Anbieter, um diese Einstellung für Ihre Konten vornehmen zu lassen.
 
### Benutzerkonten verknüpfen
{: #link_user_accounts}
Nachdem Ihre Benutzer zur IBMid-Authentifizierung gewechselt haben, können Reseller und Distributoren SoftLayer- und {{site.data.keyword.Bluemix_notm}}-Konten verknüpfen.

**Hinweis:** 
  * Der Masterbenutzer des Kontos, das verknüpft wird, muss eine IBMid sein.
  * Melden Sie sich bei jedem Endbenutzerkonto als Masterbenutzer an. Navigieren Sie zur Benutzerprofilseite und klicken Sie auf **Zu IBMid wechseln**.
  * Jedes Konto, das mit einem {{site.data.keyword.Bluemix_notm}}-Konto verknüpft wird, muss zu einer eindeutigen IBMid mit einer eindeutigen E-Mail-Adresse gehören. Zu einer IBMid können zwar mehrere SoftLayer-Konten gehören, jedoch können die Konten nicht mit {{site.data.keyword.Bluemix_notm}}-Konten verknüpft werden. Wenn eine IBMid der Masterbenutzer für mehrere SoftLayer-Konten ist und Sie diese Konten mit {{site.data.keyword.Bluemix_notm}}-Konten verknüpfen möchten, müssen Sie die Masterbenutzer für jedes Konto in eine jeweils eindeutige IBMid ändern. Wenden Sie sich an den [IBM SoftLayer-Support ![Symbol für externen Link](../icons/launch-glyph.svg)](https://knowledgelayer.softlayer.com/topic/support){: new_window}, um den Masterbenutzer für ein SoftLayer-Konto zu ändern.
  
Führen Sie die folgenden Schritte aus, um jedes Konto mit einem {{site.data.keyword.Bluemix_notm}}-Konto zu verknüpfen: 

 1. Um ein neues {{site.data.keyword.Bluemix_notm}}-Konto zu erstellen oder um eine Verknüpfung mit einem vorhandenen {{site.data.keyword.Bluemix_notm}}-Konto zu erstellen, melden Sie sich als Masterbenutzer bei Ihrem SoftLayer-Konto an und klicken Sie auf den **{{site.data.keyword.Bluemix_notm}}**-Link. Dadurch können Sie entweder ein neues {{site.data.keyword.Bluemix_notm}}-Konto erstellen oder eine Verknüpfung zu einem vorhandenen {{site.data.keyword.Bluemix_notm}}-Konto herstellen. Die IBMid, die der Masterbenutzer für das SoftLayer-Konto ist, muss der Eigner des Bluemix-Kontos sein, zu dem die Verknüpfung hergestellt wird. Befolgen Sie die Eingabeaufforderungen im Assistenten und fügen Sie die Benutzer im SoftLayer-Konto dem {{site.data.keyword.Bluemix_notm}}-Konto hinzu. 
 2. Nachdem Sie das Konto verknüpft haben, informieren Sie die Endbenutzer des Kontos darüber, dass sie zur IBMid migrieren müssen. Endbenutzer können dann in der {{site.data.keyword.Bluemix_notm}}-Konsole auf die Dashboards 'Infrastruktur', 'Anwendungen' und 'Services' zugreifen.
 3. Wenn dem verknüpften Konto neue Benutzer hinzugefügt werden, müssen Sie sie sowohl dem SoftLayer-Konto als auch dem {{site.data.keyword.Bluemix_notm}}-Konto hinzufügen, damit sie Zugriff auf alle Funktionen in der einheitlichen Konsole erhalten.
 
**Empfehlung:** Migrieren Sie nur die Endbenutzerkonten zur IBMid. Migrieren Sie keine Brandkonten. Dies sind übergeordnete Konten für Endbenutzerkonten und enthalten keine Ressourcen. Brandkontenbenutzer, die zur IBMid migrieren, können sich anschließend nicht mehr bei beim BAP (Brand Agent Portal) anmelden.

<!--
### Mapping multiple SoftLayer accounts to one IBMid
{: #map_multiple_accounts}

You can associate one IBMid with multiple SoftLayer accounts by using an existing IBMid email address when setting up the account. Only one SoftLayer user for each account can be mapped to the single IBMid. The IBMid must be unique within each SoftLayer account. However, one user with access to multiple SoftLayer accounts can use one IBMid to access multiple SoftLayer accounts.

For example, an IBMid can map to the master user in accounts A and B, and to an additional user in accounts C and D. One of the accounts mapped to that IBMid is the default account.  Usually, the default account is the account that was first mapped to the IBMid. However, you can switch which account is the default account  through an account switching feature in the Customer Portal.

For a user with IBMid access to multiple accounts with two-factor authentication enabled, an appropriate two-factored authentication verification code per account is required during account log in and account switching.
-->


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

Modernisieren Sie die Anwendungsentwicklung unter Verwendung von Containern mit Services wie {{site.data.keyword.activedeployshort}} und {{site.data.keyword.deliverypipeline}}. Sie können dann über den {{site.data.keyword.vpn_short}}-Service mit SoftLayer kommunizieren, um den Container in einem privaten Netz mit dem privaten SoftLayer-Netz zu verbinden. Alle Nutzungsgebühren für Rechenressourcen und -services werden über die {{site.data.keyword.Bluemix_notm}}-Rechnung abgerechnet. 

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

Nach der Verknüpfung Ihrer {{site.data.keyword.Bluemix_notm}}- und SoftLayer-Abrechnungskonten erfolgt die Rechnungsstellung im nächsten Abrechnungszyklus über eine einzige {{site.data.keyword.Bluemix_notm}}-Rechnung.
{:shortdesc}

Der {{site.data.keyword.Bluemix_notm}}-Nutzungszyklus basiert auf Kalendermonaten, sodass Ihr Konto monatlich an dem Abrechnungstag abgerechnet wird, der in der Gebührenvereinbarung festgelegt wurde. Bei SoftLayer beginnt der Nutzungszyklus mit dem Beginn der SoftLayer-Nutzung, sodass die Rechnungsstellung jeden Monat an dem Tag erfolgt, an dem Sie sich für Ihr SoftLayer-Konto angemeldet haben. 

Wenn Sie Ihre Konten verknüpfen, wird die {{site.data.keyword.Bluemix_notm}}-Nutzung für den aktuellen Monat noch wie bisher abgerechnet und Sie erhalten für diesen Nutzungszeitraum eine {{site.data.keyword.Bluemix_notm}}-Rechnung. Ab dem Ersten des Folgemonats werden Ihre {{site.data.keyword.Bluemix_notm}}- und SoftLayer-Gebühren zusammen über Ihre {{site.data.keyword.Bluemix_notm}}-Rechnung abgerechnet.

Wenn Sie Ihre Konten beispielsweise am 16. April verknüpft haben, erhalten Sie für die Nutzung im April eine Bluemix-Rechnung. Je nach Zeitpunkt der Verknüpfung Ihrer Konten erhalten Sie möglicherweise eine separate Rechnung für Ihre SoftLayer-Nutzung. Ihre Nutzung sowohl von SoftLayer als auch von {{site.data.keyword.Bluemix_notm}} im Monat Mai wird über Ihr {{site.data.keyword.Bluemix_notm}}-Konto abgerechnet.

![Verknüpfung von Bluemix- und SoftLayer-Konten - Zusammenfassung](images/BluemixSoftLayerBill.svg)

Nach der Verknüpfung Ihrer Rechnungen werden in Ihrer {{site.data.keyword.Bluemix_notm}}-Rechnung die verschiedenen Gebühren für alle genutzten Ressourcen unter den folgenden Überschriften aufgelistet:

* **Bare-Metal-Server und zugeordnete Services**
* **Virtuelle Server und zugeordnete Services**
* **Nicht zugeordnete Services**

Informationen zum Anzeigen der {{site.data.keyword.Bluemix_notm}}-Nutzung finden Sie unter [Nutzungsdetails anzeigen](https://console.ng.bluemix.net/docs/pricing/index.html#usage).

