---

copyright:
  years: 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Scrittura delle applicazioni web Java sicure
{: #secure_java_web_app}

Tutte le applicazioni web devono essere progettate e codificate tenendo presente la sicurezza per evitare di introdurre vulnerabilità di sicurezza gravi.
{: shortdesc}

{{site.data.keyword.Bluemix}} fornisce un'applicazione starter sicura per aiutarti a scrivere codice Java Liberty più sicuro e per prevenire molti problemi XSS (Cross-Site Scripting). Puoi scaricare questa [applicazione starter sicura](https://github.com/IBM-Bluemix/java-secure-app), eseguirne la build e distribuirla localmente e su {{site.data.keyword.Bluemix_notm}}.

## Perché scrivere applicazioni web sicure
{: #why}

Una vulnerabilità di sicurezza può essere sfruttata da vari attacchi alla sicurezza. Un attacco potrebbe rubare le credenziali, causare perdita di dati e di funzionalità, interrompere i servizi e danneggiare la reputazione e il rinnovo di un business. Cross-Site-Scripting, XSS, è una delle vulnerabilità di sicurezza comuni che si trova in molte applicazioni web che deve essere evitata.

Invece di imparare la teoria degli attacchi XSS e le tecniche correttive prima di iniziare lo sviluppo dell'applicazione web, puoi utilizzare questa [applicazione starter sicura](https://github.com/IBM-Bluemix/java-secure-app). L'applicazione starter sicura include esempi di codifica delle procedure di codifica sicure importanti che impediscono un XSS in modo che puoi iniziare a sviluppare mentre impari e applichi le tecniche di prevenzione XSS.

## Come utilizzare l'applicazione di esempio sicura
{: #how}

Puoi utilizzare l'[applicazione starter sicura](https://github.com/IBM-Bluemix/java-secure-app) come punto di partenza per lo sviluppo della nuova applicazione Liberty. Inizia imparando il codice delle contromisure XSS nell'applicazione e quindi applicalo alle operazioni dell'API dell'applicazione. Le contromisure nell'applicazione starter sicura aiutano ad evitare input utente dannoso che danneggia la tua applicazione sul server o sul browser mitigando o prevenendo gli attacchi XSS.

Per prima cosa, scarica questa applicazione starter sicura, quindi eseguine la build e distribuiscila a Bluemix o localmente nello stesso modo dell'applicazione di esempio [getting-started-java](https://github.com/IBM-Bluemix/get-started-java).  Vai a [Introduzione a Liberty su Bluemix](getting-started.html) per ulteriori informazioni sulla build e la distribuzione delle applicazioni in Bluemix.  Per iniziare, puoi utilizzare questi passi per clonare, eseguire la build ed eseguire l'applicazione.

```
git clone https://github.com/IBM-Bluemix/java-secure-app
cd java-secure-app
mvn install liberty:run-server
```
Visualizza l'applicazione all'indirizzo http://localhost:9080/GetStartedSecureJava/

## Ulteriori informazioni 
{: more}
L'applicazione starter sicura contiene **BadServlet.java**. Questa applicazione illustra un esempio di codice non sicuro che gli sviluppatori potrebbero scrivere se non viene prestata attenzione.

L'applicazione starter sicura contiene inoltre **GoodServlet.java**, che include molte buone procedure di codifica sicura come la convalida dell'input, la codifica dell'output, le impostazioni dell'intestazione HTTP sicure e la politica di sicurezza del contenuto. Queste procedure sono contromisure chiave per XSS. Applicandole è anche possibile mitigare altre vulnerabilità come gli attacchi di attraversamento delle cartelle (directory traversal) e di injection.

Fai riferimento a [XSS Prevention Cheat Sheet ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.owasp.org/index.php/XSS){: new_window} per ulteriori informazioni su XSS e le relative contromisure.
