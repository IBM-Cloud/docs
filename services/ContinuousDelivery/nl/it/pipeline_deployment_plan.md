---

copyright:
  years: 2017
lastupdated: "2017-4-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Personalizzazione dei piani di distribuzione per le pipeline composite
{: #tasks_overview}

In un piano di distribuzione di una pipeline composita, un'attività rappresenta alcune attività significative di business associate a una distribuzione software. Le attività sono definite nei piani di distribuzione.

{:shortdesc}

Molte attività hanno un punto di partenza, un punto di fine e una durata misurabile. Un'attività può essere di uno dei seguenti tipi:

<ul>
<li>Le attività manuali possono rappresentare tutte le attività associate a una distribuzione software, come esecuzione di un server offline o aggiornamento di un database.</li>
<li>Le attività UrbanCode Deploy rappresentano le applicazioni IBM&reg; UrbanCode&reg; Deploy. Puoi eseguire le applicazioni IBM UrbanCode Deploy con le attività di tipo IBM UrbanCode Deploy.</li>
<li>Le attività Continuous Delivery Pipeline rappresentano le istanze di {{site.data.keyword.deliverypipeline}}, che sono parte di {{site.data.keyword.contdelivery_full}}. Puoi gestire le tue istanze di {{site.data.keyword.deliverypipeline}} con questo tipo di attività.</li>
<li>Le attività ritardate rappresentano gli eventi critici che si verificano a un'ora precisa.</li>
<li>Le attività di intestazione sono elementi organizzativi. Ad esempio, potresti utilizzare un'attività di intestazione per identificare un gruppo di attività.</li>
</ul>

<!-- You can add tasks to deployment plans by creating tasks or you can import tasks from CSV files that are created by IBM UrbanCode Release or another application. You can also copy tasks from other deployment plans. See [Importing tasks](/docs/services/UCCR/UCCR_deployPlan.html#plan_importTasks) for information about the format of the CSV file. -->

## Creazione delle attività
{: #tasks_create}

Quando crei un'attività, seleziona il piano di distribuzione in cui desideri aggiungere l'attività. Per impostazione predefinita, le nuove attività sono inserite alla fine del piano di distribuzione. Dopo aver creato un'attività, puoi spostarla o copiarla e incollarla in un altro piano di distribuzione. Puoi anche creare dipendenze con altre [attività](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html#tasks_dependencies).

Dopo aver salvato un'attività, vengono visualizzate le icone di azione per l'attività. Puoi utilizzare le icone di attività per modificare lo stato dell'attività durante una distribuzione. Tutte le attività hanno l'icona di azione **Skip**. Le altre icone, come **Start**, vengono visualizzate quando il contenuto è appropriato per esse.

![](../UCCR/images/deploy-plan-intro.png "Piano di distribuzione tipico")

*Figura 1. Un piano di distribuzione con attività e icone di azione*

Ogni attività in un piano di distribuzione è contenuta in una riga separata. Le informazioni visualizzate per ogni attività sono descritte nella seguente tabella.

### Tabella 1. Proprietà attività

| Proprietà  | Descrizione  |
| ------------------ | ------------------ |
| Nome               |Nome attività       |
| Tipo               |Tipo di attività: manuale, Continuous Delivery Pipeline, ritardata, email, intestazione / nota, UrbanCode Deploy|             
| Stato             |Stato dell'attività: non avviato, completo, esisto negativo, saltato, non applicabile |
| Proprietario              |La persona a cui è assegnata l'attività                                                        |
| Ora di inizio  |L'ora di inizio o l'ora di inizio prevista in base all'avvio della pianificazione o alla durata prevista di altre attività        |
| Ora di fine               |L'ora in cui l'attività è stata risolta        |
| Durata               |La durata dall'avvio alla risoluzione dell'attività (in minuti)        |
| Dipendenze               |Il numero di attività prerequisite per l'attività e dipendenti da essa        |

---
Dopo aver aggiunto le attività ai piani di distribuzione, puoi gestirle in diversi modi:

   * Per spostare un'attività, trascinala in una nuova ubicazione.

   * Per copiare un'attività o un gruppo, fai clic sull'attività e sull'icona **Copy** <img class="inline" src="../UCCR/images/copy-group.png"  alt="icona copia">, posiziona il cursore dove vuoi inserire l'attività copiata e fai clic sull'icona **Paste** <img class="inline" src="../UCCR/images/paste-group.png"  alt="icona incolla">.

   * Per tagliare un'attività o un gruppo da un piano di distribuzione, fai clic sull'attività e su **Cut** <img class="inline" src="../UCCR/images/cut-group.png"  alt="icona taglia">.

   * Per eliminare un'attività, fai clic su di essa e su **Delete** <img class="inline" src="../UCCR/images/trash-group.png"  alt="icona elimina">. L'attività viene rimossa dal piano di distribuzione.

## Creazione di attività manuali
{: #tasks_manual}

Normalmente, le attività manuali rappresentano alcune attività associate a una release software che hanno un punto di partenza, un punto di fine e una durata misurabile.

Per creare un'attività manuale, completa la seguente procedura:

1. Nella pagina Deployment Plan Details, fai clic su **Create Task**. Per inserire un'attività in una posizione specifica nel piano, fai prima clic su **Create Task**, seleziona un'attività. La nuova attività viene inserita sotto l'attività selezionata.

1. Nella finestra Create Task, dall'elenco **Type**, seleziona **Manual**.

1. Nel campo **Name**, immetti un nome per l'attività.

3. Nel campo **Duration (minutes)**, immetti il numero di minuti che prevedi l'attività utilizzi per l'esecuzione fino al completamento. La durata stimata viene utilizzata per calcolare i tempi di distribuzione previsti.

3. Nell'elenco **Tags**, collega una tag all'attività. Puoi selezionare più tag. Per creare una tag, immetti il nome della tag nel campo dell'elenco.

3. Nell'elenco **Assigned groups and users**, assegna l'attività a un utente o gruppo. L'utente assegnato esegue l'attività durante la distribuzione.

3. Dall'elenco **Owner**, seleziona il proprietario dell'attività. Il proprietario predefinito è l'utente che ha creato l'attività. Viene visualizzato l'elenco **Owner** dopo che l'attività è stata assegnata a un utente o gruppo.    

5. Fai clic su **Salva**. L'attività viene inserita nel piano di distribuzione.

## Creazione di attività ritardate
{: #tasks_delayed}

Le attività di tipo ritardato rappresentano gli eventi cardine o critici durante una distribuzione. Con le attività ritardate, puoi assicurarti che le attività importanti si avviino all'ora prevista. Normalmente, le attività ritardate sono prerequisiti per le attività importanti.

Un'attività ritardata si avvia come è eleggibile per l'esecuzione e finisce all'ora specificata dall'utente. Un'attività del tipo ritardato avviata ha un ostato di "In Progress" finché raggiunge l'ora per cui è pianificata, quando il suo stato viene modificato in "Complete". Quando un'attività ritardata è completa, le attività che dipendono da essa iniziano l'esecuzione.

Per creare un'attività ritardata, completa la seguente procedura:

1. Nella pagina Deployment Plan Details, fai clic su **Create Task**. Se vuoi inserire un'attività in una posizione specifica nel piano, fai prima clic su **Create Task**, seleziona un'attività. La nuova attività viene inserita sotto l'attività selezionata.

1. Nella finestra Create Task, dall'elenco **Type**, seleziona **Delayed**.

1. Nel campo **Name**, immetti un nome per l'attività.

3. Nel campo **Time**, immetti o seleziona l'ora in cui l'attività dovrà essere stata completata.

3. Nell'elenco **Time Zone**, seleziona il fuso orario per il valore immesso nel campo **Time**.    

5. Fai clic su **Salva**. L'attività viene inserita nel piano di distribuzione.

## Creazione di attività di intestazione
{: #tasks_header}

Le attività di intestazione rappresentano gli elementi organizzativi che puoi aggiungere ai piani di distribuzione. Se crei un gruppo di attività, puoi identificare il gruppo con un'attività di intestazione. Le attività di intestazione possono avere dipendenze come qualsiasi altra attività.

<!-- When you import a deployment plan from IBM UrbanCode Release, segment tasks are bracketed by note-type Start Segment and End Segment tasks. Segment dependencies are represented by dependencies to End Segment tasks. -->

Per creare un'attività di intestazione, completa la seguente procedura:

1. Nella pagina Deployment Plan Details, fai clic su **Create Task**. Se vuoi inserire un'attività in una posizione specifica nel piano, fai prima clic su **Create Task**, seleziona un'attività. La nuova attività viene inserita sotto l'attività selezionata.

1. Nella finestra Create Task, dall'elenco **Type**, seleziona **Header**.

1. Nel campo **Name**, immetti un nome per l'attività. Il nome può rappresentare un nome del gruppo dell'attività.

3. Nel campo **Description**, immetti o incolla una descrizione. Puoi immettere una nota, un promemoria o altre istruzioni.

5. Fai clic su **Salva**. L'attività viene inserita nel piano di distribuzione.

## Creazione di attività Delivery Pipeline
{: #tasks_pipelineCD}

Nel servizio {{site.data.keyword.contdelivery_short}}, {{site.data.keyword.deliverypipeline}} automatizza i tuoi flussi di lavoro DevOps. Puoi gestire le tue istanze di {{site.data.keyword.deliverypipeline}} con le attività pipeline.

Per creare un'attività Delivery Pipeline, completa la seguente procedura:

1. Nella pagina Deployment Plan Details, fai clic su **Create Task**. Se vuoi inserire un'attività in una posizione specifica nel piano, fai prima clic su **Create Task**, seleziona un'attività. La nuova attività viene inserita sotto l'attività selezionata.

1. Nella finestra Create Task, dall'elenco **Type**, seleziona **Continuous Delivery Pipeline**.

1. Nel campo **Name**, immetti un nome per l'attività. Il nome può rappresentare un nome del gruppo dell'attività.

3. Nel campo **Description**, immetti o incolla una descrizione. Puoi immettere una nota, un promemoria o altre istruzioni.

3. Nel campo **Pipeline ID**, immetti o incolla l'ID della pipeline.

3. Nel campo **Stage Name**, immetti o incolla il nome della fase.

5. Fai clic su **Salva**. L'attività viene inserita nel piano di distribuzione.

## Gestione dei gruppi di attività
{: #tasks_groups}

Puoi combinare due o più attività in un gruppo di attività. Quando crei un gruppo, definisci il modello di esecuzione del gruppo, che è sequenziale o parallelo. Puoi eseguire le attività in un gruppo di modello parallelo in qualsiasi ordine e puoi eseguirle contemporaneamente a meno che non esistano dipendenze. Le attività in gruppi sequenziali vengono eseguite in ordine di elenco, iniziando con la prima o l'attività più in alto.

Puoi incorporare i gruppi in altri gruppi. Puoi incorporare un gruppo di modello sequenziale in un gruppo di modello parallelo e viceversa. Tuttavia, non puoi incorporare un gruppo di modello sequenziale in un altro gruppo sequenziale o incorporare un gruppo di modello parallelo in un altro gruppo parallelo.  

Per creare un gruppo di attività, completa la seguente procedura:

1. Nella pagina Deployment Plan Detail, seleziona due o più attività.

1. A seconda del tipo di gruppo che desideri creare, completa uno dei seguenti passi:

  <ul>
  <li>Per creare un gruppo parallelo, fai clic sull'icona **Parallel** <img class="inline" src="../UCCR/images/para-icon.png"  alt="icona gruppo parallelo">. Se non puoi creare un gruppo parallelo con le attività selezionata, l'icona è disabilitata. Ad esempio, potresti non essere in grado di creare un un gruppo parallelo se tutte le attività selezionate sono già in un gruppo parallelo.
  </li>
  <li>Per creare un gruppo sequenziale, fai clic sull'icona **Sequential** <img class="inline" src="../UCCR/images/seq-icon.png"  alt="icona gruppo sequenziale">.
  </li>
  </ul>

Il gruppo è formato e viene aggiunta una barra di selezione del gruppo al piano di distribuzione. Se hai selezionato attività non contigue, le attività formano un elenco contiguo che avvia l'attività selezionata più in alto.

La seguente figura mostra un gruppo parallelo. La barra di selezione del gruppo identifica il tipo di gruppo: parallelo <img class="inline" src="../UCCR/images/para-select.png"  alt="selezione gruppo parallelo"> o sequenziale <img class="inline" src="../UCCR/images/seq-select.png"  alt="selezione gruppo sequenziale">.

(![](../UCCR/images/group-select.png "Piano di distribuzione tipico"))

*Figura 2. Un gruppo parallelo*

Per spostare un gruppo, fai clic sulla **barra di selezione gruppo** o ovunque nel gruppo e trascinalo in una nuova posizione.

Per copiare un gruppo, selezionalo, fai clic sull'icona **Copy** <img class="inline" src="../UCCR/images/copy-group.png"  alt="icona copia">, posiziona il cursore dove vuoi inserire l'attività copiata e fai clic su **Paste** <img class="inline" src="../UCCR/images/paste-group.png"  alt="icona incolla">.

Per tagliare un gruppo, selezionalo e fai clic sull'icona **Cut** <img class="inline" src="../UCCR/images/cut-group.png"  alt="icona taglia">.

Per annullare il raggruppamento di un gruppo, selezionalo e fai clic sull'icona **Ungroup** <img class="inline" src="../UCCR/images/ungroup-icon.png"  alt="icona annulla gruppo"> nella barra di selezione del gruppo.

Per eliminare un gruppo, selezionalo e fai clic sull'icona **Delete** <img class="inline" src="../UCCR/images/trash-group.png"  alt="icona elimina">. Le attività vengono rimosse dal piano di distribuzione.

## Gestione delle tag attività
{: #tasks_tags}

Le tag sono elementi organizzativi che puoi aggiungere alle attività. Puoi filtrare i piani di distribuzioni con le tag. Ad esempio, durante una distribuzione a un ambiente di produzione, puoi disabilitare le attività che includono la tag `DEV_only`, che indica le attività sono solo per l'ambiente di sviluppo.

Per aggiungere una tag a un'attività, completa la seguente procedura:

1. Nella pagina Deployment Plan Details, seleziona un'attività o un gruppo di attività e fai clic su **Manage Tags**  <img class="inline" src="../UCCR/images/task-tag.png"  alt="gestione tag">. Puoi selezionare più attività e gruppi.

1. Nella finestra "Manage Tags for Selected Tasks", dall'elenco **Common Tags**, seleziona le tag. Puoi creare una tag immettendo un nome nella casella di testo dell'elenco.

1. Fai clic su **Salva**.

Le tag vengono visualizzate nelle righe dell'attività della pagina Deployment Plan Details. Nella seguente figura, l'attività Deploy WAR ha due tag: `Deployment` e `Critical`.

Le tag utilizzate da un piano di distribuzione vengono visualizzate nella scheda **Versions** della pagina Deployment Plan Details. Per rendere un'attività non applicabile per una distribuzione, cancella le tag dell'attività. Le attività con lo stato "Not Applicable" non possono essere avviate.  

![](../UCCR/images/task-tag-labels.png "Piano di distribuzione tipico")

*Figura 3. Tag attività*

## Creazione delle dipendenze dell'attività
{: #tasks_dependencies}

Puoi rendere un'attività un prerequisito di altre attività. Se un'attività è un prerequisito, un'attività dipendente non può essere avviata, anche se sono altrimenti eleggibili, finché l'attività prerequisita non è stata risolta.

Un'attività può avere più attività dipendenti e più attività prerequisite. Puoi definire le dipendenze per un'attività con qualsiasi altra attività nel piano di distribuzione. Tuttavia, non puoi creare dipendenze circolari. Ad esempio, non puoi rendere un'attività dipendente da un'attività che dipende a sua volta dalla prima attività.

Controllando le dipendenze dell'attività, puoi assicurarti che gli eventi si verifichino nel loro ordine previsto.

Per rendere un'attività un prerequisito di altre attività, completa la seguente procedura:

1. Nella pagina Deployment Plan Details, seleziona un'attività o un gruppo di attività e fai clic su **Manage Prerequisites** <img class="inline" src="../UCCR/images/task-depend.png"  alt="prerequisito attività">. Puoi selezionare più attività e gruppi.

1. Nella finestra "Manage Prerequisites for Selected Tasks", dall'elenco **Prerequisite tasks for selected tasks**, seleziona l'attività prerequisita.

1. Fai clic su **Salva**.

Le dipendenze dell'attività sono visualizzate nella colonna Dependencies nella pagina Deployment Plan Detail. Le frecce verso l'alto indicano i prerequisiti dell'attività; le frecce verso il basso le dipendenze dell'attività.

Nella seguente figura, la prima attività non ha alcun prerequisito e due attività dipendono da essa. La seconda attività ha un prerequisito e nessuna attività dipendente.

(![](../UCCR/images/plan-w-depend.png "Piano di distribuzione tipico"))

*Figura 4. Dipendenze dell'attività*

Per controllare o modificare le dipendenze, seleziona l'attività e fai clic su **Manage Prerequisites** <img class="inline" src="../UCCR/images/task-depend.png"  alt="prerequisito attività">.
