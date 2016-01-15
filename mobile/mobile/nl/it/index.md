# Creazione di applicazioni mobili
{: #mobile}

Con i servizi mobili {{site.data.keyword.Bluemix_notm}}, puoi incorporare i servizi cloud precostruiti, gestiti e scalabili nelle tue applicazioni mobili senza dipendere dall'intervento del settore IT. Puoi concentrarti sulla creazione delle applicazioni mobili anziché sulla complessità della gestione dell'infrastruttura
  di back-end.

<table><caption>Tabella 1. Contenitore tipo Bluemix Mobile Services</caption>
<tr>
	<td>Ciascuno dei servizi mobili Bluemix può essere utilizzato indipendentemente. Puoi anche utilizzarli insieme per trarne il massimo vantaggio. Per iniziare, utilizza il contenitore tipo dei servizi mobili Bluemix per creare la tua applicazione. Questo contenitore tipo:
		<ul>
			<li>Crea un runtime Node.js con un'applicazione template. Puoi utilizzare questa applicazione per fornire funzioni lato server, come le API RESTful e i file statici. Puoi leggere ulteriori informazioni sull'utilizzo di questa applicazione nella sezione relativa allo sviluppo del backend mobile.</li>
			<li>
Fornisce un'istanza di ciascuno dei servizi mobili Bluemix e associa il servizio all'applicazione Node.js. </li>
		</ul>
	</td>
	<td> <img src="images/mf_boiler_icon.png" alt="Servizi mobili Bluemix" width="500"> Contenitore tipo di servizi mobili Bluemix </td>
</tr>
</table>

Dopo che hai utilizzato il contenitore tipo di servizi mobili Bluemix per creare la tua applicazione, puoi ottenere gli esempi HelloWorld per ciascuno dei servizi o iniziare a strumentare la tua applicazione esistente per utilizzare i servizi Bluemix.


## Panoramica sui servizi
{: #services-overview}
Puoi utilizzare tutti i servizi mobili Bluemix insieme utilizzando il contenitore tipo di servizi mobili Bluemix o puoi utilizzare i
singoli servizi dal catalogo Bluemix. Il seguente diagramma illustra tutti i componenti dei servizi mobili Bluemix.

![Architettura dei servizi mobili Bluemix](images/bms_architecture.jpg)

<table>
<caption>Tabella 2. Bluemix e sistemi aziendali</caption>
<th>Bluemix</th>
<th>Sistemi aziendali</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Icona di runtime Node.js"><b>Node.js</b> <br/> Un runtime Node.js che ospita l'applicazione template viene fornito come parte del contenitore tipo di servizi mobili Bluemix. Puoi utilizzare l'applicazione template per fornire funzioni lato server, come le API RESTful e i file statici. <br/>Ad esempio, puoi estendere l'applicazione Node.js per l'elaborazione logica personalizzata oppure per stabilire una connessione alle API REST nell'infrastruttura esistente della tua azienda. Ogni applicazione da te creata su Bluemix ha un ID applicazione univoco. La tua applicazione mobile utilizza questo ID con l'SDK per accedere ai servizi associati a tale applicazione. L'ID applicazione viene utilizzato dalla piattaforma
come contesto per le funzioni comuni, come misurazione e registrazione. Puoi leggere ulteriori informazioni sull'utilizzo di questa applicazione nella sezione relativa allo sviluppo del backend mobile.</td>
<td valign="top"><b>Provider di informazioni</b> <br/>Puoi utilizzare un runtime Node.js che ospitava un Bluemix per stabilire una connessione a qualsiasi tipo di provider di informazioni:
<ul>
	<li>Backend aziendale</li>
	<li>Database </li>
	<li>Un altro servizio di terzi ospitato</li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="Icona del servizio Mobile Client Access"> <b>Mobile Client Access</b><br/>Utilizza il servizio IBM Mobile Client Access for Bluemix per proteggere le applicazioni Node.js e Java for Liberty ospitate su Bluemix. Dotando la tua applicazione mobile dell'SDK Mobile Client Access, puoi richiedere agli utenti di
eseguire il login per accedere ai servizi mobili Bluemix o Node.js. Oltre alle funzionalità di sicurezza, Mobile Client Access raccoglie anche i dati di analisi per consentirti di monitorare le prestazioni della tua applicabile mobile e di raccogliere le statistiche di utilizzo e i log client. </td>
<td valign="top"><b>Provider di identità utente</b> <br/>Puoi utilizzare i seguenti provider di identità:<ul><li>Facebook</li><li>Google</li></ul></td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="Icona del servizio Push Notifications"> <b>Push Notifications</b><br/>Il servizio IBM Push Notifications for Bluemix fornisce una piattaforma unificata per inviare e gestire notifiche di push ad applicazioni destinate a piattaforme iOS e Android. Questo servizio gestisce l'associazione dei tuoi utenti delle applicazioni ai loro dispositivi e alla loro piattaforma del dispositivo e gestisce l'invio delle notifiche di push ai dispositivi. Con questo servizio, puoi inviare broadcast, unicast (basati su ID utente e ID dispositivo) e tag (o argomenti) basati sulle notifiche di push ai tuoi utenti delle applicazioni mobili.</td>
<td valign="top"><b>Provider di servizi di push</b><ul><li>APNS (Apple Push Notifications Service)</li><li>GCM (Google Cloud Messaging)</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Icona del servizio Cloudant"><b>Cloudant NoSQLDB</b><br/> Cloudant è un DBaaS (database as a service) NoSQL. Viene creato da zero per ingrandirsi fino a un livello globale, essere eseguito non-stop e gestire un'ampia varietà di tipi di dati come JSON, full-text e geospaziali. </td>
<td>Cloudant.com</td>
</tr>
</table>
