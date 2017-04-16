---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Flussi Decahose e PowerTrack {: #decahose_powertrack}

{{site.data.keyword.twittershort}} fornisce l'accesso ai flussi Twitter Decahose e PowerTrack, in base alla registrazione del piano {{site.data.keyword.Bluemix_notm}}. 
Entrambi i flussi spediscono le diverse caratteristiche e i feed in tempo reale per adattarsi alle tue necessità.
{:shortdesc}

Il flusso Decahose è un campionamento casuale del 10% di Twitter Firehose. I Tweet derivano da Twitter in tempo reale e il flusso viene determinato dagli algoritmi di campionamento di Twitter. Per molte analisi statistiche, un campionamento casuale del 10% è sufficientemente accurato. I dati Decahose vengono indicizzati per un periodo di 2 anni, per cui le risposte delle query non possono essere restituire Tweet più vecchi di 2 anni. L'accesso a Decahose è disponibile nel piano gratuito e di ingresso, mentre l'accesso al flusso PowerTrack è esclusivo del piano di ingresso.

Il flusso PowerTrack offre i benefici aggiuntivi di filtro dei Tweet in ingresso, in base al filtro basato sulle regole e definito dall'utente conosciuto come traccia. Come utente del piano di ingresso, puoi creare fino a 1.000 regole per account. Per il filtro avanzato, possono essere combinate più tracce per creare una traccia aggregata. Le seguenti sezioni descrivono le azioni supportate, le proprietà e e gli stati della traccia che puoi eseguire sulle tracce, come la modifica, l'eliminazione e altro.

**Nota**: l'indicizzazione del flusso PowerTrack è limitata a 1 milione di Tweet per mese di calendario. Quando viene raggiunto il limite, l'indicizzazione si arresta per quel mese. All'inizio del successivo mese, puoi riattivare le tue tracce; non vengono riattivate automaticamente. Per massimizzare l'utilizzo del flusso, ti raccomandiamo di gestire al meglio le tue tracce. Ad esempio, le tracce ridondanti possono essere rese inattive.

## Tipi di traccia {: #track_types}

Gli utenti del piano di ingresso possono creare tracce personalizzabili per filtrare i messaggi raccolti nel flusso di dati PowerTrack.  {{site.data.keyword.twittershort}} supporta i seguenti due tipi di traccia.

<dl>
<dt>Regole</dt>
<dd>Tutti i messaggi raccolti in questa traccia corrispondono ad almeno una delle regole associate con la traccia. Puoi aggiungere, modificare e eliminare le regole in questo tipo di traccia.

La [GNIP PowerTrack Rules syntax](http://support.gnip.com/apis/powertrack2.0/rules.html) completa è supportata nelle tracce basate sulle regole. Tutte le query devono essere conformi al {{site.data.keyword.twittershort}} [Linguaggio di query](twitter_rest_apis.html#querylanguage "Linguaggio di query").
</dd>

<dt>Aggregata</dt>
<dd>Una combinazione di due o più regole o tracce aggregate. Le tracce aggregate sono utilizzate per il raggruppamento arbitrario di più tracce. Puoi aggiungere ed eliminare tracce individuali da un tipo di traccia aggregata. Le regole individuali non possono essere aggiunte alle tracce aggregate; utilizza invece un traccia della regola per tale scopo. Le tracce aggregate sono senza stato ma le loro tracce di regole costituenti sono sia **Attiva** che **Inattiva**.</dd>
</dl>

## Proprietà della traccia {: #track_properties}
Le tracce contengono le seguenti proprietà. Alcune proprietà non si applicano ad entrambe le tracce aggregate e basate sulle regole. Ad esempio, la proprietà regole non si applica alle tracce aggregate.

<dl>
<dt>Data di creazione</dt>
<dd>Indica quando è stata creata la traccia; specificato come `YYYYMMDDHHMM`.</dd>

<dt>Data di fine</dt>
<dd>Indica quando alla traccia è stata arrestata la raccolta di messaggi. Il valore specificato deve essere nel futuro e seguire uno dei seguenti formati: `YYYY-MM-DD` o `YYYY-MM-DDTHH:MM:SSZ`. Lo specificare una data nel passato restituisce un errore HTTP 400.

Questa proprietà non si applica alle tracce aggregate.</dd>

<dt>id</dt>
<dd>Un riferimento ID univoco assegnato alla traccia durante la creazione. L'ID è rappresentato in un formato stringa GUID (ad esempio, 3F2504E0-4F89-41D3-9A0C-0305E82C3301) per le tracce aggregate e delle regole.</dd>

<dt>nome</dt>
<dd>Il nome descrittivo della traccia. L'unicità di questa proprietà non è garantita.</dd>

<dt>regole</dt>
<dd>Un array di regole, incluse le parole chiave delle query e altri parametri che definisce i filtri della traccia. Questa proprietà si applica alle tracce basate sulle regole ma non alle tracce aggregate.</dd>

<dt>stato</dt>
<dd>Deve essere **Attiva** o **Inattiva**. Una traccia attiva raccoglie i messaggi, mentre una traccia inattiva non lo fa. Puoi modificare lo stato di una traccia in qualsiasi momento.

Questa proprietà non si applica alle tracce aggregate.</dd>

<dt>ID traccia</dt>
<dd>Un array di ID di traccia. Questa proprietà si applica solo alle tracce aggregate.</dd>

<dt>tipo</dt>
<dd>Indica se il tipo di traccia è **Regola** o **Aggregata**.

Per ulteriori informazioni sulle proprietà della traccia, incluse le operazioni di traccia e lo schema del modello, fai riferimento alla documentazione API REST di {{site.data.keyword.twittershort}}.</dd>
</dl>

