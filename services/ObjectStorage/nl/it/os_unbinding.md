---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Annullamento del bind o effettuazione del deprovisioning della tua istanza  {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

Se il servizio {{site.data.keyword.objectstorageshort}} è associato alla tua applicazione Cloud Foundry, ma non ne hai più bisogno per l'archiviazione, puoi annullare l'associazione ed eseguire il deprovisioning della tua istanza.
{: shortdesc}


## Annullamento del bind della tua istanza

Puoi mantenere i tuoi dati salvati e annullare il bind al servizio dalla tua applicazione Cloud Foundry. L'account {{site.data.keyword.objectstorageshort}} non viene eliminato finché non viene annullato il provisioning del servizio.

**Attenzione**: se annulli il bind di un'istanza {{site.data.keyword.objectstorageshort}} da un'applicazione {{site.data.keyword.Bluemix_notm}} o elimini la chiave del servizio, tutte le tue credenziali per tale istanza vengono eliminate e non possono venire ripristinate. Puoi generare delle nuove credenziali cloud eseguendo nuovamente il bind di, oppure creando, una nuova chiave di servizio.

1. Per visualizzare i servizi associati alla tua applicazione, fai clic sulla scheda delle connessioni nella tua applicazione Cloud Foundry.
2. Individua il servizio a cui desideri annullare il bind e fai clic sul pulsante del menu nel tile del servizio.
3. Seleziona **Annulla binding del servizio**.
4. Deseleziona la casella **Elimina le istanze del servizio** e fai clic su **OK**.
5. Fai clic su **Riprepara** in modo che le tue modifiche abbiano effetto.



## Deprovisioning della tua istanza

Se hai un'istanza di {{site.data.keyword.objectstorageshort}} di cui non hai più bisogno, puoi eliminarla.

**Attenzione**: quando esegui il deprovisioning di un'istanza {{site.data.keyword.objectstorageshort}}, il progetto cloud e l'account Swift vengono eliminati. Tutti i contenitori e gli oggetti nell'istanza di cui viene effettuato il deprovisioning vengono eliminati e non è possibile ripristinarli.

1. Per visualizzare i servizi associati alla tua applicazione, fai clic sulla scheda delle connessioni nella tua applicazione Cloud Foundry.
2. Individua il servizio a cui desideri annullare il provisioning e fai clic sul pulsante del menu nel tile del servizio.
3. Seleziona **Elimina il servizio**.
4. Fai clic su **Elimina** come conferma.
5. Fai clic su **Riprepara** in modo che le tue modifiche abbiano effetto.
