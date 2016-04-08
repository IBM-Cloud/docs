---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# gestione di dashboard e template {: #managing-dashboards}

I dati in tempo reale dai tuoi dispositivi IoT sono visualizzati in dashboard personalizzabili. Puoi creare manualmente dei dashboard che visualizzano metriche in tempo reale, mostrano grafici e visualizzano altre informazioni per uno o più dispositivi. I dashboard possono anche contenere degli elenchi filtrati di dispositivi e dei collegamenti ad altri dashboard.
{: shortdesc}

Oltre ai dashboard creati manualmente, {{site.data.keyword.iotrtinsights_short}} viene fornito con un dashboard degli avvisi dispositivo predefinito in **Dashboard > Panoramica** e crea dinamicamente dei dashboard dispositivo basati sugli schemi di messaggio da te creati.

## Dashboard {: #dashboards}

Gli amministratori possono creare dei nuovi dashboard e modificare quelli esistenti per visualizzare i dati di interesse dei dispositivi.  
Per creare un dashboard:
1.	Vai a **Dashboard > Sfoglia dashboard**.
2.	Fai clic su **Aggiungi nuovo dashboard**.
3.	Dai un nome al dashboard e seleziona gli attributi, come l'icona e il background. Seleziona anche se rendere modificabile questo dashboard agli utenti operatori di {{site.data.keyword.iotrtinsights_short}}.
4.	Fai clic su ![icona Crea.](images/create.png "Icona Crea").
5.	Fai clic sul tile del nuovo dashboard per aprire il dashboard vuoto.
6.	Per aggiungere dei widget al dashboard:  
 1.	Fai clic su **Aggiungi nuovo componente** per aggiungere un widget di dashboard iniziale.
 2.	Seleziona un componente da aggiungere quindi seleziona ulteriori attributi componente e, se necessario, seleziona le proprietà di visualizzazione.Ad esempio, per visualizzare il valore numerico di uno specifico punto dati per un dispositivo, seleziona `Dispositivo` e seleziona quindi il
dispositivo da aggiungere. Nell'editor di dashboard, sotto Visualizzazione, seleziona un punto dati da visualizzare. Posiziona quindi il widget appena aggiunto nella griglia del dashboard.
 3.	Fai clic su ![icona Crea.](images/create.png "Icona Crea") per aggiungere il widget al dashboard.
7.	Il dashboard viene aggiornato con i widget appena aggiunti e visualizza i dati in tempo reale definiti dal punto dati selezionato.

>**Suggerimento:** per creare un dashboard che elenca tutti i tuoi dispositivi, procedi nel seguente modo:  
1. Vai a **Dashboard > Sfoglia dashboard** e fai clic su **Aggiungi nuovo dashboard**.
2. Dai al dashboard un nome descrittivo, come `Tutti i dispositivi`, e fai clic su ![icona Crea](images/create.png "Icona Crea").
3. Nel pannello dei dashboard, fai clic sul dashboard e fai quindi clic su **Aggiungi nuovo componente**.
4. Seleziona il componente **Contenitore** e seleziona **Dispositivi filtrati** per creare un elenco di tutti i tuoi dispositivi.
5. Fai clic su ![icona Crea.](images/create.png "Icona Crea").  

>I tuoi dispositivi sono elencati nel nuovo dashboard. Fai clic su un'icona di dispositivo per aprire il dashboard del dispositivo e visualizzare i dati in tempo reale per il dispositivo.
### Widget del dashboard {: #dashboard-widgets}
I dashboard sono formati da widget che visualizzano dati in tempo reale da uno o più dispositivi. La modalità di funzionamento del widget dipende dal suo tipo, dal punto dati visualizzato e dal modo in cui il punto dati è configurato nello schema.  
Ad esempi, se aggiungi un widget dispositivo per un punto dati non elaborati ('raw'), il widget visualizza i dati non elaborati solo come una stringa.

Se, tuttavia, configuri il punto dati con un valore minimo e uno massimo, hai l'opzione di visualizzare un widget come un indicatore.

Puoi anche assegnare un tipo sensore (Sensor) per il punto dati per abilitare un tipo speciale di widget di visualizzazione per illustrare meglio il tipo di dati sensore visualizzato. Ad esempio, puoi selezionare il tipo di sensore `Luce accesa/spenta` per abilitare un widget di visualizzazione `Indicatore luminoso normale (acceso/spento)`.

Disponi anche dell'opzione di includere diversi widget per lo stesso punto dati nello stesso dashboard per visualizzare sia il valore numerico non elaborato sia l'umidità fianco a fianco.![Più widget per lo stesso punto dati.](images/widgets.svg "Icona di più widget per lo stesso punto dati")  
*Tre opzioni di visualizzazione per lo stesso punto dati.*


Widget | Tipo e visualizzazione
------------- | -------------
Dispositivo  | Dati - valore in tempo reale dei punti dati per il dispositivo. Se il punto dati è configurato per includere un valore minimo e uno massimo, le opzioni di visualizzazione includono la presentazione del punto dati come un indicatore. Inoltre, se il punto dati è configurato con un tipo di sensore, sono disponibili delle opzioni di visualizzazione aggiuntive.
Grafico | Grafico - traccia valori in tempo reale di punti dati per uno o più dispositivi.
Dashboard | Link a un dashboard o a un template.
Testo | Casella di testo - testo formattato.
Contenitore | Tipi di widget contenitore:<ul><li>Tutti i dashboard - un elenco collegato di tutti i dashboard.</li><li>Dispositivi filtrati - un elenco di tutti i dispositivi oppure filtrati in base a nome o ubicazione.</li><li>Dispositivi filtrati con avvisi - un elenco di tutti i dispositivi con gli avvisi oppure filtrati in base a nome o ubicazione.</li><li>Avvisi per dispositivo - un elenco di avvisi per un dispositivo selezionato in un contenitore Dispositivi filtrati con avvisi.</li></ul>
Speciale | Tipi di widget speciali:<ul><li>Associazione - un'associazione che individua il dispositivo selezionato.</li><li>Informazioni aggiuntive sul dispositivo - ulteriori informazioni sul dispositivo selezionato.</li></ul>

La seguente tabella riepiloga le opzioni di visualizzazione disponibili per i widget dispositivo se il punto dati selezionato è configurato con un attributo di tipo di sensore nello schema messaggi.

Tipo di sensore del punto dati | Opzioni di visualizzazione | Dettagli | Tipo di dati supportato
------------- | ------------- | -------------
Nessuna selezione | Valore normale | - | String/Integer/Float
Luce accesa/spenta | Indicatore luminoso normale (acceso/spento) | 0=spento | Integer
Interruttore attivo/disattivo | Indicatore interruttore normale (attivo/disattivo) | 0=disattivo | Integer
Sensore di temperatura | Indicatore di temperatura generico | N/D | Integer/Float
Controllo temperatura | Indicatore di temperatura generico | N/D | Integer/Float
Sensore di pressione | Indicatore di pressione normale | N/D | Integer/Float
Livelli batteria | Widget della batteria normale(bassa/carica) | 0=buona | Integer
Luminosità | Indicatore di luminosità (scuro/luminoso) | 0=scuro | Integer
Finestra aperta/chiusa | Stato finestra normale (aperta/chiusa) | 0=chiusa | Integer
Porta aperta/chiusa | Stato porta normale (aperta/chiusa) | 0=chiusa | Integer
Sensore di umidità | Stato umidità (asciutto/bagnato) | 0=asciutto | Integer
Consumo di energia | Indicatore di energia normale | N/D | Integer/Float
Contatore di energia | Valore normale | N/D | Integer/Float
Percentuale | Percentuale normale (0-100) | N/D | Integer/Float
Voltaggio | Indicatore voltaggio normale | N/D | Integer/Float
Corrente | Indicatore corrente normale | N/D | Integer/Float
Longitudine | Ubicazione dispositivo sul widget Speciale > associazione (è richiesto anche il widget Latitudine) | **Importante:** al punto dati utilizzato per il valore di longitudine deve essere assegnato il tipo di sensore Longitudine nello schema messaggi.  | Float
Latitudine | Ubicazione dispositivo sul widget Speciale > associazione (è richiesto anche il widget Longitudine) | **Importante:** al punto dati utilizzato per il valore di latitudine deve essere assegnato il tipo di sensore Latitudine nello schema messaggi.  | Float  


## Layout dei dashboard predefiniti
{{site.data.keyword.iotrtinsights_short}} viene fornito con dei dashboard predefiniti, un dashboard degli avvisi e dei dashboard di dispositivo.

Le seguenti tabelle descrivono i widget e il layout dei dashboard predefiniti.
### Dashboard Avvisi (Dashboard > Panoramica)
Questo dashboard è incluso con il prodotto e fornisce un elenco di dispositivi che hanno degli avvisi aperti. Puoi selezionare un dispositivo per visualizzare i dettagli sugli avvisi e puoi fare clic sull'icona del dispositivo per aprire un dashboard del dispositivo per visualizzare i relativi dati in tempo reale.

<table>
<thead>
<tr>
<th colspan="3">Dashboard Avvisi</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Contenitore: dispositivi con avvisi</td>
<td style="width:30%">Contenitore: avvisi per dispositivo</td>
<td style="width:30%">Speciale: informazioni sul dispositivo aggiuntive</td>
</tr>
<tr>
<td style="width:30%"></td>
<td style="width:30%"></td>
<td style="width:30%">Speciale: associazione</td>
</tr>
</tbody>
</table>

*Layout del dashboard Avvisi*

### Dashboard del dispositivo
Se fai clic su un'icona di dispositivo in un elenco dispositivi, viene aperto un dashboard a esso relativo. Quando un punto dati viene aggiunto allo schema messaggi, viene aggiunto anche come un widget nel template del dispositivo, che crea dinamicamente il dashboard del dispositivo. Gli amministratori possono aggiungere o rimuovere widget manualmente.

<table>
<thead>
<tr>
<th colspan="3">Dashboard del dispositivo</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Dispositivo: punto dati 1</td>
<td style="width:30%">Dispositivo: punto dati 2</td>
<td style="width:30%">Dispositivo: punto dati 3</td>
</tr>
<tr>
<td style="width:30%">Dispositivo: punto dati N</td>
<td style="width:30%"></td>
<td style="width:30%"></td>
</tr>
</tbody>
</table>

*Layout del dashboard del dispositivo predefinito*

### Esempio di dashboard: elenco di tutti i dispositivi
Il seguente dashboard include un elenco di tutti i dispositivi e fornisce le informazioni sul dispositivo quando ne selezioni uno dall'elenco.

<table>
<thead>
<tr>
<th colspan="3">Dashboard di elenco di tutti i dispositivi</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Contenitore: dispositivi filtrati (nessun parametro di filtro impostato)</td>
<td style="width:30%">Speciale: informazioni sul dispositivo aggiuntive</td>
<td style="width:30%"></td>
</tr>
</tbody>
</table>

*Layout del dashboard di elenco di tutti i dispositivi*

## Template {: #templates}
I template controllano il layout dei dashboard predefiniti per uno specifico tipo di dispositivo. Gli amministratori possono modificare questi template predefiniti in base alle tue esigenze. Ad esempio, un template predefinito include solo i punti dati generici. Puoi aggiungere grafici e altri componenti come necessario.

Ad esempio, un utente può accedere al dashboard del dispositivo predefinito per visualizzare i dati sul dispositivo di base e seguire quindi un link a un template creato manualmente che potrebbe contenere una serie completa di grafici in tempo reale. Crei un template in modo molto simile a come crei un dashboard.  

Per modificare un template predefinito:
1.	Vai a **Dashboard > Gestisci template**.
2.	Nel pannello Gestisci template, trova il tile del template e fai clic su ![icona Configura.](images/gear.png "Icona Configura")** > Modifica layout** per aprire il template per la modifica.  
3.	Aggiungi i widget al template.
 1.	Fai clic su **Aggiungi nuovo componente template** per aggiungere un widget di template iniziale.
 2.	Seleziona un componente da aggiungere e seleziona quindi ulteriori attributi componente e, se necessario, seleziona le proprietà di visualizzazione.  
 3.	Fai clic su ![icona Crea.](images/create.png "Icona Crea") per aggiungere il widget al template.
4.	Modifica i widget esistenti.
 1.	Metti il puntatore del mouse su un widget del template e fai clic su ![icona Configura.](images/gear.png "Icona Configura").
 2.	Modifica il componente e i relativi attributi e riposiziona il widget come necessario.
 3.	Fai clic su ![icona Crea.](images/create.png "Icona Crea") per aggiornare il widget.  

Il template viene aggiornato con le modifiche da te specificate.

<!-- Administrators can also manually add templates for specific device types. These templates can then be linked to from the predefined templates.  -->

<!-- To create a template:
1.	Go to **Dashboards > Manage templates**.
2.	Click **Add new template**.
3.	Give the template a name, select a device type and attributes such as icon and background.
4.	Click ![Create icon.](images/create.png "Create icon").
5.	The empty template opens.
6.	Add widgets to the template.  
For a list of widgets, see below.
 1.	Click **Add new component** to add an initial template widget.
 2.	Select a component to add, then select further component attributes and, if needed, select display properties.
 For example, ... Then position the newly added widget in the dashboard grid.
 3.	Click ![Create icon.](images/create.png "Create icon") to add the widget to the template.
7.	The template updates with the newly added widgets.

### Template widgets
Widget | Type and visualization
------------- | -------------
Device | Data - Real-time value of data points for the device. For a description of the available widget options, see [Dashboard widgets](#dashboard-widgets "Dashboard widgets") above.
Chart | Graph - Plot real-time values of data points for one or more devices.
Dashboard | Link to a dashboard or a template.
Text | Text box - Formatted text
Container | Types of containers:<ul><li>All dashboards – A linked list of all dashboards</li><li>Filtered devices – A list of all devices, or filtered by name or location</li><li>Filtered devices with alerts – A list of all devices with alerts, or filtered by name or location</li><li>Alerts for device – A list of alerts for a device that is selected in a Filtered devices with alerts container</li></ul>
Special | Types of special:<ul><li>Map – A map that locates the selected device</li><li>Additional device information – More information about the selected device</li></ul>

### Template example: Selected set of graphs
One way of using device templates is to expand on the predefined device template by creating specialized templates for a device type, and then linking these from the predefined template by using a Dashboard widget.

<table>
<thead>
<tr>
<th colspan="3">Descriptive graphs template</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Device: ID</td>
<td style="width:30%">Graph: One data point</td>
<td style="width:30%">Graph: Another data point</td>
</tr>
<tr>
<td style="width:30%">Special: Additional device information</td>
<td style="width:30%">Text: Short description of how to <br>interpret the device data in the graphs.</td>
<td></td>
</tr>
</tbody>
</table>

*Descriptive graphs template*

Link to this template from a predefined device template:

<table>
<thead>
<tr>
<th colspan="3">Predefined device dashboard layout with link to template</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Device: Datapoint 1</td>
<td style="width:30%">Device: Datapoint 2</td>
<td style="width:30%">Device: Datapoint 3</td>
</tr>
<tr>
<td style="width:30%">Device: Datapoint N</td>
<td style="width:30%"><b>Dashboard: Descriptive graphs template</b></td>
<td style="width:30%"></td>
</tr>
</tbody>
</table>

*Predefined device dashboard layout with link to template* -->


## Reimpostazione di template e dashboard predefiniti {: #resetting-dashboards}
Se modifichi un template predefinito, il template non viene più aggiornato dinamicamente dagli aggiornamenti dello schema messaggi e devi reimpostare il dashboard o il template per ripristinare il layout e i widget originali.
Per reimpostare i template e i dashboard predefiniti:
1.	Vai a **Dashboard > Gestisci template** oppure a **Dashboard > Sfoglia dashboard**.
2.	Trova il tile del dashboard o del template predefinito e fai clic su **![icona Configura.](images/gear.png "Icona Configura") > Reimposta layout** per eliminare e quindi ricreare il template.  

Il template o il dashboard vengono ricreati con la serie predefinita di widget.
