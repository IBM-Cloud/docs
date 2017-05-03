---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Aggiornamenti più recenti al pacchetto di build Liberty
{: #latest_updates}

## Un elenco degli aggiornamenti più recenti nel pacchetto di build Liberty.

### 14 marzo, 2017: pacchetto di build Liberty aggiornato v3.8-20170308-1507

* La versione del runtime Liberty predefinita è stata aggiornata alla release 17.0.0.1.
* Il runtime Liberty predefinito include la iFix PI75512 WebSockets.
* La versione del runtime Liberty è stata aggiornata alla release [2017.2.0.0](https://developer.ibm.com/wasdev/blog/2017/02/17/beta-websphere-liberty-tools-february-2017/). 
* Le versioni di IBM JRE 8 e 7.1 sono state aggiornate a SR4 FP1.
* Il supporto di configurazione automatica è stato esteso per utilizzare [ibm-websphere-extreme-scale IBM Container](https://console.ng.bluemix.net/docs/images/docker_image_extreme_scale/ibm-websphere-extreme-scale_starter.html).
* Il supporto di configurazione automatica per [Cloudant NoSQL Database](https://console.ng.bluemix.net/docs/services/Cloudant/index.html) è stato aggiornato per fornire l'opzione di utilizzare la libreria Java Cloudant invece di org.ektorp. Per abilitare l'utilizzo della libreria Java Cloudant devi configurare la seguente variabile di ambiente:    
```
cf set-env <appName> LBP_SERVICE_CONFIG_CLOUDANTNOSQLDB 'type : cloudant'
```
* Il pacchetto di build fornisce inoltre una versione aggiornata dell'agent per il [servizio Auto-Scaling](/docs/services/Auto-Scaling/index.html) e vari miglioramenti nella gestione dell'applicazione.
* Questo pacchetto di build modifica il modo in cui la configurazione automatica utilizza il [servizio Monitoring and Analytics](/docs/services/monana/index.html). Le applicazioni che utilizzano il piano gratuito non avranno più la funzionalità di registrazione aggiunta alle loro applicazioni; sta venendo sostituita da logmet.  


### 23 gennaio 2017: pacchetto di build Liberty aggiornato v3.7-20170118-2046
* La versione del runtime Liberty è stata aggiornata alla release [2017.1.0.0](https://developer.ibm.com/wasdev/blog/2017/01/20/beta-websphere-liberty-tools-january-2017/). 
* La versione di IBM JRE 8 è stata aggiornata alla versione SR3 FP22.
* Il supporto per la [configurazione automatica](autoConfig.html) è stato inoltre esteso per utilizzare il [servizio Compose for MongoDB](https://console.ng.bluemix.net/docs/services/ComposeForMongoDB/index.html) (Al momento disponibile solo con il runtime Liberty mensile).

### 13 dicembre, 2016: pacchetto di build Liberty aggiornato v3.6-20161209-1351
* La versione del runtime Liberty predefinita è stata aggiornata alla release [16.0.0.4](http://www-01.ibm.com/support/docview.wss?uid=swg27009661). 
* La versione di IBM JRE 8 è stata aggiornata alla versione SR3 FP21.
* Il supporto per la [configurazione automatica](autoConfig.html) è stato inoltre esteso per utilizzare il [servizio Compose for PostgreSQL](https://console.ng.bluemix.net/docs/services/ComposeForPostgreSQL/index.html).
* Il pacchetto di build fornisce inoltre una versione aggiornata dell'agent per il [servizio Auto-Scaling](/docs/services/Auto-Scaling/index.html).
* Il pacchetto di build è stato aggiornato per supportare le variabili di ambiente come parte delle ubicazioni incluse nei file `server.xml`.

### 29 novembre 2016: pacchetto di build Liberty aggiornato v3.5-20161114-1152
* La versione del runtime Liberty predefinita `16.0.0.3` è stata aggiornata per includere la iFix [PI62375](https://www-01.ibm.com/support/docview.wss?uid=swg24042712) e per fornire la funzione pratica `microProfile-1.0`.
* La versione del runtime Liberty è stata aggiornata alla release `2016.11.0.0`. 
* Il pacchetto di build contiene inoltre le IBM JRE aggiornate: versione 8 SR3 FP20 e versione 7.1 SR3 FP60.
* Il driver DB2 JDBC è stato aggiornato alla versione `4.21.29`.
* L'integrazione del servizio Monitoring and Analytics è stata corretta per utilizzare [Diego ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.cloudfoundry.org/concepts/diego/diego-architecture.html).
* Le integrazioni del servizio [Dynatrace](dynatrace.html) sono state aggiornate per utilizzare in modo migliore le offerte del servizio Dynatrace.
* Il supporto per la [configurazione automatica](autoConfig.html) per i tipi di servizio PostgreSQL e MySQL è stato migliorato per funzionare in modo migliore durante la distribuzione di una directory server o di un server in pacchetto.
* Il runtime Node.js utilizzato dai [programmi di utilità devconsole e shell di Gestione applicazioni](/docs/manageapps/app_mng.html#app_management) è stato aggiornato alla versione `0.12.17` più recente.
* Sono state incluse [correzioni per la protezione](http://www.ibm.com/support/docview.wss?uid=swg21994945) per il runtime di Liberty.

### 1 novembre 2016: pacchetto di build Liberty aggiornato v3.4.1-20161030-2241
* Il pacchetto di build contiene una correzione a un problema di avvio di alcuni tipi di applicazioni. Nello specifico, le applicazioni distribuite come una directory del server o come un server compresso con i file dell'applicazione nella directory `dropins`.

### 21 ottobre 2016: pacchetto di build Liberty aggiornato v3.4-20161018-2004
* La versione del runtime Liberty predefinita `16.0.0.3` è stata aggiornata per includere le iFix [PI68805](http://www-01.ibm.com/support/docview.wss?uid=swg1PI68805) e [PI69141](http://www-01.ibm.com/support/docview.wss?uid=swg1PI69141).
* La versione del runtime Liberty è stata aggiornata alla release [2016.9.0.1](https://developer.ibm.com/wasdev/blog/2016/09/23/beta-websphere-liberty-and-tools-october-2016/).
* Il pacchetto di build contiene anche una versione aggiornata di IBM JRE 8.0: SR3 FP12.
* La IBM JRE 8.0 e 7.1 sono ora configurate per abilitare [tutti i protocolli TLS quando viene richiamato `SSLContext.getContext("TLS")`](https://www.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.security.component.80.doc/security-component/jsse2Docs/matchsslcontext_tls.html) a corrispondere al funzionamento JRE di Oracle. IBM JRE 7.1 è anche configurata per abilitare [tutti i protocolli TLS quando viene richiamato `SSLContext.getDefault()`](https://www.ibm.com/support/knowledgecenter/SSYKE2_7.1.0/com.ibm.java.security.component.71.doc/security-component/jsse2Docs/overrideSSLprotocol.html) a corrispondere al funzionamento JRE 8.0 di IBM.
* Il pacchetto di build fornisce un raccoglitore di dati aggiornato per il [servizio Monitoring and Analytics](/docs/services/monana/index.html#monana_oview).
* Il pacchetto di build è stato nuovamente modificato per scaricare l'ultimo 1.5.x [MariaDB Connector/J JDBC driver ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/) quando di esegue la [configurazione automatica per il tipo MySQL dei servizi](autoConfig.html).
* Il pacchetto di build introduce il supporto alla personalizzazione del funzionamento di configurazione automatica del servizio tramite la variabile di ambiente `LBP_SERVICE_CONFIG_<serviceType>`. Ad esempio, può essere utilizzato per modificare l'ubicazione o la versione di un driver JDBC in modo da scaricare il servizio MySQL. Consulta la documentazione dei [servizi che supportano la configurazione automatica](autoConfig.html) per ulteriori informazioni.
* Il pacchetto di build include anche una serie di miglioramenti di [Diego ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.cloudfoundry.org/concepts/diego/diego-architecture.html) correlati al controllo di integrità dell'applicazione e la funzionalità [Gestione applicazione](/docs/manageapps/app_mng.html).

### 16 settembre, 2016: pacchetto di build Liberty aggiornato v3.3-20160912-1729
* La versione del runtime Liberty predefinita è stata aggiornata alla release [16.0.0.3](http://www-01.ibm.com/support/docview.wss?uid=swg27009661). La versione del runtime Liberty è stata aggiornata alla release [2016.9.0.0](https://developer.ibm.com/wasdev/blog/2016/08/26/beta-websphere-liberty-and-tools-september-2016/). Con questi aggiornamenti, le funzioni Liberty `cloudant-1.0` e `passwordUtilities-1.0`, precedentemente disponibili come funzioni beta, sono ora disponibili come funzioni pronte per la produzione.
* Sono state incluse [correzioni per la protezione](http://www-01.ibm.com/support/docview.wss?uid=swg21990527) per il runtime di Liberty.
* Il pacchetto di build contiene anche una versione aggiornata di IBM JRE 8.0: SR3 FP11.
* Il pacchetto di build è stato modificato per scaricare l'ultimo 1.4.x [MariaDB Connector/J JDBC driver ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/) quando di esegue la [configurazione automatica per il tipo MySQL dei servizi](autoConfig.html) a causa di un problema con l'ultimo 1.5.x driver.

### 26 agosto, 2016: pacchetto di build Liberty aggiornato v3.2-20160822-2200
* Il pacchetto di build contiene le versioni aggiornate di IBM JRE: 8 SR3 FP10 e 7.1 SR3 FP50.
* La versione del runtime Liberty è stata aggiornata alla release [2016.8.0.0](https://developer.ibm.com/wasdev/blog/2016/07/28/beta-websphere-liberty-and-tools-august-2016/).
* Il plug-in del servizio che fornisce il [supporto di configurazione automatica](autoConfig.html) per il servizio [SQL Database](/docs/services/SQLDB/index.html#SQLDB) è stato aggiornato per utilizzare sempre i certificati firmati JVM durante la connessione al servizio tramite TLS.

### 22 luglio 2016: pacchetto di build Liberty aggiornato v3.1-20160717-2254
* La funzionalità [Gestione applicazione](/docs/manageapps/app_mng.html) è stata aggiornata per supportare l'autenticazione federata. Inoltre, il runtime Node.js utilizzato dai programmi di utilità `devconsole` e `shell` è stato aggiornato alla versione `0.12.15` più recente.
* Il pacchetto di build aggiunge il supporto per l'agent di monitoraggio dell'applicazione [Dynatrace Ruxit ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.dynatrace.com/en/ruxit/).
* Il pacchetto di build fornisce un raccoglitore di dati aggiornato per il [servizio Monitoring and Analytics](/docs/services/monana/index.html#monana_oview).
* Il pacchetto di build fornisce inoltre una versione aggiornata dell'agent per il [servizio Auto-Scaling](/docs/services/Auto-Scaling/index.html).
* La versione del runtime Liberty è stata aggiornata alla release [2016.7.0.0](https://developer.ibm.com/wasdev/blog/2016/06/30/beta-websphere-liberty-and-tools-july-2016/).

### 17 giugno 2016: pacchetto di build Liberty aggiornato v3.0-20160608-1450
* Il pacchetto di build ora contiene due versioni di WebSphere Liberty, l'ultima release stabile e l'ultima release mensile. Nello specifico, fornisce la release stabile [16.0.0.2](http://www-01.ibm.com/support/docview.wss?uid=swg21984970) e la release mensile [2016.6.0.0](https://developer.ibm.com/wasdev/blog/2016/06/03/beta-websphere-liberty-and-tools-june-2016/). La release stabile sarà utilizzata per impostazione predefinita. Consulta [Versioni Liberty](buildpackDefaults.html#liberty_versions) per ulteriori dettagli.
* Il pacchetto di build contiene inoltre delle correzioni per la sicurezza per [Apache Standard Taglibs vulnerability](http://www-01.ibm.com/support/docview.wss?uid=swg21985531).

### 25 maggio 2016: pacchetto di build Liberty aggiornato v2.9-20160519-1249
* Il pacchetto di build contiene una versione aggiornata di WebSphere Liberty basata sul [beta di maggio](https://developer.ibm.com/wasdev/blog/2016/05/06/beta-websphere-liberty-and-tools-may-2016/). La versione aggiornata di Liberty rende disponibile le funzioni beta *bluemixLogCollector-1.1* e *logstashCollector-1.1* in Bluemix.

### 5 maggio 2016: pacchetto di build Liberty aggiornato v2.8-20160430-1011
* Il pacchetto di build contiene una versione aggiornata di WebSphere Liberty basata sul [beta di aprile](https://developer.ibm.com/wasdev/blog/2016/04/08/beta-websphere-liberty-and-tools-april-2016/). La versione aggiornata di Liberty rende disponibile la funzione GA *logstashCollector-1.0* e la funzione beta *logmetCollector-1.0* in Bluemix.
* Il pacchetto di build contiene anche le versioni aggiornate di IBM JRE: 8 SR3 e 7.1 SR3 FP40.
* Il pacchetto di build aggiunge il supporto per l'agent di monitoraggio dell'applicazione [AppDynamics ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.appdynamics.com/).
* Il supporto [Dynatrace](dynatrace.html) è stato migliorato per semplificare l'installazione dell'agent.
* Il pacchetto di build fornisce un raccoglitore di dati aggiornato per il [servizio Monitoring and Analytics](/docs/services/monana/index.html#monana_oview). Contiene una correzione per un problema con il raccoglitore dei dati di heap massimi.
* Il runtime Node.js utilizzato dai [programmi di utilità devconsole e shell di Gestione applicazioni](/docs/manageapps/app_mng.html#app_management) è stato aggiornato alla versione 0.12.13 più recente.

### 25 marzo 2016: pacchetto di build Liberty aggiornato v2.7-20160321-1358
* Il pacchetto di build contiene una versione aggiornata di WebSphere Liberty basata sul [beta di marzo](https://developer.ibm.com/wasdev/blog/2016/03/18/new-websphere-liberty-features-march-2016/). La versione aggiornata di Liberty rende disponibile la funzione beta cloudant-1.0 in Bluemix.
* Il pacchetto di build contiene anche le versioni aggiornate di IBM JRE: 8 SR2 FP12 e 7.1 SR3 FP32.
* Il pacchetto di build fornisce una versione aggiornata dell'agent per il [servizio Auto-Scaling](/docs/services/Auto-Scaling/index.html).
* Il pacchetto di build viene ora fornito con un nuovo raccoglitore di dati per il [servizio Monitoring and Analytics](/docs/services/monana/index.html#monana_oview). Il nuovo raccoglitore abilita la configurazione delle soglie di monitoraggio e contiene delle correzioni di bug.
* Il pacchetto di build fornisce una versione driver DB2® JDBC 4.19.49 aggiornata.
* Il runtime Node.js utilizzato dai [programmi di utilità devconsole e shell di Gestione applicazioni](/docs/manageapps/app_mng.html#app_management) è stato aggiornato alla versione 0.12.12 più recente.

### 7 marzo 2016: pacchetto di build Liberty aggiornato v2.6-20160225-1649
* Il pacchetto di build aggiunge il supporto per l'applicazione di monitoraggio Dynatrace. Consulta [Utilizzo di Dynatrace](dynatrace.html) per i dettagli.
* Il pacchetto di build aggiunge il supporto per [DynamicPULSE](www.fujitsu.com/jp/group/fsweb/products/dynamic-pulse/).

### 10 febbraio 2016: pacchetto di build Liberty aggiornato v2.5-20160209-1336
* Il pacchetto di build contiene una versione aggiornata di WebSphere Liberty basata sul [beta di febbraio](https://developer.ibm.com/wasdev/blog/2016/02/12/beta-websphere-liberty-and-tools-february/). La versione aggiornata del profilo Liberty rende disponibile la funzione apiDiscovery-1.0 GA in Bluemix.

### 4 febbraio 2016: pacchetto di build Liberty aggiornato v2.4-20160127-1437
* Il pacchetto di build contiene una versione aggiornata di WebSphere Liberty basata sul beta di gennaio. Con questo aggiornamento, la funzione Liberty scim-1.0, precedentemente disponibile come una funzione beta, è ora disponibile come una funzione pronta per la produzione. La versione aggiornata di Liberty rende inoltre disponibile la funzione beta passwordUtilities-1.0 in Bluemix.
* Il pacchetto di build contiene anche un aggiornamento IBM JRE 7.1 SF3 FP20 e IBM JRE 8 SR2 FP10.
* Il pacchetto di build è stato aggiornato per scaricare l'ultimo 1.x [MariaDB Connector/J JDBC driver ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/) quando di esegue la [configurazione automatica per il tipo MySQL dei servizi](autoConfig.html).

### 16 dicembre 2015: pacchetto di build Liberty aggiornato v2.3-20151208-1311
* Il pacchetto di build contiene una versione aggiornata del profilo Liberty basata sul [beta di dicembre](https://developer.ibm.com/wasdev/blog/2015/11/20/beta-was-liberty-beta-with-tools-december-2015/). La versione aggiornata del profilo Liberty rende disponibili le funzioni spnego-1.0 e wsSecuritySaml-1.1 GA e la funzione beta scim-1.0 in Bluemix.
* Il pacchetto di build contiene anche un IBM JRE 8 SR2 aggiornato.
* Il pacchetto di build è stato aggiornato per scaricare gli ultimi [9.4.x PostgreSQL JDBC driver ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://jdbc.postgresql.org/) e 1.2.x [MariaDB Connector/J JDBC driver ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/) quando si esegue la [configurazione automatica](autoConfig.html) per il tipo PostgreSQL o MySQL dei servizi.

### 23 novembre 2015: pacchetto di build Liberty aggiornato v2.2-20151119-1720
* Il pacchetto di build contiene una versione aggiornata del runtime di profilo Liberty e WebSphere eXtreme
Scale Client con le correzioni per la protezione per la [vulnerabilità di Apache Commons Collection](http://www-01.ibm.com/support/docview.wss?uid=swg21971426).
* Il pacchetto di build contiene anche una versione aggiornata del [Java MongoDB Driver ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.mongodb.org/ecosystem/drivers/java/), v2.13.3. Il nuovo driver è compatibile con MongoDB versione 2.4, 2.6 e 3.0.
* Il pacchetto di build fornisce anche una versione aggiornata del raccoglitore di dati per il [servizio Monitoring and Analytics](/docs/services/monana/index.html). Il raccoglitore di dati aggiornato offre delle funzionalità di traccia di metodo migliorate.

### 16 ottobre 2015: pacchetto di build Liberty aggiornato v2.1-20151006-0912
* Il pacchetto di build contiene una versione aggiornata del profilo Liberty basata sul [beta di ottobre](https://developer.ibm.com/wasdev/blog/2015/09/25/beta-was-liberty-beta-with-tools-october-2015/). Con questo aggiornamento, le funzioni Liberty bells-1.0, rtcomm-1.0, rtcommGateway-1.0, samlWeb-2.0, sipServlet-1.1 , precedentemente disponibili come beta, sono ora disponibili come funzioni pronte per la produzione.
* Il pacchetto di build contiene anche un IBM JRE 8 SR1 FP11 aggiornato.
* Il pacchetto di build fornisce anche diversi miglioramenti e ottimizzazioni delle prestazioni:
  * La funzione di scansione degli archivi di bean impliciti [CDI 1.2](optionsForPushing.html)
è disabilitata per impostazione predefinita quando si distribuiscono file WAR o EAR.
  * Per ridurre la dimensione del droplet, i [programmi di utilità di gestione applicazioni](/docs/manageapps/app_mng.html) evconsole e shell richiedono un'operazione di ripreparazione, invece di un riavvio.
  * La cache di classe condivisa di IBM JRE è disabilitata poiché non veniva riutilizzata nell'ambiente Bluemix.

### 18 settembre 2015: pacchetto di build Liberty aggiornato v2.0-20150914-1535
* Il pacchetto di build introduce due importanti modifiche:
  * La configurazione predefinita per i file WAR e EAR abilita le funzioni del profilo Web Java EE 7 anziché
le funzioni del profilo Web Java EE 6.
  * La versione Java predefinita è la versione 8 anziché la funzione 7.
* Fai riferimento a [Upcoming Liberty for Java buildpack changes](https://developer.ibm.com/bluemix/2015/09/08/upcoming-liberty-for-java-buildpack-changes/) per dettagli su queste modifiche e su come possono influire sulla tua applicazione.
* Il pacchetto di build introduce anche l'opzione di configurazione app_state per disabilitare la funzione appstate tramite la variabile di ambiente JBP_CONFIG_LIBERTY. La funzione appstate si integra con il processo di verifica dell'integrità di Cloud Foundry per garantire che l'applicazione Liberty venga inizializzata completamente prima di poter ricevere richieste HTTP. Per disabilitare la funzione appstate, puoi impostare la variabile di ambiente JBP_CONFIG_LIBERTY su “app_state: false”.

### 4 settembre 2015: pacchetto di build Liberty aggiornato v1.22-20150824-1104
* Il pacchetto di build supporta le [variabili di ambiente HTTP_PROXY e
HTTPS_PROXY](environmentVariables.html). Se impostate, il pacchetto di build utilizza il server proxy specificato da queste variabili di ambiente quando scarica i diversi componenti del pacchetto di build.

### 19 agosto 2015: pacchetto di build Liberty aggiornato v1.21-20150811-1342
* Il pacchetto di build contiene una versione aggiornata del profilo Liberty basata sul [beta di agosto](https://developer.ibm.com/wasdev/blog/2015/07/30/beta-was-liberty-beta-with-tools-august-2015/). La versione aggiornata del profilo Liberty rende disponibili le seguenti nuove [funzioni beta](usingBetaFeatures.html) in Bluemix: bells-1.0, rtcommGateway-1.0, samlWebSso-2.0.

### 31 luglio 2015: pacchetto di build Liberty aggiornato v1.20.1-20150729-1255
* Il pacchetto di build contiene versioni aggiornate dei JRE IBM: 7.1 SR1 FP10 r 8 SR1 FP10.
I JRE aggiornati
contengono le [ultime correzioni di sicurezza](http://www-01.ibm.com/support/docview.wss?uid=swg21964161) e altri miglioramenti.
* Il plug-in del servizio che fornisce il [supporto di configurazione automatica](autoConfig.html) per il servizio [Cloudant NoSQL Database](/docs/services/Cloudant/index.html#Cloudant) è stato aggiornato per garantire che le connessioni al servizio vengano stabilite su un canale sicuro.

### 21 luglio 2015: pacchetto di build Liberty aggiornato v1.20-20150713-1450
* Il pacchetto di build contiene una versione aggiornata del profilo Liberty basata sulla [release 8.5.5.6](https://developer.ibm.com/wasdev/blog/2015/06/25/java-ee-7-has-landed-in-was-liberty/). Con questa release, tutte le funzioni Liberty Java EE 7 precedentemente disponibili come funzioni beta sono ora disponibili come funzioni pronte per la produzione. A causa di limitazioni relative
alle porte e anche di altra natura esistenti in Bluemix, alcune funzioni come ad esempio gli EJB remoti non sono
pienamente supportati nella piattaforma.
* Il pacchetto di build riconosce ed esegue le applicazioni fornite in [distZip-style ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.gradle.org/current/userguide/application_plugin.html).
* Il pacchetto di build contiene un raccoglitore di dati aggiornato per il servizio [Monitoring and Analytics](/docs/services/monana/index.html) e WebSphere eXtreme Scale Client che supporta la nuova versione di runtime di Liberty.

### 30 giugno 2015: pacchetto di build Liberty aggiornato v1.19.1-20150622-1509
* Questa versione del pacchetto di build contiene un IBM JRE aggiornato con una correzione per la protezione per la [vulnerabilità LogJam](http://www-01.ibm.com/support/docview.wss?uid=swg21961390).
* L'agent [New Relic](newRelic.html) è stato aggiornato alla versione 3.17. La nuova versione fornisce un'integrazione migliorata con il runtime di profilo Liberty.

### 14 giugno 2015: pacchetto di build Liberty aggiornato v1.19-20150608-1717
* Il pacchetto di build contiene diversi miglioramenti alla gestione delle applicazioni che includono il supporto per la console di
sviluppo e un accesso shell basato sul web. Per i dettagli, consulta [la documentazione Gestione applicazioni](/docs/manageapps/app_mng.html).
* Il pacchetto di build contiene anche una correzione per un problema a causa del quale non era possibile
trovare la funzione Liberty per il [servizio Monitoring and Analytics](/docs/services/monana/index.html).

### 27 maggio 2015: pacchetto di build Liberty aggiornato v1.18-20150519-1642
* Il pacchetto di build contiene una versione aggiornata del profilo Liberty basata sul [beta di maggio](https://developer.ibm.com/wasdev/blog/2015/05/08/beta-liberty-and-tools-may-2015/).

### 5 maggio 2015: pacchetto di build Liberty aggiornato v1.17-20150501-1729
* Il pacchetto di build contiene una versione aggiornata del profilo Liberty basata sul [beta di aprile](https://developer.ibm.com/wasdev/blog/2015/04/10/announcing-liberty-beta-with-tools-aprilmay-2015/). Con questo aggiornamento, le funzioni Liberty jsp-2.3, el-3.0 e jdbc-4.1, precedentemente disponibili come funzioni beta, sono ora disponibili come funzioni pronte per la produzione. Inoltre, le funzioni Java EE 7 come jsf-2.2, javaMail-1.5, webProfile-7.0 e javaee-7.0 sono ora disponibili come [funzioni beta](usingBetaFeatures.html).
* Il pacchetto di build fornisce anche un supporto iniziale per Java 8. IBM JRE 7.1 continua a essere il JRE predefinito ma è possibile abilitare IBM JRE 8 per un'applicazione impostando la variabile di ambiente JBP_CONFIG_IBMJDK. È anche supportata
la configurazione della versione di OpenJDK. Per tutti i dettagli, consulta [Personalizzazione del JRE](customizingJRE.html).
* Il pacchetto di build fornisce una nuova variabile di ambiente JBP_CONFIG_LIBERTY che può essere utilizzata per
sovrascrivere l'insieme predefinito di funzioni Liberty abilitato per un'applicazione quando distribuisce un
file WAR o EAR. Per ulteriori informazioni, consulta [Applicazioni autonome](optionsForPushing.html#stand_alone_apps).
* Il plug-in di servizio per il [servizio Monitoring and Analytics](/docs/services/monana/index.html) è stato aggiornato per ridurre la dimensione dei log generati per il servizio.
* Con questa versione del pacchetto di build, la modalità di disposizione dei file applicazione nel droplet è cambiata. La modifica nella struttura dei file ha eliminato la complessità correlata a mantenere i link simbolici e non dovrebbe aver alcun impatto sulle applicazioni.

### 15 aprile 2015: pacchetto di build Liberty aggiornato v1.16-20150407-1737
* Questa versione del pacchetto di build contiene un IBM JRE 7.1-2.11 aggiornato
con una [correzione per la sicurezza per la vulnerabilità Bar Mitzvah](http://www-01.ibm.com/support/docview.wss?uid=swg21882777).
* Quando vengono distribuiti file WAR autonomi, se forniti, il pacchetto di build utilizza ora la
root di contesto specificata nel file **ibm-web-ext.xml** incorporato
come root di contesto dell'applicazione. Con questa modifica, le applicazioni precedentemente
distribuite sotto la root di contesto potrebbero essere distribuite sotto un
contesto diverso sulla base delle impostazioni contenute nel file **ibm-web-ext.xml**.

### 3 aprile 2015: pacchetto di build Liberty aggiornato v1.15-20150402-1422
* Il pacchetto di build contiene una versione aggiornata del profilo Liberty basata sul [beta di marzo](https://developer.ibm.com/wasdev/blog/2015/03/13/announcing-liberty-beta-tools-march-2015/). La versione aggiornata dei profili Liberty rende disponibile la funzione beta jsf-2.2 in Bluemix.
* Il pacchetto di build contiene anche una versione aggiornata del raccoglitore di dati per il [servizio Monitoring and Analytics](/docs/services/monana/index.html).

### 20 marzo 2015: pacchetto di build Liberty aggiornato v1.14-20150319-1159
* Questa versione del pacchetto di build contiene un IBM JRE 7.1.2.11 aggiornato con una correzione per la protezione per la [vulnerabilità FREAK](http://www-01.ibm.com/support/docview.wss?uid=swg21699864).
* Il servizio [ SQL Database](services/SQLDB/index.html#SQLDB) offre dei piani pagati
che forniscono un'opzione per connettersi al server di database sul protocollo SSL. Il supporto della configurazione automatica del pacchetto di
build per il servizio SQL Database è stato aggiornato per configurare il runtime per connettersi al database su SSL, se sono
disponibili le informazioni di connessione SSL.
* Il pacchetto di build è stato aggiornato per segnalare un errore quando viene distribuito un file WAR o EAR autonomo che
contiene un file di configurazione **server.xml ** nella root dell'archivio dell'applicazione.
* Il pacchetto di build contiene una correzione per il plug-in del servizio di configurazione automatica
di MongoDB che, in alcuni casi, generava una configurazione **server.xml** non valida.

### 10 febbraio 2015: pacchetto di build Liberty aggiornato v1.13-20150209-1122
* Il pacchetto di build contiene delle correzioni per la sicurezza per gli [Apache HttpComponents e le vulnerabilità della funzione di overlay Java](https://www-304.ibm.com/connections/blogs/PSIRT/entry/ibm_security_bulletin_multiple_vulnerabilities_fixed_in_liberty_for_java_for_ibm_bluemix_cve_2012_6153_cve_2014_3577_cve_2015_0178?lang=en_us).
* Il pacchetto di build contiene una versione aggiornata del profilo Liberty basata sul [beta di febbraio](https://developer.ibm.com/wasdev/blog/2015/02/13/announcing-liberty-beta-tools-february-2015/). La versione aggiornata del profilo Liberty fornisce una versione aggiornata della funzione WebSocket GA websocket-1.1. Rende inoltre disponibili le seguenti funzioni beta Java EE 7 in Bluemix:
  * cdi-1.2, el-3.0, jsp-2.3,  jca-1.7, jacc-1.5 e jaspic-1.1
* Il pacchetto di build fornisce l'integrazione con [ZeroTrunaround's JRebel tool ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://zeroturnaround.com/software/jrebel/). L'integrazione semplifica l'utilizzo di JRebel con le applicazioni Bluemix e l'esecuzione di aggiornamenti delle applicazioni istantanei senza ridistribuire o ripreparare l'applicazione. Sono supportate solo le applicazioni web autonome.

### 6 febbraio 2015: pacchetto di build Liberty aggiornato v1.12-20150130-1016
* Il pacchetto di build contiene una versione aggiornata del profilo Liberty basata sul [beta di gennaio](https://developer.ibm.com/wasdev/blog/2015/01/16/announcing-liberty-beta-tools-january-2015/).
* Il pacchetto di build contiene una versione snellita del raccoglitore di dati per [servizio Monitoring and Analytics](/docs/services/monana/index.html#gettingstartedtemplate).

### 23 gennaio 2015: pacchetto di build Liberty aggiornato v1.11-20150119-1511
* Il pacchetto di build contiene un IBM JRE versione 7.1 SR2 FP1 aggiornato.
* Contiene anche un WebSphere eXterme Scale Client versione 8.6.0.6 aggiornato e un agent aggiornato per il servizio di scaling automatico.
* Il supporto del servizio [New Relic](newRelic.html) è stato migliorato per supportare i servizi definiti dall'utente.
* Il pacchetto di build è stato migliorato per segnalare versioni dettagliate del profilo Liberty e di IBM JRE.

### 19 dicembre 2014: pacchetto di build Liberty aggiornato v1.10-20141218-0103
* Questo pacchetto di build fornisce una modalità di sviluppo per le applicazioni. La modalità di sviluppo
è una modalità speciale che consente agli sviluppatori di condurre molte attività per un'istanza dell'applicazione
che prima non erano possibili. Utilizzando questa funzione, questa versione di IBM Eclipse Tools for Bluemix può ora supportare il debug remoto con gli aggiornamenti file incrementali su un'applicazione Liberty in esecuzione in Bluemix. Per uno sviluppatore, ciò rende conveniente l'utilizzo di Eclipse per eseguire il debug di un'applicazione nel cloud e applicare le modifiche a tale applicazione istantaneamente.
* Il pacchetto di build contiene anche una versione aggiornata del profilo Liberty basata sul [beta di dicembre](https://developer.ibm.com/wasdev/blog/2014/12/10/announcing-liberty-beta-december/).
* Inoltre, le seguenti quattro funzioni Liberty che erano in precedenza disponibili come funzioni beta sono ore pronte per la produzione:
  * concurrent-1.0
  * jsonp-1.0
  * servlet-3.1
  * websocket-1.0.
* Il pacchetto di build fornisce l'integrazione con il servizio New Relic. Dopo che è stato eseguito il bind di un'applicazione al servizio New Relic, il pacchetto di build
scarica e configura automaticamente il runtime con l'agent New Relic.
* Il pacchetto di build ha i seguenti limiti noti:
  * quando si è in modalità di sviluppo, non è possibile eseguire il bind di un servizio SessionCache.
  * quando si è in modalità di sviluppo, non è possibile creare un dump dei thread.
  * Quando si utilizza la funzione servlet-3.1 o websocket-v1.0, non è possibile eseguire il bind del
servizio Monitoring & Analytics.

### 5 dicembre 2014: pacchetto di build Liberty aggiornato v1.9-20141202-0947
* Il pacchetto di build fornisce un supporto migliorato delle opzioni JVM. Le opzioni JVM
possono ora essere applicate con un'operazione di riavvio. La ripreparazione dell'applicazione
non è necessaria. Inoltre, le opzioni JVM predefinite sono ottimizzate per il rilevamento rapido delle possibili
condizioni di errore (e preconfigurate con un'ubicazione comune che semplifica l'individuazione dei
dump generati. Ulteriori dettagli sono forniti nell'[articolo Custom Configuration of Java JVM for the Liberty Runtime](https://developer.ibm.com/bluemix/2014/12/12/custom-configurations-java-jvm-liberty-runtime/).
* Il pacchetto di build contiene un driver JDBC DB2 aggiornato versione 4.17.29.
* Contiene anche una correzione per un problema che impediva la raccolta delle informazioni sull'utilizzo del pool di thread Liberty per il servizio Monitoring & Analytics.

### 21 novembre 2014: pacchetto di build Liberty aggiornato v1.8-20141118-1610
* Il pacchetto di build contiene un IBM JRE aggiornato versione 7.1 SR2 che fornisce una correzione per la [vulnerabilità POODLE](http://www-01.ibm.com/support/docview.wss?uid=swg21687173).
* Contiene anche una versione aggiornata del profilo Liberty basata sul [beta di novembre](https://developer.ibm.com/wasdev/blog/2014/11/07/announcing-liberty-profile-beta-november/).

### 30 ottobre 2014: pacchetto di build Liberty aggiornato v1.7-20141020-1759
* Il pacchetto di build contiene un IBM JRE aggiornato versione 7.1 SR1 FP3.
* Fornisce anche una correzione per un problema che impediva la distribuzione di applicazioni
con una configurazione server che conteneva caratteri Unicode.

### 23 ottobre 2014: pacchetto di build Liberty aggiornato v1.6-20141013-1628
* Il pacchetto di build viene ora fornito con un nuovo raccoglitore di dati per [Monitoring and Analytics](/docs/services/monana/index.html). Il nuovo raccoglitore di dati raccoglie le informazioni approfondite di diagnostica,
che abilitano gli utenti del piano di diagnostica del servizio a diagnosticare
i problemi relativi alle loro applicazioni, con una precisione fino alla specifica riga di codice.
* Il pacchetto di build contiene delle versioni aggiornate degli agent di gestione e di
scaling automatico che includono correzioni di bug e miglioramenti secondari. Include anche una versione aggiornata di [Liberty profile](https://developer.ibm.com/wasdev/) e di [Java MongoDB Driver ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.mongodb.org/ecosystem/drivers/java/), v2.12.3.
* Nella funzione cloudAutowiring, un bug che causava degli errori di aggiunta di risorse in alcune applicazioni è stato corretto.

### 3 ottobre 2014: pacchetto di build Liberty aggiornato v1.5-20140923-1143
* Con il pacchetto di build aggiornato, le applicazioni possono ora utilizzare le funzioni beta di Liberty,
comprese WebSocket 1.0, Servlet 3.1 o JAX-RS 2.0. Per ulteriori informazioni, consulta [Utilizzo delle funzioni beta](usingBetaFeatures.html).

### 30 settembre 2014: pacchetto di build Liberty aggiornato v1.4-20140908-1803
* Il pacchetto di build fornisce ora il supporto per i servizi di terze parti ElephantSQL e ClearDB MySQL Database. Il supporto di configurazione
automatica funziona anche con i servizi sperimentali posgresql e mysql. Con il nuovo totale di 13 servizi, il supporto di configurazione automatica nel pacchetto di build Liberty rende più rapido e facile l'utilizzo di servizi Bluemix nelle applicazioni Liberty.
* Durante la preparazione dell'applicazione, il pacchetto di build visualizza dei messaggi di log migliorati relativi alla configurazione automatica e alle altre azioni che esegue.
* Il pacchetto di build contiene una versione aggiornata del profilo Liberty con correzioni e miglioramenti.
* Contiene anche una versione aggiornata di IBM JRE versione 7.1 che presenta dei miglioramenti delle prestazioni. Consulta la pagina [What's new](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.71.doc/diag/preface/changes_71/changes.html) per un insieme delle modifiche in dettaglio.

### 28 agosto 2014: pacchetto di build Liberty aggiornato v1.3-20140818-1538
* Il pacchetto di build contiene anche una versione aggiornata di [ Liberty Profile](https://developer.ibm.com/wasdev/) con le correzioni e i miglioramenti più recenti.
* Questa versione del pacchetto di build corregge il supporto per la variabile di ambiente JAVA_OPTS
per passare delle opzioni JVM aggiuntive al runtime dell'applicazione.
* Corregge anche un problema che impediva la distribuzione di applicazioni Jar basate su Spring autonome.
* È ora possibile generare e scaricare tracce di snap IBM JVM utilizzando l'interfaccia utente Bluemix. Consulta l'[argomento relativo alla risoluzione dei problemi](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/troubleshooting.html) nella documentazione di IBM JVM per saperne di più sulle tracce di snap e le altre informazioni di diagnostica generate dalla JVM.

### 29 luglio 2014: pacchetto di build Liberty aggiornato v1.1-20140725-1341
* La nuova versione di Liberty Bluemix Edition è ora disponibile!
  * Con questa versione di Liberty, disponiamo di correzioni e di nuove funzioni che ti consentono di utilizzare i servizi Bluemix in modo più efficiente!
  * Con la nuova funzione CouchDB disponibile il servizio Cloudant® può ora configurarla automaticamente in modo tale che un oggetto connettore sia prontamente disponibile! Analizzare
VCAP_SERVICES e fornire i jar client ektorp non è più necessario.
* La nuova versione di IBM SDK for Java è disponibile!
  * Quando ne verrà eseguito nuovamente il push, le tue applicazioni utilizzeranno IBM SDK for Java Versione 7.1-1.0. Questo si traduce in un notevole miglioramento delle prestazioni. La tua applicazione mostra ora una migliore
velocità effettiva e un utilizzo della memoria ridotto. Per ulteriori informazioni su IBM Java SDK fai clic [qui](http://www-01.ibm.com/support/docview.wss?uid=swg21671466).

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
  * [Runtime Liberty](index.html)
  * [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
