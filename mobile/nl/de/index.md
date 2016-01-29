# Mobile Apps erstellen
{: #mobile}

Mit {{site.data.keyword.Bluemix_notm}} Mobile Services können Sie vordefinierte, verwaltete und skalierbare Cloud-Services in Ihre mobilen iOS-Anwendungen integrieren, ohne dass die IT-Abteilung involviert werden muss. Sie können sich auf das Erstellen mobiler Apps statt auf die Komplexitäten beim Verwalten der Back-End-Infrastruktur konzentrieren. 

<table><caption>Tabelle 1. Bluemix Mobile Services-Boilerplate</caption>
<tr>
	<td>Jeder der Bluemix Mobile Services kann unabhängig verwendet werden. Durch die kombinierte Verwendung können Sie den größten Nutzen erzielen. Erstellen Sie zu Beginn mit der Bluemix Mobile Services-Boilerplate eine eigene App. Die Boilerplate führt Folgendes aus:
		<ul>
			<li>Sie erstellt eine Node.js-Laufzeit mit einer Vorlagenanwendung. Mithilfe dieser Anwendung können Sie serverseitige Funktionen wie REST-konforme APIs und statische Dateien bereitstellen. Weitere Informationen zum Betreiben dieser Anwendung finden Sie im Abschnitt über das Entwickeln des mobilen Back-Ends. </li>
			<li>
Sie stellt eine Instanz für jeden Bluemix Mobile Service bereit und bindet den Service an die Node.js-Anwendung. </li>
		</ul>
	</td>
	<td> <img src="images/mf_boiler_icon.png" alt="Bluemix Mobile Services" width="500"> Bluemix Mobile Services-Boilerplate </td>
</tr>
</table>

Nachdem Sie mit der Bluemix Mobile Services-Boilerplate eine eigene App erstellt haben, können Sie entweder HelloWorld-Beispiele für jeden der Services abrufen oder mit dem Instrumentieren Ihrer bestehenden App für die Verwendung von Bluemix-Services beginnen.


## Übersicht über Services
{: #services-overview}
Sie können entweder mithilfe der Blumix Mobile Services-Boilerplate alle Bluemix Mobile Services zusammen verwenden, oder Sie können einzelne Services aus dem Bluemix-Katalog verwenden. Im folgenden Diagramm werden alle Komponenten von Bluemix Mobile Services dargestellt.

![Architektur der mobilen Bluemix-Services](images/bms_architecture.jpg)

<table>
<caption>Tabelle 2. Bluemix und Unternehmenssysteme</caption>
<th>Bluemix</th>
<th>Unternehmenssysteme</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Symbol für Node.js-Laufzeit"><b>Node.js</b> <br/> Eine Node.js-Laufzeit, die eine Vorlagenanwendung hostet, wird als Bestandteil der Bluemix Mobile Services-Boilerplate bereitgestellt. Mithilfe dieser Vorlagenanwendung können Sie serverseitige Funktionen wie REST-konforme APIs und statische Dateien bereitstellen. <br/>Sie können z. B. die Node.js-Anwendung zur Verarbeitung angepasster Logik erweitern oder zum Verbinden mit REST-APIs in der bestehen Infrastruktur Ihres Unternehmens. Jede App, die Sie in Bluemix erstellen, besitzt eine eindeutige Anwendungs-ID. Ihre mobile App verwendet diese ID im SDK, um auf die Services zuzugreifen, die der Anwendung zugeordnet sind. Die App-ID wird von der Plattform als Kontext für allgemeine Funktionen verwendet, z. B. zum Messen und Protokollieren.
Weitere Informationen zum Betreiben dieser Anwendung finden Sie im Abschnitt über das Entwickeln des mobilen Back-Ends.</td>
<td valign="top"><b>Informationsanbieter</b> <br/>Sie können eine in Bluemix gehostete Node.js-Laufzeit verwenden, um die Verbindung zu einem beliebigen Informationsanbietertyp herzustellen:
<ul>
	<li>Unternehmens-Back-End</li>
	<li>Datenbank</li>
	<li>Gehosteter Service eines anderen Anbieters</li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="Symbol für Mobile Client Access-Service"> <b>Mobile Client Access</b><br/>Mit dem Service 'IBM Mobile Client Access for Bluemix' können Sie Node.js- und Java for Liberty-Anwendungen schützen, die in Bluemix gehostet werden. Durch das Instrumentieren Ihrer mobilen App mit dem Mobile Client Access-SDK kann die Benutzeranmeldung bei Node.js oder Bluemix Mobile Services erzwungen werden. Zusätzlich zur Bereitstellung von Sicherheitsfunktionen erfasst Mobile Client Access auch Analysedaten, mit denen Sie die Leistung Ihrer mobilen Anwendung überwachen sowie Clientprotokolle und Nutzungsstatistiken erfassen können. </td>
<td valign="top"><b>Benutzeridentitätsanbieter</b> <br/>Sie können die folgenden Identitätsanbieter verwenden: <ul><li>Facebook</li><li>Google</li></ul></td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="Symbol für Push-Benachrichtigungsservice"> <b>Push-Benachrichtigungen</b><br/>Der IBM Push Notifications for Bluemix-Service stellt eine einheitliche Plattform zum Senden und Verwalten von mobilen Push-Benachrichtigungen für iOS- und Android-Plattformen bereit. Dieser Service verwaltet die Zuordnung Ihrer Anwendungsbenutzer zu den zugehörigen Geräten und zur Geräteplattform und führt das Senden von Push-Benachrichtigungen an die Geräte aus. Mit diesem Service können Sie Rundsendungen, Unicasts (auf der Basis von Benutzer-ID und Geräte-ID) sowie tagbasierte (themenbasierte) Push-Benachrichtigungen an die Benutzer Ihrer mobilen Anwendungen senden.</td>
<td valign="top"><b>Push-Serviceanbieter</b><ul><li>Apple Push Notifications Service</li><li>Google Cloud Messaging</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Symbol für Cloudant-Service"><b>Cloudant NoSQLDB</b><br/> Cloudant ist eine NoSQL Database as a Service (DBaaS). Sie kann von lokal bis global beliebig skaliert werden, ist rund um die Uhr betriebsbereit und kann eine Vielzahl von Datentypen verarbeiten (z. B. JSON-, Volltext- und geografisch-räumliche Daten). </td>
<td>Cloudant.com</td>
</tr>
</table>
