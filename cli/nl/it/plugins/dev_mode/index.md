---

 

copyright:

  years: 2015, 2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# CLI modalità di sviluppo
{: #devmodecli}

*Ultimo aggiornamento: 11 aprile 2016*

Con l'interfaccia riga di comando in modalità di sviluppo di Bluemix (CLI dev_mode), puoi aggiornare le tue applicazioni mentre sono in esecuzione nel cloud. La CLI dev_mode è stata messa a punto come un plug-in CLI cf e supporta sia applicazioni Node.js IBM sia Liberty.
{: shortdesc}
 

Puoi eseguire le seguenti attività con la CLI dev_mode:
- Alterna la tua applicazione tra la modalità sviluppo e quella normale.
- Aggiorna i file applicazione in modo incrementale senza una nuova distribuzione.
- Avvia, arresta o riavvia la tua applicazione nel contenitore esistente.

## Installazione del plug-in dev_mode
**Prerequisito:** prima di iniziare, installa la CLI Cloud Foundry. Vedi [Inizia a codificare con l'interfaccia riga di comando Cloud Foundry](https://github.com/cloudfoundry/cli) per i dettagli. 


Utilizza uno dei seguenti metodi per installare lo strumento riga di comando dev_mode:
- Installa in locale.
  1. Scarica il plug-in dev_mode per la tua piattaforma da [IBM Bluemix CLI Plugin Repository](http://plugins.{DomainName}).
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

## Visualizzazione dei comandi dev_mode
**Per visualizzare tutti i comandi della CLI dev_mode, utilizza il seguente comando:**

```
cf plugins
```

## dev_mode CLI commands index
{: #dev_mode_cmds_index}

Utilizza l'indice nella seguente tabella in modo che faccia riferimento ai comandi CLI dev_mode utilizzati più frequentemente:

<table summary="dev_mode commands index"> 
 <thead>
 <th colspan="4">Comandi dev_mode</th>
 </thead>
 <tbody> 
 <tr> 
 <td>[help](#help)</td> 
 <td>[mode](#mode)</td> 
 <td>[status](#status)</td>
 <td>[update-file](#update_file)</td>
 </tr> 
 <tr> 
 <td>[delete-file](#delete_file)</td>
 <td>[start-inplace](#start_inplace)</td>
 <td>[stop-inplace](#stop_inplace)</td>
 <td>[restart-inplace](#restart_inplace)</td>
 </tr>
  </tbody> 
 </table> 
*Tabella 1. Comandi dev_mode*



## help
{: #help}

Visualizza la guida relativa a un comando.

```
cf help <nomeComando>
```


## mode
{: #mode}

Modifica la modalità dell'applicazione.

```
cf mode <nomeApplicazione> <dev|normal>
```
<strong>Opzioni del comando</strong>:

   <dl>
   <dt>dev</dt>
   <dd>Modalità di sviluppo.</dd>
   <dt>normal</dt>
   <dd>Modalità di produzione.</dd>
   </dl>


## status
{: #status}

Visualizza la modalità dell'applicazione e lo stato del runtime.
```
cf status <nomeApplicazione>
```



## update-file
{: #update_file}

Aggiorna i file applicazione nel cloud.

```
cf update-file <percorsoRemoto> <percorsoLocale> [opzioni_comando]
```


<strong>Opzioni del comando</strong>:

   <dl>
   <dt>expand</dt>
   <dd>Indica se i file caricati devono essere estratti dal file zip.</dd>
   <dt>restart</dt>
   <dd>Riavvia il runtime dell'applicazione dopo che i file sono stati aggiornati.</dd>
   </dl>


  
## delete-file
{: #delete_file}

Elimina i file applicazione nel cloud.

```
cf delete-file <percorsoRemoto> [opzioni_comando]
```


<strong>Opzioni del comando</strong>:
 <dl>
   <dt>restart</dt>
   <dd>Riavvia il runtime dell'applicazione dopo che i file sono stati aggiornati.</dd>
  </dl>


## start-inplace
{: #start_inplace}
Avvia l'applicazione nel contenitore esistente.

```
cf start-inplace <nomeApplicazione>
```



## stop-inplace
{: #stop_inplace}
Arresta l'applicazione nel contenitore esistente.

```
cf stop-inplace <nomeApplicazione>
```



## restart-inplace
{: #restart_inplace}

Riavvia l'applicazione nel contenitore esistente.

```
cf restart-inplace <nomeApplicazione>
```



# Link correlati
{: #rellinks}

## Link correlati
{: #general}

<!-- Include a link to your full product documentation, pricing sheet, IBM Bluemix prerequisites -->


* [CLI e strumenti di sviluppo](../../index.html#cli){:new_window}


