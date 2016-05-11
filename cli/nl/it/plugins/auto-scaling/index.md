---

 

copyright:

  years: 2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# CLI Auto-Scaling
{: #autoscalingcli}

*Ultimo aggiornamento: 25 febbraio 2016*

Puoi configurare il servizio {{site.data.keyword.autoscaling}} utilizzando la CLI {{site.data.keyword.autoscaling}} per {{site.data.keyword.Bluemix_notm}}. La CLI {{site.data.keyword.autoscaling}} supporta Linux64, Win64 e OSX e fornisce delle funzionalità simili a quelle fornite dall'API RESTful di ridimensionamento automatico.
{: shortdesc}

Prima di iniziare, installa la CLI {{site.data.keyword.Bluemix_notm}}. Consulta [Download {{site.data.keyword.Bluemix_notm}} CLI](http://plugins.{DomainName}/ui/home.html){: new_window} per istruzioni.

## Aggiunta del plug-in CLI {{site.data.keyword.Bluemix_notm}}

Una volta installata la CLI {{site.data.keyword.Bluemix_notm}}, puoi aggiungere il plug-in della CLI {{site.data.keyword.autoscaling}}.

Completa la seguente procedura per aggiungere il repository e installare il plug-in:
1. Per aggiungere il repository di plug-in della CLI {{site.data.keyword.Bluemix_notm}}, immetti il seguente comando:
```
bluemix plugin repo-add bluemix-plugin-repo https://plugins.ng.bluemix.net
```
2. Per installare il plug-in della CLI {{site.data.keyword.autoscaling}}, immetti il seguente comando:
```
bluemix plugin install auto-scaling -r bluemix-plugin-repo
```

## Collegamento di una politica di ridimensionamento automatico

Puoi collegare una politica di ridimensionamento automatico a una specifica applicazione. Immetti il seguente comando:

```bx as policy-attach <APP_NAME> -p <policy_file>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Il nome dell'applicazione a cui collegare una politica di ridimensionamento automatico.</dd>
<dt class="pt dlterm">&lt;policy_file&gt;</dt>
<dd class="pd">Il nome del file JSON che descrive la politica di ridimensionamento automatico. Vedi la <a href="https://new-console.{DomainName}/apidocs/48" target="_blank">documentazione dell'API RESTful {{site.data.keyword.autoscaling}}</a> per ulteriori dettagli.</dd>
</dl>


## Generazione di una politica di ridimensionamento automatico

Puoi generare una politica di ridimensionamento automatico rispondendo alle domande visualizzate nell'interfaccia riga di comando. A seconda del tuo input, un file JSON contenente la definizione della politica di ridimensionamento automatico viene salvato con il nome immesso. Se non immetti il nome del file, il contenuto della politica viene stampato direttamente nella riga di comando senza essere salvato in un file. Immetti il seguente comando:

```bx as policy-create```
{: codeblock}


## Visualizzazione di una politica di ridimensionamento automatico

Puoi visualizzare la politica di ridimensionamento automatico di un'applicazione. Il contenuto della politica viene stampato direttamente nella riga di comando. Immetti il seguente comando:

```bx as policy-show <APP_NAME> [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Il nome dell'applicazione per cui visualizzare la politica di ridimensionamento automatico. Per impostazione predefinita, la struttura JSON viene tradotta in una serie di output leggibili.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare l'opzione **--json** per stampare invece la riposta JSON originale.


## Scollegamento di una politica di ridimensionamento automatico

Puoi rimuovere una politica di ridimensionamento automatico da un'applicazione. Immetti il seguente comando:

```bx as policy-detach <APP_NAME>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Il nome dell'applicazione per la quale scollegare la politica di ridimensionamento automatico.</dd>
</dl>


## Abilitazione o disabilitazione di una politica di ridimensionamento automatico

Puoi abilitare o disabilitare la politica di ridimensionamento automatico di una specifica applicazione. Immetti il seguente comando:

```bx as policy-enable|policy-disable <APP_NAME>```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Il nome dell'applicazione per cui abilitare o disabilitare la politica di ridimensionamento automatico.</dd>
</dl>


## Visualizzazione della cronologia di ridimensionamento automatico di un'applicazione

Puoi visualizzare la cronologia dell'attività di ridimensionamento automatico di una specifica applicazione. Una tabella di record della cronologia del ridimensionamento automatico viene visualizzata nell'interfaccia riga di comando.

```bx as history-show <APP_NAME>  [--start-date=<start_timestamp>][--end-date=<end_timestamp>]  [--json]```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Il nome dell'applicazione per cui visualizzare la cronologia della politica di ridimensionamento automatico.
<dt class="pt dlterm">&lt;start_timestamp&gt;</dt>
<dd class="pd">La data e ora di inizio dell'intervallo della cronologia. I formati supportati sono `yyyy-MM-ddTHH:mm:ss+/-hhmm, yyyy-MM-ddTHH:mm:ssZ`. Per impostazione predefinita, la data e ora viene impostata su 50 ore avanti rispetto all'ora corrente. Consultare la <a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">W3C Date e Time Formats standard</a> per i dettagli relativi al formato data / ora. 
<dt class="pt dlterm">&lt;end_timestamp&gt;</dt>
<dd class="pd">La data e ora di fine dell'intervallo della cronologia. I formati supportati sono `yyyy-MM-ddTHH:mm:ss+/-hhmm, yyyy-MM-ddTHH:mm:ssZ`. Per impostazione predefinita, la data e ora viene impostata sull'ora corrente. Consultare la <a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">W3C Date e Time Formats standard</a> per i dettagli relativi al formato data e ora. 
</dl>

**Suggerimento:** puoi anche utilizzare l'opzione **--json** per stampare invece la riposta JSON originale.

# rellinks
## generale
* [{{site.data.keyword.autoscaling}}servizio](../../../services/Auto-Scaling/index.html)
* [{{site.data.keyword.Bluemix_notm}} CLI](http://plugins.{DomainName}/ui/home.html){: new_window}
* [W3C Date and Time Formats standard](https://www.w3.org/TR/NOTE-datetime){: new_window}


