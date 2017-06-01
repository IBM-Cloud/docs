---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Analisi cloud
{: #cloud_analytics}

Utilizzando le analisi cloud {{site.data.keyword.iot_short}}, specifichi le condizioni della regola basate sui dati del dispositivo in tempo reale e che attivano gli avvisi e le azioni facoltative quando incontrate.    
{: shortdesc}

Ad esempio, puoi creare una regola per assicurarti che quando viene eliminato un dispositivo o quando aumenta la temperatura del dispositivo, venga inviato un avviso al dashboard in un dispositivo dell'utente e che sia inviata una email all'amministratore.

## Prima di cominciare
{: #byb}
Assicurati che le proprietà del dispositivo che desideri utilizzare come le condizioni nelle tue regole siano state associate agli schemi. Consulta [Connessione dispositivi](iotplatform_task.html) e [Creazione di schemi](im_schemas.html) per ulteriori informazioni.

Inoltre, controlla la ricetta [Using Rules and Actions with {{site.data.keyword.iot_short}} Cloud Analytics ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){: new_window} per comprendere le regole e le azioni che vengono utilizzate in Cloud Analytics.

## Gestione delle regole e delle azioni  
{: #managing_rules}

Utilizza il dashboard **Rules** per creare e gestire le regole e le azioni per la tua organizzazione.

Per ottenere una panoramica delle regole e degli avvisi che sono stati attivati dai tuoi dispositivi, utilizza le seguenti tabelle:

 |Nome tabella | Descrizione |  
 |:---|:---|  
  |Analisi incentrata sulla regola | Visualizza le regole per la tua organizzazione. Ulteriori schede elencano gli avvisi attivati, i dispositivi associati, le proprietà del dispositivo e le informazione sull'avviso. |  
 |Analisi incentrata sul dispositivo | Visualizza i dispositivi collegati alla tua organizzazione. Ulteriori schede mostrano gli avvisi e le informazioni per un dispositivo selezionato, le proprietà del dispositivo e le informazioni sull'avviso. |

 Per ulteriori informazioni sulle tabelle di analisi predefinite, consulta [Visualizzazione dei dati in tempo reale utilizzando le tabelle e le schede](data_visualization.html#default_boards).


## Creazione di regole
{: #rules}

Le regole sono punti di decisione che corrispondono ai dati in tempo reale con valori di soglia predefiniti o altri dati della proprietà per attivare un avviso se viene riscontrata una condizione. In aggiunta all'avviso che viene visualizzato nel dashboard {{site.data.keyword.iot_short}}, puoi aggiungere una o più azioni per eseguire la logica di business quando viene attivata la regola.

**Importante:** prima di poter creare le regole per un tipo dispositivo, devi creare uno schema per il tipo dispositivo. Per informazioni, consulta [Crea schemi per il tipo dispositivo](im_schemas.html).

Per creare una regola:
1. Nel dashboard {{site.data.keyword.iot_short}}, passa a **Rules**.
2. Fai clic su **Create A Rule**, fornisci un nome e una descrizione per la regola, seleziona un tipo dispositivo a cui applicare la regola e quindi fai clic su **Next**.  
3. Per configurare la logica della regola, aggiungi una o più condizioni IF da utilizzare come trigger per la regola.  
Puoi aggiungere condizioni in righe parallele per applicarle come condizioni OR o puoi aggiungere le condizioni in colonne sequenziali per applicarle come condizioni AND.  
**Importante:** per attivare una condizione che confronta due proprietà o per attivare due o più condizioni della proprietà combinate sequenzialmente utilizzando AND, i punti dei dati di attivazione devono essere inclusi nello stesso messaggio del dispositivo. Se i dati sono ricevuti in più di un messaggio, la condizione o le condizioni in sequenza non vengono attivate.  
**Esempi:**  
Una regola semplice può attivare una avviso se un valore del parametro è maggiore di un valore specificato:
Condizione = `temp_cpu>80`  
Una regola più complessa può essere attivata quando viene soddisfatta una combinazione di soglie:
Condizione = `temp_cpu>60 AND cpu_load>90`   

4. Configura i requisiti di attivazione condizionali per la tua regola.  
Per controllare il numero di avvisi che vengono attivati per un regola in un intervallo di tempo, puoi configurare i requisiti di attivazione condizionali per la tua regola.  
**Importante:**  l'attivazione condizionale agisce su qualsiasi condizione nella regola. Ad esempio, se una regola ha cinque condizioni parallele differenti impostate utilizzando OR, ogni condizione che è true viene conteggiata nel numero di trigger condizionali.
Per impostare l'attivazione condizionale per un regola:
 1. Nell'editor della regola, fai clic sul link **Trigger each time conditions are met** predefinito per aprire la casella di dialogo per la configurazione dei requisiti della frequenza della serie.
 2. Seleziona e configura il trigger condizionale che desideri utilizzare nella regola.
 <ul>
 <li>Attiva ogni volta che le condizioni sono soddisfatte</li>
 <li>Attiva se le condizioni sono soddisfatte N volte in M *Unità di tempo*</li>
 </ul>  
 Per una descrizione più dettagliata dei trigger condizionali, consulta [Attivazione regola condizionale](#conditional "Panoramica attivazione condizionale").
5. Crea o seleziona una o più azioni che si verificano se vengono soddisfatte le condizioni della regola.  
Per ulteriori informazioni sulle azioni, consulta [Utilizzo delle azioni con le tue regole](#shared "Crea azioni").   
 Ad esempio: un azione può essere di inviare una email o di inserire un webhook.
3. **Facoltativo:** seleziona una priorità dell'avviso per la regola.  
 La priorità viene utilizzata per classificare gli avvisi che vengono visualizzati nella tabella **Rule-Based Analytics**. La priorità predefinita è bassa.
6. Quando sei soddisfatto della tua regola, fai clic su **Save** per salvare senza attivare o su **Activate** per salvare e attivare la regola.

La tua regola è stata creata. Se attivi la regola, quando vengono soddisfatte le condizioni della regola, viene aggiunto un avviso nella tabella **Boards > Rule-Based Analytics** e vengono eseguite tutte le azioni della regola.

## Attivazione regola condizionale
{: #conditional}

Per controllare il numero di avvisi che vengono attivati per un regola in un intervallo di tempo, puoi configurare i requisiti di attivazione condizionali per la tua regola.

A seconda della frequenza del messaggio e delle condizioni della regola, una regola può essere attivata molte volte dopo che è stata soddisfatta una condizione di attivazione. Ad esempio, se la condizione è `temp >= 90` e la temperatura aumenta e si stabilizza su 91, la regola viene attivata da qualsiasi messaggio in entrata. In base alla frequenza dei messaggi e alle azioni del dispositivo che la regola ha impostato di eseguire, questo volume di avvisi può velocemente riempire la casella posta in entrata o inviare una marea di feed Twitter con messaggi che non forniscono alcun valore aggiunto.

**Importante:**  l'attivazione condizionale agisce su qualsiasi condizione nella regola. Ad esempio, se una regola ha cinque condizioni parallele differenti impostate utilizzando OR, ogni condizione che è soddisfatta viene conteggiata nel numero di trigger condizionali.

Condizione | Descrizione
------------- | -------------
Attiva ogni volta che le condizioni sono soddisfatte | La regola viene attivata ogni volta che vengono soddisfatte le condizioni della regola.
Attiva se le condizioni sono soddisfatte *N* volte in *M* *giorni/ore/minuti/intervallo personalizzato* | La regola viene attivata quando vengono soddisfatte le condizioni *N* volte nell'intervallo di tempo selezionato e non viene riattivata nuovamente finché non trascorre l'intervallo di tempo selezionato. </br>Esempio: il requisito di attivazione condizionale =`Trigger only once if conditions are met 4 times in 30 minutes`. Il dispositivo invia un nuovo messaggio ogni cinque minuti. A mezzogiorno, la temperatura iniziale supera i 90 gradi, che soddisfa la condizione. Il contatore di attivazione condizionale viene avviato ma la regola non è ancora stata attivata.  Dopo 15 minuti e tre ulteriori messaggi che indicano che è stato ricevuto `temp > 90`, la regola viene attivata. La regola non viene quindi attivata per altri 15 minuti indipendentemente dalla temperatura.
Attiva solo la prima volta che vengono soddisfatte le condizioni e reimposta quando le condizioni non vengono più soddisfatte. | La regola viene attivata quando vengono soddisfatte le condizioni ma non viene attivata dei successivi messaggi che soddisfano le stesse condizioni. I criteri di attivazione sono reimpostati dal primo messaggio che non soddisfa le condizioni della regola.
Attiva se le condizioni sono soddisfatte per *M* *days/hours/minutes/custom*. | La regola viene attivata dopo l'intervallo di tempo selezionato se tutti i punti dati ricevuti durante l'intervallo di tempo soddisfano le condizioni o se non viene ricevuto alcun altro punto dati. L'intervallo di tempo avvia le condizioni inizialmente soddisfatte.



## Utilizzo delle azioni nelle tue regole
{: #shared}

In aggiunta alla visualizzazione degli avvisi nel dashboard degli avvisi, {{site.data.keyword.iot_short}} supporta diversi tipi di azioni di attivazione della regola, come l'invio di email e la pubblicazione di webhook.

Puoi creare le azioni direttamente nell'editor della regola o nella scheda delle azioni e quindi selezionare le azioni quando crei le tue regole.

Per creare un'azione nella scheda delle azioni:
1. Nel dashboard {{site.data.keyword.iot_short}}, passa a **Rules**.
2. Nel dashboard delle regole, seleziona la scheda **Actions**.
2. Fai clic su **Create An Action**, fornisci una descrizione e un nome per l'azione e seleziona un tipo di azione e fai quindi clic su **Next**.
3. Fornisci i parametri obbligatori per il tipo di azione che stai creando.  
Tipi di azione:  
 - [Send email](#email "Send email")
 - [IFTTT](#ifttt "IFTTT")
 - [Node-RED](#nodered "Node-RED")
 - [Webhook](#webhook "Webhook")
4. Fai clic su **OK** per creare una nuova azione.

L'azione è ora disponibile nell'editor della regola.

**Nota:** i seguenti esempi rappresentano tutti un'azione che invia una notifica a un ingegnere del servizio quando la temperatura, rappresentata dalla proprietà `temp_cpu` di un dispositivo, supera gli 80 gradi, utilizzando la seguente condizione della regola: `temp_cpu >= 80`

### Invia email  
{: #email}
Utilizza l'azione di invio email per inviare un email a uno o più recipienti quando viene attivata una regola.

Esempio: [Invia email](#emailex).

Vengono utilizzati i seguenti parametri per configurare ed inviare un'azione email:

Parametro | Descrizione
---|---
Nome | Il nome dell'azione, utilizzato nel dashboard degli avvisi
Descrizione | Una breve descrizione dell'azione.
Oggetto | La riga dell'oggetto dell'email. La riga dell'oggetto predefinita è "IBM Watson IoT Alert: Mail action".
A | Seleziona di inviare l'avviso soltanto a te stesso o a un elenco separato da virgole di indirizzi email. Se selezioni di inviare solo a te stesso, l'email viene inviata all'indirizzo email {{site.data.keyword.iot_short}} con cui hai eseguito l'accesso.
Cc | Nessuno o un elenco di indirizzi email separati da virgole.
Il corpo dell'email viene automaticamente creato dal messaggio del dispositivo nel momento in cui viene attivata la regola.  
**Importante:** per impostazione predefinita, le email non includono i dati del dispositivo che possono includere informazioni sensibili. Modifica l'impostazione **Include Data** per i includere i dati del dispositivo.

#### Esempio: utilizzo di invia email
{: #emailex}

In questo esempio, l'azione viene configurata per utilizzare la funzione di invio dell'email per inviare un'email all'ingegnere del servizio principale e per inviare una email di backup al suo manager.

Per creare l'azione email:
1. Nel dashboard {{site.data.keyword.iot_short}}, passa a **Rules**.
2. Fai clic su **Create An Action**.
4. Immetti il nome dell'azione `Send service request email`.
5. Immetti la descrizione `Send an email to the service engineer and his manager`.
3. Seleziona il tipo **Email**.
6. Nel campo A, seleziona **Specific people** e immetti `service.engineer@company.com`.
7. Nel campo CC, seleziona **Specific people** e immetti: `service.manager@company.com`.
8. Nella riga dell'oggetto, immetti: `Service required.`
10. Seleziona **Include Data** per includere i dati del dispositivo nell'email.
11. Fai clic su **Finish** per salvare l'azione.  


### IFTTT  
{: #ifttt}

Utilizza l'azione IFTTT per attivare una 'ricetta' IFTTT quando viene attivata una regola. Per ulteriori informazioni sull'attivazione delle azioni come 'ricette' IFTTT, consulta [Maker Channel ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://ifttt.com/maker){: new_window} nel sito IFTTT.

Esempio: [Utilizza IFTTT per pubblicare una scheda Trello](#iftttex).

Vengono utilizzati i seguenti parametri per configurare un'azione IFTTT:

Parametro | Descrizione
---|---
Nome | Il nome dell'azione, utilizzato nel dashboard degli avvisi.
Descrizione | Una breve descrizione dell'azione.
Chiave | La chiave del canale Maker da utilizzare per attivare l'evento.
Evento | Il nome dell'evento configurato come un trigger per l'evento Maker. Puoi creare più ricette con diversi trigger, ognuno con un nome evento differente.
Valore 1-3 | Puoi trasmettere tutto il contenuto in questi parametri, che vengono trasmessi all'azione nella tua ricetta IFTTT. **Suggerimento:** puoi utilizzare la [sostituzione della variabile](#variable_substitution) per includere dinamicamente ulteriori dati nell'intestazione.

#### Esempio: utilizza IFTTT per pubblicare una scheda Trello {: #iftttex}

In questo esempio, l'azione è configurata per utilizzare IFTTT per pubblicare una scheda in un elenco delle richieste del servizio in Trello.

Per creare il post di una scheda nell'azione Trello:
1.	In IFTTT, collegati al canale Trello.
2.	In IFTTT, collegati al canale Maker. Prendi nota della tua chiave IFTTT. Hai bisogno di questa chiave per collegarti a IFTTT da {{site.data.keyword.iot_short_notm}}.
5.	In IFTTT, crea una ricetta:
 1. Fai clic su **THIS**.
 2. Seleziona il canale **Maker**.  
 2. Fai clic su **Recieve a web request**.
 3. Immetti il nome evento `post-Trello-card`.
 4. Fai clic su **THAT**.
 5. Seleziona il canale **Trello**.
 6. Seleziona la scheda Trello in cui creare la scheda.
 7. Immetti un nome per l'elenco in cui aggiungere le schede.
 8. Modifica il titolo e la descrizione.
 9. Assegna i membri @service.engineer e @service.manager.
 8. Fai clic su **Create Action**.   
3. Nel dashboard {{site.data.keyword.iot_short}}, vai a **Rules > Actions** e crea una nuova azione che dispone dei seguenti parametri:
<ul>
<li>Tipo - **IFTTT**</li>
<li>Nome - `Post service request card`</li>
<li>Descrizione - `Use IFTTT to post a card in the service requests list in Trello.`</li>
<li>Chiave - La tua chiave IFTTT</li>
<li>Evento - `post-Trello-card`</li>
<li>Facoltativamente, aggiungi i valori per Valore 1-3. **Suggerimento:** puoi utilizzare la [sostituzione della variabile](#variable_substitution) per includere dinamicamente i dati del dispositivo.</li>
</ul>
4. Fai clic su **OK** per salvare l'azione.


### Node-RED
{: #nodered}

Utilizza l'azione Node-RED per collegarti a un'applicazione Node-RED quando viene attivata la regola. Per ulteriori informazioni sull'utilizzo di Node-RED, vedi [Creating apps with the Internet of Things starter application](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html).

Esempio: [Utilizza Node-RED per inviare un messaggio di testo](#noderedex).

Vengono utilizzati i seguenti parametri per configurare un'azione Node-RED:

Parametro | Descrizione
---|---
Nome | Il nome dell'azione, utilizzato nel dashboard degli avvisi.
Descrizione | Una breve descrizione dell'azione.
URL | L'URL del nodo di input HTTP di Node-RED di destinazione.
Nome utente | Da includere se richiesto dal servizio Node-RED.
Password | Da includere se richiesto dal servizio Node-RED. **Importante:** la password è inviata in cleartext.
Corpo | Per impostazione predefinita, il campo del corpo viene prepopolato con tutte le variabili elencate nella [sostituzione della variabile](#variable_substitution).

#### Esempio: utilizza Node-RED per inviare un messaggio di testo
{: #noderedex}

In questo esempio, l'azione è configurata per utilizzare Node-RED con un nodo Twilio per inviare un messaggio di testo all'ingegnere del servizio.

Per creare l'azione di invio del messaggio di testo:
1. In Twilio, individua o crea un nuovo servizio del messaggio da utilizzare per inviare i messaggi di testo dal tuo account Twilio. Per informazioni, consulta [Twilio documentation ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.twilio.com/help){: new_window}.
2. In Bluemix, configura e accedi al tuo account Node-RED con l'URL Node-RED `http://mynodered.mybluemix.net/red/`. Per ulteriori informazioni, consulta l'argomento [Creating apps with Node-RED Starter](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html) nella documentazione di Bluemix.
3. In Node-RED, crea un flusso a due nodi di esempio, come [RTI-alert]->[SMS].  
Dove il primo nodo è un nodo http e il secondo nodo è un nodo twilio.
 1. Aggiungi il nodo di input "http" e configuralo con i seguenti attributi:
  <ul>
  <li>Metodo - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>Nome - RTI Action</li>
  </ul>
  2. Aggiungi un nodo di output "http response" e collegalo ai nodi di input "http" unendo la porta di output di uno alla porta di input dell'altro.
  3. Aggiungi un nodo di output "twilio" e configuralo con i seguenti attributi:
  <ul>
  <li>Servizio - **Servizio esterno**</li>
  <li>Twilio - Aggiungi nuova twilio-api</li>
  <li>SMS a - `Numero di telefono dell'ingegnere del servizio`</li>
  <li>Nome - **SMS**</li>
  </ul>
  4. Collega i nodi tra loro  
  Collega i nodi http e twilio tra loro unendo la porta di output di uno alla porta di input dell'altro.
  5. Fai clic sul pulsante **Deploy** per distribuire il flusso al server
4. Nel dashboard {{site.data.keyword.iot_short}}, vai a **Rules > Actions** e crea una nuova azione che dispone dei seguenti parametri:
 - Tipo - **Node-RED**
 - Nome - `Send text using Node-RED and Twilio`
 - Descrizione - `Send a text message alert to the service engineer.`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - CORPO   
 ```json
 {"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iot_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}
 ```  
5. Fai clic su **Finish** per salvare l'azione.



### Webhook
{: #webhook}

Utilizza l'azione webhook per effettuare una richiesta HTTP al servizio web basato su webhook quando viene attivato un avviso. Ad esempio, un webhook può essere utilizzato per aprire una richiesta del servizio per un asset se un sensore nel dispositivo riporta una lettura anomala.

Esempio: [Utilizza webhook per pubblicare su Slack](#webhookex).

Vengono utilizzati i seguenti parametri per configurare un'azione webhook:

Parametro | Descrizione
---|---
Nome | Il nome dell'azione, utilizzato nel dashboard degli avvisi.
Descrizione | Una breve descrizione dell'azione.
URL | L'URL del server abilitato webhook di destinazione. **Suggerimento:** puoi utilizzare la [sostituzione della variabile](#variable_substitution) per includere dinamicamente ulteriori dati nell'URL.
Metodo | Il tipo di chiamata webhook da eseguire. Seleziona uno dei seguenti tipi: GET, HEAD, OPTIONS, PATCH, PUT, POST o DELETE.
Nome utente | Da includere se richiesto dal servizio web.
Password | Da includere se richiesto dal servizio web. **Importante:** la password è inviata in cleartext.
Intestazione | Le intestazioni sono formate dalla coppie di chiave valore. **Suggerimento:** puoi utilizzare la [sostituzione della variabile](#variable_substitution) per includere dinamicamente ulteriori dati nell'intestazione.
Tipo di contenuto | Il tipo di contenuto del corpo: JSON, XML, formato WWW codificato URL o testo semplice.  Disponibile per i metodi OPTIONS, PATCH, PUT, POST e DELETE.
Corpo | Il corpo della chiamata webhook.  Disponibile per i metodi OPTIONS, PATCH, PUT, POST e DELETE. Per impostazione predefinita, il campo del corpo viene prepopolato con tutte le variabili elencate nella [sostituzione della variabile](#variable_substitution). **Importante:** il server webhook può richiedere di includere alcuni campi specifici nel corpo. Ad esempio, un webhook Slack deve contenere il campo "text".   

#### Esempio: utilizza un webhook per pubblicare su Slack
{: #webhookex}

In questo esempio, l'azione è configurata per utilizzare un webhook per pubblicare un messaggio al canale Slack delle richieste per #servizio.

Per creare il post di un'azione slack:
1. In Slack, configura l'integrazione dei webhook in entrata per il canale delle richieste per #servizio. Prendi nota dell'URL dei webhook. Per ulteriori informazioni, consulta [Slack documentation ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://api.slack.com/incoming-webhooks){: new_window}.
2. Nel dashboard {{site.data.keyword.iot_short}}, vai a **Rules > Actions** e crea una nuova azione che dispone dei seguenti parametri:
 - Nome - `Post service request on Slack`
 - Tipo - **Webhook**
 - URL - `Your Slack webhooks URL`
 - Metodo - **POST**
 - Tipo di contenuto - `application/json`
 - Corpo   
 ```json
 {"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iot_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}
 ```  
  **Importante:** un webhook Slack deve contenere almeno il campo "text". Per informazioni, consulta [Incoming Webhooks ![icona link esterno](../icons/launch-glyph.svg)](https://api.slack.com/incoming-webhooks "Slack documentation"){: new_window} nella documentazione Slack.
11. Fai clic su **Finish** per salvare l'azione.


### Sostituzione della variabile  
{: #variable_substitution}

Includi le seguenti sostituzioni della variabile per includere dinamicamente i dati del dispositivo. La variabile deve essere racchiusa tra due parentesi graffe.

Variabile | Descrizione
---|---
**URL, intestazione e corpo** |
`{{timestamp}}` | La data/ora dal messaggio.
`{{orgId}}` | L'ID dell'organizzazione del servizio {{site.data.keyword.iot_short_notm}}.
`{{tenantId}}` | Obsoleto: l'ID del servizio {{site.data.keyword.iotrtinsights_full}}.
`{{deviceId}}` | L'ID del dispositivo.
`{{ruleName}}` | Il nome della regola che include l'azione.
`{{ruleID}}` | L'ID della regola che include l'azione.
**Solo il corpo** |
`{{ruleDescription}}`| La descrizione della regola che include l'azione.
`{{ruleCondition}}` | La condizione della regola che attiva l'azione.
`{{message}}` | Il messaggio del dispositivo non elaborato che include il valore del punto dati che attiva la regola.

## Ricette in Cloud Analytics

Le seguenti 'ricette' descrivono come utilizzare le funzioni Cloud Analytics in differenti casi di utilizzo:

- [Real Time Data Analysis Using IBM Watson™ IoT Platform Analytics ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/real-time-data-analysis-using-ibm-watson-iot-platform-analytics/){: new_window}

- [Predictive Analytics on IOT Sample Data ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/predictive-analytics-on-iot-sample-data/){: new_window}

- [Device List Card SIMPLIFIES Real Time Device Monitoring on WIoTP Dashboard ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/device-list-card-simplifies-real-time-device-monitoring-on-wiotp-dashboard/){: new_window}

- [Perform Actions in IBM Watson IoT Platform Cloud Analytics ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/perform-actions-in-ibm-watson-iot-platform-cloud-analytics/){: new_window}

- [Use IBM Data Science Experience to detect time series anomalies ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/recipes/tutorials/use-ibm-data-science-experience-to-detect-time-series-anomalies/){: new_window}
