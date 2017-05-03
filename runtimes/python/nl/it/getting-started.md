---

copyright:
  years: 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Introduzione a Python su Bluemix
{: #getting_started}

* {: download} Congratulazioni, hai distribuito un'applicazione di esempio Hello World su {{site.data.keyword.Bluemix}}!  Per iniziare, segui questa guida dettagliata. O <a class="xref" href="http://bluemix.net" target="_blank" title="(Scarica il codice di esempio)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Scarica codice di esempio" />scarica codice di esempio</a> o esplora da solo.

Seguendo questa guida, configurerai un ambiente di sviluppo, distribuirai un'applicazione localmente e in {{site.data.keyword.Bluemix}} e integrerai un servizio database {{site.data.keyword.Bluemix}} nella tua applicazione.

## Prerequisiti
{: #prereqs}

Avrai bisogno di quanto segue:
* [Account {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [CLI Cloud Foundry ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://git-scm.com/downloads){: new_window}
* [Python ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.python.org/downloads/){: new_window}

## 1. Clona l'applicazione di esempio
{: #clone}

Ora sei pronto per iniziare ad utilizzare l'applicazione. Clona il repository e modifica la directory in cui è ubicata l'applicazione di esempio. 
  ```
git clone https://github.com/IBM-Bluemix/get-started-python
  ```
  {: pre}
  ```
cd get-started-python
  ```
  {: pre}

  Studia i file nella directory *get-started-python* per acquisire familiarità con i contenuti.

## 2. Esegui l'applicazione localmente
{: #run_locally}

Consulta [The Hitchhiker’s Guide to Python! ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://docs.python-guide.org/en/latest/) per supporto nella configurazione di Python nel tuo sistema.
{: tip}

Installa le dipendenze elencate nel file [requirements.txt ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://pip.readthedocs.io/en/stable/user_guide/#requirements-files) per poter eseguire l'applicazione localmente.

Puoi facoltativamente utilizzare un [ambiente virtuale ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://packaging.python.org/installing/#creating-and-using-virtual-environments) per evitare di avere queste dipendenze in conflitto con quelle di altri progetti Python o del tuo sistema operativo.
{: tip}

  ```
pip install -r requirements.txt
  ```
  {: pre}

In alternativa con Python3 puoi immettere

  ```
python3 -m pip install -r requirements.txt
  ```
  {: pre}

Esegui l'applicazione.
  ```
python hello.py
  ```
  {: pre}

 Visualizza la tua applicazione in: http://localhost:8000


## 3. Prepara l'applicazione per la distribuzione
{: #prepare}

Per distribuire a {{site.data.keyword.Bluemix_notm}}, può essere utile impostare un file manifest.yml. Il manifest.yml include le informazioni di base sulla tua applicazione, come il nome, quanta memoria allocare per ogni istanza e la rotta. Abbiamo fornito un file manifest.yml di esempio nella directory `get-started-python`.

Apri il file manifest.yml e modifica `name` da `GetStartedPython` con il nome della tua applicazione, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
  - name: GetStartedPython
    random-route: true
    memory: 128M
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

Dall'interno della directory *get-started-python* trasmetti la tua applicazione a {{site.data.keyword.Bluemix_notm}}
  ```
cf push
  ```
  {: pre}

Ci può volere un minuto. Se si riscontra un errore nel processo di distribuzione puoi utilizzare il comando `cf logs <Your-App-Name> --recent` per risolverlo.

Quando la distribuzione è stata completata dovresti visualizzare un messaggio che indica che la tua applicazione è in esecuzione.  Visualizza la tua applicazione all'URL elencato nell'output del comando trasmesso.  Puoi anche immettere il
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
2. Nella sezione `Data & Analytics`, seleziona `Cloudant NoSQL DB` e `Create` il servizio.
3. Seleziona `Restage` quando richiesto. {{site.data.keyword.Bluemix_notm}} riavvierà la tua applicazione e fornirà le credenziali del database alla tua applicazione utilizzando la variabile di ambiente `VCAP_SERVICES`. Questa variabile di ambiente è disponibile solo per l'applicazione quando viene eseguita su {{site.data.keyword.Bluemix_notm}}.

Le variabili di ambiente ti abilitano a separare le impostazioni di distribuzione dal tuo codice di origine. Ad esempio, invece di impostare come hardcoded una password del database, puoi archiviarla in una variabile di ambiente di riferimento nel tuo codice di origine. [Ulteriori informazioni...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. Utilizza il database
{: #use_database}
Ora aggiorneremo il tuo codice locale per puntare a questo database. Creeremo un file json che archivierà le credenziali per i servizi che l'applicazione utilizzerà. Questo file sarà utilizzato SOLO quando l'applicazione è in esecuzione localmente. Quando è in esecuzione in {{site.data.keyword.Bluemix_notm}}, le credenziali saranno lette dalla variabile di ambiente VCAP_SERVICES.

1. Crea un file denominato `vcap-local.json` nella directory `get-started-python` con il seguente contenuto:
  ```
  {
    "services": {
      "cloudantNoSQLDB": [
        {
          "credentials": {
            "username":"CLOUDANT_DATABASE_USERNAME",
            "password":"CLOUDANT_DATABASE_PASSWORD",
            "host":"CLOUDANT_DATABASE_HOST"
          },
          "label": "cloudantNoSQLDB"
        }
      ]
    }
  }
  ```
  {: pre}

2. Torna nella IU {{site.data.keyword.Bluemix_notm}}, seleziona your App -> Connections -> Cloudant -> View Credentials

3. Copia e incolla `username`, `password` e `host` dalle credenziali negli stessi campi del file `vcap-local.json` sostituendo **CLOUDANT_DATABASE_USERNAME**, **CLOUDANT_DATABASE_PASSWORD** e **CLOUDANT_DATABASE_URL**.

4. Esegui la tua applicazione localmente.
  ```
python hello.py
  ```
  {: pre}

  Visualizza la tua applicazione in: http://localhost:8000. Tutti i nomi immessi nell'applicazione saranno ora aggiunti al database.

  La tua applicazione locale e {{site.data.keyword.Bluemix_notm}} stanno condividendo il database.  Visualizza la tua applicazione {{site.data.keyword.Bluemix_notm}} all'URL elencato nell'output del comando trasmesso precedentemente.  I nomi che aggiungi dall'applicazione dovrebbero essere visualizzati entrambi quando aggiorni i browser.

Ricorda che se non hai bisogno della tua applicazione live, arrestala così da non incorrere in alcun addebito non previsto.
{: tip}
