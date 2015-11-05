{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestione di {{site.data.keyword.Bluemix_notm}}
{: #mng}

*Ultimo aggiornamento: 15 ottobre 2015*

Utilizza la Console di gestione per gestire le risorse, monitorare l'utilizzo, amministrare le autorizzazioni degli utenti, visualizzare report,
log, stati di sicurezza e aggiornare le notifiche per il tuo ambiente {{site.data.keyword.Bluemix}} locale o dedicato.
{:shortdesc}

## Accesso alla Console di gestione
{: #oc_access}

Puoi accedere alla Console di gestione immettendo il seguente URL:


`https://opsconsole.<subdomain>.bluemix.net/`. 

<dl>
<dt><strong>&lt;subdomain&gt;</strong></dt>
<dd>Questo valore è il nome della tua istanza locale o dedicata. Il nome del dominio secondario per la tua istanza {{site.data.keyword.Bluemix}} è stato
assegnato durante il caricamento.</dd>
</dl>

## Visualizzazione delle informazioni di sistema
{: #oc_system}

Utilizza la Console di gestione per monitorare le informazioni di sistema. 

Per visualizzare le informazioni di sistema, fai clic su **AMMINISTRAZIONE&gt; INFORMAZIONI DI SISTEMA**.

Puoi espandere e visualizzare le diverse sezioni relative ad aggiornamenti in sospeso. informazioni di sistema generali e
dettagli di configurazione LDAP. 

* Nella sezione Aggiornamenti, puoi visualizzare eventuali aggiornamenti in
sospeso che richiedono un'azione da parte tua. Puoi anche tracciare facilmente i tuoi aggiornamenti utilizzando il
link al calendario al fine di importare gli aggiornamenti pianificati in un'applicazione di calendario. 

<ol>
<li>Per agire su uno specifico aggiornamento, completa la seguente procedura:
<ol type="a">
<li>Fai clic su <strong><em>Numero</em> aggiornamenti in sospeso</strong> per visualizzare tutti gli aggiornamenti
in sospeso.</li>
<li>Selezionare un aggiornamento da effettuare o di cui visualizzare i dettagli, che includono la finestra di
aggiornamento, la data pianificata o lo stato di interruzione.</li>
<li>Fai clic su <strong>IMPOSTA DATE NON DISPONIBILI</strong> per impostare specifici giorni nella finestra di
aggiornamento come non adatti all'applicazione dell'aggiornamento. Se imposti delle date non disponibili, IBM approva e
pianifica il tuo aggiornamento in base alle selezioni da te effettuate. Una volta approvato e pianificato l'aggiornamento,
riceverai una notifica.</li>
<li>Fai clic su <strong>APPROVA</strong> per approvare l'aggiornamento, se non hai impostato alcuna data non
disponibile. Se approvi, l'aggiornamento viene applicato durante la finestra di aggiornamento pianificato. IBM invia una
notifica all'inizio e alla fine della distribuzione dell'aggiornamento.</li>
</ol>
</li>
<li>Per importare i tuoi aggiornamenti pianificati in un'applicazione di calendario a tua scelta, completa la seguente procedura:
<ol type="a">
<li>Apri l'applicazione di calendario.</li>
<li>Importa il calendario di aggiornamenti incollando l'**URL calendario** elencato nella pagina Informazioni di sistema della tua applicazione. In alternativa, scarica il file di calendario facendo clic su URL calendario, quindi importalo nella tua applicazione di calendario utilizzando il file `.ics`.</li>
<li>Immetti le tue credenziali.</li>
<li>Visualizza i tuoi aggiornamenti pianificati.</li>
</ol>
</li>
</ol>

* Nella sezione Informazioni generali, puoi visualizzare le seguenti informazioni: 
    * Informazioni di base relative alla build {{site.data.keyword.Bluemix_notm}}.
    * Informazioni sull'API tra cui la versione, l'URL, la regione e un link alla documentazione della CLI.
    * Informazioni del dominio condiviso relative al tuo sistema e servizio.
    * Statistiche relative al numero totale di applicazioni, utenti e organizzazioni.
* Nella sezione Dettagli di configurazione LDAP, puoi selezionare il server LDAP
e visualizzare le informazioni relative alle associazioni di utenti e gruppi. Se stai utilizzando l'ID Web {{site.data.keyword.IBM}}, viene indicato nella sezione Dettagli di configurazione
LDAP. 

## Visualizzazione delle informazioni sull'utilizzo
{: #oc_resource}

Utilizza la Console di gestione per monitorare l'utilizzo delle risorse e della rete. 

Per visualizzare le informazioni sulle risorse, fai clic su **AMMINISTRAZIONE&gt; UTILIZZO**.

Nella sezione Monitoraggio risorse, puoi visualizzare le seguenti
informazioni:

* Informazioni sull'utilizzo delle risorse, ad esempio la quantità di GB di memoria e di GB di spazio su disco
utilizzata. Puoi visualizzare il valore medio dell'utilizzo della CPU tra tutti gli agent DEA (Droplet Execution Agent). Fai clic sul
tile **CPU** per visualizzare l'utilizzo della CPU per ogni DEA. Il DEA con
l'utilizzo maggiore viene elencato per primo e ciascuno è identificato dal proprio lavoro e indirizzo IP. L'utilizzo della CPU è
suddiviso in tre categorie che includono la quantità di CPU utilizzata nei processi del sistema, la quantità
utilizzata nei processi dell'utente e la quantità utilizzata nel processi in attesa.
* Informazioni sull'utilizzo della rete per la larghezza di banda in entrata e in uscita, nel corso del giorno, settimana o
mese precedente.
I dati visualizzati si basano sulla somma del traffico in entrata e in uscita per entrambe le reti pubblica e
privata.
* Tempo medio di risposta per {{site.data.keyword.Bluemix_notm}} nel corso degli ultimi 10 minuti, ora e giorno.
* Transazioni medie al secondo per {{site.data.keyword.Bluemix_notm}} nel corso degli ultimi 10
minuti, ora e giorno.

## Visualizzazione dei report
{: #oc_report}

Puoi visualizzare report e log di sicurezza, quali DataPower&trade;, firewall e controllo accessi, per
la tua istanza {{site.data.keyword.Bluemix_notm}}.

Per visualizzare i report e i log, fai clic su **AMMINISTRAZIONE &gt; REPORT E LOG**.

Scegli tra le seguenti opzioni:

* Puoi selezionare le date di inizio e di fine dai campi per filtrare i report e i log da
visualizzare.
* Puoi espandere e visualizzare i diversi report dal riquadro di navigazione a
sinistra.
* Puoi eseguire ricerche nella tua raccolta di report e log. La ricerca si applica ai nomi di report
nonché al contenuto del testo incluso nei report e nei log. Puoi anche scegliere di
filtrare la ricerca per **Eventi amministrazione**, **Report
DataPower**, **Firewall** e **Controllo
accessi**.
* Durante la visualizzazione di un report o log, puoi fare clic sull'icona ![Scarica](images/icon_download.png) nell'angolo superiore destro del report per scaricarlo.

## Visualizzazione dello stato
{: #oc_status}

Puoi monitorare lo stato della tua istanza {{site.data.keyword.Bluemix_notm}} attraverso la Console di
gestione. Inoltre, puoi sottoscrivere a un feed RSS per le notifiche in modo da non doverle controllare personalmente.  

Per visualizzare lo stato relativo alla tua istanza {{site.data.keyword.Bluemix_notm}}, completa la seguente procedura:

1. Nella Console di gestione, nell'angolo superiore destro, fai clic
sull'icona **Impostazioni profilo**.

2. Quindi, fai clic su **Stato**.

Viene visualizzata la pagina Stato del sistema. Il riquadro a sinistra visualizza lo stato
dei tuoi runtime e servizi tra le regioni e l'istanza {{site.data.keyword.Bluemix_notm}}. Il riquadro a destra mostra
le notifiche.

3. Se hai configurato il tuo browser per i feed RSS, puoi sottoscrivere a un feed RSS delle
notifiche. Individua l'icona ![RSS](images/icon_RSS.png) posta a destra di **AGGIORNAMENTI** nella parte superiore sinistra dell'elenco di
notifiche e seleziona una delle seguenti azioni: 

* Trascina l'icona ![RSS](images/icon_RSS.png) nel lettore RSS.
* Fai clic con il tasto destro del mouse sull'icona RSS, seleziona **Copia indirizzo link** e incolla l'URL
nel lettore RSS. 

4. Filtra le notifiche da visualizzare. Fai clic su **FILTRO** in alto a
destra dell'elenco di notifiche. Puoi quindi cercare e restringere l'elenco di notifiche immettendo
una parola che ti aspetti di trovare in una notifica, ad esempio "manutenzione". Oppure, puoi
selezionare quali notifiche visualizzare in base a **Tipo**,
**Regione**, **Categoria**, **Data di inizio**
o **Data di fine**. 

## Gestione del Catalogo
{: #oc_catalog}

Puoi gestire quali servizi e starter {{site.data.keyword.Bluemix_notm}} saranno visibili agli utenti nel Catalogo {{site.data.keyword.Bluemix_notm}}.

Per utilizzare la Console di gestione per gestire il Catalogo,
fai clic su **AMMINISTRAZIONE &gt; GESTIONE CATALOGO**.

Seleziona un tile di servizio o starter per modificare la visibilità del piano del servizio o dello starter. Per modificare la
visibilità, scegli tra le seguenti opzioni:
* Per mostrare il servizio o starter nascosto in modo che sia visibile agli utenti nel
Catalogo, seleziona **ABILITA TUTTI I PIANI**.
* Per nascondere agli utenti il servizio o starter nel Catalogo {{site.data.keyword.Bluemix_notm}},
seleziona **DISABILITA TUTTI I PIANI**.
* Per controllare la visibilità di un singolo piano, seleziona il nome del piano, quindi utilizza
il menu a discesa per selezionare **Abilita per tutte le organizzazioni**, **Disabilita per tutte
le organizzazioni** o **Abilita piano per specifiche
organizzazioni**.

## Amministrazione delle organizzazioni
{: #oc_organizations}

Puoi gestire le tue organizzazioni attraverso la creazione e l'eliminazione di organizzazioni, l'aggiunta di gestori alle organizzazioni e il monitoraggio dell'utilizzo delle quote.

Per utilizzare la Console di gestione per gestire le tue organizzazioni, fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE ORGANIZZAZIONI**.

Puoi espandere e visualizzare le diverse sezioni. Puoi anche rivedere e gestire i piani di quota per le
tue organizzazioni.

* Per creare una nuova organizzazione e aggiungere gestori, fai clic su <strong>CREA
ORGANIZZAZIONE</strong>. 
Immetti un nome per l'organizzazione, quindi specifica il nome o l'e-mail della
persona che vuoi aggiungere come gestore. Puoi aggiungere più
di un gestore immettendo e selezionando più nomi. Fai clic su <strong>CREA
ORGANIZZAZIONE</strong> per salvare le modifiche e creare l'organizzazione. 
* Nella sezione Monitoraggio quota, puoi espandere la sezione e visualizzare
le seguenti informazioni:
    * Utilizzo della memoria dell'ambiente. Questa sezione mostra in dettaglio l'utilizzo della memoria per l'intero ambiente di sistema.
	Il grafico fornisce informazioni che includono la memoria di sistema utilizzata, la memoria totale di sistema, la quota
utilizzata e la quota totale assegnata. Il seguente elenco di termini definisce i tipi di utilizzo di memoria
visualizzati nel grafico.
	<dl>
	<dt><strong>Memoria di sistema utilizzata</strong></dt>
	<dd>La memoria fisica utilizzata dal tuo ambiente.</dd>
	<dt><strong>Memoria totale di sistema</strong></dt>
	<dd>La memoria fisica totale disponibile nel tuo ambiente.</dd>
	<dt><strong>Quota distribuita</strong></dt>
	<dd>La somma di memoria assegnata per tutte le applicazioni distribuite, tra tutte le organizzazioni. La somma
	della quota distribuita può superare la memoria fisica totale del sistema per il tuo ambiente. Ad esempio, se
disponi di una memoria totale di sistema pari a 16 GB e assegni 4 GB di memoria ciascuna per un totale di cinque
diverse organizzazioni, la quota totale supera la memoria di sistema complessiva che ti è stata assegnata
per tutte le organizzazioni. Tuttavia, in molti casi, è possibile che non tutte le organizzazioni utilizzino
la quota totale assegnata singolarmente a ciascuna organizzazione. Inoltre, è possibile che le organizzazioni non utilizzino
contemporaneamente la propria assegnazione di quota totale della memoria. </dd>
	<dt><strong>Quota totale</strong></dt>
	<dd>La memoria totale assegnata tra tutte le organizzazioni.</dd>
	</dl>
	* Utilizzo della memoria dell'organizzazione. Questa sezione mostra in dettaglio l'utilizzo della memoria a livello di organizzazione. Puoi
visualizzare l'indennità di quota totale e la quota che viene distribuita per ogni organizzazione. Il grafico
fornisce informazioni che vengono elencate in base all'utilizzo massimo della memoria per ogni organizzazione e, per impostazione predefinita,
viene elencata per prima l'organizzazione che utilizza la maggiore quantità di memoria. Puoi ordinare le informazioni per
**Utilizzo massimo memoria** e **Assegnazione memoria in eccesso**.
	<dl>
	<dt><strong>Utilizzo massimo memoria</strong></dt>
	<dd>Usa questa opzione per identificare l'organizzazione che utilizza la maggior quantità di memoria. Ordina per Utilizzo massimo
	memoria per identificare le organizzazioni che utilizzano la maggior quantità di memoria. L'elenco è ordinato
per quota distribuita. </dd>
	<dt><strong>Assegnazione memoria in eccesso</strong></dt>
	<dd>Usa questa opzione per identificare le organizzazioni che hanno un piano di quota superiore a quello necessario.
	Ordina per Assegnazione memoria in eccesso per identificare le organizzazioni che utilizzano la minore quantità di memoria per
la quota assegnata per l'organizzazione. </dd>
	</dl>
* Per modificare il piano di quota per un'organizzazione, fai clic sulla barra del grafico relativo
all'organizzazione che vuoi modificare nella sezione Utilizzo della memoria dell'organizzazione o seleziona il nome
dell'organizzazione dalla sezione Elenco organizzazioni. Nella pagina Modifica
organizzazione, puoi cambiare il piano di quota, modificare il nome dell'organizzazione e aggiungere o
rimuovere gestori. Se selezioni un piano di quota che non è sufficiente per l'utilizzo corrente
nell'organizzazione, riceverai un messaggio. Per salvare le modifiche apportate nella pagina Modifica
organizzazione, fai clic su **SALVA**.
* Nella sezione Elenco organizzazioni, puoi visualizzare tutte le organizzazioni
nell'ambiente di {{site.data.keyword.Bluemix_notm}}.
	* Per eliminare l'organizzazione, fai clic su ![Elimina](images/icon_trash.png) nella colonna Azioni.
	* Per visualizzare e modificare il piano di quota per un'organizzazione, fai clic sul nome dell'organizzazione
nell'elenco.
	* Per modificare il nome dell'organizzazione e aggiungere o rimuovere i gestori, fai clic sul nome dell'organizzazione
nell'elenco.

## Gestione di utenti e autorizzazioni
{: #oc_useradmin}
Puoi aggiungere utenti alla tua istanza {{site.data.keyword.Bluemix_notm}} dal registro utenti della tua azienda tramite LDAP. Puoi aggiungere gli utenti singolarmente
o in gruppi e visualizzarne le autorizzazioni. Se disponi dell'autorizzazione `ammin`,
puoi anche impostare e gestire le autorizzazioni per gli altri utenti.

Per utilizzare la Console di gestione per gestire gli utenti, fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE UTENTI**.

La pagina Amministrazione utenti visualizza tutti gli utenti per l'istanza locale o dedicata.
Sono visualizzate le autorizzazioni per ciascun utente. Le autorizzazioni possono essere: Nessuna,
`Ammin`, `Catalogo`, `Accesso`,
`Report` e `Utenti`. È possibile abilitare le autorizzazioni oppure
è possibile fornire agli utenti la capacità di `visualizzazione` o di `scrittura` per
l'autorizzazione indicata, come rappresentato dalle icone. Vedi [Autorizzazioni](#permissions) per una descrizione
di ciascun tipo di icona e la relativa spiegazione. 

Scegli tra le seguenti opzioni:
* Individua utenti. Puoi individuare gli utenti nella tabella utilizzando il campo **Ricerca**
posto in alto.
* Aggiungi utenti. Se disponi dell'autorizzazione `ammin` o
dell'autorizzazione `utenti` con la capacità di `scrittura`, puoi aggiungere gli utenti. Per aggiungere un utente o un gruppo di utenti, fai clic su **AGGIUNGI SINGOLO UTENTE** o **AGGIUNGI GRUPPO
DI UTENTI**. Nel campo **Ricerca**, immetti un nome utente o nome gruppo da
ricercare, quindi seleziona l'organizzazione a cui aggiungere l'utente o il gruppo di utenti
dall'elenco **Organizzazione**. Una volta trovato l'utente o il gruppo che desideri aggiungere,
fai clic sul nome utente e quindi su **AGGIUNGI UTENTE** o **AGGIUNGI UTENTI**.
I gruppi di più di 50 utenti vengono aggiunti attraverso un processo batch in background. Se l'operazione di aggiunta viene
completata correttamente, l'utente o il gruppo viene aggiunto alla tabella per la visualizzazione e la ricerca. Quando gli utenti vengono aggiunti,
non dispongono di autorizzazioni.
* Modificare autorizzazioni e organizzazioni. Se disponi dell'autorizzazione `ammin`, puoi modificare
le autorizzazioni e le organizzazioni per gli altri utenti. Per modificare le autorizzazioni, individua
l'utente e fai clic sul nome utente. Per abilitare o disabilitare autorizzazioni, seleziona dalle seguenti opzioni nella finestra che viene visualizzata:
	* Seleziona **Attivo** dall'elenco per abilitare un'autorizzazione.
	* Seleziona **Lettura** dall'elenco per consentire all'utente di disporre
della capacità di `visualizzazione` (sola lettura) per tale autorizzazione oppure **Scrittura**
per consentire la capacità di `scrittura` (modifica o aggiunta e rimozione) per l'autorizzazione.
	* Seleziona **Disattivo** per disabilitare l'autorizzazione.
Per modificare le organizzazioni, seleziona dalle seguenti opzioni:
	* Aggiungi l'utente a un'organizzazione utilizzando il campo di ricerca per individuare un'organizzazione, facendo clic per
selezionare dalle opzioni e facendo clic su **AGGIUNGI**.
	* Rimuovi un utente da un'organizzazione facendo clic sull'icona ![Rimuovi, rappresentato da un segno meno](images/icon_remove.png).
Al termine, fai clic su **SALVA**.
* Rimuovi gli utenti. Se disponi dell'autorizzazione `ammin` o
dell'autorizzazione `utenti` con la capacità di `scrittura`, puoi rimuovere
gli utenti.
Per rimuovere un utente, individua l'utente e fai clic sull'icona ![Elimina](images/icon_trash.png) e quindi su **Rimuovi**.

### Autorizzazioni
{: #permissions}

È possibile assegnare agli utenti le seguenti autorizzazioni:

| **Autorizzazione utente** | **Descrizione** |       
|-----------------|-------------------|
| Ammin | Gli utenti con l'autorizzazione `ammin` possono
modificare le autorizzazioni per gli altri utenti. | 
| Catalogo | Agli utenti con l'autorizzazione `catalogo` può essere assegnata la capacità di `visualizzare ` o `scrivere` (modificare) quali servizi sono disponibili nell'istanza locale o dedicata.  |  
| Accesso | Gli utenti con l'autorizzazione `accesso` possono accedere alla Console di gestione. Senza questa autorizzazione, gli utenti non possono accedere. |
| Report | Agli utenti con l'autorizzazione `report` può essere assegnata la capacità di
`visualizzare` o `scrivere` (modificare) i report di sicurezza. |
| Utenti | Agli utenti con l'autorizzazione `utenti` può essere assegnata la capacità
di `visualizzare` l'elenco di utenti o di `scrivere` (aggiungere o rimuovere) gli utenti. Questa autorizzazione non ti consente di impostare le autorizzazioni per gli altri utenti.|

*Tabella 1. Autorizzazioni*

È possibile abilitare le autorizzazioni oppure è possibile fornire agli utenti la capacità di `visualizzazione` o
di `scrittura` per l'autorizzazione indicata, come rappresentato dalle seguenti icone:

* L'icona ![Abilitato, rappresentata da un segno di spunta](images/icon_enabled.png) accanto a un'autorizzazione significa che è abilitata.
* L'icona ![Visualizza, rappresentata da un occhio](images/icon_read.png) significa che l'utente dispone della capacità di `visualizzazione` (sola lettura) per tale
autorizzazione.
* L'icona ![Scrittura, rappresentata da una matita](images/icon_write.png) significa che l'utente dispone della capacità di `scrittura` (modifica, aggiunta o rimozione) per tale
autorizzazione.

## Gestione degli utenti con la API REST Admin
{: #usingadminapi}

Puoi utilizzare l'API REST `Admin` per aggiungere e rimuovere utenti dalla tua
istanza {{site.data.keyword.Bluemix_notm}}.
Gli endpoint della API REST `Admin` e le risposte JSON sono fornite su base sperimentale per abilitare le operazioni di base da una riga di comando. Gli endpoint e gli URL negli esempi nelle presenti
informazioni possono variare o potrebbero essere abbandonate con breve preavviso.

I seguenti strumenti sono prerequisiti per utilizzare gli esempi di seguito riportati. Puoi anche scegliere di
            utilizzare altri strumenti.
* cURL, per immettere richieste API REST come comandi. cURL è un programma di utilità gratuito che puoi
                    utilizzare per inviare richieste HTTP a un server e ricevere le risposte
                    attraverso un'interfaccia riga di comando. Puoi
scaricare cURL dal [sito di download cURL](http://curl.haxx.se/download.html){: new_window}.
* Python, per utilizzare lo strumento JSON Pretty-Print Python. Questo strumento
facoltativo prende il testo JSON come input e fornisce un output facile da leggere. Puoi scaricare Python dal [sito di download Python](https://www.python.org/downloads){: new_window}.

### Accesso alla Console di gestione

Prima di poter eseguire qualsiasi richiesta API `Admin`,
devi eseguire l'accesso alla Console di gestione. Se disponi dell'autorizzazione `ammin`
o dell'autorizzazione `utenti` con la capacità di `scrittura`,
puoi aggiungere o rimuovere utenti. Per modificare le autorizzazioni di altri utenti devi disporre
dell'autorizzazione `ammin`.

Per accedere alla Console di gestione, puoi utilizzare l'autenticazione di accesso di base
sull'endpoint `https://<your_host>.ibm.com/login`. Il server restituisce un cookie con la tua sessione. Puoi utilizzare tale
cookie per tutte le operazioni con la Console di gestione.

**Nota:** la sessione non sarà più valida se non viene utilizzata per qualche ora.

Per accedere alla
Console di gestione, esegui questo comando:

`curl --user <id_utente>:<password> -c ./cookies.txt --header "Accept: application/json" https://<il_tuo_host>.ibm.com/login | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">--user <em>id_utente</em>:<em>password</em></dt>
<dd class="pd">Accetta l'ID utente e la password e invia un'intestazione di autorizzazione di base.</dd>


<dt class="pt dlterm">-c <em>nomefile</em></dt>
<dd class="pd">Memorizza l'ID utente e la password specificati come un cookie nel file specificato.</dd>


<dt class="pt dlterm">--header</dt>
<dd class="pd">Invia un'intestazione Accept.</dd>

</dl>

Il seguente esempio mostra l'output di questo
                comando:
```
{
    "message": "Logged in",
    "name": {
        "familyName": "*last_name*",
        "givenName": "*first_name*"
    }
}
```
{: screen}

### Elenco delle organizzazioni
{: #listingorg}

Quando aggiungi un utente, devi specificare un'organizzazione. Puoi
utilizzare la API REST `Admin` per elencare tutte le organizzazioni. Per elencare le organizzazioni,
devi disporre dell'autorizzazione `utenti` con la capacità di `lettura`.
Per elencare tutte le organizzazioni, immetti il seguente comando:

`curl -b ./cookies.txt https://<il_tuo_host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>nomefile</em></dt>
<dd class="pd">Passa l'ID utente e la password memorizzati precedentemente
con l'opzione <samp class="ph codeph">-c</samp> nel file al server HTTP come
un cookie.</dd>

</dl>

Per ciascuna organizzazione, i risultati includono le seguenti informazioni: 
* `"guid"`, GUID dell'organizzazione
* `"name"`, nome dell'organizzazione

Il seguente esempio mostra l'output di questo
                comando:
``` 
{
     "resources": [
         {
             "guid": "05af098d-d476-4fb0-8b87-a84350e72af3",
             "name": "org-1"
         },
         {
             "guid": "5129a5a8-37c2-4ee4-a9b2-bebae3531db5",
             "name": "org-2"
         },
 
		 		 ....
		 		 
		 ],
		 "total_results": 284
}
```
{: screen}

### Elenco degli utenti
{: #listingusr}

Puoi determinare se un utente è già stato aggiunto al tuo
ambiente {{site.data.keyword.Bluemix_notm}}
utilizzando l'API REST `Admin` per elencare gli utenti registrati. Per elencare gli
utenti registrati, devi disporre dell'autorizzazione `utenti` con la capacità di `lettura`.
Per elencare tutti gli utenti, immetti il seguente comando:

`curl -b ./cookies.txt https://<il_tuo_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>nomefile</em></dt>
<dd class="pd">Passa l'ID utente e la password memorizzati precedentemente
con l'opzione <samp class="ph codeph">-c</samp> nel file al server HTTP come
un cookie.</dd>
</dl>

Per ciascun utente registrato, i risultati includono le seguenti informazioni: 
* `"first_name"` (nome) e
                                `"last_name"` (cognome)
* `"user_id"`, ID utente e indirizzo email
* `"guid"`, GUID dell'organizzazione.
* `"permissions"`, ossia le autorizzazioni assegnate all'utente per la Console di gestione.

Il seguente esempio mostra l'output di questo
                comando:

```
{
    "next_url": "/codi/v1/users?results_per_page=100&amp;page=2",
    "prev_url": "",
    "resources": [
        {
            "active": true,
            "created_at": "2015-04-08T17:38:51.788Z",
            "created_by": "",
            "first_name": "some first name",
            "guid": "5d5268cf-39c0-48d3-96ae-7afe928e5dd7",
            "last_name": "some last name",
            "permissions": [
                {
                    "display": "ops.admin"
                },
                {
                    "display": "ops.catalog.write"
                },
                {
                    "display": "ops.reports.write"
                },
                {
                    "display": "ops.catalog.read"
                },
                {
                    "display": "ops.users.write"
                },
                {
                    "display": "ops.reports.read"
                },
                {
                    "display": "ops.login"
                },
                {
                    "display": "ops.users.read"
                }
            ],
            "user_id": "someid@us.ibm.com"
        },
		 		 ...
		 		 
		 		 
     }
    ],
    "total_pages": 395,
    "total_results": 39421
}

```
{: screen}

### Aggiunta di un utente

Puoi utilizzare l'API REST `Admin` per aggiungere utenti alla
tua istanza {{site.data.keyword.Bluemix_notm}}. Per aggiungere utenti devi disporre dell'autorizzazione `utenti`
con la capacità di `scrittura`.

Puoi aggiungere un solo utente o un elenco di utenti. Inoltre, puoi aggiungere utenti a una singola
organizzazione o a più organizzazioni. -->Per
aggiungere un utente, devi fornire le seguenti informazioni:

* Nome e cognome dell'utente. Fornisci il
nome (`"first_name"`) e il cognome (`"last_name"`) dall'[Elenco degli utenti](index.html#listingusr).
* Indirizzo e-mail e ID utente: fornisci l'`"id_utente"` dall'[Elenco degli utenti](index.html#listingusr) sia per l'indirizzo e-mail che per l'ID utente.
* `"guid"`. Fornisci il GUID dell'organizzazione dall'[Elenco delle organizzazioni](index.html#listingorg).

Per fornire le informazioni, ti servi di un file JSON.

`curl -b ./cookies.txt https://<il_tuo_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>nomefile</em></dt>
<dd class="pd">Passa l'ID utente e la password memorizzati precedentemente
con l'opzione <samp class="ph codeph">-c</samp> nel file al server HTTP come
un cookie.</dd>
</dl>

<ol>
<li>Crea un file JSON che contiene le informazioni in un formato JSON corretto. 
<p>Ad esempio, crea un file denominato `user.json` che presenta
questo contenuto:</p>
<code>
{
    "members": [
        {
            "emails": [
                "un_id_utente@dominio.com"
            ],
            "first_name": "un_nome",
            "last_name": "un_cognome",
            "user_id": "un_id_utente@domain.com"
        }
    ],
    "organization_roles": [
        {
            "id": "7a891f9c-e4e7-46c7-8b4e-dffaa7eb3bcd"
        }
    ]
}
</code><br/><br/>
</li>
<li>Pubblica il contenuto del file JSON nell'endpoint dell'utente immettendo il seguente
comando: <br/><br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<il_tuo_host>.ibm.com/codi/v1/users
</code>
</li>
</ol>

<dl class="parml">

<dt class="pt dlterm">-v </dt>
<dd class="pd">Specifica un output dettagliato.</dd>


<dt class="pt dlterm">-X POST</dt>
<dd class="pd">Specifica una richiesta POST, sovrascrivendo la richiesta GET predefinita.</dd>


<dt class="pt dlterm">-H "Content-Type: application/json"</dt>
<dd class="pd">Specifica l'intestazione content-type, che in questo caso è JSON.</dd>


<dt class="pt dlterm">-d *dati*</dt>
<dd class="pd">Specifica i dati, in questo caso il file `user.json`,
da inviare nella richiesta POST al server HTTP.</dd>

</dl>



Il seguente esempio mostra l'output di questo
                comando:

``` 
* Connected to localhost (127.0.0.1) port 3000 (#0)
 > POST /codi/v1/users HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 > Content-Type: application/json
 > Content-Length: 333
 > 
 * upload completely sent off: 333 out of 333 bytes
 &lt; HTTP/1.1 201 Created
 &lt; x-powered-by: Express
 &lt; vary: X-HTTP-Method-Override
 &lt; content-type: application/json
 &lt; date: Wed, 22 Apr 2015 19:32:54 GMT
 &lt; connection: close
 &lt; transfer-encoding: chunked
 &lt; X-Time_Check: Proxy Time: 5612 msec
 ``` 
{: screen}

### Rimozione di un utente

Puoi utilizzare l'API REST `Admin` per rimuovere gli utenti dall'istanza
{{site.data.keyword.Bluemix_notm}}. Per rimuovere gli utenti registrati devi disporre dell'autorizzazione `utenti` con la capacità di `scrittura`.

Per rimuovere un utente, devi fornire l'ID dell'utente: Immetti il seguente comando:

`curl -v -b ./cookies.txt -X DELETE https://<il_tuo_host>.ibm.com/codi/v1/users?user_id=<un_id_utente@domain.com>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-X DELETE</dt>
<dd class="pd">Specifica una richiesta DELETE.</dd>
</dl>

Il seguente esempio mostra l'output di questo
                comando:

```
 * connect to ::1 port 3000 failed: Connection refused
 *   Trying 127.0.0.1...
 * Connected to localhost (127.0.0.1) port 3000 (#0)
 &gt; DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 &gt; User-Agent: curl/7.37.1
 &gt; Host: localhost:3000
 &gt; Accept: */*
 &gt; Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 &gt; 
 &lt; HTTP/1.1 201 Created
 &lt; x-powered-by: Express
 &lt; content-type: application/json
 &lt; date: Wed, 22 Apr 2015 21:01:09 GMT
 &lt; connection: close
 &lt; transfer-encoding: chunked
 &lt; X-Time_Check: Proxy Time: 1922 msec
 &lt; 
 ``` 
{: screen}

## Gestione degli utenti con la CLI cf
{: #usingadmincli}

Puoi gestire gli utenti per il tuo
ambiente {{site.data.keyword.Bluemix_notm}}
utilizzando l'interfaccia riga di comando Cloud Foundry con il plug-in
{{site.data.keyword.Bluemix_notm}} Admin CLI. Ad
esempio, puoi aggiungere utenti da un registro LDAP.

Prima di iniziare, installa l'interfaccia riga di comando cf. Il plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI richiede cf versione 6.11.2 o successive. [Scarica
l'interfaccia riga di comando Cloud Foundry](https://github.com/cloudfoundry/cli/releases){: new_window}

**Limitazione:** l'interfaccia riga di comando Cloud Foundry non è supportata
da Cygwin. Utilizza l'interfaccia riga di comando Cloud Foundry
in una finestra riga di comando diversa da quella di Cygwin.

### Aggiunta del plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI

Dopo aver installato l'interfaccia riga di comandi cf, puoi
aggiungere il plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI.

Completa la seguente procedura per aggiungere il deposito e installare
il plug-in: 

<ol>
<li>Per aggiungere il repository del plug-in {{site.data.keyword.Bluemix_notm}} Admin, immetti il seguente comando:<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://opsconsole.<subdomain>;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">Dominio secondario dell'URL per la tua istanza {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>
</li>
<li>Per installare il plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI, immetti il seguente comando: <br/><br/>
<code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

### Utilizzo del plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI

Puoi utilizzare il plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI per aggiungere o rimuovere utenti, assegnare o annullare l'assegnazione degli utenti dalle organizzazioni ed
effettuare altre attività di gestione. Per visualizzare un elenco di comandi, immetti il seguente
comando:

`cf plugins`
{: codeblock}

Per ulteriore assistenza per un comando, utilizza
l'opzione `--help`.

#### Connessione e accesso a {{site.data.keyword.Bluemix_notm}}

Prima di poter utilizzare il plug-in Admin CLI per la gestione degli utenti,
devi connetterti ed effettuare l'accesso.

<ol>
<li>Per connetterti all'endpoint API {{site.data.keyword.Bluemix_notm}}>, immetti il seguente comando: <br/><br/>
<code>
cf api https://api.<subdomain>.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">Dominio secondario dell'URL per la tua istanza {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>
<p>Puoi controllare l'URL corretto nella pagina Risorse e informazioni della
Console di gestione. L'URL viene mostrato
nella sezione Informazioni API all'interno del campo **URL API**.</p>
</li>
<li>Accedi a {{site.data.keyword.Bluemix_notm}} con il seguente comando: <br/><br/>
<code>
cf login
</code>
</li>
</ol>

#### Aggiunta di un utente

Puoi aggiungere un utente al tuo
ambiente {{site.data.keyword.Bluemix_notm}} da
un registro LDAP. Immetti il seguente comando: 

`cf bluemix-admin-add-user <user_name> <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Il nome dell'utente nel registro LDAP.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Il nome o GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui aggiungere l'utente.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **baau** come alias per il
nome comando **bluemix-admin-add-user** più lungo.

#### Rimozione di un utente

Puoi rimuovere un utente dal
tuo ambiente {{site.data.keyword.Bluemix_notm}}
immettendo il seguente comando: 

`cf bluemix-admin-remove-user <user_name>`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Il nome dell'utente in {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Suggerimento:** puoi anche utilizzare **baru** come alias per il
nome comando **bluemix-admin-remove-user** più lungo.

#### Aggiunta ed eliminazione di un'organizzazione

Puoi aggiungere ed eliminare un'organizzazione.

* Per aggiungere un'organizzazione, immetti il seguente comando:

`cf Bluemix-admin-create-organization <organization> <manager>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Il nome o GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} da aggiungere.</dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">Il nome utente del gestore per l'organizzazione.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **baco** come alias per il nome comando
**bluemix-admin-create-organization** più lungo.

* Per eliminare un'organizzazione, immetti il seguente comando:

`cf Bluemix-admin-delete-organization <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Il nome o GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} da eliminare.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **bado** come alias per il nome comando
**bluemix-admin-create-organization** più lungo.

#### Assegnazione di un utente a un'organizzazione

Puoi assegnare un utente del tuo
ambiente {{site.data.keyword.Bluemix_notm}} a una
determinata organizzazione. Immetti il seguente comando: 

`cf bluemix-admin-set-org <user_name> <organization> [<role>]`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Il nome dell'utente in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Il nome o GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui assegnare l'utente.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">Vedi [Ruoli](#roles) per i ruoli utente di {{site.data.keyword.Bluemix_notm}} e le relative
descrizioni.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **baso** come alias per il nome comando
**bluemix-admin-set-org** più lungo.

#### Annullamento dell'assegnazione di un utente da un'organizzazione

Puoi annullare l'assegnazione di un utente del tuo
ambiente {{site.data.keyword.Bluemix_notm}} da una
determinata organizzazione. Immetti il seguente comando: 

`cf bluemix-admin-unset-org <user_name> <organization> [<role>]`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">Il nome dell'utente in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Il nome o GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui assegnare l'utente.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">Vedi [Ruoli](#roles) per i ruoli utente di {{site.data.keyword.Bluemix_notm}} e le relative
descrizioni.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **bauo** come alias per il nome comando
**bluemix-admin-unset-org** più lungo.

### Ruoli

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">Gestore organizzazione. Un gestore organizzazione ha l'autorità per svolgere le seguenti azioni:
<ul>
<li>Creare o eliminare spazi all'interno dell'organizzazione.</li>
<li>Invitare gli utenti all'organizzazione e gestirli.</li>
<li>Gestire i domini dell'organizzazione.</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">Gestore fatturazione. Un gestore fatturazione può visualizzare le informazioni relative all'utilizzo di runtime e servizi
per l'organizzazione.</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">Revisore organizzazione. Un revisore organizzazione può visualizzare i contenuti di applicazioni e servizi in uno
spazio.</dd>
</dl>

### Impostazione di una quota per un'organizzazione

Puoi impostare la quota di utilizzo per una determinata organizzazione. 

`cf bluemix-admin-set-quota <organization> <plan>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Il nome o GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} per la quale impostare la quota.</dd>
<dt class="pt dlterm">&lt;plan&gt;</dt>
<dd class="pd">Il piano di quota per un'organizzazione.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **basq** come alias per il nome comando
**bluemix-admin-set-quota** più lungo.

### Aggiunta, eliminazione e recupero dei report

Puoi aggiungere, eliminare e recuperare i report di sicurezza. 
* Per aggiungere un report, immetti il seguente comando:

`cf bluemix-admin-add-report <category> <date> <PDF|TXT|LOG> <RTF>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">La categoria per il report. Se nel nome è presente uno spazio, racchiudi il nome
tra virgolette.</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">La data del report in formato <samp class="ph codeph">AAAAMMGG</samp>.</dd>
<dt class="pt dlterm">&lt;PDF|TXT|LOG&gt;</dt>
<dd class="pd">Il percorso del PDF, file di testo o file di log del report da caricare.</dd>
<dt class="pt dlterm">&lt;RTF&gt;</dt>
<dd class="pd">Un'opzione per includere una versione RTF (Rich Text Format) del PDF. Questa opzione si applica solo se
hai incluso il percorso del PDF del report. La versione RTF è utilizzata per l'indicizzazione e la ricerca.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **baar** come alias per il nome comando
**bluemix-admin-add-report** più lungo.

* Per eliminare un report, immetti il seguente comando:

`cf bluemix-admin-delete-report <category> <date> <name>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">La categoria per il report. Se nel nome è presente uno spazio, racchiudi il nome
tra virgolette.</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">La data del report in formato <samp class="ph codeph">AAAAMMGG</samp>.</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">Il nome del report.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **badr** come alias per il nome comando
**bluemix-admin-delete-report** più lungo.

* Per recuperare un report, immetti il seguente comando:

`cf bluemix-admin-retrieve-report <category> <date> <name>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">La categoria per il report. Se nel nome è presente uno spazio, racchiudi il nome
tra virgolette.</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">La data del report in formato <samp class="ph codeph">AAAAMMGG</samp>.</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">Il nome del report.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **barr** come alias per il nome comando **bluemix-admin-retrieve-report** più lungo.

### Abilitazione e disabilitazione dei servizi per tutte le organizzazioni

Puoi abilitare o disabilitare la visualizzazione di un servizio nel Catalogo {{site.data.keyword.Bluemix_notm}} per tutte le organizzazioni.

* Per abilitare la visualizzazione di un servizio nel Catalogo {{site.data.keyword.Bluemix_notm}} per tutte le
organizzazioni, immetti il seguente comando:

`cf bluemix-admin-enable-service-plan <plan_identifier>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">Il nome o GUID del servizio da abilitare. Se immetti un nome servizio non univoco,
ti verrà richiesto di scegliere tra dei piani di servizio.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **baesp** come alias per il nome comando
**bluemix-admin-enable-service-plan** più lungo.

* Per disabilitare la visualizzazione di un servizio nel Catalogo {{site.data.keyword.Bluemix_notm}} per tutte le
organizzazioni, immetti il seguente comando:

`cf bluemix-admin-disable-service-plan <plan_identifier>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">Il nome o GUID del servizio da disabilitare. Se immetti un nome servizio non univoco,
ti verrà richiesto di scegliere tra dei piani di servizio.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **badsp** come alias per il nome comando
**bluemix-admin-disable-service-plan** più lungo.

### Aggiunta, rimozione e modifica della visibilità dei servizi per le organizzazioni

Puoi aggiungere o rimuovere un'organizzazione dall'elenco di organizzazioni che possono visualizzare
uno specifico servizio nel Catalogo {{site.data.keyword.Bluemix_notm}}. Puoi anche modificare e sostituire l'elenco dei servizi che le specifiche
organizzazioni possono visualizzare nel Catalogo {{site.data.keyword.Bluemix_notm}}. 

* Per consentire a un'organizzazione di visualizzare uno specifico servizio nel Catalogo {{site.data.keyword.Bluemix_notm}}, immetti il
seguente comando:

`cf bluemix-admin-add-service-plan-visibility <plan_identifier> <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">Il nome o GUID del servizio per il quale vuoi aggiungere la visibilità. Se immetti un nome servizio non univoco,
ti verrà richiesto di scegliere tra dei piani di servizio.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Il nome o GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui aggiungere l'elenco di visibilità del servizio.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **baaspv** come alias per il nome comando
**bluemix-admin-add-service-plan-visibility** più lungo.

* Per rimuovere la visibilità di un servizio nel Catalogo {{site.data.keyword.Bluemix_notm}} per
un'organizzazione, immetti il seguente comando:

`cf bluemix-admin-remove-service-plan-visibility <plan_identifier> <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">Il nome o GUID del servizio per il quale vuoi rimuovere la visibilità. Se immetti un nome servizio non univoco,
ti verrà richiesto di scegliere tra dei piani di servizio.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Il nome o GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} da cui rimuovere l'elenco di visibilità del servizio.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **barspv** come alias per il nome comando
**bluemix-admin-remove-service-plan-visibility** più lungo.

* Per sostituire tutti servizi visibili esistenti per una o più organizzazioni, utilizza il
seguente
comando:

`cf bluemix-admin-edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>`
{: codeblock}

**Nota:** questo
comando sostituisce i servizi visibili esistenti per le organizzazioni specificate con il servizio
indicato nel comando.

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">Il nome o GUID del servizio che desideri rendere visibile. Se immetti un nome servizio non univoco,
ti verrà richiesto di scegliere tra dei piani di servizio.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Il nome o GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} per la quale aggiungere la visibilità. Puoi abilitare la visibilità del servizio per più di
un'organizzazione immettendo ulteriori nomi o GUID di organizzazione nel comando.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **baespv** come alias per il nome comando
**bluemix-admin-edit-service-plan-visibility** più lungo.
