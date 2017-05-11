---

copyright:
  years: 2017
lastupdated: "2017-04-13"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Eigene APIs
{: #manage_api}

Auf der Registerkarte **Verwaltete APIs anzeigen** können Sie den allgemeinen Status der APIs, die Sie verwalten, und der APIs, die Sie zuvor verwaltet haben, die aber zurzeit nicht verfügbar gemacht sind, prüfen. Auf der Seite **Gemeinsam genutzte APIs** werden alle APIs angezeigt, die zur gemeinsamen Nutzung mit Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation über das API-Management oder durch den {{site.data.keyword.apiconnect_short}}-Service verfügbar gemacht wurden. 

Sie können alle APIs, die Sie über das API-Management verwalten, im API-Dashboard zusammen anzeigen.  

## Verwaltete APIs anzeigen
{: #view_api}

Hier können Sie APIs anzeigen, die für {{site.data.keyword.openwhisk_short}}-Aktionen und andere externe Quellen erstellt wurden. 

1. Wählen Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard das Symbol **Menü** > **Services** > **APIs** aus. 
2. Klicken Sie auf **APIs verwalten**, um Ihre Quelle auszuwählen. Es wird eine Liste der APIs angezeigt, die zurzeit verwaltet werden. Zu den Typen von APIs gehören die folgenden: 
    * Benutzerdefinierte Endpunkte - Diese Einträge sind APIs, die sich außerhalb der {{site.data.keyword.Bluemix_notm}}-Umgebung befinden und die über ihren URL-Endpunkt verfolgt werden.  
    * {{site.data.keyword.openwhisk_short}}-Apps - Diese Einträge sind {{site.data.keyword.openwhisk_short}}-Aktionen, die in eine API eingeschlossen sind. 

Wählen Sie den Namen einer API aus, um weitere Details zu dieser API anzuzeigen. 

## Verwaltete APIs erstellen
{: #create_mgd_api}

Sie können der Liste eine API hinzufügen, ohne die Liste der verwalteten APIs zu verlassen, indem Sie **Verwaltete API erstellen** auswählen. 

Wenn Sie nach der Auswahl einen {{site.data.keyword.openwhisk_short}}- oder API-Proxy (externe API) erstellen wollen, geben Sie die Informationen für Ihre neue API ein.   

Dies ist die einzige Position, an der Sie einen API-Proxy oder eine externe API hinzufügen können. Eine externe API ist eine, die nicht im Bereich der {{site.data.keyword.Bluemix_notm}}-Organisation erstellt wurde oder gespeichert ist. Sie können eine externe API verwalten, indem Sie die URL des externen Endpunkts der API auswählen. Dies ist hilfreich, wenn Sie das API-Management ausprobieren, um zu prüfen, ob es Ihre Anforderungen erfüllt, oder wenn Sie bereits APIs haben, die mit vorhandenen URLs ausgeführt werden, die Sie nicht unterbrechen wollen.  

Weitere Informationen zu den erforderlichen Einstellungen zur Erstellung von APIs finden Sie unter [APIs verwalten](manage_apis.html). 

## Mit gemeinsam genutzten APIs arbeiten
{: #share_api}

Auf der Registerkarte **Gemeinsam genutzte APIs erkunden** können Sie APIs anzeigen, die von anderen Benutzern erstellt und zur gemeinsamen Nutzung für Sie verfügbar gemacht wurden. Sie können außerdem API-Schlüssel für die APIs erstellen, die {{site.data.keyword.openwhisk_short}}-Aktionen und dem {{site.data.keyword.appconserviceshort}}-Service zugeordnet sind. 

1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf das Symbol **Menü** > **Services** > **APIs**. 
2. Wählen Sie im Navigationsbereich die Option **Gemeinsam genutzte APIs erkunden** aus. Alle APIs, die Sie nutzen können, werden hier angezeigt. 
3. Zur Nutzung einer API wählen Sie sie aus, um das zugehörige Entwicklerportal zu öffnen, in dem Sie einen Plan zur Verwendung der API abonnieren können.  
4. Nach der Auswahl einer zu verwaltenden API, finden Sie weitere Informationen zur Ausführung der folgenden Tasks unter [APIs verwalten](manage_apis.html):  
    * API-Nutzung anzeigen
    * API-Schlüssel erstellen
    * Dokumentation im API-Explorer anzeigen und API testen
