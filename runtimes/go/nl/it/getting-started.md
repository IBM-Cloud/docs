---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Introduzione a Go su Bluemix

* {: download} Congratulazioni, hai distribuito un'applicazione di esempio Hello World su {{site.data.keyword.Bluemix}}!  Per iniziare, segui questa guida dettagliata. O <a class="xref" href="http://bluemix.net" target="_blank" title="(Scarica il codice di esempio)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Scarica codice di esempio" />scarica codice di esempio</a> o esplora da solo.

Seguendo questa guida, configurerai un ambiente di sviluppo, distribuirai un'applicazione localmente e in {{site.data.keyword.Bluemix}} e integrerai un servizio database {{site.data.keyword.Bluemix}} nella tua applicazione.

## Prerequisiti
{: #prereqs}

Avrai bisogno di quanto segue:
* [Account {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [CLI Cloud Foundry ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://git-scm.com/downloads){: new_window}
* [Go ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://golang.org/dl/){: new_window}

## 1. Configura l'ambiente locale e clona l'applicazione di esempio
{: #clone}

Per prima cosa configureremo l'ambiente locale per assicurarci che tutte le variabili GO siano configurate correttamente. Ad esempio:
```
mkdir $HOME/work
export GOPATH=$HOME/work
export PATH=$PATH:$GOPATH/bin
```

Modifica il percorso in $GOPATH/src
```
mkdir $GOPATH/src
cd $GOPATH/src
```

Ora sei pronto per iniziare ad utilizzare l'applicazione Go *hello world*. Clona il repository e modifica la directory in cui è ubicata l'applicazione di esempio.
```
go get github.com/IBM-Bluemix/get-started-go
```
{: pre}
```
cd github.com/IBM-Bluemix/get-started-go
```
{: pre}

Studia i file nella directory *get-started-go* per acquisire familiarità con i contenuti.

## 2. Esegui l'applicazione localmente
{: #run_locally}

  {: pre}

  Crea ed esegui l'applicazione.
  ```
make
  ```
  {: pre}

  ```
go run main.go
  ```
  {: pre}

  Visualizza la tua applicazione in: http://localhost:8080

Utilizza *Ctrl-c* per arrestare la tua applicazione dalla stessa finestra in cui hai avviato l'applicazione.
{: tip}

## 3. Prepara l'applicazione per la distribuzione
{: #prepare}

Per distribuire a {{site.data.keyword.Bluemix_notm}}, può essere utile impostare un file manifest.yml. Il manifest.yml include le informazioni di base sulla tua applicazione, come il nome, quanta memoria allocare per ogni istanza e la rotta. Abbiamo fornito un file manifest.yml di esempio nella directory `get-started-go`.

Apri il file manifest.yml e modifica `name` da `GetStartedGo` con il nome della tua applicazione, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
 applications:
 - name: GetStartedGo
   random-route: true
   memory: 128M
   buildpack: go_buildpack
  ```
  {: codeblock}

In questo file manifest.yml, **random-route: true** genera una rotta casuale per la tua applicazione per evitare il conflitto con altre rotte.  Se scegli di farlo, puoi sostituire **random-route: true** con **host: myChosenHostName**, fornendo un nome host di tua scelta. [Ulteriori informazioni...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Distribuisci l'applicazione
{: #deploy}
Puoi utilizzare la CLI Cloud Foundry per distribuire le applicazioni.

Scegli il tuo endpoint API
   ```
cf api <API-endpoint>
   ```
   {: pre}

Sostituisci *API-endpoint* nel comando con un endpoint API dal seguente elenco.

|URL                             |Regione          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | Stati Uniti Sud       |
| https://api.eu-gb.bluemix.net  | Regno Unito |
| https://api.au-syd.bluemix.net | Sydney         |

Accedi al tuo account {{site.data.keyword.Bluemix_notm}}

  ```
cf login
  ```
  {: pre}

Dall'interno della directory *get-started-go* trasmetti la tua applicazione a {{site.data.keyword.Bluemix_notm}}
  ```
cf push
  ```
  {: pre}

Ci può volere un minuto. Se si riscontra un errore nel processo di distribuzione puoi utilizzare il comando `cf logs <Your-App-Name> --recent` per risolverlo.

Quando la distribuzione è stata completata dovresti visualizzare un messaggio che indica che la tua applicazione è in esecuzione.  Visualizza la tua applicazione all'URL elencato nell'output del comando trasmesso. Puoi anche immettere il

   ```
cf apps
    ```
  {: pre}
comando per visualizzare lo stato delle tue applicazioni e l'URL.

## 5. Aggiungi un database
{: #add_database}

Successivamente, aggiungeremo un database NoSQL a questa applicazione e la configureremo in modo che possa essere eseguita localmente o su {{site.data.keyword.Bluemix_notm}}.

1. Accedi a {{site.data.keyword.Bluemix_notm}} nel tuo browser. Seleziona il `Dashboard`. Seleziona la tua applicazione facendo clic sul relativo nome nella colonna `Name`.
2. Fai cli su `Connections` e su `Connect new`.
3. Nella sezione `Data & Analytics`, seleziona `Cloudant NoSQL DB` e `Create` il servizio.
4. Seleziona `Restage` quando richiesto. {{site.data.keyword.Bluemix_notm}} riavvierà la tua applicazione e fornirà le credenziali del database alla tua applicazione utilizzando la variabile di ambiente `VCAP_SERVICES`. Questa variabile di ambiente è disponibile solo per l'applicazione quando viene eseguita su {{site.data.keyword.Bluemix_notm}}.

Le variabili di ambiente ti abilitano a separare le impostazioni di distribuzione dal tuo codice di origine. Ad esempio, invece di impostare come hardcoded una password del database, puoi archiviarla in una variabile di ambiente di riferimento nel tuo codice di origine. [Ulteriori informazioni...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. Utilizza il database 
{: #use_database}
Ora aggiorneremo il tuo codice locale per puntare a questo database. Creeremo un file json che archivierà le credenziali per i servizi che l'applicazione utilizzerà. Questo file sarà utilizzato SOLO quando l'applicazione è in esecuzione localmente. Quando è in esecuzione in {{site.data.keyword.Bluemix_notm}}, le credenziali saranno lette dalla variabile di ambiente VCAP_SERVICES.

1. Crea un file denominato `.env` nella directory `get-started-go` con il seguente contenuto:
  ```
  CLOUDANT_URL=
  ```
  {: pre}

2. Torna nella IU {{site.data.keyword.Bluemix_notm}}, seleziona your App -> Connections -> Cloudant -> View Credentials

3. Copia e incolla solo l'`url` dalle credenziali nel campo `CLOUDANT_URL` del file `.env` e salva le modifiche.  Il risultato sarà qualcosa di simile:
  ```
  CLOUDANT_URL=https://123456789 ... bluemix.cloudant.com
  ```

4. Esegui la tua applicazione localmente. 
  ```
go run main.go
  ```
  {: pre}

  Visualizza la tua applicazione in: http://localhost:8080. Tutti i nomi immessi nell'applicazione saranno ora aggiunti al database.

  La tua applicazione locale e {{site.data.keyword.Bluemix_notm}} stanno condividendo il database.  Visualizza la tua applicazione {{site.data.keyword.Bluemix_notm}} all'URL elencato nell'output del comando trasmesso precedentemente.  I nomi che aggiungi dall'applicazione dovrebbero essere visualizzati entrambi quando aggiorni i browser.


Ricorda che se non hai bisogno della tua applicazione live, arrestala così da non incorrere in alcun addebito non previsto.
{: tip}
