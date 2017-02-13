---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-19"

---

# Mobile Apps aus der {{site.data.keyword.mobilefirstbp}} Starter-Boilerplate erstellen
{: #try_mobile}

Jeder {{site.data.keyword.Bluemix}} Mobile-Service kann unabhängig verwendet werden. Durch die kombinierte Verwendung mit der {{site.data.keyword.mobilefirstbp}} Starter-Boilerplate können Sie den größten Nutzen erzielen.

Erstellen Sie zu Beginn mit dem {{site.data.keyword.mobilefirstbp}}-Starter Ihre App. Die Boilerplate ermöglicht Ihnen die Durchführung der folgenden Aktionen:

* Erstellen Sie eine Node.js-Laufzeit mit einer Vorlagenanwendung. Mithilfe dieser Anwendung können Sie serverseitige Funktionen wie REST-konforme APIs und statische Dateien bereitstellen. <!-- You can read more about operating this application in the Developing Mobile Backend section.-->
* Stellen Sie eine Instanz für jeden der {{site.data.keyword.Bluemix_notm}} Mobile-Services bereit und binden Sie den Service an die Node.js-Anwendung.

<!--
<img src="images/mf_boiler_icon.png" alt="Bluemix mobile services" width="500"> {{site.data.keyword.mobilefirstbp}} Starter boilerplate
-->

Nachdem Sie mit der {{site.data.keyword.mobilefirstbp}} Starter-Boilerplate eine eigene App erstellt haben, können Sie entweder Hello Bluemix-Beispiele für jeden der Services abrufen oder mit dem Instrumentieren Ihrer bestehenden App für die Verwendung von {{site.data.keyword.Bluemix_notm}}-Services beginnen.


## Übersicht über Services
{: #services-overview}
Sie können entweder mithilfe der {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobilefirstbp}} Starter-Boilerplate alle {{site.data.keyword.Bluemix_notm}} Mobile-Services zusammen verwenden oder Sie können einzelne Services aus dem {{site.data.keyword.Bluemix_notm}}-Katalog verwenden. Im folgenden Diagramm werden die Komponenten von {{site.data.keyword.Bluemix_notm}} Mobile-Services dargestellt.

![Architektur der {{site.data.keyword.Bluemix_notm}} Mobile-Services](images/bms_architecture.jpg)

<table summary="In dieser Tabelle werden die {{site.data.keyword.Bluemix_notm}} Mobile-Services beschrieben">
<caption>Tabelle 1. {{site.data.keyword.Bluemix_notm}} und Unternehmenssysteme</caption>
<th>{{site.data.keyword.Bluemix_notm}}</th>
<th>Unternehmenssysteme</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Symbol für Node.js-Laufzeit"><b>Node.js</b> <br/> Eine Node.js-Laufzeit, die eine Vorlagen-App hostet, wird als Bestandteil der {{site.data.keyword.mobilefirstbp}} Starter-Boilerplate bereitgestellt. Mithilfe dieser Vorlagenanwendung können Sie serverseitige Funktionen wie REST-konforme APIs und statische Dateien bereitstellen. <br/>Sie können z. B. die Node.js-Anwendung zur Verarbeitung angepasster Logik erweitern oder zum Verbinden mit REST-APIs in der bestehen Infrastruktur Ihres Unternehmens. Jede App, die Sie in {{site.data.keyword.Bluemix_notm}} erstellen, besitzt eine eindeutige App-ID. Ihre mobile App verwendet diese ID im SDK, um auf die Services zuzugreifen, die der Anwendung zugeordnet sind. Die App-ID wird von der Plattform als Kontext für allgemeine Funktionen verwendet, z. B. zum Messen und Protokollieren.
<!--You can read more about operating this application in the "Developing Mobile Backend" section.--></td>
<td valign="top"><b>Informationsanbieter</b> <br/>Sie können eine in {{site.data.keyword.Bluemix_notm}} gehostete Node.js-Laufzeit verwenden, um eine Verbindung zu einem beliebigen Informationsanbietertyp herzustellen:
<ul>
	<li>Unternehmens-Back-End</li>
	<li>Datenbank </li>
	<li>Gehosteter Service eines anderen Anbieters</li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/authentication_icon.png" alt="Symbol für Service {{site.data.keyword.amashort}}"> <b>{{site.data.keyword.amashort}}</b><br/>Mit dem Service {{site.data.keyword.amafull}} können Sie Node.js- und Java for Liberty-Anwendungen schützen, die in {{site.data.keyword.Bluemix_notm}} gehostet werden. Durch das Instrumentieren Ihrer mobilen App mit dem {{site.data.keyword.amashort}}-SDK kann die Benutzeranmeldung bei Node.js oder bei den mobilen {{site.data.keyword.Bluemix_notm}}-Services erzwungen werden. <!-- In addition to security capabilities, {{site.data.keyword.amashort}} also gathers analytics data, so that you can monitor your mobile application performance and collect client logs and usage statistics.--> </td>
<td valign="top"><b>Benutzeridentitätsanbieter</b> <br/>Sie können die folgenden Identitätsanbieter verwenden: <ul><li>Facebook</li><li>Google</li><li> Angepasst </li></ul></td>
</tr>
<tr>
<td>Symbol für <img src="images/push_icon.png" alt="{{site.data.keyword.mobilepushshort}}-Service"> <b>{{site.data.keyword.mobilepushshort}}</b><br/>Der Service '{{site.data.keyword.mobilepushfull}}' bietet eine einheitliche Plattform zum Senden und Verwalten von Push-Benachrichtigungen mit mobilen Plattformen und Web-Browser-Anwendungen (iOS & Android) als Ziel. Dieser Service verwaltet die Zuordnung Ihrer Anwendungsbenutzer zu ihren Geräten, zur Geräteplattform und zu den Browsern und führt das Senden von Push-Benachrichtigungen an Subskribenten aus. Mit diesem Service können Sie Rundsendungen, Unicasts (auf der Basis von Benutzer-ID und Geräte-ID) sowie tagbasierte (themenbasierte) Push-Benachrichtigungen an Ihre Kunden senden.</td>
<td valign="top"><b>Push-Serviceanbieter</b><ul><li>Apple Push Notifications Service</li><li>Firebase Cloud Messaging</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Symbol für Cloudant-Service"><b>Cloudant NoSQLDB</b><br/> Cloudant ist eine NoSQL Database as a Service (DBaaS). Sie kann von lokal bis global beliebig skaliert werden, ist rund um die Uhr betriebsbereit und kann eine Vielzahl von Datentypen verarbeiten (z. B. JSON-, Volltext- und geografisch-räumliche Daten). </td>
<td>Cloudant.com</td>
</tr>
</table>
