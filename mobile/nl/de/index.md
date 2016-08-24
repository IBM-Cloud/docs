---

copyright:
  years: 2016

---
{:new_window: target="_blank"}

# Mobile Projekte mithilfe des Mobile-Dashboards erstellen
{: #mobile}
*Letzte Aktualisierung: 18. Juli 2016*
{: .last-updated}

Mit {{site.data.keyword.Bluemix}} Mobile-Services können Sie vordefinierte, verwaltete und skalierbare Cloud-Services in Ihre mobilen Anwendungen integrieren, ohne dass die IT-Abteilung involviert werden muss. Sie können sich auf das Erstellen mobiler Apps statt auf die Komplexitäten beim Verwalten der Back-End-Infrastruktur konzentrieren.

Über das Mobile-Dashboard steht ein integrierter Zugang zu {{site.data.keyword.Bluemix_notm}} bereit. Sie können neue mobile Projekte problemlos aus dem Dashboard erstellen. Über die Ansicht **Projekte** können Sie alle Projekte von einer Position aus verwalten. In der Ansicht **Services** werden Ihre vorhandenen Instanzen mobiler Services angezeigt.

Um das Mobile-Dashboard anzuzeigen, klicken Sie an der {{site.data.keyword.Bluemix_notm}}-Ausgangsposition auf **Mobile**.
<img src="images/mobile_dashboard.jpg" alt="{{site.data.keyword.Bluemix_notm}}-Ausgangsposition">

Klicken Sie für den Beginn Ihrer Arbeit in der Ansicht **Projects** des Mobile-Dashboards auf **Neues Projekt**.

## {{site.data.keyword.Bluemix_notm}} Mobile-Services - Übersicht
{: #mobile_services_overview}

In der folgenden Tabelle werden die verfügbaren {{site.data.keyword.Bluemix_notm}} Mobile-Services dargestellt. Sie können einzelne Services aus dem {{site.data.keyword.Bluemix_notm}}-Katalog nutzen oder diese Services in Ihr mobiles Projekt integrieren.

<table summary="In dieser Tabelle werden {{site.data.keyword.Bluemix_notm}} Mobile-Services beschrieben und Links zur Servicedokumentation angegeben">
<caption>Tabelle 1. {{site.data.keyword.Bluemix_notm}} Mobile-Services</caption>
<th>{{site.data.keyword.Bluemix_notm}} Mobile-Service</th>
<th>Beschreibung</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="{{site.data.keyword.mobileanalytics_short}}-Symbol"><br/><b>{{site.data.keyword.mobileanalytics_short}} (Experimentell)</b></td>
<td valign="top">Mithilfe des Service {{site.data.keyword.mobileanalytics_full}} können Sie Status, Verhalten und Kontext mobiler Apps, mobiler Benutzer und mobiler Geräte messen.<br/><br/>
Weitere Informationen zum Betrieb dieses Service finden Sie in der <a href="../services/mobileanalytics/index.html" alt="{{site.data.keyword.mobileanalytics_short}} - Link zur Dokumentation">Dokumentation zu {{site.data.keyword.mobileanalytics_short}}</a>.
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="{{site.data.keyword.amashort}}-Servicesymbol"><br/><b>{{site.data.keyword.amashort}}</b></td>
<td valign="top">Mithilfe des Service {{site.data.keyword.amafull}} können Sie Sicherheitsfunktionen zu Ihrer mobilen App hinzufügen. Sie können Clientauthentifizierung und Identitätsprovider konfigurieren, damit sich Benutzer bei der Apppp mit ihren bereits vorhandenen Google- oder Facebook-Konten anmelden können.<br/><br/>
Weitere Informationen zum Betrieb dieses Service finden Sie in der <a href="../services/mobileaccess/index.html" alt="{{site.data.keyword.amashort}} - Link zur Dokumentation">Dokumentation zu {{site.data.keyword.amashort}}</a>.</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="{{site.data.keyword.mobilefoundation_short}}-Servicesymbol"><br/> <b>{{site.data.keyword.mobilefoundation_short}}</b></td>
<td valign="top">Mithilfe des Service {{site.data.keyword.mobilefoundation_long}} können Sie die Einrichtung einer {{site.data.keyword.mfp_full}}-Umgebung für Entwicklung, Test und Betrieb mobiler Unternehmens-Apps beschleunigen.<br/><br/>
Weitere Informationen zum Betrieb dieses Service finden Sie in der <a href="../services/mobilefoundation/index.html" alt="{{site.data.keyword.mobilefoundation_short}} - Link zur Dokumentation">Dokumentation zu {{site.data.keyword.mobilefoundation_short}}</a>.</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="{{site.data.keyword.mqa}}-Servicesymbol"><br/><b>{{site.data.keyword.mqa}}</b></td>
<td valign="top">Mithilfe des Service {{site.data.keyword.mqafull}} können Sie mobile Qualitätsservices für Ihre Apps erkunden und einrichten. Für einen raschen Einblick in die Problekmatik in Bezug auf die Apps, mit denen Sie arbeiten, können Sie die allgemeinen Qualitätsmetriken für Ihre mobilen Apps anzeigen. Diese Metriken umfassen Informationenen zu Abstürzen, Programmfehlern, Benutzerfeedback und Benutzerstimmung. Wenn Sie diese Informationen für Ihre Apps anzeigen, können Sie feststellen, ob bestimmte Themen einer weiteren Untersuchung bedürfen.<br/><br/>
Weitere Informationen zum Betrieb dieses Service finden Sie in der <a href="../services/MobileQualityAssurance/index.html" alt="{{site.data.keyword.mqa}} - Link zur Dokumentation">Dokumentation zu {{site.data.keyword.mqa}}</a>.</td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="Symbol für Push Notifications-Service"><br/><b>{{site.data.keyword.mobilepushshort}}</b></td>
<td valign="top">Mithilfe des Service {{site.data.keyword.mobilepushfull}} können Sie mobile Push-Benachrichtigungen für iOS- und Android-Plattformen senden und verwalten. Dieser Service verwaltet die Zuordnung Ihrer Anwendungsbenutzer zu den zugehörigen Geräten und zur Geräteplattform und führt das Senden von Push-Benachrichtigungen an die Geräte aus. Mit diesem Service können Sie Rundsendungen, Unicasts (auf der Basis von Benutzer-ID und Geräte-ID) sowie tagbasierte (themenbasierte) Push-Benachrichtigungen an die Benutzer Ihrer mobilen Anwendungen senden.<br/><br/>
Weitere Informationen zum Betrieb dieses Service finden Sie in der <a href="../services/mobilepush/index.html" alt="{{site.data.keyword.mobilepushshort}} - Link zur Dokumentation">Dokumentation zu {{site.data.keyword.mobilepushshort}}</a>.</td>
</table>

## Mobile Services integrieren
{: #services_integration}
Sie können Ihre bereits vorhandenen {{site.data.keyword.Bluemix_notm}} Mobile-Services wie {{site.data.keyword.mobilepushshort}} und {{site.data.keyword.cloudant}} in Ihr Projekt integrieren.

#### {{site.data.keyword.mobilepushshort}} integrieren
{: #push_integration}

Führen Sie die folgenden Schritte aus, um Ihren bereits vorhandenen {{site.data.keyword.mobilepushshort}}-Service zu integrieren:

1. Klicken Sie auf Ihre Instanz des Service {{site.data.keyword.mobilepushshort}}.
2. Klicken Sie auf **Mobile Optionen** und kopieren Sie die Werte für **Route** und **App-Guid**.

   **Anmerkung**: Ihr {{site.data.keyword.mobilepushshort}}-Service muss an eine App gebunden sein, damit **Mobile Optionen** sichtbar werden.

3. Navigieren Sie wieder zur Ansicht **Projekte** des Mobile-Dashboards.
4. Klicken Sie auf Ihre Projekt, um es zu bearbeiten.
5. Klicken Sie auf **Push** und aktivieren Sie die Benachrichtigungen.
6. Geben Sie den Wert für **App-Guid** an, den Sie zuvor in das Feld **App-ID** kopiert haben.
7. Geben Sie den Wert für **Route** an, den Sie zuvor in das Feld **App-Route-URL** kopiert haben.

#### {{site.data.keyword.cloudant}} integrieren
{: #cloudant_integration}

Führen Sie die folgenden Schritte aus, um Ihren bereits vorhandenen {{site.data.keyword.cloudant}}-Service zu integrieren:

1. Klicken Sie auf Ihre Instanz des Service {{site.data.keyword.cloudant}}.
2. Klicken Sie auf **STARTEN**.
3. Klicken Sie in der Ansicht **Datenbanken** auf Ihren Datenbanknamen.
4. Klicken Sie auf **API** und kopieren Sie den Wert für den **API-Schlüssel** bis hin zu Ihrem Datenbanknamen.

   **Anmerkung**: Kopieren Sie keinen Inhalt, der hinter Ihrem Datenbanknamen steht.

5. Klicken Sie auf **Berechtigungen** > **API-Schlüssel generieren** und kopieren Sie die Werte für **Schlüssel** und **Kennwort**.
6. Navigieren Sie wieder zur Ansicht **Projekte** des Mobile-Dashboards.
7. Klicken Sie auf Ihre Projekt, um es zu bearbeiten.
8. Klicken Sie auf **Daten** > **+ Datenquelle** > **Cloudant**, geben Sie Ihren Datenquellennamen an und klicken Sie auf **Hinzufügen**.
9. Klicken Sie auf die Option für die Cloudant-Konfiguration.
10. Geben Sie den Wert für den **API-Schlüssel** an, den Sie zuvor in die **API-URL** kopiert haben.
11. Geben Sie den Wert für den **Schlüssel** an, den Sie zuvor in das Feld **Benutzer** kopiert haben.
12. Geben Sie den Wert für das **Kennwort** an, den Sie zuvor in das Feld **Kennwort** kopiert haben.
13. Klicken Sie auf **OK**.


# Zugehörige Links
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Experimental)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## Blogbeiträge
{: #general}
* [Blogbeitrag: Einführung in das Bluemix Mobile-Dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [Blogbeitrag: Bluemix Mobile, Teil 1: App 'Store Catalog' erstellen](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [Blogbeitrag: Bluemix Mobile, Teil 2: Angepasstes Bluemix-Back-End in die App 'Store Catalog' integrieren](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## Lernprogramme und Beispiele
{: #samples}
* [Mobiles Back-End für Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
