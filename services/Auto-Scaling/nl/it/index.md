{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introduzione al servizio {{site.data.keyword.autoscaling}}
{: #autoscaling}

*Ultimo aggiornamento: 18 gennaio 2015*

In {{site.data.keyword.Bluemix_notm}}, puoi gestire automaticamente
la capacità della tua applicazione. Utilizza il servizio {{site.data.keyword.autoscalingfull}} per aumentare o ridurre
		automaticamente la capacità di calcolo della tua applicazione. Il numero di istanze
		dell'applicazione viene regolato in modo dinamico in base alla politica {{site.data.keyword.autoscaling}} da te definita.
{:shortdesc} 

## Utilizzo del servizio {{site.data.keyword.autoscaling}} in {{site.data.keyword.Bluemix_notm}}
{: #as-service}

Per utilizzare il servizio {{site.data.keyword.autoscaling}}, completa la seguente procedura:

1. Sul Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic su *Aggiungi un servizio o una API* e seleziona quindi il servizio {{site.data.keyword.autoscaling}} dalla sezione DevOps del catalogo del servizio. Viene visualizzata una nuova finestra con una panoramica del servizio {{site.data.keyword.autoscaling}}.
2. Seleziona l'applicazione di cui vuoi eseguire il bind al servizio {{site.data.keyword.autoscaling}} e fai clic su
*Crea*. <br/>
*Ricorda:* puoi associare un solo servizio {{site.data.keyword.autoscaling}} a un'applicazione. Se l'applicazione è già associata a un altro servizio {{site.data.keyword.autoscaling}},
      non selezionare l'applicazione in questo passo. In caso contrario, otterrai l'errore CWSCV2004E.<br/>Viene visualizzata la finestra Prepara di nuovo applicazione.
3. Nella finestra Prepara di nuovo applicazione, fai clic su *Riprepara* per ripreparare l'applicazione prima di utilizzare il nuovo servizio {{site.data.keyword.autoscaling}} appena aggiunto. Una volta completata la ripreparazione dell'applicazione, puoi iniziare a configurare
						il servizio {{site.data.keyword.autoscaling}} per la tua applicazione.
4. Per configurare il servizio {{site.data.keyword.autoscaling}} per
un'applicazione, nell'interfaccia utente {{site.data.keyword.Bluemix_notm}},
fai clic su questa applicazione a cui è associato il servizio {{site.data.keyword.autoscaling}}.
5. Nella sezione dei servizi presente sul Dashboard, fai clic
						sull'icona *Auto-Scaling*.
6. Se non lo hai già fatto, definisci la politica {{site.data.keyword.autoscaling}} per l'applicazione facendo clic su *Crea politica {{site.data.keyword.autoscaling}}*.

Adesso puoi configurare la politica di {{site.data.keyword.autoscaling}},
			consultare le statistiche delle metriche o visualizzare la cronologia di scaling dell'applicazione.
<dl>
<dt>Configurazione della politica</dt>
<dd>Utilizza questa sezione per creare o modificare le regole di scalabilità per specificare le condizioni in cui alcune attività di ridimensionamento devono essere attivate.<ul>
<li> Per le applicazioni Liberty for Java™, puoi definire le regole di scalabilità per Heap JVM, Memoria e Velocità effettiva.
<li> Per le applicazioni Node.js, puoi definire le regole di scalabilità per la Memoria.
<li> Per le applicazioni Ruby, puoi definire le regole di scalabilità per la
Memoria.</ul>
*Nota:* puoi definire più regole di scalabilità per più di un tipo di metrica. Tuttavia, il servizio {{site.data.keyword.autoscaling}}
							non rileva i conflitti tra le politiche di scalabilità. Quando definisci la politica di scalabilità, devi accertarti che
							le diverse regole di scalabilità non siano in conflitto tra di loro. In caso contrario, potresti notare delle oscillazioni nel numero totale di istanze in quanto l'applicazione esegue in un primo minuto il ridimensionamento decrementare e in quello successivo il ridimensionamento incrementale.<br/><br/>
Se il carico di lavoro della tua applicazione cambia notevolmente tra l'ora di utilizzo massimo e l'ora di utilizzo minimo, puoi creare una pianificazione di scalabilità per gestirne i diversi requisiti durante i vari periodi di tempo. Utilizza il parametro Numero minimo di istanze specificato in una pianificazione per definire la linea di base del numero di istanze dell'applicazione, mentre le regole di scalabilità dinamica si applicano ancora alla pianificazione per attivare le azioni di ridimensionamento decrementale e incrementale. </dd>
<dt>Statistiche delle metriche</dt>
<dd>Visualizza le statistiche delle metriche per le istanze della tua applicazione. Puoi visualizzare le statistiche medie e selezionare una specifica istanza per
visualizzarne le statistiche.</dd>
<dt>Cronologia scaling</dt>
<dd>Visualizza la cronologia di scaling delle tue applicazioni.<ul>
<li> Settimana scorsa:
visualizza la cronologia di scaling della settimana scorsa.
<li> Mese scorso:
visualizza la cronologia di scaling del mese scorso.
<li> Intervallo personalizzato:
puoi impostare l'intervallo di tempo.</ul>
*Nota:* puoi filtrare il record di cronologia selezionando Stato scaling o Scaling decrementale/incrementale.</dd>
</dl>


## Campi della politica per il servizio {{site.data.keyword.autoscaling}}
{: #policyfields}

| Nome campo  | Descrizione |
|-------------|----------------------|
|*Numero massimo di istanze
consentito* |	Numero massimo di istanze dell'applicazione che è possibile
avviare. Se il numero corrente di istanze dell'applicazione è uguale a questo valore, il servizio {{site.data.keyword.autoscaling}} non eseguirà più il ridimensionamento
incrementale dell'applicazione. Numero minimo di istanze predefinito	Numero minimo di istanze dell'applicazione che è possibile avviare. Se il numero di istanze è uguale a questo valore, il servizio {{site.data.keyword.autoscaling}} non eseguirà più il ridimensionamento decrementale
dell'applicazione. |
| *Tipo di metrica*	| 	I tipi di metrica supportati che è possibile
monitorare. Per ulteriori informazioni, vedi la Tabella 2. |
| *Ridimensionamento incrementale* | 	Specifica la soglia che attiva un'azione di ridimensionamento incrementale e il numero di
istanze che vengono incrementate quando si attiva l'azione di ridimensionamento incrementale. |
| *Ridimensionamento decrementale* |	Specifica una soglia che attiva un'azione di ridimensionamento decrementale e il numero di
istanze che vengono diminuite quando si attiva l'azione di ridimensionamento decrementale. |
| *Finestra statistica* |	La durata del periodo di tempo trascorso in cui
i valori di metrica ricevuti vengono riconosciuti come validi. I valori di metrica sono validi solo se le date/ore rientrano in questo periodo. L'unità del parametro Finestra statistica è il secondo.  |
| *Durata violazione*	| La durata del periodo di tempo trascorso in cui potrebbe essere attivata un'azione di
scaling. Un'azione di scaling viene attivata quando i valori di metrica raccolti si trovano al di sopra della soglia
superiore o al di sotto della soglia inferiore più lunga del tempo specificato. L'unità del parametro Durata violazione è il secondo. |
| *Periodo di raffreddamento per lo scaling decrementale* | Dopo che si è verificata un'azione di scaling decrementale, le altre richieste di scaling vengono ignorate durante il periodo di tempo specificato dal parametro Periodo di raffreddamento per lo scaling decrementale. L'unità di questo parametro è il secondo. |
| *Periodo di raffreddamento per lo scaling incrementale*	| Dopo che si è verificata un'azione di scaling incrementale, le altre richieste di scaling vengono ignorate durante il periodo di tempo specificato dal parametro Periodo di raffreddamento per lo scaling incrementale. L'unità di questo parametro è il secondo. |
| *Fuso orario*	| Il fuso orario in cui si applica la pianificazione. |
| *Ora di inizio*  |	L'ora di inizio di una pianificazione ricorrente. |
| *Ora di fine*    |	L'ora di fine di una pianificazione ricorrente.	|
| *Ripetere per*	|	Il giorno in una settimana in cui si applica una pianificazione ricorrente. |
| *Numero minimo di istanze* |	Il numero di minimo di istanze che è possibile avviare per un'applicazione
durante il periodo di tempo specificato nella pianificazione. |
| *Data e ora di inizio* |	La data e ora di inizio della pianificazione impostata su una specifica
data. |
| *Data e ora di fine* |	La data e ora di fine della pianificazione impostata su una specifica data.	|

Tabella 1. Campi di politica nella politica di scalabilità

| Nome metrica | Descrizione | Tipo di metrica
supportata |
|-------------|----------------------| ------------------- |
| *Heap JVM* |	La percentuale di utilizzo della memoria heap JVM.	| Liberty for Java |
| *Memoria*   |	La percentuale di utilizzo della memoria.	|  Liberty for Java<br/> Node.js <br/> Ruby <br/> |
| *Velocità effettiva* | Il numero di richieste
elaborate al secondo.| Liberty for Java |
| *Tempo di risposta* |	Il tempo di risposta delle
richieste elaborate.	| Liberty for Java |

Tabella 2. Nomi delle metriche supportate

## Messaggi di errore
{: #errmsgs}
Questa sezione elenca i messaggi di avvertenza e di errore prodotti dal servizio {{site.data.keyword.autoscaling}}.
 
### CWSCV2004E Un altro servizio {{site.data.keyword.autoscaling}} è
già associato all'applicazione.
**Puoi associare un solo servizio {{site.data.keyword.autoscaling}} a un'applicazione. Questo errore si verifica quando vuoi associare il servizio {{site.data.keyword.autoscaling}} a un'applicazione già associata a un altro servizio {{site.data.keyword.autoscaling}}.**

Seleziona un'altra applicazione non associata a un altro servizio {{site.data.keyword.autoscaling}} e associa il
servizio {{site.data.keyword.autoscaling}} di destinazione a questa applicazione.
Se riscontri questo errore in tutti gli altri casi, contatta il supporto IBM.

### CWSCV6001E Il server API non è in grado di analizzare le stringhe JSON di input per la API: {0}.
**Si è verificato un problema durante l'analisi delle stringhe JSON di input.**

Controllare il documento relativo al JSON di input con la API e correggere l'errore in esso.

### CWSCV6002E Il server API non è in grado di analizzare le stringhe JSON di output per la API: {0}.
**Si è verificato un problema durante l'analisi delle stringhe JSON di input.**

Per ulteriori informazioni, rivolgersi all'amministratore di Cloud.

### CWSCV6003E Errore del formato delle stringhe JSON di input: {0} nel
JSON di input per la API: {1}.
**È stato rilevato un errore di formato durante l'analisi delle stringhe JSON di input.**

Controllare il documento relativo al JSON di input con la API e correggere l'errore in esso.

### CWSCV6004E Errore di formato delle stringhe JSON di output: {0}
nel JSON di output per la API: {1}.
**È stato rilevato un errore di formato durante l'analisi delle stringhe JSON di output.**

Per ulteriori informazioni, rivolgersi all'amministratore di Cloud.

### CWSCV6005E Si è verificato un errore server interno durante: {0}.
**Durante l'elaborazione della richiesta, si è verificato un errore server interno.**

Per ulteriori informazioni, rivolgersi all'amministratore di Cloud.

### CWSCV6006E Richiamo delle API CloudFoundry non riuscito: {0}
**Si è verificato un errore durante il richiamo delle API CloudFoundry.**

Per ulteriori informazioni, rivolgersi all'amministratore di Cloud.

### CWSCV6007E L'applicazione non è stata trovata: {0}
**L'applicazione non è stata trovata.**

Per ulteriori dettagli, controllare le informazioni sull'applicazione.

### CWSCV6008E Durante il recupero delle informazioni per l'applicazione
{0} si è verificato il seguente errore: {1}
**Recupero delle informazioni sull'applicazione non riuscito con qualche errore.**

Per ulteriori dettagli, controllare le informazioni sull'applicazione.

### CWSCV6009E Il servizio: {0} per l'applicazione {1} non è stato trovato.
**Non è stato possibile trovare il servizio per questa applicazione.**

Per ulteriori informazioni, controllare il binding di servizio per questa applicazione.

### CWSCV6010E Non è stato possibile trovare la politica per l'applicazione {0}
**Non è stato possibile trovare la politica per questa applicazione.**

Per ulteriori informazioni, controllare la configurazione dell'applicazione.

### CWSCV6011E L'autenticazione interna non è riuscita durante:
{0}
**Autenticazione interna non riuscita.**

Per ulteriori informazioni, rivolgersi all'amministratore di Cloud.


# rellinks
## esempi
* [Esercitazione: Make your application elastic on {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window}
* [Laboratori sull'architettura Cloud Foundry](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## sdk
* [API Rest di IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}}](https://www.{DomainName}/docs/api/content/api/auto-scaling/index.html){:new_window}

## generale
* [Listino prezzi di {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){:new_window}
* [Prerequisiti di {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){:new_window}
* [CLI {{site.data.keyword.autoscaling}}](../../cli/plugins/auto-scaling/index.html){:new_window}

