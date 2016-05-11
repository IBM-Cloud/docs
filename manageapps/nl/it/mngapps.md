---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

#Gestione delle applicazioni
{: #manageapps}

*Ultimo aggiornamento: 17 marzo 2015*

Puoi utilizzare il Dashboard nell'interfaccia utente {{site.data.keyword.Bluemix}} per visualizzare e gestire le tue applicazioni e i tuoi servizi, nonché per monitorare l'utilizzo delle risorse mediante i misuratori di quota.
{:shortdesc}

La sezione relativa alle applicazioni nel Dashboard fornisce delle informazioni di riepilogo per le applicazioni da te create. Le informazioni di riepilogo includono
nome, icona, URL, runtime e stato di esecuzione dell'applicazione,
oltre a istanze di servizio associate all'applicazione. Per indicare lo
stato di esecuzione di ogni applicazione vengono utilizzati colori diversi.

**Arrestato o Sconosciuto (grigio)**

  La tua applicazione è arrestata oppure lo stato è sconosciuto. L'icona grigia indica che l'applicazione è arrestata oppure che lo stato è sconosciuto.

**In esecuzione (verde)**

  La tua applicazione è in esecuzione. L'icona verde indica che l'applicazione è avviata e tutte le istanze sono in esecuzione.

*Numero* **in esecuzione (giallo)**

  L'applicazione è stata avviata ma non tutte le istanze sono in esecuzione. L'icona gialla indica che è in esecuzione meno del 100% delle istanze. Viene visualizzato il numero di istanze in esecuzione e il numero di istanze non riuscite.

**Non in esecuzione (rosso)**

  La tua applicazione non è in esecuzione. L'icona rossa indica che l'applicazione è avviata, ma nessuna istanza è
in esecuzione.

Nel catalogo {{site.data.keyword.Bluemix_notm}}, puoi visualizzare i servizi e gli starter disponibili. Puoi selezionare uno starter
per creare un'applicazione, eseguire il bind di un servizio e gestire l'applicazione. Dopo che un servizio è stato associato a un'applicazione, puoi gestire le istanze
di servizio esistenti associate all'applicazione corrente e creare
istanze di servizio per l'applicazione. Inoltre puoi eliminare l'associazione mediante bind o l'istanza di
servizio da un'applicazione oppure puoi scegliere un diverso piano
di servizio.

Per visualizzare ulteriori informazioni su un'applicazione, fai clic sulla tile per aprire la pagina Panoramica dell'applicazione.

**Nota:** puoi visualizzare le risorse di una sola organizzazione alla volta. Se sei un membro di più organizzazioni, puoi passare da un'organizzazione all'altra
facendo clic sull'icona **CAMBIA ORGANIZZAZIONE** accanto
all'organizzazione corrente visualizzata nell'intestazione del dashboard.

Quando
un'applicazione viene distribuita, puoi avviare, arrestare, riavviare
o (nel caso di applicazioni Web) modificare il numero di istanze e la quantità
di memoria utilizzata dall'applicazione. In questo momento, per le applicazioni Web, {{site.data.keyword.Bluemix_notm}} non
dimensiona automaticamente la tua applicazione in base al suo carico, quindi
devi essere tu a gestire questo aspetto.

Le applicazioni possono essere ridistribuite
se viene eseguito un aggiornamento. Il meccanismo di aggiornamento dell'applicazione è
uguale al meccanismo utilizzato per la sua originale distribuzione. {{site.data.keyword.Bluemix_notm}} arresta
tutte le istanze in esecuzione e le sostituisce con le nuove istanze automaticamente.
