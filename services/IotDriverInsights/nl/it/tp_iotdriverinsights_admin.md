---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestione di Trajectory Pattern Analysis
{: #tp_iotdriverinsights_admin}

Ultimo aggiornamento: 22 luglio 2016
{: .last-updated}

Per gestire il servizio Trajectory Pattern Analysis, usa la console di gestione nel dashboard {{site.data.keyword.Bluemix_notm}}. Dalla console di gestione, puoi configurare i parametri per Trajectory Pattern Analysis e gestire i dati memorizzati nel servizio. Puoi anche visualizzare le informazioni sul tenant e reimpostarne la password.

{:shortdesc}

## Avvio della console di gestione
{: #start-admin-console}

Per accedere alla console di gestione per il servizio Trajectory Pattern Analysis di {{site.data.keyword.iotdriverinsights_full}}

1. Nel dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sul tile del servizio {{site.data.keyword.iotdriverinsights_short}}.
2. Seleziona la vista **Gestisci** della tua istanza del servizio.
Annota le credenziali di nome utente e password perché ti serviranno in seguito. Per accedere alla console di gestione, è necessario il tuo ID IBM, che potrebbe non essere uguale alle tue credenziali {{site.data.keyword.Bluemix_notm}}.
3. Fai clic su **Avvia** e, quando richiesto, immetti le tue credenziali di ID IBM.
4. Fai clic su **ACCEDI**. Viene visualizzata la finestra **Console di gestione**.


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

I parametri del servizio controllano la modalità di analisi dei dati dei viaggi. Per modificare i parametri del servizio Trajectory Pattern Analysis:

1. Apri la vista **Parametri**.
2. Fai clic sulla scheda **Parametri di schema della traiettoria** e aggiorna i [parametri di analisi degli schemi di traiettoria](#tp_parameters) per adattarli ai tuoi requisiti.
3. Fai clic su **SALVA**.
4. Fai clic su **OK**.

I valori di parametro aggiornati vengono applicati al successivo lavoro che viene inoltrato.

### Parametri di soglia di supporto

La seguente tabella descrive i parametri di soglia di supporto che puoi configurare nella scheda **Parametri di schema della traiettoria**.

|Nome del parametro|Descrizione|Valore predefinito|
|:--------|:--------|:-------|
|Supporto minimo di numeri di viaggio per una O/D|I numeri di viaggio di supporto assoluti minimi necessari per uno schema O/D (Origine/Destinazione)|4 (deve essere maggiore di zero)|
|Supporto minimo di numeri di viaggio per una rotta|I numeri di viaggio di supporto assoluti minimi necessari per uno schema di rotta|2 (deve essere maggiore di zero)|

## Gestione dei dati dei risultati
{: #managedata}

I dati dei risultati generati dall'analisi del servizio Trajectory Pattern Analysis sono memorizzati nel sistema finché non li elimini.

Per eliminare i dati dei risultati:

1. Fai clic su **Gestione dati** > **Risultato dello schema di traiettoria**. Vengono visualizzati i dati dei risultati.
2. Seleziona un record e fai quindi clic su **ELIMINA**.
