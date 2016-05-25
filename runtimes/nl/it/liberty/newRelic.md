---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilizzo di New Relic
{: #new_relic}

*Ultimo aggiornamento: 23 marzo 2016*

New Relic è un servizio di terze parti che fornisce delle
metriche di monitoraggio per la tua applicazione. Per ulteriori informazioni su cosa fornisce il servizio New Relic, consulta [New
Relic](http://newrelic.com/java).

In base alla [documentazione di installazione manuale dell'agent Java](https://docs.newrelic.com/docs/agents/java-agent/installation/java-agent-manual-installation), è di norma richiesto che le applicazioni Java che devono essere monitorate utilizzando il servizio New Relic siano integrate e configurate con un agent New Relic e una chiave di licenza dell'account. Nell'ambiente IBM Bluemix, è possibile ottenere un nuovo accordo di licenza e un account New Relic creando un'istanza del servizio in IBM Bluemix. È quindi possibile eseguire il bind delle applicazioni Java all'istanza del servizio New Relic e il pacchetto di build Liberty configura automaticamente l'applicazione, che è pronta a essere monitorata dal servizio New Relic.
In modo specifico, il pacchetto di build:

* fornisce all'applicazione un agent New Relic;
* ottiene il nome dell'applicazione e la chiave di licenza dalle variabili di ambiente dell'applicazione VCAP_APPLICATION e VCAP_SERVICES.
* configura le proprietà e il template di configurazione di cui ha bisogno l'agent New Relic.

Vedi la configurazione di esempio generata dal pacchetto di build Liberty per l'applicazione:

```
    -javaagent:/home/vcap/app/.new_relic_agent/new_relic_agent-3.12.0.jar
    -Dnewrelic.home=/home/vcap/app/.new_relic_agent
    -Dnewrelic.config.license_key=123456
    -Dnewrelic.config.app_name=myapp
    -Dnewrelic.config.log_file_path=../../../../../logs
```
{: #codeblock}

## Aggiungi un servizio New Relic
{: #add_new_relic}

Per fare in modo che un'applicazione Java esistente sia monitorata con New Relic in IBM Bluemix, attieniti alla seguente procedura.
1. Crea un'istanza del servizio New Relic in IBM Bluemix.
```
    $ cf create-service newrelic standard mynewrelic
```
{: #codeblock}

2. Distribuisci la tua applicazione a IBM Bluemix con il servizio New Relic.  Consulta il seguente manifest dell'applicazione
di esempio:
```
        ---
        applications:
        - name: myapp
         memory: 1G
         instances: 1
         host: myapp
         domain: mybluemix.net
         path: myapp.war
         services:
          - mynewrelic
```
{: #codeblock}

3. Accedi al dashboard New Relic dalla tua applicazione direttamente dal dashboard IBM Bluemix della tua applicazione.

### Aggiungi un servizio New Relic fornito dall'utente
{: #add_user_provided_new_relic}

Se hai un account e una chiave di licenza New Relic esistenti, puoi eseguire il bind del servizio New Relic esistente alla tua applicazione utilizzando un "servizio fornito dall'utente".

1. Crea un'istanza del servizio fornito dall'utente utilizzando la tua chiave di licenza esistente.  Ad esempio, se la tua chiave di licenza esistente è 1234567, puoi utilizzare la CLI CF per eseguire una creazione del servizio fornito dall'utente ("create-user-provided-service") e fornire la chiave di licenza 1234567 al prompt come segue:
```
    $ cf create-user-provided-service mynewrelic -p "licenseKey"
    licenseKey> 1234567
```
{: #codeblock}

2. Distribuisci la tua applicazione a IBM Bluemix con l'istanza del servizio New Relic fornito dall'utente.  Il seguente è un manifest
dell'applicazione di esempio che utilizza un'istanza del servizio New Relic
fornito dall'utente:
```
        ---
        applications:
        - name: myapp
         memory: 1G
         instances: 1
         host: myapp
         domain: mybluemix.net
         path: myapp.war
         services:
          - mynewrelic
```
{: #codeblock}

3. Accedi al dashboard New Relic per visualizzare le metriche dell'applicazione.

La configurazione automatica del servizio New Relic è diversa dalla configurazione automatica di altri servizi poiché è un servizio gestito dal contenitore che viene reso disponibile mediante il framework del pacchetto di build.  Poiché viene
reso disponibile mediante il framework, la configurazione automatica per questo servizio è diversa dagli altri servizi in tre modi:
* La non inclusione (opt-out) non è un'opzione.
* L'integrazione del servizio si basa sull'agent di New Relic, un agent Java. Viene pertanto configurato mediante le opzioni Java invece che mediante le variabili cloud nel file server.xml.
* La configurazione si basa sia su VCAP_SERVICES sia su VCAP_APPLICATION.

# rellinks
## general
* [Runtime Liberty](index.html)
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
