---



copyright:

  anni: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestione di {{site.data.keyword.Bluemix_notm}} locale e {{site.data.keyword.Bluemix_notm}} dedicato
{: #mng}
Ultimo aggiornamento: 20 settembre 2016
{: .last-updated}

Se disponi dell'accesso come amministratore per {{site.data.keyword.Bluemix}} locale o {{site.data.keyword.Bluemix_notm}} dedicato, vai alla pagina **Amministrazione** per gestire risorse, monitorare l'utilizzo delle quote, amministrare le autorizzazioni utente, pianificare le notifiche di aggiornamento, visualizzare log e report di sicurezza e altro. Puoi gestire le tue organizzazioni creando degli spazi e impostando dei [ruoli e delle autorizzazioni per gli utenti](index.html#oc_useradmin); vedi [Gestione delle tue organizzazioni](../admin/orgs_spaces.html).
{:shortdesc}

*Tabella 1. Attività amministrative per la gestione della tua istanza di {{site.data.keyword.Bluemix_notm}} locale o dedicato*

| Quali operazioni posso eseguire? | Dettagli |    
|----------------|---------|
|Monitorare l'utilizzo del sistema | Fai clic su **AMMINISTRAZIONE &gt; UTILIZZO**. Visualizza le informazioni sul sistema, monitora l'utilizzo della CPU e pianifica l'utilizzo per ottimizzare il processo decisionale per la tua azienda. Vedi [Visualizzazione delle informazioni sull'utilizzo](index.html#oc_resource).|
|Gestire il tuo catalogo | Fai clic su **AMMINISTRAZIONE &gt; GESTIONE CATALOGO** per stabilire quali servizi sono visibili ai tuoi utenti e organizzazioni. Vedi [Gestione del tuo catalogo](index.html#oc_catalog).|
|Amministrare le organizzazioni | Fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE ORGANIZZAZIONE** per creare organizzazioni, monitorare le quote per le organizzazioni e prendere decisioni rapide basate sulle esigenze. Vedi [Amministrazione delle organizzazioni](index.html#oc_organizations).|
|Creare spazi e assegnare i ruoli utente | Fai clic sull'icona **{{site.data.keyword.avatar}}** ![Avatar](../support/images/account_support.svg), quindi seleziona **Gestisci organizzazioni** per creare spazi all'interno delle tue organizzazioni. Aggiungi utenti e assegna loro dei ruoli per l'organizzazione e lo spazio. Vedi [Gestione delle tue organizzazioni](../admin/orgs_spaces.html). |
|Gestire le autorizzazioni degli utenti amministrativi | Fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE UTENTI** per aggiungere e rimuovere utenti e modifica le autorizzazioni utente. Vedi [Gestione di utenti e autorizzazioni](index.html#oc_useradmin). |
|Esaminare report e log | Fai clic su **AMMINISTRAZIONE &gt; REPORT E LOG** per visualizzare i report di sicurezza e i log di controllo relativi alla tua istanza. Vedi [Visualizzazione dei report](index.html#oc_report). |
|Visualizzare le informazioni sul sistema. | Fai clic su **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA** per visualizzare le informazioni di sistema, quali aggiornamenti di manutenzione in sospeso, nome e versione della tua istanza, regione, URL API, URL CLI, dettagli di configurazione LDAP, associazioni di gruppi e utenti, statistiche e domini condivisi. Vedi [Visualizzazione delle informazioni sul sistema](index.html#oc_system). |
|Estendere le notifiche e impostare le sottoscrizioni evento | Fai clic su **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA &gt; *Numero* in sospeso**. Puoi utilizzare webhook da integrare con un servizio Web a scelta per impostare una sottoscrizione di notifica evento per un aggiornamento o incidente. Vedi [Notifiche e sottoscrizioni di eventi](index.html#oc_eventsubscription). |



## Notifiche e sottoscrizioni di eventi
{: #oc_eventsubscription}

Puoi sempre conoscere lo stato del tuo ambiente consultando la pagina Stato. Non appena si verificano, gli incidenti e gli eventi di aggiornamento della manutenzione pianificata con interruzioni del servizio vengono segnalati nella pagina Stato. {{site.data.keyword.Bluemix_notm}} invia inoltre alla pagina Amministrazione dell'area Notifiche le eventuali notifiche riguardanti eventi quali aggiornamenti di manutenzione pianificati o in sospeso.

### Notifiche

Puoi visualizzare le notifiche riguardanti il tuo ambiente locale o dedicato, al fine di monitorare lo stato del tuo ambiente. Consulta la seguente tabella per informazioni sui diversi tipi di notifiche e sui rispettivi punti di pubblicazione.

*Tabella 2. Tipi di evento e metodi di notifica*

| **Tipo di evento** | **Metodo di notifica** |       
|-----------------|-------------------|
| Aggiornamenti di manutenzione | L'avviso dei prossimi aggiornamenti di manutenzione viene effettuato nella pagina Amministrazione dell'area Notifiche. Vai alla pagina **Amministrazione**, quindi seleziona l'icona **Notifiche** ![Notifiche](images/icon_announcement.svg). Per visualizzare uno storico e un elenco completo delle tue notifiche complete e in sospeso, fai clic su **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA** &gt; *Numero* **in sospeso**.|
|  | Ricevi anche un avviso degli eventi di aggiornamento della manutenzione pianificata con interruzioni del servizio nella pagina Stato. Fai clic sull'icona **{{site.data.keyword.avatar}}** ![Avatar](../support/images/account_support.svg) e seleziona **Stato**.|
|  | Puoi estendere la funzionalità di notifica impostando una sottoscrizione che invia un'email a destinatari di tua scelta. In alternativa, puoi impostare una sottoscrizione che utilizza dei webhook per integrare le notifiche provenienti dalla pagina Amministrazione con un servizio Web a scelta.|
| Incidenti critici | Vieni avvisato degli incidenti critici sulla pagina Stato. Fai clic sull'icona **{{site.data.keyword.avatar}}** ![Avatar](../support/images/account_support.svg) e seleziona **Stato**. Puoi estendere la funzionalità di notifica impostando una sottoscrizione evento che invia un'email a un destinatario di tua scelta. In alternativa, puoi impostare una sottoscrizione che utilizza dei webhook per integrare le notifiche provenienti dalla pagina Amministrazione con un servizio Web a scelta.  |  
| Stato di {{site.data.keyword.Bluemix_notm}} | In qualsiasi momento puoi visualizzare l'ultimo stato della piattaforma, dei servizi e della tua istanza {{site.data.keyword.Bluemix_notm}} nella pagina Stato. Fai clic sull'icona **{{site.data.keyword.avatar}}** ![Avatar](../support/images/account_support.svg) e seleziona **Stato**.  |

### Impostazione di sottoscrizioni evento

Puoi estendere la funzionalità delle notifiche inviate alla pagina Amministrazione e alla pagina Stato, utilizzando le sottoscrizioni evento. Utilizza le sottoscrizioni evento per configurare un'e-mail personalizzata o utilizzare dei webhook da integrare con uno strumento a scelta.  
 * Se selezioni l'opzione e-mail, le tue notifiche vengono inviate agli indirizzi e-mail specificati. Puoi selezionare le notifiche di incidenti o di aggiornamenti di manutenzione. Viene inviata una notifica e-mail iniziale. Successivamente, ogni volta che l'incidente o l'aggiornamento di manutenzione presenta delle modifiche, viene inviata un'altra notifica con la modifica apportata.  
 * Se selezioni l'opzione webhook, le tue notifiche vengono indirizzate direttamente a una destinazione a scelta, ad esempio un numero di telefono (tramite messaggio SMS). Puoi personalizzare il tipo di notifica, in particolare aggiornamenti di manutenzione o avvisi di incidente critico, e le informazioni incluse nel corpo della notifica.

**Nota**: solo gli utenti con autorizzazione Superuser (`ops.admin`) possono impostare le sottoscrizioni evento.

Puoi accedere alla pagina **Sottoscrizioni evento** in uno dei seguenti modi:

* Per le notifiche di aggiornamento di manutenzione, vai a **INFORMAZIONI DI SISTEMA &gt; *Numero* in sospeso &gt; Sottoscrizioni**.
* Per le notifiche di incidente, fai clic sull'icona **{{site.data.keyword.avatar}}** ![Avatar](../support/images/account_support.svg) &gt; **Stato**, quindi fai clic sull'icona **Sottoscrivi** ![Sottoscrivi](images/icon_subscribe.svg).

**Nota**: puoi accedere alla pagina di sottoscrizione evento per entrambi i tipi di notifica, utilizzando uno qualsiasi dei due metodi descritti.

Per creare una sottoscrizione webhook o e-mail dalla pagina **Sottoscrizioni evento**, completa la seguente procedura:

1. Fai clic su **Aggiungi sottoscrizione**.
2. Compila il modulo di sottoscrizione evento. Per informazioni sui campi del modulo e sui valori da utilizzare nella sezione del payload e nel corpo del messaggio del template e-mail, consulta le seguenti tabelle.
3. Una volta completato il modulo, puoi scegliere tra le seguenti opzioni:

  * Fare clic su **Salva** per salvare la sottoscrizione al tuo elenco di sottoscrizioni evento.
  * Fare clic su **Salva e verifica** per salvare e verificare la notifica.
  * Fare clic su **Salva e chiudi** per salvare la sottoscrizione al tuo elenco di sottoscrizioni evento e tornare alla pagina precedente.

*Tabella 3. Campi del modulo di sottoscrizione evento per una sottoscrizione e-mail*

| **Campo** | **Descrizione** |
|-----------------|-------------------|
| Abilitato | Seleziona questa opzione per abilitare le notifiche e-mail. Deselezionare l'opzione per disabilitare la notifica e-mail. Le sottoscrizioni sono abilitate per impostazione predefinita. |
| Tipo | Seleziona **E-mail**. |
| Evento | Seleziona l'opzione per sottoscrivere le notifiche di un evento di **Manutenzione** o **Incidente**. |
| Combina notifiche | Seleziona l'opzione per combinare le notifiche di incidente di tutte le regioni in una singola notifica. Questa opzione è disponibile solo per gli incidenti. |
| Oggetto | Compila la riga oggetto dell'e-mail. Questo campo è obbligatorio.  |
| Corpo | Immetti il testo del corpo del messaggio da inviare nell'e-mail. Puoi utilizzare i valori payload IBM per inserire nella notifica e-mail informazioni pertinenti. Vedi la tabella [Valori della sezione di payload](index.html#payload) per identificare i valori utilizzabili. Utilizza tag HTML di base per strutturare l'e-mail. Questo campo è obbligatorio. |
| A: | Immetti uno o più indirizzi e-mail tramite elenco separato da virgole per indicare i destinatari della notifica e-mail. Espandi le opzioni "cc" o "bcc" per inviare copia dell'e-mail ad altri destinatari. Questo campo è obbligatorio. |
| Descrizione | Aggiungi una descrizione univoca della sottoscrizione e stai creando. |


*Tabella 4. Campi del modulo di sottoscrizione evento per una sottoscrizione webhook*

| **Campo** | **Descrizione** |
|-----------------|-------------------|
| Abilitato | Seleziona l'opzione per abilitare la notifica. Deselezionare l'opzione per disabilitare la notifica. Le sottoscrizioni sono abilitate per impostazione predefinita. |
| Tipo | Seleziona **Webhook** |
| Metodo | Seleziona **GET** o **POST**. |
| Evento | Seleziona l'opzione per sottoscrivere le notifiche di un evento di **Manutenzione** o **Incidente**. |
| Combina notifiche | Seleziona l'opzione per combinare le notifiche di incidente di tutte le regioni in una singola notifica. Questa opzione è disponibile solo per gli incidenti. |
| URL | Immetti l'URL per la connessione al tuo servizio Web. |
| Descrizione | Aggiungi una descrizione univoca della sottoscrizione e stai creando. |
| Nome utente | Immetti il tuo nome utente per il tuo servizio Web. Se non desideri utilizzare le tue credenziali personali, puoi impostare un ID funzionale da utilizzare specificatamente con {{site.data.keyword.Bluemix_notm}}. |
| Password | Immetti la password per il tuo servizio Web. |
| Payload | Se hai selezionato il metodo POST, immetti le proprietà specifiche del servizio Web che stai utilizzando insieme i valori di payload utilizzati per la notifica IBM. Vedi la tabella [Valori della sezione di payload](index.html#payload) per identificare i valori utilizzabili. Se non immetti informazioni in questa sezione, ricevi una notifica priva di informazioni aggiuntive. |

*Tabella 5. Valori della sezione payload*
{: #payload}

| **Valore IBM** | **Descrizione** | **Tipo di evento** |
|----------------|----------------|------------------------|
| {{content.title}} | Titolo del messaggio |  Aggiornamento di manutenzione e incidente |
| {{content.message}} | Descrizione del messaggio |   Aggiornamento di manutenzione e incidente |
| {{region}} | Regione interessata | Aggiornamento di manutenzione e incidente |
| {{content.severity}} | Classificazione della severità | Incidente |
| {{content.category}} | Servizi interessati | Incidente |
| {{content.subCategoryName}} | Componenti interessati | Incidente |
| {{status}} | Stato dell'aggiornamento | Aggiornamento di manutenzione |
| {{content.scheduleWindow.start}} | La data di inizio pianificata per l'aggiornamento | Aggiornamento di manutenzione |
| {{content.disruption}} | Componenti interessati | Aggiornamento di manutenzione |
| {{type}} | Aggiornamento o incidente | Aggiornamento di manutenzione e incidente |
| {{content.scheduleWindow.end}} | L'ora di fine pianificata per l'aggiornamento | Aggiornamento di manutenzione |

Quando salvi la tua sottoscrizione evento, ricevi notifiche attraverso il metodo che hai impostato. Le notifiche vengono ancora pubblicate nelle seguenti posizioni:  
 * Nella pagina Stato per gli incidenti 
 * Nella pagina Stato per gli eventi di aggiornamento della manutenzione pianificata con interruzioni del servizio
 * Nell'area Notifica della pagina Amministrazione per gli aggiornamenti di manutenzione

Puoi selezionare qualsiasi sottoscrizione evento salvata, visualizzare le attività recenti o modificarle come necessario. Fai clic per espandere qualsiasi voce delle attività recenti per visualizzare i dettagli della cronologia.

## Aggiornamenti di manutenzione
{: #oc_schedulemaintenance}

Puoi visualizzare gli aggiornamenti di manutenzione pianificata e in sospeso solo se disponi dell'autorizzazione superuser (`ops.admin`), facendo clic su **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA &gt; *Numero* in sospeso** per accedere alla pagina **Aggiornamenti di sistema**.  Tutti gli utenti del tuo ambiente possono visualizzare gli eventi di aggiornamento della manutenzione pianificata con interruzioni del servizio facendo clic sull'icona **{{site.data.keyword.avatar}}** ![Avatar](../support/images/account_support.svg) e selezionando quindi **Stato**.

**Nota**: consultare la seguente sezione per [Impostazione di finestre di manutenzione preapprovate](index.html#preapprovedmaintenance). Queste finestre devono essere impostate per consentire a IBM di pianificare la manutenzione per il tuo ambiente.

<dl>
<dt>Aggiornamenti che non comportano interruzioni del servizio</dt>
<dd>Un aggiornamento che non comporta interruzioni del servizio non influenza il tuo ambiente, le tue applicazioni in esecuzione o l'accesso dei tuoi utenti alle tue applicazioni. Questo tipo di aggiornamento non richiede un'approvazione caso per caso e verrà applicato durante le finestre di manutenzione disponibili preapprovate da te impostate dalla pagina Aggiornamenti di sistema.</dd>
<dt>Aggiornamenti che comportano interruzioni del servizio</dt>
<dd>Un aggiornamento che comporta interruzioni del servizio può influenzare il tuo ambiente, le applicazioni in esecuzione o l'accesso dei tuoi utenti alle tue applicazioni. Devi pianificare e approvare ciascuno di questi aggiornamenti di manutenzione entro la finestra di manutenzione di 21 giorni assegnata. Puoi selezionare l'ora e la data di distribuzione suggerita, l'opzione per qualsiasi finestra preapprovata da te oppure aprire il calendario per selezionare tre date/ore specifiche tra cui IBM può scegliere durante la pianificazione dell'aggiornamento.</dd>
</dl>


### Impostazione delle finestre di manutenzione preapprovate
{: #preapprovedmaintenance}

Prima di iniziare la pianificazione e l'approvazione di aggiornamenti, devi impostare le tue finestre di manutenzione preapprovate. Gli aggiornamenti che non comportano interruzioni del servizio vengono pianificati in modo che vengano eseguiti all'interno delle finestre temporali preapprovate.

Devi impostare un minimo di 12 ore disponibili in una settimana per un periodo minimo di due giorni per ogni settimana. Ad esempio, puoi impostare finestre temporali di 6 ore in due giorni distinti o puoi impostare finestre di 4 ore in tre giorni diversi. Per accertarti che le finestre temporali siano sufficienti per consentire l'applicazione di un aggiornamento, la durata minima di ciascuna finestra deve essere pari a quattro ore.

**Nota**: solo gli utenti con autorizzazione Superuser (`ops.admin`) possono pianificare e approvare gli aggiornamenti di manutenzione.

1. Vai a **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA &gt; *Numero* in sospeso &gt; Gestisci disponibilità**.
2. Espandi la sezione **Gestisci finestre di aggiornamento disponibili**.
3. Fai clic su **Aggiungi nuovo** ![Aggiungi nuovo](images/add-new.png).
4. Imposta la prima finestra di disponibilità selezionando la frequenza, la durata e l'ora di inizio per la finestra.
5. Facoltativo: seleziona **Contrassegna come preferito**, se vuoi impostare la tua finestra di disponibilità ricorrente come orario preferito per le distribuzioni da pianificare. Le finestre temporali preferiti avranno la priorità, laddove possibile.
6. Fai clic su **Inoltra**.
7. Ripeti questo processo finché non hai soddisfatto i requisiti minimi per le finestre temporali settimanali.

### Impostazione delle finestre di manutenzione non disponibili

Dopo che hai impostato le tue finestre di manutenzione disponibili preapprovate, puoi scegliere di impostare specifiche date e ore per cui il tuo ambiente non è disponibile per gli aggiornamenti. Ad esempio, puoi scegliere un fine settimana o una vacanza ad alto traffico durante la quale non vuoi che venga applicata alcuna manutenzione per garantire che le tue applicazioni siano disponibili ai tuoi utenti.

1. Vai a **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA &gt; *Numero* in sospeso &gt; Gestisci disponibilità**.
2. Espandi la sezione **Gestisci finestre di aggiornamento non disponibili**.
3. Fai clic su **Aggiungi nuovo** ![Aggiungi nuovo](images/add-new.png).
4. Imposta la tua finestra non disponibile selezionando la frequenza, la durata e l'ora di inizio per la finestra.
5. Fai clic su **Inoltra**.

### Pianificazione e approvazione di aggiornamenti
{: #scheduleandapprove}

Dopo che hai impostato le tue finestre di manutenzione preapprovate, gli aggiornamenti che non comportano interruzioni del servizio verranno automaticamente pianificati durante questi periodi. Per questi tipi di aggiornamenti non è richiesta la tua approvazione esplicita. Puoi tuttavia visualizzare i dettagli per ciascun aggiornamento di manutenzione, compresa l'indicazione di cosa si sta aggiornando, quanto ci vorrà per l'aggiornamento e quando esso è pianificato.

Per visualizzare i dettagli per un aggiornamento che non comporta l'interruzione del servizio, completa la seguente procedura:

1. Vai a **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA &gt; *Numero* in sospeso**
2. Identifica le righe in cui **Pianificazione cliente obbligatoria** è impostato su **No**.
3. Seleziona la riga per l'aggiornamento di cui visualizzare i dettagli.

Un aggiornamento che comporta interruzioni del servizio può influenzare il tuo ambiente, le applicazioni in esecuzione o l'accesso dei tuoi utenti alle tue applicazioni. Devi pianificare e approvare ciascuno di questi aggiornamenti di manutenzione entro la finestra di manutenzione di 21 giorni assegnata. Puoi selezionare l'ora e la data di distribuzione suggerita, l'opzione per qualsiasi finestra preapprovata da te oppure aprire il calendario per selezionare tre date/ore specifiche tra cui IBM può scegliere durante la pianificazione dell'aggiornamento.

Per gli aggiornamenti che comportano un'interruzione del servizio che richiedono la tua approvazione, completa la seguente procedura:

1. Vai a **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA &gt; *Numero* in sospeso**
2. Identifica le righe in cui **Pianificazione cliente obbligatoria** è impostato su **Sì**.
3. Seleziona la riga per di un aggiornamento per esaminarne i dettagli, compresi la sua descrizione, la sua data e ora consigliata, i componenti interessati e la sua durata.
4. Seleziona **Pianifica e approva**.
5. Scegli una delle seguenti opzioni: **Data suggerita**, **Date alternative** o **Qualsiasi finestra preapprovata**. Se selezioni **Date alternative**, puoi aprire il calendario per selezionare tre opzioni tra cui può scegliere IBM.
6. Facoltativo: dall'elenco di date alternative selezionate nel calendario, seleziona quelle che desideri impostare come preferite per la distribuzione. Ogni data selezionata viene indicata come preferita per il deployer che pianificherà la distribuzione. IBM tenta di pianificare la manutenzione durante le finestre di aggiornamento preferite.
7. Quando hai finito, seleziona **Invia**.

A seconda della tua selezione, l'aggiornamento viene pianificato in modo da essere distribuito durante la data suggerita che hai accettato, durante una delle tue finestre temporali preapprovate o in una delle date e ore specifiche che hai selezionato. Quando IBM pianifica la distribuzione dell'aggiornamento, la data prevista viene rispecchiata nei dettagli dell'aggiornamento, sulla pagina **Aggiornamenti di sistema**. Puoi ripianificare una distribuzione già pianificata solo un giorno (24 ore) prima della data e ora di inizio pianificata. Dopo aver ripianificato una distribuzione, non potrai ripianificarla di nuovo.


## Visualizzazione delle informazioni sul sistema
{: #oc_system}

Per visualizzare le informazioni sul sistema, fai clic su **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA**.

Puoi espandere e visualizzare diverse sezioni relative ad aggiornamenti di manutenzione in sospeso, informazioni sul sistema generali e dettagli della configurazione LDAP.

### Aggiornamenti di sistema in sospeso

Nella sezione Aggiornamenti, puoi visualizzare il numero di notifiche di
aggiornamenti in sospeso che richiedono un tuo intervento. Ci sono due tipi di aggiornamenti di manutenzione che potresti vedere:

<dl>
<dt>Aggiornamenti che non comportano interruzioni del servizio</dt>
<dd>Un aggiornamento che non comporta interruzioni del servizio non influenza il tuo ambiente, le tue applicazioni in esecuzione o l'accesso dei tuoi utenti alle tue applicazioni. Questo tipo di aggiornamento non richiede un'approvazione caso per caso. Questi aggiornamenti sono applicati nelle finestre di manutenzione disponibili preapprovate da te impostate dalla pagina Aggiornamenti di sistema.</dd>
<dt>Aggiornamenti che comportano interruzioni del servizio</dt>
<dd>Un aggiornamento che comporta interruzioni del servizio può influenzare il tuo ambiente, le applicazioni in esecuzione o l'accesso dei tuoi utenti alle tue applicazioni. Puoi pianificare e approvare ciascuno di questi aggiornamenti di manutenzione entro la finestra di manutenzione di 21 giorni assegnata per garantire che l'aggiornamento non venga applicato durante ore lavorative critiche. Puoi selezionare la data e l'ora di distribuzione consigliata che è basata sulle tue finestre di aggiornamento preapprovate oppure puoi selezionare due ore e date aggiuntive da cui IBM può scegliere quando applica l'aggiornamento.</dd>
</dl>

Per ulteriori informazioni sull'impostazione delle finestre di manutenzione preapprovate e sull'impostazione di specifiche date non disponibili per la manutenzione, vedi [Aggiornamenti di manutenzione](admin/index.html#oc_schedulemaintenance).

### Informazioni generali sul sistema

Nella sezione di informazioni generali, puoi visualizzare le seguenti informazioni:

- Le informazioni di base sulla build {{site.data.keyword.Bluemix_notm}}.
- Le informazioni sull'API, compresi versione, URL, regione e un link alla documentazione della CLI.
- Le informazioni sul dominio condiviso relative al tuo sistema e al tuo servizio.
- Le statistiche sul numero totale di applicazioni, utenti e organizzazioni.

### Dettagli configurazione LDAP

Nella sezione Dettagli di configurazione LDAP, puoi selezionare il server LDAP
e visualizzare le informazioni relative alle associazioni di utenti e gruppi. Se stai utilizzando un WebID {{site.data.keyword.IBM}}, questo viene indicato in questa sezione.

## Visualizzazione di utilizzo e report
{: #oc_resource}

Puoi visualizzare differenti tipi di informazioni sull'utilizzo della tua istanza locale o dedicata e sull'account {{site.data.keyword.Bluemix_notm}}. Puoi anche scaricare e visualizzare i report e i log di sicurezza per la tua istanza {{site.data.keyword.Bluemix_notm}}.

- Informazioni sulle risorse, quali spazio su disco, utilizzo della CPU, utilizzo della rete e tempi medi di risposta. Vedi [Utilizzo risorsa](index.html#resourceusage).
- Utilizzo dell'account per organizzazione, incluso il numero di applicazioni di runtime con utilizzo, numero totale di GB-ore di runtime e numero di istanze di servizio con relativo utilizzo. Vedi [Utilizzo dell'account](index.html#accountusage).
- Utilizzo di quote di memoria, memoria dell'applicazione assegnata in base alla percentuale totale di memoria utilizzata e una vista sull'utilizzo di GB-ore per applicazione in relazione a un'organizzazione specifica. Puoi anche visualizzare l'utilizzo della quota per tutte le organizzazioni nella pagina Amministrazione della sezione **Monitoraggio quota**. Vedi [Amministrazione organizzazione](../admin/index.html#orgusage).


### Utilizzo delle risorse
{: #resourceusage}

Per visualizzare le informazioni sull'utilizzo delle risorse, fai clic su **AMMINISTRAZIONE &gt; Utilizzo risorsa**.

Nella sezione **Utilizzo risorsa **, puoi visualizzare le seguenti informazioni:

- Informazioni sull'utilizzo delle risorse, ad esempio la quantità di memoria e spazio su disco che può essere riservata e quella fisicamente disponibile e la quantità di memoria e spazio su disco realmente riservata e quella fisicamente utilizzata. Puoi anche visualizzare le informazioni relative all'utilizzo medio della CPU tra tutti gli agent DEA (Droplet Execution Agent). Per visualizzare l'utilizzo della memoria, disco o CPU da parte di DEA, fai clic su **Suddivisione**.
Puoi vedere un riepilogo dello spazio **Riservato** e **Fisico** relativo a memoria e disco.
	<dl>
	<dt><strong>Fisico</strong></dt>
	<dd>La quantità di memoria o spazio su disco che è stata acquistata per il tuo ambiente. </dd>
	<dt><strong>Riservato</strong></dt>
	<dd>La quantità totale di memoria o spazio su disco disponibile che può essere riservata da tutte le applicazioni distribuite e in esecuzione nel tuo ambiente. Poiché le applicazioni raramente utilizzano tutta la memoria riservata per loro, il valore fisico è di solito inferiore al valore riservato.</dd>
	</dl>

	Oltre alla rappresentazione grafica, puoi visualizzare la percentuale di memoria e spazio su disco utilizzata dal tuo ambiente.  Puoi anche visualizzare la quantità riservata e fisica, in GB, dell'utilizzo reale rispetto alla quantità disponibile.
Per informazioni più dettagliate sull'utilizzo della memoria fisica e riservata, fai clic su **Cronologia.** Puoi specificare l'intervallo di tempo da visualizzare come settimanale o mensile. La vista **Cronologia di utilizzo della memoria** mostra un grafico di utilizzo della memoria nel corso del tempo da te scelto.  

	<dl>
	<dt><strong>Limite riservato</strong></dt>
	<dd>Indicato in forma di linea tratteggiata orizzontale, il limite riservato è la quantità totale di memoria che può essere riservata collettivamente da tutte le applicazioni in esecuzione nel tuo ambiente.</dd>
	<dt><strong>Riservato</strong></dt>
	<dd>L'area Riservato mostra la memoria riservata collettivamente da tutte le applicazioni in esecuzione nel tuo ambiente.
	<p>Per vedere quali organizzazioni hanno riservato la maggior parte della memoria in un determinato momento, passa il mouse sopra il punto lungo l'area Riservato associato a quel momento nel tempo. Puoi quindi fare clic su un'organizzazione nel grafico a torta che viene mostrato per visualizzare ulteriori informazioni su tale organizzazione.</p></dd>
	<dt><strong>Limite fisico</strong></dt>
	<dd>Indicato in forma di linea tratteggiata orizzontale, il limite fisico mostra la quantità di memoria fisica che è stata acquistata per il tuo ambiente.</dd>
	<dt><strong>Fisico</strong></dt>
	<dd>L'area Fisico mostra la quantità di memoria effettivamente utilizzata.</dd>
	</dl>
- Informazioni sull'utilizzo della rete per la larghezza di banda in entrata e in uscita nelle ultime 6 ore o nel giorno precedente. I dati visualizzati sono basati sulla somma del traffico in entrata e in uscita per la rete pubblica e quella privata.
- Il tempo di risposta medio per {{site.data.keyword.Bluemix_notm}} negli ultimi 10 minuti, 1 ora e 1 giorno.
- Le transazioni medie al secondo per {{site.data.keyword.Bluemix_notm}} nel corso degli ultimi 10 minuti, dell'ultima ora e dell'ultimo giorno.

### Utilizzo dell'account
{: #accountusage}

Puoi visualizzare l'utilizzo mensile del tuo account per il tuo ambiente locale o dedicato. Puoi utilizzare questi dati per sapere quanto addebitare a determinate organizzazioni in base all'uso effettuato. Tutti gli utenti della console di gestione che dispongono dell'autorizzazione **Utenti** con accesso in **Lettura** possono visualizzare i dati di utilizzo dell'account. Inoltre, i gestori di fatturazione dell'organizzazione possono visualizzare i dati di utilizzo account relativi alle proprie organizzazioni, anche se il gestore di fatturazione non dispone dell'autorizzazione **Utenti** della console di gestione. In qualità di amministratore della console di gestione (autorizzazione Superuser), puoi assegnare il ruolo di gestore di fatturazione per le organizzazioni facendo clic sull'icona **{{site.data.keyword.avatar}}** ![Avatar](../support/images/account_support.svg) &gt; **Gestisci organizzazioni**.

Per visualizzare i dati di utilizzo account, completa la seguente procedura:

<ol>
<li>Fai clic sull'icona <strong>{{site.data.keyword.avatar}}</strong> ![Avatar](../support/images/account_support.svg) &gt; <strong>Account</strong> &gt; <strong>Dettagli di utilizzo</strong>.</li>
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
<li>Fai clic sull'icona <strong>{{site.data.keyword.avatar}}</strong> ![Avatar](../support/images/account_support.svg) &gt; <strong>Account</strong> &gt; <strong>Dettagli di utilizzo</strong>.</li>
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

### Report
{: #oc_report}

Puoi visualizzare i report e i log di sicurezza, quali DataPower&trade;, firewall e controllo accessi, per la tua istanza {{site.data.keyword.Bluemix_notm}}. Per visualizzare report e log, fai clic su **AMMINISTRAZIONE &gt; REPORT E LOG**.

Seleziona dalle seguenti opzioni:

- Puoi selezionare le date di inizio e di fine dai campi per filtrare i report e i log da
visualizzare.
- Puoi espandere e visualizzare i diversi report dal riquadro di navigazione.
- Puoi effettuare ricerche nella tua raccolta di report e log. La ricerca si applica ai nomi di report e al contenuto testuale
all'interno di report e log. Puoi anche scegliere di filtrare la ricerca in base
agli **Eventi di amministrazione**, ai **Report DataPower**, al **Firewall** e al **Controllo accessi**.
- Durante la visualizzazione di un report o log, puoi fare clic sull'icona ![Download](images/icon_download.png)
per scaricare il report.

La seguente tabella mostra l'elenco dei report di sicurezza generati per {{site.data.keyword.Bluemix_notm}} locale e {{site.data.keyword.Bluemix_notm}} dedicato. La maggior parte dei report viene generata ogni giorno.  Tuttavia, i report per gli eventi di gestione chiavi e crittografia vengono generati mensilmente. Tutti i report vengono conservati per 90 giorni nella console di gestione. Al termine dei 90 giorni, i report sono disponibili offline su richiesta a {{site.data.keyword.Bluemix_notm}} per 9 mesi. In totale, i report sono disponibili per il recupero per un massimo di 1 anno.

*Tabella 6. Elenco dei report di sicurezza*

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

Puoi visualizzare lo stato per l'ambiente {{site.data.keyword.Bluemix_notm}} e per la console di gestione.

### Stato dell'ambiente {{site.data.keyword.Bluemix_notm}}

Puoi monitorare lo stato per la tua istanza {{site.data.keyword.Bluemix_notm}} utilizzando la pagina Stato di {{site.data.keyword.Bluemix_notm}}. Fai clic sull'icona **{{site.data.keyword.avatar}}** ![Avatar](../support/images/account_support.svg) e seleziona **Stato**.

La pagina Stato è la posizione centrale per trovare notifiche e annunci sugli eventi chiave che interessano la piattaforma {{site.data.keyword.Bluemix_notm}} e i servizi principali in {{site.data.keyword.Bluemix_notm}}. Puoi sottoscrivere a un feed RSS per le notifiche in modo da non doverle controllare personalmente. Per ulteriori informazioni sulla pagina Stato e sulla configurazione del feed RSS, vedi [Visualizzazione di {{site.data.keyword.Bluemix_notm}}](../support/index.html#viewing-bluemix-status).

### Stato della console di gestione

Dopo la distribuzione iniziale del tuo ambiente {{site.data.keyword.Bluemix_notm}}, un controllo di verifica viene completato automaticamente sui componenti utilizzati per amministrare il tuo ambiente. Puoi andare alla pagina Controllo verifica console di gestione per controllare lo stato dei componenti dopo che è stato eseguito il controllo di verifica. Per accedere alla pagina,
vai a <code>https://console.&lt;dominiosecondario&gt;.bluemix.net/check</code>, dove `<dominiosecondario>` è il nome della tua istanza locale o dedicata.

Puoi eseguire una verifica in qualsiasi momento. Devi aver eseguito l'accesso per selezionare l'opzione per eseguire la verifica. Se riscontri dei malfunzionamenti mentre stai aggiungendo un utente, modificando un'organizzazione o gestendo i tuoi servizi, esegui questo controllo per identificare eventuali componenti malfunzionanti o disconnessi. Puoi aprire un ticket del supporto con le informazioni dal controllo per far risolvere rapidamente il problema.

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

Puoi inoltre gestire l'ordine di priorità dei pacchetti di build disponibili da scegliere in base alla compatibilità, che i tuoi sviluppatori utilizzeranno durante la creazione di applicazioni.

1. Vai a **AMMINISTRAZIONE&gt; GESTIONE CATALOGO**
2. Vai alla sezione **Calcola**.
3. Seleziona **Priorità pacchetto di build**.
4. Seleziona l'opzione pacchetto di build a cui assegnare una priorità maggiore o minore nell'elenco.
5. Con l'opzione selezionata, utilizza le frecce per spostare l'opzione all'interno dell'elenco.

<!-- staging only end -->

### Registrazione di un broker dei servizi
{: #servicebrokerui}

Se vuoi visualizzare un determinato servizio nel tuo catalogo {{site.data.keyword.Bluemix_notm}}, devi implementare e registrare un [broker dei servizi](http://docs.cloudfoundry.org/services/api.html){: new_window}. Una volta registrato il tuo broker, puoi scegliere quali organizzazioni possono accedere al servizio nella tua istanza locale o dedicata.

Le modalità d'uso del tuo broker dei servizi variano a seconda del numero di servizi che gestisce o dalla sua eventuale precedente registrazione in {{site.data.keyword.Bluemix_notm}}.

- Se il tuo broker dei servizi gestisce un unico servizio, puoi utilizzare l'interfaccia utente per registrarlo al termine dell'implementazione dell'[API broker dei servizi](http://docs.cloudfoundry.org/services/api.html){: new_window}. Vedi [Registrazione di un broker dei servizi che gestisce un unico servizio](index.html#registerbrokerui).
- Se il tuo broker dei servizi gestisce più servizi, utilizza la CLI cf con il plug-in [{{site.data.keyword.Bluemix_notm}} Admin CLI](../cli/plugins/bluemix_admin/index.html) (sottocomando `ba`) o l'[API del servizio personalizzato](index.html#servicebrokerapi).
- Se il tuo broker dei servizi è già registrato e desideri aggiornarlo o eliminarlo, utilizza la CLI cf con il plug-in [{{site.data.keyword.Bluemix_notm}} Admin CLI](../cli/plugins/bluemix_admin/index.html) (sottocomando `ba`) o l'[API del servizio personalizzato](index.html#servicebrokerapi).

#### Registrazione di un broker dei servizi che gestisce un unico servizio
{: #registerbrokerui}

Esamina le seguenti informazioni e completa la procedura per registrare il tuo broker dei servizi:

**Prima di iniziare**: <a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">implementa l'API broker dei servizi Cloud Foundry</a> per consentire la comunicazione tra il tuo servizio e {{site.data.keyword.Bluemix_notm}}. L'API broker dei servizi è un insieme di endpoint REST utilizzati da {{site.data.keyword.Bluemix_notm}}.

Quando implementi il broker dei servizi, nella risposta JSON di <code>GET /v2/catalog</code> devi fornire le definizioni per i tuoi piani di servizio e servizi, incluse le informazioni sul servizio che desideri visualizzare. Ad esempio, consulta il seguente file JSON di esempio della risposta del catalogo (GET):

```
{
"services":[
   {
      "bindable":true,
      "description":"Cool Service è una soluzione di analisi e data warehousing.",
      "id":"cool-service-id",
      "name":"coolservice",
      "metadata":{
         "displayName":"Cool Service",
         "serviceMonitorApi":"https://myservicesstatus.mybluemix.net/healthcheck/",
         "providerDisplayName":"Cool company",
         "longDescription":"Cool Service è una soluzione di data warehousing e analisi. Puoi spostare rapidamente i tuoi dati in un database in-memoria a colonne di prossima generazione e iniziare ad eseguire query analitiche complesse.",
         "bullets":[
            {
               "title":"Rapido e semplice",
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
               "caption":"Cool Service gestisce le tabelle",
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
                  "1 GB per istanza. 10 GB Max per istanza."
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
```
{: codeblock}

Le seguenti tabelle possono aiutarti a compilare il file JSON.

*Tabella. Campi JSON*

| **Campi JSON** | **Descrizione** |
|-----------------|-----------------|
|bindable   | Un valore booleano che indica se le istanze del servizio possono essere associate tramite bind alle applicazioni.  |
|description | La descrizione del servizio visualizzata quando utilizzi il comando cf marketplace o passi il mouse sull'icona del servizio nel catalogo dell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Puoi aggiungere una singola parola o frase per la descrizione. |
|name | Il nome del servizio visualizzato nell'interfaccia riga di comando cf. Questo nome deve essere univoco all'interno di {{site.data.keyword.Bluemix_notm}}, deve utilizzare lettere minuscole e non può contenere spazi. Dopo aver registrato il servizio con {{site.data.keyword.Bluemix_notm}}, non potrai più modificarne il nome. |
|ID  | L'ID del servizio. Questo ID deve essere univoco in {{site.data.keyword.Bluemix_notm}} e deve essere un GUID (Globally Unique Identifier). Dopo aver registrato il servizio con {{site.data.keyword.Bluemix_notm}}, non potrai più modificare l'ID. |
|metadata | I metadati del piano di servizio visualizzati nel catalogo {{site.data.keyword.Bluemix_notm}} e nel listino prezzi. Il campo dei metadati è facoltativo. Puoi specificare dei campi aggiuntivi per i metadati. Per ulteriori informazioni, vedi la seguente tabella per i [campi Metadati](index.html#metadatafields). |
|plans | Un array di definizioni del piano di servizio. Per ulteriori informazioni, vedi la seguente tabella per i [campi Piano](index.html#planfields). |

*Tabella. Campi Metadati*
{: #metadatafields}

| **Valori metadati** | **Descrizione** |
|---------------------|-----------------|
|displayName          | Il nome del piano visualizzato nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Questo nome viene visualizzato sia nel catalogo alla pagina dei dettagli del servizio che nel listino prezzi. Scrivi in maiuscolo solo la prima lettera del nome del piano. Non utilizzare "Predefinito" come nome piano predefinito, usa invece "Standard". |
|providerDisplayName | Il nome del provider di servizi |
|longDescription | La descrizione dettagliata per il servizio. Utilizza almeno due frasi per una descrizione lunga.  |
|plans                | Un array di definizioni del piano di servizio. Ogni voce di array del campo plans comprende i seguenti campi: name, description, free, id e metadata. Per ulteriori informazioni, vedi la seguente tabella per i [campi Piano](index.html#planfields). |
|bullets | Un array di stringhe visualizzate per un servizio. Puoi utilizzare gli elementi bullet per fornire informazioni in aggiunta alla descrizione lunga. Il campo bullets deve contenere almeno due elementi bullet. Ogni elemento bullet include il campo del titolo e della descrizione. |
|imageUrl | L'URL di un'immagine PNG grande  (50 x 50 pixel). |
|smallImageUrl | L'URL di un'immagine PNG piccola (24 x 24 pixel). |
|mediumImageUrl | L'URL di un'immagine PNG media (32 x 32 pixel). |
|featuredImageUrl | L'URL di un'immagine in evidenza (64 x 64 pixel). |
|documentationUrl | L'URL della documentazione per il servizio. |
|termsUrl | L'URL dei file PDF che contengono i termini dell'accordo. |
|media (facoltativo) | Un array di elementi per visualizzare i video e le acquisizioni schermo che introducono il servizio nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Un elemento media può contenere i seguenti campi: type (image, youtube, video), thumbnailUrl (l'URL dell'immagine di anteprima per l'elemento media), url (l'URL dell'acquisizione schermo o del video YouTube), source (le origini dei video che non sono ospitati su YouTube. Il "type" delle origini del video deve essere supportato da HTML5. Includi "type" e "url" per il video) e caption (la didascalia per l'elemento media. Le didascalie consentono un accesso facilitato agli utenti con disabilità per comprendere gli elementi media). |
|serviceKeysSupported | Un valore booleano che indica se l'API delle chiavi del servizio è supportata. L'API delle chiavi del servizio permette di abilitare l'utilizzo di un servizio al di fuori di {{site.data.keyword.Bluemix_notm}}. Il valore predefinito è false. |
|plan_updateable | Un valore booleano che indica se il servizio supporta le modifiche del piano. Il valore predefinito è false. |
|embeddableDashboard (facoltativo) | Un campo che indica come viene visualizzato il dashboard del servizio nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Se non specifichi questo campo, il dashboard viene integrato ma viene limitato a una larghezza minima di 960px e il dashboard avrà un riempimento orizzontale aggiuntivo intorno all'iframe. Puoi utilizzare true, false, drilldown o launch. Per questo valore puoi utilizzare i seguenti campi: true, false, drilldown e launch.  |
|notCreatable (facoltativo) | Un valore booleano che indica se le istanze per il servizio possono essere create dall'interfaccia utente {{site.data.keyword.Bluemix_notm}} e dall'interfaccia riga di comando cf. Il valore true significa che le istanze del servizio non possono essere create né dall'interfaccia utente {{site.data.keyword.Bluemix_notm}} né dall'interfaccia riga di comando cf. Il valore predefinito è false. |
|notCreatableMessage (facoltativo) | Un messaggio che viene visualizzato nell'interfaccia utente {{site.data.keyword.Bluemix_notm}} se non è possibile creare le istanze del servizio. Se non specifichi questo campo, verrà visualizzato il seguente messaggio predefinito: Per ricevere una notifica sulla disponibilità del servizio, confermare l'indirizzo email o immettere un nuovo indirizzo. |
|notCreatableRobotMessage (facoltativo) | Un messaggio che viene visualizzato nell'area commenti della pagina dei dettagli del servizio nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Il messaggio viene utilizzato per indicare che un servizio potrebbe avere un problema o altre cause che lo rendono non disponibile. Puoi specificare un messaggio per spiegare il motivo. Se non specifichi questo campo, verrà visualizzato il seguente messaggio predefinito: Questo servizio non è al momento disponibile. |
|apiReferenceUrl (facoltativo) | L'URL dell'iframe nell'area Riferimento API nella pagina dei dettagli del servizio all'interno del catalogo. Se non viene utilizzato per la pagina dei dettagli del servizio nel Catalogo, puoi immettere il valore numerico assegnato alla Documentazione API REST del tuo servizio durante la registrazione nel microservizio Documentazione API REST di {{site.data.keyword.Bluemix_notm}}. In questo modo, la documentazione dell'API REST verrà visualizzata nel dashboard del servizio. |
|sdkDownloadUrl (facoltativo) | L'URL della pagina Web che si apre quando fai clic sul pulsante Scarica SDK. Il pulsante Scarica SDK si trova nel tile del servizio nella pagina di panoramica dell'applicazione nel Dashboard. La pagina Web si apre in una scheda del browser.  |
|serviceMonitorApi    | L'URL di un'API che restituisce i dati JSON, come mostrato nel seguente esempio, che segnala l'integrità del servizio. Devi avere serviceMonitorApi o serviceMonitorApp nei metadati del servizio. Consulta il seguente codice come esempio. |
|serviceMonitorApp    | L'URL a un'applicazione che può essere distribuita in {{site.data.keyword.Bluemix_notm}} ed essere associata a un servizio per fornire l'output specifico dello stato del servizio. L'applicazione deve restituire il formato dei dati JSON uguale al serviceMonitorApi. Devi avere serviceMonitorApi o serviceMonitorApp nei metadati del servizio. Consulta il seguente codice come esempio. |

```
{
    "service": "servicename",
    "version": 1,
    "health": [
        {
            "plan": "starter",
            "status": 0,
            "serviceinput": "count(*) from healthcheck",
            "serviceoutput": "10…or error 1234 database not running",
            "responsetime": 4
        },
        {
            "plan": "enterprise",
            "status": 1,
            "serviceinput": "count(*)fromhealthcheck",
            "serviceoutput": "10…orerror1234databasenotrunning",
            "responsetime": 4
        }
    ]
}
```
{: pre}

Il seguente esempio mostra come la risposta JSON di GET /v2/catalog è associata alla pagina dei dettagli del servizio nel catalogo {{site.data.keyword.Bluemix_notm}}:

![Dettagli del servizio nel catalogo.](images/metadata.png "Vista dettagli del servizio nel catalogo Bluemix")

*Tabella. Campi Piano*
{: #planfields}

| **Valori del piano** | **Descrizione** |
|---------------------|-----------------|
|name       | Il nome del piano di servizio utilizzato nell'interfaccia riga di comando cf. Il nome del piano viene, ad esempio, visualizzato nell'output del comando cf marketplace. Il nome del piano deve essere in lettere minuscole, non può contenere spazi e deve essere univoco all'interno del servizio.   |
|description       | La descrizione del piano di servizio. La descrizione viene visualizzata quando selezioni una piano nella pagina dei dettagli del servizio nel catalogo {{site.data.keyword.Bluemix_notm}}. |
|free      | Un valore booleano che indica se il piano di servizio è gratuito. Il valore predefinito è true. |
|ID       | L'ID del piano di servizio. L'ID deve essere univoco all'interno di {: new_window} e deve essere un GUID.  |
|metadata (facoltativo)    | I metadati del piano di servizio visualizzati nel catalogo {{site.data.keyword.Bluemix_notm}} e nel listino prezzi. Il campo dei metadati è facoltativo. Nel campo metadata puoi specificare i seguenti campi: displayName, type (subscription, reservable, planDetails), bullets, costs (unitId, unit, partNumber) e paidOnly. Per ulteriori informazioni, vedi la seguente tabella per i [campi Metadati del piano](index.html#planmetadata). |

*Tabella. Campi Metadati del piano*
{: #planmetadata}

| **Valori dei metadati del piano** | **Descrizione** |
|------------------------|-----------------|
|displayName             | Il nome del piano visualizzato nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Questo nome viene visualizzato sia nel catalogo alla pagina dei dettagli del servizio che nel listino prezzi.    |
|type                    | Il tipo di piano. Per questo campo, puoi utilizzare i seguenti valori: subscription (un piano di sottoscrizione. Il valore predefinito è false), reservable (un piano riservabile. Questo valore viene utilizzato solo quando il piano è un piano di sottoscrizione, ossia, il valore di plan.metadata.subscription è true. Il valore predefinito è false), planDetails (quantità e descrizione dettagliata delle risorse che possono essere utilizzate con il piano. Questo valore viene utilizzato solo quando il piano è riservabile, ossia, il valore di  plan.metadata.reserveable è true.) |
|bullets                 | Una descrizione delle risorse che possono essere utilizzate con il piano. La descrizione viene visualizzata nella colonna **Funzioni** nella pagina dei dettagli del servizio del catalogo e nel listino prezzi. |
|costs                   | Informazioni sui costi del servizio che vengono visualizzate nella colonna Prezzo nella pagina dei dettagli del servizio del catalogo e nel listino prezzi. Ogni voce di array contiene i seguenti campi: unitId (l'ID dell'unità. Utilizza la forma plurale e scrivi in maiuscolo tutte le lettere. Per i piani gratuiti, questo campo è facoltativo), unit (la metrica utilizzata per calcolare gli addebiti del servizio. Il valore di questo campo è utilizzato nell'interfaccia utente {{site.data.keyword.Bluemix_notm}} per rappresentare la metrica di addebito) e partNumber (l'identificativo `part_number` utilizzato dal sistema di fatturazione. Per i piani gratuiti, questo campo è facoltativo).   |
|paidOnly (facoltativo)     | Un valore booleano che indica se questo piano di servizio è disponibile solo per gli account a pagamento {{site.data.keyword.Bluemix_notm}}. Il valore **true** significa che il piano di servizio è destinato solo agli account a pagamento e non può essere aggiunto agli account di prova. Il valore **false** significa che il piano di servizio può essere aggiunto sia agli account a pagamento che di prova. Il valore predefinito è **false**.	  |

Il seguente esempio mostra come la risposta JSON di GET /v2/catalog è associata alla pagina dei dettagli del servizio nel catalogo {{site.data.keyword.Bluemix_notm}}. In particolare, il modo in cui i campi dei metadati del piano descritti nella tabella precedente vengono associati all'interfaccia utente:

![Dettagli dei metadati del piano nel catalogo.](images/plan_metadata.png "Vista dei valori metadati del piano nel catalogo")


<ol>
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

### Creazione di spazi

Puoi creare degli spazi nella tua organizzazione; ad esempio,
uno spazio *dev* come un ambiente di sviluppo,
uno spazio *test* come un ambiente di test e uno
spazio *production* come un ambiente di produzione. Puoi quindi associare
le tue applicazioni agli spazi. Per creare uno spazio completa la seguente procedura:

1. Vai all'icona **{{site.data.keyword.avatar}}** ![icona Avatar](../admin/images/account_support.svg) &gt; **Gestisci organizzazioni**.
2. Seleziona l'organizzazione a cui vuoi aggiungere uno spazio.
3. Fai clic su **Crea uno spazio**.
4. Immetti un nome spazio.
5. Fai clic su **Crea**.


### Monitoraggio quota

Puoi espandere la sezione **Monitoraggio quota** per visualizzare le seguenti informazioni:

- Utilizzo della memoria dell'ambiente mostra in dettaglio l'utilizzo della memoria per l'intero ambiente di sistema. Il grafico mostra le seguenti informazioni: 
<ul>
<li>La memoria fisica in uso e il limite di memoria fisica</li>
<li>la quota di memoria riservata e il limite di memoria riservata</li>
<li>la quota totale di memoria per le tue organizzazioni</li>
</ul>
I seguenti tipi di utilizzo della memoria vengono visualizzati nel grafico.

	<dl>
	<dt><strong>Memoria fisica utilizzata</strong></dt>
	<dd>La memoria fisica utilizzata dal tuo ambiente.</dd>
	<dt><strong>Limite fisico</strong></dt>
	<dd>La memoria fisica totale disponibile nel tuo ambiente.</dd>
	<dt><strong>Quota riservata</strong></dt>
	<dd>La somma di memoria riservata per tutte le applicazioni distribuite, tra tutte le organizzazioni. La somma della quota riservata può superare il limite fisico di memoria per il tuo ambiente. Ad esempio, se hai un limite di memoria fisica pari a 16 GB, potresti riservare 4 GB di memoria ciascuna per un totale di cinque diverse applicazioni. La quota riservata supera il limite fisico della memoria.  Tuttavia, in molti casi, le applicazioni potrebbero non utilizzare la quota totale riservata singolarmente a ciascuna di esse. Inoltre, è possibile che le applicazioni non utilizzino
	contemporaneamente la quota totale della memoria riservata.</dd>
	<dt><strong>Limite riservato</strong></dt>
	<dd>La memoria totale che può essere riservata tra tutte le applicazioni per il tuo ambiente.</dd>
	<dt><strong>Quota totale</strong></dt>
	<dd>La quota di memoria totale tra tutte le organizzazioni.</dd>
	</dl>
	**Nota**: i dati vengono aggiornati automaticamente ogni 4 ore. Fai clic su **Ricalcola** se desideri aggiornare i dati sulla pagina prima dell'aggiornamento automatico. 

- Utilizzo della memoria dell'organizzazione. Questa sezione mostra in dettaglio l'utilizzo della memoria a livello di organizzazione. Puoi visualizzare la quota di memoria totale, la quota riservata e la memoria fisica utilizzata da ogni organizzazione. Il grafico fornisce informazioni che vengono elencate in base alla quantità di memoria riservata per ogni organizzazione e, per impostazione predefinita, viene elencata per prima l'organizzazione che riserva la maggiore quantità di memoria. Puoi ordinare per **Utilizzo massimo memoria** e **Assegnazione memoria in eccesso**.

	<dl>
	<dt><strong>Utilizzo massimo memoria</strong></dt>
	<dd>Usa questa opzione per identificare l'organizzazione che ha riservato la maggiore quantità di memoria.  Ordina in base all'utilizzo massimo di memoria per identificare le organizzazioni che hanno riservato la maggiore quantità di memoria. L'elenco viene ordinato in base alla quota riservata. </dd>
	<dt><strong>Assegnazione memoria in eccesso</strong></dt>
	<dd>Usa questa opzione per identificare le organizzazioni che hanno una quota di memoria totale superiore a quella necessaria. Ordina per Assegnazione memoria in eccesso per identificare le organizzazioni che utilizzano
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

Puoi aggiungere gli utenti singolarmente o in gruppi. In genere, gli utenti vengono aggiunti alla tua istanza {{site.data.keyword.Bluemix_notm}} dal registro utenti della tua azienda tramite LDAP (Lightweight Directory Access Protocol). Puoi anche visualizzare le autorizzazioni utente. Se disponi dell'autorizzazione **Superuser**, puoi anche impostare e gestire le autorizzazioni per gli altri utenti. Fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE UTENTI**.

La pagina Amministrazione utenti visualizza tutti gli utenti per l'istanza locale o dedicata. Sono visualizzate le autorizzazioni per ciascun utente utilizzando le icone nella tabella. Le autorizzazioni possono essere: Nessuna, **Superuser**, **Accesso di base**, **Catalogo**, **Report** e **Utenti**.
Le autorizzazioni **Superuser** e **Accesso di base** possono essere impostate su **Attivo** o **Disattivo**, mentre le altre autorizzazioni vengono abilitate o disabilitate con specifici tipi di accesso, tra cui l'accesso in **Lettura** o **Scrittura** per l'autorizzazione indicata, come rappresentato dalle icone. Consulta [Autorizzazioni](#permissions) per delle descrizioni di
ciascun tipo e una spiegazione delle icone.

### Gestione degli utenti

A seconda del tuo accesso di **Lettura** o **Scrittura** per le autorizzazioni dell'utente, puoi cercare utenti esistenti, rimuovere utenti e aggiungere utenti singolarmente o in base a un gruppo. Se hai l'autorizzazione **Superuser**, disponi dell'accesso completo per eseguire tutte le attività di gestione utente nell'ambiente. Esamina le seguenti attività di gestione utente e il livello di accesso necessario per completare ogni attività:

* Individua utenti. Se disponi dell'accesso in **Lettura** o **Scrittura** e conosci tutto o parte del nome utente, puoi individuare gli utenti nella tabella utilizzando il campo **Ricerca**. Puoi anche filtrare l'elenco di utenti in base alle relative organizzazioni e autorizzazioni. Per filtrare un elenco di utenti, completa la seguente procedura:
  <ol>
  <li>Fai clic su <strong>Filtro</strong>.</li>
  <li> Seleziona <strong>Organizzazioni</strong> o <strong>Autorizzazioni</strong>, a seconda del filtro che desideri utilizzare.
  <dl>
	<dt><strong>Organizzazione</strong></dt>
	<dd>Per filtrare gli utenti in base all'organizzazione, inizia a immettere il nome dell'organizzazione nel campo <strong>Organizzazione</strong> e selezionala dall'elenco. Seleziona, quindi, uno o più ruoli assegnati agli utenti all'interno dell'organizzazione.</dd>
	<dt><strong>Autorizzazioni</strong></dt>
	<dd>Per filtrare gli utenti in base alle autorizzazioni, seleziona prima il tipo di utente o utenti. Ad esempio, potresti voler visualizzare tutti i Superuser. Per le autorizzazioni diverse da <strong>Superuser</strong> o <strong>Accesso di base</strong>, puoi selezionare anche il tipo di accesso, ad esempio <strong>Lettura</strong> o <strong>Scrittura</strong>.</dd>
	</dl></li>
  <li>Fai clic su <strong>Applica</strong>.</li>
   </ol>

   La finestra Gestione utenti mostra i filtri da te impostati e gli utenti che risultano dai filtri specificati. Puoi quindi cercare un utente nella tabella filtrata. Inoltre, puoi modificare l'elenco dei filtri specificati rimuovendo un'opzione di filtro.

* Aggiungi un singolo utente. Se disponi dell'autorizzazione **Superuser** o
**Utenti** con l'accesso in **Scrittura**, puoi aggiungere gli utenti.

  1. Per aggiungere un singolo utente dalla tua directory LDAP, fai clic su **Aggiungi utente**.
  2. Nel campo **Ricerca**, immetti l'indirizzo email per l'utente e seleziona quindi l'utente dall'elenco compilato.
  3. Quindi, dal campo **Organizzazione**, scegli l'organizzazione a cui vuoi aggiungere l'utente immettendo il nome dell'organizzazione e selezionandolo dall'elenco compilato.
  4. Per aggiungere l'utente all'organizzazione selezionata, fai clic su **Aggiungi utente**.

  **Nota**: quando l'operazione di aggiunta viene eseguita con esito positivo, l'utente viene aggiunto alla tabella per consentirti operazioni di visualizzazione e ricerca. Quando gli utenti vengono aggiunti,
non dispongono di autorizzazioni.

* Aggiunta di un gruppo di utenti dalla tua directory LDAP. Se disponi dell'autorizzazione **Superuser** o
**Utenti** con l'accesso in **Scrittura**, puoi aggiungere gli utenti.

  1. Fai clic su **Aggiungi gruppo di utenti**.
  2. Nel campo **Ricerca**, immetti un nome gruppo da cercare e seleziona il nome gruppo dall'elenco compilato.
  3. Quindi, dal campo **Organizzazione**, scegli l'organizzazione a cui vuoi aggiungere il gruppo di utenti immettendo il nome dell'organizzazione e selezionandolo dall'elenco compilato.
  4. Per aggiungere il gruppo di utenti all'organizzazione selezionata, fai clic su **Aggiungi utenti**.

  **Nota**: i gruppi di più di 50 utenti vengono aggiunti tramite un lavoro batch in background. Se l'operazione di aggiunta viene
completata correttamente, l'utente o il gruppo viene aggiunto alla tabella per consentirti operazioni di visualizzazione e ricerca. Quando gli utenti vengono aggiunti,
non dispongono di autorizzazioni.

* Aggiungi un gruppo di utenti importando un foglio di calcolo che include ID utente, indirizzi email utente e l'organizzazione a cui intendi aggiungere l'utente. Se disponi dell'autorizzazione **Superuser** o **Utenti** con l'accesso in **Scrittura**, puoi aggiungere gli utenti.

**Nota**: immetti gli ID utente che corrispondono ai valori utilizzati nel tuo registro utenti.

  1. Fai clic su **Importa utenti**.
  2. Fai clic su **Scarica modello (.CSV)** per scaricare un foglio di calcolo con le colonne richieste compilabili. In alternativa puoi crearne uno personalizzato, utilizzando un foglio di calcolo che includa le intestazioni di colonna richieste: **ID utente**, **Email** e **Organizzazione**.  Il template include anche due colonne facoltative: **Nome** e **Cognome**.
  3. Compila i valori utente per le colonne obbligatorie. Se non utilizzi una directory LDAP, utilizza le intestazioni colonna obbligatorie e facoltative per gli utenti di importazione.
  4. Salva il tuo file e fai clic su **Carica file**.

  **Nota**: le colonne nel tuo foglio di calcolo possono essere in qualsiasi ordine, a condizione che tu abbia tutte le colonne obbligatorie. Se l'importazione ha avuto esito positivo, ricevi un messaggio di conferma che indica che sono stati aggiunti tutti gli utenti. Se l'importazione ha avuto esito positivo per qualche utente ma non per altri, esamina il messaggio di errore per intervenire sugli utenti che non è stato possibile aggiungere.

* Rimuovere utenti. Se disponi dell'autorizzazione **Superuser** o **Utenti** con l'accesso in **Scrittura**, puoi rimuovere gli utenti dall'ambiente in modo permanente.

    1. Individua l'utente e fai clic sull'icona ![Elimina](images/icon_trash.svg).
    2. Fai clic su **Rimuovi**.

* La modifica di autorizzazioni e organizzazioni a cui appartengono gli utenti richiede che tu disponga dell'autorizzazione  **Superuser**. Per modificare le autorizzazioni per gli utenti, individua l'utente e fai clic sul nome utente. Dalla pagina **Modifica utente**, puoi abilitare o disabilitare le autorizzazioni:

    * Seleziona **Attivo** dall'elenco per abilitare l'autorizzazione **Superuser** o **Accesso di base**.
    * Seleziona **Lettura** dall'elenco per consentire all'utente di disporre dell'accesso in **Visualizzazione** (sola lettura) per tale autorizzazione oppure seleziona **Scrittura** per consentire l'accesso in **Scrittura** (modifica o aggiunta e rimozione) per tale autorizzazione.
    * Seleziona **Disattivo** per disabilitare tutte le autorizzazioni.

    **Nota**: l'impostazione dell'autorizzazione **Superuser** su **Attivo** imposta tutte le altre autorizzazioni con l'accesso in **Scrittura**.

* Per aggiungere o rimuovere un utente da una specifica organizzazione, devi disporre dell'autorizzazione **Superuser** o **Utenti** con l'accesso in **Scrittura**.

    1. Per aggiungere un utente a un'organizzazione, seleziona il nome utente dalla tabella per accedere alla pagina **Modifica utente**. Utilizza quindi il campo di ricerca per individuare un'organizzazione, seleziona l'organizzazione dall'elenco e fai clic su **Salva**.
    2. Per rimuovere un utente da un'organizzazione, seleziona il nome utente dalla tabella per accedere alla pagina **Modifica utente**. Fai quindi clic su ![Rimuovi](images/icon_remove.svg) per l'organizzazione da cui vuoi rimuovere l'utente e fai clic su **Salva**.

### Autorizzazioni
{: #permissions}

È possibile assegnare agli utenti le seguenti autorizzazioni con livelli di accesso specifici (lettura o scrittura) che consentono all'utente di completare attività specifiche all'interno della console di gestione.

*Tabella 7. Autorizzazioni*

| **Autorizzazione utente** | **Descrizione** |       
|-----------------|-------------------|
| Superuser | Gli utenti con l'autorizzazione **Superuser** impostata su **Attivo** possono modificare le autorizzazioni per gli altri utenti. Se hai l'autorizzazione attiva, ti viene automaticamente abilitato l'accesso completo alle altre autorizzazioni. Oltre alle attività descritte per ogni autorizzazione nella tabella, questi utenti possono anche impostare la sottoscrizione di eventi per avvertirti direttamente sulla manutenzione o gli incidenti, pianificare la manutenzione, eseguire i controlli di verifica sui componenti della console e creare organizzazioni e spazi per l'ambiente. Questa autorizzazione equivale al ruolo di amministratore (admin) per la console di gestione.   |
| Accesso di base | Gli utenti con l'autorizzazione **Accesso di base** impostata su **Attivo** possono visualizzare l'opzione della pagina di amministrazione nell'interfaccia utente  {{site.data.keyword.Bluemix_notm}}. Gli utenti con l'autorizzazione abilitata possono avere accesso alle [Informazioni di sistema](#oc_system) e ai tile [Utilizzo della risorsa](#oc_resource). Senza questa autorizzazione, gli utenti non possono visualizzare o accedere all'opzione di menu Amministrazione. Questa autorizzazione equivale al ruolo di amministratore (admin) per la console di gestione. Equivale all'autorizzazione di accesso utilizzata precedentemente per la console di gestione. |
| Catalogo | Agli utenti con autorizzazione **Catalogo** può essere assegnato l'accesso in **Lettura** o in **Scrittura** (modifica) per i servizi disponibili nell'istanza locale o dedicata. L'accesso in lettura consente all'utente di accedere al tile di gestione del catalogo per visualizzare i servizi disponibili. L'accesso in scrittura consente all'utente di accedere al tile [Gestione catalogo](#oc_catalog) per visualizzare i servizi, modificare la visibilità dei servizi, registrare i servizi personalizzati e controllare l'elenco di priorità del pacchetto di build. |  
| Report | Agli utenti con autorizzazione **Report** può essere assegnato l'accesso in **Lettura** o in **Scrittura** (modifica) per i report di sicurezza. L'accesso in lettura consente all'utente di accedere al tile Report e log per scaricare i report. L'accesso in scrittura consente agli utenti di visualizzare il tile [Report e log](#oc_report) così come di utilizzare la CLI per caricare nuovi report e creare nuove categorie per l'accesso degli utenti. |
| Utenti | Agli utenti con autorizzazione **Utenti** può essere assegnato l'accesso in  **Lettura ** (visualizzazione) per l'elenco di utenti o in **Scrittura** (aggiunta o rimozione) per gli utenti. Questa autorizzazione non ti consente di impostare le autorizzazioni per gli altri utenti. L'accesso in scrittura consente all'utente di aggiungere nuovi utenti all'ambiente, eliminare utenti dall'ambiente e aggiungere utenti esistenti all'organizzazione che già esistono nell'ambiente. In aggiunta, l'accesso in **Scrittura** consente agli utenti di aggiungere nuove organizzazioni, eliminare le organizzazioni e modificare gli utenti nelle organizzazioni. |


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
devi eseguire l'accesso alla Console di gestione. Se disponi dell'autorizzazione **Superuser** o **Utenti**
con l'accesso in **Scrittura**, puoi aggiungere o rimuovere gli utenti. Per modificare le autorizzazioni di altri utenti devi disporre
dell'autorizzazione **Superuser**.

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
        "familyName": "*last_name*",
        "givenName": "*first_name*"
    }
}
```
{: screen}

### Elenco delle organizzazioni
{: #listingorg}

Quando aggiungi un utente, devi specificare un'organizzazione. Puoi
utilizzare la API REST `Admin` per elencare tutte le organizzazioni. Devi disporre dell'autorizzazione
**Utenti** con l'accesso in **Lettura** per elencare
le organizzazioni. Per elencare tutte le organizzazioni, esegui questo comando:

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
l'API REST `Admin` per elencare gli utenti registrati. Devi disporre dell'autorizzazione
**Utenti** con l'accesso in **Lettura** per elencare gli
utenti registrati. Per elencare tutti gli utenti, esegui questo comando:

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

Puoi utilizzare l'API REST `Admin` per aggiungere utenti all'istanza {{site.data.keyword.Bluemix_notm}}. Devi
disporre dell'autorizzazione **Utenti** con l'accesso in **Scrittura** per aggiungere
gli utenti o l'autorizzazione **Superuser** (ops.admin) per la console di gestione. Inoltre, in qualità di Ammin, puoi consentire ai membri dell'organizzazione che non hanno le autorizzazioni `utente` o `superuser` generali della console di gestione, la possibilità di aggiungere nuovi utenti solo alle loro organizzazioni. Utilizza il seguente comando API per questa specifica capacità per i gestori organizzazione:

```
PUT console.<subdomain>.bluemix.net/codi/env_config/allow_managers?flag=<TRUE or FALSE>
```
{: screen}

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

Puoi utilizzare l'API REST `Admin` per rimuovere gli utenti dall'istanza {{site.data.keyword.Bluemix_notm}}. Per rimuovere
gli utenti, devi disporre dell'autorizzazione **Utenti** con l'accesso in **Scrittura**.

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

| **Nome** | **Descrizione** |
|-----------------|-------------------|
| name | Nome del broker dei servizi. |
| auth_username | Nome utente utilizzato per connettersi al broker dei servizi. |
| auth_password | Password utilizzata per connettersi al broker dei servizi. |
| broker_url | URL utilizzato per connettersi al broker dei servizi. |
| owningOrganization | Organizzazione iniziale per cui aggiungere il servizio nell'elenco elementi consentiti. |

*Tabella 8. Campi*

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

| **Nome** | **Descrizione** |
|-----------------|-------------------|
| name | Nome del broker dei servizi. Questo nome non può essere modificato dal nome con cui è stato creato il servizio. |
| auth_username | Nome utente utilizzato per connettersi al broker dei servizi. |
| auth_password | Password utilizzata per connettersi al broker dei servizi. |
| broker_url | URL utilizzato per connettersi al broker dei servizi. |
| owningOrganization | Organizzazione iniziale per cui aggiungere il servizio nell'elenco elementi consentiti. |

*Tabella 9. Campi*

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

| **Nome** | **Descrizione** |
|-----------------|-------------------|
| name | Nome del broker dei servizi. Questo nome non può essere modificato dal nome con cui è stato creato il servizio. |

*Tabella 10. Parametro*

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
