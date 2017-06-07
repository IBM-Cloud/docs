---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Riutilizzo delle risorse Kibana per l'analisi dei log Bluemix
{:#k4_reuse_resource}

Per copiare una ricerca, una visualizzazione o un dashboard da uno spazio {{site.data.keyword.Bluemix}} a un altro, utilizza le funzionalità di esportazione e importazione disponibili in Kibana. Puoi copiare le risorse singolarmente o esportare tutte le risorse in Kibana.
{:shortdesc}

| Attività | Descrizione |
|------|-------------|
| [Copia una ricerca](k4_reuse_resource.html#k4_reuse_search) | Copia una ricerca tra gli spazi. |
| [Copia una visualizzazione](k4_reuse_resource.html#k4_reuse_visualization) | Copia una visualizzazione tra gli spazi |

Prendi in considerazione i seguenti scenari in {{site.data.keyword.Bluemix_notm}} per riutilizzare ricerche, visualizzazioni o dashboard: 

* Copia una risorsa tra gli spazi nella stessa organizzazione.

    Ad esempio, potresti voler copiare le visualizzazioni dal tuo spazio di sviluppo in {{site.data.keyword.Bluemix_notm}} al tuo spazio di preparazione.
    
* Copia una risorsa tra gli spazi di organizzazioni diverse nello stesso account.

    Ad esempio, potresti voler copiare le visualizzazioni da uno spazio nella tua organizzazione di sviluppo in {{site.data.keyword.Bluemix_notm}} a uno spazio nella tua organizzazione di preparazione.

* Copia una risorsa tra gli spazi della stessa organizzazione ma ubicati in regioni pubbliche diverse.

    Ad esempio, potresti voler copiare le visualizzazioni da uno spazio nell'organizzazione A in {{site.data.keyword.Bluemix_notm}} che si trova nella regione pubblica Stati Uniti Sud a uno spazio nella tua organizzazione A nella regione pubblica Regno Unito.



## Copia di una ricerca
{:#k4_reuse_search}

Completa la seguente procedura per copiare una ricerca tra gli spazi in {{site.data.keyword.Bluemix_notm}}:

1. Avvia Kibana dove è disponibile la ricerca che desideri copiare. 

    * Avvia Kibana dalla IU {{site.data.keyword.Bluemix_notm}}: il file di ricerca JSON che puoi esportare include i seguenti campi: *ID spazio* e *ID applicazione* per le applicazioni Cloud Foundry (CF) o *ID istanza* per i contenitori. Per ulteriori informazioni, vedi [Accesso al dashboard Kibana dal dashboard {{site.data.keyword.Bluemix_notm}}](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix).
    
    * Avvia Kibana da un browser: il file di ricerca JSON che puoi esportare include il campo *ID spazio*. Per ulteriori informazioni, vedi [Accesso al dashboard Kibana da un browser](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser).

2. Nella pagina *Impostazioni*, seleziona **Oggetti** e la scheda **Ricerche**. Seleziona quindi una ricerca e copia le seguenti informazioni:

    <table>
      <tbody>
        <tr>
          <th align="center">Campo di ricerca</th>
          <th align="center">Descrizione</th>
        </tr>
        <tr>
          <td align="left">gruppo</td>
          <td align="left"> ID spazio in cui viene applicata la ricerca per filtrare i dati.</td>
        </tr>
        <tr>
          <td align="left">titolo</td>
          <td align="left">Nome della ricerca.</td>
        </tr>
        <tr>
          <td align="left">versione</td>
          <td align="left">Versione della ricerca.</td>
        </tr>
      </tbody>
    </table>
   
3. Esporta la ricerca.

    1. Nella pagina Impostazioni, seleziona la scheda **Oggetti**.
    2. Nella scheda **Ricerche**, seleziona la ricerca che desideri esportare.
    3. Fai clic su **Esporta**.
    4. Salva il file JSON.

4. Nella IU {{site.data.keyword.Bluemix_notm}}, passa allo spazio in cui vuoi copiare la ricerca e verifica che l'applicazione CF o il contenitore sia disponibile e in esecuzione.
    
5. Avvia Kibana per lo spazio {{site.data.keyword.Bluemix_notm}} in cui vuoi importare la ricerca e ottieni quindi le seguenti informazioni:

    Dalla [IU Bluemix](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix):
    
    <table>
      <tbody>
        <tr>
          <th align="center">Campo di ricerca</th>
          <th align="center">Descrizione</th>
        </tr>
        <tr>
          <td align="left">ID spazio</td>
          <td align="left"> <ol><li> Nella pagina *Impostazioni*, seleziona la scheda *Indici*.</li> <br> <li>L'ID spazio viene incorporato nel modello di indice. Il formato del modello di indice è il seguente: `[logstash-3d8d2eae-SpaceID-]YYYY.MM.DD` dove *SpaceID* è l'ID dello spazio. Copia l'ID spazio.</li></ol></td>
        </tr>
        <tr>
          <td align="left">ID applicazione o ID istanza</td>
          <td align="left"><ul><li>Quando avvii Kibana dall'IU {{site.data.keyword.Bluemix_notm}}, la pagina *Rileva* si apre per impostazione predefinita. Ottieni l'ID applicazione o l'ID istanza dalla barra di ricerca nella pagina *Rileva*, ad esempio `application_id:d88d1f16-e9d9-4623-bce7-0348c88f5133`.</li> <br> <li>Quando avvii Kibana da un browser, seleziona il campo application_id o instance_id dall'elenco Campi nella pagina Rileva.</li></ul></td>
        </tr>
      </tbody>
    </table>

6. Modifica il file JSON di ricerca che hai esportato in un passo precedente. Sostituisci il valore dell'ID applicazione. 

    Il seguente JSON è un esempio di file JSON di ricerca. 
 
    <pre class="pre">
    [
  {
    "_id": "52edf6e6-5386-4235-8fb8-598de3b80f41_Dev",
    "_type": "search",
    "_source": {
      "columns": [
        "application_id",
        "source_id",
        "instance_id"
      ],
      "description": "",
      "group": "52edf6e6-5386-4235-8fb8-598de3b80f41",
      "hits": 0,
      "kibanaSavedObjectMeta": {
        "searchSourceJSON": "{\"index\":\"[logstash-52edf6e6-5386-4235-8fb8-598de3b80f41-]YYYY.MM.DD\",\"query\":{\"query_string\":{\"analyze_wildcard\":true,\"query\":\"application_id:4ae73dcd-1fc4-48f0-9dc7-425839040436\"}},\"highlight\":{\"pre_tags\":[\"@kibana-highlighted-field@\"],\"post_tags\":[\"@/kibana-highlighted-field@\"],\"fields\":{\"*\":{}},\"fragment_size\":2147483647},\"filter\":[{\"meta\":{\"negate\":false,\"index\":\"[logstash-52edf6e6-5386-4235-8fb8-598de3b80f41-]YYYY.MM.DD\",\"key\":\"application_id\",\"value\":\"4ae73dcd-1fc4-48f0-9dc7-425839040436\",\"disabled\":false},\"query\":{\"match\":{\"application_id\":{\"query\":\"4ae73dcd-1fc4-48f0-9dc7-425839040436\",\"type\":\"phrase\"}}}}]}"
      },
      "sort": [
        "@timestamp",
        "desc"
      ],
      "title": "Dev",
      "version": 1
    }
  }
]
    </pre>
    
    In questo file JSON di esempio, puoi modificare le seguenti variabili con le informazioni del nuovo spazio: 
    
    * SPACEID: sostituisci questa variabile con l'ID spazio del nuovo spazio.
    * NAME: sostituisci questa variabile se vuoi modificare il nome della ricerca nel nuovo spazio. Per mantenere lo stesso nome, non modificare questo valore.
    * APPID: sostituisci questa variabile con il valore application_id dell'applicazione CF o con l'ID istanza del contenitore nel nuovo spazio.
    
   <pre class="pre">
   [
  {
    "_id": "SPACEID_NAME",
    "_type": "search",
    "_source": {
      "columns": [
        "application_id",
        "source_id",
        "instance_id"
      ],
      "description": "",
      "group": "SPACEID",
      "hits": 0,
      "kibanaSavedObjectMeta": {
        "searchSourceJSON": "{\"index\":\"[logstash-SPACEID-]YYYY.MM.DD\",\"query\":{\"query_string\":{\"analyze_wildcard\":true,\"query\":\"application_id:APPID\"}},\"highlight\":{\"pre_tags\":[\"@kibana-highlighted-field@\"],\"post_tags\":[\"@/kibana-highlighted-field@\"],\"fields\":{\"*\":{}},\"fragment_size\":2147483647},\"filter\":[{\"meta\":{\"negate\":false,\"index\":\"[logstash-SPACEID-]YYYY.MM.DD\",\"key\":\"application_id\",\"value\":\"APPID\",\"disabled\":false},\"query\":{\"match\":{\"application_id\":{\"query\":\"APPID\",\"type\":\"phrase\"}}}}]}"
      },
      "sort": [
        "@timestamp",
        "desc"
      ],
      "title": "Dev",
      "version": 1
    }
  }
]
    </pre>

6. Importa il file JSON di ricerca in Kibana per il nuovo spazio.

    1. Nella pagina Impostazioni, seleziona la scheda **Oggetti**.
    2. Nella scheda **Ricerche**, seleziona il file JSON di ricerca che vuoi importare.
    3. Fai clic su **Importa**.

Puoi utilizzare la ricerca in Kibana per monitorare i dati disponibili per la tua applicazione nel nuovo spazio.


    
## Copia di una visualizzazione
{:#k4_reuse_visualization}

Completa la seguente procedura per copiare una visualizzazione utilizzata per l'analisi dei dati di un'applicazione da uno spazio a un altro:

1. Avvia Kibana per lo spazio in cui è disponibile la visualizzazione che desideri copiare. 

    * Avvia Kibana dalla IU {{site.data.keyword.Bluemix_notm}}: il file di ricerca JSON che puoi esportare include i seguenti campi: *ID spazio* e *ID applicazione* per le applicazioni Cloud Foundry (CF) o *ID istanza* per i contenitori. Per ulteriori informazioni, vedi [Accesso al dashboard Kibana dal dashboard {{site.data.keyword.Bluemix_notm}}](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix).
    
    * Avvia Kibana da un browser: il file di ricerca JSON che puoi esportare include il campo *ID spazio*. Per ulteriori informazioni, vedi [Accesso al dashboard Kibana da un browser](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser).
    
2. Copia la ricerca che è associata alla visualizzazione tra gli spazi. Per ulteriori informazioni, vedi [Copia di una ricerca tra gli spazi Bluemix](k4_reuse_resource.html#k4_reuse_search).

    Una visualizzazione utilizza una ricerca per filtrare i dati visualizzati. Una visualizzazione può essere collegata a una ricerca in modo che tutti gli aggiornamenti che apporti alla ricerca vengano eseguiti automaticamente o non collegati a una ricerca in modo che i soli dati disponibili per l'analisi siano i dati visualizzati al momento della creazione della visualizzazione.

    Quando copi una visualizzazione, indipendentemente dal suo stato collegato a una ricerca, dovrai copiare anche la ricerca associata ad essa. **Nota:** quando importi una visualizzazione nel nuovo spazio, la nuova visualizzazione viene collegata alla ricerca del nuovo spazio.
    
3. Nella pagina *Impostazioni*, seleziona **Oggetti** e la scheda **Visualizzazioni**. Seleziona quindi una visualizzazione e ottieni le seguenti informazioni: 

    <table>
      <tbody>
        <tr>
          <th align="center">Campo di visualizzazione</th>
          <th align="center">Descrizione</th>
        </tr>
        <tr>
          <td align="left">gruppo</td>
          <td align="left"> Valore dell'ID spazio in cui viene utilizzata la visualizzazione per analizzare i dati.</td>
        </tr>
        <tr>
          <td align="left">titolo</td>
          <td align="left">Nome della visualizzazione.</td>
        </tr>
        <tr>
          <td align="left">versione</td>
          <td align="left">Versione della visualizzazione.</td>
        </tr>
        <tr>
          <td align="left">savedSearchID</td>
          <td align="left">ID della ricerca che viene utilizzata per filtrare i dati visualizzati attraverso la visualizzazione. <br> Il valore ha il seguente formato: `SpaceID_SearchTitle` dove SearchTitle è il valore del campo *titolo* della ricerca. </td>
        </tr>
      </tbody>
    </table>
   

4. Esporta la visualizzazione.

    1. Nella pagina Impostazioni, seleziona la scheda **Oggetti**.
    2. Nella scheda **Visualizzazioni**, seleziona la visualizzazione che desideri esportare.
    3. Fai clic su **Esporta**.
    4. Salva il file JSON.
    
5. Nella IU {{site.data.keyword.Bluemix_notm}}, passa allo spazio in cui vuoi copiare la visualizzazione e verifica che l'applicazione CF o il contenitore sia disponibile e in esecuzione.
    
6.  Modifica il file di visualizzazione JSON della ricerca che hai esportato in un passo precedente. Sostituisci i valori di ID spazio e ID ricerca. 

    Il seguente JSON è un esempio di file JSON di visualizzazione. 

    <pre class="pre">
    [
  {
    "_id": "3d8d2eae-f3f0-44f6-9717-126113a00b51_test",
    "_type": "visualization",
    "_source": {
      "description": "",
      "group": "3d8d2eae-f3f0-44f6-9717-126113a00b51",
      "kibanaSavedObjectMeta": {
        "searchSourceJSON": "{\"filter\":[]}"
      },
      "savedSearchId": "3d8d2eae-f3f0-44f6-9717-126113a00b51_Default_9d222152-8834-4bab-8685-3036cd25931a",
      "title": "test",
      "version": 1,
      "visState": "{\"type\":\"line\",\"params\":{\"shareYAxis\":true,\"addTooltip\":true,\"addLegend\":true,\"showCircles\":true,\"smoothLines\":false,\"interpolate\":\"linear\",\"scale\":\"linear\",\"drawLinesBetweenPoints\":true,\"radiusRatio\":9,\"times\":[],\"addTimeMarker\":false,\"defaultYExtents\":false,\"setYExtents\":false,\"yAxis\":{}},\"aggs\":[{\"id\":\"1\",\"type\":\"count\",\"schema\":\"metric\",\"params\":{}}],\"listeners\":{}}"
    }
    }
    ]
    </pre>
    
    In questo file JSON di esempio, puoi modificare le seguenti variabili: 
    
    * SPACEID: sostituisci questa variabile con l'ID spazio del nuovo spazio.
    * NAME: sostituisci questa variabile se vuoi modificare il nome della visualizzazione nel nuovo spazio.
    * SEARCHID: sostituisci questa variabile con l'ID ricerca nel nuovo spazio. Questo è l'ID della query che viene utilizzata per filtrare i dati visualizzati attraverso la visualizzazione.
    
       <pre class="pre">
    [
  {
    "_id": "SPACEID_NAME",
    "_type": "visualization",
    "_source": {
      "description": "",
      "group": "SPACEID",
      "kibanaSavedObjectMeta": {
        "searchSourceJSON": "{\"filter\":[]}"
      },
      "savedSearchId": "SPACEID_SEARCHID",
      "title": "NAME",
      "version": 1,
      "visState": "{\"type\":\"line\",\"params\":{\"shareYAxis\":true,\"addTooltip\":true,\"addLegend\":true,\"showCircles\":true,\"smoothLines\":false,\"interpolate\":\"linear\",\"scale\":\"linear\",\"drawLinesBetweenPoints\":true,\"radiusRatio\":9,\"times\":[],\"addTimeMarker\":false,\"defaultYExtents\":false,\"setYExtents\":false,\"yAxis\":{}},\"aggs\":[{\"id\":\"1\",\"type\":\"count\",\"schema\":\"metric\",\"params\":{}}],\"listeners\":{}}"
    }
    }
    ]
    </pre>

8. Importa la visualizzazione.

    1. Nella pagina Impostazioni, seleziona la scheda **Oggetti**.
    2. Nella scheda **Visualizzazioni**, seleziona il file JSON di visualizzazione che vuoi importare.
    3. Fai clic su **Importa**.


Puoi utilizzare la visualizzazione in Kibana per monitorare i dati disponibili per la tua applicazione nel nuovo spazio.
    
