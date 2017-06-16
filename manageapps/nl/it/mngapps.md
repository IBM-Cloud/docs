---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Dettagli dell'applicazione
{: #manageapps}

Il dashboard Applicazioni nella console {{site.data.keyword.Bluemix}} fornisce delle informazioni di riepilogo per le applicazioni da te create. Le informazioni di riepilogo includono nome, icona, URL, runtime, stato di esecuzione e istanze del servizio associate all'applicazione. 
{:shortdesc}

Dal dashboard Applicazioni, puoi visualizzare lo stato di ciascuna applicazione.

**Arrestato o Sconosciuto (grigio)**

  La tua applicazione è arrestata oppure lo stato è sconosciuto. L'icona grigia indica che l'applicazione è arrestata oppure che lo stato è sconosciuto.

**In esecuzione (verde)**

  La tua applicazione è in esecuzione. L'icona verde indica che l'applicazione è avviata e tutte le istanze sono in esecuzione.

*Numero* **in esecuzione (giallo)**

  L'applicazione è stata avviata ma non tutte le istanze sono in esecuzione. L'icona gialla indica che è in esecuzione meno del 100% delle istanze. Viene visualizzato il numero di istanze in esecuzione e il numero di istanze non riuscite.

**Non in esecuzione (rosso)**

  La tua applicazione non è in esecuzione. L'icona rossa indica che l'applicazione è avviata, ma nessuna istanza è in esecuzione.

Per visualizzare ulteriori informazioni su un'applicazione, fai clic sul nome per aprire la pagina Panoramica dell'applicazione.

Quando un'applicazione viene distribuita, puoi avviare, arrestare, riavviare o (nel caso di applicazioni Web) modificare il numero di istanze e la quantità di memoria utilizzata dall'applicazione. Attualmente, per le applicazioni Web, {{site.data.keyword.Bluemix_notm}} non dimensiona automaticamente la tua applicazione in base al suo carico, quindi devi essere tu a gestire questo aspetto.

Le applicazioni possono essere ridistribuite
se viene eseguito un aggiornamento. Il meccanismo di aggiornamento dell'applicazione è uguale al meccanismo utilizzato per la sua originale distribuzione. {{site.data.keyword.Bluemix_notm}} arresta
tutte le istanze in esecuzione e le sostituisce con le nuove istanze automaticamente.
