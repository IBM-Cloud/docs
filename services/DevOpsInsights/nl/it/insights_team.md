---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Team Dynamics (sperimentale)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} Team Dynamics utilizza le analisi di codice social per identificare il livello di interazione tra i membri in modo che il team possa correggere le procedure non produttive. 
{:shortdesc}

Dopo aver aperto {{site.data.keyword.DRA_short}} dalla tua toolchain, fai clic su **Team Dynamics**. Da lì, puoi selezionare una categoria analitica per un approfondimento sulle tue pratiche e abitudini di collaborazione con il team. Cosa ogni serie di dati indica può variare da team a team e puoi eseguire il drill down in ogni visualizzazione per supporto e assistenza.  

## Categorie di dati

I dati che {{site.data.keyword.DRA_short}} utilizza per popolare il suo dashboard sono estratti automaticamente dal repository di controllo dell'origine del tuo team. Puoi ottenere ulteriori informazioni sul significato dei dati e su come puoi applicarli al tuo progetto facendo clic su **Information** o **Guidance** in qualsiasi grafico.

### Codifica social

Il grafico Codifica social mostra le connessioni tra i tuoi collaboratori del progetto in un modo visivo, altamente interattivo. Ogni nodo nel grafico rappresenta uno sviluppatore. La dimensione di un nodo viene ridimensionata in modo logaritmico in base ai contributi di uno sviluppatore di un progetto. Le righe tra i nodi indicano la collaborazione; più spessa è la riga, più due sviluppatori hanno collaborato nel periodo selezionato. 

Ogni nodo è colorato di blu e rosso di varie gradazioni. Il blu indica quante righe di codice sono state aggiunta da un collaboratore come parte del numero totale di righe che ha toccato. Il rosso indica quante righe di codice un collaboratore ha rimosso. Un collaboratore che ha soltanto aggiunto codice sarà completamente blu, mentre un collaboratore che ha aggiunto e rimosso un numero uguale di righe sarà mezzo blu e mezzo rosso. 

### Autori

La categoria Autori fornisce il numero di commit, modifiche riga e modifiche file per collaboratore del repository. Mentre qualcosa come il numero totale di righe codificate non può essere utilizzato per determinare un contributo di rete del membro del team ad un progetto, tali informazioni possono essere fornite ai gestori e leader del team. Un membro del team che contribuisce in molte modifiche di riga potrebbe essere sovraccarico, rappresenta un collo di bottiglia nei tuoi processi o codifica in un modo più dettagliato in confronto agli altri membri del team. 
