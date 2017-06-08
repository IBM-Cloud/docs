---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_wind{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Gestione dei classificatori con il toolkit
{: #managing-toolkit}

Puoi gestire i tuoi dati di formazione e classificatori utilizzando l'applicazione web toolkit {{site.data.keyword.nlclassifierfull}}. Il toolkit ti fornisce una vista unificata di tutti i classificatori in esecuzione nella stessa istanza del servizio {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Questa è una release beta del toolkit. La versione beta di questo toolkit potrebbe non essere supportata dopo una nuova release o dopo che il toolkit esce dallo stato beta. Non utilizzare il toolkit per l'utilizzo in produzione.

L'interfaccia web del toolkit semplifica come prepari e verifichi un classificatore. I tuoi esperti del dominio possono utilizzare il toolkit per focalizzarsi sulla qualità dei tuoi dati di formazione.

## Ottenere l'accesso
{: #getting-access}

Puoi trovare un link al toolkit nella pagina del dashboard del servizio {{site.data.keyword.Bluemix_notm}} della tua istanza di {{site.data.keyword.nlclassifiershort}}.

### Accedere personalmente al toolkit

Per trovare il link al toolkit, segui questi passi per ottenere il tuo dashboard del **servizio** {{site.data.keyword.Bluemix_notm}}:

1. Apri il tuo tile del servizio {{site.data.keyword.nlclassifiershort}} accedendo al tuo [Dashboard {{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.{DomainName}/dashboard/services){: new_window}.

	-  Nell'area **Services**, fai clic sul tuo tile del servizio {{site.data.keyword.nlclassifiershort}} per aprire il dashboard dell'istanza. (Se non hai un tile del servizio, [crea un'istanza ![Icona link esterno](../../icons/launch-glyph.svg)](https://console.{DomainName}/catalog/services/natural-language-classifier/){: new_window} del servizio {{site.data.keyword.nlclassifiershort}}.)
1. Nel dashboard del servizio, fai clic su **Access the beta toolkit**.

	Segnati l'URL per un successivo facile accesso al toolkit.
	{: tip}

### Fornire l'accesso al tuo toolkit ad altri

Puoi consentire ad altri di utilizzare il tuo toolkit aggiungendoli in {{site.data.keyword.Bluemix_notm}}.

1.  In {{site.data.keyword.Bluemix_notm}}, fai clic su **Account > Invita membri del team**.
1.  Seleziona l'organizzazione che ospita il tuo servizio classificatore e fai clic su **Avanti**.
1.  Seleziona lo spazio che ospita il tuo servizio classificatore. 
1.  Seleziona il ruolo dello spazio **Developer**. Per i dettagli sui ruoli, consulta [Gestione dei membri dei team e dei ruoli](/docs/admin/users_roles.html).
1.  Immetti l'indirizzo email dell'utente e fai clic su **Invia**.
1.  In una mail separata, invia l'URL del tuo toolkit (che ti sei prima segnato) agli utenti.

## Utilizzi di esempio
{: #example-uses}

In questi esempi, crei e modifichi i dati di formazione, verifichi un classificatore interattivamente o da una serie di dati di verifica e aggiorni i dati di formazione dai risultati.

### Crea i dati di formazione nel toolkit

Prendi familiarità con il toolkit {{site.data.keyword.nlclassifiershort}} creando una piccola serie di dati di formazione con il toolkit.

Prima di poter creare un classificatore, hai bisogno dei dati di formazione. Puoi creare i dati immettendo testi e classi oppure puoi caricare i tuoi dati di formazione da un file CSV che soddisfa il formato file [](/docs/services/natural-language-classifier/using-your-data.html).
1. Nella pagina **Training data** del toolkit, aggiungi un testo. Se non te ne viene in mente uno, aggiungi, "Where is the nearest ATM?". 
1. Assegna una classe al testo immettendola in esso. Per l'esempio ATM, immetti "location".
1. Continua ad aggiungere testo e classi per i tuoi dati di formazione. Puoi assegnare le classi ai testi nei seguenti modi:
	-   Seleziona una classe facendo clic su di essa e quindi fai clic su **Add text**. O seleziona un testo e fai clic su **Assign classes**.
	-   Seleziona una classe, quindi trascina un testo in essa. O seleziona un testo e trascina una classe in esso.

	Puoi utilizzare più di una classe o testo alla volta premendo Ctrl e facendo clic sul testo o sulla classe (premi Command su Mac). Provali.
1. Dopo aver utilizzato i tuoi dati di formazione per un po', fai clic su **Download training data** per salvarli come un backup.

	Puoi anche caricare questo file nel toolkit per utilizzare i dati di formazione successivamente.
	{: tip}
1. Una volta che hai assegnato le classi ad almeno cinque testi, puoi creare un classificatore da questi dati di formazione. Fai clic su **Create classifier**. {{site.data.keyword.watson}} avvia la preparazione del classificatore.

### Verifica il tuo classificatore e aggiorna i tuoi dati di formazione.

Dopo che un classificatore è stato preparato ed è disponibile, puoi verificare come classifica i testi che non ha mai visto prima. Puoi verificare una serie di testi per migliorare i dati di formazione aggiungendo le risposte non corrette o con bassa confidenza.

1.  Nella pagina **Classifiers**, fai clic su **Test and improve performance** per il classificatore che desideri verificare.
1.  Nella pagina **Improve performance**, immetti un testo non presente nei tuoi dati di formazione e fai clic su **Classify**. {{site.data.keyword.watson}} restituisce le classi rilevanti e i rispettivi livelli di confidenza.
1.  Aggiungi ulteriori testi per verificare le prestazioni.
1.  Controlla le risposte. Contrassegna o approva i risultati che desideri aggiungere ai tuoi dati di formazione:
	- Se la classificazione non è corretta, contrassegna il risultato.
	- Se la risposta è corretta ma la confidenza è bassa, aggiungila ai tuoi dati di formazione facendo clic su **Approve**.
1.  Fai clic su **Add to training data** per aggiungere le risposte approvate o contrassegnate ai tuoi dati di formazione.
1.  Nella pagina **Training data**, controlla e aggiorna le classi assegnate ai testi che hai contrassegnato.
1.  Per aggiornare il tuo classificatore con questi nuovi dati di formazione, ne devi creare uno nuovo. Fai clic su **Create classifier**. Dopo averlo preparato, verifica il nuovo classificatore per visualizzare come è stato migliorato.

### Carica i dati per verificare il tuo classificatore

Immettere dei testi da classificare uno ad uno è efficace per i test veloci. Tuttavia se hai una *serie di test*, puoi caricare la serie nel toolkit per classificarne molti contemporaneamente. Una serie di test è un gruppo di testi di esempio non presenti nei tuoi dati di formazione. Utilizza la serie per controllare le prestazioni del classificatore.

1.  Crea un file di serie di test:
	- Il file può utilizzare lo stesso formato dei dati di formazione (in altre parole, può includere le classi corrette) o includere solo i testi, uno per riga. Assicurati che i testi (e le classi) rispettino i requisiti del [formato file](/docs/services/natural-language-classifier/using-your-data.html).
    -   Salava il file con un'estensione `.csv`.
1.  Nella pagina **Classifiers**, fai clic su **Test and improve performance** per il classificatore che desideri verificare.
1.  Nella pagina **Improve performance**, fai clic su **Use test data**. {{site.data.keyword.watson}} carica i dati, classifica ogni testo e restituisce una risposta.
1.  Confronta le risposte con la classificazione corretta e inoltre ricerca la confidenza bassa.
1.  Migliora i dati di formazione aggiungendo ulteriori esempi. Non aggiungere esempi presenti nella tua serie di test se desideri continuare ad utilizzarli per valutare le prestazioni del classificatore.
