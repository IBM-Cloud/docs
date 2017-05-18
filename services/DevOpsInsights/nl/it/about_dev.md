---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Informazioni su Developer Insights
{: #gettingstarted}

{{site.data.keyword.DRA_full}} Developer Insights fornisce un modo completo di esplorare il rischio di sviluppo del tuo progetto. Puoi identificare i file con alta tendenza all'errore e ottenere una vista di conformità del progetto per le procedure DevOps.
{:shortdesc}

Dopo aver aperto {{site.data.keyword.DRA_short}} dalla tua toolchain, fai clic su **Developer Insights**. Da lì, puoi selezionare una categoria analitica per un approfondimento sulla base di codice del tuo progetto. Cosa ogni serie di dati indica può variare da team a team e puoi eseguire il drill down in ogni visualizzazione per supporto e assistenza. 

## Categorie di dati
I dati che {{site.data.keyword.DRA_short}} utilizza per popolare il suo dashboard sono estratti automaticamente dal repository di controllo dell'origine del tuo team. Puoi ottenere ulteriori informazioni sul significato dei dati e su come puoi applicarli al tuo progetto facendo clic su **Information** o **Guidance** in qualsiasi grafico.

### Procedure consigliate sviluppatore 

Developer Insights fornisce vari grafici che misurano il tuo progetto per buone procedure da sviluppatore e DevOps. Utilizza questa categoria per ottenere una vista di alto livello della maturità, integrità e efficienza del tuo progetto. 

### Inclinazione all'errore

L'*inclinazione all'errore* è la probabilità che un file o un commit possa generare errori secondo le tendenze storiche, l'esperienza di committer, la frequenza di modifica, il peso della modifica e altri fattori. 

Puoi controllare questa categoria mentre esegui le revisioni del codice o migliori il processo di revisione del codice. I file a rischio meritano un esame più minuzioso rispetto a quelli sicuri. Al contrario, i file e i commit sicuri possono servire come esempi per il tuo team di come migliori come lavori.

### Problemi 

La categoria Problemi visualizza tutti i problemi di traccia del lavoro del tuo team in un solo posto. I problemi vengono automaticamente raggruppati per tipo, priorità e tag e possono essere visualizzati nel tempo. 

Questi raggruppamenti di problemi possono essere diversi nel significato da team a team. Un team potrebbe voler sapere se molti elementi contrassegnati con tag per una release in particolare sono chiusi, mentre un altro team potrebbe non contrassegnare con tag le release e invece lavorare in base alla priorità di apertura del problema.  

### Commit

I commit indicano il contributo dei tuoi membri del team alla tua base di codice. Esamina i tuoi dati di commit per comprendere dove stanno venendo profusi gli sforzi storicamente e come puoi migliorare il bilanciamento dei carichi di lavoro dei tuoi membri del team. 

### File 

La categoria File visualizza quali file del tuo progetto sono i più impegnati. Tramite le modifiche riga, i commit, gli autori o i problemi, questi dati indicano dove il tuo team è più attivo. 

In generale, tenta di ridurre sia il numero di mani che toccano un file che la frequenza di modifica di tale file. Questo obiettivo potrebbe essere impossibile con alcuni file, come i file di configurazione comuni. Tuttavia, molti sviluppatori che effettuano molte modifiche allo stesso file contemporaneamente è un ricettacolo di problemi. 

## Filtro dell'estensione file

DevOps Insights ignora i file con queste estensioni:

* .bin
* .cdr
* .jpeg
* .jpg
* .json
* .markdown
* .md
* .png
* .pyc
* .svg
* .text
* .yaml
* .yml

