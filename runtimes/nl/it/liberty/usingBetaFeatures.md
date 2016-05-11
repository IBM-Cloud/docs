---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilizzo delle funzioni beta
{: #using_beta_features}

*Ultimo aggiornamento: 23 marzo 2016*

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
<td>cloudant-1.0</td>
<td>httpWhiteboard-1.0</td>
<td>osgiBundle-1.0</td>
<td>passwordUtilities-1.0</td>
</tr>
</table>

Per utilizzare le funzioni beta Liberty in Bluemix, dovrai:

1. [Distribuire una directory server o un server in pacchetto](optionsForPushing.html) con una o più funzioni beta abilitate nel file server.xml come nel seguente esempio:
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>passwordUtilities-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  Imposta la variabile di ambiente IBM_LIBERTY_BETA su **true**. Questa variabile indica al pacchetto di build Liberty
di installare e abilitare le funzioni beta per la tua applicazione.  Consulta i seguenti esempi:
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
{: #codeblock}

# rellinks
## general
* [Runtime Liberty](index.html)
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
