---

copyright:
  years: 2015,2016

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Connessione e visualizzazione dei tuoi dispositivi
{: #iotrtinsights_task}
*Ultimo aggiornamento: 11 febbraio 2016*

{{site.data.keyword.iotrtinsights_short}} utilizza {{site.data.keyword.iot_short}} per l'accesso ai dispositivi e il richiamo di dati. I dispositivi che connetti a {{site.data.keyword.iot_short}} vengono automaticamente connessi a {{site.data.keyword.iotrtinsights_short}}.
{: shortdesc}

Se stai connettendo un nuovo tipo di dispositivo, devi configurare anche lo schema messaggi per associare i punti dati del dispositivo, impostare le unità e denominare il tipo di dispositivo. Se i tuoi dispositivi sono di un tipo di dispositivo già configurato, i loro dati vengono automaticamente visualizzati nel dashboard.

## Aggiunta di un nuovo dispositivo
{: #iotrtinsights_subtask}

Per aggiungere un nuovo dispositivo:  
L'aggiunta di un nuovo dispositivo è un processo in due fasi. Aggiungi prima il dispositivo a {{site.data.keyword.iot_short}} e configuri quindi
la modalità di utilizzo e visualizzazione dei dati dispositivo da parte di {{site.data.keyword.iotrtinsights_short}}.
1. Aggiungi i dispositivi al tuo {{site.data.keyword.iot_short}}.
> **Suggerimento:** se hai distribuito l'applicazione telefonica Internet delle cose (IoT), un dispositivo iotphone è già stato aggiunto a *iot-phone-iotf-service* {{site.data.keyword.iot_short}} e puoi tralasciare questo passo.  

  Per aggiungere nuovi dispositivi al tuo {{site.data.keyword.iot_short}}, consulta la [documentazione di {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html) e le [ricette di connessione dispositivo {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/?post_type=tutorials&s=IoTF).
2. Configura il tuo dispositivo in {{site.data.keyword.iotrtinsights_short}}.  
  1. Accedi alla console {{site.data.keyword.iotrtinsights_short}} come un utente amministratore.
  9. Vai a **Dispositivi > Sfoglia dispositivi** e verifica che il tuo dispositivo appena aggiunto sia elencato.
  > **Suggerimento:** l'elenco dispositivi viene aggiornato dalla tua origine dati una volta al minuto. Fai clic su **Aggiorna** per aggiornare l'elenco dispositivi immediatamente.
  3. Vai a **Dispositivi > Gestisci schemi** e fai clic su **Aggiungi nuovo schema messaggi**.  
  4. Immetti un nome per lo schema messaggi, ad esempio:
  `Nuovo schema messaggi`.
  5. Fai clic su **Collega nuova origine dati** e seleziona l'origine dati e il tipo di dispositivo che corrisponde alla tua istanza e al tuo dispositivo {{site.data.keyword.iot_short}}. Facoltativamente, immetti un nome evento per raccogliere i dati solo per tale evento oppure lascia il carattere jolly `+` per raccogliere tutti gli eventi. Ulteriori informazioni su come identificare i tipi di evento per il tuo dispositivo sono disponibili [qui](#identify-datapoints "Identifica punti dati.").  
  >**Importante:** ogni schema messaggi deve avere una combinazione univoca di origine dati, tipo di dispositivo e nome evento. Per creare più di uno schema per una specifica combinazione di origine dati e tipo di dispositivo, specifica un nome evento univoco per ogni schema messaggi invece di utilizzare il carattere jolly `+` predefinito.   
  6. Aggiungi uno o più punti dati che vuoi includere nei dashboard del dispositivo.
    Puoi selezionare i punti dati da un dispositivo connesso oppure aggiungere punti dati manualmente. I punti dati disponibili sono definiti nel payload dei messaggi inviati da un dispositivo. Per informazioni sul formato del payload {{site.data.keyword.iot_short}}, consulta l'argomento [Payload del messaggio](https://docs.internetofthings.ibmcloud.com/messaging/payload.html "Payload del messaggio.") nella documentazione di {{site.data.keyword.iot_short}}.   
    > **Suggerimento:** puoi creare manualmente dei punti dati virtuali che modificano o combinano punti dati esistenti che sono di tipo Integer (numero intero) o Float (virgola mobile). Ad esempio, se il punto dati del dispositivo temp restituisce un valore della temperatura in Fahrenheit, e vuoi invece utilizzare Celsius, puoi creare un punto dati virtuale *temp_c* con la seguente funzione *temp_c=(temp-32)/1.8*. Puoi quindi utilizzare il punto dati *temp_c* virtuale invece del punto dati *temp* in tempo reale nelle tue condizioni della regola. Nei dashboard,
i punti dati virtuali sono identificati da una sottolineatura tratteggiata.    

  <dl>
  <dt>Seleziona dal dispositivo connesso</dt>
  <dd>
  <ol>
    <li>Fai clic su **Seleziona dal dispositivo connesso**.</li>  
    <li>Nella finestra di dialogo Aggiungi punti dati, seleziona uno o più punti dati da aggiungere e fai quindi clic su **OK**.</li>   
    <li>I punti dati selezionati vengono aggiunti con la descrizione impostata sul nome del punto dati. Fai clic sul punto dati nell'elenco per modificarlo e aggiungere attributi quali il tipo di sensore, il tipo di dati e il numero di posizioni decimali.</li>
  </ol>
  </dd>
  <dt>Aggiungi manualmente</dt>
  <p><b>Suggerimento:</b> per creare una [struttura di punti dati nidificata](schemas.html), aggiungi prima un punto dati che abbia il tipo di dati Parent (principale). Nella tabella dei punti dati, puoi quindi fare clic su ![icona Aggiungi secondario](images/add_child.png "Aggiungi secondario") per aggiungere uno o più punti dati secondari.</p>
  <dd>
  <ol>
    <li>Fai clic su **Aggiungi manualmente**.</li>
    <li>Seleziona **Punto dati in tempo reale** o **Punto dati virtuale**</br></li>
    <li>Definisci le seguenti informazioni sul punto dati:
    <ul>  
     <li> Punto dati - l'identificativo del punto dati da te [individuato nel dashboard {{site.data.keyword.iot_short}}](#identify-datapoints "Identifica endpoint."). Ad esempio:  
   `id`, `ts`, `lat`  </li>
     <li>Descrizione - una breve descrizione del punto dati. Questa descrizione viene utilizzata quando si visualizzano i punti dati nei dashboard.</li>
     <li>Funzione punto dati virtuale - aggiungi uno o più componenti per definire una funzione valida. Per mettere a punto la tua funzione, puoi utilizzare punti dati, valori numerici e operatori matematici come +, -, \*, / ( e ). </li>
     <li>Tipo di dati - il tipo di dati del punto dati:  
   `String` (stringa), `Integer` (numero intero), `Float` (virgola mobile) o `Parent` (principale).</li>
     <li>Tipo di sensore - seleziona, facoltativamente, come interpretare il punto dati nei dashboard. A seconda della combinazione di tipo e tipo di sensore, potrebbero essere disponibili delle opzioni di visualizzazione aggiuntive per i tuoi widget del dashboard. Per ulteriori informazioni sui tipi di sensore e sulle opzioni di visualizzazione,
consulta [Widget del dashboard](dashboards.html#dashboard-widget "Widget del dashboard").</li>
     <li>Icona punto dati - seleziona, facoltativamente, un'icona che rappresenta il punto dati nei widget del dashboard.</li>
     <li>Valore minimo/valore massimo - facoltativo, solo Integer (numero intero) e Float (virgola mobile); se viene immesso un valore minimo e uno massimo, i dati dispositivo possono essere visualizzati come un indicatore nei dashboard.</li>
     <li>Unità dati - facoltativo: l'unità dei dati del punto dati. Ad esempio:  
     `C`, `km/h`  </li>
     <li> Posizioni decimali - facoltativo, solo Float (virgola mobile): il numero di decimali da includere nei dati dispositivo.</li>
    </ul>
    </li>
  </ol>
  </dd>
  </dl>
   8. Fai clic su **OK** per creare lo schema messaggi.
   9. Vai a **Dispositivi > Sfoglia dispositivi** e fai clic sul dispositivo di nuova aggiunta per verificare che vengano visualizzati i dati dispositivo in tempo reale e che i punti dati siano associati correttamente.

## Identificazione di punti dati ed eventi nel dashboard {{site.data.keyword.iot_short}}.
{: #identify-datapoints}
   I punti dati e i tipi di evento per un dispositivo sono disponibili nel dashboard {{site.data.keyword.iot_short}}.
   >**Suggerimento:** se stai utilizzando l'applicazione telefonica Internet delle cose (IoT) come tuo dispositivo IoT, puoi utilizzare l'evento sensorData e i seguenti punti dati per configurare lo schema messaggi:
   >- d.id - ID dispositivo
   >- d.ts - data/ora
   >- d.lat - latitudine
   >- d.lng - longitudine
   >- d.ax - accelerazione X
   >- d.ay - accelerazione Y
   >- d.az - accelerazione Z
   >- d.oa - movimento alfa
   >- d.ob - movimento beta
   >- d.og - movimento gamma
   >dove d.*puntodati* indica che il punto dati è nidificato sotto un punto dati di tipo parent (principale) d nel payload del messaggio.

   1. Dal dashboard Bluemix, fai clic sul tile Internet delle cose.  
   >**Nota:** se stati utilizzando l'applicazione telefonica Internet delle cose (IoT), fai clic sul tile *iot-phone-iotf-service*.  
   2. Fai clic su **Avvia dashboard** per aprire il dashboard {{site.data.keyword.iot_short}}.
   3. Vai alla pagina **Dispositivi**.
   4. Fai clic sul tuo dispositivo per aprire la pagina dei dettagli del dispositivo.
     Scorri giù alla sezione **Informazioni sul sensore** per visualizzare un elenco degli eventi e dei punti dati disponibili per il dispositivo. Queste informazioni sono richieste quando configuri il dispositivo in {{site.data.keyword.iotrtinsights_short}}.
