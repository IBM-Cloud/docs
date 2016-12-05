---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-04"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Annullamento del bind o effettuazione del deprovisioning della tua istanza  {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}



### Annullamento del bind della tua istanza
Se non hai più bisogno di {{site.data.keyword.objectstorageshort}} nella tua applicazione Cloud Foundry ma desideri conservare i dati salvati, puoi annullare il bind della tua istanza al servizio dalla tua applicazione.

**Attenzione**: se annulli il bind di un'istanza {{site.data.keyword.objectstorageshort}} da un'applicazione {{site.data.keyword.Bluemix_notm}} o elimini la chiave del servizio, tutte le tue credenziali per tale istanza vengono eliminate e non possono venire ripristinate. L'account {{site.data.keyword.objectstorageshort}} viene eliminato solo dopo che è stato effettuato il deprovisioning dell'istanza {{site.data.keyword.objectstorageshort}}. Puoi generare delle nuove credenziali cloud eseguendo nuovamente il bind di, oppure creando, una nuova chiave di servizio. 

1. Per visualizzare i servizi associati alla tua applicazione, fai clic sulla scheda delle connessioni nella tua applicazione Cloud Foundry.
2. Individua il servizio a cui desideri annullare il bind e fai clic sul pulsante del menu nel tile del servizio.
3. Seleziona **Annulla binding del servizio**.
4. Deseleziona **Elimina le istanze del servizio** e fai clic su **OK**.
5. Fai clic su **Riprepara** in modo che le tue modifiche abbiano effetto.



### Deprovisioning della tua istanza

Se hai un'istanza non associata di {{site.data.keyword.objectstorageshort}} di cui non hai più bisogno, puoi eliminarla.

**Attenzione**: quando esegui il deprovisioning di un'istanza {{site.data.keyword.objectstorageshort}}, il progetto cloud e l'account Swift vengono eliminati. Tutti i contenitori e gli oggetti nell'istanza di cui viene effettuato il deprovisioning vengono eliminati e non è possibile ripristinarli.

1. Per visualizzare i servizi associati alla tua applicazione, fai clic sulla scheda delle connessioni nella tua applicazione Cloud Foundry.
2. Individua il servizio a cui desideri annullare il bind e fai clic sul pulsante del menu nel tile del servizio.
3. Seleziona **Elimina il servizio**. 
4. Fai clic su **Elimina** come conferma.
5. Fai clic su **Riprepara** in modo che le tue modifiche abbiano effetto.
