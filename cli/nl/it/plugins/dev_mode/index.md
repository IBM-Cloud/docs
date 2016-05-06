---

 

copyright:

  years: 2015, 2016

 

---
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# CLI modalità di sviluppo
{: #devmodecli}

*Ultimo aggiornamento: 25 febbraio 2016* 

La modalità di sviluppo (dev_mode) è una funzione Bluemix che puoi utilizzare per gestire le tue applicazioni mentre sono in esecuzione nel cloud. La modalità di sviluppo include l'interfaccia riga di comando dev_mode. La CLI dev_mode è stata messa a punto come un plug-in CLI cf e supporta sia applicazioni Node.js IBM sia Liberty.

La CLI dev_mode fornisce le seguenti funzioni:
- Alterna la tua applicazione tra la modalità sviluppo e quella normale.
- Aggiorna i file applicazione in modo incrementale senza una nuova distribuzione.
- Avvia, arresta o riavvia la tua applicazione nel contenitore esistente.

## Introduzione
**Prerequisito:** prima di iniziare, installa la CLI Cloud Foundry. Vedi [Inizia a codificare con l'interfaccia riga di comando Cloud Foundry](https://github.com/cloudfoundry/cli) per i dettagli. 


Utilizza uno dei seguenti metodi per installare lo strumento riga di comando dev_mode:
- Installa in locale.
  1. Scarica il plug-in dev_mode per la tua piattaforma da [IBM Bluemix CLI Plugin Repository](http://plugins.ng.bluemix.net).
  2. Installa il plug-in dev_mode utilizzando il comando cf install-plugin:
  
        ```
        cf install-plugin dev_mode-linux_amd64
        ```

- Installa dal repository CLI Bluemix.
  1. Aggiungi il repository bluemix-repo nel repository CLI Cloud Foundry utilizzando il seguente comando:
  
        ```
        cf add-plugin-repo bluemix-repo http://plugins.ng.bluemix.net
        ```

  2. Immetti cf repo-plugins. Il plug-in dev_mode viene visualizzato nel repository bluemix-repo.
		
		```
        cf repo-plugins
        ```
  
  3. Installa il plug-in dev_mode nei plug-in CLI Cloud Foundry utilizzando il seguente comando:
  
        ```
        cf install-plugin dev_mode -r bluemix-repo
        ```

## Utilizzo
**Per visualizzare tutti i comandi CLI dev_mode, utilizza il seguente comando:**

```
cf plugins
```

### Comandi dev_mode

### mode

```
cf mode <nomeApplicazione> <dev|normal>
```

Modifica la modalità dell'applicazione.

### status

```
cf status <nomeApplicazione>
```

Visualizza la modalità dell'applicazione e lo stato del runtime.

### update-file

```
cf update-file <percorsoRemoto> <percorsoLocale> [opzioni_comando]
```

Aggiorna i file applicazione nel cloud.

Opzioni comando:

**expand**

Indica se i file caricati devono essere estratti dal file zip.

**restart**

Riavvia il runtime dell'applicazione dopo che i file sono stati aggiornati.
  
### delete-file

```
cf delete-file <percorsoRemoto> [opzioni_comando]
```

Elimina i file applicazione nel cloud.

Opzioni comando:

**restart**

Riavvia il runtime dell'applicazione dopo che i file sono stati eliminati.

### start-inplace

```
cf start-inplace <nomeApplicazione>
```

Avvia l'applicazione nel contenitore esistente.

### stop-inplace

```
cf stop-inplace <nomeApplicazione>
```

Arresta l'applicazione nel contenitore esistente.

### restart-inplace

```
cf restart-inplace <nomeApplicazione>
```

Riavvia l'applicazione nel contenitore esistente.



### help

```
cf help <nomeComando>
```
Visualizza la guida relativa a un comando.
