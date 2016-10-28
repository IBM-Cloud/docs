---

copyright:
  years: 2016
lastupdated: "2016-10-06"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Risoluzione dei problemi
{: #troubleshooting}

Qui troverai le risposte alle domande per la risoluzione dei problemi comuni relativi all'utilizzo di {{site.data.keyword.iotinsurance_full}} su {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problema con la distribuzione delle applicazioni
{: #deployingapps}

Potresti non riuscire a distribuire le applicazioni per {{site.data.keyword.iotinsurance_short}} se non disponi di memoria sufficiente nella tua organizzazione {{site.data.keyword.Bluemix_notm}}. Puoi ridurre la memoria utilizzata dalle tue applicazioni oppure aumentare la quota di memoria per il tuo account.

### Cosa sta succedendo

Quando apri il servizio {{site.data.keyword.iotinsurance_short}}, la funzione Distribuisci non è abilitata e non puoi distribuire alcuna applicazione. 

### Perché sta succedendo

Per abilitare la funzione Distribuisci, nella tua organizzazione devono essere disponibili almeno 2 GB di memoria. Gli account di prova hanno una quota di memoria massima pari a 2 GB. Se hai creato applicazioni o servizi diversi da {{site.data.keyword.iotinsurance_short}}, la tua organizzazione non dispone della memoria sufficiente per distribuire le applicazioni {{site.data.keyword.iotinsurance_short}}.

### Come porvi rimedio

Puoi aumentare la quota di memoria del tuo account o ridurre la memoria utilizzata dai tuoi servizi e applicazioni.

  - Per aumentare la quota di memoria del tuo account, puoi [convertire il tuo account di prova in un account a pagamento](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).

  - Per ridurre rapidamente la memoria in uso, rimuovi tutti i servizi e le applicazioni che non siano {{site.data.keyword.iotinsurance_short}}. Riavvia il servizio {{site.data.keyword.iotinsurance_short}} per rendere effettive le modifiche.

  - Per gli account a pagamento che dispongono di oltre 2 GB di memoria totale, potresti riuscire a evitare di rimuovere altre applicazioni o servizi regolando la quantità di memoria che utilizzano. Per informazioni, vedi [Limite di memoria dell'organizzazione superato](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory).
