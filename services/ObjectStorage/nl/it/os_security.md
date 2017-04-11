---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# Gestione dell'accesso

Gli elenchi del controllo dell'accesso possono essere utilizzati per gestire l'accesso al servizio. [Gli utenti amministratori](/docs/services/ObjectStorage/os_access_types.html) possono concedere l'accesso in lettura e scrittura, così come rimuoverlo.
{: shortdesc}

Prima di gestire l'accesso utilizzando la IU o la CLI Swift, assicurati di aver configurato il servizio e avviato l'archiviazione degli oggetti.

Quando stai utilizzando gli elenchi del controllo dell'accesso, tieni i seguenti punti in mente:
  * Quando un utente crea un contenitore, gli vengono automaticamente concessi i privilegi da amministratore per tale contenitore.
  * Gli elenchi del controllo dell'accesso non sono disponibili per l'istanza del servizio, per l'account di archiviazione o al livello del progetto. L'accesso può essere gestito solo al livello del contenitore o dell'oggetto.
  * Assicurati di verificare che l'accesso a un contenitore sia stato [rimosso](/docs/services/ObjectStorage/os_remove_access.html).
