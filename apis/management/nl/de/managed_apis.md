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

Auf der Registerkarte **Verwaltete APIs anzeigen** können Sie den Gesamtstatus der verwalteten APIs und der APIs anzeigen, die zuvor verwaltet, aber momentan nicht bereitgestellt werden. Auf der Registerkarte **Gemeinsam genutzte APIs** werden alle APIs angezeigt, die über die API-Verwaltung oder den {{site.data.keyword.apiconnect_short}}-Service mit Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation gemeinsam genutzt werden.

Im Dashboard für APIs können alle APIs angezeigt werden, die über die API-Verwaltung verwaltet werden. 

## Verwaltete APIs anzeigen
{: #view_api}

Hier können APIs angezeigt werden, die für {{site.data.keyword.openwhisk_short}}-Aktionen und andere externe Quellen erstellt wurden.

1. Wählen Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard **Menü** > **Services** > **APIs** aus.
2. Klicken Sie auf **APIs verwalten**, um die Quelle auszuwählen. Daraufhin wird eine Liste der momentan verwalteten APIs angezeigt. Die folgenden API-Typen sind verfügbar:
    * Benutzerdefinierte Endpunkte - Diese Einträge stellen APIs dar, die sich außerhalb der {{site.data.keyword.Bluemix_notm}}-Umgebung befinden und über den zugehörigen URL-Endpunkt überwacht werden. 
    * {{site.data.keyword.openwhisk_short}}-Apps - Diese Einträge stellen {{site.data.keyword.openwhisk_short}}-Aktionen dar, die in eine API eingeschlossen sind.

Wählen Sie den Namen einer API aus, um weitere Details zu dieser API anzuzeigen.

## Verwaltete APIs erstellen
{: #create_mgd_api}

Sie können eine API zur Liste der verwalteten APIs hinzufügen, ohne die Liste verlassen zu müssen. Wählen Sie dazu **Verwaltete API erstellen** aus.

Wählen Sie aus, ob Sie eine {{site.data.keyword.openwhisk_short}}-API oder einen API-Proxy (externe API) erstellen möchten, und geben Sie die Informationen für die neue API ein.  

API-Proxys (externe APIs) können nur hier hinzugefügt werden. Eine externe API ist eine API, die nicht im {{site.data.keyword.Bluemix_notm}}-Organisationsbereich erstellt oder gespeichert wurde. Die Verwaltung einer externen API erfolgt durch Angabe der URL des externen Endpunkts. Dies ist nützlich, wenn Sie testen möchten, ob die API-Verwaltung Ihre Anforderungen erfüllt, oder wenn Sie bereits über APIs mit vorhandenen URLs verfügen, die Sie nicht unterbrechen möchten. 

Weitere Informationen zu den erforderlichen Einstellungen für die API-Erstellung finden Sie in [APIs verwalten](manage_apis.html).

## Mit gemeinsam genutzten APIs arbeiten
{: #share_api}

Auf der Registerkarte **Gemeinsam genutzte APIs erkunden** können Sie APIs anzeigen, die von anderen Benutzern erstellt wurden und gemeinsam genutzt werden. Ferner können für die APIs, die {{site.data.keyword.openwhisk_short}}-Aktionen und dem {{site.data.keyword.appconserviceshort}}-Service zugeordnet sind, API-Schlüssel erstellt werden.

1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf **Menü** > **Services** > **APIs**.
2. Wählen Sie in der Navigation **Gemeinsam genutzte APIs erkunden** aus. Hier werden alle APIs angezeigt, die Sie nutzen können.
3. Wählen Sie eine API aus, um das zugehörige Entwicklerportal zu öffnen, in dem Sie einen Plan für die Nutzung subskribieren können. 
4. Lesen Sie nach Auswahl einer API die Informationen im Abschnitt [APIs verwalten](manage_apis.html), um die folgenden Tasks auszuführen: 
    * API-Nutzung anzeigen
    * API-Schlüssel erstellen
    * API-Explorer zum Anzeigen von Dokumentation und Testen der API verwenden
