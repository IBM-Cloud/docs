---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Informazioni su {{site.data.keyword.twittershort}}
{: #about_twitter}

*Ultimo aggiornamento: 13 maggio 2016*
{: .last-updated}

Utilizza {{site.data.keyword.twitterfull}} per incorporare il contenuto di Twitter dai flussi Twitter [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window} o [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window} nelle tue applicazioni {{site.data.keyword.Bluemix}}.
{:shortdesc}

L'archivio del contenuto viene aggiornato e indicizzato in tempo reale, rendendo le ricerche dinamiche e veloci. Il servizio arricchisce i Tweet con sentimento e altre opinioni per più lingue, in base agli algoritmi di elaborazione della lingua naturali da [IBM Social Media Analytics](http://www.ibm.com/software/products/en/social-media-analytics/){: new_window}. L'elaborazione in tempo reale dei flussi di dati di Twitter è completamente supportata e configurabile con un'ampia gamma di parametri di query e parole chiave. {{site.data.keyword.twittershort}} include API RESTful che ti permettono di personalizzare le tue ricerche e restituisce Tweet e arricchimenti nel formato JSON. I Tweet restituiti rispettano il formato [Gnip Activity Stream](http://support.gnip.com/sources/twitter/data_format.html){: new_window} per i dati di Twitter.

Il servizio {{site.data.keyword.twittershort}} analizza i flussi di Twitter Decahose e PowerTrack in tempo reale per fornire i seguenti arricchimenti per ogni autore di Tweet:
* Genere
* Ubicazione permanente (definita da nazione, stato e città)

Sono inoltre disponibili i seguenti arricchimenti per il contenuto dei Tweet:

* Sentimento (positivo, negativo, ambivalente o neutrale per i Tweet in inglese, tedesco, francese e spagnolo)
* Le frasi per il sentimento positivo/negativo in un Tweet (per i Tweet in inglese, tedesco, francese e spagnolo)

Per convalidare i risultati della ricerca {{site.data.keyword.twittershort}}, il servizio fornisce un metodo API REST che conferma se un particolare Tweet è ancora accessibile su Twitter. 

## Feedback e supporto 
{: #feedback_support}

Il team di {{site.data.keyword.twitterfull}} è interessato a conoscere il parere degli utenti.

Se riscontri un problema con questo servizio, visita il sito
IBM [developerWorks Answers](https://developer.ibm.com/answers/topics/insights-twitter/?smartspace=bluemix){: new.window} forum. Cerca le risposte a domande già inviate o fanne una.
Includi le tag **insights-twitter** e **bluemix** per migliorare il tempo di risposta.

Se le tue domande non sono risolte in developerWorks Answers, inserisci la tua domanda in
[Stack Overflow](http://stackoverflow.com/search?q=twitter+bluemix){: new.window} e aggiungi le seguenti tag alla tua domanda: **twitter** e **bluemix**.

Puoi inoltre visualizzare lo stato della [Bluemix Platform](https://developer.ibm.com/bluemix/support/#status){: new.window}
o [aprire un ticket di supporto](https://cloudoe.support.ibmcloud.com/ics/support/default.asp?deptid=31036&offering=ibmbluemix){: new.window}. Per ulteriori informazioni, consulta [Troubleshooting](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}.
