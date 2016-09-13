---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestione di Driving Behavior Analysis
{: #1stanchor}
Ultimo aggiornamento: 19 giugno 2016
{: .last-updated}

Gestisci la tua istanza del servizio {{site.data.keyword.iotdriverinsights_full}} utilizzando la console di gestione nel dashboard {{site.data.keyword.Bluemix_notm}}. Dalla console di gestione, puoi configurare i parametri per {{site.data.keyword.iotdriverinsights_short}} e gestire i dati memorizzati nel servizio. Puoi anche visualizzare le informazioni sul tenant e reimpostarne la password.

{:shortdesc}

## Avvio della console di gestione
{: #start-admin-console}

Per accedere alla console di gestione per il servizio {{site.data.keyword.iotdriverinsights_short}}:

1. Dal dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sul tile del servizio {{site.data.keyword.iotdriverinsights_short}}.
2. Seleziona la vista **Gestisci** della tua istanza del servizio.
Annota le credenziali di *nome utente* e *password*. Per accedere alla console di gestione, è necessario il tuo ID IBM, che potrebbe non essere uguale alle tue credenziali {{site.data.keyword.Bluemix_notm}}.
3. Fai clic su **Avvia** e, quando richiesto, immetti le tue credenziali di ID IBM.
4. Fai clic su **ACCEDI**. La **console di gestione** viene aperta in una nuova finestra.

## Gestione delle informazioni sul tenant
{: #viewtenantinfo}

Per visualizzare le informazioni sul tenant, fai clic su **Informazioni sul tenant**.

### Reimpostazione della password del tenant
{: #resettenantpassword}

Per reimpostare la password del tenant:

1. Dalla finestra **Informazioni sul tenant**, fai clic su **REIMPOSTA**.
2. Nella finestra di dialogo di conferma, fai clic su **OK**.
Una nuova password viene generata e presentata nella vista **Informazioni sul tenant**.
**Importante:** assicurati di aggiornare la password in tutte le tue applicazioni che accedono alla API {{site.data.keyword.iotdriverinsights_short}}.

## Configurazione dei parametri del servizio
{: #configureparameters}

I parametri del servizio controllano la modalità di analisi dei dati dei viaggi. Per modificare i parametri del servizio:

1. Apri la vista **Parametri** e regola i seguenti parametri del servizio, come richiesto:
  - Fai clic sulla scheda **Comportamento** e aggiorna i [parametri di comportamento di guida](#behavior_parameters) per adattarli alle tue esigenze.
  - Fai clic sulla scheda **Contesto** e aggiorna i [parametri di associazione del contesto](#context_parameters) per adattarli alle tue esigenze.
2. Fai clic su **SALVA**.
3. Fai clic su **OK**.

I valori di parametro aggiornati vengono applicati al successivo lavoro che viene inoltrato.

### Parametri di comportamento di guida
{: #behavior_parameters}

Le seguenti tabelle descrivono i parametri di comportamento di guida per le categorie che puoi configurare nella scheda **Comportamento**.

#### Impostazioni del limite di velocità

Puoi specificare il limite di velocità in km/h per ciascun tipo di strada. Se la velocità supera il valore di limite di velocità da te specificato per il tipo di strada, viene rilevato un eccesso di velocità.

|Nome del parametro|Descrizione|Valore predefinito (km/h)|
|:--------|:--------|:-------|
|Autostrada|Limite di velocità per un tipo di strada Autostrada|120|
|Autostrada urbana|Limite di velocità per un tipo di strada Autostrada urbana|90|
|Strada primaria urbana|Limite di velocità per un tipo di strada Strada primaria urbana|60|
|Strada urbana|Limite di velocità per un tipo di strada Strada urbana|40|
|Altri|Il limite di velocità per un tipo di strada classificato come 'Altri'|30|
|Sconosciuta|Limite di velocità per i tipi di strada Sconosciuta|120|

#### Impostazioni della svolta

|Nome del parametro|Descrizione|Valore predefinito|
|:--------|:--------|:-------|
|Velocità angolare (Min \- Max, gradi/s)|Il valore di velocità angolare normale di una svolta. Il valore minimo viene utilizzato come una soglia per identificare il segmento di svolta. Il valore massimo viene utilizzato per rilevare un comportamento di svolta ad alta velocità.|10 \- 25|
|Velocità media (km/h)|Velocità normale durante una svolta. Questo valore viene utilizzato per identificare i comportamenti in un segmento di svolta che ha dei valori di velocità angolare.|60|

#### Impostazioni di guida in condizioni di affaticamento

|Nome del parametro|Descrizione|Valore predefinito|
|:--------|:--------|:-------|
|Tempo di guida continua (s)|Il tempo massimo di guida continua consentito.|10800|


### Parametri di associazione di contesto
{: #context_parameters}

Le seguenti tabelle descrivono i parametri di associazione di contesto per le categorie che puoi configurare nella scheda **Contesto**.

#### Impostazioni di fuso orario e intervallo di tempo

Specifica il fuso orario e le ore per ciascun periodo di tempo.

|Nome del parametro|Descrizione|Valore predefinito|
|:--------|:--------|:-------|
|Fuso orario analisi|Il fuso orario applicato per l'analisi.  |+00:00|
|Tempo diurno|Intervallo di tempo diurno.|1030 \- 1730|
|Tempo notturno|Intervallo di tempo notturno.|2030 \- 0700|
|Picco mattutino|Intervallo di tempo di picco mattutino.|0700 \- 1030|
|Picco serale|Intervallo di tempo di picco serale.|1730 \- 2030|

#### Tipi di strada

I parametri dei tipi di strada vengono utilizzati per associare i valori di tipo di strada dei dati di input alle classificazioni di tipo di strada di {{site.data.keyword.iot4auto_short}}. Se non hai un valore di tipo di strada, puoi richiamarlo utilizzando la API REST "getLinkInformation", che è fornita da "{{site.data.keyword.iotmapinsights_short}}".

 Il valore di tipo di strada è memorizzato in "properties > type" nella risposta. Per un esempio che mostra la posizione di "type" nella risposta, consulta [Risposta JSON di esempio per `getLinkInformation`](#sampleJson).

 |Nome del parametro|Descrizione|Valore predefinito|
 |:--------|:--------|:-------|
|Autostrada|Valore di tipo di strada associato ad Autostrada.|1|
|Autostrada urbana|Valore di tipo di strada associato ad Autostrada urbana.|2|
|Strada primaria urbana|Valore di tipo di strada associato a Strada primaria urbana.|3|
|Strada urbana|Valore di tipo di strada associato a Strada urbana.|4|
|Altri|Valore di tipo di strada associato ad Altri.|5|

#### Soglia di velocità

I parametri di soglia velocità definiscono l'intervallo di velocità medio per ciascun tipo di strada in km/h. L'intervallo di velocità medio è l'intervallo tra il valore più basso e quello più alto specificati.

|Nome del parametro|Descrizione|Valore predefinito|
|:--------|:--------|:-------|
|Autostrada|Intervallo di velocità media per il tipo di strada Autostrada.|55 \- 85|
|Autostrada urbana|Intervallo di velocità media per il tipo di strada Autostrada urbana.|35 \- 65|
|Strada primaria urbana|Intervallo di velocità media per il tipo di strada Strada primaria urbana.|20 \- 40|
|Strada urbana|Intervallo di velocità media per il tipo di strada Strada urbana.|15 \- 35|
|Altri|Intervallo di velocità media per il tipo di strada Altri.|10 \- 20|
|Sconosciuta|Intervallo di velocità media per il tipo di strada Sconosciuta.|20 \- 60|

### Risposta JSON di esempio della API REST "getLinkInformation"
{: #sampleJson}

```
{
	"links": [{
		"internal_link_id": "32088220365736308",
		"external_link_id": "3846419005",
		...
		"properties": {
			"type": "5",
			...
		},
		...
	}]
}
```
{: screen}


## Gestione dei dati archiviati nel servizio
{: #managedata}

I dati di analisi degli autoveicoli, i dati di contesto e i risultati dell'analisi sono memorizzati nel servizio finché non vengono eliminati.

Per eliminare i dati memorizzati nel servizio:

1. Fai clic su **Gestione dati** per visualizzare i dati relativi all'analisi degli autoveicoli e ai risultati dell'analisi.
2. Seleziona un record e quindi, nel record, fai clic su **ELIMINA**.
