---


copyright:
  years: 2015, 2017
lastupdated: "2017-04-18"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Gestione di {{site.data.keyword.Bluemix_notm}} locale e {{site.data.keyword.Bluemix_notm}} dedicato
{: #mng}

Se disponi dell'accesso come amministratore per {{site.data.keyword.Bluemix}} locale o {{site.data.keyword.Bluemix_notm}} dedicato, vai alla pagina **Amministrazione** per gestire risorse, monitorare l'utilizzo delle quote, amministrare le autorizzazioni utente, pianificare le notifiche di aggiornamento, visualizzare log e report di sicurezza e altro. Puoi gestire le tue organizzazioni creando degli spazi e impostando dei [ruoli e delle autorizzazioni per gli utenti](/docs/admin/index.html#oc_useradmin); vedi [Gestione delle tue organizzazioni](/docs/admin/orgs_spaces.html).
{:shortdesc}

{: #ld_table1}

| Quali operazioni posso eseguire? | Dettagli |    
|----------------|---------|
|Monitorare l'utilizzo del sistema | Fai clic su **AMMINISTRAZIONE &gt; UTILIZZO**. Visualizza le informazioni sul sistema, monitora l'utilizzo della CPU e pianifica l'utilizzo per ottimizzare il processo decisionale per la tua azienda. Vedi [Visualizzazione delle informazioni sull'utilizzo](/docs/admin/index.html#oc_resource).|
|Gestire il tuo catalogo | Fai clic su **AMMINISTRAZIONE &gt; GESTIONE CATALOGO** per stabilire quali servizi sono visibili ai tuoi utenti e organizzazioni. Vedi [Gestione del tuo catalogo](/docs/admin/index.html#oc_catalog).|
|Amministrare le organizzazioni | Fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE ORGANIZZAZIONE** per creare organizzazioni, monitorare le quote per le organizzazioni e prendere decisioni rapide basate sulle esigenze. Vedi [Amministrazione delle organizzazioni](/docs/admin/index.html#oc_organizations).|
|Creare spazi e assegnare i ruoli utente | Fai clic su **Account** &gt; **Gestisci organizzazioni** per creare gli spazi tra le tue organizzazioni. Aggiungi utenti e assegna loro dei ruoli per l'organizzazione e lo spazio. Vedi [Gestione delle tue organizzazioni](/docs/admin/orgs_spaces.html). |
|Gestire le autorizzazioni degli utenti amministrativi | Fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE UTENTI** per aggiungere e rimuovere utenti e modifica le autorizzazioni utente. Vedi [Gestione di utenti e autorizzazioni](/docs/admin/index.html#oc_useradmin). |
|Esaminare report e log | Fai clic su **AMMINISTRAZIONE &gt; REPORT E LOG** per visualizzare i report di sicurezza e i log di controllo relativi alla tua istanza. Vedi [Visualizzazione dei report](/docs/admin/index.html#oc_report). |
|Visualizzare le informazioni sul sistema. | Fai clic su **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA** per visualizzare le informazioni di sistema, quali aggiornamenti di manutenzione in sospeso, nome e versione della tua istanza, regione, URL API, URL CLI, dettagli di configurazione LDAP, associazioni di gruppi e utenti, statistiche e domini condivisi. Vedi [Visualizzazione delle informazioni sul sistema](/docs/admin/index.html#oc_system). |
|Estendere le notifiche e impostare le sottoscrizioni notifica | Fai clic su **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA &gt; *Numero* in sospeso**. Puoi utilizzare webhook da integrare con un servizio Web a scelta per impostare una sottoscrizione di notifica evento per un aggiornamento o incidente. Vedi [Notifiche e sottoscrizioni di notifica](/docs/admin/index.html#oc_eventsubscription). |
{: caption="Tabella 1. Attività amministrative per la gestione della tua istanza Bluemix locale o dedicata" caption-side="top"}

<!-- staging only for WoW start -->

**Suggerimento**: il dashboard Infrastruttura nella console {{site.data.keyword.Bluemix_notm}} è disponibile solo per gli account collegati negli ambienti di {{site.data.keyword.Bluemix_notm}} pubblico.


<!-- staging only for WoW end -->


## Notifiche e sottoscrizioni di notifica
{: #oc_eventsubscription}

Puoi sempre conoscere lo stato del tuo ambiente consultando la pagina Stato. Non appena si verificano, gli incidenti e gli eventi di aggiornamento della manutenzione pianificata con interruzioni del servizio vengono segnalati nella pagina Stato. {{site.data.keyword.Bluemix_notm}} invia inoltre alla pagina Amministrazione dell'area Notifiche le eventuali notifiche riguardanti eventi quali aggiornamenti di manutenzione pianificati o in sospeso.

### Notifiche

Puoi visualizzare le notifiche riguardanti il tuo ambiente locale o dedicato, al fine di monitorare lo stato del tuo ambiente. Consulta la seguente tabella per informazioni sui diversi tipi di notifiche e sui rispettivi punti di pubblicazione.

{: #ld_table2}

| **Tipo di evento** | **Metodo di notifica** |       
|-----------------|-------------------|
| Aggiornamenti di manutenzione | Per visualizzare uno storico e un elenco completo delle tue notifiche complete e in sospeso, fai clic su **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA** &gt; *Numero* **in sospeso**. Ricevi anche un avviso degli eventi di aggiornamento della manutenzione pianificata con interruzioni del servizio nella pagina Stato. Fai clic su **Supporto** &gt; **Stato**. Puoi estendere la funzionalità di notifica impostando una sottoscrizione che invia un'e-mail a destinatari di tua scelta. In alternativa, puoi impostare una sottoscrizione che utilizza dei webhook per integrare le notifiche provenienti dalla pagina Amministrazione con un servizio Web a scelta.|
| Incidenti critici | Vieni avvisato degli incidenti critici sulla pagina Stato. Fai clic su **Supporto** &gt; **Stato**. Puoi estendere la funzionalità di notifica impostando una sottoscrizione di notifica che invia un'e-mail a un destinatario di tua scelta. In alternativa, puoi impostare una sottoscrizione che utilizza dei webhook per integrare le notifiche provenienti dalla pagina Amministrazione con un servizio Web a scelta.  |  
| Eventi di soglia | Puoi impostare una sottoscrizione di notifica che invia un'e-mail a un destinatario di tua scelta quando nel tuo ambiente vengono raggiunte le soglie per la quota dell'organizzazione, il disco fisico, la memoria fisica o la memoria riservata. In alternativa, puoi impostare una sottoscrizione che utilizza dei webhook per integrare le notifiche con un servizio Web di tua scelta.  |  
| Stato di {{site.data.keyword.Bluemix_notm}} | In qualsiasi momento puoi visualizzare l'ultimo stato della piattaforma, dei servizi e della tua istanza {{site.data.keyword.Bluemix_notm}} nella pagina Stato. Fai clic su **Supporto** &gt; **Stato**.  |
{: caption="Tabella 2. Tipi di evento e metodi di notifica" caption-side="top"}

### Impostazione di sottoscrizioni di notifica
{: #seteventsub}

Puoi estendere la funzionalità delle notifiche inviate alla pagina Amministrazione e alla pagina Stato, utilizzando le sottoscrizioni di notifica. Utilizza le sottoscrizioni di notifica per configurare un'e-mail personalizzata o utilizzare dei webhook da integrare con uno strumento a scelta.
 * Se selezioni l'opzione e-mail, le notifiche vengono inviate agli indirizzi e-mail da te specificati. Puoi selezionare le notifiche di incidenti, aggiornamenti di manutenzione o soglie. Viene inviata una notifica e-mail iniziale. Successivamente, ogni volta che l'evento subisce delle modifiche, viene inviata un'altra notifica con la modifica apportata.  
 * Se selezioni l'opzione webhook, le tue notifiche vengono indirizzate direttamente a una destinazione a scelta, ad esempio un numero di telefono (tramite messaggio SMS). Puoi personalizzare il tipo di notifica, in particolare gli aggiornamenti di manutenzione, gli avvisi di incidenti critici e le soglie. Puoi scegliere se ricevere nuove notifiche oppure notifiche sulle modifiche apportate alle sottoscrizioni e puoi indicare quali informazioni includere nel corpo di ogni notifica.

**Nota**: solo gli utenti con autorizzazione Superuser (`ops.admin`) possono impostare le sottoscrizioni di notifica.

Per creare una sottoscrizione webhook o e-mail dalla pagina **Sottoscrizioni di notifica**, completa la seguente procedura:

1. Passa alla pagina **Sottoscrizioni di notifica**.  Vai a **INFORMAZIONI DI SISTEMA&gt; Ambiente &gt; Sottoscrizioni**.
2. Fai clic su **Aggiungi sottoscrizione**.
3. Completa il modulo di sottoscrizione di notifica.

  * Per creare sottoscrizioni di notifica e-mail per gli aggiornamenti di manutenzione o gli incidenti, vedi le informazioni nella [Tabella 3](index.html#emailnotmaintinc).
  * Per creare sottoscrizioni di notifica e-mail per le soglie, vedi le informazioni nella [Tabella 4](index.html#emailnottrhesh).
  * Per creare sottoscrizioni di notifica webhook per gli aggiornamenti di manutenzione o gli incidenti, vedi le informazioni nella [Tabella 5](index.html#webhooknotsub).
  * Per creare sottoscrizioni di notifica webhook per le soglie, vedi le informazioni nella [Tabella 6](index.html#webhooknotthresh).

4. Una volta completato il modulo, puoi scegliere tra le seguenti opzioni:

  * Fai clic su **Salva** per salvare la sottoscrizione nel tuo elenco di sottoscrizioni di notifica.
  * Fare clic su **Salva e verifica** per salvare e verificare la notifica.
  * Fai clic su **Salva e chiudi** per salvare la sottoscrizione nel tuo elenco di sottoscrizioni di notifica e tornare alla pagina precedente.

{: #emailnotmaintinc}

| **Campo** | **Descrizione** |
|-----------------|-------------------|
| Abilitato | Seleziona questa opzione per abilitare le notifiche e-mail. Deselezionare l'opzione per disabilitare la notifica e-mail. Le sottoscrizioni sono abilitate per impostazione predefinita. |
| Tipo | Seleziona **E-mail**. |
| Evento | Seleziona l'opzione per sottoscrivere le notifiche di un evento di **Manutenzione** o **Incidente**. |
| Combina notifiche | Seleziona l'opzione per combinare le notifiche di incidente di tutte le regioni in una singola notifica. Questa opzione è disponibile solo per gli incidenti. |
| Oggetto | Compila la riga oggetto dell'e-mail. Questo campo è obbligatorio.  |
| Corpo | Immetti il testo del corpo del messaggio da inviare nell'e-mail. Puoi utilizzare i valori payload IBM per inserire nella notifica e-mail informazioni pertinenti. Vedi la tabella [Valori della sezione di payload di manutenzione e incidenti](index.html#payload) per identificare i valori utilizzabili. Utilizza tag HTML di base per strutturare l'e-mail. Questo campo è obbligatorio. |
| A: | Immetti uno o più indirizzi e-mail tramite elenco separato da virgole per indicare i destinatari della notifica e-mail. Espandi le opzioni "cc" o "bcc" per inviare copia dell'e-mail ad altri destinatari. Questo campo è obbligatorio. |
| Descrizione | Aggiungi una descrizione univoca della sottoscrizione e stai creando. |
{: caption="Tabella 3. Campi per sottoscrizioni di notifica e-mail per le soglie" caption-side="top"}


{: #emailnottrhesh}

| **Campo** | **Descrizione** |
|-----------------|-------------------|
| Abilitato | Seleziona questa opzione per abilitare le notifiche e-mail. Deselezionare l'opzione per disabilitare la notifica e-mail. Le sottoscrizioni sono abilitate per impostazione predefinita. |
| Tipo | Seleziona **E-mail**. |
| Evento | Seleziona **Soglia**. |
| Soglia | Seleziona il tipo di soglia per cui ricevere una notifica: Quota organizzazione, Disco fisico, Memoria fisica, Disco riservato o Memoria riservata. |
| Direzione soglia | Seleziona la direzione in cui spostare i dati, in ordine crescente o decrescente, quando si supera il valore Notifica quando incrociato che hai impostato. Ad esempio, se il valore di Notifica quando incrociato è 50%,  e la direzione è decrescente, riceverai una notifica solo se la percentuale di utilizzo va da più di 50%  a meno di 50%.  Se imposti la direzione su Crescente, riceverai una notifica quando la percentuale di utilizzo va da meno di 50% a più di 50%.   |
| Notifica quando incrociato superiore a (%) | Immetti la percentuale di soglia per cui ricevere una notifica. Se nel campo Direzione soglia hai scelto la proprietà Crescente, la notifica e-mail viene inviata quando la soglia supera questa percentuale. |
| Notifica quando incrociato inferiore a (%) | Immetti la percentuale di soglia per cui ricevere una notifica. Se nel campo Direzione soglia hai scelto la proprietà Decrescente, la notifica e-mail viene inviata quando la soglia scende sotto questa percentuale. |
| Descrizione | Aggiungi una descrizione univoca della sottoscrizione e stai creando. |
| Oggetto | Compila la riga oggetto dell'e-mail. Questo campo è obbligatorio.  |
| Corpo del messaggio | Immetti il testo del corpo del messaggio da inviare nell'e-mail. Puoi utilizzare i valori payload IBM per inserire nella notifica e-mail informazioni pertinenti. Vedi la tabella [Valori della sezione di payload di soglia](index.html#threshpayload) per identificare i valori utilizzabili. Utilizza tag HTML di base per strutturare l'e-mail. Questo campo è obbligatorio. |
| A: | Immetti uno o più indirizzi e-mail tramite elenco separato da virgole per indicare i destinatari della notifica e-mail. Espandi le opzioni "cc" o "bcc" per inviare copia dell'e-mail ad altri destinatari. Questo campo è obbligatorio. |
{: caption="Tabella 4. Campi per sottoscrizioni di notifica e-mail per gli aggiornamenti di manutenzione o gli incidenti" caption-side="top"}

I dati della soglia vengono raccolti una volta ogni 6 ore. Una notifica viene inviata solo una volta quando il valore supera il valore soglia impostato. Se hai scelto la proprietà crescente, non viene inviata una nuova notifica a meno che il valore non scenda sotto la soglia e quindi la oltrepassi nuovamente. Allo stesso modo, se hai scelto la proprietà decrescente, ricevi una notifica solo se il valore supera la soglia impostata e quindi scende di nuovo sotto la soglia. 

Se non vuoi aspettare 6 ore per ricevere la notifica sul raggiungimento della soglia, dopo aver completato i campi nel modulo, puoi fare clic su **Salva e verifica** per ricevere una notifica di verifica con i dati di esempio.  

Una notifica per la soglia della Quota organizzazione include solo le organizzazioni che hanno superato la percentuale di soglia specificata nel periodo di tempo di 6 ore corrispondente a tale notifica. Le organizzazioni che hanno superato una soglia durante intervalli di 6 ore precedenti non verranno incluse, anche se rimangono sopra o sotto la soglia.  Le tre risorse che compongono la quota di un'organizzazione (memoria riservata, servizi e rotte) vengono considerate separatamente quando si deve valutare se inviare una notifica sulla quota. Ad esempio, se la quantità di memoria riservata utilizzata da un'organizzazione supera il 50% della quota, una soglia della Quota organizzazione configurata con un valore di 50% comporterà l'invio di una notifica.  Se il numero di servizi utilizzati dalla stessa organizzazione supera successivamente il 50% della quota, anche se la quantità di memoria utilizzata rimane invariata, la stessa sottoscrizione di soglia della Quota dell'organizzazione comporterà anch'essa l'invio di una notifica.

{: #webhooknotsub}

| **Campo** | **Descrizione** |
|-----------------|-------------------|
| Abilitato | Seleziona l'opzione per abilitare la notifica. Deselezionare l'opzione per disabilitare la notifica. Le sottoscrizioni sono abilitate per impostazione predefinita. |
| Tipo | Seleziona **Webhook** |
| Evento | Seleziona l'opzione per sottoscrivere le notifiche di un evento di **Manutenzione** o **Incidente**. |
| Autorizzazione | Scegli se abilitare l'autorizzazione.  Le opzioni sono: **Di base** o **Nessuna**. |
| Nome utente | Se hai scelto l'autorizzazione **Di base**, immetti il tuo nome utente per il servizio Web. Se non desideri utilizzare le tue credenziali personali, puoi impostare un ID funzionale da utilizzare specificatamente con {{site.data.keyword.Bluemix_notm}}. |
| Password | Se hai scelto l'autorizzazione **Di base**, immetti la tua password per il servizio Web. |
| Descrizione | Aggiungi una descrizione univoca della sottoscrizione e stai creando. |
| Nuovo evento | Seleziona questa opzione per abilitare la notifica per i nuovi eventi di manutenzione o incidente. Deselezionare l'opzione per disabilitare la notifica. |
| Metodo | Seleziona **GET**, **POST** o **PUT**. |
| URL | Immetti l'URL per la connessione al tuo servizio Web. |
| Proprietà di risposta | Questo campo facoltativo è il nome della proprietà che identifica la risorsa creata dal tuo servizio Web quando viene inviata una richiesta POST o PUT. Se fornisci una proprietà di risposta per un nuovo evento e scegli di creare una sottoscrizione per le modifiche a un evento, dovrai fornirla anche per la sottoscrizione Modifica all'evento. A seconda del servizio Web utilizzato, puoi specificarla come parte dell'URL o come valore di payload.  |
| Payload | Se hai selezionato il metodo POST o PUT, immetti le proprietà specifiche del servizio Web che stai utilizzando insieme i valori di payload utilizzati per la notifica IBM. Vedi la tabella [Valori della sezione di payload di manutenzione e incidenti](index.html#payload) per identificare i valori utilizzabili. Se non immetti informazioni in questa sezione, ricevi una notifica che non contiene informazioni aggiuntive. |
| Modifica all'evento | Seleziona questa opzione per creare sottoscrizioni di notifica relative alle modifiche agli eventi di manutenzione o incidenti per cui hai creato le sottoscrizioni. Deselezionare l'opzione per disabilitare la notifica. |
| Utilizza valori e payload da Nuovo evento | Usa il contenuto del campi Metodo, URL e Payload della sezione Nuovo evento. Nota che se l'opzione è selezionata, questi campi non sono disponibili per ulteriori modifiche nella sezione Modifica all'evento. |
| Metodo | Seleziona **GET**, **POST** o **PUT**. |
| URL | Immetti l'URL per la connessione al tuo servizio Web. |
| Payload | Se hai selezionato il metodo POST o PUT, immetti le proprietà specifiche del servizio Web che stai utilizzando insieme i valori di payload utilizzati per la notifica IBM. Vedi la tabella [Valori della sezione di payload di manutenzione e incidenti](index.html#payload) per identificare i valori utilizzabili. Se non immetti informazioni in questa sezione, ricevi una notifica che non contiene informazioni aggiuntive. |
| Combina notifiche | Seleziona l'opzione per combinare le notifiche di incidente di tutte le regioni in una singola notifica. Questa opzione è disponibile solo per gli incidenti. |
{: caption="Tabella 5. Campi del modulo per una sottoscrizione di notifica webhook per la manutenzione o gli incidenti" caption-side="top"}


{: #webhooknotthresh}

| **Campo** | **Descrizione** |
|-----------------|-------------------|
| Abilitato | Seleziona l'opzione per abilitare la notifica. Deselezionare l'opzione per disabilitare la notifica. Le sottoscrizioni sono abilitate per impostazione predefinita. |
| Tipo | Seleziona **Webhook**. |
| Evento | Seleziona **Soglia**. |
| Soglia | Seleziona il tipo di soglia per cui ricevere una notifica: Quota organizzazione, Disco fisico, Memoria fisica, Disco riservato o Memoria riservata.|
| Direzione soglia | Scegli se visualizzare i dati di soglia in ordine crescente o decrescente.  |
| Notifica quando incrociato inferiore a (%) | Se hai selezionato la **Direzione di soglia** **Decrescente**, immetti la percentuale di soglia per cui ricevere una notifica. Quando la soglia scende sotto questa percentuale, viene inviata una notifica webhook. |
| Notifica quando incrociato superiore a (%) | Se hai selezionato la **Direzione di soglia** **Crescente**, immetti la percentuale di soglia per cui ricevere una notifica. Quando la soglia supera questa percentuale, viene inviata una notifica webhook. |
| Descrizione | Aggiungi una descrizione univoca della sottoscrizione e stai creando. |
| Autorizzazione | Scegli se abilitare l'autorizzazione.  Le opzioni sono: **Di base** o **Nessuna**. |
| Nome utente | Se hai scelto l'autorizzazione di base, immetti il tuo nome utente per il servizio Web. Se non desideri utilizzare le tue credenziali personali, puoi impostare un ID funzionale da utilizzare specificatamente con {{site.data.keyword.Bluemix_notm}}. |
| Password | Se hai scelto l'autorizzazione di base, immetti la tua password per il servizio Web. |
| Metodo | Seleziona **GET**, **POST** o **PUT**. |
| URL | Immetti l'URL per la connessione al tuo servizio Web. |
{: caption="Tabella 6. Campi del modulo per una sottoscrizione di notifica webhook per le soglie" caption-side="top"}

I dati della soglia vengono raccolti una volta ogni 6 ore. Una notifica viene inviata solo una volta quando il valore supera il valore soglia impostato. Non viene inviata una nuova notifica a meno che il valore non vada al di sotto della soglia (se hai scelto la proprietà crescente) e quindi la risuperi nuovamente. Allo stesso modo, se hai scelto la proprietà decrescente, ricevi una nuova una notifica se il valore supera la soglia impostata e quindi scende di nuovo sotto la soglia. 

Se non vuoi aspettare 6 ore per ricevere la notifica sul raggiungimento della soglia, dopo aver completato i campi nel modulo, puoi fare clic su **Salva e verifica** per salvare e verificare la notifica con i dati di esempio.

Una notifica per la soglia della Quota organizzazione include solo le organizzazioni che hanno superato la percentuale di soglia specificata nel periodo di tempo di 6 ore corrispondente a tale notifica. Le organizzazioni che hanno superato una soglia durante intervalli di 6 ore precedenti non verranno incluse, anche se rimangono sopra o sotto la soglia.  Le tre risorse che compongono la quota di un'organizzazione, ossia memoria riservata, servizi e rotte, vengono considerate separatamente quando si deve valutare se inviare una notifica sulla quota. Ad esempio, se la quantità di memoria riservata utilizzata da un'organizzazione supera il 50% della quota, una soglia della Quota organizzazione configurata con un valore di 50% comporterà l'invio di una notifica.  Se il numero di servizi utilizzati dalla stessa organizzazione supera successivamente il 50% della quota, anche se la quantità di memoria utilizzata rimane invariata, la stessa sottoscrizione di soglia della Quota dell'organizzazione comporterà anch'essa l'invio di una notifica.

{: #payload}

| **Valore IBM** | **Descrizione** | **Tipo di evento** |
|----------------|----------------|------------------------|
| {{content.category}} | Servizi interessati | Incidente |
| {{content.disruption}} | Componenti interessati | Aggiornamento di manutenzione |
| {{content.message}} | Descrizione del messaggio |   Aggiornamento di manutenzione e incidente |
| {{content.scheduleWindow.start}} | Data di inizio pianificata per l'aggiornamento | Aggiornamento di manutenzione |
| {{content.scheduleWindow.end}} | Ora di fine pianificata per l'aggiornamento | Aggiornamento di manutenzione |
| {{content.severity}} | Classificazione della severità | Incidente |
| {{content.subCategoryName}} | Componenti interessati | Incidente |
| {{content.title}} | Titolo del messaggio | Aggiornamento di manutenzione e incidente |
| {{region}} | Regione interessata | Aggiornamento di manutenzione e incidente |
| {{status}} | Stato dell'aggiornamento | Aggiornamento di manutenzione |
| {{type}} | Aggiornamento o incidente | Aggiornamento di manutenzione e incidente |
{: caption="Tabella 7. Valori della sezione di payload di manutenzione e incidenti" caption-side="top"}


{: #threshpayload}

| **Valore IBM** | **Descrizione** | **Tipo di evento** |
|----------------|----------------|------------------------|
| {{content.org_quota}} | Soglia quota organizzazione | Soglia |
| {{content.physical_disk}} | Soglia disco fisico | Soglia |
| {{content.physical_memory}} | Soglia memoria fisica | Soglia |  
| {{content.reserved_disk}} | Soglia disco riservato | Soglia |
| {{content.reserved_memory}} | Soglia memoria riservata | Soglia |
{: caption="Tabella 8. Valori della sezione di payload della soglia" caption-side="top"}

Quando salvi la tua sottoscrizione di notifica, ricevi notifiche attraverso il metodo che hai impostato. Le notifiche vengono ancora pubblicate nelle seguenti posizioni:  
 * Nella pagina Stato per gli incidenti
 * Nella pagina Stato per gli eventi di aggiornamento della manutenzione pianificata con interruzioni del servizio
 * Nell'area Notifica della pagina Amministrazione per gli aggiornamenti di manutenzione

Puoi selezionare qualsiasi sottoscrizione di notifica salvata, visualizzare le attività recenti o modificarle come necessario. Fai clic per espandere qualsiasi voce delle attività recenti per visualizzare i dettagli della cronologia.

## Aggiornamenti di manutenzione
{: #oc_schedulemaintenance}

Puoi visualizzare gli aggiornamenti di manutenzione pianificata e in sospeso solo se disponi dell'autorizzazione superuser (`ops.admin`), facendo clic su **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA &gt; *Numero* in sospeso** per accedere alla pagina **Aggiornamenti di sistema**.  Tutti gli utenti del tuo ambiente possono visualizzare gli eventi di aggiornamento della manutenzione pianificata con interruzioni del servizio facendo clic su **Supporto** &gt; **Stato**.

**Nota**: consultare la seguente sezione per [Impostazione di finestre di manutenzione preapprovate](index.html#preapprovedmaintenance). Queste finestre devono essere impostate per consentire a IBM di pianificare la manutenzione per il tuo ambiente.

<dl>
<dt>Aggiornamenti che non comportano interruzioni del servizio</dt>
<dd>Un aggiornamento che non comporta interruzioni del servizio non influenza il tuo ambiente, le tue applicazioni in esecuzione o l'accesso dei tuoi utenti alle tue applicazioni. Questo tipo di aggiornamento non richiede un'approvazione caso per caso e verrà applicato durante le finestre di manutenzione disponibili preapprovate da te impostate dalla pagina Aggiornamenti di sistema.</dd>
<dt>Aggiornamenti che comportano interruzioni del servizio</dt>
<dd>Un aggiornamento che comporta interruzioni del servizio può influenzare il tuo ambiente, le applicazioni in esecuzione o l'accesso dei tuoi utenti alle tue applicazioni. Devi pianificare e approvare ciascuno di questi aggiornamenti di manutenzione entro la finestra di manutenzione di 21 giorni assegnata. Puoi selezionare l'ora e la data di distribuzione suggerita, l'opzione per qualsiasi finestra preapprovata da te oppure aprire il calendario per selezionare tre date/ore specifiche tra cui IBM può scegliere durante la pianificazione dell'aggiornamento.</dd>
</dl>


### Impostazione delle finestre di manutenzione preapprovate
{: #preapprovedmaintenance}

Gli aggiornamenti di manutenzione che non comportano interruzioni del servizio sono pianificati per essere eseguiti durante finestre temporali preapprovate. Per impostazione predefinita, vengono create due finestre di aggiornamenti disponibili settimanali per il tuo sistema. Queste finestre sono in genere impostate per ripetersi ogni sabato e domenica sera. Puoi modificare le impostazioni predefinite in uno dei seguenti modi:
 * Modifica le finestre di aggiornamento predefinite scegliendo un giorno e/o un'ora di inizio differenti.
 * Crea una finestra di aggiornamento e quindi elimina la finestra predefinita

Per salvare le modifiche, devi comunque rispettare il periodo di tempo minimo richiesto per ogni settimana.

Devi impostare un minimo di 12 ore disponibili in una settimana per un periodo minimo di due giorni per ogni settimana. Ad esempio, puoi impostare finestre temporali di sei ore in due giorni distinti o puoi impostare finestre di quattro ore in tre giorni diversi. Per accertarti che le finestre temporali siano sufficienti per consentire l'applicazione di un aggiornamento, la durata minima di ciascuna finestra deve essere pari a 4 ore.  

**Nota**: solo gli utenti con autorizzazione Superuser (`ops.admin`) possono pianificare e approvare gli aggiornamenti di manutenzione.

1. Vai a **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA &gt; *Numero* in sospeso &gt; Gestisci disponibilità**.
2. Espandi la sezione **Gestisci finestre di aggiornamento disponibili**.
3. Fai clic su **Aggiungi nuovo** ![Aggiungi nuovo](images/add-new.png).
4. Imposta la prima finestra di disponibilità selezionando la frequenza, la durata e l'ora di inizio per la finestra.
5. Facoltativo: seleziona **Contrassegna come preferito**, se vuoi impostare la tua finestra di disponibilità ricorrente come orario preferito per le distribuzioni da pianificare. Le finestre temporali preferiti avranno la priorità, laddove possibile.
6. Fai clic su **Inoltra**.
7. Ripeti questo processo finché non hai soddisfatto i requisiti minimi per le finestre temporali settimanali.

### Impostazione delle finestre di manutenzione non disponibili
{: #blockpreapprovedmaintenance}

Puoi scegliere di impostare specifiche finestre di aggiornamento non disponibili in cui il tuo ambiente non sarà disponibile per gli aggiornamenti di manutenzione che non comportano interruzioni del servizio. Ad esempio, puoi scegliere un fine settimana o una vacanza ad alto traffico in cui non applicare alcuna manutenzione per garantire che le tue applicazioni siano disponibili ai tuoi utenti.

Devi impostare un minimo di 12 ore disponibili in una settimana per un periodo minimo di due giorni per ogni settimana. Se tenti di creare una finestra di aggiornamento non disponibile, potresti non riuscire a salvare le modifiche qualora questa nuova finestra faccia sì che il sistema scenda al di sotto del minimo settimanale richiesto. In questo caso, devi prima rimuovere alcune finestre di aggiornamento non disponibili esistenti o aggiungerne delle altre prima di poter salvare la nuova finestra di aggiornamento non disponibile. Per ulteriori informazioni, vedi [Impostazione delle finestre di manutenzione preapprovate](index.html#preapprovedmaintenance).

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

Puoi visualizzare diverse sezioni che includono aggiornamenti di sistema in sospeso, informazioni generali sul sistema, informazioni su API e CLI e
dettagli di configurazione LDAP.

### Aggiornamenti di sistema in sospeso

Nella sezione Aggiornamenti, puoi visualizzare il numero di notifiche di
aggiornamenti in sospeso che richiedono un tuo intervento. Ci sono due tipi che potresti vedere:

<dl>
<dt>Aggiornamenti che non comportano interruzioni del servizio</dt>
<dd>Un aggiornamento che non comporta interruzioni del servizio non influenza il tuo ambiente, le tue applicazioni in esecuzione o l'accesso dei tuoi utenti alle tue applicazioni. Questo tipo di aggiornamento non richiede un'approvazione caso per caso. Questi aggiornamenti sono applicati nelle finestre di manutenzione disponibili preapprovate da te impostate dalla pagina Aggiornamenti di sistema.</dd>
<dt>Aggiornamenti che comportano interruzioni del servizio</dt>
<dd>Un aggiornamento che comporta interruzioni del servizio può influenzare il tuo ambiente, le applicazioni in esecuzione o l'accesso dei tuoi utenti alle tue applicazioni. Puoi pianificare e approvare ciascuno di questi aggiornamenti di manutenzione entro la finestra di manutenzione di 21 giorni assegnata per garantire che l'aggiornamento non venga applicato durante ore lavorative critiche. Puoi selezionare la data e ora di distribuzione consigliata, che si basa sulle tue finestre di aggiornamento preapprovate, oppure selezionare due ore e date aggiuntive tra cui IBM può scegliere durante l'applicazione dell'aggiornamento.</dd>
</dl>

Per ulteriori informazioni sull'impostazione delle finestre di manutenzione preapprovate e sull'impostazione di specifiche date non disponibili per la manutenzione, vedi [Aggiornamenti di manutenzione](index.html#oc_schedulemaintenance).

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

- Informazioni sull'utilizzo delle risorse, ad esempio la quantità di memoria e spazio su disco che può essere riservata e quella fisicamente disponibile e la quantità di memoria e spazio su disco realmente riservata e quella fisicamente utilizzata.  Puoi anche visualizzare le informazioni relative all'utilizzo medio della CPU tra tutti gli agent DEA (Droplet Execution Agent). Per informazioni più dettagliate sull'utilizzo di memoria, disco e CPU, vedi [Dettagli memoria, disco e CPU](index.html#resourceusagedetails).
- Informazioni sull'utilizzo della rete per la larghezza di banda in entrata e in uscita nelle ultime 6 ore o nel giorno precedente. I dati visualizzati sono basati sulla somma del traffico in entrata e in uscita per la rete pubblica e quella privata.
- Il tempo di risposta medio per {{site.data.keyword.Bluemix_notm}} negli ultimi 10 minuti, 1 ora e 1 giorno.
- Le transazioni medie al secondo per {{site.data.keyword.Bluemix_notm}} nel corso degli ultimi 10 minuti, dell'ultima ora e dell'ultimo giorno.


#### Dettagli di memoria di sistema, disco e CPU
{: #resourceusagedetails}

Nella sezione **Utilizzo risorsa**, puoi vedere un riepilogo dello spazio **Riservato** e **Fisico** relativo a memoria e disco.    
	<dl>
	<dt><strong>Fisico</strong></dt>
	<dd>La quantità di memoria o spazio su disco che è stata acquistata per il tuo ambiente.</dd>
	<dt><strong>Riservato</strong></dt>
	<dd>La quantità totale di memoria o spazio su disco disponibile che può essere riservata da tutte le applicazioni distribuite e in esecuzione nel tuo ambiente. Poiché le applicazioni raramente utilizzano tutta la memoria riservata per loro, il valore fisico è di solito inferiore al valore riservato.</dd>
	</dl>

Oltre alla rappresentazione grafica, puoi visualizzare la percentuale di memoria e spazio su disco utilizzata dal tuo ambiente. Puoi anche visualizzare la quantità riservata e fisica, in GB, dell'utilizzo reale rispetto alla quantità disponibile.

Per visualizzare l'utilizzo della memoria, disco o CPU da parte di DEA, fai clic su **Suddivisione**.  

Per informazioni più dettagliate sull'utilizzo della memoria o del disco fisico e riservato nel tempo, fai clic su **Cronologia.** Puoi specificare l'intervallo di tempo da visualizzare come settimanale o mensile. La vista dell'utilizzo cronologico mostra un grafico di utilizzo della memoria o del disco nel corso del tempo da te scelto.  
	<dl>
	<dt><strong>Limite riservato</strong></dt>
	<dd>Indicato in forma di linea tratteggiata orizzontale, il limite riservato è la quantità totale di memoria o spazio su disco che può essere riservata in blocco da tutte le applicazioni in esecuzione nel tuo ambiente.</dd>
	<dt><strong>Riservato</strong></dt>
	<dd>L'area Riservato mostra la quantità di memoria o di spazio su disco che è attualmente riservata in blocco da tutte le applicazioni in esecuzione nel tuo ambiente.
	<p>Per vedere quali organizzazioni hanno riservato la maggior parte della memoria in un determinato momento, passa il mouse sopra il punto lungo l'area Riservato associato a quel momento nel tempo. Puoi quindi fare clic su un'organizzazione nel grafico a torta che viene mostrato per visualizzare ulteriori informazioni su tale organizzazione.</p></dd>
	<dt><strong>Limite fisico</strong></dt>
	<dd>Indicato in forma di linea tratteggiata orizzontale, il limite fisico mostra la quantità fisica di memoria o spazio su disco che è stata acquistata per il tuo ambiente.</dd>
	<dt><strong>Fisico</strong></dt>
	<dd>L'area Fisico mostra la quantità di memoria o spazio su disco effettivamente utilizzata.</dd>
	</dl>
	
#### Dettagli di utilizzo del servizio
{: #servicesresourceusage}

La scheda **Servizio** mostra l'utilizzo totale del servizio in relazione alla capacità massima di cui disponi per un servizio dedicato. Ad esempio, se hai un servizio Cloudant dedicato e stai utilizzando 500 GB della tua capacità di 1000 GB, visualizzi un grafico che mostra che hai utilizzato il 50%  della tua capacità totale. Il colore del grafico cambia in base a quanto sei vicino al limite di capacità. Il giallo viene mostrato quando hai utilizzato tra il 70% e l'84% della tua capacità e il rosso viene usato quando hai raggiunto l'85%  o più della capacità disponibile.

**Nota**: in questo momento, le informazioni sul consumo del servizio potrebbero non essere disponibili in tutti gli ambienti. Questa funzione è disponibile per Cloudant, MessageHub, API Connect e Session Cache.


### Utilizzo dell'account
{: #accountusage}

Puoi visualizzare l'utilizzo mensile del tuo account per il tuo ambiente locale o dedicato. Puoi utilizzare questi dati per sapere quanto addebitare a determinate organizzazioni in base all'uso effettuato. Tutti gli utenti della console di gestione che dispongono dell'autorizzazione **Utenti** con accesso in **Lettura** possono visualizzare i dati di utilizzo dell'account. Inoltre, i gestori di fatturazione dell'organizzazione possono visualizzare i dati di utilizzo account relativi alle proprie organizzazioni, anche se il gestore di fatturazione non dispone dell'autorizzazione **Utenti** della console di gestione. In qualità di amministratore della console di gestione (autorizzazione Superuser), puoi assegnare il ruolo di gestore di fatturazione per le organizzazioni facendo clic su **Account** &gt; **Gestisci organizzazioni**.

Per visualizzare i dati di utilizzo account, completa la seguente procedura:

<ol>
<li>Fai clic su <strong>Account</strong> &gt; <strong>Dashboard di utilizzo</strong>.</li>
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
<li>Fai clic su <strong>Account</strong> &gt; <strong>Dashboard di utilizzo</strong>.</li>
<li>Fai clic su <strong>Pubblico</strong>.</li>
<li>Seleziona l'organizzazione per cui desideri visualizzare i dati.</li>
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

La seguente tabella mostra l'elenco dei report di sicurezza generati per {{site.data.keyword.Bluemix_notm}} locale e {{site.data.keyword.Bluemix_notm}} dedicato. La maggior parte dei report viene generata ogni giorno. Tuttavia, i report per gli eventi di gestione chiavi e crittografia vengono generati mensilmente. Tutti i report vengono conservati per 90 giorni nella console di gestione. Al termine dei 90 giorni, i report sono disponibili offline su richiesta a {{site.data.keyword.Bluemix_notm}} per 9 mesi. In totale, i report sono disponibili per il recupero per un massimo di 1 anno.


{: #ld_table9}

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
{: caption="Tabella 9. Elenco dei report di sicurezza" caption-side="top"}

## Visualizzazione dello stato
{: #oc_status}

Puoi visualizzare lo stato per l'ambiente {{site.data.keyword.Bluemix_notm}} e per la console di gestione.

### Stato dell'ambiente {{site.data.keyword.Bluemix_notm}}

Puoi monitorare lo stato per la tua istanza {{site.data.keyword.Bluemix_notm}} utilizzando la pagina Stato di {{site.data.keyword.Bluemix_notm}}. Fai clic su **Supporto** &gt; **Stato**.

La pagina Stato è la posizione centrale per trovare notifiche e annunci sugli eventi chiave che interessano la piattaforma {{site.data.keyword.Bluemix_notm}} e i servizi principali in {{site.data.keyword.Bluemix_notm}}. Puoi sottoscrivere a un feed RSS per le notifiche in modo da non doverle controllare personalmente. Per ulteriori informazioni sulla pagina Stato e sulla configurazione del feed RSS, vedi [Visualizzazione di {{site.data.keyword.Bluemix_notm}}](../support/index.html#viewing-bluemix-status).

### Stato della console di gestione

Dopo la distribuzione iniziale del tuo ambiente {{site.data.keyword.Bluemix_notm}}, un controllo di verifica viene completato automaticamente sui componenti utilizzati per amministrare il tuo ambiente. Puoi andare alla pagina Controllo verifica console di gestione per controllare lo stato dei componenti dopo che è stato eseguito il controllo di verifica. Per accedere alla pagina,
vai a <code>https://console.&lt;dominiosecondario&gt;.bluemix.net/check</code>, dove `<dominiosecondario>` è il nome della tua istanza locale o dedicata.

Puoi eseguire una verifica in qualsiasi momento. Devi aver eseguito l'accesso per selezionare l'opzione per eseguire la verifica. Se riscontri dei malfunzionamenti mentre stai aggiungendo un utente, modificando un'organizzazione o gestendo i tuoi servizi, esegui questo controllo per identificare eventuali componenti malfunzionanti o disconnessi. Puoi aprire un ticket del supporto con le informazioni dal controllo per far risolvere rapidamente il problema.

## Gestione del tuo catalogo
{: #oc_catalog}

Puoi gestire quali servizi {{site.data.keyword.Bluemix_notm}} sono visibili agli utenti nel Catalogo {{site.data.keyword.Bluemix_notm}}. Fai clic su **AMMINISTRAZIONE &gt; GESTIONE CATALOGO**.

Seleziona un tile di servizio per modificare la visibilità del piano di servizio. Per modificare la
visibilità, seleziona dalle seguenti opzioni:

- Per visualizzare il servizio nascosto in modo che sia visibile ai tuoi utenti nel
Catalogo, seleziona **ABILITA TUTTI I PIANI**.
- Per nascondere il servizio ai tuoi utenti nel Catalogo {{site.data.keyword.Bluemix_notm}},
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

Se vuoi visualizzare un determinato servizio nel tuo catalogo {{site.data.keyword.Bluemix_notm}}, devi implementare e registrare un [broker dei servizi ![Icona link esterno](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/services/api.html){: new_window}. Una volta registrato il tuo broker, puoi scegliere quali organizzazioni possono accedere al servizio nella tua istanza locale o dedicata.

Le modalità d'uso del tuo broker dei servizi variano a seconda del numero di servizi che gestisce o dalla sua eventuale precedente registrazione in {{site.data.keyword.Bluemix_notm}}.

- Se il tuo broker dei servizi gestisce un unico servizio, puoi utilizzare l'interfaccia utente per registrarlo al termine dell'implementazione dell'[API broker dei servizi ![Icona link esterno](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/services/api.html){: new_window}. Vedi [Registrazione di un broker dei servizi che gestisce un unico servizio](index.html#registerbrokerui).
- Se il tuo broker dei servizi gestisce più servizi, utilizza la CLI cf con il plug-in [{{site.data.keyword.Bluemix_notm}} Admin CLI](../cli/plugins/bluemix_admin/index.html) (sottocomando `ba`) o l'[API del servizio personalizzato](index.html#servicebrokerapi).
- Se il tuo broker dei servizi è già registrato e desideri aggiornarlo o eliminarlo, utilizza la CLI cf con il plug-in [{{site.data.keyword.Bluemix_notm}} Admin CLI](../cli/plugins/bluemix_admin/index.html) (sottocomando `ba`) o l'[API del servizio personalizzato](index.html#servicebrokerapi).

#### Registrazione di un broker dei servizi che gestisce un unico servizio
{: #registerbrokerui}

<!-- staging only start -->

Esamina le seguenti informazioni e completa la procedura per registrare il tuo broker dei servizi:

**rima di iniziare**: <a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">implementa l'API broker dei servizi Cloud Foundry <img src="../icons/launch-glyph.svg" alt="Icona link esterno"></a> per consentire la comunicazione tra il tuo servizio e {{site.data.keyword.Bluemix_notm}}. L'API broker dei servizi è un insieme di endpoint REST utilizzati da {{site.data.keyword.Bluemix_notm}}.

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
```
{: codeblock}

Le seguenti tabelle possono aiutarti a compilare il file JSON.


{: #ld_table10}

| **Campi JSON** | **Descrizione** |
|-----------------|-----------------|
|bindable   | Un valore booleano che indica se le istanze del servizio possono essere associate tramite bind alle applicazioni.  |
|description | La descrizione del servizio visualizzata quando utilizzi il comando cf marketplace o passi il mouse sull'icona del servizio nel catalogo dell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Puoi aggiungere una singola parola o frase per la descrizione. |
|name | Il nome del servizio visualizzato nell'interfaccia riga di comando cf. Questo nome deve essere univoco all'interno di {{site.data.keyword.Bluemix_notm}}, deve utilizzare lettere minuscole e non può contenere spazi. Dopo aver registrato il servizio con {{site.data.keyword.Bluemix_notm}}, non potrai più modificarne il nome. |
|ID  | L'ID del servizio. Questo ID deve essere univoco in {{site.data.keyword.Bluemix_notm}} e deve essere un GUID (Globally Unique Identifier). Dopo aver registrato il servizio con {{site.data.keyword.Bluemix_notm}}, non potrai più modificare l'ID. |
|metadata | I metadati del piano di servizio visualizzati nel catalogo {{site.data.keyword.Bluemix_notm}} e nel listino prezzi. Il campo dei metadati è facoltativo. Puoi specificare più campi per i metadati. Per ulteriori informazioni, vedi la seguente tabella per i [campi Metadati](index.html#metadatafields). |
|plans | Un array di definizioni del piano di servizio. Per ulteriori informazioni, vedi la seguente tabella per i [campi Piano](index.html#planfields). |
{: caption="Tabella 10. Campi JSON" caption-side="top"}


{: #metadatafields}

| **Valori metadati** | **Descrizione** |
|---------------------|-----------------|
|displayName          | Il nome del piano visualizzato nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Questo nome viene visualizzato sia nel catalogo alla pagina dei dettagli del servizio che nel listino prezzi. Scrivi in maiuscolo solo la prima lettera del nome del piano. Non utilizzare "Predefinito" come nome piano predefinito, usa invece "Standard". |
|providerDisplayName | Il nome del provider di servizi |
|longDescription | La descrizione dettagliata per il servizio. Utilizza almeno due frasi per una descrizione lunga. |
|plans                | Un array di definizioni del piano di servizio. Ogni voce di array del campo plans comprende i seguenti campi: name, description, free, id e metadata. Per ulteriori informazioni, vedi la seguente tabella per i [campi Piano](index.html#planfields). |
|bullets | Un array di stringhe visualizzate per un servizio. Puoi utilizzare gli elementi bullet per fornire informazioni in aggiunta alla descrizione lunga. Il campo bullets deve contenere almeno due elementi bullet. Ogni elemento bullet include il campo del titolo e della descrizione. |
|imageUrl | L'URL di un'immagine PNG grande  (50 x 50 pixel). |
|smallImageUrl | L'URL di un'immagine PNG piccola (24 x 24 pixel). |
|mediumImageUrl | L'URL di un'immagine PNG media (32 x 32 pixel). |
|featuredImageUrl | L'URL di un'immagine in evidenza (64 x 64 pixel). |
|documentationUrl | L'URL della documentazione per il servizio. |
|termsUrl | L'URL dei file PDF che contengono i termini dell'accordo. |
|media (facoltativo) | Un array di elementi per visualizzare i video e le acquisizioni schermo che introducono il servizio nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Un elemento media può contenere i seguenti campi: type (image, youtube, video), thumbnailUrl (l'URL dell'immagine di anteprima per l'elemento media), url (l'URL dell'acquisizione schermo o del video YouTube), source (le origini dei video che non sono ospitati su YouTube. Il "type" delle origini del video deve essere supportato da HTML5. Includi "type" e "url" per il video)e caption (la didascalia per l'elemento media. Le didascalie consentono un accesso facilitato agli utenti con disabilità per comprendere gli elementi media). |
|serviceKeysSupported | Un valore booleano che indica se l'API delle chiavi del servizio è supportata. L'API delle chiavi del servizio permette di abilitare l'utilizzo di un servizio al di fuori di {{site.data.keyword.Bluemix_notm}}. Il valore predefinito è false. |
|plan_updateable | Un valore booleano che indica se il servizio supporta le modifiche del piano. Il valore predefinito è false. |
|embeddableDashboard (facoltativo) | Un campo che indica come viene visualizzato il dashboard del servizio nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Se non specifichi questo campo, il dashboard viene integrato ma viene limitato a una larghezza minima di 960px e il dashboard avrà un ulteriore riempimento orizzontale intorno all'iframe. Puoi utilizzare true, false, drilldown o launch. Per questo valore puoi utilizzare i seguenti campi: true, false, drilldown e launch.  |
|notCreatable (facoltativo) | Un valore booleano che indica se le istanze per il servizio possono essere create dall'interfaccia utente {{site.data.keyword.Bluemix_notm}} e dall'interfaccia riga di comando cf. Il valore true significa che le istanze del servizio non possono essere create né dall'interfaccia utente {{site.data.keyword.Bluemix_notm}} né dall'interfaccia riga di comando cf. Il valore predefinito è false. |
|notCreatableMessage (facoltativo) | Un messaggio che viene visualizzato nell'interfaccia utente {{site.data.keyword.Bluemix_notm}} se non è possibile creare le istanze del servizio. Se non specifichi questo campo, verrà visualizzato il seguente messaggio predefinito: Per ricevere una notifica sulla disponibilità del servizio, confermare l'indirizzo email o immettere un nuovo indirizzo. |
|notCreatableRobotMessage (facoltativo) | Un messaggio che viene visualizzato nell'area commenti della pagina dei dettagli del servizio nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Il messaggio viene utilizzato per indicare che un servizio potrebbe avere un problema o altre cause che lo rendono non disponibile. Puoi specificare un messaggio per spiegare il motivo. Se non specifichi questo campo, verrà visualizzato il seguente messaggio predefinito: Questo servizio non è al momento disponibile. |
|apiReferenceUrl (facoltativo) | L'URL dell'iframe nell'area Riferimento API nella pagina dei dettagli del servizio all'interno del catalogo. Se non viene utilizzato per la pagina dei dettagli del servizio nel Catalogo, puoi immettere il valore numerico assegnato alla Documentazione API REST del tuo servizio durante la registrazione nel microservizio Documentazione API REST di {{site.data.keyword.Bluemix_notm}}. In questo modo, la documentazione dell'API REST verrà visualizzata nel dashboard del servizio. |
|sdkDownloadUrl (facoltativo) | L'URL della pagina Web che si apre quando fai clic sul pulsante Scarica SDK. Il pulsante Scarica SDK si trova nel tile del servizio nella pagina di panoramica dell'applicazione nel Dashboard. La pagina Web si apre in una scheda del browser. |
|serviceMonitorApi    | L'URL di un'API che restituisce i dati JSON, come mostrato nel seguente esempio, che segnala l'integrità del servizio. Devi avere serviceMonitorApi o serviceMonitorApp nei metadati del servizio. Consulta il seguente codice come esempio. |
|serviceMonitorApp    | L'URL a un'applicazione che può essere distribuita in {{site.data.keyword.Bluemix_notm}} ed essere associata a un servizio per fornire l'output specifico dello stato del servizio. L'applicazione deve restituire il formato dei dati JSON uguale al serviceMonitorApi. Devi avere serviceMonitorApi o serviceMonitorApp nei metadati del servizio. Consulta il seguente codice come esempio. |
{: caption="Tabella 11. Campi dei metadati" caption-side="top"}


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


{: #planfields}

| **Valori del piano** | **Descrizione** |
|---------------------|-----------------|
|name       | Il nome del piano di servizio utilizzato nell'interfaccia riga di comando cf. Il nome del piano viene, ad esempio, visualizzato nell'output del comando cf marketplace. Il nome del piano deve essere in lettere minuscole, non può contenere spazi e deve essere univoco all'interno del servizio.  |
|description       | La descrizione del piano di servizio. La descrizione viene visualizzata quando selezioni una piano nella pagina dei dettagli del servizio nel catalogo {{site.data.keyword.Bluemix_notm}}. |
|free      | Un valore booleano che indica se il piano di servizio è gratuito. Il valore predefinito è true. |
|ID       | L'ID del piano di servizio. L'ID deve essere univoco e deve essere un GUID.  |
|metadata (facoltativo)    | I metadati del piano di servizio visualizzati nel catalogo {{site.data.keyword.Bluemix_notm}} e nel listino prezzi. Il campo dei metadati è facoltativo. Nel campo metadata puoi specificare i seguenti campi: displayName, type (subscription, reservable, planDetails), bullets, costs (unitId, unit, partNumber) e paidOnly. Per ulteriori informazioni, vedi la seguente tabella per i [campi Metadati del piano](index.html#planmetadata). |
{: caption="Tabella 12. Campi del piano" caption-side="top"}


{: #planmetadata}

| **Valori dei metadati del piano** | **Descrizione** |
|------------------------|-----------------|
|displayName             | Il nome del piano visualizzato nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Questo nome viene visualizzato sia nel catalogo alla pagina dei dettagli del servizio che nel listino prezzi.   |
|type                    | Il tipo di piano. Per questo campo, puoi utilizzare i seguenti valori: subscription (un piano di sottoscrizione. Il valore predefinito è false), reservable (un piano riservabile. Questo valore viene utilizzato solo quando il piano è un piano di sottoscrizione, ossia, il valore di plan.metadata.subscription è true. Il valore predefinito è false), planDetails (quantità e descrizione dettagliata delle risorse che possono essere utilizzate con il piano. Questo valore viene utilizzato solo quando il piano è riservabile, ossia, il valore di  plan.metadata.reserveable è true.) |
|bullets                 | Una descrizione delle risorse che possono essere utilizzate con il piano. La descrizione viene visualizzata nella colonna **Funzioni** nella pagina dei dettagli del servizio del catalogo e nel listino prezzi. |
|costs                   | Informazioni sui costi del servizio che vengono visualizzate nella colonna Prezzo nella pagina dei dettagli del servizio del catalogo e nel listino prezzi. Ogni voce di array contiene i seguenti campi: unitId (l'ID dell'unità. Utilizza la forma plurale e scrivi in maiuscolo tutte le lettere. Per i piani gratuiti, questo campo è facoltativo), unit (la metrica utilizzata per calcolare gli addebiti del servizio. Il valore di questo campo è utilizzato nell'interfaccia utente {{site.data.keyword.Bluemix_notm}} per rappresentare la metrica di addebito)e partNumber (l'identificativo `part_number` utilizzato dal sistema di fatturazione. Per i piani gratuiti, questo campo è facoltativo).   |
|paidOnly (facoltativo)     | Un valore booleano che indica se questo piano di servizio è disponibile solo per gli account a pagamento {{site.data.keyword.Bluemix_notm}}. Il valore **true** significa che il piano di servizio è destinato solo agli account a pagamento e non può essere aggiunto agli account di prova. Il valore **false** significa che il piano di servizio può essere aggiunto sia agli account a pagamento che di prova. Il valore predefinito è **false**.	  |
{: caption="Tabella 13. Campi dei metadati del piano" caption-side="top"}

Il seguente esempio mostra come la risposta JSON di GET /v2/catalog è associata alla pagina dei dettagli del servizio nel catalogo {{site.data.keyword.Bluemix_notm}}. In particolare, il modo in cui i campi dei metadati del piano descritti nella tabella precedente vengono associati all'interfaccia utente:

![Dettagli dei metadati del piano nel catalogo.](images/plan_metadata.png "Vista dei valori metadati del piano nel catalogo")


<!-- staging only end -->

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

Per creare un'organizzazione e aggiungere gestori, completa la seguente procedura:

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

1. Dalla barra dei menu, fai clic su **Account** &gt; **Gestisci organizzazioni**.
2. Seleziona l'organizzazione a cui vuoi aggiungere uno spazio.
3. Fai clic su **Crea uno spazio**.
4. Immetti un nome spazio.
5. Fai clic su **Crea**.

### Monitoraggio quota

Puoi espandere la sezione **Monitoraggio quota** per visualizzare le seguenti informazioni:

- Utilizzo della memoria dell'ambiente mostra in dettaglio l'utilizzo della memoria per l'intero ambiente di sistema. Il grafico mostra le seguenti informazioni:
<ul>
<li>La memoria fisica in uso e il limite di memoria fisica disponibile</li>
<li>La quota di memoria attualmente riservata e il limite di memoria che è possibile riservare</li>
<li>La quota totale di memoria per le tue organizzazioni</li>
</ul>
I seguenti tipi di utilizzo della memoria vengono visualizzati nel grafico.

	<dl>
	<dt><strong>Memoria fisica utilizzata</strong></dt>
	<dd>La memoria fisica utilizzata dal tuo ambiente.</dd>
	<dt><strong>Limite fisico</strong></dt>
	<dd>La memoria fisica totale disponibile nel tuo ambiente.</dd>
	<dt><strong>Quota riservata</strong></dt>
	<dd>La somma di memoria riservata per tutte le applicazioni distribuite, tra tutte le organizzazioni. La somma della quota riservata può superare il limite fisico di memoria per il tuo ambiente. Ad esempio, se hai un limite di memoria fisica pari a 16 GB, potresti riservare 4 GB di memoria ciascuna per un totale di cinque diverse applicazioni. La quota riservata supera il limite fisico della memoria. Tuttavia, in molti casi, le applicazioni potrebbero non utilizzare la quota totale riservata singolarmente a ciascuna di esse. Inoltre, è possibile che le applicazioni non utilizzino
	contemporaneamente la quota totale della memoria riservata.</dd>
	<dt><strong>Limite riserva</strong></dt>
	<dd>La memoria totale che può essere riservata tra tutte le applicazioni per il tuo ambiente.</dd>
	<dt><strong>Quota totale</strong></dt>
	<dd>La quota di memoria totale tra tutte le organizzazioni.</dd>
	</dl>
	**Nota**: i dati vengono aggiornati automaticamente ogni 4 ore. Fai clic su **Ricalcola** se desideri aggiornare i dati sulla pagina prima dell'aggiornamento automatico.

- Utilizzo della memoria dell'organizzazione. Questa sezione mostra in dettaglio l'utilizzo della memoria a livello di organizzazione. Puoi visualizzare la quota di memoria totale, la quota riservata e la memoria fisica utilizzata da ogni organizzazione. Il grafico fornisce informazioni che vengono elencate in base alla quantità di memoria riservata per ogni organizzazione e, per impostazione predefinita, viene elencata per prima l'organizzazione che riserva la maggiore quantità di memoria. Puoi ordinare per **Utilizzo massimo memoria** e **Assegnazione memoria in eccesso**.

	<dl>
	<dt><strong>Utilizzo massimo memoria</strong></dt>
	<dd>Usa questa opzione per identificare l'organizzazione che ha riservato la maggiore quantità di memoria. Ordina in base all'utilizzo massimo di memoria per identificare le organizzazioni che hanno riservato la maggiore quantità di memoria. L'elenco viene ordinato in base alla quota riservata. </dd>
	<dt><strong>Assegnazione memoria in eccesso</strong></dt>
	<dd>Usa questa opzione per identificare le organizzazioni che hanno una quota di memoria totale superiore a quella necessaria. Ordina per Assegnazione memoria in eccesso per identificare le organizzazioni che utilizzano
la minore quantità di memoria per la quota assegnata per l'organizzazione. </dd>
	</dl>

### Gestione delle quote
{: #manageorgquota}

Una quota rappresenta i limiti di risorse per le organizzazioni, che viene assegnata quando l'organizzazione viene creata. Applicazioni o servizi in uno spazio all'interno dell'organizzazione contribuiscono tutti all'utilizzo della quota assegnata. Per gestire i seguenti passi completare la gestione della quota per un'organizzazione:

<ol>
<li>Fai clic sulla barra del grafico
relativo all'organizzazione che vuoi modificare nella sezione Utilizzo della memoria dell'organizzazione o seleziona il nome
dell'organizzazione nella sezione Elenco organizzazioni. Dalla pagina Informazioni sull'organizzazione, puoi ridenominare l'organizzazione e aggiungere o rimuovere i gestori.
<p><strong>Nota</strong>: se selezioni un piano di quota che non è sufficiente per l'utilizzo corrente
dell'organizzazione, riceverai un messaggio.</p></li>
<li>Fai clic su <strong>Cloud Foundry</strong> o <strong>Containers</strong>.  Per impostazione predefinita, si apre la pagina della quota Cloud Foundry. 
<ul>
<li>Dalla pagina Cloud Foundry, puoi selezionare un piano e visualizzare i dettagli della quota per le seguenti risorse:
<ul>
<li>Servizi</li>
<li>Rotte</li>
<li>Quota di memoria</li>
<li>Assegnazione applicazione</li>
</ul>
</li>
<li>Dalla pagina <strong>Containers</strong>, puoi assegnare i valori, che devono essere numeri interi, per i seguenti campi:
<dl class="parml">
<dt class="pt dlterm">Limite immagine</dt>
<dd class="pd">Il numero massimo di immagini contenitore che puoi avere nel tuo registro privato. Un'immagine contenitore è la base per ogni contenitore che crei. Un'immagine viene creata da un Dockerfile che è un file in sola lettura che ospita il sistema operativo, l'applicazione e tutte le relative dipendenze e descrive come viene configurato un contenitore. Le immagini sono condivise tra tutti i membri di un'organizzazione.</dd>
<dt class="pt dlterm">Assegnazione memoria predefinita</dt>
<dd>La quantità di memoria del contenitore che viene automaticamente assegnata quando viene creato un nuovo spazio. Quando crei un contenitore, devi scegliere una dimensione del contenitore. La dimensione determina la quantità di memoria che il contenitore può utilizzare sull'host di calcolo ed è compresa nel tuo limite di memoria del contenitore. </dd>
<dt class="pt dlterm">Assegnazione memoria massima</dt>
<dd>La quantità massima di memoria della memoria del contenitore che può essere assegnata tra tutti gli spazi di un'organizzazione.</dd>
<dt class="pt dlterm">IP mobili predefiniti</dt>
<dd>Il numero di indirizzi IP pubblici che viene automaticamente assegnato quando viene creato un nuovo spazio. Puoi eseguire il bind degli indirizzi IP pubblici a contenitori singoli o a gruppi di contenitori per renderli accessibili da internet.</dd>
<dt class="pt dlterm">Numero massimo di IP mobili</dt>
<dd>Il numero massimo di indirizzi IP pubblici che puoi assegnare tra tutti gli spazi di un'organizzazione.</dd>
</dl>
<strong>Nota</strong>: se non disponi ancora di contenitori nel tuo ambiente o se non li hai ancora configurati, ricevi un messaggio di errore.
<p>Per ulteriori informazioni sui contenitori, consulta [Informazioni su IBM Containers](/docs/containers/container_ov.html). Per ulteriori informazioni sulle quote del contenitore, consulta [Quota e account Bluemix](/docs/containers/container_planning_org_ov.html#container_planning_quota).</p>
<strong>Nota:</strong> i contenitori non sono disponibili nella regione {{site.data.keyword.Bluemix_notm}} Sydney.</li>
</ul>
<li>Per salvare le eventuali modifiche apportate nella pagina Gestisci organizzazione, fai clic su <strong>SALVA</strong>.</li>
</ol>


### Gestione delle tue organizzazioni dall'elenco delle organizzazioni
{: #manageorgfrolis}

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
- Per visualizzare le informazioni su un utente specifico dell'organizzazione che stai visualizzando, fai clic sul nome utente per visualizzarne le informazioni. Puoi quindi fare clic sul nome dell'organizzazione per ritornare a visualizzare le informazioni sull'organizzazione. 

## Gestione di utenti e autorizzazioni
{: #oc_useradmin}

Puoi aggiungere gli utenti singolarmente o in gruppi. In genere, gli utenti vengono aggiunti alla tua istanza {{site.data.keyword.Bluemix_notm}} dal registro utenti della tua azienda tramite LDAP (Lightweight Directory Access Protocol). Puoi anche visualizzare le autorizzazioni utente. Se disponi dell'autorizzazione **Superuser**, puoi anche impostare e gestire le autorizzazioni per gli altri utenti. Fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE UTENTI**.

La pagina Amministrazione utenti visualizza tutti gli utenti per l'istanza locale o dedicata. Sono visualizzate le autorizzazioni per ciascun utente utilizzando le icone nella tabella. Le autorizzazioni possono essere: Nessuna, **Superuser**, **Accesso di base**, **Catalogo**, **Report** e **Utenti**.
Le autorizzazioni **Superuser** e **Accesso di base** possono essere impostate su **Attivo** o **Disattivo**, mentre le altre autorizzazioni vengono abilitate o disabilitate con specifici tipi di accesso, tra cui l'accesso in **Lettura** o **Scrittura** per l'autorizzazione indicata, come rappresentato dalle icone. Consulta [Autorizzazioni](#permissions) per delle descrizioni di
ciascun tipo e una spiegazione delle icone.

### Gestione degli utenti
{: #workwithusers}

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
    
* Per visualizzare le informazioni sull'organizzazione a cui è assegnato l'utente, fai clic sul nome dell'organizzazione per visualizzarne le informazioni. Puoi quindi fare clic sul nome dell'utente per ritornare a visualizzare le informazioni sull'utente. 

### Autorizzazioni
{: #permissions}

È possibile assegnare agli utenti le seguenti autorizzazioni con livelli di accesso specifici (lettura o scrittura) che consentono all'utente di completare attività specifiche all'interno della console di gestione.


{: #ld_table14}

| **Autorizzazione utente** | **Descrizione** |       
|-----------------|-------------------|
| Superuser | Gli utenti con l'autorizzazione **Superuser** impostata su **Attivo** possono modificare le autorizzazioni per gli altri utenti. Se hai l'autorizzazione attiva, ti viene automaticamente abilitato l'accesso completo alle altre autorizzazioni. Oltre alle attività descritte per ogni autorizzazione nella tabella, questi utenti possono anche impostare le sottoscrizioni di notifica per essere direttamente avvertiti in merito a manutenzione o incidenti, per pianificare la manutenzione, eseguire i controlli di verifica sui componenti della console e creare organizzazioni e spazi per l'ambiente. Questa autorizzazione equivale al ruolo di amministratore (admin) per la console di gestione.  |
| Accesso di base | Gli utenti con l'autorizzazione **Accesso di base** impostata su **Attivo** possono visualizzare l'opzione della pagina di amministrazione nell'interfaccia utente  {{site.data.keyword.Bluemix_notm}}. Gli utenti con l'autorizzazione abilitata possono avere accesso alle [Informazioni di sistema](#oc_system) e ai tile [Utilizzo della risorsa](#oc_resource). Senza questa autorizzazione, gli utenti non possono visualizzare o accedere all'opzione di menu Amministrazione. Questa autorizzazione equivale al ruolo di amministratore (admin) per la console di gestione. Equivale all'autorizzazione di accesso utilizzata precedentemente per la console di gestione. |
| Catalogo | Agli utenti con autorizzazione **Catalogo** può essere assegnato l'accesso in **Lettura** o in **Scrittura** (modifica) per i servizi disponibili nell'istanza locale o dedicata. L'accesso in lettura consente all'utente di accedere al tile di gestione del catalogo per visualizzare i servizi disponibili. L'accesso in scrittura consente all'utente di accedere al tile [Gestione catalogo](#oc_catalog) per visualizzare i servizi, modificare la visibilità dei servizi, registrare i servizi personalizzati e controllare l'elenco di priorità del pacchetto di build. |  
| Report | Agli utenti con autorizzazione **Report** può essere assegnato l'accesso in **Lettura** o in **Scrittura** (modifica) per i report di sicurezza. L'accesso in lettura consente all'utente di accedere al tile Report e log per scaricare i report. L'accesso in scrittura consente agli utenti di visualizzare il tile [Report e log](#oc_report) così come di utilizzare la CLI per caricare nuovi report e creare nuove categorie per l'accesso degli utenti. |
| Utenti | Agli utenti con autorizzazione **Utenti** può essere assegnato l'accesso in  **Lettura ** (visualizzazione) per l'elenco di utenti o in **Scrittura** (aggiunta o rimozione) per gli utenti. Questa autorizzazione non ti consente di impostare le autorizzazioni per gli altri utenti. L'accesso in scrittura consente all'utente di aggiungere nuovi utenti all'ambiente, eliminare utenti dall'ambiente e aggiungere utenti esistenti all'organizzazione che già esistono nell'ambiente. In aggiunta, l'accesso in **Scrittura** consente agli utenti di aggiungere nuove organizzazioni, eliminare le organizzazioni e modificare gli utenti nelle organizzazioni. |
{: caption="Tabella 14. Autorizzazioni" caption-side="top"}

## Utilizzo delle API REST 
{: #auth_adminapi}

Per utilizzare i comandi dell'API REST, devi innanzitutto eseguire l'autenticazione. Per generare e supportare le sessioni, puoi utilizzare i comandi cURL per compiere le seguenti attività:

* [Accesso alla Console di gestione](#auth_loginapi) 
* [Memorizzazione di ID utente e password](#auth_setuidpw)
* [Memorizzazione di cookie](#auth_apistorecook)
* [Riutilizzo dei cookie](#auth_apireusecook)

### Accesso alla Console di gestione
{: #auth_loginapi}

Prima di poter eseguire qualsiasi richiesta API `Admin`,
devi eseguire l'accesso alla Console di gestione. 

Per accedere alla Console di gestione, puoi utilizzare l'autenticazione di accesso di base
sull'endpoint `https://console.<region>.bluemix.net/login`. Il server restituisce un cookie con la tua sessione. Puoi utilizzare tale
cookie per tutte le operazioni con la Console di gestione.

**Nota:** la sessione diventa non valida se non viene utilizzata per qualche ora.

Per accedere alla
Console di gestione, esegui questo comando:

`curl --user <user_id>:<password> -c ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/login | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">--user <em>id_utente</em>:<em>password</em></dt>
<dd class="pd">Accetta l'ID utente e la password e invia un'intestazione di autorizzazione di base.</dd>
<dt class="pt dlterm">-c <em>nomefile</em></dt>
<dd class="pd">Memorizza l'ID utente e la password specificati come un cookie nel file specificato.</dd>
<dt class="pt dlterm">-b <em>nomefile</em></dt>
<dd class="pd">Richiama l'ID utente e la password specificati come un cookie nel file specificato.</dd>
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

### Memorizzazione di ID utente e password
{: #auth_setuidpw}

Puoi memorizzare il tuo ID utente e password in modo da non doverli immettere manualmente ogni volta che esegui l'accesso.  Per memorizzare il tuo ID utente e password per poterli riutilizzare, utilizza il seguente esempio cURL:

`curl -X GET -H "Authorization: Basic <redacted>" -H "Accept: application/json" "http://localhost:3000/login"`
{: codeblock}

Per configurare le tue informazioni di accesso in un file separato e quindi richiamare il file in modo da non doverlo immettere per ogni richiesta di autenticazione, utilizza l'opzione `--netrc` fornita dal comando cURL.

Per utilizzare l'opzione `--netrc` con cURL, crea prima un file nella directory home dell'utente in uno dei seguenti modi:
* Su un sistema Unix, crea un file denominato .netrc 
* Su un sistema Windows, crea un file denominato _netrc. 

Nel file, immetti le seguenti informazioni:

`machine console.<region>.bluemix.net
login <id>
password <password>`
{: codeblock}

Quando si richiama un comando cURL, aggiungi il seguente argomento: `--netrc`.
<p>Per utilizzare un file netrc che si trova in una directory differente, utilizza l'opzione `--netrc-file [file]`, dove `[file]` è la posizione del file netrc.</p>
</li>
</ol>


### Memorizzazione di cookie
{: #auth_apistorecook}

Quando accedi alla Console di gestione, il server restituisce un cookie con la tua sessione. Questo cookie è richiesto come parte del processo di accesso per le future chiamate API per tutte le operazioni con la Console di gestione. Puoi memorizzare i cookie anche per un utilizzo successivo.

Per memorizzare i cookie dopo aver eseguito l'accesso, utilizza l'opzione `-c`, come mostrato nel seguente esempio CURL:

`curl --user <user_id>:<password> -c ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/login | python -m json.tool`
{: codeblock}

### Riutilizzo dei cookie
{: #auth_apireusecook}

Per riutilizzare i cookie, utilizza l'opzione `-b` con il nome del file cookie che hai assegnato con l'opzione `-c`, come mostrato nel seguente esempio CURL:

`curl --user <user_id>:<password> -b ./cookies.txt`
{: codeblock}

## Gestione degli utenti con la API REST Admin

{: #usingadminapi}

Puoi utilizzare l'API REST `Admin` per aggiungere e rimuovere utenti per l'istanza {{site.data.keyword.Bluemix_notm}}.
Gli endpoint della API REST `Admin` e le risposte JSON sono fornite su base sperimentale per abilitare le operazioni di base da una riga di comando. Gli endpoint e gli URL negli esempi nelle presenti
informazioni possono variare o potrebbero essere abbandonate con breve preavviso.

Se disponi dell'autorizzazione **Superuser** o **Utenti**
con l'accesso in **Scrittura**, puoi aggiungere o rimuovere gli utenti. Per modificare le autorizzazioni di altri utenti devi disporre
dell'autorizzazione **Superuser**.

Anche se puoi utilizzare altri strumenti, i seguenti sono prerequisiti per l'utilizzo degli esempi che seguono:
utilizzare altri strumenti.
* cURL, per immettere richieste API REST come comandi. cURL è un programma di utilità gratuito che puoi
                    utilizzare per inviare richieste HTTP a un server e ricevere le risposte
                    attraverso un'interfaccia riga di comando. Puoi scaricare
cURL dal [sito cURL Download ![Icona link esterno](../icons/launch-glyph.svg)](http://curl.haxx.se/download.html){: new_window}.
* Python, per utilizzare lo strumento JSON Pretty-Print Python. Questo strumento
facoltativo prende il testo JSON come input e fornisce un output facile da leggere. Puoi scaricare
Python dal [sito Python Downloads ![Icona link esterno](../icons/launch-glyph.svg)](https://www.python.org/downloads){: new_window}.


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
<li>Pubblica il contenuto del file JSON nell'endpoint dell'utente immettendo il seguente
comando:<br/><br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<your_host>.ibm.com/codi/v1/users
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

## API per le metriche (sperimentale)
{: #envappmetricsapi}

Puoi utilizzare tre API sperimentali per raccogliere le metriche sul tuo ambiente o sulle tue applicazioni. Queste API restituiscono un array di punti dati per le metriche che hai richiesto nell'intervallo di tempo che hai specificato.

Puoi accedere alle API delle metriche descritte nelle seguenti sezioni dall'endpoint specifico della regione, ad esempio: 

`https://console.<region>.bluemix.net/admin/metrics`
{: codeblock}

**Note**:

1. Un utente può effettuare fino a 200 richieste API per le metriche in un'ora.
2. Ogni richiesta API restituisce fino a 200 punti dati per richiesta. Se sono disponibili più dati, viene fornito un URL per il caricamento della successiva serie di dati.
3. Ogni richiesta API richiede che un utente disponga almeno dell'accesso di base alla Console di gestione.  Potrebbero essere richieste delle autorizzazioni aggiuntive, come specificato di seguito.

## Raccolta delle metriche sul tuo ambiente 

Puoi utilizzare l'API di ambiente sperimentale per raccogliere le informazioni sull'ambiente di alto livello in un periodo di tempo che specifichi. Vengono restituiti i punti dati nel periodo di tempo che specifichi. I dati sono registrati approssimativamente ogni ora. Se, ad esempio, hai richiesto sei ore di dati CPU per l'ambiente, la risposta includerà i dati CPU per ognuna delle sei ore richieste.


### Endpoint di ambiente 

Puoi utilizzare il seguente endpoint per richiamare questo comando API:  `/api/v1/env`

**Nota**: per accedere a questi endpoint, è richiesta una delle seguenti autorizzazioni: **Accesso di base**, **Lettura utente**, **Scrittura utente** o **Superuser**

### Parametri della query delle metriche di ambiente

Utilizzando i seguenti parametri della query, puoi raccogliere le metriche per i tuoi CPU, disco, memoria, rete, quota e applicazioni:

<dl class="parml">
<dt class="pt dlterm">metrica</dt>
<dd class="pd">Uno o più dei seguenti valori, separati da virgole: `memory`, `disk`, `cpu`, `network`, `quota` e `apps`.</dd>
<dt class="pt dlterm">OraInizio</dt>
<dd class="pd">Il primo punto nel tempo da cui vengono restituiti i dati. Se non viene specificata una OraInizio, viene incluso il primo punto dati disponibile. Ad esempio, per raccogliere i dati tra la 14 e le 17, specificare una OraInizio di 14.</dd>
<dt class="pt dlterm">OraFine</dt>
<dd class="pd">L'ultimo  punto nel tempo da cui vengono restituiti i dati. Se non viene specificata alcuna OraFine, viene utilizzato il punto dati più recente. Ad esempio, per raccogliere i dati tra la 14 e le 17, specificare una OraFine di 17.</dd>
<dt class="pt dlterm">ordinamento</dt>
<dd class="pd">L'ordinamento in cui vengono restituiti i dati. I valori validi sono `asc` (crescente) e `desc` (decrescente). Il valore predefinito è decrescente, che restituisce prima i dati più recenti. </dd>
</dl>

Il seguente esempio utilizza i parametri di query per raccogliere le metriche relative al tuo ambiente:

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/admin/metrics/api/v1/env?metric=cpu,network,disk,apps,memory
```
{: codeblock}


### Formato dei dati delle metriche di ambiente

Le seguenti sezioni forniscono il formato dei dati.

 * Per raccogliere i dati registrati sul tuo utilizzo della memoria, utilizza il seguente formato dei dati:
 
```
{
  "sample_time": 1477494000000,
  "memory": {
    "total": {
      "physical": {
        "total_gb": 1728,
        "used": {
          "value_gb": 673.68,
          "percent": 38.99
        }
      },
    "allocated": {
        "reserved_gb": 3456,
        "total_allocated": {
          "value_gb": 2575.18,
          "percent": 74.51
        }
      },
    },
  	"cell": {
      "physical": {
        "total_gb": 864,
      "used": {
          "value_gb": 336.84,
        "percent": 38.99
      }
      },
    "allocated": {
        "reserved_gb": 1728,
      "total_allocated": {
          "value_gb": 1287.59,
        "percent": 74.51
      }
      },
    },
    "dea": {
      "physical": {
      	"total_gb": 864,
      "used": {
          "value_gb": 336.84,
        "percent": 38.99
      }
      },
    "allocated": {
        "reserved_gb": 1728,
      "total_allocated": {
          "value_gb": 1287.59,
        "percent": 74.51
      }
      },
    },
    "memory_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "percent": "47"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "percent": "51"
      },
      {
        "name": "dea_next/2",
        "type": "dea",
        "ip": "169.53.230.49",
        "percent": "45"
      },
      {
        "name": "dea_next/3",
        "type": "dea",
        "ip": "169.44.109.231",
        "percent": "43"
      }
    ]
  }
}
```
{: screen}

 * Per raccogliere i dati registrati sul tuo utilizzo del disco, utilizza il seguente formato dei dati:
 
```
{
  "sample_time": 1477494000000,
  "disk": {
    "total": {
      "physical": {
        "total_gb": 16200,
        "used": {
          "value_gb": 1614,
          "percent": 9.96
        }
      },
    "allocated": {
        "reserved_gb": 32400,
        "total_allocated": {
          "value_gb": 3979,
          "percent": 12.28
        }
      },
    },
    "cell": {
      "physical": {
        "total_gb": 8100,
      "used": {
          "value_gb": 807,
        "percent": 9.96
      }
      },
    "allocated": {
        "reserved_gb": 16200,
      "total_allocated": {
          "value_gb": 1989.5,
        "percent": 12.28
      }
      },
    },
    "dea": {
      "physical": {
        "total_gb": 8100,
      "used": {
          "value_gb": 807,
        "percent": 9.96
      }
      },
    "allocated": {
        "reserved_gb": 16200,
      "total_allocated": {
          "value_gb": 1989.5,
        "percent": 12.28
      }
      },
    },
    "disk_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "percent": "13"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "percent": "14"
      },
      {
        "name": "dea_next/2",
        "type": "dea",
        "ip": "169.53.230.49",
        "percent": "13"
      },
      {
        "name": "dea_next/3",
        "type": "dea",
        "ip": "169.44.109.231",
        "percent": "12"
      }
    ]
  }
}
```
{: screen}

 * Per raccogliere i dati registrati sul tuo utilizzo della CPU, utilizza il seguente formato dei dati:
 
```
{
  "sample_time": 1477494000000,
  "cpu": {
    "total": {
      "average_percent_cpu_used": 14.725
    },
    "cell": {
      "average_percent_cpu_used": 19
    },
    "dea": {
      "average_percent_cpu_used": 10.45
    },
    "cpu_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "sys_percent": "8.4",
        "user_percent": "2.7",
        "wait_percent": "0.0"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "sys_percent": "7.4",
        "user_percent": "2.4",
        "wait_percent": "0.0"
      },
      {
        "name": "cell/1",
        "type": "cell",
        "ip": "169.53.230.49",
        "sys_percent": "5.3",
        "user_percent": "1.9",
        "wait_percent": "0.0"
      },
      {
        "name": "cell/2",
        "type": "cell",
        "ip": "169.44.109.231",
        "sys_percent": "8.2",
        "user_percent": "22.6",
        "wait_percent": "0.0"
      }
    ]
  }
}
```
{: screen}

 * Per raccogliere i dati registrati sulla tua rete, utilizza il seguente formato dei dati:
 
```
{
  "sample_time": 1477494000000,
  "network": {
    "datapower": {
    "response_times": [
      {
        "proxy": "custom_certificates",
        "ten_seconds_ms": "0",
        "one_minute_ms": "0",
        "ten_minutes_ms": "0",
        "one_hour_ms": "0",
        "one_day_ms": "0"
      },
      {
        "proxy": "bluemix",
        "ten_seconds_ms": "90",
        "one_minute_ms": "89",
        "ten_minutes_ms": "83",
        "one_hour_ms": "85",
        "one_day_ms": "95"
      }
      ],
        "transactions": [
      {
        "proxy": "custom_domains",
        "ten_seconds_ms": "0",
        "one_minute_ms": "0",
        "ten_minutes_ms": "0",
        "one_hour_ms": "0",
        "one_day_ms": "0"
      },
      {
        "proxy": "bluemix",
        "ten_seconds_ms": "697",
        "one_minute_ms": "747",
        "ten_minutes_ms": "802",
        "one_hour_ms": "794",
        "one_day_ms": "730"
      }
      ],
        "bandwidth": {
        "in_kbps": 10855,
        "out_kbps": 38090
      }
  }
}
```
{: screen}

* Per raccogliere i dati registrati sul tuo utilizzo della quota, utilizza il seguente formato dei dati:
 
```
{
  "sample_time": 1477494000000,
  "quota": {
    "reserved_memory": {
      "total_bytes": 33176474877952
    },
    "services": {
      "total": 111650
    },
    "routes": {
      "total": 1675000
    }
  }
}
```
{: screen}

* Per raccogliere i dati registrati sulle tue applicazioni, utilizza il seguente formato dei dati:
 
```
{
  "sample_time": 1477494000000,
  "apps": {
    "count": 1406,
    "allocation": {
      "memory_gb": 571.8,
      "disk_gb": 1204
    }
  }
}
```
{: screen}

### Formato della risposta delle metriche di ambiente

```
{
   docs: [],
   next_url:
}
```
{: screen}

## Raccolta delle metriche sulle tue organizzazioni

I dati vengono registrati per tutte le organizzazioni approssimativamente ogni ora. Una richiesta per una metrica particolare restituisce le informazioni per tutte le organizzazioni in ogni esempio di dati nel periodo di tempo che specifichi, ordinate in modo decrescente per la metrica richiesta. Ad esempio, la richiesta di tutte le organizzazioni per memoria in un periodo di tempo di 6 ore in un ambiente con 200 applicazioni restituisce 1200 record, 200 alla volta.

Per ridurre la quantità di informazioni restituite per ogni esempio di dati nel periodo di tempo richiesto, puoi specificare un'opzione di conteggio. Utilizzando il precedente esempio e aggiungendo un'opzione di conteggio di 5, vengono restituiti 30 record che rappresentano le prime 5 organizzazioni per memoria per ogni esempio di dati.

### Endpoint delle organizzazioni 

Puoi utilizzare i seguenti endpoint per richiamare questo comando API:
* `/api/v1/org/memory/physical`
* `/api/v1/org/memory/reserved`
* `/api/v1/org/disk/physical`
* `/api/v1/org/disk/reserved`

**Nota**: per accedere a questi endpoint, è richiesta una delle seguenti autorizzazioni: **Lettura utente**, **Scrittura utente** o **Superuser**

### Parametri di query delle organizzazioni
 
Utilizza i seguenti parametri della query per raccogliere le metriche per le tue organizzazioni:

<dl class="parml">
<dt class="pt dlterm">OraInizio</dt>
<dd class="pd">Il primo punto nel tempo da cui vengono restituiti i dati. Se non viene specificata una OraInizio, viene incluso il primo punto dati disponibile. Ad esempio, per raccogliere i dati tra la 14 e le 17, specificare una OraInizio di 14.</dd>
<dt class="pt dlterm">OraFine</dt>
<dd class="pd">L'ultimo  punto nel tempo da cui vengono restituiti i dati. Se non viene specificata alcuna OraFine, viene utilizzato il punto dati più recente. Ad esempio, per raccogliere i dati tra la 14 e le 17, specificare una OraFine di 17.</dd>
<dt class="pt dlterm">conteggio</dt>
<dd class="pd">Il numero di record da restituire in ogni esempio di dati.
</dd>
<dt class="pt dlterm">minValue</dt>
<dd class="pd">Il valore minimo da restituire per la metrica specificata.  Se non si specifica alcun minValue, vengono restituiti tutti i valori.  Ad esempio, per raccogliere organizzazioni che utilizzano almeno 20000 byte di memoria fisica, specifica un minValue di 20000.
</dd>
</dl>

Il seguente esempio raccoglie le metriche relative alle tue organizzazioni:

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/admin/metrics/api/v1/org/memory/physical?count=5&startTime=2016-12-02T16:54:09.467Z
```
{: codeblock}

### Formato della risposta delle organizzazioni

```
{
   docs: [],
   next_url:
}
```
{: screen}

Ogni documento restituito rappresenta le metriche richieste per un'organizzazione in ogni esempio di dati, al momento della richiesta.

## Raccolta delle metriche sulle tue applicazioni

I dati vengono registrati per tutte le applicazioni approssimativamente ogni ora. Una richiesta per una metrica particolare restituisce le informazioni per tutte le applicazioni in ogni esempio di dati nel periodo di tempo che specifichi, ordinate in modo decrescente per la metrica richiesta. Ad esempio, la richiesta di tutte le applicazioni per la CPU in un periodo di tempo di 6 ore in un ambiente con 200 applicazioni restituisce 1200 record, 200 alla volta.

Per ridurre la quantità di informazioni restituite per ogni esempio di dati nel periodo di tempo richiesto, puoi specificare un'opzione di conteggio. Utilizzando il precedente esempio e aggiungendo un'opzione di conteggio di 5, vengono restituiti 30 record che rappresentano le prime 5 applicazioni per CPU per ogni esempio di dati.

### Endpoint delle applicazioni 

Puoi utilizzare i seguenti endpoint per richiamare questo comando API:
* `/api/v1/app/cpu/physical` 
* `/api/v1/app/memory/physical`
* `/api/v1/app/memory/reserved`
* `/api/v1/app/disk/physical`
* `/api/v1/app/disk/reserved`

**Nota**: per accedere a questi endpoint, è richiesta una delle seguenti autorizzazioni: **Lettura utente**, **Scrittura utente** o **Superuser**

### Parametri della query delle applicazioni
 
Utilizza i seguenti parametri della query per raccogliere le metriche per le tue applicazioni:

<dl class="parml">
<dt class="pt dlterm">OraInizio</dt>
<dd class="pd">Il primo punto nel tempo da cui vengono restituiti i dati. Se non viene specificata una OraInizio, viene incluso il primo punto dati disponibile. Ad esempio, per raccogliere i dati tra la 14 e le 17, specificare una OraInizio di 14.</dd>
<dt class="pt dlterm">OraFine</dt>
<dd class="pd">L'ultimo  punto nel tempo da cui vengono restituiti i dati. Se non viene specificata alcuna OraFine, viene utilizzato il punto dati più recente. Ad esempio, per raccogliere i dati tra la 14 e le 17, specificare una OraFine di 17.</dd>
<dt class="pt dlterm">conteggio</dt>
<dd class="pd">Il numero di record da restituire in ogni esempio di dati.
</dd>
<dt class="pt dlterm">minValue</dt>
<dd class="pd">Il valore minimo da restituire per la metrica specificata. Se non si specifica alcun minValue, vengono restituiti tutti i valori. Ad esempio, per raccogliere applicazioni che utilizzano almeno 20000 byte di memoria fisica, specifica un minValue di 20000.
</dd>
</dl>

Il seguente esempio raccoglie le metriche relative alle tue applicazioni:

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/admin/metrics/api/v1/app/cpu/physical?count=5&startTime=2016-12-02T16:54:09.467Z
```
{: codeblock}


### Formato della risposta delle applicazioni

```
{
   docs: [],
   next_url:
}
```
{: screen}

Ogni documento restituito rappresenta le metriche richieste per un'applicazione in ogni esempio di dati, al momento della richiesta.


## API del servizio personalizzato
{: #servicebrokerapi}

Sono disponibili tre API che ti consentono di registrare o creare un servizio, di aggiornare un servizio e di eliminare un servizio.

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

{: #ld_table15}

| **Nome** | **Descrizione** |
|-----------------|-------------------|
| name | Nome del broker dei servizi. |
| auth_username | Nome utente utilizzato per connettersi al broker dei servizi. |
| auth_password | Password utilizzata per connettersi al broker dei servizi. |
| broker_url | URL utilizzato per connettersi al broker dei servizi. |
| owningOrganization | Organizzazione iniziale per cui aggiungere il servizio nell'elenco elementi consentiti. |
{: caption="Tabella 15. Campi" caption-side="top"}

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
    "_id": "2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "name": "Service broker's name",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "proxy_broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "auth_username": "username",
    "created_on": "2016-09-30T16:45:56.304Z"
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

{: #ld_table16}

| **Nome** | **Descrizione** |
|-----------------|-------------------|
| name | Nome del broker dei servizi. Questo nome non può essere modificato dal nome con cui è stato creato il servizio. |
| auth_username | Nome utente utilizzato per connettersi al broker dei servizi. |
| auth_password | Password utilizzata per connettersi al broker dei servizi. |
| broker_url | URL utilizzato per connettersi al broker dei servizi. |
| owningOrganization | Organizzazione iniziale per cui aggiungere il servizio nell'elenco elementi consentiti. |
{: caption="Tabella 16. Richieste" caption-side="top"}

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
    "_id": "2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "name": "Service Broker's name",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "proxy_broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "auth_username": "username",
    "created_on": "2016-09-30T16:45:56.304Z"
}
```
{: screen}

## Eliminazione di un servizio

Utilizza i seguenti esempi di API e codice per eliminare un servizio.


{: #ld_table17}

| **Nome** | **Descrizione** |
|-----------------|-------------------|
| name | Nome del broker dei servizi. Questo nome non può essere modificato dal nome con cui è stato creato il servizio. |
{: caption="Tabella 17. Parametro" caption-side="top"}

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

### Gestione degli utenti con la CLI cf
{: #usingadmincli}

Puoi gestire gli utenti per il tuo ambiente {{site.data.keyword.Bluemix_notm}}
utilizzando l'interfaccia riga di comando Cloud Foundry insieme al plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI. Devi scaricare questo plug-in per la tua CLI Cloud Foundry.

Prima di iniziare, installa l'interfaccia riga di comando cf. Il plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI richiede cf versione 6.11.2 o successive. [Scarica Cloud Foundry command line interface ![Icona link esterno](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}.

**Limitazione:** l'interfaccia riga di comando Cloud Foundry non
è supportata da Cygwin. Utilizza l'interfaccia riga di comando Cloud Foundry
in una finestra riga di comando diversa da quella di Cygwin.

#### Aggiunta del plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI

Dopo aver installato l'interfaccia riga di comandi cf, puoi
aggiungere il plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI.

**Nota**: se avevi già installato il plug-in Gestione {{site.data.keyword.Bluemix_notm}}, per ottenere gli ultimi aggiornamenti potresti doverlo disinstallare, eliminare il repository e reinstallare il plug-in.

Completa la seguente procedura per aggiungere il repository e installare
il plug-in:

<ol>
<li>Per aggiungere il repository del plug-in Gestione {{site.data.keyword.Bluemix_notm}}, immetti il seguente comando:<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;dominiosecondario&gt;</dt>
<dd class="pd">Dominio secondario dell'URL per la tua istanza {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>
</li>
<li>Per installare il plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI, immetti il seguente comando:<br/><br/>
<code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

Per visualizzare un elenco di sottocomandi disponibili dai plug-in installati, immetti il seguente
comando:

```
cf plugins
```
{: codeblock}

Per visualizzare un elenco dei gruppi di comandi disponibili per il plug-in {{site.data.keyword.Bluemix_notm}} Admin, immetti il seguente comando:

```
cf ba
```
{: codeblock}

Per ulteriore assistenza per un comando, utilizza l'opzione `-help`.

Per ulteriori informazioni su come utilizzare il plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI, vedi [{{site.data.keyword.Bluemix_notm}} admin](../cli/plugins/bluemix_admin/index.html).
