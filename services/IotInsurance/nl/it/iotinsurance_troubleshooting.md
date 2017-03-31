---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Risoluzione dei problemi di {{site.data.keyword.iotinsurance_short}}
{: #ts}

Qui troverai le risposte alle domande per la risoluzione dei problemi comuni relativi all'utilizzo di {{site.data.keyword.iotinsurance_full}} su {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problema con la distribuzione delle applicazioni
{: #deployingapps}
Potresti non riuscire a distribuire le applicazioni per {{site.data.keyword.iotinsurance_short}} se non disponi di memoria sufficiente nella tua organizzazione {{site.data.keyword.Bluemix_notm}}. Puoi ridurre la memoria utilizzata dalle tue applicazioni oppure aumentare la quota di memoria per il tuo account.
{:shortdesc}

Quando apri il servizio {{site.data.keyword.iotinsurance_short}}, la funzione Distribuisci non è abilitata e non puoi distribuire alcuna applicazione.
{: tsSymptoms}

Per abilitare la funzione Distribuisci, nella tua organizzazione devono essere disponibili almeno 2 GB di memoria. Gli account di prova hanno una quota di memoria massima pari a 2 GB. Se hai creato applicazioni o servizi diversi da {{site.data.keyword.iotinsurance_short}}, la tua organizzazione non dispone della memoria sufficiente per distribuire le applicazioni {{site.data.keyword.iotinsurance_short}}.
{: tsCauses}

Puoi aumentare la quota di memoria del tuo account o ridurre la memoria utilizzata dai tuoi servizi e applicazioni.
- Per aumentare la quota di memoria del tuo account, puoi [convertire il tuo account di prova in un account a pagamento](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).
- Per ridurre rapidamente la memoria in uso, rimuovi tutti i servizi e le applicazioni che non siano {{site.data.keyword.iotinsurance_short}}. Riavvia il servizio {{site.data.keyword.iotinsurance_short}} per rendere effettive le modifiche.
- Per gli account a pagamento che dispongono di oltre 2 GB di memoria totale, potresti riuscire a evitare di rimuovere altre applicazioni o servizi regolando la quantità di memoria che utilizzano. Per informazioni, vedi [Limite di memoria dell'organizzazione superato](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory).
{: tsResolve}

## Problemi relativi alle prestazioni
{: #performance_issues}

Duranti i periodi di picco di attività, puoi riscontrare delle prestazioni lente.
{:shortdesc}

I sistemi occupati che effettuano chiamate API frequenti possono riscontrare ritardi nei tempi di risposta.
{: tsSymptoms}

Per impostazione predefnita, {{site.data.keyword.iotinsurance_short}} distribuisce una versione di prova di {{site.data.keyword.cloudantfull}}. Questa versione limita il numero di chiamate API che possono essere effettuate al secondo.
{: tsCauses}

Aggiornamento alla versione standard di {{site.data.keyword.cloudant}}.
{: tsResolve}

## Come ottenere aiuto e supporto per {{site.data.keyword.iotinsurance_short}}
{: #gettinghelp}

Se hai dei problemi o delle domande quando utilizzi
{{site.data.keyword.iotinsurance_full}}, puoi controllare {{site.data.keyword.Bluemix_notm}} o ottenere aiuto ricercando le informazioni o facendo delle domande in un forum. Puoi inoltre aprire un ticket di supporto.

- Puoi controllare se {{site.data.keyword.Bluemix_notm}} è disponibile andando alla [pagina sullo stato Bluemix ![icona link esterno](../../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/support/#status){:new_window}.

- Puoi rivedere i forum per controllare se altri utenti hanno riscontrato lo stesso problema. Quando utilizzi i forum per fare una domanda, contrassegnala con una tag in modo che sia visualizzabile dai team di sviluppo {{site.data.keyword.Bluemix_notm}}.
  <!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->
- Se hai domande tecniche sullo sviluppo o la distribuzione di un'applicazione con {{site.data.keyword.iotinsurance_short}}, inserisci la tua domanda in [Stack Overflow ![icona link esterno](../../icons/launch-glyph.svg)](http://stackoverflow.com/search?q=iot-insurance+ibm-bluemix){:new_window} e contrassegnala con le tag "ibm-bluemix" e "iot-for-insurance".
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
- Per domande sul servizio e sulle istruzioni per l'utilizzo iniziale, utilizza il forum [IBM developerWorks dW Answers ![icona link esterno](../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/topics/iot-insurance/?smartspace=bluemix){:new_window}. Includi le tag "iot-for-insurance" e "bluemix".

Consulta [Come ottenere supporto](https://www.{DomainName}/docs/support/index.html#getting-help) per ulteriori dettagli sull'utilizzo dei forum.

- Se ancora non riesci a risolvere il problema, puoi aprire un ticket di supporto IBM. Per informazioni su come aprire un ticket di supporto IBM o sui livelli di supporto e sulla gravità dei ticket, consulta
[Come contattare il supporto](../support/index.html#contacting-support).
