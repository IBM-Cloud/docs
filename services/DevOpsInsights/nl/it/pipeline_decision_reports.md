---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visualizzazione di dashboard e report
{: #DRA_toolchain_reports}

{{site.data.keyword.DRA_short}} ti fornisce un gran numero di di informazioni operative sui tuoi progetti.
{:shortdesc}

## Dashboard {{site.data.keyword.DRA_short}}    
{: #DI_toolchain_dashboards}

{{site.data.keyword.DRA_short}} fornisce i dashboard che visualizzano le informazioni sulle prestazioni nell'organizzazione Bluemix. Per visualizzarli, dopo aver aperto {{site.data.keyword.DRA_short}}, fai clic su **Build Verification** o **Deploy Verification**.

I dashboard vengono popolati automaticamente con le informazioni più recenti dai lavori di test {{site.data.keyword.DRA_short}} delle tue pipeline. Fai clic sugli elementi nei dashboard per ulteriori informazioni su di essi.

### Indicatori delle prestazioni chiave nelle build    
{: #DI_key_performance_indicators}

La pagina **Build Verification** contiene tre grafici che contengono le informazioni sull'integrità del ramo di sviluppo selezionato:

<table>
<thead>
<tr>
<th>Grafico</th>
<th>Descrizione</th>
</tr>
</thead>

<tbody>
<tr>
<td>Ultime build</td>
<td>Il numero di build recenti completate confrontato al numero totale di build recenti.</td>
</tr>
<tr>
<td>Test</td>
<td>Il numero di test superati confrontato al numero totale di test.</td>
</tr>
<tr>
<td>Copertura del codice</td>
<td>Le percentuali delle tue funzioni o istruzioni del codice richiamate dai tuoi test.</td>
</tr>
</tbody></table>

## Visualizzazione dei report di decisione    
{: #DI_decision_reports}

Dopo aver eseguito una pipeline, {{site.data.keyword.DRA_short}} inizia a raccogliere e analizzare i risultati del test da essa per stabilire una linea di base. I dati di ogni successiva esecuzione sono raccolti e confrontati con i risultati precedenti. I gate di decisione utilizzano questi dati per determinare quando arrestare una distribuzione. 

Per visualizzare il report di decisione per un gate dalla pipeline, completa questi passi:

   1. Nella fase che contiene il gate da verificare, fai clic su **Visualizza log e cronologia**.

   2. Dalla finestra dei lavori nella fase, fai clic sul nome del gate.

   3. Nella vista del log, individua il messaggio 'Verifica il report {{site.data.keyword.DRA_short}} qui` e fai clic sul link fornito per aprire il report.
