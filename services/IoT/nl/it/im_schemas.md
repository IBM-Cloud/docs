---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Crea schemi di tipo di dispositivi
{: #iotrtinsights_task}

Per utilizzare le funzioni {{site.data.keyword.iot_short}} come le regole e le azioni, devi creare uno schema per associare le proprietà del dispositivo ai nomi delle proprietà semplici da usare, impostare le unità di dati per le proprietà e specificare il tipo di messaggio da utilizzare con lo schema.
{: shortdesc}

**Importante:** gli schemi sono necessari per utilizzare le regole le azioni. Per informazioni, consulta [Analisi cloud](cloud_analytics.html#rules).

**Importante:** le funzioni di analisi vengono unite dal servizio {{site.data.keyword.iotrtinsights_full}} Se la tua organizzazione {{site.data.keyword.iot_short_notm}} viene utilizzata come origine dati per un'istanza {{site.data.keyword.iotrtinsights_short}} esistente, Cloud and Edge Analytics non è abilitato finché non siano state migrate le istanze {{site.data.keyword.iotrtinsights_short}} esistenti. Continuare ad utilizzare il dashboard {{site.data.keyword.iotrtinsights_short}} per le tue analisi finché non viene completata la migrazione. Per ulteriori informazioni, consulta il blog [IBM Watson IoT Platform blog ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://developer.ibm.com/iotplatform/2016/04/28/iot-real-time-insights-and-watson-iot-platform-a-match-made-in-heaven/){: new_window} in IBM developerWorks e i tuoi dashboard dell'istanza {{site.data.keyword.iotrtinsights_short}} esistenti.  

## Aggiunta di uno schema del dispositivo
{: #add_schema}

Per aggiungere uno schema:  
1. Vai a **Devices > Manage Schemas** e fai clic su **Add Schema**.  
2. Seleziona un tipo dispositivo da associare a questo schema del messaggio. **Importante:** può essere definito solo uno schema per tipo dispositivo.

3. Aggiungi una o più proprietà.  
    Puoi selezionare le proprietà dal dispositivo collegato, creare proprietà virtuali per modificare o da combinare a proprietà esistenti o aggiungere le proprietà manualmente.  

    **Suggerimento:** le proprietà disponibili sono definite nel payload dei messaggi inviati da un dispositivo. Per informazioni sul formato del payload {{site.data.keyword.iot_short}}, consulta l'argomento [Message payload](reference/mqtt/index.html#message-payloadl "Message payload.").   
  <dl>
  <dt>Aggiungi una proprietà manualmente</dt>
  <p><b>Suggerimento:</b> per creare una struttura della proprietà nidificata, aggiungi prima una proprietà con il tipo di dati Prent. Nella tabella delle proprietà, puoi quindi fare clic su ![icona Add child.](images/add_child.png "Add child") per aggiungere una o più proprietà child.</p>
  <dd>
  <ol>
    <li>Seleziona la scheda **Manual**.</li>
    <li>Definisci i seguenti dettagli della proprietà:
    <ul>  
      <li>Nome - Un nome descrittivo per la proprietà che viene utilizzato nei dashboard, menu e procedure guidate di {{site.data.keyword.iot_short}}.</li>
      <li>Tipo di dati - Il tipo di dati della proprietà:  
   `String`, `Integer`, `Float` o `Parent`.</li>
   <!--<li>Event - A specific event to collect data for. Leave blank to collect for all events.</li>-->
   <li>Proprietà - L'identificativo della proprietà, ad esempio:  
 `temp` o `speed`  </br> Per informazioni su come identificare la proprietà dai messaggi del dispositivo, consulta [Identifying properties for your devices](#identify-datapoints "Identify properties.").</li>
  <li>Unità di dati - Facoltativo: l'unità di dati della proprietà. Ad esempio:  
     `C` o `Mph`  </li>
     <li> Posizioni decimali - Facoltativo, solo float: il numero di numeri decimali da includere nel dati del dispositivo.</li>
    </ul>
    </li>
    <li>Fai cli su **Finish** per creare la proprietà.</li>
  </ol>
  </dd>
  <dt>Crea una proprietà virtuale</dt>
  <dd> Ad esempio, se la proprietà del dispositivo temp restituisce un valore per la temperatura in Fahrenheit e invece desideri utilizzare Celsius, puoi creare una proprietà virtuale *temp_c* che dispone della seguente funzione *temp_c=(temp-32)/1.8*. Puoi quindi utilizzare la proprietà *temp_c* virtuale invece della proprietà *temp* in tempo reale nelle tue condizioni della regola.  
  Per creare una proprietà virtuale:
  <ol>
    <li>Seleziona la scheda **Virtual Property**.</li>  
    <li>Definisci i seguenti dettagli della proprietà:
    <ul>
    <li>Nome - Un nome descrittivo per la proprietà che viene utilizzato nei dashboard, menu e procedure guidate di {{site.data.keyword.iot_short}}.</li>
    <li>Tipo di dati - Il tipo di dati della proprietà:  
 `Float` o `Integer`.</li>
 <li>Proprietà - Un identificativo della proprietà per la proprietà virtuale. Ad esempio:  
`temp_virt`</li>
    <li>Calcolo - Aggiungi uno o più componenti per definire una funzione valida. Puoi utilizzare le proprietà, i valori numerici e gli operatori matematici come +, -, \*, /, ( e ).  
    Fai clic su **Advanced** per una serie di formule da utilizzare con le serie di punti dati nei dispositivi edge. Per ulteriori informazioni sulle formule avanzate, consulta [Calcoli avanzati per le proprietà virtuali edge](im_vir_calculations.html).  
    **Importante:** le condizioni della regola che confrontano le proprietà virtuali basate sulle formule avanzate non sono supportate.</li>
    <li>Unità di dati - Facoltativo: l'unità di dati della proprietà. Ad esempio: `C` o `Mph`</li>
    <li> Posizioni decimali - Facoltativo, solo float: il numero di numeri decimali da includere nel dati del dispositivo.</li>
   </ul>
   </li>
   <li>Fai cli su **Finish** per creare la proprietà.</li>
  </ol>
  </dd>
  <dt>Seleziona le proprietà da un dispositivo collegato</dt>
  <dd>
  <ol>
    <li>Seleziona la scheda **From Connected**.</li>  
    <li>Seleziona una o più proprietà da aggiungere allo schema. Queste proprietà possono essere modificate per impostare gli attributi, come il nome o l'unità di dati.  
<!--**Important:** Each property must be unique for a schema. If you select multiple occurrences of the same property for different events, only one of the selected properties is added to the schema.</li>-->
  <li>Fai clic su **OK** per creare la proprietà.</li>
  </ol>
  </dd>
    <dd>Le proprietà selezionate vengono aggiunte e la descrizione è impostata sul nome della proprietà. Fai clic sulla proprietà nell'elenco per modificarla e aggiungi ulteriori attributi, come il tipo di sensore, il tipo di dati e il numero di posizioni decimali.</dd>
  </dl>
8. Fai cli su **Finish** per creare lo schema del messaggio.

## Identificazione delle proprietà per i tuoi dispositivi.
{: #identify-datapoints}
   Le proprietà per un dispositivo possono essere trovate nel dashboard {{site.data.keyword.iot_short}}.

1. Nel dashboard {{site.data.keyword.iot_short}}, vai a **Devices**.
2. Fai clic su un dispositivo per aprire una pagina che mostra i dettagli del dispositivo.
3. Scorri verso il basso fino alla sezione **Sensor Information** per visualizzare un elenco di proprietà disponibili per un dispositivo collegato.
