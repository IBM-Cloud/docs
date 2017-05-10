---

copyright:
  years: 2017
lastupdated: "2017-04-12"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Creare API da azioni {{site.data.keyword.openwhisk_short}}
{: #manage_openwhisk_apis}

Le azioni OpenWhisk possono trarre vantaggio dall'essere gestite da Gestione delle API.

Con Gestione delle API, puoi esporre un'azione {{site.data.keyword.openwhisk_short}} come una API. Dopo che hai definito la API, puoi applicare le politiche di sicurezza e di limitazione della frequenza, visualizzare l'utilizzo delle API e i log delle risposte e definire le politiche di condivisione delle API.  

Per creare una API {{site.data.keyword.openwhisk_short}}, completa la seguente procedura:

1. Nel dashboard {{site.data.keyword.openwhisk_short}}, fai clic sulla scheda **API**. Se già hai delle API {{site.data.keyword.openwhisk_short}} create, viene visualizzato un elenco delle tue API {{site.data.keyword.openwhisk_short}}. Se non hai alcuna API {{site.data.keyword.openwhisk_short}}, viene visualizzata una schermata di introduzione. 
2. Fai clic su **Crea una API {{site.data.keyword.openwhisk_short}}**. Viene visualizzata la finestra Crea API per {{site.data.keyword.openwhisk_short}}. 
3. Completa i campi nella sezione Informazioni API e fai quindi clic su **Crea operazione**. Viene visualizzata la finestra Crea operazione. Crei le operazioni per definire l'endpoint, il percorso https e il metodo per la tua API.
4. nella finestra "Crea operazione", completa i campi obbligatori e seleziona **Crea**. L'operazione viene aggiunta alla tabella Operazioni che richiamano azioni {{site.data.keyword.openwhisk_short}}.
5. Completa le restanti informazioni che vuoi completare. Puoi anche aggiungere o aggiornare le restanti informazioni in un secondo momento quando gestisci le tue API.
6. Fai clic su **Salva**. Viene visualizzata la pagina di panoramica della gestione delle API per la tua API e vengono visualizzate tutte le informazioni da te appena definite.
7. Continua la gestione della tua API con [Gestisci API](manage_apis.html).
