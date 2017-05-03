---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Risoluzione dei problemi di Liberty for Java
{: #ts}


Sono qui riportate le risposte alle domande comuni di risoluzione dei problemi sull'utilizzo di Liberty for Java su {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## L'applicazione non riesce ad iniziare ad accettare le connessioni
{: #health_check_timeout}


L'avvio dell'applicazione Liberty non riesce a causa dell'errore “Failed to start accepting connections”. Ad esempio, l'errore nei log può essere simile al seguente:
{: tsSymptoms}

```
   2016-11-14T14:44:58.45+0000 [API/0]      OUT App instance exited with guid 21ac63eb-9595-428a-94c7-b0b02aaf77cc payload: {"cc_partition"=>"default", "droplet"=>"21ac63eb-9595-428a-94c7-b0b02aaf77cc", "version"=>"b2772438-92de-4d47-b680-ea772ac2288a", "instance"=>"f4799c8c89214bbd8067883c3ffe23e0", "index"=>0, "reason"=>"CRASHED", "exit_status"=>255, "exit_description"=>"failed to accept connections within health check timeout", "crash_timestamp"=>1479134698} 2016-11-14T14:45:07.50+0000 [DEA/4]      ERR Instance (index 0) failed to start accepting connections
```
{: #codeblock}

Bluemix esegue un controllo di integrità sull'applicazione per controllare se è stata avviata correttamente. Il controllo di integrità verifica se l'applicazione è in ascolto sulla porta assegnata all'applicazione. Il timeout predefinito per questo controllo è di 60 secondi e alcune applicazioni possono impiegare più di 60 secondi ad avviarsi. Esistono molti motivi per cui l'applicazione può impiegare molto tempo ad avviarsi. Ad esempio, l'associazione di servizi come [Monitoring and Analytics](/docs/services/monana/index.html#gettingstartedtemplate) o [New Relic](/docs/runtimes/liberty/newRelic.html) o [abilitazione del programma di debug](/docs/manageapps/app_mng.html#debug) aumenteranno il tempo di avvio. L'applicazione potrebbe inoltre eseguire i passi di inizializzazione che possono impiegare molto tempo per il completamento.
{: tsCauses}

Per prima cosa, esamina i log per ogni errore ovvio che può aver causato il malfunzionamento dell'applicazione Liberty. Se non è stato trovato alcun errore ovvio tenta quanto segue:
{: tsResolve}

### **Incrementa il timeout del controllo di integrità. **

* Quando distribuisci l'applicazione utilizzando il comando “cf push” specifica un timeout di avvio dell'applicazione più lungo utilizzando l'opzione “-t”. Ad esempio:

        $ cf push myApp -t 180
        {: #codeblock}

* Il timeout del controllo di integrità può inoltre essere specificato nel file manifest.yml. Ad esempio:

        ---
           ...
           timeout: 180
        {: #codeblock}

### **Disabilita la funzione appstate. **

La funzione appstate si integra con il processo di verifica dell'integrità di Bluemix per garantire che l'applicazione Liberty venga inizializzata completamente prima di poter ricevere richieste HTTP. Come l'applicazione è completamente inizializzata, la funzione appstate non ha più effetto.  L'effetto collaterale di questa funzione è che alcune applicazioni potrebbero richiedere più tempo per avviarsi. Per disabilitare la funzione appstate, imposta la seguente proprietà di ambiente sulla tua applicazione e ripreparala:

```
$ cf set-env myApp JBP_CONFIG_LIBERTY “app_state: false”
```
{: #codeblock}

### **Considera di rieseguire il factoring dell'applicazione. **

Se la tua applicazione impiega troppo tempo ad inizializzarsi, potresti dover rieseguire il factoring dell'applicazione per effettuare un'inizializzazione asincrona e/o lenta.

### **Distribuisci con l'opzione “no-route”.**

1. Distribuisci la tua applicazione con l'opzione “--no-route”. Questo disabiliterà il controllo di integrità della porta. Ad esempio:

        $ cf push myApp –no-route
        {: #codeblock}

2. Dopo aver inizializzato l'applicazione, associa una rotta all'applicazione. Ad esempio:

        $ cf map-route myApp mybluemix.net
        {: #codeblock}

## Errori SSL con il gateway di IBM
{: #ssl_handshake_failure}


I seguenti errori sono visualizzati nei log e l'applicazione potrebbe non avviarsi:
{: tsSymptoms}

```
    2016-11-03T12:32:44.82-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error 2016-11-03T12:32:44.83-0200 [App/0]      ERR [ERROR   ] CWPKI0022E: SSL HANDSHAKE FAILURE:  A signer with SubjectDN CN=*.gateway.prd.na.ca.ibmserviceengage.com, O=International Business Machines Corp., L=Armonk, ST=New York, C=US was sent from the target host.  The signer might need to be added to local trust store /home/vcap/app/wlp/usr/servers/defaultServer/resources/security/key.jks, located in SSL configuration alias defaultSSLConfig.  The extended error message from the SSL handshake exception is: PKIX path building failed: java.security.cert.CertPathBuilderException: PKIXCertPathBuilderImpl could not build a valid CertPath.; internal cause is: 2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: The certificate issued by CN=DigiCert Global Root CA, OU=www.digicert.com, O=DigiCert Inc, C=US is not trusted; internal cause is: 2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error
```
{: codeblock}

Gli errori possono essere stati generati quando il servizio Monitoring & Analytics viene associato a un'applicazione Liberty e tale applicazione è stata distribuita come una directory del server o un server compresso che contiene il file server.xml che configura la funzione Liberty ssl-1.0. Il bind del servizio Monitoring & Analytics all'applicazione Liberty impedisce al runtime di collegarsi al servizio tramite una connessione sicura. Tale connessione sicura viene stabilita utilizzando le impostazioni SSL predefinite. Poiché, le impostazioni SSL predefinite vengono specificate nel file server.xml di Liberty, il truststore configurato non può rendere attendibile il certificato utilizzato dal servizio Monitoring & Analytics.
{: tsCauses}

Modifica la configurazione per utilizzare il truststore di JVM con una delle seguenti opzioni.  Assicurati di ripreparare la tua applicazione dopo aver effettuato la modifica.
{: tsResolve}

### Aggiorna il server.xml di Liberty

Aggiorna il server.xml in modo che utilizzi il file cacerts di JVM come truststore. Aggiungi quanto segue al tuo file server.xml:

        <ssl id="defaultSSLConfig" trustStoreRef="defaultTrustStore"/>
        <keyStore id="defaultTrustStoretore" location="${java.home}/lib/security/cacerts"/>
        {: codeblock}

### Aggiorna il truststore configurato

Modifica il truststore configurato per rendere attendibile la CA RADICE DigitCert.
  1. Scarica la CA radice da https://www.digicert.com/CACerts/DigiCertGlobalRootCA.crt. 
  2. Supponendo che viene utilizzato resources/security/key.jks come truststore, importa la CA nella chiave utilizzando il programma di utilità dello strumento chiave di Java. 

            $ keytool -importcert --storepass <keyStorePassword> -keystore &lt;path&gt;/resources/security/key.jks -file DigiCertGlobalRootCA.crt
            {: codeblock}
