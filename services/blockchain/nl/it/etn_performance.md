---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Prestazioni verificate
{: #etn_performance}


Le seguenti modalità di funzionamento sono state testate e verificate da IBM. I risultati sono stati ottenuti su una rete di sicurezza elevata, se non diversamente indicato:
{:shortdesc}

### Prestazioni/stress

Questo test è stato eseguito per ottenere il valore TPS (transactions per-second, transazioni al secondo) di richiami e query in intervalli di test di breve durata - 10 minuti, e intervalli di test di lunga durata - 60 minuti, con PBFT / Sicurezza e privacy abilitata.  Le prestazioni possono variare in base ad ambiente, tipo di applicazione, impostazioni di configurazione/sicurezza, dimensione del batch di transazioni e altri fattori.  (**Nota:** queste metriche sono state ottenute su una rete distribuita a più tenant).

- esempio chaincode02
- livello di registrazione: errore
- numero di thread: 100
- dimensione batch: 1000
- durata: 10 min. e 60 min.
- tipi di transazione: richiamare a->b, richiamare b->a, ripetere quindi & query a, query b e quindi ripetere

| Tipo di transazione | Numero di peer | Numero di thread | Durata esecuzione (min) | Transazioni al secondo |
| ---------- |:-------:|:-----:|:------:|:------:|
| richiami   |  4  | 100 | 10 | 72  |
| richiami   |  4  | 100 | 60 | 66  |
| query   |  4  | 100 | 10 | 252 |
| query   |  4  | 100 | 60 | 248 |

### Resilienza/consenso

Questo test è stato eseguito per garantire la stabilità e la resilienza di PBFT quando si verificano degli errori Byzantine.  I test includevano:

- L'arresto di 1 nodo senza smettere di inviare transazioni di distribuzione, richiamo e query.  La rete continua a funzionare. Eseguito su ciascun nodo nella rete.
- Arresto di 2 nodi; la rete si arresta per una mancanza di consenso.
- Riavvio di uno dei nodi arrestati nel test precedente.  La rete riprende e il nodo che è stato riavviato esegue la sincronizzazione con gli altri peer di convalida. Per una procedura dettagliata dell'esecuzione di test PBFT, consulta l'argomento [Esecuzione di test di consenso e disponibilità](etn_pbft.html).

Continua all'argomento [Esecuzione di test aggiuntivi](etn_next.html) per dei test aggiuntivi e per la funzionalità verificata.  
