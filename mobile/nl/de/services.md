---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-11"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Services
{: #services}

Über die Ansicht **Services** des {{site.data.keyword.Bluemix}} Mobile-Dashboards können Sie Ihre vorhandenen Services anzeigen oder neue Services erstellen. Das Mobile-Dashboard bietet einen einzigen Punkt zum Anzeigen aller Bluemix-Services, die aktuell von Projekten verwaltet werden.  

Wenn Sie Services aus der Ansicht **Services** löschen, trennen Sie den Service von dem Projekt, dem er zugeordnet ist. Wenn Sie den Service wieder mit dem Projekt verbinden möchten, erstellen Sie eine neue Serviceinstanz.

## {{site.data.keyword.Bluemix_notm}} Mobile-Services - Übersicht
{: #mobile_services_overview}

In der folgenden Tabelle sind die {{site.data.keyword.Bluemix_notm}} Mobile-Services dargestellt. Sie können einzelne Services aus dem {{site.data.keyword.Bluemix_notm}}-Katalog nutzen oder diese Services in Ihr mobiles Projekt integrieren.

<table summary="In dieser Tabelle werden {{site.data.keyword.Bluemix_notm}} Mobile-Services beschrieben und Links zur Servicedokumentation angegeben">
<caption>Tabelle 1. {{site.data.keyword.Bluemix_notm}} Mobile-Services</caption>
<th>{{site.data.keyword.Bluemix_notm}} Mobile-Service</th>
<th>Beschreibung</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="{{site.data.keyword.mobileanalytics_short}}-Symbol"><br/>{{site.data.keyword.mobileanalytics_short}}</td>
<td valign="top">Mithilfe des Service {{site.data.keyword.mobileanalytics_full}} erhalten Sie Einblick in die Leistung und die Art der Nutzung
Ihrer mobilen Apps.<br/><br/> Weitere Informationen zum Betrieb dieses Service finden Sie in der <a href="/docs/services/mobileanalytics/index.html" alt="Link zur {{site.data.keyword.mobileanalytics_short}}-Dokumentation">{{site.data.keyword.mobileanalytics_short}}-Dokumentation</a>.
</td>
</tr>
<tr>
<td><img src="images/authentication_icon
.png" alt="{{site.data.keyword.amashort}}-Servicesymbol"><br/>{{site.data.keyword.amashort}}</td>
<td valign="top">Verwenden Sie den Service {{site.data.keyword.amafull}}, um Ihrer mobilen App Sicherheitsfunktionalität hinzuzufügen. Sie können Clientauthentifizierung und Identitätsprovider konfigurieren, damit sich Benutzer bei der App mit ihren bereits vorhandenen Google- oder Facebook-Konten anmelden können.<br/><br/>
Weitere Informationen zum Betrieb dieses Service finden Sie in der <a href="/docs/services/mobileaccess/index.html" alt="Link zur {{site.data.keyword.amashort}}-Dokumentation">{{site.data.keyword.amashort}}-Dokumentation</a>.</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="{{site.data.keyword.mobilefoundation_short}}-Servicesymbol"><br/> {{site.data.keyword.mobilefoundation_short}}</td>
<td valign="top">Mithilfe des Service {{site.data.keyword.mobilefoundation_long}} können Sie die Einrichtung einer {{site.data.keyword.mfp_full}}-Umgebung für Entwicklung, Test und Betrieb mobiler Unternehmens-Apps beschleunigen.<br/><br/>
Weitere Informationen zum Betrieb dieses Service finden Sie in der <a href="/docs/services/mobilefoundation/index.html" alt="Link zur {{site.data.keyword.mobilefoundation_short}}-Dokumentation">{{site.data.keyword.mobilefoundation_short}}-Dokumentation</a>.</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="{{site.data.keyword.mqa}}-Servicesymbol"><br/>{{site.data.keyword.mqa}}</td>
<td valign="top">Mithilfe des Service {{site.data.keyword.mqafull}} können Sie mobile Qualitätsservices für Ihre Apps erkunden und einrichten. Für einen raschen Einblick in die Problematik in Bezug auf die Apps, mit denen Sie arbeiten, können Sie die allgemeinen Qualitätsmetriken für Ihre mobilen Apps anzeigen. Diese Metriken umfassen Informationenen zu Abstürzen, Programmfehlern, Benutzerfeedback und Benutzerstimmung. Wenn Sie diese Informationen für Ihre Apps anzeigen, können Sie feststellen, ob bestimmte Themen einer weiteren Untersuchung bedürfen.<br/><br/>
Weitere Informationen zum Betrieb dieses Service finden Sie in der <a href="/docs/services/MobileQualityAssurance/index.html" alt="Link zur {{site.data.keyword.mqa}}-Dokumentation link">{{site.data.keyword.mqa}}-Dokumentation</a>.</td>
</tr>
<tr>
<td><img src="images/push_icon.png" alt="{{site.data.keyword.mobilepushshort}}-Servicesymbol"><br/>{{site.data.keyword.mobilepushshort}}</td>
<td valign="top">Der Service '{{site.data.keyword.mobilepushfull}}' bietet eine einheitliche Plattform zum Senden und Verwalten von mobilen Benachrichtigungen und Web-Push-Benachrichtigungen, die verschiedene Plattformen als Ziel haben.
<br/><br/>
{{site.data.keyword.mobilepushshort}} verwaltet die Zuordnung Ihrer Anwendungsbenutzer zu den zugehörigen Geräten, zur Geräteplattform sowie zu den Web-Browsern und führt die Senden von Push-Benachrichtigungen an die Geräte aus. Sie können Rundsendungen, Unicasts (auf der Basis von Geräte-ID und Benutzer-ID) sowie Tags (oder Themen) als Push-Benachrichtigungen an die Benutzer Ihrer mobilen Anwendungen und Web-Browser-Anwendungen senden. Außerdem können Sie ein SDK und REST-APIs verwenden, um Ihre Clientanwendungen weiter zu entwickeln.
<br/><br/>
Weitere Informationen zum Betrieb dieses Service finden Sie in der <a href="/docs/services/mobilepush/index.html" alt="Link zur {{site.data.keyword.mobilepushshort}}-Dokumentation">{{site.data.keyword.mobilepushshort}}-Dokumentation</a>.</td>
</table>

## Mobile Services integrieren
{: #services_integration}
Sie können Ihre bereits vorhandenen {{site.data.keyword.Bluemix_notm}} Mobile-Services, z. B. {{site.data.keyword.cloudant}}, in Ihr Projekt integrieren.


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
