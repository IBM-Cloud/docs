---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Annullamento del bind o effettuazione del deprovisioning della tua istanza  {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

*Ultimo aggiornamento: 19 ottobre 2016*
{: .last-updated}


### Annullamento del bind della tua istanza 
Se non hai più bisogno di {{site.data.keyword.objectstorageshort}} nella tua applicazione Cloud Foundry ma desideri conservare i dati salvati, puoi annullare il bind della tua istanza al servizio dalla tua applicazione.

**Attenzione**: se annulli il bind di un'istanza {{site.data.keyword.objectstorageshort}} da un'applicazione {{site.data.keyword.Bluemix_notm}} o elimini la chiave del servizio, tutte le tue credenziali per tale istanza vengono eliminate e non possono venire ripristinate.

1. Apri i dettagli della tua applicazione nella console {{site.data.keyword.Bluemix_notm}}.
2. Seleziona la tua istanza {{site.data.keyword.objectstorageshort}} e fai clic su **Annulla binding del servizio**.
3. Fai clic su **RIMUOVI**.
4. Fai clic su **RIPREPARA**.



### Deprovisioning della tua istanza

Se hai un'istanza non associata di {{site.data.keyword.objectstorageshort}} di cui non hai più bisogno, puoi eliminarla.

**Attenzione**: quando esegui il deprovisioning di un'istanza {{site.data.keyword.objectstorageshort}}, viene eliminato il progetto cloud. Tutti i contenitori e gli oggetti nell'istanza di cui viene effettuato il deprovisioning vengono eliminati e non è possibile ripristinarli. 

1. Apri i dettagli della tua applicazione nella console {{site.data.keyword.Bluemix_notm}}.
2. Seleziona la tua istanza {{site.data.keyword.objectstorageshort}} e fai clic su **Elimina**.
3. Fai clic su **RIPREPARA**.
