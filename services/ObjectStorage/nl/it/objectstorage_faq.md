---

copyright:
  years: 2014, 2016

---

{:new_window: target="_blank"}

# Domande frequenti {: #faq} 

*Ultimo aggiornamento: 18 luglio 2016*
{: .last-updated}


## Come variano i prezzi a seconda del piano da me scelto? {: #plan-price}
Il prezzo varia a seconda del piano scelto. Per ulteriori informazioni sui prezzi, consulta il [listino prezzi di IBM Bluemix](https://console.ng.bluemix.net/pricing/){: new_window} oppure utilizza il [Calcolatore](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window} per delle stime più dettagliate.


## Quali account e piani di pagamento posso usare per {{site.data.keyword.objectstorageshort}}? {: #account-payment}
Il servizio {{site.data.keyword.objectstorageshort}} offre più opzioni di piano. A partire dalla nostra release di disponibilità generale, sono attualmente offerti due piani, Standard e Gratuito. Il piano Standard è disponibile solo con gli account a pagamento {{site.data.keyword.Bluemix_notm}}, Pagamento a consumo o Sottoscrizione, e agli utenti interni IBM. Il piano Standard include una franchigia di 5 GB introduttiva sull'utilizzo dell'archiviazione per account.

Gli account di prova che sono ancora attivi possono utilizzare il piano Gratuito che consente l'esistenza di una sola istanza in un'organizzazione {{site.data.keyword.Bluemix_notm}}. Dopo la scadenza della versione di prova di {{site.data.keyword.Bluemix_notm}}, l'istanza del servizio {{site.data.keyword.objectstorageshort}} associata viene
disabilitata, il che significa che non è possibile accedere all'account di archiviazione dalla riga di comando o dall'interfaccia utente {{site.data.keyword.Bluemix_notm}}. Dopo un periodo di tolleranza di 30 giorni, l'account {{site.data.keyword.Bluemix_notm}} viene eliminato e tutti i dati vengono eliminati. Per evitare perdite di dati, ti consigliamo di eseguire un upgrade a un account a pagamento {{site.data.keyword.Bluemix_notm}} quanto prima. Per eseguire un upgrade del tuo account, fai clic sul menu di gestione degli utenti e seleziona **Account**, che fornisce istruzioni sul processo di upgrade.

## Come modifico il mio piano? {: #changeplan}  
Le istanze create con il piano Beta o Gratuito possono essere aggiornate al piano Standard. L'organizzazione associata deve essere un account a pagamento {{site.data.keyword.Bluemix_notm}}. Non è possibile eseguire l'upgrade degli account di prova con istanze {{site.data.keyword.objectstorageshort}} al piano Standard e non è possibile eseguire il downgrade delle istanze nel piano Standard ad altri piani. Quando esegui l'aggiornamento, le tue istanze dei servizi e i tuoi dati cliente vengono spostati al nuovo piano.

Per aggiornare il tuo piano:
1.	Nell'interfaccia utente {{site.data.keyword.objectstorageshort}}, fai clic su **Piano**.
2.	Seleziona **Standard** come nuovo piano e fai quindi clic su **Salva**.

Puoi anche modificare il piano di pagamento utilizzando l'interfaccia riga di comando. Per ulteriori informazioni, vedi il documento relativo a [come modificare il tuo piano](../../pricing/index.html#changing).


## In che modo mi verrà addebitato e fatturato l'utilizzo di {{site.data.keyword.objectstorageshort}}? {: #charge-bill}

L'addebito del servizio {{site.data.keyword.objectstorageshort}} comprende solo ciò che si utilizza.  Non sono previste tariffe minime, costi di installazione od obblighi di spesa per iniziare a utilizzare il servizio. Non sono previsti addebiti per le richieste API o il traffico di rete dei dati in entrata.

L'utilizzo di {{site.data.keyword.objectstorageshort}} viene fatturato sulla base del tuo utilizzo dell'archiviazione nel ciclo di fatturazione. Sono inclusi tutti i dati oggetti dei contenitori che hai creato nel tuo account organizzazione {{site.data.keyword.Bluemix_notm}}. 

La tariffa di Trasferimento dati in uscita viene applicata ogni volta che vengono letti dati da uno qualsiasi dei tuoi contenitori di dati nella rete pubblica. La larghezza di banda in uscita pubblica viene fatturata per tutta la larghezza di banda utilizzata nel ciclo di fatturazione.

I componenti delle metriche per i prezzi {{site.data.keyword.objectstorageshort}} sono i seguenti:
* Utilizzo dell'archiviazione: $ 0,04 per GB al mese
* Trasferimento pubblico dati in uscita: $ 0,09 per GB al mese 

Al termine del ciclo di fatturazione, {{site.data.keyword.Bluemix_notm}} creerà automaticamente la fattura per il periodo di utilizzo per il periodo di fatturazione corrente. Puoi visualizzare i tuoi addebiti per il periodo di fatturazione corrente attraverso il reporting {{site.data.keyword.Bluemix_notm}}.

Il piano di servizio standard rilasciato per Londra e Dallas ha gli stessi prezzi.

## In che modo viene eseguita la replica dei dati in {{site.data.keyword.objectstorageshort}}? {: #replication}
Il servizio {{site.data.keyword.objectstorageshort}} gestisce tre copie dei tuoi dati che vengono replicate tra più nodi di archiviazione. Per ulteriori informazioni, vedi il documento [Replica OpenStack Swift](http://docs.openstack.org/developer/swift/overview_replication.html){: new_window}.

