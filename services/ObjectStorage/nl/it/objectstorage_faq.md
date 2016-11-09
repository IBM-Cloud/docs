---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Domande frequenti {: #faq}

*Ultimo aggiornamento: 19 ottobre 2016*
{: .last-updated}

Questa FAQ fornisce risposte a domande comuni sul servizio {{site.data.keyword.objectstorageshort}}.
{: shortdesc}


## Quali account e piani di pagamento posso usare per {{site.data.keyword.objectstorageshort}}? {: #account-payment}

Il servizio {{site.data.keyword.objectstorageshort}} offre due opzioni di piano, Gratuito e Standard. Il [Prezzo](https://console.ng.bluemix.net/pricing/) varia a seconda del piano scelto.

<table>
  <tr>
    <th> Piano gratuito </th>
    <th> Piano standard</th>
  </tr>
  <tr>
    <td> Consente solo una istanza del servizio in un'organizzazione {{site.data.keyword.Bluemix_notm}} alla volta </td>
    <td> Istanze del servizio illimitate </td>
  </tr>
  <tr>
    <td> Disponibile per chiunque </td>
    <td> Disponibile solo per gli account a pagamento {{site.data.keyword.Bluemix_notm}} e gli utenti interni IBM </td>
  </tr>
  <tr>
    <td> Gratuito </td>
    <td> Pagamento a consumo o sottoscrizione ai piani a pagamento </td>
  </tr>
  <tr>
    <td> Include un limite di utilizzo dell'archiviazione di 5 GB iniziale </td>
    <td> Archiviazione illimitata </td>
  </tr>
</table>

*Tabella 1: Confronto tra i piani Gratuito e Standard*

**Attenzione**: gli utenti che utilizzano un account di prova {{site.data.keyword.Bluemix_notm}} possono utilizzare il piano Gratuito. Dopo la scadenza della versione di prova, l'istanza del servizio {{site.data.keyword.objectstorageshort}} associata sarà disabilitata, il che significa che non sarai più in grado di accedere all'account di archiviazione. Dopo 30 giorni, il tuo account {{site.data.keyword.Bluemix_notm}} sarà eliminato e tutti i dati vengono eliminati. Per evitare perdite di dati, esegui l'aggiornamento a un [account {{site.data.keyword.Bluemix_notm}} a pagamento](https://new-console.ng.bluemix.net/docs/admin/account.html) quanto prima.

## Come modifico il mio piano? {: #changeplan}  
Le istanze create con il piano Beta o Gratuito possono essere aggiornate al piano Standard. L'organizzazione associata deve essere un account a pagamento {{site.data.keyword.Bluemix_notm}}. Non è possibile eseguire l'upgrade degli account di prova con istanze Object Storage al piano Standard e non è possibile eseguire il downgrade delle istanze nel piano Standard ad altri piani. Quando esegui l'aggiornamento, le tue istanze dei servizi e i tuoi dati cliente vengono spostati al nuovo piano.

Per aggiornare:
1.	Nell'interfaccia utente {{site.data.keyword.objectstorageshort}}, fai clic su **Piano**.
2.	Seleziona **Standard** come nuovo piano e fai quindi clic su **Salva**.

Puoi anche [modificare il piano di pagamento](../../pricing/index.html#changing) utilizzando l'interfaccia riga di comando.

## In che modo mi verrà addebitato e fatturato l'utilizzo di {{site.data.keyword.objectstorageshort}}? {: #charge-bill}

L'addebito del servizio {{site.data.keyword.objectstorageshort}} comprende solo ciò che si utilizza.  Non sono previsti costi di installazione od obblighi di spesa per iniziare a utilizzare il servizio. Non sono previsti addebiti per le richieste API o il traffico di rete dei dati in entrata. 

{{site.data.keyword.objectstorageshort}} viene fatturato sulla base del tuo utilizzo dell'archiviazione nel ciclo di fatturazione. Sono inclusi tutti i dati oggetti dei contenitori che hai creato nella tua organizzazione {{site.data.keyword.Bluemix_notm}}.

Una tariffa di Trasferimento dati in uscita viene applicata ogni volta che vengono letti dati da uno qualsiasi dei tuoi contenitori di dati nella rete pubblica. Tutta la banda utilizzata nel ciclo di fatturazione viene fatturata come banda in uscita pubblica.

Al termine del ciclo di fatturazione, {{site.data.keyword.Bluemix_notm}} viene automaticamente creata la fattura per l'utilizzo durante tale periodo di fatturazione. Puoi visualizzare i tuoi addebiti per il periodo di fatturazione corrente attraverso il reporting {{site.data.keyword.Bluemix_notm}}.
