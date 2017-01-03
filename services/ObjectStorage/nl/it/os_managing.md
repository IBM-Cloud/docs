---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Gestione degli oggetti

Puoi utilizzare la CLI Swift, l'API, o la IU Bluemix per gestire i tuoi oggetti e contenitori.
{: shortdesc}

Prima di poter gestire gli oggetti, assicurati di aver autenticato la tua istanza del servizio, generato le credenziali del servizio e configurato la CLI Swift.

Puoi archiviare, scaricare ed eliminare gli oggetti quando utilizzi il servizio. Esistono poche cose da tenere a mente quando gestisci i tuoi oggetti.
  * Non esiste limite alla quantità di dati che puoi archiviare, ma ogni caricamento non può essere superiore a 5 GB. Se hai bisogno di caricare file più grandi di 5 GB segui le istruzioni in [archiviazione di oggetti grandi](/docs/services/ObjectStorage/os_large_files.html).
  * Swift non dispone di una vera struttura di directory, ma puoi aggiungere una [directory esistente](/docs/services/ObjectStorage/os_directories.html) ai tuoi comandi.
  * Per evitare la sovrascrittura non intenzionale di un file, [configura le versioni dell'oggetto](/docs/services/ObjectStorage/os_versioning.html).
  * Puoi [pianificare una data/ora](/docs/services/ObjectStorage/os_deletion.html) per l'eliminazione dei tuoi oggetti.
