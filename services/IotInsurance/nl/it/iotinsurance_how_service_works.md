---

copyright:
  years: 2016
lastupdated: "2016-10-26"

---


{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Come funziona il sevizio
{{site.data.keyword.iotinsurance_full}} crea un flusso per raccogliere, gestire e analizzare i dati dai possessori della polizza collegati.
{:shortdesc}

Il provider dell'assicurazione crea un'istanza {{site.data.keyword.iotinsurance_short}} nell'organizzazione {{site.data.keyword.Bluemix_notm}}. I clienti dell'assicuratore dispongono di sensori nelle loro case, collegati al cloud del provider dei sensori. Per i loro dispositivi mobili, i clienti autorizzano il servizio {{site.data.keyword.iotinsurance_short}} a ricevere i dati dai sensori. Il trasformatore {{site.data.keyword.iotinsurance_short}} si collega al cloud del provider dei sensori e trasmette i dati di ogni utente e li invia al server {{site.data.keyword.iot_short_notm}}. Se il sensore mostra che i parametri specificati negli scudi dell'assicuratore vengono soddisfatti nella casa del cliente, le notifiche vengono inviate al dashboard dell'assicuratore e al dispositivo del cliente.

Un sensore collegato rileva un evento, come una fuoriuscita d'acqua ed invia queste informazioni a un fornitore casa intelligente, come Wink.  {{site.data.keyword.iotinsurance_short}} rileva il segnale utilizzando la propria connessione con il cloud del fornitore casa intelligente e crea un payload dell'avviso. Il payload è inviato tramite MQTT al motore dello scudo {{site.data.keyword.iotinsurance_short}} per l'elaborazione. Il motore dello scudo analizza se il payload corrisponde ai criteri definiti dalle regole dello scudo. Se corrisponde, il motore dello scudo emette un payload di pericolo tramite MQTT al motore delle azioni {{site.data.keyword.iotinsurance_short}}. Il motore delle azioni esegue le azioni definite dallo scudo per tale tipo di pericolo, ad esempio, inviando un messaggio di testo al proprietario di casa.

{{site.data.keyword.iotinsurance_short}} si basa su {{site.data.keyword.iot_full}} per trasmettere l'avviso e i payload di pericolo tra i componenti. Un sistema di lavoro completo richiede utenti, scudi e associazioni tra gli utenti e gli scudi.

![{{site.data.keyword.iotinsurance_short}} Processo. Questo diagramma è descritto nel corpo principale dell'argomento.](images/IoT4I_process.svg "{{site.data.keyword.iotinsurance_short}} processo")

# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}
* [Sample mobile app code on GitHub](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## Riferimento API
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [{{site.data.keyword.iotinsurance_short}} API Examples](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}

## Link correlati
{: #general}
* [Documentazione {{site.data.keyword.iot_full}}](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [Developer support forum](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack overflow support forum](http://stackoverflow.com/questions/tagged/ibm-bluemix)
