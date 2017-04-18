---

copyright:
  years: 2015, 2016
lastupdated: "2016-06-10"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilizzo delle funzioni beta
{: #using_beta_features}

Le funzioni beta Liberty forniscono un accesso anticipato ai nuovi modelli di funzionalità e
programmazione che potrebbero essere inclusi in una futura release di Liberty. La maggior parte delle funzioni beta può essere utilizzata anche nelle applicazioni distribuite a Bluemix.

**Importante**: le funzioni beta sono solo per scopi di sviluppo e test e non possono essere utilizzate in produzione. Per le condizioni di utilizzo complete, consulta l'[ accordo di licenza beta](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

Funzioni beta Liberty disponibili in Bluemix
<table>
<tr>
<th align="left">Funzione</th>
<th align="left">Funzione</th>
<th align="left">Funzione</th>
<th align="left">Funzione</th>
</tr>

<tr>
<td>bluemixLogCollector-1.1</td>
<td>httpWhiteboard-1.0</td>
<td>logstashCollector-1.1</td>
<td>osgiBundle-1.0</td>
</tr>
</table>

Per utilizzare le funzioni beta Liberty in Bluemix devi fare quanto segue:

1. [Distribuire una directory server o un server in pacchetto](optionsForPushing.html) con una o più funzioni beta abilitate nel file server.xml come nel seguente esempio:
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>bluemixLogCollector-1.1</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  Imposta la variabile di ambiente **IBM_LIBERTY_BETA** su **true**. Questa variabile indica al pacchetto di build Liberty
di installare e abilitare le funzioni beta per la tua applicazione.  Ad esempio:
  * utilizzando lo strumento di riga di comando cf:
```
       $ cf set-env <nomedellatuaapplicazione> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * oppure utilizzando il file manifest.yml:
```
      env:
          IBM_LIBERTY_BETA: "true"
```

3. Imposta la variabile di ambiente **JBP_CONFIG_LIBERTY** su **"version: +"**. Questa variabile abilita il [Runtime mensile Liberty](buildpackDefaults.html#liberty_versions) il quale supporta le funzioni beta. Ad esempio:
  * utilizzando lo strumento di riga di comando cf:
```
       $ cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
```
{: #codeblock}

  * oppure utilizzando il file manifest.yml:
```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
```

Se stai abilitando le funzioni beta su un'applicazione esistente, non dimenticare di ripreparare la tua applicazione dopo la configurazione delle variabili di ambiente.

{: #codeblock}

# rellinks
{: #rellinks}
## general
{: #general}
* [Runtime Liberty](index.html)
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
