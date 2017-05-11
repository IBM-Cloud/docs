---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Risoluzione dei problemi di {{site.data.keyword.GlobalizationPipeline_short}}
{: #globalizationpipelinets}


Qui trovi alcune risposte a domande comuni sull'utilizzo di {{site.data.keyword.GlobalizationPipeline_short}}. 
{:shortdesc}


## Il nome della mia applicazione non è stato tradotto correttamente
{: #problem1}

Le traduzioni generate per alcune stringhe non sono cosa mi aspettavo.
{:shortdesc}

Quando un file di risorsa viene tradotto, le stringhe che contengono i nomi dei prodotti o altri nomi propri potrebbero non venire tradotte correttamente.
{: tsSymptoms}

Molte volte, i nomi dei prodotti e i nomi propri non vengono tradotti correttamente in altre lingue, specialmente se il nome contiene parole reali. Quando vengono tradotti questi tipi di parole o frasi, a seconda del significato di tali parole in una lingua specifica, il testo tradotto può avere un significato differente rispetto al nome inglese.
{: tsCauses}

Verifica la traduzione dei nomi dei prodotti prima di utilizzarli e se riscontri dei problemi, modifica il testo o la traduzione di conseguenza. Per i suggerimenti sugli stili di scrittura quando utilizzi la machine translation, consulta [Suggerimenti sulla machine translation](./tips.html#globalizationpipeline_tips).
{: tsResolve}



## Non sono riuscito a caricare un file di risorsa
{: #problem2}

Il file di risorsa che sto provando a caricare non viene accettato.
{:shortdesc}

Quando aggiungo un file di risorsa a un nuovo bundle della traduzione o aggiorno un file di risorsa esistente da tradurre, ricevo un errore.
{: tsSymptoms}

{{site.data.keyword.GlobalizationPipeline_short}} accetta solo file di risorsa del seguente tipo: Java™ .properties, JSON e AMD I18N.
{: tsCauses}

Assicurati che il file di risorsa che stai caricando sia di uno dei seguenti tipi.
{: tsResolve}
* Java .properties
* JSON
* AMD I18N



## Non posso caricare il mio file di risorsa perché è troppo grande
{: #problem3}

Il file di risorsa che sto provando a caricare non viene accettato.
{:shortdesc}

Quando aggiungi o aggiorni un file di risorsa a un progetto di traduzione, si verifica un errore perché una porzione del file è troppo grande.
{: tsSymptoms}

{{site.data.keyword.GlobalizationPipeline_short}} può solo accettare file di risorsa che rispettino alcuni requisiti di dimensione.
{: tsCauses}

Assicurati che il file di risorsa sia conforme alle seguenti linee guida:
{: tsResolve}
* Ogni chiave può essere di 256 caratteri massimo.
* Ogni valore può essere di 2048 caratteri massimo.
* Ogni progetto di traduzione può contenere al massimo 500 coppie chiave / valore.
* Un file di risorsa non può essere più grande di 2 MB.




## La spaziatura delle variabili contenute nelle stringhe non è coerente
{: #problem5}

La spaziatura utilizzata per le variabili dopo la traduzione non è sempre la stessa.
{:shortdesc}

La spaziatura utilizzata per le variabili contenute nelle stringhe non è sempre coerente da lingua a lingua dopo la traduzione.
{: tsSymptoms}

I motori della machine translation sono progettati per funzionare con la lingua naturale e non sempre possono riconoscere o sapere come gestire una sintassi specifica utilizzata dai linguaggi di programmazione. Come risultato, la gestione della sintassi mista con testo piano può variare.
{: tsCauses}

{{site.data.keyword.GlobalizationPipeline_short}} al momento riconosce il pattern "{}" utilizzato comunemente per rappresentare le variabili e conserverà il formato originale del contenuto al suo interno.
{: tsResolve}
