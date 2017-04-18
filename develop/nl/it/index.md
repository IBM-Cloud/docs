---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:new_window: target="_blank"}

# Sviluppo di applicazioni 
{: #develop-apps-IDS}

*Ultimo aggiornamento: 07 dicembre 2015*  

Puoi sviluppare applicazioni utilizzando un ambiente di sviluppo integrato (o IDE, integrated development
environment) o un editor di testo oppure puoi utilizzare {{site.data.keyword.jazzhub}}. 
{: shortdesc}

## Sviluppo di applicazioni con Bluemix DevOps Services
{: #dev_ops}

Puoi utilizzare {{site.data.keyword.jazzhub_short}} per
sviluppare, tracciare e pianificare un'applicazione nel cloud e puoi quindi eseguirne la distribuzione a {{site.data.keyword.Bluemix_notm}}. Puoi passare dal codice sorgente a un'applicazione in esecuzione nel giro di pochi minuti.  

{{site.data.keyword.jazzhub_short}}
fornisce due servizi: {{site.data.keyword.trackplan}} e {{site.data.keyword.deliverypipeline}}. Il servizio {{site.data.keyword.trackplan}}
viene utilizzato per un'agile pianificazione. Il servizio {{site.data.keyword.deliverypipeline}} automatizza build e distribuzioni. Puoi trovare questi servizi nel catalogo {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni sulla loro modalità di utilizzo, consulta [Introduzione a Track & Plan](../services/TrackPlan/index.html#gettingstartedtemplate) e [Introduzione a Delivery Pipeline](../services/DeliveryPipeline/index.html#getstartwithCD). 

{{site.data.keyword.jazzhub_short}} fornisce inoltre l'hosting Git per il controllo dell'origine e un IDE Web dove puoi modificare, gestire e distribuire il tuo codice. In un'applicazione, abiliti l'hosting Git facendo clic sul link **AGGIUNGI GIT**, che si trova nell'angolo superiore destro della pagina Panoramica dell'applicazione. Puoi quindi modificare il codice dell'applicazione nell'IDE Web facendo clic su **MODIFICA CODE**. Dalla shell IDE Web, puoi eseguire i comandi cf con content assist. Ad esempio, puoi
ricevere un elenco di tutti i comandi Cloud Foundry immettendo il seguente
comando:  
```
help cfo
```
{:pre}
