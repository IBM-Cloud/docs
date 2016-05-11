---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestione di {{site.data.keyword.Bluemix_notm}} locale e {{site.data.keyword.Bluemix_notm}} dedicato
{: #mng}
*Ultimo aggiornamento: 19 aprile 2016*

Se disponi dell'accesso come amministratore per {{site.data.keyword.Bluemix_notm}} locale o {{site.data.keyword.Bluemix_notm}} dedicato, vai alla pagina **Amministrazione** per gestire risorse, monitorare l'utilizzo delle quote, amministrare le autorizzazioni utente, pianificare le notifiche di aggiornamento, visualizzare log e report di sicurezza e altro. Puoi gestire le tue organizzazioni creando degli spazi e impostando dei [ruoli e delle autorizzazioni per gli utenti](index.html#oc_useradmin); vedi [Gestione delle tue organizzazioni](../admin/adminpublic.html#orgmng).
{:shortdesc}

*Tabella 1. Attività amministrative per la gestione della tua istanza di {{site.data.keyword.Bluemix_notm}} locale o dedicato*

| Quali operazioni posso eseguire? | Dettagli |    
|----------------|---------|
|Monitorare l'utilizzo del sistema | Fai clic su **AMMINISTRAZIONE &gt; UTILIZZO**. Visualizza le informazioni di sistema, monitora l'utilizzo della CPU e pianifica l'utilizzo per ottimizzare il processo decisionale per la tua azienda. Vedi [Visualizzazione delle informazioni sull'utilizzo](index.html#oc_resource).|
|Gestire il tuo catalogo | Fai clic su **AMMINISTRAZIONE &gt; GESTIONE CATALOGO** per stabilire quali servizi sono visibili ai tuoi utenti e organizzazioni. Vedi [Gestione del tuo catalogo](index.html#oc_catalog).|
|Amministrare le organizzazioni | Fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE ORGANIZZAZIONE** per creare organizzazioni, monitorare le quote per le organizzazioni e prendere decisioni rapide basate sulle esigenze. Vedi [Amministrazione delle organizzazioni](index.html#oc_organizations).|
|Creare spazi e assegnare i ruoli utente | Fai clic sull'icona **Account e supporto** ![Account e supporto](../support/images/account_support.svg), quindi seleziona **Gestisci organizzazioni** per creare spazi nelle tue organizzazioni. Aggiungi utenti e assegna loro dei ruoli per l'organizzazione e lo spazio. Vedi [Gestione delle tue organizzazioni](../admin/adminpublic.html#orgmng). |
|Gestire le autorizzazioni degli utenti amministrativi | Fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE UTENTI** per aggiungere e rimuovere utenti e modifica le autorizzazioni utente. Vedi [Gestione di utenti e autorizzazioni](index.html#oc_useradmin). |
|Esaminare report e log | Fai clic su **AMMINISTRAZIONE &gt; REPORT E LOG** per visualizzare i report di sicurezza e i log di controllo relativi alla tua istanza. Vedi [Visualizzazione dei report](index.html#oc_report). |
|Visualizzare le informazioni di sistema. | Fai clic su **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA** per visualizzare le informazioni di sistema, quali aggiornamenti in sospeso, nome e versione della tua istanza, regione, URL API, URL CLI, dettagli di configurazione LDAP, associazioni di gruppi e utenti, statistiche e domini condivisi. Puoi inoltre accedere al feed calendario e alle sottoscrizioni evento per ampliare le tue notifiche nella sezione Aggiornamenti in sospeso. Vedi [Visualizzazione delle informazioni sul sistema](index.html#oc_system). |
|Estendere le notifiche e impostare le sottoscrizioni evento | Fai clic su **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA &gt; *Numero* aggiornamenti in sospeso**. Puoi utilizzare gli hook Web da integrare con un servizio Web a scelta, per impostare una sottoscrizione di notifica evento per un aggiornamento o incidente. Vedi [Notifiche e sottoscrizioni di eventi](index.html#oc_eventsubscription). |


## Notifiche e sottoscrizioni di eventi
{: #oc_eventsubscription}

Puoi sempre conoscere lo stato del tuo ambiente consultando la pagina Stato. {{site.data.keyword.Bluemix_notm}} invia inoltre all'area Notifiche le eventuali notifiche riguardanti la pagina Amministrazione in relazione a eventi quali aggiornamenti e manutenzione pianificati. Gli incidenti vengono segnalati nella pagina Stato.

### Notifiche

Puoi visualizzare le notifiche inviate da IBM per il tuo ambiente locale o dedicato e monitorare lo stato del tuo ambiente. Consulta la seguente tabella per informazioni sui diversi tipi di notifiche e sui punti in cui vengono pubblicate.

Tabella 2. Tipi di evento e metodi di notifica

| **Tipo di evento** | **Metodo di notifica** |       
|-----------------|-------------------|
| Aggiornamenti di manutenzione | Vieni avvisato dei prossimi aggiornamenti di manutenzione nella pagina Notifiche per l'amministrazione. Vai alla pagina **Amministrazione**, quindi seleziona l'icona **Notifiche** ![Notifiche](images/icon_announcement.svg). Per visualizzare un storico e un elenco completo delle tue notifiche complete e in sospeso, fai clic su **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA** &gt; *Numero* **aggiornamenti in sospeso**. Puoi estendere la funzionalità di notifica impostando una sottoscrizione evento che integri gli avvisi di aggiornamento di manutenzione provenienti dalla pagina Amministrazione con un servizio Web a scelta che instradi i messaggi a un indirizzo e-mail di help desk o che invii un messaggio SMS a un numero telefonico prescelto. |
| Incidenti critici | Vieni avvisato degli incidenti critici sulla pagina Stato. Fai clic sull'icona **Account e supporto** ![Account e supporto](../support/images/account_support.svg), quindi seleziona **Stato**. Puoi estendere la funzionalità di notifica impostando una sottoscrizione evento che integri gli avvisi di incidente provenienti dalla pagina Stato con un servizio Web a scelta che instradi i messaggi a un indirizzo e-mail di help desk o che invii un messaggio SMS a un numero telefonico prescelto. |  
| Stato | Puoi visualizzare l'ultimo stato della piattaforma, dei servizi e della tua istanza {{site.data.keyword.Bluemix_notm}}. Fai clic sull'icona **Account e supporto** ![Account e supporto](../support/images/account_support.svg), quindi seleziona **Stato**.  |

### Impostazione di sottoscrizioni evento

Puoi estendere la funzionalità delle notifiche inviate alle pagine Amministrazione e Stato, utilizzando le sottoscrizioni evento che implementano hook Web. Gli hook Web instradano le tue notifiche direttamente a una destinazione a scelta, ad esempio un indirizzo e-mail help desk (tramite e-mail) o un numero di telefono (tramite messaggio SMS). Puoi personalizzare il tipo di notifica, in particolare gli aggiornamenti di manutenzione o gli avvisi di incidente critico, e le informazioni incluse nella notifica.

Per utilizzare gli hook Web per l'impostazione di una sottoscrizione evento specifica, completa la seguente procedura:

* Per le notifiche di aggiornamento di manutenzione, vai a **INFORMAZIONI DI SISTEMA** &gt; *Numero* **aggiornamenti in sospeso**, quindi fai clic sull'icona **Sottoscrivi** ![Sottoscrivi](images/icon_subscribe.svg).
* Per le notifiche di avviso di incidente, fai clic sull'icona **Account e supporto** ![Account e supporto](../support/images/account_support.svg) &gt; **Stato**, quindi fai clic sull'icona **Sottoscrivi** ![Sottoscrivi](images/icon_subscribe.svg).

**Nota**: puoi accedere alla pagina di sottoscrizione evento per entrambi i tipi di notifica, utilizzando uno qualsiasi dei due metodi descritti.

1. Fai clic su **Aggiungi sottoscrizione**.

2. Compila il modulo di sottoscrizione evento. Per informazioni sui campi del modulo, consulta la seguente tabella:

*Tabella 3. Campi del modulo di sottoscrizione evento*

| **Campo** | **Descrizione** |
|-----------------|-------------------|
| Tipo | Seleziona l'hook Web. |
| Metodo | Seleziona GET o POST. |
| Evento | Selezionalo per sottoscrivere le notifiche di aggiornamenti o incidenti. |
| URL | Immetti l'URL per agganciarti al tuo servizio Web. |
| Descrizione | Aggiungi una descrizione della sottoscrizione evento che stai creando. |
| Nome utente | Immetti il tuo nome utente per il tuo servizio Web. Se non desideri utilizzare le tue credenziali personali, puoi impostare un ID funzionale da utilizzare specificatamente con {{site.data.keyword.Bluemix_notm}}. |
| Password | Immetti la password per il tuo servizio Web. |
| Payload | Se hai selezionato il metodo POST, immetti le proprietà specifiche del servizio Web che stai utilizzando insieme i valori utilizzati per la notifica IBM. Ad esempio, se desideri che la notifica proveniente dal servizio Web riporti il titolo, il messaggio e il grado di severità, devi definire i valori {{site.data.keyword.Bluemix_notm}} con la proprietà corrispondente per il tuo servizio Web. I seguenti valori possono essere utilizzati per estrarre informazioni dalla notifica {{site.data.keyword.Bluemix_notm}} in relazione a livello di severità, corpo del messaggio e titolo della notifica: `"{{title}}`, `"{{message}},"` e `"{{severity}}"`. Se non immetti informazioni in questa sezione, ricevi la notifica priva di informazioni supplementari.  |

Quando salvi la tua sottoscrizione evento, ricevi notifiche attraverso il metodo che hai impostato attraverso il tuo servizio Web. Le notifiche vengono ancora pubblicate nella pagina Stato per quanto riguarda gli incidenti e nell'area Notifiche della pagina Amministrazione per quanto riguarda gli aggiornamenti di manutenzione.

Puoi selezionare qualsiasi sottoscrizione evento salvata e visualizzare l'attività recente. Puoi fare clic per espandere qualsiasi voce delle attività recenti per visualizzare i dettagli. I dettagli includono i valori IBM per la notifica utilizzabili nella sezione payload. Per visualizzare questi valori, espandi la voce dell'attività recente, l'**Evento** e infine l'**Oggetto**.


## Visualizzazione delle informazioni sul sistema
{: #oc_system}

Per visualizzare le informazioni sul sistema, fai clic su **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA**.

Puoi espandere e visualizzare diverse sezioni relative ad aggiornamenti in sospeso, informazioni generali sul sistema e dettagli della configurazione LDAP.

### Notifiche e aggiornamenti in sospeso

Nella sezione Aggiornamenti, puoi visualizzare il numero di notifiche di
aggiornamenti in sospeso che richiedono un tuo intervento. Per intervenire per uno specifico aggiornamento, completa questa procedura:

<ol>
<li>Fai clic su <strong><em>Numero</em> aggiornamenti in sospeso</strong> per visualizzare tutti
gli aggiornamenti in sospeso.</li>
<li>Seleziona un aggiornamento per intervenire o per visualizzare i relativi dettagli, che
includono la finestra di aggiornamento, la data pianificata e lo stato di interruzione del servizio.</li>
<li>Fai clic su <strong>SELEZIONA DATE NON DISPONIBILI</strong> per impostare degli specifici giorni nella finestra
di aggiornamenti che non siano opportuni per l'applicazione dell'aggiornamento. Se imposti delle date non disponibili, IBM approva
e pianifica il tuo aggiornamento in base alle tue selezioni. Ricevi una notifica quando l'aggiornamento viene approvato e pianificato.</li>
<li>Fai clic su <strong>APPROVA AGGIORNAMENTO</strong> per approvare l'aggiornamento, se non hai alcuna data non disponibile. Se approvi, l'aggiornamento viene applicato durante la finestra di aggiornamento pianificata. IBM invia una notifica quando la distribuzione dell'aggiornamento inizia e finisce.</li>
</ol>

**Nota**: se non imposti le date non disponibili o non approvi l'aggiornamento, quest'ultimo viene applicato alla fine della finestra temporale di 21 giorni per assicurare che la tua piattaforma resti attuale e aggiornata.

Dalla pagina Aggiornamenti in sospeso, puoi scegliere di tracciare la pianificazione dei tuoi aggiornamenti facendo clic sull'icona **Calendario** ![Calendario](images/icon_calendar.svg) e scaricando il file `.ics` per importare i tuoi aggiornamenti pianificati in un'applicazione calendario a scelta:

<ol>
<li>Apri la tua applicazione calendario.</li>
<li>Scarica il file calendario facendo clic sull'icona **Calendario** ![Calendario](images/icon_calendar.svg), quindi importalo nella tua applicazione calendario attraverso il file `.ics`.</li>
<li>Immetti le tue credenziali.</li>
<li>Visualizza i tuoi aggiornamenti pianificati.</li>
</ol>

Puoi anche estendere la funzionalità di notifica per la pagina Amministrazione utilizzando delle sottoscrizioni evento da integrare con un servizio Web a scelta. Per impostare una sottoscrizione di notifica evento per un aggiornamento o un incidente, vedi [Notifiche e sottoscrizioni evento](index.html#oc_eventsubscription).

### Informazioni generali sul sistema

Nella sezione di informazioni generali, puoi visualizzare le seguenti informazioni:

- Le informazioni di base sulla build {{site.data.keyword.Bluemix_notm}}.
- Le informazioni sull'API, compresi versione, URL, regione e un link alla documentazione della CLI.
- Le informazioni sul dominio condiviso relative al tuo sistema e al tuo servizio.
- Le statistiche sul numero totale di applicazioni, utenti e organizzazioni.

### Dettagli configurazione LDAP

Nella sezione Dettagli di configurazione LDAP, puoi selezionare il server LDAP
e visualizzare le informazioni relative alle associazioni di utenti e gruppi. Se stai utilizzando un WebID {{site.data.keyword.IBM}}, questo viene indicato in questa sezione.

## Visualizzazione delle informazioni sull'utilizzo
{: #oc_resource}

Puoi visualizzare differenti tipi di informazioni sull'utilizzo della tua istanza locale o dedicata e sull'account {{site.data.keyword.Bluemix_notm}}:

- Informazioni sulle risorse, quali spazio su disco, utilizzo della CPU, utilizzo della rete e tempi medi di risposta. Vedi [Utilizzo risorsa](index.html#resourceusage).
- Utilizzo dell'account per organizzazione, incluso il numero di applicazioni di runtime con utilizzo, numero totale di GB-ore di runtime e numero di istanze di servizio con relativo utilizzo. Vedi [Utilizzo dell'account](index.html#accountusage).
- Utilizzo di quote di memoria, memoria dell'applicazione assegnata in base alla percentuale totale di memoria utilizzata e una vista sull'utilizzo di GB-ore per applicazione in relazione a un'organizzazione specifica. Puoi anche visualizzare l'utilizzo delle quote di memoria per tutte le organizzazioni sulla pagina Amministrazione organizzazione nella sezione Monitoraggio quota. Vedi [Amministrazione organizzazione](../admin/index.html#orgusage).


### Utilizzo delle risorse
{: #resourceusage}

Per visualizzare le informazioni sulle risorse, fai clic su **AMMINISTRAZIONE &gt; UTILIZZO**.

Nella sezione di monitoraggio delle risorse, puoi visualizzare le seguenti informazioni:

- Informazioni sull'utilizzo delle risorse, ad esempio la quantità di GB di memoria e di GB di spazio su disco
utilizzata. Puoi visualizzare l'utilizzo della CPU calcolato come media su tutti i DEA (droplet execution agent). Fai clic
sul tile **CPU**, per potere così visualizzare l'utilizzo della CPU per ogni DEA. Il DEA con
l'utilizzo più elevato è elencato per primo; ognuno di essi è identificato dal relativo lavoro e indirizzo IP. L'utilizzo
della CPU è separato in tre categorie che includono la quantità di CPU impiegata nei processi di sistema, quella
impiegata nei processi utente e quella impiegata nei processi in attesa.
- Informazioni sull'utilizzo della rete per la larghezza di banda in entrata e in uscita, nel corso del giorno, settimana o
mese precedente.
I dati visualizzati sono basati sulla somma del traffico in entrata e in uscita per la rete pubblica e quella privata.
- Il tempo di risposta medio per {{site.data.keyword.Bluemix_notm}} nel corso degli ultimi 10 minuti, dell'ultima ora e dell'ultimo giorno.
- Le transazioni medie al secondo per {{site.data.keyword.Bluemix_notm}} nel corso degli ultimi 10 minuti, dell'ultima ora e dell'ultimo giorno.

### Utilizzo dell'account
{: #accountusage}

Puoi visualizzare l'utilizzo mensile del tuo account per il tuo ambiente locale o dedicato. Puoi utilizzare questi dati per sapere quanto addebitare a determinate organizzazioni in base all'uso effettuato.

<ol>
<li>Fai clic sull'icona <strong>Account e supporto</strong> ![Account e supporto](../support/images/account_support.svg) &gt; <strong>Account</strong> &gt; <strong>Dettagli di utilizzo</strong>.</li>
<li>Seleziona l'organizzazione per cui desideri visualizzare i dati.</li>
<li>Puoi vedere i dettagli di utilizzo per le seguenti categorie:
<ul>
<li>Applicazioni di runtime con utilizzo</li>
<li>Utilizzo totale delle applicazioni di runtime in GB-ore</li>
<li>Istanze di servizio con utilizzo</li>
</ul>
</li>
<li>Facoltativo: visualizza i tuoi dati per un mese specifico, utilizzando il menu <strong>La tua attività cloud</strong> per selezionare un mese a scelta.</li>
<li>Facoltativo: fai clic su <strong>ESPORTA DATI</strong> e scegli tra <strong>CSV</strong> o <strong>JSON</strong> per esportare i dati per il mese selezionato in un file <code>CSV</code> o <code>JSON</code>.</li>
</ol>

Puoi anche visualizzare l'utilizzo mensile e gli addebiti associati a livello di account per i tuoi runtime, applicazioni e servizi diffusi da {{site.data.keyword.Bluemix_notm}} pubblico. Puoi utilizzare questi dati per sapere quanto addebitare a determinate organizzazioni in base all'uso effettuato.

<ol>
<li>Fai clic sull'icona <strong>Account e supporto</strong> ![Account e supporto](../support/images/account_support.svg) &gt; <strong>Account</strong> &gt; <strong>Dettagli di utilizzo</strong>.</li>
<li>Fai clic su <strong>Pubblico</strong>.</li>
<li>Seleziona l'organizzazione per cui desideri visualizzare i dati o <strong>Tutte le organizzazioni</strong> per visualizzare in una volta sola i dati di tutte le organizzazioni.</li>
<li>Puoi vedere i dettagli di utilizzo per le seguenti categorie:
<ul>
<li>Applicazioni di runtime con utilizzo</li>
<li>Utilizzo totale delle applicazioni di runtime in GB-ore</li>
<li>Istanze di servizio con utilizzo</li>
<li>Riepilogo degli addebiti per tutte le applicazioni, i servizi e i runtime diffusi</li>
</ul>
</li>
<li>Facoltativo: visualizza i tuoi dati per un mese specifico, selezionando un mese a scelta dal grafico a barre. Per impostazione standard vengono visualizzati i dati del mese corrente.</li>
<li>Facoltativo: fai clic su <strong>ESPORTA DATI</strong> e scegli tra <strong>CSV</strong> o <strong>JSON</strong> per esportare i dati per il mese selezionato in un file <code>CSV</code> o <code>JSON</code>.</li>
</ol>


### Utilizzo delle organizzazioni
{: #orgusage}

Per visualizzare l'utilizzo per organizzazione, fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE ORGANIZZAZIONE**, quindi seleziona un'organizzazione dall'**Elenco delle organizzazioni**. Nella pagina **Gestisci organizzazioni** dell'organizzazione selezionata, puoi visualizzare le seguenti informazioni sull'utilizzo:

- Numero di servizi attualmente in uso.
- Numero di rotte attualmente in uso.
- Grafico delle quote di memoria che mostra le percentuali di quota di memoria attualmente in uso e non in uso.
- Grafico sull'assegnazione delle applicazioni che mostra quali applicazioni sono incluse nella quota di memoria utilizzata.
- Grafico sull'utilizzo misurato dell'applicazione che mostra un report trimestrale sulle GB-ore utilizzate per applicazione distribuita. Puoi selezionare la **Vista elenco** per visualizzare i dati per tutte le applicazioni, compresa l'assegnazione di memoria per applicazione e l'utilizzo a consumo di GB-ore degli ultimi tre mesi.

Per ulteriori informazioni sulla visualizzazione dell'utilizzo per organizzazione, sull'adeguamento dei piani di quota e sulla gestione delle tue organizzazioni, vedi [Amministrazione delle organizzazioni](../admin/index.html#oc_organizations).

## Visualizzazione dei report
{: #oc_report}

Puoi visualizzare i report e i log di sicurezza, quali DataPower&trade;, firewall e controllo accessi, per la tua istanza {{site.data.keyword.Bluemix_notm}}.

Per visualizzare report e log, fai clic su **AMMINISTRAZIONE &gt; REPORT E LOG**.

Seleziona dalle seguenti opzioni:

- Puoi selezionare le date di inizio e di fine dai campi per filtrare i report e i log da
visualizzare.
- Puoi espandere e visualizzare i diversi report dal riquadro di navigazione.
- Puoi effettuare ricerche nella tua raccolta di report e log. La ricerca si applica ai nomi di report e al contenuto testuale
all'interno di report e log. Puoi anche scegliere di filtrare la ricerca in base
agli **Eventi di amministrazione**, ai **Report DataPower**, al **Firewall** e al **Controllo accessi**.
- Durante la visualizzazione di un report o log, puoi fare clic sull'icona ![Download](images/icon_download.png)
per scaricare il report.

La seguente tabella mostra l'elenco dei report di sicurezza generati per {{site.data.keyword.Bluemix_notm}} locale e {{site.data.keyword.Bluemix_notm}} dedicato.

*Tabella 4. Elenco dei report di sicurezza*

| **Categoria** | **Report** | **Descrizione** |      
|-----------------|-------------------|---------------------|
| Firewall | Accessi firewall | Eventi relativi all'accesso dell'amministratore ai dispositivi firewall Vyatta. |
| Firewall | Accessi firewall negati | Eventi generati da dispositivi firewall Vyatta quando una richiesta di accesso viene negata in base alle regole firewall in vigore. |
| Eventi di accesso dell'amministratore {{site.data.keyword.Bluemix_notm}} | Accesso amministratori {{site.data.keyword.Bluemix_notm}} | Eventi generati dal sistema operativo quando un amministratore avvia una sessione SSH su ogni sistema {{site.data.keyword.Bluemix_notm}}. |
| Eventi di accesso dello sviluppatore di applicazioni {{site.data.keyword.Bluemix_notm}} | Accesso sviluppatori di applicazioni {{site.data.keyword.Bluemix_notm}} | Eventi generati dal componente di accesso della piattaforma {{site.data.keyword.Bluemix_notm}} quando un utente di {{site.data.keyword.Bluemix_notm}} avvia una sessione utilizzando la riga comandi, le API REST o l'interfaccia utente {{site.data.keyword.Bluemix_notm}}. |
| Eventi amministrativi dell'amministratore {{site.data.keyword.Bluemix_notm}} | Eventi amministrativi di sistema operativo degli amministratori {{site.data.keyword.Bluemix_notm}} | Eventi generati dal sistema operativo quando un amministratore svolge un'azione all'interno di una sessione di lavoro corrente. |
| Eventi amministrativi dello sviluppatore di applicazioni {{site.data.keyword.Bluemix_notm}} | Eventi amministrativi {{site.data.keyword.Bluemix_notm}} (Cloud Foundry) | Eventi relativi alle operazioni effettuate dall'utente della piattaforma {{site.data.keyword.Bluemix_notm}} utilizzando la riga comandi, le API REST o l'interfaccia utente {{site.data.keyword.Bluemix_notm}}. |
| Eventi amministrativi di database dell'amministratore {{site.data.keyword.Bluemix_notm}} | Eventi amministrativi di database | Eventi relativi alle operazioni effettuate da un amministratore di database nei database interni {{site.data.keyword.Bluemix_notm}}. |
| Eventi di amministrazione | Eventi di gestione utente | Eventi relativi alle azioni di gestione utente eseguite nella pagina Amministrazione. |
| Eventi di amministrazione | Catalogo | Eventi relativi alle modifiche del catalogo dei servizi. |
| Eventi di amministrazione | Eventi di gestione dei report di sicurezza | Eventi relativi alle azioni di gestione dei report di sicurezza eseguite nella pagina Amministrazione. |
| Revisioni accesso | Report di revisioni accesso | Revisioni per accessi privilegiati. |
| Gestione modifiche | Gestione delle modifiche del software | Attività di gestione delle modifiche. |
| Gestione chiavi | Gestione dei certificati SSL personalizzati | Certificazioni SSL personalizzate che sono state caricate e archiviate. |
| Crittografia | Crittografia dei data-in-transit | Crittografia configurata per i data-in-transit. |
| Antivirus | Report di scansione antivirus | Software antivirus in uso. |
| Gestione delle correzioni software | Report di applicazione patch | Correzioni software applicate. |
| Gestione degli incidenti di sicurezza | Report di correzione incidenti di sicurezza | Prove di incidenti di sicurezza per consentirne la gestione. |

## Visualizzazione dello stato
{: #oc_status}

Puoi monitorare lo stato per la tua istanza {{site.data.keyword.Bluemix_notm}} utilizzando la pagina Stato di {{site.data.keyword.Bluemix_notm}}. Fai clic sull'icona **Account e supporto** ![Account e supporto](../support/images/account_support.svg), quindi seleziona **Stato**.

La pagina Stato è la posizione centrale per trovare notifiche e annunci sugli eventi chiave che interessano la piattaforma {{site.data.keyword.Bluemix_notm}} e i servizi principali in {{site.data.keyword.Bluemix_notm}}.

Puoi sottoscrivere a un feed RSS per le notifiche in modo da non doverle controllare personalmente. Per ulteriori informazioni sulla pagina Stato e sulla configurazione del feed RSS, vedi [Visualizzazione di {{site.data.keyword.Bluemix_notm}}](../support/index.html#viewing-bluemix-status).

## Gestione del tuo catalogo
{: #oc_catalog}

Puoi gestire quali servizi e starter {{site.data.keyword.Bluemix_notm}} sono visibili agli utenti nel Catalogo {{site.data.keyword.Bluemix_notm}}. Fai clic su **AMMINISTRAZIONE &gt; GESTIONE CATALOGO**.

Seleziona un tile di servizio o di starter per modificare la visibilità del piano di servizio o starter. Per modificare la
visibilità, seleziona dalle seguenti opzioni:

- Per visualizzare il servizio o lo starter nascosto in modo che sia visibile ai tuoi utenti nel Catalogo,
seleziona **ABILITA TUTTI I PIANI**.
- Per nascondere il servizio o lo starter ai tuoi utenti nel Catalogo {{site.data.keyword.Bluemix_notm}},
seleziona **DISABILITA TUTTI I PIANI**.
- Per controllare la visibilità di un singolo piano, seleziona il nome del piano e utilizza quindi
il menu a discesa per selezionare **Abilita per tutte le organizzazioni**, **Disabilita per
tutte le organizzazioni** o **Abilita piano per specifiche organizzazioni**.

<!-- staging only start -->

### Registrazione di un broker dei servizi
{: #servicebrokerui}

Se vuoi visualizzare un determinato servizio nel tuo catalogo {{site.data.keyword.Bluemix_notm}}, devi implementare e registrare un broker dei servizi. Una volta registrato il tuo broker, puoi scegliere quali organizzazioni possono accedere al servizio nella tua istanza locale o dedicata.

Le modalità d'uso del tuo broker dei servizi variano a seconda del numero di servizi che gestisce o dalla sua eventuale precedente registrazione in {{site.data.keyword.Bluemix_notm}}.

- Se il tuo broker dei servizi gestisce un unico servizio, puoi utilizzare l'interfaccia utente per registrarlo al termine dell'implementazione dell'[API broker dei servizi](http://docs.cloudfoundry.org/services/api.html){: new_window}. Vedi [Registrazione di un broker dei servizi che gestisce un unico servizio](index.html#registerbrokerui).
- Se il tuo broker dei servizi gestisce più servizi, al momento non puoi registrarlo al termine dell'implementazione dell'API broker dei servizi. Utilizza invece la CLI cf con il plug-in [{{site.data.keyword.Bluemix_notm}} Admin CLI](../cli/plugins/bluemix_admin/index.html) (sottocomando `ba`) o l'[API del servizio personalizzato](index.html#servicebrokerapi).
- Se il tuo broker dei servizi è già registrato e desideri aggiornarlo o eliminarlo, utilizza la CLI cf con il plug-in [{{site.data.keyword.Bluemix_notm}} Admin CLI](../cli/plugins/bluemix_admin/index.html) (sottocomando `ba`) o l'[API del servizio personalizzato](index.html#servicebrokerapi).

#### Registrazione di un broker dei servizi che gestisce un unico servizio
{: #registerbrokerui}

Completa la seguente procedura per registrare il tuo broker dei servizi:

<ol>
<li><a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">Implementa l'API broker dei servizi Cloud Foundry</a> per consentire la comunicazione tra il tuo servizio e {{site.data.keyword.Bluemix_notm}}. L'API broker dei servizi è un insieme di endpoint REST utilizzati da {{site.data.keyword.Bluemix_notm}}.<br />
<br />
<p>Quando implementi il broker dei servizi, nella risposta JSON di <code>GET /v2/catalog</code> devi fornire le definizioni per i tuoi piani di servizio e servizi, incluse le informazioni sul servizio che desideri visualizzare. Ad esempio, consulta il seguente file JSON di esempio della risposta del catalogo (GET)</p>
<p><pre>
"services":[
   {
      "bindable":true,
      "description":"Cool Service è una soluzione di immagazzinamento e di analisi dei dati.",
      "id":"cool-service-id",
      "name":"coolservice",
      "tags":[
         "customer_dedicated"
      ],
      "metadata":{
         "displayName":"Cool Service",
         "serviceMonitorApi":"https://myservicesstatus.mybluemix.net/healthcheck/",
         "providerDisplayName":"Cool company",
         "longDescription":"Cool Service è una soluzione di immagazzinamento e di analisi dei dati. Puoi spostare rapidamente i tuoi dati in un database in-memoria a colonne di prossima generazione e iniziare ad eseguire query analitiche complesse.",
         "bullets":[
            {
               "title":"Rapida e semplice",
               "description":"Cool Service utilizza innovazioni e tecnologia a colonne in memoria dinamiche, come l'elaborazione vettoriale parallela e una compressione su cui è possibile intervenire per eseguire rapidamente la scansione dei dati pertinenti ed eseguirne la restituzione."
            },
            {
               "title":"Connettività",
               "description":"Cool Service è progettato per consentirti di connetterti facilmente a tutti i servizi e a tutte le applicazioni. Puoi iniziare immediatamente ad analizzare i tuoi dati con strumenti familiari."
            }
         ],
         "featuredImageUrl":"http://path/to/icon_64x64.png",
         "imageUrl":"http://path/to/icon_50x50.png",
         "mediumImageUrl":"http://path/to/icon_32x32.png",
         "smallImageUrl":"http://path/to/icon_24x24.png",
         "documentationUrl":"http://path/to/documentation.html",
         "instructionsUrl":"http://path/to/servicesample.md",
         "termsUrl":"http://path/to/terms_of_agreement.pdf",
         "media":[
            {
               "type":"youtube",
               "thumbnailUrl":"http://path/to/thumbnail.png",
               "url":"http://path/to/youtube/video",
               "caption":"Come usare Cool Service in 60 secondi"
            },
            {
               "type":"image",
               "thumbnailUrl":"http://path/to/thumbnail.png",
               "url":"http://path/to/image_file.png",
               "caption":"Connessione di applicazioni con Cool Service"
            },
            {
               "type":"video",
               "thumbnailUrl":"http://path/to/thumb.png",
               "caption":"Utilizzo delle tabelle da parte di Cool Service",
               "source":[
                  {
                     "type":"video/mp4",
                     "url":"http://path/to/video_file.mp4"
                  },
                  {
                     "type":"video/ogg",
                     "url":"http://path/to/video_file.ogg"
                  }
               ]
            }
         ]
      },
      "plans":[
         {
            "name":"smallplan",
            "description":"Spazio tabelle e schema dedicati per istanza di servizio su un server condiviso. L'archiviazione dei database compressi da 1 e 10 GB può contenere fino a, rispettivamente, 5 e 50 GB di dati non compressi, con rapporti di compressione standard.",
            "free":false,
            "id":"cool-service-plan-id",
            "metadata":{
               "bullets":[
                  "Minimo 1 GB per istanza. Massimo 10 GB per istanza."
               ],
               "costs":[
                  {
                     "unitId":"INSTANCES_PER_MONTH",
                     "unit":"MONTHLY",
                     "partNumber":"D15UTLL"
                  }
               ],
               "displayName":"Small"
            }
         }
      ]
   }
]
}
</pre></p>
<p><strong>Nota</strong>: quando crei un broker dei servizi per un ambiente locale o dedicato, devi specificare `customer_dedicated` nel campo "tags" del tuo file JSON di definizione dei servizi.</p>
</li>
<li>Una volta implementata l'API broker dei servizi, vai a <strong>AMMINISTRAZIONE</strong> &gt; <strong>GESTIONE CATALOGO</strong>.</li>
<li>Fai clic su <strong>REGISTRA UN BROKER DEI SERVIZI</strong>.</li>
<li>Completa il modulo immettendo valori nei seguenti campi:
<ul>
<li>Nome del broker dei servizi</li>
<li>URL del broker dei servizi</li>
<li>Nome utente del broker dei servizi</li>
<li>Password del broker dei servizi</li>
</ul>
</li>
<li>Fai clic su <strong>CONNETTI</strong>.</li>
<li>Controlla le informazioni sul tuo servizio, inclusi i piani disponibili, l'icona e la descrizione del servizio.<br />
<p><strong>Nota</strong>: se devi modificare le informazioni di catalogo del servizio, aggiorna il tuo broker di servizi e riavvia il processo di registrazione, compilando il modulo.</p>
</li>
<li>Fai clic su <strong>REGISTRA</strong>.</li>
<li>Scegli di abilitare tutti i piani o solo piani specifici per il servizio. Tutti i piani sono disabilitati per impostazione predefinita.</li>
<li>Abilita l'istanza del servizio per tutte le organizzazioni o solo per organizzazioni specifiche.</li>
</ol>

Ora puoi vedere il tuo servizio nella categoria Servizi personalizzati del tuo catalogo {{site.data.keyword.Bluemix_notm}}. Vai a **AMMINISTRAZIONE &gt; GESTIONE CATALOGO** e seleziona il tile del catalogo. Puoi abilitare differenti piani e modificarne la visibilità per le tue organizzazioni in qualsiasi momento.

## Amministrazione delle organizzazioni
{: #oc_organizations}

Puoi gestire le tue organizzazioni attraverso la creazione e l'eliminazione di organizzazioni, l'aggiunta o la rimozione di gestori alle/dalle organizzazioni e il monitoraggio dell'utilizzo delle quote, così da adottare le scelte migliori per la tua attività.

Fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE ORGANIZZAZIONE**.

Puoi espandere e visualizzare le diverse sezioni. Puoi anche riesaminare e gestire i piani di quota per le tue organizzazioni.

### Creazione di organizzazioni

Per creare una nuova organizzazione e aggiungere gestori, completa la seguente procedura:

1. Fai clic su <strong>CREA ORGANIZZAZIONE</strong>.
2. Immetti un nome per l'organizzazione.
3. Immetti il nome o l'email della persona che vuoi aggiungere come gestore. Puoi aggiungere più di un gestore immettendo e selezionando più nomi.
4. Fai clic su <strong>CREA ORGANIZZAZIONE</strong> per salvare le tue modifiche e creare l'organizzazione.

### Monitoraggio quota

Nella sezione Monitoraggio quota, puoi espandere la sezione e visualizzare le seguenti informazioni:

- Utilizzo della memoria dell'ambiente. Questa sezione mostra in dettaglio l'utilizzo della memoria per l'intero ambiente di sistema.
	Il grafico fornisce informazioni che includono la memoria di sistema utilizzata, la memoria totale di sistema, la quota utilizzata e la quota totale assegnata. Il seguente elenco di termini definisce i tipi di utilizzo di memoria visualizzati nel grafico.

	<dl>
	<dt><strong>Memoria di sistema utilizzata</strong></dt>
	<dd>La memoria fisica utilizzata dal tuo ambiente.</dd>
	<dt><strong>Memoria totale di sistema</strong></dt>
	<dd>La memoria fisica totale disponibile nel tuo ambiente.</dd>
	<dt><strong>Quota distribuita</strong></dt>
	<dd>La somma di memoria assegnata per tutte le applicazioni distribuite, su tutte le organizzazioni. La somma
	della quota distribuita può superare la memoria totale di sistema fisica per il tuo ambiente. Ad esempio,
se disponi di una memoria totale di sistema pari a 16 GB e assegni 4 GB di memoria ciascuna per un totale di cinque diverse organizzazioni, la quota totale supera la
memoria di sistema totale che ti è stata assegnata per tutte le organizzazioni. Tuttavia, in molti casi,
è possibile che le organizzazioni non utilizzino la quota totale assegnata singolarmente a ciascuna di esse. Inoltre, è possibile che le organizzazioni non utilizzino contemporaneamente
la propria assegnazione di quota totale della memoria. </dd>
	<dt><strong>Quota totale</strong></dt>
	<dd>La memoria totale assegnata su tutte le organizzazioni.</dd>
	</dl>

- Utilizzo della memoria dell'organizzazione. Questa sezione mostra in dettaglio l'utilizzo della memoria a livello di organizzazione. Puoi visualizzare
la quota totale consentita e la quota che viene distribuita per ogni organizzazione. Il grafico fornisce informazioni che vengono elencate
in base all'utilizzo massimo della memoria per ogni organizzazione e, per impostazione predefinita, viene elencata per prima l'organizzazione che utilizza la maggiore quantità di memoria. Puoi ordinare per **Utilizzo massimo memoria** e **Assegnazione memoria in eccesso**.

	<dl>
	<dt><strong>Utilizzo massimo memoria</strong></dt>
	<dd>Usa questa opzione per identificare l'organizzazione che utilizza la maggior quantità di memoria. Ordina per Utilizzo
	massimo memoria per identificare le organizzazioni che stanno utilizzando la maggiore quantità di
memoria. L'elenco viene ordinato in base alla quota distribuita. </dd>
	<dt><strong>Assegnazione memoria in eccesso</strong></dt>
	<dd>Usa questa opzione per identificare le organizzazioni che hanno un piano di quota superiore a quello necessario.
	Ordina per Assegnazione memoria in eccesso per identificare le organizzazioni che utilizzano
la minore quantità di memoria per la quota assegnata per l'organizzazione. </dd>
	</dl>

### Regolazione dei piani di quota

Per modificare il piano di quota di un'organizzazione, completa la seguente procedura:

<ol>
<li>Fai clic sulla barra del grafico
relativo all'organizzazione che vuoi modificare nella sezione Utilizzo della memoria dell'organizzazione o seleziona il nome
dell'organizzazione nella sezione Elenco organizzazioni.</li>
<li>Nella pagina Gestisci organizzazione, puoi cambiare il piano di quota, modificare il nome dell'organizzazione e aggiungere o
rimuovere gestori.<br />
<p><strong>Nota</strong>: se selezioni un piano di quota che non è sufficiente per l'utilizzo corrente
dell'organizzazione, riceverai un messaggio.</p>
</li>
<li>Per salvare le eventuali modifiche apportate nella pagina Gestisci organizzazione, fai clic su <strong>SALVA</strong>.</li>
</ol>

### Gestione delle tue organizzazioni dall'elenco delle organizzazioni

Nella sezione Elenco organizzazioni, puoi visualizzare tutte le organizzazioni
dell'ambiente {{site.data.keyword.Bluemix_notm}} e intervenire sulle singole organizzazioni facendo clic sul nome dell'organizzazione.

- Per eliminare l'organizzazione, fai clic sull'icona **Elimina** ![Elimina](images/icon_trash.svg) nella colonna Azioni.
- Per visualizzare il piano di quota e l'utilizzo di un'organizzazione, fai clic sul nome dell'organizzazione
nell'elenco. Nella pagina **Gestisci organizzazioni** dell'organizzazione selezionata, puoi visualizzare le seguenti informazioni sull'utilizzo:

  - Numero di servizi attualmente in uso.
  - Numero di rotte attualmente in uso.
  - Grafico delle quote di memoria che mostra le percentuali di quota di memoria attualmente in uso e non in uso.
  - Grafico sull'assegnazione delle applicazioni che mostra quali applicazioni sono incluse nella quota di memoria utilizzata.
  - Grafico sull'utilizzo misurato dell'applicazione che mostra un report trimestrale sulle GB-ore utilizzate per applicazione distribuita. Puoi selezionare la **Vista elenco** per visualizzare i dati per tutte le applicazioni, compresa l'assegnazione di memoria per applicazione e l'utilizzo a consumo di GB-ore degli ultimi tre mesi.

- Per modificare il nome dell'organizzazione e aggiungere o rimuovere gestori, fai clic sul nome dell'organizzazione
 nell'elenco e segui i prompt mostrati a schermo.

## Gestione di utenti e autorizzazioni
{: #oc_useradmin}

Puoi aggiungere degli utenti alla tua istanza {{site.data.keyword.Bluemix_notm}} dal registro utenti della tua azienda tramite LDAP. Puoi aggiungere gli utenti singolarmente
o in gruppi e visualizzarne le autorizzazioni. Se disponi dell'autorizzazione `ammin`,
puoi anche impostare e gestire le autorizzazioni per gli altri utenti. Fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE UTENTI**.

La pagina Amministrazione utenti visualizza tutti gli utenti per l'istanza locale o dedicata.
Sono visualizzate le autorizzazioni per ciascun utente. Le autorizzazioni possono essere: Nessuna,
`Ammin`, `Catalogo`, `Accesso`,
`Report` e `Utenti`. È possibile abilitare le autorizzazioni oppure
fornire agli utenti l'accesso in `visualizzazione` o `scrittura` per
l'autorizzazione indicata, come indicato dalle icone. Consulta [Autorizzazioni](#permissions) per delle descrizioni di
ciascun tipo e una spiegazione delle icone.

Scegli tra le seguenti opzioni:

* Individuare utenti. Puoi individuare gli utenti nella tabella utilizzando il campo
**Ricerca**.
* Aggiungere utenti. Se disponi dell'autorizzazione `ammin` o
dell'autorizzazione `utenti` con accesso in `scrittura`, puoi aggiungere utenti. Per aggiungere un utente o un gruppo di utenti, fai clic su **AGGIUNGI SINGOLO UTENTE** o **AGGIUNGI GRUPPO
DI UTENTI**. Nel campo **Ricerca**, immetti un nome utente o nome gruppo da
ricercare, quindi seleziona l'organizzazione a cui aggiungere l'utente o il gruppo di utenti
dall'elenco **Organizzazione**. Una volta trovato l'utente o il gruppo che desideri aggiungere,
fai clic sul nome utente e quindi su **AGGIUNGI UTENTE** o **AGGIUNGI UTENTI**.
I gruppi di più di 50 utenti vengono aggiunti attraverso un processo batch in background. Se l'operazione di aggiunta viene
completata correttamente, l'utente o il gruppo viene aggiunto alla tabella per consentirti operazioni di visualizzazione e ricerca. Quando gli utenti vengono aggiunti,
non dispongono di autorizzazioni.
* Modificare autorizzazioni e organizzazioni. Se disponi dell'autorizzazione `ammin`, puoi modificare
le autorizzazioni e le organizzazioni per gli altri utenti. Per modificare le autorizzazioni, individua
l'utente e fai clic sul nome utente. Per abilitare o disabilitare autorizzazioni, seleziona dalle seguenti opzioni nella finestra che viene visualizzata:
	* Seleziona **Attivo** dall'elenco per abilitare un'autorizzazione.
	* Seleziona **Lettura** dall'elenco per consentire all'utente di disporre dell'accesso in `visualizzazione` (sola lettura) per tale autorizzazione oppure **Scrittura**
 per consentire l'accesso in `scrittura` (modifica o aggiunta e rimozione) per tale autorizzazione.
	* Seleziona **Disattivo** per disabilitare l'autorizzazione.
Per modificare le organizzazioni, seleziona dalle seguenti opzioni:
	* Aggiungi l'utente a un'organizzazione utilizzando il campo di ricerca per individuare un'organizzazione, facendo clic per
selezionare dalle opzioni e facendo clic su **AGGIUNGI**.
	* Rimuovi un utente da un'organizzazione facendo clic sull'icona ![Rimuovi, rappresentato da un segno meno](images/icon_remove.svg).
Al termine, fai clic su **SALVA**.
* Rimuovere utenti. Se disponi dell'autorizzazione `ammin` o
dell'autorizzazione `utenti` con accesso in `scrittura`, puoi rimuovere utenti.
Per rimuovere un utente, individualo e fai clic sull'icona ![Elimina](images/icon_trash.svg) e quindi su **Rimuovi**.

### Autorizzazioni
{: #permissions}

È possibile assegnare agli utenti le seguenti autorizzazioni:

*Tabella 5. Autorizzazioni*

| **Autorizzazione utente** | **Descrizione** |       
|-----------------|-------------------|
| Ammin | Gli utenti con l'autorizzazione `ammin` possono
modificare le autorizzazioni per gli altri utenti. |
| Catalogo | Agli utenti con autorizzazione `catalogo` può essere assegnato l'accesso in `visualizzazione` o in `scrittura` (modifica) per i servizi disponibili nell'istanza locale o dedicata. |  
| Accesso | Agli utenti con autorizzazione `accesso` è consentito visualizzare la pagina Amministrazione. Senza questa autorizzazione, gli utenti non possono vedere l'opzione di menu Amministrazione. |
| Report | Agli utenti con autorizzazione `report` può essere assegnato l'accesso in `visualizzazione` o in `scrittura` (modifica) per i report di sicurezza. |
| Utenti | Agli utenti con autorizzazione `utenti` può essere assegnato l'accesso in `visualizzazione` per l'elenco di utenti o in `scrittura` (aggiunta o rimozione) per gli utenti. Questa autorizzazione non ti consente di impostare le autorizzazioni per gli altri utenti.|

È possibile abilitare le autorizzazioni o fornire agli utenti l'accesso in `visualizzazione` o
in `scrittura` per l'autorizzazione indicata, come indicato dalle seguenti icone:

* L'icona ![Abilitato, rappresentata da un segno di spunta](images/icon_enabled.svg) con un'autorizzazione significa che essa è abilitata.
* L'icona ![Visualizza, rappresentata da un occhio](images/icon_read.svg) indica che l'utente dispone di un accesso in `visualizzazione` (sola lettura) per tale autorizzazione.
* L'icona ![Scrittura, rappresentata da una matita](images/icon_write.svg) indica che l'utente dispone di un accesso in `scrittura` (modifica, aggiunta o rimozione) per tale autorizzazione.

## Gestione degli utenti con la API REST Admin
{: #usingadminapi}

Puoi utilizzare l'API REST `Admin` per aggiungere e rimuovere utenti per l'istanza {{site.data.keyword.Bluemix_notm}}.
Gli endpoint della API REST `Admin` e le risposte JSON sono fornite su base sperimentale per abilitare le operazioni di base da una riga di comando. Gli endpoint e gli URL negli esempi nelle presenti
informazioni possono variare o potrebbero essere abbandonate con breve preavviso.

I seguenti strumenti sono prerequisiti per utilizzare gli esempi di seguito riportati. Puoi anche scegliere di
            utilizzare altri strumenti.
* cURL, per immettere richieste API REST come comandi. cURL è un programma di utilità gratuito che puoi
                    utilizzare per inviare richieste HTTP a un server e ricevere le risposte
                    attraverso un'interfaccia riga di comando. Puoi scaricare
cURL dal [sito cURL/Download](http://curl.haxx.se/download.html){: new_window}.
* Python, per utilizzare lo strumento JSON Pretty-Print Python. Questo strumento
facoltativo prende il testo JSON come input e fornisce un output facile da leggere. Puoi scaricare Python dal sito [Downloads di Python](https://www.python.org/downloads){: new_window}.

### Accesso alla Console di gestione

Prima di poter eseguire qualsiasi richiesta API `Admin`,
devi eseguire l'accesso alla Console di gestione. Se disponi dell'autorizzazione `ammin`
o dell'autorizzazione `utenti` con accesso in `scrittura`, puoi aggiungere o rimuovere utenti. Per modificare le autorizzazioni di altri utenti devi disporre
dell'autorizzazione `ammin`.

Per accedere alla Console di gestione, puoi utilizzare l'autenticazione di accesso di base sull'endpoint `https://<il_tuo_host>.ibm.com/login`. Il server restituisce un cookie con la tua sessione. Puoi utilizzare tale
cookie per tutte le operazioni con la Console di gestione.

**Nota:** la sessione diventa non valida se non viene utilizzata per qualche ora.

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
        "familyName": "*cognome*",
        "givenName": "*nome*"
    }
}
```
{: screen}

### Elenco delle organizzazioni
{: #listingorg}

Quando aggiungi un utente, devi specificare un'organizzazione. Puoi
utilizzare la API REST `Admin` per elencare tutte le organizzazioni. Per elencare le
organizzazioni devi disporre dell'autorizzazione `utenti` con accesso in
`lettura`. Per elencare tutte le organizzazioni, esegui il seguente comando:

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

Puoi determinare se un utente è già stato aggiunto al tuo ambiente {{site.data.keyword.Bluemix_notm}} utilizzando
l'API REST `Admin` per elencare gli utenti registrati. Per elencare gli utenti registrati devi disporre di un'autorizzazione `utenti`
con accesso in `lettura`. Per elencare tutti gli utenti, esegui il seguente comando:

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

Puoi utilizzare l'API REST `Admin` per aggiungere utenti all'istanza {{site.data.keyword.Bluemix_notm}}. Per aggiungere utenti
devi disporre dell'autorizzazione `utenti` con accesso in
`scrittura`.

Puoi aggiungere un singolo utente o un elenco di utenti. Puoi aggiungere utenti a una
o più organizzazioni. Per aggiungere un utente,
devi fornire le seguenti informazioni:

* Nome e cognome dell'utente. Fornisci `"nome"` e `"cognome"` da [Elenco degli utenti](index.html#listingusr).
* Indirizzo email e ID utente: fornisci l'`"id_utente"` da [Elenco degli utenti](index.html#listingusr) sia per l'indirizzo email sia per l'ID utente.
* `"guid"`. Fornisci il GUID dell'organizzazione da [Elenco delle organizzazioni](index.html#listingorg).

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
<pre>
{
    "members": [
        {
            "emails": [
                "un_id_utente@dominio.com"
            ],
            "first_name": "un_nome",
            "last_name": "un_cognome",
            "user_id": "un_id_utente@dominio.com"
        }
    ],
    "organization_roles": [
        {
            "id": "7a891f9c-e4e7-46c7-8b4e-dffaa7eb3bcd"
        }
    ]
}
</pre>
</li>
<li>Pubblica il contenuto del file JSON nell'endpoint dell'utente immettendo il seguente comando:<br/><br/>
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
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < vary: X-HTTP-Method-Override
 < content-type: application/json
 < date: Wed, 22 Apr 2015 19:32:54 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 5612 msec
 ```
{: screen}

### Rimozione di un utente

Puoi utilizzare l'API REST `Admin` per rimuovere gli utenti dall'istanza {{site.data.keyword.Bluemix_notm}}. Per
rimuovere degli utenti devi disporre dell'autorizzazione `utenti` con accesso in `scrittura`.

Per rimuovere un utente, devi fornire l'ID dell'utente: Immetti il seguente comando:

`curl -v -b ./cookies.txt -X DELETE https://<il_tuo_host>.ibm.com/codi/v1/users?user_id=<un_id_utente@dominio.com>`
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
 > DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 >
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < content-type: application/json
 < date: Wed, 22 Apr 2015 21:01:09 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 1922 msec
 <
 ```
{: screen}


## API del servizio personalizzato
{: #servicebrokerapi}

Sono disponibili tre API che ti consentono di registrare o creare un nuovo servizio, di aggiornare un servizio e di eliminare un servizio.

Tutte le API sono relative a <code>https://console.&lt;subdomain&gt;.bluemix.net/</code>.

<dl>
<dt><strong>&lt;dominiosecondario&gt;</strong></dt>
<dd>Questo valore è il nome della tua istanza locale o dedicata. Il nome del dominio secondario per la tua istanza {{site.data.keyword.Bluemix}} è stato
assegnato durante l'onboarding.</dd>
</dl>

## Registrazione di un nuovo servizio

Utilizza i seguenti esempi di API e codice per registrare un nuovo servizio.

### Rotta
{: #registerroute}

```
POST /codi/v1/serviceBrokers
```
{: screen}

### Richiesta
{: #registerrequest}

*Tabella 6. Campi*

| **Nome** | **Descrizione** |
|-----------------|-------------------|
| name | Nome del broker dei servizi. |
| auth_username | Nome utente utilizzato per connettersi al broker dei servizi. |
| auth_password | Password utilizzata per connettersi al broker dei servizi. |
| broker_url | URL utilizzato per connettersi al broker dei servizi. |
| owningOrganization | Organizzazione iniziale per cui aggiungere il servizio nell'elenco elementi consentiti. |


#### Corpo
{: #registerbody}

```
{
  "name" : "Nome del broker dei servizi",
  "auth_username" : "nome utente",
  "auth_password" : "password",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### Intestazioni
{: #registerheaders}

```
Autorizzazione: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Risposta
{: #registerresponse}

#### Stato
{: #registerstatus}

```
201 Creato
```
{: screen}

#### Corpo
{: #registerbody2}

```
{
  "entity": {
    "name": "Nome del broker dei servizi",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "auth_username": "nome utente",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "49f3adcc-ecc2-46fa-83c1-03322f04b3b1",
    "created_at": "2015-12-07T19:51:50Z",
    "updated_at": null,
    "url": "/v2/service_brokers/49f3adcc-ecc2-46fa-83c1-03322f04b3b1"
  }
}
```
{: screen}

## Aggiornamento di un servizio

Utilizza i seguenti esempi di API e codice per aggiornare un servizio.

### Rotta
{: #updateroute}

`PUT /codi/v1/serviceBrokers`
{: screen}

### Richiesta
{: #updaterequest}

*Tabella 7. Campi*

| **Nome** | **Descrizione** |
|-----------------|-------------------|
| name | Nome del broker dei servizi. Questo nome non può essere modificato dal nome con cui è stato creato il servizio. |
| auth_username | Nome utente utilizzato per connettersi al broker dei servizi. |
| auth_password | Password utilizzata per connettersi al broker dei servizi. |
| broker_url | URL utilizzato per connettersi al broker dei servizi. |
| owningOrganization | Organizzazione iniziale per cui aggiungere il servizio nell'elenco elementi consentiti. |


#### Corpo
{: #updatebody}

```
{
  "name" : "Nome del broker dei servizi",
  "auth_username" : "nome utente",
  "auth_password" : "nuova password",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### Intestazioni
{: #updateheaders}

```
Autorizzazione: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Risposta
{: #updateresponse}

#### Stato
{: #updatestatus}

```
201 Creato
```
{: screen}

#### Corpo
{: #updatebody2}

```
{
  "entity": {
    "name": "Nome del broker dei servizi",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "auth_username": "nome utente",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "2cbdb812-d37f-443b-894a-a96de31e5c38",
    "created_at": "2015-12-07T20:11:08Z",
    "updated_at": "2015-12-07T20:11:19Z",
    "url": "/v2/service_brokers/2cbdb812-d37f-443b-894a-a96de31e5c38"
  }
}
```
{: screen}

## Eliminazione di un servizio

Utilizza i seguenti esempi di API e codice per eliminare un servizio.

*Tabella 8. Parametro*

| **Nome** | **Descrizione** |
|-----------------|-------------------|
| name | Nome del broker dei servizi. Questo nome non può essere modificato dal nome con cui è stato creato il servizio. |


### Rotta

```
DELETE /codi/v1/serviceBrokers?name=name of service broker
```
{: screen}

### Richiesta
{: #deleterequest}

#### Intestazioni
{: #deleteheaders}

```
Autorizzazione: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Risposta
{: #deleteresponse}

#### Stato
{: #deletestatus}

```
204 Nessun contenuto
```
{: screen}

## Gestione degli utenti con la CLI cf
{: #usingadmincli}

Puoi gestire gli utenti per il tuo ambiente {{site.data.keyword.Bluemix_notm}}
utilizzando l'interfaccia riga di comando Cloud Foundry insieme al plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI. Ad
esempio, puoi aggiungere utenti da un registro LDAP.

Prima di iniziare, installa l'interfaccia riga di comando cf. Il plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI richiede cf versione 6.11.2 o successive. [Scarica
l'interfaccia riga di comando Cloud Foundry](https://github.com/cloudfoundry/cli/releases){: new_window}

**Limitazione:** l'interfaccia riga di comando Cloud Foundry non
è supportata da Cygwin. Utilizza l'interfaccia riga di comando Cloud Foundry
in una finestra riga di comando diversa da quella di Cygwin.

### Aggiunta del plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI

Dopo aver installato l'interfaccia riga di comandi cf, puoi
aggiungere il plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI.

**Nota**: se avevi già installato il plug-in Gestione {{site.data.keyword.Bluemix_notm}}, per ottenere gli ultimi aggiornamenti potresti doverlo disinstallare, eliminare il repository e reinstallare il plug-in.

Completa la seguente procedura per aggiungere il repository e installare
il plug-in:

<ol>
<li>Per aggiungere il repository del plug-in {{site.data.keyword.Bluemix_notm}} Admin, esegui questo comando:<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;dominiosecondario&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;dominiosecondario&gt;</dt>
<dd class="pd">Dominio secondario dell'URL per la tua istanza {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>
</li>
<li>Per installare il plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI, esegui questo comando:<br/><br/>
<code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

Per visualizzare un elenco di comandi, immetti il seguente
comando:

`cf plugins`
{: codeblock}

Per ulteriore assistenza per un comando, utilizza l'opzione `-help`.

Per ulteriori informazioni su come utilizzare il plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI, vedi [{{site.data.keyword.Bluemix_notm}} admin](../cli/plugins/bluemix_admin/index.html).
