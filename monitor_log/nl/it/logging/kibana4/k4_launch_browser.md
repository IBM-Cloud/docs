---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Accesso al dashboard Kibana da un browser web
{: #launch_Kibana_from_browser}

Avvia Kibana da un browser se hai bisogno di analizzare le voci di log in uno spazio {{site.data.keyword.Bluemix}}.
{:shortdesc}

La query utilizzata per filtrare i dati visualizzati in Kibana richiama le voci di log per uno spazio nell'organizzazione {{site.data.keyword.Bluemix_notm}}. Le informazioni di log visualizzate da Kibana includono i record per tutte le risorse che vengono distribuite all'interno dello spazio dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui sei connesso.

Completa la seguente procedura per avviare Kibana da un browser:

1. Apri [https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) per accedere all'interfaccia utente Kibana.

2. Seleziona la versione di Kibana che desideri utilizzare per analizzare i tuoi log.
    * Seleziona **Kibana 4** per lavorare con Kibana 4. Viene aperta la pagina Rileva. Per ulteriori informazioni, consulta [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Seleziona la scheda **Kibana 3** per lavorare con Kibana 3. Viene aperto il dashboard Kibana predefinito. Per ulteriori informazioni sulla personalizzazione di un dashboard Kibana 3, consulta [questo post del blog](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/).
     
        **Nota:** Kibana 3 è obsoleto. 

    Se la pagina Rileva non mostra alcuna voce di log, modifica il selezionatore di tempo. Per ulteriori informazioni, consulta [Configurazione di un filtro temporale](logging_kibana_set_time_filter.html#set_time_filter).

Per ulteriori informazioni su Kibana, consulta [Kibana User Guide ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.
