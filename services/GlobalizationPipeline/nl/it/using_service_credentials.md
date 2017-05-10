---

copyright:
  years: 2015, 2017
lastupdated: "2016-07-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilizzo di {{site.data.keyword.GlobalizationPipeline_short}} al di fuori di {{site.data.keyword.Bluemix_notm}}
{: #globalizationpipeline_external}


Molti servizi di {{site.data.keyword.Bluemix_notm}}, incluso {{site.data.keyword.GlobalizationPipeline_short}} possono essere utilizzati da un ambiente che ospita l'applicazione in loco o anche da un'altra piattaforma cloud senza dover ospitare l'applicazione su {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Per utilizzare {{site.data.keyword.GlobalizationPipeline_short}} al di fuori di {{site.data.keyword.Bluemix_notm}}, completa la seguente procedura:

1. Vai la catalogo di {{site.data.keyword.Bluemix_notm}} e seleziona il servizio **{{site.data.keyword.GlobalizationPipeline_short}}** dalla categoria **DevOps**.

2. Dalla pagina del catalogo del servizio {{site.data.keyword.GlobalizationPipeline_short}}, compila le informazioni richieste.  Dal campo **Connetti a**, scegli l'opzione **Lascia senza binding**.

3. Fai clic su **Crea** per aggiungere il servizio alla tua organizzazione {{site.data.keyword.Bluemix_notm}}.  Sarai riportato al dashboard di {{site.data.keyword.GlobalizationPipeline_short}}.

4. Dal dashboard, fai clic sulla scheda **Credenziali del servizio**.  

La scheda **Credenziali del servizio** mostra tutte le credenziali che sono disponibili per un istanza particolare del servizio.  Utilizzando queste credenziali e l'URL del servizio fornito, puoi accedere all'API {{site.data.keyword.GlobalizationPipeline_short}} e utilizzare le sue funzioni dalla tua applicazione in qualsiasi ambiente ospitato.

Per informazioni sull'API RESTful {{site.data.keyword.GlobalizationPipeline_short}}, consulta la [Guida di riferimento API](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}.
