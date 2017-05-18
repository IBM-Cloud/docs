---

copyright:
  years: 2016, 2017
lastupdated: "2017-4-4"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Informazioni su Delivery Pipeline
{: #deliverypipeline_about}

Il servizio IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}}, anche conosciuto come pipeline, automatizza la distribuzione continua dei tuoi progetti Bluemix. In una pipeline, le sequenze di fasi richiamano l'input ed eseguono i lavori, come le build, i test e le distribuzioni.
{:shortdesc}

Le seguenti sezioni descrivono i dettagli concettuali dietro le pipeline.

## Fasi
{: #deliverypipeline_stages}

Le fasi organizzano l'input e i lavori e come il tuo codice viene generato, distribuito e verificato. Le fasi accettano l'input dai repository di controllo dell'origine (repository SCM) o dai lavori di creazione (risorse utente di creazione) in altri fasi. Quando crei la tua prima fase, vengono ti configurate le impostazioni predefinite nella scheda **INPUT**.

L'input di una fase viene trasmesso ai lavori contenuti nella fase e ad ogni lavoro viene assegnato un contenitore vuoto in cui essere eseguito. Il lavori in una fase non possono trasmettere le risorse utente tra di loro.

Puoi definire le proprietà dell'ambiente della fase che possono essere utilizzate in tutti i lavori. Ad esempio, puoi definire la proprietà `TEST_URL` che trasmette un solo URL per distribuire e verificare i lavori in una singola fase. Il lavoro di distribuzione sarà distribuito a tale URL e il lavoro di verifica verificherà l'applicazione in esecuzione in tale URL.

Per impostazione predefinita, in una fase le creazioni e le distribuzioni vengono eseguite automaticamente ogni volta che si distribuiscono delle modifiche al repository SCM di un progetto. Le fasi e i lavori vengono eseguiti serialmente; abilitano il controllo del flusso per il tuo lavoro. Ad esempio, puoi posizionare una fase di verifica prima di una fase di distribuzione. Se le verifiche nella fase di verifica hanno esito negativo, la fase di distribuzione non sarà eseguita.

Potresti desiderare di avere maggiore controllo su una fase specifica. Se non desideri che una fase venga eseguita ogni volta che viene effettuata una modifica nel relativo input, puoi disabilitare tale funzionalità. Nella scheda **INPUT**, nella sezione Stage Trigger, fai clic su **Run jobs only when this stage is run manually**.

![La scheda INPUT](images/input_tab_only_execute.png)

## Lavori
{: #deliverypipeline_jobs}

Il lavoro è un'unità di esecuzione in una fase. Una fase può contenere più lavori e i lavori in una fase vengono eseguiti in sequenza. Per impostazione predefinita, se un lavoro ha esito negativo, il lavoro seguente nella fase non viene eseguito.

![Crea e verifica i lavori in una fase](images/jobs.png)

I lavori vengono eseguiti in directory di lavoro separate all'interno dei contenitori Docker che sono stati creati per ogni esecuzione della pipeline. Prima che un lavoro venga eseguito, la relativa directory di lavoro viene compilata con l'input definito al livello della fase. Ad esempio, puoi avere una fase che contiene un lavoro di verifica e un lavoro di distribuzione. Se installi le dipendenze su un lavoro, non sono disponibili per un altro lavoro. Tuttavia, se rendi le dipendenze disponibili nell'input della fase, sono disponibili per entrambi i lavori.

Con eccezione dei lavori di creazione di tipo semplice, quando configuri un lavoro, puoi includere gli script shell UNIX che includono i comandi di creazione, verifica o distribuzione. Poiché i lavori sono eseguiti in un contenitore ad hoc, le azioni di un contenitore non possono influenzare gli ambienti di esecuzione di altri lavori, anche se tali lavori sono parte della stessa fase.

In aggiunta, i lavori della pipeline possono eseguire solo i seguenti comandi come `sudo`:
  * `/usr/sbin/service`
  * `/usr/bin/apt-get`
  * `/usr/bin/apt-key`
  * `/usr/bin/dpkg`
  * `/usr/bin/add-apt-repository`
  * `/opt/IBM/node-v0.10.40-linux-x64/npm`
  * `/opt/IBM/node-v0.12.7-linux-x64/npm`
  * `/opt/IBM/node-v4.2.2-linux-x64/npm`
  * `/usr/bin/Xvfb`
  * `/usr/bin/pip`


Dopo l'esecuzione di un lavoro, il contenitore creato per esso viene eliminato. I risultati di un'esecuzione di un lavoro possono essere conservati, ma l'ambiente nel quale è stato eseguito non può esserlo.

**Nota**: i lavori possono essere eseguiti fino a un massimo di 60 minuti. Quando i lavori superano tale limite, vengono considerati con esito negativo. Se un lavoro sta per superare il limite, suddividilo in più lavori. Ad esempio, se un lavoro esegue tre attività, puoi suddividerlo in tre lavori: uno per ogni attività.

Per maggiori informazioni su come aggiungere un lavoro a una fase, consulta [Aggiunta di un lavoro a una fase](/docs/services/ContinuousDelivery/pipeline_build_deploy.html#deliverypipeline_add_job){: new_window}.

### Lavori di creazione

I lavori di creazione compilano il tuo progetto durante la preparazione per la distribuzione. Essi generano delle risorse utente che possono essere inviate a una directory di archivio di creazione, sebbene per impostazione predefinita, le risorse utente vengono posizionate nella directory root del progetto.

I lavori che ricevono l'input dai lavori di creazione devono far riferimento alle risorse utente di creazione nella stessa struttura in cui sono state create. Ad esempio, se un lavoro di creazione archivia le risorse utente di creazione in una directory `output`, uno script di distribuzione deve fare riferimento alla directory `output` anziché alla directory root del progetto per distribuire il progetto compilato. Puoi specificare la directory di archivio immettendo il nome directory nel campo **Build Archive Directory**. Lasciando il campo vuoto, si archivierà la directory root.

**Nota**: se selezioni il tipo di builder **Semplice** per un lavoro di creazione, puoi saltare il processo di creazione. In questo caso, il tuo codice non è compilato, ma è stato inviato alla fase di distribuzione così come è. Per creare e distribuire, selezionare un tipo di builder diverso da **Semplice**.

#### Proprietà dell'ambiente per gli script di creazione
Puoi includere le proprietà dell'ambiente nei comandi shell di creazione del lavoro di creazione. Le proprietà forniscono l'accesso alle informazioni sull'ambiente di esecuzione del lavoro. Per ulteriori informazioni, consulta [Risorse e proprietà dell'ambiente per il servizio {{site.data.keyword.deliverypipeline}}](/docs/services/ContinuousDelivery/pipeline_deploy_var.html).

### Lavori di distribuzione

I lavori di distribuzione caricano il tuo progetto in Bluemix come un'applicazione e sono accessibili da un URL. Dopo che il progetto è stato distribuito, puoi trovare l'applicazione distribuita nel tuo dashboard Bluemix.

I lavori di distribuzione possono distribuire nuove applicazioni o aggiornare applicazioni esistenti. Anche se hai prima distribuito un'applicazione utilizzando un altro metodo, come l'interfaccia della riga di comando Cloud Foundry o la barra di esecuzione nell'IDE web, puoi aggiornare l'applicazione utilizzando un lavoro di distribuzione. Per aggiornare un'applicazione, nel lavoro di distribuzione, utilizza il nome dell'applicazione.

Puoi eseguire la distribuzione a uno o più regioni e servizi. Ad esempio, puoi impostare il tuo {{site.data.keyword.deliverypipeline}} per utilizzare uno o più servizi, eseguire verifiche in una regione e distribuire in produzione in più regioni. Per ulteriori informazioni, consulta [Regioni](/docs/overview/whatisbluemix.html#ov_intro_reg){: new_window}.

#### Proprietà dell'ambiente per gli script di distribuzione

Puoi includere le proprietà dell'ambiente in uno script di distribuzione del lavoro di distribuzione. Queste proprietà forniscono l'accesso alle informazioni sull'ambiente di esecuzione del lavoro. Per ulteriori informazioni, consulta [Risorse e proprietà dell'ambiente per il servizio {{site.data.keyword.deliverypipeline}}](/docs/services/ContinuousDelivery/pipeline_deploy_var.html).

### Lavori di verifica
Se desideri richiedere che vengano rispettate le condizioni, includi i lavori di verifica prima o dopo i tuoi lavori di distribuzione o di creazione. Puoi personalizzare i lavori di verifica in modo che siano semplici o complessi a secondo dei tuoi bisogni. Ad esempio, puoi immettere un comando cURL e attendere una risposta particolare. Puoi anche eseguire una suite di verifiche dell'unità o di verifiche funzionali dell'esecuzione con servizi di verifica di terze parti, come ad esempio Sauce Labs.

Se le tue verifiche producono dei file dei risultati nel formato XML JUnit, viene visualizzato un report che si basa sui file dei risultati nella scheda **Tests** per ogni pagina del risultato della verifica. Se una verifica ha esito negativo, anche il lavoro ha esito negativo.

#### Proprietà dell'ambiente per gli script di verifica

Puoi includere le proprietà dell'ambiente nello script del lavoro di verifica. Le proprietà forniscono l'accesso alle informazioni sull'ambiente di esecuzione del lavoro. Per ulteriori informazioni, consulta [Risorse e proprietà dell'ambiente per il servizio {{site.data.keyword.deliverypipeline}}](/docs/services/ContinuousDelivery/pipeline_deploy_var.html).

## File manifest
{: #deliverypipeline_manifest}

I file manifest, denominati `manifest.yml` sono archiviati nella directory root del progetto e controllano come il tuo progetto viene distribuito a Bluemix. Per informazioni sulla creazione dei file manifest per un progetto, consulta la [documentazione Bluemix sui manifest dell'applicazione](/docs/manageapps/depapps.html#appmanifest). Per l'integrazione con Bluemix, il tuo progetto deve disporre di un file manifest nella relativa directory root. Tuttavia, non è obbligatorio eseguire la distribuzione in base alle informazioni nel file.

Nella pipeline, puoi specificare tutte le informazioni sul file manifest utilizzando gli argomenti del comando `cf push`. Gli argomenti del comando `cf push` sono utili nei progetti con più destinazioni di distribuzione. Se più lavori di distribuzione tentano tutti di utilizzare la rotta specificata nel file manifest del progetto, si verifica un conflitto.

Per prevenire i conflitti, puoi specificare una rotta utilizzando `cf push` seguito all'argomento del nome host, `-n` e un nome della rotta. Modificando lo script di distribuzione per le singole fasi, puoi prevenire conflitti di rotta quando distribuisci a più destinazioni.

Per utilizzare gli argomenti del comando `cf push`, apri le impostazioni di configurazione per un lavoro di distribuzione e modifica il campo **Deploy Script**. Per ulteriori informazioni, consulta la documentazione [Cloud Foundry Push ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push){: new_window}.

## Una pipeline di esempio
{: #deliverypipeline_example}

Una pipeline di esempio può contenere tre fasi:

1. Una fase di build che compila ed esegue i processi di creazione su un'applicazione.
2. Una fase di verifica che distribuisce un'istanza dell'applicazione e successivamente esegue le verifiche su di essa.
3. Una fase di produzione che distribuisce un'istanza di produzione dell'applicazione verificata.

Questa pipeline viene mostrata nel seguente diagramma concettuale:

![Un diagramma concettuale di fasi e lavori in una pipeline](images/diagram.jpg)

*Un modello concettuale di una pipeline a tre fasi*

Le fasi ricevono i loro input dai repository e dai lavori di creazione e i lavori all'interno di una fase eseguono in sequenza e indipendentemente ogni lavoro. Nella pipeline di esempio, le fasi sono eseguite in sequenza, anche se le fasi di verifica e produzione prendono entrambe l'output della fase di build come proprio input.
