---

copyright:
  years: 2015, 2016
lastupdated: "2016-06-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Valori predefiniti dei pacchetti di build
{: #buildpack_defauts}

Il pacchetto di build Liberty viene aggiornato frequentemente in Bluemix. Ogni release può contenere delle correzioni per la protezione o dei miglioramenti delle funzioni.

Il pacchetto di build ha dei valori predefiniti per impostazioni quali
la versione Java o l'insieme di funzioni Liberty per applicazioni WAR o
EAR. Tra le diverse release del pacchetto di build, alcuni dei valori predefiniti
potrebbero subire delle variazioni che potrebbero avere un impatto
negativo sull'applicazione. Per evitare che l'applicazione risenta delle
variazioni dei valori predefiniti del pacchetto di build, attieniti
alla seguente procedura per configurare la tua applicazione in modo che
non si basi sui valori predefiniti del pacchetto di build.

## Versioni Liberty
{: #liberty_versions}

Il pacchetto di build fornisce due versioni del runtime Liberty:
1. La release stabile
  * È il runtime Liberty predefinito.
  * Non fornisce alcuna [funzione beta](usingBetaFeatures.html).
  * Normalmente aggiornato su base trimestrale.

2. La release mensile
  * Deve essere abilitata esplicitamente impostando la variabile di ambiente **JBP_CONFIG_LIBERTY** con il valore **"version: +"**.
  * Fornisce le [funzioni beta](usingBetaFeatures.html).
  * Normalmente aggiornata su base mensile.

## Funzioni Liberty
{: #liberty_features}

Quando
distribuisci file WAR O EAR, il pacchetto di build fornisce una
configurazione per l'applicazione con un insieme predefinito di
funzioni Liberty. Seppur raramente, l'insieme predefinito di funzioni Liberty
potrebbe cambiare, tra le release del pacchetto di build. La variazione nell'insieme di
funzioni predefinito potrebbe avere un impatto negativo sull'applicazione. Sono disponibili
delle opzioni per garantire che l'applicazione non risenta della modifica nei
valori predefiniti delle funzioni.

* Imposta la variabile di ambiente JBP_CONFIG_LIBERTY per specificare esplicitamente
un elenco di funzioni abilitate per l'applicazione. Per ulteriori informazioni, consulta [Applicazioni autonome](optionsForPushing.html#stand_alone_apps).
* Distribuisci la tua applicazione come una [directory server](optionsForPushing.html#server_directory)
o un [server in pacchetto](optionsForPushing.html#packaged_server). Fornisci un file server.xml personalizzato che specifica l'esatto insieme di funzioni di cui la tua applicazione ha bisogno.

Le applicazioni distribuite come una directory server
o come un server in pacchetto non risentono della modifica nel valore predefinito delle funzioni Liberty.

## Versione Java
{: #java_version}

Il pacchetto di build fornisce
un JRE predefinito per l'applicazione. La versione principale o quella secondaria
del JRE potrebbero variare, tra le release del pacchetto di build. La versione
secondaria del JRE potrebbe essere aggiornata frequentemente, mentre
la versione principale viene aggiornata di rado. La modifica nella versione principale
del JRE potrebbe avere un impatto negativo sull'applicazione.

Per garantire che l'applicazione non sia influenzata dalla modifica della versione principale, imposta la variabile di ambiente con la versione JRE appropriata come descritto in [Customizing the JRE](customizingJRE.html). Per dei risultati
ottimali, adotta Java 8 per le tue applicazioni.


# rellinks
{: #rellinks}
## general
{: #general}
* [Runtime Liberty](index.html)
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
