---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introduzione a {{site.data.keyword.graphfull}}
{: #gettingstartedtemplate}
Ultimo aggiornamento: 27 luglio 2016
{: .last-updated}

{{site.data.keyword.graphfull}} è un servizio del database grafico interamente gestito,
accessibile con un'interfaccia API HTTP basata su REST.
Utilizzala per creare le tue applicazioni web e mobili che richiedono le capacità di database grafiche.
{:shortdesc}

{{site.data.keyword.graphfull}} è basato sullo stack [Apache TinkerPop](http://tinkerpop.incubator.apache.org/)&trade;,
per la creazione di applicazioni grafiche ad alte prestazioni che utilizzano un'API compatibile v3.
Lo stack fornisce ulteriori capacità e flessibilità in base a un ambiente conosciuto.
Utilizzando il dashboard {{site.data.keyword.Bluemix}},
puoi facilmente integrare il servizio {{site.data.keyword.graphfull}} con le tue applicazioni {{site.data.keyword.Bluemix_short}}.

Puoi utilizzare {{site.data.keyword.graphfull}} in due modi:

*	Utilizzando i comandi API semplificati {{site.data.keyword.graphfull}}.
*	Utilizzando il linguaggio di query Apache TinkerPop v3 completo (Gremlin).

Le funzioni {{site.data.keyword.graphfull}} sono disponibili come un'API utilizzando gli endpoint HTTP REST.
Questi endpoint forniscono un modo facile per le tue applicazioni di collegarsi ed utilizzare il servizio {{site.data.keyword.graphfull}},
utilizzando HTTP o eseguendo richieste API e ottenere dei risultati.
Utilizza le funzioni HTTP fornite dal tuo linguaggio di programmazione dell'applicazione scelto per accedere agli endpoint.
In alternativa puoi utilizzare un'interfaccia di comando o un script `curl` per ottenere gli stessi effetti.
La guida di riferimento alle API descrive le varie funzioni fornite dal servizio {{site.data.keyword.graphfull}},
con esempi per il loro utilizzo.

La tua applicazione può inoltre utilizzare il linguaggio di query Apache TinkerPop,
conosciuto come Gremlin,
per le attività che utilizzano il servizio {{site.data.keyword.graphfull}}.
Includi la query Gremlin in un documento JSON,
quindi passa il documento all'endpoint del servizio `/gremlin`.
Gli esempi di utilizzo di Gremlin con {{site.data.keyword.graphfull}} sono forniti nella documentazione completa.

Completa la seguente procedura per iniziare ad utilizzare il servizio {{site.data.keyword.graphfull}}:

1.	[Crea un'istanza](https://www.ng.bluemix.net/docs/services/reqnsi.html#req_instance) del servizio {{site.data.keyword.graphfull}}.
2.	Registra i tre valori essenziali generati quando viene creata l'istanza. I valori sono disponibili dalla scheda `Credenziali del servizio` dopo aver fatto clic sul tile del servizio.
	*	Gli endpoint di IBM Graph: `apiURL`.
	*	Il nome dell'istanza del servizio `username`.
	*	La password dell'istanza del servizio `password`.
3.	Utilizza i tre valori essenziali nelle tue applicazioni o script per le attività {{site.data.keyword.graphfull}}. Gli esempi sono forniti nella documentazione completa.

# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}

* [Esempi](https://ibm-graph-docs.ng.bluemix.net/examples.html){:new_window}

## Guida di riferimento API
{: #api}

* [REST API for IBM Graph](https://ibm-graph-docs.ng.bluemix.net/api.html){:new_window}
* [Using Gremlin with IBM Graph](https://ibm-graph-docs.ng.bluemix.net/api.html#gremlin-apis){:new_window}

## Link correlati
{: #general}

* [Documentazione completa](https://ibm-graph-docs.ng.bluemix.net/){:new_window}
* [Overflow dello stack](http://stackoverflow.com/questions/tagged/ibm-graph){:new_window}
* [Apache Tinkerpop](http://tinkerpop.incubator.apache.org/){:new_window}
