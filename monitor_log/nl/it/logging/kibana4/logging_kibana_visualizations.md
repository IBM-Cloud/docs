---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analisi dei log in Kibana utilizzando le visualizzazioni 
{:#logging_kibana_visualizations}

Utilizza la pagina *Visualizza* in Kibana per creare visualizzazioni come grafici e tabelle che puoi utilizzare per analizzare i tuoi dati di log e confrontare i risultati. 
{:shortdesc}

Puoi utilizzare una visualizzazione individualmente per analizzare i tuoi log. 

* Puoi creare le visualizzazioni da una ricerca che definisci e salvi nella pagina *Rileva* o da una nuova query che definisci nella pagina *Visualizza*. La ricerca definisce la sottoserie di dati che visualizza la visualizzazione.

* Il tipo di visualizzazione che scegli determina come i dati sono visualizzati per l'analisi.

La seguente tabella elenca i diversi tipi di visualizzazione:

| Tipo di visualizzazione | Descrizione |
|-----------------------|-------------|
| Grafico ad aree | Visualizza i dati quantitativi graficamente. Utilizza per confrontare due o più serie di dati aggregati. |
| Tabella di dati | Visualizza i dati non elaborati in formato tabulare per un'aggregazione composta. |
| Grafico a linee | Visualizza i dati basati sul tempo. Utilizza per confrontare due o più serie di dati aggregati basati sul tempo. |
| Widget Markdown | Utilizza per visualizzare le informazioni di testo. |
| Metrica | Utilizza per visualizzare il numero di riscontri o la media esatta in un campo numerico. |
| Grafico a torta | Utilizza per visualizzare differenti valori di un campo. | 
| Grafico a barre verticali | Visualizza i dati basati sul tempo e non basati sul tempo. Utilizza per raggruppare i dati. |
{: caption="Tabella 1. Tipi di visualizzazione" caption-side="top"}

Nella pagina Visualizza, puoi eseguire tutte le seguenti attività:

| Attività | Informazioni aggiuntive |
|------|------------------|
| [Creare una nuova visualizzazione](logging_kibana_visualizations.html#logging_k4_visualizations_create) | Puoi creare le visualizzazioni da una ricerca che definisci e salvi nella pagina *Rileva* o da una nuova query che definisci nella pagina *Visualizza*. |
| [Salvare una visualizzazione](logging_kibana_visualizations.html#logging_kibana_visualizations_save) | Puoi salvare le visualizzazioni per un riutilizzo successivo. |
| [Caricare una visualizzazione](logging_kibana_visualizations.html#logging_kibana_visualizations_reload) | Puoi caricare una visualizzazione per aggiornarne i dati, modificarla o analizzare i dati. |
| [Elimina una visualizzazione](logging_kibana_visualizations.html#logging_kibana_visualizations_delete) | Elimina le visualizzazioni non richieste. |
| [Esporta una visualizzazione](logging_kibana_visualizations.html#logging_kibana_visualizations_export) | Puoi esportare una visualizzazione come un file JSON.  |
| [Importa una visualizzazione](logging_kibana_visualizations.html#logging_kibana_visualizations_import) | Puoi importare una visualizzazione come un file JSON.  |
| [Condividi una visualizzazione](logging_kibana_visualizations.html#logging_kibana_visualizations_share) | Puoi condividere una visualizzazione tramite la tua origine HTML o il dashboard Kibana.  |
{: caption="Tabella 2. Attività per lavorare con le visualizzazioni" caption-side="top"}


## Creazione di visualizzazioni da query in Kibana
{:#logging_k4_visualizations_create}

Completa la seguente procedura per creare una visualizzazione dalla pagina Visualizza:

1. Avvia Kibana e seleziona la pagina **Visualizza**.

2. Crea una nuova visualizzazione. Nella barra degli strumenti, fai clic sul pulsante **Nuova visualizzazione** ![Nuova visualizzazione](images/k4_visualization_new_icon.jpg "Nuova visualizzazione").

3. Seleziona una visualizzazione.
    
4. Seleziona un'origine di ricerca. Scegli una delle seguenti opzioni:

    * Fa clic su **Da una nuova ricerca**.
    * Fai clic su **Da una ricerca salvata**. 
  
5. Configura la query.

    * Se selezioni **Da una ricerca salvata**, seleziona una query di ricerca. La query viene utilizzata per richiamare i dati utilizzati per la visualizzazione. 

        Dopo aver selezionato una ricerca, viene aperto il builder della visualizzazione e vengono caricati i dati per la query selezionata. Viene visualizzato il seguente messaggio: *Questa visualizzazione è collegata a una ricerca salvata: tuo_nome_ricerca*. 
	
	**Nota**: tutte le modifiche che effettui a una ricerca salvata vengono automaticamente riportate nella visualizzazione. Per disabilitare gli aggiornamenti automatici che esegui alla query collegata a questa visualizzazione, fai doppio clic sul messaggio *Questa visualizzazione è collegata a una ricerca salvata: tuo_nome_ricerca* 

    * Se selezioni **Da una nuova ricerca**, definisci una nuova query. La query viene utilizzata per definire la sottorete di dati richiamati e utilizzati dalla visualizzazione.

        Per ulteriori informazioni, vedi [Filtro dei log definendo query personalizzate](k4_filter_queries.html#k4_filter_queries).

6. Nel builder della visualizzazione, seleziona un'aggregazione della metrica per l'asse Y.

7. Nel builder della visualizzazione, seleziona un tipo di bucket. Quindi, seleziona un aggregazione di bucket.
  
8. Aggiungi bucket secondari per suddividere i dati.

Per ulteriori informazioni su Kibana, consulta [Kibana User Guide ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

## Eliminazione di una visualizzazione
{:#logging_kibana_visualizations_delete}

Per eliminare una visualizzazione, completa la seguente procedura nella pagina Impostazioni:

1. Nella pagina Impostazioni, seleziona la scheda **Oggetti**.

2. Nella scheda **Visualizzazioni**, seleziona le visualizzazioni che desideri eliminare.

3. Fai clic su **Elimina**.


## Esportazione di una visualizzazione
{:#logging_kibana_visualizations_export}

Per esportare una visualizzazione come un file JSON, completa la seguente procedura nella pagina Impostazioni:

1. Nella pagina Impostazioni, seleziona la scheda **Oggetti**.

2. Nella scheda **Visualizzazioni**, seleziona la visualizzazione che desideri esportare.

3. Fai clic su **Esporta**.

4. Salva il file.

## Importazione di una visualizzazione
{:#logging_kibana_visualizations_import}

Per importare una visualizzazione come un file JSON, completa la seguente procedura nella pagina Impostazioni:

1. Nella pagina Impostazioni, seleziona la scheda **Oggetti**.

2. Nella scheda **Visualizzazioni**, seleziona **Importa**.

3. Seleziona un file e fai clic su **Apri**.

La visualizzazione viene aggiunta all'elenco delle visualizzazioni.


 
## Caricamento di una visualizzazione
{:#logging_kibana_visualizations_reload}

Completa la seguente procedura per caricare una visualizzazione salvata:

1. Nella barra degli strumenti della pagina Visualizza, fai clic sul pulsante **Carica visualizzazione salvata** ![Carica visualizzazione salvata](images/k4_visualization_open_icon.jpg "Carica visualizzazione salvata").

2. Seleziona la visualizzazione che desideri caricare. 


## Salvataggio di una visualizzazione
{:#logging_kibana_visualizations_save}

Completa la seguente procedura per salvare una visualizzazione nella pagina Visualizza:

1. Nella barra degli strumenti della pagina Visualizza, fai clic sul pulsante **Salva visualizzazione** ![Salva visualizzazione](images/k4_visualization_save_icon.jpg "Salva visualizzazione").

2. Immetti un nome per la visualizzazione.

3. Fai clic su Salva. 



## Condivisione di una visualizzazione
{:#logging_kibana_visualizations_share}

Completa la seguente procedura per condividere una visualizzazione nella pagina Visualizza:

1. Nella barra degli strumenti della pagina Visualizza, fai clic sul pulsante **Condividi visualizzazione** ![Condividi visualizzazione](images/k4_visualization_share_icon.jpg "Condividi visualizzazione").

2. Scegli una delle seguenti azioni:

    * **Incorpora questa visualizzazione**: seleziona questa opzione per condividere la visualizzazione tramite la tua origine HTML. 
    
        Fai clic sul pulsante di copia ![Copia negli appunti](images/k4_copy_to_clipboard.jpg "Copia negli appunti") per copiare il codice HTML che puoi utilizzare per incorporare la visualizzazione nella tua origine HTML. 
	
	**Nota**: per visualizzare la visualizzazione, gli utenti devono poter accedere a Kibana.
	
    * **Condividi un link**: seleziona questa opzione per condividere la visualizzazione in Kibana con altri utenti.



