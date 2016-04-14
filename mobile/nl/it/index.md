# Creazione di applicazioni mobili
{: #mobile}
*Ultimo aggiornamento: 28 gennaio 2016* 

Con i servizi mobili {{site.data.keyword.Bluemix}}, puoi incorporare i servizi cloud precostruiti, gestiti e scalabili nelle tue applicazioni mobili senza dipendere dall'intervento del settore IT. Puoi concentrarti sulla creazione delle applicazioni mobili anziché sulla complessità della gestione dell'infrastruttura
  di back-end.

<table><caption>Tabella 1. Contenitore tipo MobileFirst&trade; Services Starter</caption>
<tr>
	<td>Ciascuno dei servizi mobili può essere utilizzato indipendentemente. Puoi anche utilizzarli insieme per trarne il massimo vantaggio. Per iniziare, usa {{site.data.keyword.mobilefirstbp}} Starter per creare la tua applicazione. Questo contenitore tipo:
		<ul>
			<li>Crea un runtime Node.js con un'applicazione template. Puoi utilizzare questa applicazione per fornire funzioni lato server, come le API RESTful e i file statici. <!-- You can read more about operating this application in the Developing Mobile Backend section.--> </li>
			<li>
Fornisce un'istanza di ciascuno dei servizi mobili {{site.data.keyword.Bluemix_notm}} ed esegue il bind del servizio all'applicazione Node.js. </li>
		</ul>
	</td>
	<td> <img src="images/mf_boiler_icon.png" alt="Servizi mobili Bluemix" width="500"> Contenitore tipo {{site.data.keyword.mobilefirstbp}} Starter </td>
</tr>
</table>

Dopo che hai utilizzato il contenitore tipo {{site.data.keyword.mobilefirstbp}} Starter per creare la tua applicazione, puoi ottenere degli esempi HelloWorld per ciascuno dei servizi oppure iniziare a strumentare la tua applicazione esistente per utilizzare i servizi {{site.data.keyword.Bluemix_notm}}.


## Panoramica sui servizi
{: #services-overview}
Puoi utilizzare tutti i servizi mobili {{site.data.keyword.Bluemix_notm}} insieme utilizzando il contenitore tipo {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobilefirstbp}} Starter oppure puoi utilizzare dei singoli servizi dal catalogo {{site.data.keyword.Bluemix_notm}}. Il seguente diagramma illustra tutti i componenti dei servizi mobili {{site.data.keyword.Bluemix_notm}}.

![Architettura dei servizi mobili {{site.data.keyword.Bluemix_notm}}](images/bms_architecture.jpg)

<table>
<caption>Tabella 2. {{site.data.keyword.Bluemix_notm}} e sistemi aziendali</caption>
<th>{{site.data.keyword.Bluemix_notm}}</th>
<th>Sistemi aziendali</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Icona di runtime Node.js"><b>Node.js</b> <br/> Un runtime Node.js che ospita un'applicazione template viene fornito come parte del contenitore tipo {{site.data.keyword.mobilefirstbp}} Starter. Puoi utilizzare l'applicazione template per fornire funzioni lato server, come le API RESTful e i file statici. <br/>Ad esempio, puoi estendere l'applicazione Node.js per l'elaborazione logica personalizzata oppure per stabilire una connessione alle API REST nell'infrastruttura esistente della tua azienda. Ciascuna applicazione da te creata su {{site.data.keyword.Bluemix_notm}} ha un ID applicazione univoco. La tua applicazione mobile utilizza questo ID con l'SDK per accedere ai servizi associati a tale applicazione. L'ID applicazione viene utilizzato dalla piattaforma
come contesto per le funzioni comuni, come misurazione e registrazione.
Puoi leggere ulteriori informazioni sull'utilizzo di questa applicazione nella sezione relativa allo sviluppo del backend mobile.</td>
<td valign="top"><b>Provider di informazioni</b> <br/>Puoi utilizzare un runtime Node.js ospitato su {{site.data.keyword.Bluemix_notm}} per stabilire una connessione a qualsiasi tipo di provider di informazioni:
<ul>
	<li>Backend aziendale</li>
	<li>Database </li>
	<li>Un altro servizio di terzi ospitato</li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="{{site.data.keyword.amashort}} - icona di servizio"> <b>{{site.data.keyword.amashort}}</b><br/>Utilizza il servizio {{site.data.keyword.amafull}}  per proteggere le applicazioni Node.js e Liberty for Java ospitate su {{site.data.keyword.Bluemix_notm}}. Strumentando la tua applicazione mobile con SDK {{site.data.keyword.amashort}}, puoi richiedere agli utenti di eseguire il login per accedere ai servizi mobili {{site.data.keyword.Bluemix_notm}} o Node.js. Oltre alle funzionalità di sicurezza, {{site.data.keyword.amashort}} raccoglie anche i dati di analisi per consentirti di monitorare le prestazioni delle applicazioni mobili e raccogliere i log client e le statistiche di utilizzo. </td>
<td valign="top"><b>Provider di identità utente</b> <br/>Puoi utilizzare i seguenti provider di identità: <ul><li>Facebook</li><li>Google</li></ul></td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="Icona di servizio Push Notifications"> <b>{{site.data.keyword.mobilepushshort}}</b><br/>Il  servizio {{site.data.keyword.mobilepushfull}} fornisce una piattaforma unificata per inviare e gestire le notifiche di push mobili destinate a piattaforme iOS e Android. Questo servizio gestisce l'associazione dei tuoi utenti delle applicazioni ai loro dispositivi e alla loro piattaforma del dispositivo e gestisce l'invio delle notifiche di push ai dispositivi. Con questo servizio, puoi inviare broadcast, unicast (basati su ID utente e ID dispositivo) e tag (o argomenti) basati sulle notifiche di push ai tuoi utenti delle applicazioni mobili.</td>
<td valign="top"><b>Provider di servizi di push</b><ul><li>APNS (Apple Push Notifications Service)</li><li>GCM (Google Cloud Messaging)</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Icona del servizio Cloudant"><b>Cloudant NoSQLDB</b><br/> Cloudant è un DBaaS (database as a service) NoSQL. Viene creato da zero per ingrandirsi fino a un livello globale, essere eseguito non-stop e gestire un'ampia varietà di tipi di dati come JSON, full-text e geospaziali. </td>
<td>Cloudant.com</td>
</tr>
</table>
