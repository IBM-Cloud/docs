---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Amministrazione di {{site.data.keyword.iotdriverinsights_short}}
{: #1stanchor}
*Ultimo aggiornamento: 6 maggio 2016*


L'amministrazione di {{site.data.keyword.iotdriverinsights_full}} include la visualizzazione delle informazioni sul tenant e la reimpostazione della password del tenant, la configurazione dei parametri per il servizio e la gestione dei dati archiviati nel servizio.
{:shortdesc}

Puoi eseguire le attività di amministrazione utilizzando la Console di gestione di {{site.data.keyword.iotdriverinsights_full}}.

Per accedere alla Console di gestione:

1. Vai alla vista **Gestisci** della tua istanza del servizio.
2. Fai clic su **Avvia**. La **Console di gestione** viene visualizzata come una nuova finestra.
3. Immetti i tuoi *nomeutente* e *password*, come mostrato nella vista **Gestisci**, e fai quindi clic su **ACCEDI**.

## Visualizzazione delle informazioni sul tenant
{: #viewtenantinfo}

Dopo che hai eseguito l'accesso alla **Console di gestione**, puoi vedere la vista **Informazioni sul tenant** e le informazioni sul tenant.

## Reimpostazione della password del tenant
{: #resettenantpassword}

Nella vista **Informazioni sul tenant**, 

1. Fai clic su **REIMPOSTA**.
2. Nella finestra di dialogo di conferma, fai clic su **OK**.
La nuova password viene quindi visualizzata nella vista **Informazioni sul tenant**

## Configurazione dei parametri per il servizio
{: #configureparameters}

Fai clic su **Parametri** nel riquadro di navigazione. Vengono visualizzati la vista **Parametri** e i parametri.

Puoi modificare i parametri per modificare i risultati dell'analisi.

La seguente tabella descrive i parametri comportamentali:

|Categoria|Nome parametro|Descrizione|Valore predefinito|
|:-------:|:--------:|:--------|:-------:|
|Limite di velocità (km/h)|\-|Limite di velocità per ciascun tipo di strada. Se la velocità del veicolo supera questo valore sulla strada di ciascun tipo, il servizio la identifica come eccesso di velocità.|\-|
|Limite di velocità (km/h)|Autostrada|Limite di velocità per Autostrada|120|
|Limite di velocità (km/h)|Autostrada urbana|Limite di velocità per Autostrada urbana|90|
|Limite di velocità (km/h)|Strada primaria urbana|Limite di velocità per Strada primaria urbana|60|
|Limite di velocità (km/h)|Strada urbana|Limite di velocità per Strada urbana|40|
|Limite di velocità (km/h)|Altre|Limite di velocità per Altre|30|
|Limite di velocità (km/h)|Sconosciuta|Limite di velocità per Sconosciuta|120|
|Svolta|Velocità angolare (Min \- Max, gradi/s)|Il valore di velocità angolare normale nella svolta. Il valore minimo viene utilizzato come soglia per identificare il segmento di svolta. Il valore massimo viene utilizzato per rilevare un comportamento di svolta ad alta velocità.|10 \- 25|
|Svolta|Velocità media (km/h)|Velocità normale durante la svolta. Questo valore viene utilizzato per identificare i comportamenti nel segmento di svolta insieme ai valori di velocità angolare.|60|
|Guida in condizioni di affaticamento|Tempo di guida continua (s)|Se un veicolo viene guidato continuamente per un periodo superiore a questo valore, il servizio lo identifica come "Guida in condizioni di affaticamento".|10800|

La seguente tabella descrive i parametri di contesto:

|Categoria|Nome parametro|Descrizione|Valore predefinito|
|:-------:|:--------:|:--------|:-------:|
|Fuso orario dell'analisi|\-|Il fuso orario applicato per l'analisi |+00:00|
|Intervallo di tempo|\-|Questo valore definisce il tipo di periodo di tempo.|\-|
|Intervallo di tempo|Tempo diurno|Intervallo di tempo diurno|1030 \- 1730|
|Intervallo di tempo|Tempo notturno|Intervallo di tempo notturno|2030 \- 0700|
|Intervallo di tempo|Picco mattutino|Intervallo di tempo di picco mattutino|0700 \- 1030|
|Intervallo di tempo|Picco serale|Intervallo di tempo di picco serale|1730 \- 2030|
|Tipo di strada|\-|Questi valori vengono utilizzati per associare il valore di tipo di strada dell'utente nei dati di input alle classificazioni di
tipo di strada univoche per {{site.data.keyword.iotdriverinsights_short}}. Se non disponi di un
valore di Tipo di strada, puoi richiamarlo utilizzando l'API REST `getLinkInformation`, fornita
da **{{site.data.keyword.iotmapinsights_short}}**. Il valore di tipo di strada è archiviato in **properties > type** nella risposta. [JSON di esempio](#sampleJson) rappresenta la posizione di `type` nella risposta.|\-|
|Tipo di strada|Autostrada|Associazione del valore Tipo di strada ad Autostrada|1|
|Tipo di strada|Autostrada urbana|Associazione del valore Tipo di strada ad Autostrada urbana|2|
|Tipo di strada|Strada primaria urbana|Associazione del valore Tipo di strada ad Strada urbana primaria|3|
|Tipo di strada|Strada urbana|Associazione del valore Tipo di strada a Strada urbana|4|
|Tipo di strada|Altre|Associazione del valore Tipo di strada ad Altre|5|
|Soglia velocità (bassa \- alta, km/h)|\-|Questo valore definisce l'intervallo di velocità media per ciascun tipo di strada.|\-|
|Soglia velocità (bassa \- alta, km/h)|Autostrada|Intervallo di velocità media per Autostrada|55 \- 85|
|Soglia velocità (bassa \- alta, km/h)|Autostrada urbana|Intervallo di velocità media per Autostrada urbana|35 \- 65|
|Soglia velocità (bassa \- alta, km/h)|Strada primaria urbana|Intervallo di velocità media per Strada primaria urbana|20 \- 40|
|Soglia velocità (bassa \- alta, km/h)|Strada urbana|Intervallo di velocità media per Strada urbana|15 \- 35|
|Soglia velocità (bassa \- alta, km/h)|Altre|Intervallo di velocità media per Altre|10 \- 20|
|Soglia velocità (bassa \- alta, km/h)|Sconosciuta|Intervallo di velocità media per Sconosciuta|20 \- 60|


Per applicare le modifiche ai parametri:

1. Fai clic su **SALVA**. 
2. Nella finestra di dialogo di conferma, fai clic su **OK**.

I nuovi parametri vengono quindi applicati e diventano effettivi per il successivo lavoro inoltrato.

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

- Fai clic su **Gestione dati** nel riquadro di navigazione. Puoi vedere la vista **Gestione dati** e i dati dei risultati dell'analisi di quanto rilevato per le vetture.
- Puoi eliminare i dati facendo clic su **ELIMINA** in un record.
