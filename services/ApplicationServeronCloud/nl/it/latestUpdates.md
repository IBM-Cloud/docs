---

copyright:
  years: 2015, 2016
lastupdated: "2017-04-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Ultimi aggiornamenti
{: #latest_updates}

Un elenco degli aggiornamenti più recenti al servizio.

## 15 marzo 2017: aggiornamento di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* Manutenzione dei servizi vari integrata.
* I file binari di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} sono stati aggiornati in modo che il fixpack 8.5.5.11 o 9.0.0.3 venga installato con le nuove istanze di Traditional WebSphere Application Server.
* Sono state risolte [diverse vulnerabilità di sicurezza](https://www-01.ibm.com/support/docview.wss?uid=swg22000587){: new_window} in WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}, tra cui:
  * Una vulnerabilità non specificata correlata al componente Librerie che ha un alto impatto sull'integrità e nessun impatto sulla riservatezza e sulla disponibilità.
  * Una vulnerabilità non specificata correlata al componente Librerie che potrebbe consentire a un aggressore remoto di ottenere informazioni sensibili comportando un alto impatto sulla riservatezza tramite vettori di attacco sconosciuti.
  * Una vulnerabilità non specificata correlata al componente Librerie che potrebbe consentire a un aggressore remoto di causare un attacco DoS (Denial of Service), comportando un basso impatto sulla disponibilità tramite vettori di attacco sconosciuti.
  * Una vulnerabilità in OpenSSL che potrebbe consentire a un aggressore remoto di ottenere informazioni sensibili, causata da un errore nella crittografia DES/3DES, utilizzata come parte del protocollo SSL/TLS.
  * Una vulnerabilità che consente agli utenti di incorporare codice JavaScript arbitrario nell'interfaccia utente Web alterando così la funzionalità desiderata che potrebbe portare a divulgare le credenziali in una sessione attendibile. 
  * Una vulnerabilità in Apache HTTPD per gli attacchi di suddivisione della risposta HTTP, causata da una convalida impropria dell'input fornito dall'utente.
  * Una vulnerabilità in Samba che potrebbe consentire a un aggressore autenticato remoto di ottenere privilegi elevati sul sistema, causata dall'errore di gestione del checksum PAC.
  * Una vulnerabilità in Samba che potrebbe consentire a un aggressore autenticato remoto di ottenere privilegi elevati sul sistema, causata dall'inoltro di un TGT (Ticket Granting Ticket) a un altro servizio durante l'utilizzo dell'autenticazione Kerberos.
  * Una vulnerabilità in Samba in un overflow di buffer basato su heap, causata da un problema di integer wrap nella funzione ndr_pull_dnsp_name().


## 10 febbraio 2017: aggiornamento di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* Manutenzione dei servizi vari integrata.
* I file binari di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} sono stati aggiornati in modo che il fixpack 8.5.5.11 o 9.0.0.2 venga installato con le nuove istanze di Traditional WebSphere Application Server.
* I file binari di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} sono stati aggiornati in modo che il fixpack 16.0.0.4 venga installato con le nuove istanze di WebSphere Application Server Liberty (piani Core e ND).
* Sono state risolte [diverse vulnerabilità di sicurezza](https://www-01.ibm.com/support/docview.wss?uid=swg21997657){: new_window} in WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}, tra cui:
  * Una vulnerabilità a DoS (Denial of Service), causata dall'esecuzione di oggetti serializzati provenienti fonti non attendibili provocando così il consumo di risorse.
  * L'utilizzo di richieste SOAP con formato errato, che potrebbe consentire a un aggressore remoto di ottenere informazioni sensibili.


## 16 dicembre 2016: aggiornamento di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* Manutenzione dei servizi vari integrata.
* Sono state risolte [diverse vulnerabilità di sicurezza](https://www-01.ibm.com/support/docview.wss?uid=swg21995995){: new_window} in IBM SDK Java Technology Edition che influivano su WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}, tra cui:
  * Una vulnerabilità non specificata in Oracle Java SE e Java SE Embedded correlata al componente Hotspot che ha un alto impatto sulla riservatezza, un alto impatto sull'integrità e un alto impatto sulla disponibilità.
  * Una vulnerabilità non specificata in Oracle Java SE e Java SE Embedded correlata al componente Rete che potrebbe consentire a un aggressore remoto di ottenere informazioni sensibili comportando un alto impatto sulla riservatezza tramite vettori di attacco sconosciuti. 
  *  Una vulnerabilità cross-site scripting in IBM WebSphere Application Server che consente agli utenti di incorporare codice JavaScript arbitrario nell'interfaccia utente Web alterando così la funzionalità desiderata che potrebbe portare a divulgare le credenziali in una sessione attendibile. 


## 8 novembre 2016: aggiornamento di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* Aggiunta la capacità per i clienti di richiedere un indirizzo [IP pubblico](networkEnvironment.html#networkEnvironment) per le loro VM di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}
* Sono state risolte [diverse vulnerabilità di sicurezza](http://www-01.ibm.com/support/docview.wss?uid=swg21993842){: new_window} che influivano su WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}, tra cui:
  * Una vulnerabilità in IBM WebSphere Application Server che può consentire ad aggressori in remoto di eseguire il codice Java arbitrario con un oggetto serializzato da origini non attendibili.
  * Una vulnerabilità DoS (Denial of Service) causata da una lettura non compresa nell'intervallo nella funzione TS_OBJ_print_bio. Un aggressore in remoto può avvalersi di questa vulnerabilità utilizzando un file di data/ora creato appositamente per causare l'arresto anomalo dell'applicazione.
  * Una vulnerabilità potenziale in OpenSSL che può consentire a un aggressore in remoto di ottenere informazioni sensibili, causata da un errore nel Triple-DES nella crittografia a blocchi a 64-bit, utilizzato come parte del protocollo SSL/TLS. Acquisendo una grande quantità di traffico crittografato tra il server e il client SSL/TLS, un aggressore in remoto in grado di effettuare un attacco MiTM (Man-in-the-Middle) può sfruttare questa vulnerabilità per recuperare i dati di testo non crittografato e ottenere informazioni sensibili. Questa vulnerabilità è conosciuta come attacco SWEET32 Birthday.
  * OpenSSL è vulnerabile a DoS (Denial of Service). Richiedendo ripetutamente la rinegoziazione, un aggressore autenticato in remoto potrebbe inviare un'estensione della richiesta dello stato OCSP eccessivamente grande per consumare tutte le risorse di memoria disponibili.
  * OpenSSL è vulnerabile a DoS (Denial of Service), causato da un overflow di numeri interi nella funzione MDC2_Update. Utilizzando dei vettori di attacco sconosciuti, un aggressore in remoto può avvalersi di questa vulnerabilità per attivare una scrittura non compresa nell'intervallo e causare l'arresto anomalo dell'applicazione.
  * Una vulnerabilità potenziale in OpenSSL che consente a un aggressore in remoto di ottenere informazioni sensibili, causata da un errore nell'implementazione DSA che consente l'aggiunta di un percorso di codice dell'ora non costante per alcune operazioni. Un aggressore in remoto può avvalersi di questa vulnerabilità utilizzando una attacco di timing nella cache per recuperare la chiave DSA privata.
  * OpenSSL è vulnerabile a DoS (Denial of Service), causato dalla mancanza dei controlli di lunghezza del messaggio durante l'analisi dei certificati. Un aggressore autenticato in remoto può avvalersi di questa vulnerabilità per attivare una lettura compresa nell'intervallo e causare un attacco Denial of Service.

## 19 settembre 2016: aggiornamento di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* I file binari di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} sono stati aggiornati in modo che le nuove istanze di WebSphere Application Server Liberty (piani Core e ND) abbiano il fixpack 16.0.0.3 installato.
* Sono state risolte [diverse vulnerabilità di sicurezza](http://www-01.ibm.com/support/docview.wss?uid=swg21990236){: new_window} che influivano su WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}, tra cui:
  * Una vulnerabilità in IBM WebSphere Application Server Liberty che può consentire ad aggressori in remoto di effettuare attacchi di pishing.
  * Una vulnerabilità in IBM WebSphere Application Server Liberty di XSS (Cross-Site Scripting) nei client OpenID Connect.
  * Una vulnerabilità potenziale in IBM WebSphere Application Server Liberty che può consentire ad aggressori in remoto di ottenere informazioni sensibili causata dalla gestione non corretta delle eccezioni quando una pagina dell'errore predefinita non esiste.
  * Un vulnerabilità in Apache Tomcat per un DoS (Denial of Service), causata da un errore nel componente Apache Commons FileUpload.
  * Una vulnerabilità in IBM WebSphere Application Server e IBM WebSphere Application Server Liberty che può consentire ad aggressori in remoto di ottenere informazioni sensibili, causata dalla gestione non corretta delle risposte in alcune condizioni.
  * Una vulnerabilità non specificata correlata al componente di rete che non ha un impatto di confidenzialità, di bassa integrazione e nessuna disponibilità.

## 17 settembre 2016: aggiornamento di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* I file binari di WebSphere Application Server in Bluemix sono stati aggiornati dalla 8.5.5.9 alla 8.5.5.10
* Sono state risolte [diverse vulnerabilità di sicurezza](http://www-01.ibm.com/support/docview.wss?uid=swg21988710){: new_window} che influivano su WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}, tra cui:
  * Le vulnerabilità Apache Struts che riguardano WebSphere Application Server e la console di gestione WebSphere Application Server Hypervisor Edition.
  * Una vulnerabilità DoS (Denial of Service) potenziale con IBM WebSphere Application Server quando si utilizzano i servizi SIP.
  * Le vulnerabilità server che potevano riguardare il IBM HTTP Server utilizzato da WebSphere Application Server.
  * Una vulnerabilità che consente il reindirizzamento del traffico HTTP con le applicazioni CGI che può influenzare il IBM HTTP Server (IHS). Questa vulnerabilità è conosciuta come "HTTPOXY".
  * Una vulnerabilità di divulgazione delle informazioni in IBM WebSphere Application Server.
  * Una vulnerabilità di sicurezza di bypass potenziale in IBM WebSphere Application Server che si verifica solo negli ambienti con la proprietà personalizzata di contenitore HttpSessionIdReuse abilitata.


## 24 giugno 2016: aggiornamento di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* Aggiunta la possibilità per i clienti di scegliere tra la V8.5 e la V9.0 quando creano una nuova istanza *Traditional ND* o *Traditional WebSphere*.
* I file binari di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} sono stati aggiornati in modo che le nuove istanze di WebSphere Application Server Liberty (piani Core e ND) abbiano il fixpack 16.0.0.2 installato. 16.0.0.2 è il fixpack successivo a 8.5.5.9. Come parte di 16.0.0.2, tutte le funzioni facoltative intitolate Liberty supportate per questi piani sono installate per impostazioni predefinita.
* Sono state risolte [diverse vulnerabilità di sicurezza](http://www-01.ibm.com/support/docview.wss?uid=swg21984977){: new_window} che influivano su WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}, tra cui:
  * Una vulnerabilità XML External Entity Injection (XXE) in Apache Standard Taglibs che riguardava IBM WebSphere Application Server.
  * Una sicurezza potenziale più debole del previsto durante l'utilizzo della funzione WebSphere Application Server Liberty profile API Discovery e della documentazione Swagger.
  * Una vulnerabilità di divulgazione delle informazioni potenziale nel Admin Center per IBM WebSphere Application Server Liberty.
  * Una vulnerabilità di suddivisione della risposta HTTP in IBM WebSphere Application Server.
  * Le vulnerabilità OpenSSL divulgate il 3 maggio 2016 dal progetto OpenSSL.

## 13 giugno 2016: aggiornamento di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* Aggiunta la possibilità per i clienti di creare, fornire, gestire ed eliminare istanze della macchina virtuale attraverso la creazione di un'applicazione o script che utilizza le API RESTful WebSphere Application Server in Bluemix.
* Aggiunta la funzione che consente a un cliente di avere un numero fisso di istanze ARRESTATE con non più di 10 indirizzi IP o 64 GB di memoria. Ai clienti vengono ora addebitate le istanze accumulate nello stato ARRESTATO a un tasso ridotto del 5%.

## 26 aprile 2016: aggiornamento di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* Sono state risolte [potenziali vulnerabilità di sicurezza](http://www-01.ibm.com/support/docview.wss?uid=swg21982128){: new_window} in WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} con FIPS 140-2 abilitato e altre vulnerabilità in Samba - incluso Badlock.
* Manutenzione dei servizi vari integrata.

## 15 aprile 2016: aggiornamento di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* I file binari di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} sono stati aggiornati dalla 8.5.5.8 alla 8.5.5.9
* È stata risolta una vulnerabilità [Cross-site scripting](http://www-01.ibm.com/support/docview.wss?uid=swg21981221){: new_window} in Liberty for Java per IBM {{site.data.keyword.Bluemix_notm}} che influiva sull'utilizzo del client OpenID Connect (OIDC) da parte dei clienti.
* Manutenzione dei servizi vari integrata.

## 19 febbraio 2016: aggiornamento di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}
* Aggiunta un'opzione per i clienti con applicazioni intensive di memoria per "dimensionare correttamente" il loro ambiente con grandi macchine virtuali. I clienti possono selezionare la dimensione della risorsa specifica di un determinato componente di WebSphere Application Server o un singolo sistema fino a 32 GB RAM di macchine virtuali.
* I file binari di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} sono stati aggiornati dalla 8.5.5.7 alla 8.5.5.8
* Sono state risolte diverse vulnerabilità in IBM SDK Java Technology Edition che influivano su WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} a cui si fa comunemente riferimento come [SLOTH](http://www-01.ibm.com/support/docview.wss?uid=swg21977244){: new_window}.
* È stata risolta una vulnerabilità [Cross-site scripting](http://www-01.ibm.com/support/docview.wss?uid=swg21976337){: new_window} che influenzava l'output del provider OAuth dei clienti.
* Manutenzione dei servizi vari integrata.

## 11 dicembre 2015: aggiornamento di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}
* È stato modificato il nome del prodotto ufficiale da IBM Application Server on Cloud in {{site.data.keyword.Bluemix_notm}} a IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}
* Sono state aggiunte delle nuove funzionalità al piano di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Network Deployment. Il piano consiste in un ambiente di cella WebSphere Application Server Network Deployment con due o più macchine virtuali. Queste nuove funzionalità consentono agli utenti di impostare un ambiente in cluster per l'elevata disponibilità, il failover e la scalabilità.
* Sono state aggiunte delle nuove funzionalità al piano di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Liberty Core. Il piano include l'utilizzo di un collettivo Liberty, che è un dominio amministrativo per un gruppo di profili Liberty (server) e consiste in due o più macchine virtuali
* I file binari di WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} sono stati aggiornati dalla 8.5.5.6 alla 8.5.5.7
* È stata risolta una [vulnerabilità di Apache Commons Collections](https://www.us-cert.gov/ncas/current-activity/2015/11/13/Apache-Commons-Collections-Java-Library-Vulnerability){: new_window} per
gestire la deserializzazione di oggetti Java.
* È stata risolta una vulnerabilità che potrebbe consentire un [attacco HTTP
Response Splitting](http://www-01.ibm.com/support/docview.wss?uid=swg21972254){: new_window}.
* Manutenzione dei servizi vari integrata.

## 15 ottobre 2015: Application Server on Cloud aggiornato
* Sono stati aggiunti i seguenti due nuovi piani:
  * [WebSphere Application Server Traditional V9 Beta](https://www-01.ibm.com/marketing/iwm/iwmdocs/web/cc/earlyprograms/websphere.shtml){: new_window}
  * WebSphere Application Server ND
* Manutenzione di servizio varia
