---

copyright:
  years: 2016, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visualizzazione dei risultati

## Valutazioni Deployment Risk

Dopo aver eseguito una pipeline, {{site.data.keyword.DRA_short}} inizia a raccogliere e analizzare i risultati del test da essa per stabilire una linea di base. I dati di ogni successiva esecuzione sono raccolti e confrontati con i risultati precedenti. I gate di decisione utilizzano questi dati per determinare quando arrestare una distribuzione. 

Puoi visualizzare i dati della valutazione del gate e la tua distribuzione dal dashboard Deployment Risk. Per aprire il dashboard, apri {{site.data.keyword.DRA_short}} e dal manu laterale, fai clic su **Deployment Risk**.

Se stai utilizzando una {{site.data.keyword.contdelivery_short}} pipeline, puoi visualizzare i report di esecuzione del gate individuali dalla stessa pipeline. Per visualizzare il report di decisione per un gate dalla pipeline: 

1. Nella fase che contiene il gate da verificare, fai clic su **Visualizza log e cronologia**.

2. Dal lavoro che contiene il gate, fai clic sul nome del gate.

3. Nella vista del log, individua il messaggio `Check {{site.data.keyword.DRA_short}} report here` e fai clic sul link per aprire il report.

## Report Developer Insights e Team Dynamics

Puoi visualizzare i dashboard sul tuo team e codice dopo un periodo di estrazione dei dati iniziale. Nel menu di navigazione del servizio, fai clic su **Developer Insights** o **Team Dynamics** e seleziona quindi una categoria di dati per visualizzare queste informazioni.
