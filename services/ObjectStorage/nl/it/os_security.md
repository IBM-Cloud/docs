---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# Gestione dell'accesso

Gli elenchi del controllo dell'accesso possono essere utilizzati per gestire l'accesso al servizio. [Gli utenti amministratori](/docs/services/ObjectStorage/os_access_types.html) possono concedere l'accesso in lettura e scrittura, così come rimuoverlo quando gestiscono la tua istanza del servizio.
{: shortdesc}


Gli elenchi del controllo dell'accesso possono essere gestiti utilizzando la CLI Swift o la IU Bluemix. Prima di gestire l'accesso, assicurati di aver configurato il servizio e avviato l'archiviazione degli oggetti. Esistono poche cose da tenere a mente quando gestisci l'accesso. 
  * Quando un utente crea un contenitore, gli vengono automaticamente concessi i privilegi da amministratore per tale contenitore.
  * Gli elenchi del controllo dell'accesso non sono disponibili per l'istanza del servizio, per l'account di archiviazione o al livello del progetto. L'accesso può soltanto essere gestito al livello del contenitore.
  * Assicurati di verificare che l'accesso a un contenitore sia stato [rimosso](/docs/services/ObjectStorage/os_remove_access.html).
