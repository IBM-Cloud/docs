---



copyright:

  years: 2015，2017

lastupdated: "2017-05-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Creazione di applicazioni Cloud Foundry

Con {{site.data.keyword.Bluemix}}, puoi
creare la tua applicazione nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Dopo averla creata, puoi decidere di continuare a usare l'interfaccia utente, l'interfaccia riga di comando cf o {{site.data.keyword.jazzhub_title}} per
sviluppare, tracciare, pianificare e distribuire la tua applicazione.
{:shortdesc}

Quando crei un'applicazione in {{site.data.keyword.Bluemix_notm}},
inizi con uno starter. Uno *starter* è un template che include
dei servizi predefiniti e del codice applicativo configurato con uno
specifico pacchetto di build. Ci sono due tipi di starter: contenitori tipo e runtime.

Un *contenitore tipo* è un contenitore per un'applicazione e il
suo ambiente di runtime associato e i servizi predefiniti per uno specifico dominio. Ad esempio,
il contenitore tipo Mobile Cloud include un runtime Node.js, oltre che i servizi
Mobile Data, Mobile Application Security e Push. Include anche un SDK e delle applicazioni di esempio per iniziare a sviluppare applicazioni
mobili che accedono a tali servizi.

Un *runtime* è la serie di risorse utilizzata per eseguire un'applicazione. {{site.data.keyword.Bluemix_notm}} fornisce ambienti di runtime come contenitori per diversi tipi di applicazioni. Gli ambienti di runtime sono integrati come pacchetti di build in {{site.data.keyword.Bluemix_notm}},
sono configurati automaticamente per l'utilizzo e richiedono una manutenzione minima, se non nulla.

Per iniziare a creare la tua applicazione, attieniti alla seguente procedura:
  1. Vai al Dashboard nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}.
  2. Fai clic su **CREA UN'APPLICAZIONE**.
  3. Fai clic su **WEB** e attieniti all'esperienza guidata
per scegliere uno starter, specificare un nome e selezionare come desideri eseguire
la codifica.
  4. Dopo che hai terminato l'esperienza guidata, fai clic su **VISUALIZZA PANORAMICA DELL'APPLICAZIONE**. La Panoramica per la tua applicazione è visualizzata nel Dashboard.
  5. Puoi aggiungere un servizio alla tua applicazione facendo clic su **AGGIUNGI UN SERVIZIO O UNA API** nella Panoramica dell'applicazione nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Cerca e seleziona i servizi dal catalogo o scorri alla fine del catalogo e fai clic su Servizi sperimentali **{{site.data.keyword.Bluemix_notm}}** per visualizzare i servizi sperimentali. In alternativa, puoi utilizzare l'interfaccia riga di comando cf. Vedi Opzioni per gestire le applicazioni.
  6. Nella pagina Panoramica dell'applicazione, scorri alla scheda "Fornitura continua" e fai clic su **Abilita**. L'origine della tua applicazione verrà salvata in un repository in Repository Git e tracciamento del problema, che è ospitato su Bluemix. Viene creata inoltre una toolchain aperta che utilizza quel repository e una delivery pipeline per sviluppare e distribuire la tua applicazione. Per ulteriori informazioni sul servizio Continuous Delivery, vedi <a href="https://console.ng.bluemix.net/docs/services/ContinuousDelivery/index.html#cd_getting_started">Introduzione a Continuous Delivery</a>.

**Nota:** se un servizio che associ mediante bind a un'applicazione si arresta in modo anomalo, l'applicazione potrebbe interrompere l'esecuzione o provocare errori. {{site.data.keyword.Bluemix_notm}} non
riavvia automaticamente l'applicazione per eseguire un ripristino da tali problemi. Valuta una codifica della tua applicazione per identificare e ripristinare interruzioni, eccezioni ed errori
di connessione. Per ulteriori informazioni, consulta l'argomento di risoluzione dei problemi Le applicazioni non si riavviano automaticamente.

## Opzioni per gestire le applicazioni

Una volta creata la tua applicazione, disponi di alcune opzioni per continuare ad aggiungere
servizi ad essa, oltre che per crearla e distribuirla:

<dl><dt>Interfaccia riga di comando cf</dt>
<dd>Usa l'interfaccia riga di comando cf per aggiornare la tua applicazione, creare un'istanza del servizio o eseguire il bind del servizio alla tua applicazione. Puoi anche usare l'interfaccia riga di comando cloud-cli per creare, aggiornare ed eliminare offerte di servizi.</dd>
<dt>Interfaccia utente {{site.data.keyword.Bluemix_notm}}</dt>
<dd>Usa l'interfaccia utente {{site.data.keyword.Bluemix_notm}} per
creare la tua applicazione selezionando, tra l'altro, quali servizi e runtime combinare per risolvere i
tuoi problemi di business.</dd>
<dt>{{site.data.keyword.contdelivery_full}}</dt>
<dd>Utilizza {{site.data.keyword.contdelivery_short}} per automatizzare le build, i test di unità, le distribuzioni e altro. Modifica e trasmetti il codice tramite la IDE basata sul web avanzato. Crea le toolchain per abilitare integrazioni dello strumento che supportano le attività di sviluppo, distribuzione e funzionamento. Il servizio Continuous Delivery include Delivery Pipeline, Eclipse Orion Web IDE e Git Repos and Issue Tracking. Per ulteriori informazioni, vedi <a href="https://console.ng.bluemix.net/docs/services/ContinuousDelivery/index.html#cd_getting_started">Introduzione a Continuous Delivery</a>.</dd>
</dl>

## Suggerimenti

Mentre sviluppi le tue applicazioni web, avvaliti dei seguenti suggerimenti:

<dl><dt>Persistenza</dt>
<dd>Non specificare archiviazioni locali per le tue applicazioni. Ogni istanza
della tua applicazione, anche se è in esecuzione solo una singola istanza,
può essere riavviata o spostata su una macchina virtuale differente in
qualsiasi momento, di norma per il bilanciamento del carico. Tutto quanto è memorizzato
in un'archiviazione locale viene cancellato quando l'applicazione viene spostata
o eliminata. Per la persistenza, usa uno dei servizi di archivio dati {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>Limiti delle risorse</dt>
<dd>Tieni presente i limiti sulle quantità di risorse che un account di prova
può utilizzare. I limiti sono i seguenti:
<table style="width:100%">
<caption>Tabella 1. Limiti delle risorse {{site.data.keyword.Bluemix_notm}} per un account di prova</caption>
  <th>Tipo di risorsa</th>	<th>Quantità limite</th>
<tr><td>Numero di servizi utilizzati in tutte le applicazioni</td> <td>10</td>
<tr><td>Memoria utilizzata in tutte le applicazioni</td> <td>	2 G</td>
<tr><td>Numero di rotte</td> <td>500</td>
</table>
</dd></dl>
