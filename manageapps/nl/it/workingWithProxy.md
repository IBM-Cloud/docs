---

copyright:
  years: 2016, 2017
lastupdated: "2016-07-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Gestione di un proxy
{: #working_with_proxy}



In alcuni ambienti come [Bluemix dedicato](/docs/dedicated/index.html#dedicated) e
[Bluemix locale](/docs/local/index.html#local), un proxy può essere configurato in modo che influisca
sul comportamento della tua applicazione durante le fasi di preparazione e runtime.

Puoi configurare la tua applicazione per lavorare con il proxy utilizzando le seguenti variabili di ambiente:
  * [http_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [https_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [no_proxy](http://www.gnu.org/software/wget/manual/html_node/Proxies.html)

Puoi impostare queste variabili utilizzando *cf se* oppure il file *manifest.yml*.  Se la tua applicazione
richiede delle risorse da scaricare da Internet durante la fase di preparazione ed è impostata una variabile di ambiente proxy, le risorse
verranno scaricate mediante il proxy a seconda del modo in cui vengono configurate le variabili di ambiente corrispondenti.

Ad esempio, supponiamo che tua abbia un'applicazione nodejs in esecuzione in un ambiente in cui la variabile *http_proxy* sia impostata su
*yourProxyURL*.  Supponiamo inoltre che tu voglia consentire a npm di scaricare i moduli del nodo da Internet. A tale scopo, puoi
impostare *no_proxy* su *npmjs.org*.

**Nota**: in questo caso, è possibile che la tua applicazione si avvalga del proxy durante il runtime.  Il proxy è totalmente dipendente
dall'applicazione e non viene influenzato né dal pacchetto di build né dalle tre variabili di ambiente.

## Applicazioni Java
{: #java_apps}

Per le applicazioni [Liberty for Java](/docs/runtimes/liberty/index.html) e [java_buildpack](/docs/runtimes/tomcat/index.html), le impostazioni del proxy possono essere passate al runtime tramite la variabile di ambiente **JAVA_OPTS**.  Ad esempio, puoi immettere il comando:
```
   $ cf se myApp JAVA_OPTS "-Dhttp.proxyHost=yourProxyURL -Dhttp.proxyPort=yourProxyPort"
```
{: codeblock}

e ripreparare la tua applicazione.  Al runtime, l'applicazione utilizzerà quindi le impostazioni proxy specificate. Per ulteriori informazioni sulle opzioni del proxy Java, vedi [Java Networking and Proxies](https://docs.oracle.com/javase/8/docs/technotes/guides/net/proxies.html).

# rellinks
{: #rellinks notoc}
## generale
{: #general}
* [Liberty for Java](/docs/runtimes/liberty/index.html)
* [SDK for Nodejs](/docs/runtimes/nodejs/index.html)
