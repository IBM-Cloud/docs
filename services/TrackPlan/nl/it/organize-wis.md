---

 

copyright:

  anni: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Organizzazione e filtro degli elementi di lavoro {: #tp-organize}  

*Ultimo aggiornamento 29 aprile 2016*
{: .last-updated}

Il servizio {{site.data.keyword.trackplan}} comprende diverse opzioni per ordinare e organizzare i tuoi elementi di lavoro.
{: shortdesc}

##Filtro degli elementi di lavoro {: #tp-filteringwis}

Puoi filtrare gli elementi di lavoro in base a parole o valori per specifici attributi. 

L'opzione di filtro è supportata nelle seguenti viste:   
- Il mio lavoro
- Le mie sottoscrizioni
- Lavoro in entrata
- Backlog
- Pianificazione sprint
- Lavoro del team
- Tutti i lavori

Se digiti una parola, vengono mostrati i riepiloghi degli elementi di lavoro che contengono tale parola. Puoi anche filtrare gli elementi di lavoro in base a valori per specifici attributi. Per i dettagli, consulta la seguente tabella.

| Attributo |Esempio | 
|-------|-------|
|*Type  | `*Defect` |
|#Tag  | `#conference`| 
|@:Owner  | `@:jasmith`|
|$Priority|`$High`|
|!Severity|`!Major`|       
   

Puoi creare query che utilizzano un qualsiasi attributo dell'elemento di lavoro digitando il nome dell'attributo. Ad esempio, se immetti `Creato da`, vengono mostrate la sintassi e le opzioni della query. Puoi utilizzare degli operatori, quali "and", "or" e "not" nei criteri di filtro. Puoi anche includere delle operazioni complesse che nidificano più operatori utilizzando le parentesi. Per vedere degli esempi, fai clic sull'icona **Guida**.
![Icona Guida del filtro](images/filter_helpicon.png)

Quando fai clic sul campo **Filtra elementi di lavoro per parola chiave**, vengono mostrati gli operatori e i filtri che puoi utilizzare per creare query.

![Filtro con opzioni di completamento automatico](images/filterMenu2.png)

##Salvataggio delle viste personalizzate {: #tp-customviews}
Puoi creare viste personalizzate applicando dei filtri. Puoi quindi condividere le viste con il tuo team.    

1. Nel campo **Filtra elementi di lavoro**, digita la forma abbreviata di un tipo di attributo e un valore per quell'attributo, ad esempio `$high`. Alcune scelte di attributi vengono elencate automaticamente quando digiti la forma abbreviata, ad esempio *Type, $Priority e !Severity.
![Filtro con tipi di attributo e attributi](images/filterAttributes.png)
2. Fai clic su **SALVA**.
3. Fornisci un nome per la vista. 
4. Se vuoi che la vista personalizzata includa lo sprint che stai visualizzando, seleziona la casella di spunta per includere lo sprint. Nel seguente esempio, lo sprint Backlog verrà incluso nella vista "Backlog con priorità alta".
![Finestra di dialogo Salva vista personalizzata con sprint incluso](images/filterIncludeSprints.png)
5. Fai clic su **SALVA**. 
6. Se vuoi condividere le viste salvate con il tuo team, nella sezione Viste personalizzate fai clic sull'icona Condividi accanto alla vista Nuovo. Quindi, fai clic su **OK**.
![Freccia Condividi vista personalizzata](images/filterShare.png)

Le viste personalizzate restituiscono i risultati solo per lo sprint e lo stato corrente visualizzati. Se vuoi che la vista restituisca i risultati per più sprint o stati, fai clic sulla vista e modificala come necessario.

##Visualizzazione e organizzazione degli elementi di lavoro{: #tp-organizingwis}

- Per visualizzare gli elementi di lavoro di cui sei proprietario, vai alla vista Il mio lavoro. 
- Se usi spesso degli specifici elementi di lavoro, puoi contrassegnarli come preferiti facendo clic sulle icone Stella <img class="inline"  src="./images/star.gif" alt="Icona Stella">. Puoi quindi visualizzare tutti i tuoi elementi di lavoro preferiti nella vista I miei preferiti. Quando selezioni l'icona Stella per un elemento di lavoro, solo tu puoi vedere che è contrassegnato come preferito.  
- Per visualizzare tutti gli elementi di lavoro a cui hai sottoscritto, vai alla vista Le mie sottoscrizioni.
- Per visualizzare gli elementi di lavoro in base alla data di modifica, vai alla vista Il mio lavoro recente.
- Per visualizzare l'attività degli elementi di lavoro, vai alla vista Le mie attività. La sezione I miei eventi elenca gli elementi di lavoro in cui sei stato menzionato. La sezione Le mie sottoscrizioni elenca tutte le modifiche che si sono verificate negli elementi di lavoro a cui hai sottoscritto. 

##Valutazione degli elementi di lavoro {: #tp-triaging}

Quando un elemento di lavoro viene creato ma non assegnato a uno sprint, tale elemento viene mostrato nella vista Lavoro in entrata.
Non appena un elemento di lavoro viene assegnato a uno sprint, viene rimosso dalla vista Lavoro in entrata.

Nella vista Lavoro in entrata, puoi valutare gli elementi di lavoro in diversi modi: 
- Per rifiutare un elementi di lavoro, fai clic sull'icona **Elimina questo elemento** <img class="inline"  src="./images/trash.gif" alt="Icona Elimina questo elemento">. L'elemento di lavoro viene risolto e il suo stato passa a Non valido.
- Per accettare l'elemento di lavoro e assegnarlo al Backlog, fai clic sull'icona **Valuta su backlog** <img  class="inline" src="./images/triage.gif" alt="Icona Valuta su backlog">. Puoi quindi valutare l'elemento di lavoro rispetto agli altri elementi nella vista Pianificazione sprint e assegnare l'elemento di lavoro a uno sprint.
- Per assegnare l'elemento di lavoro a uno sprint, apri l'elemento e seleziona un valore dall'elenco **Pianificato per**.

![Valutazione degli elementi di lavoro nella vista Lavoro in entrata](images/incoming_work_attributes.png)  

Per ulteriori informazioni sulla gestione degli elementi di lavoro, [vedi Managing a project with Quick Planner](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.1/com.ibm.team.concert.tutorial.doc/topics/tut_quick_planner_lesson.html).
