---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analisi dei log in Kibana tramite un dashboard
{:#kibana_analize_logs_dashboard}

Utilizza la pagina *Dashboard* in Kibana per visualizzare le raccolte di visualizzazioni raggruppate nei dashboard. Utilizza i dashboard per analizzare i tuoi dati di log e confrontare i risultati.
{:shortdesc}

In {{site.data.keyword.Bluemix}}, esistono diversi tipi di dashboard che puoi definire e personalizzare per visualizzare e analizzare i dati. Ad esempio, la seguente tabella elenca alcuni tipi di dashboard comuni: 

| Tipo di dashboard | Descrizione |
|-------------------|-------------|
| Dashboard a singola applicazione cf  | Questo dashboard mostra le informazioni per una singola applicazione Cloud Foundry.  |
| Dashboard a singolo contenitore   | Questo dashboard mostra le informazioni per un singolo contenitore.   |
| Dashboard del gruppo di contenitori   | Questo dashboard mostra le informazioni per un gruppo di contenitori specifico.   |
| Dashboard a più applicazioni cf  | Questo dashboard mostra informazioni per tutte le applicazioni Cloud Foundry distribuite nello stesso spazio {{site.data.keyword.Bluemix_notm}}.   | 
| Dashboard a più contenitori  | Questo dashboard mostra informazioni per tutti i contenitori distribuiti nello stesso spazio {{site.data.keyword.Bluemix_notm}}.  |
| Dashboard spazio | Questo dashboard mostra la registrazione dei dati disponibile in uno spazio {{site.data.keyword.Bluemix_notm}}.  | 

Per visualizzare i dati in un dashboard, configura i pannelli. Kibana include diverse visualizzazioni, come tabella, tendenze e istogramma, che puoi utilizzare per analizzare le informazioni. Una visualizzazione viene aggiunta come un pannello a un dashboard. Puoi aggiungere, rimuovere e riorganizzare i pannelli nel dashboard. Ogni pannello ha un obiettivo diverso. Alcuni pannelli sono organizzati in righe che forniscono i risultati di una o più query. Altri pannelli visualizzano documenti o informazioni personalizzate. Ogni pannello si basa su una ricerca. La ricerca definisce la sottoserie di dati che visualizza il pannello. Ad esempio, puoi configurare un grafico a barre, un grafico a torta o una tabella per visualizzare i dati e analizzarli.  

La seguente tabella elenca diverse attività che puoi eseguire nella pagina Dashboard:

| Attività | Informazioni aggiuntive |
|------|------------------|
| [Creare un nuovo dashboard](logging_kibana_analize_logs_dashboard.html#K4_dashboard_new) | Puoi creare più dashboard. Ogni dashboard può essere progettato per includere diverse ricerche, visualizzazioni e una sottorete di dati di log differente.  |
| [Salvare un dashboard](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save) | Puoi salvare un dashboard per un riutilizzo successivo. |
| [Caricare un dashboard](logging_kibana_analize_logs_dashboard.html#k4_dashboard_reload) | Puoi caricare un dashboard per aggiornarne i dati, modificarlo o analizzare i dati. |
| [Eliminare un dashboard](logging_kibana_analize_logs_dashboard.html#k4_dashboard_delete) | Eliminare i dashboard che non sono richiesti. |
| [Esportare un dashboard](logging_kibana_analize_logs_dashboard.html#k4_dashboard_export) | Puoi esportare un dashboard come un file JSON. |
| [Importare un dashboard](logging_kibana_analize_logs_dashboard.html#k4_dashboard_import) | Puoi importare un dashboard come un file JSON.  |
| [Condividere un dashboard](logging_kibana_analize_logs_dashboard.html#k4_dashboard_share) | Puoi condividere un dashboard tramite la tua origine HTML o il dashboard Kibana. |
| [Aggiungere una visualizzazione](logging_kibana_analize_logs_dashboard.html#k4_dashboard_add_visualization) | Puoi aggiungere una ricerca o una visualizzazione esistente a un dashboard.|

Per ulteriori informazioni su Kibana, consulta [Kibana User Guide ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.



## Creazione di un nuovo dashboard Kibana
{: #K4_dashboard_new}

Per creare un nuovo dashboard completa la seguente procedura: 

1. Nella barra degli strumenti della pagina Dashboard, fai clic sul pulsante **Nuovo dashboard** ![Nuovo dashboard](images/k4_dash_new_icon.jpg "Nuovo dashboard").

2. Aggiungi una o più ricerche o visualizzazioni. Per ulteriori informazioni, vedi [Aggiunta di una nuova ricerca o visualizzazione](logging_kibana_analize_logs_dashboard.html#K4_dashboard_add_visualization).

    Dopo aver aggiunto una ricerca o una visualizzazione, viene aggiunto un pannello al dashboard.

3. Trascina e rilascia un pannello nella parte del dashboard in cui desideri posizionarlo.
 
4. Salva il dashboard per un riutilizzo successivo. Per ulteriori informazioni, vedi [Salvataggio di un dashboard Kibana](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save).


## Aggiunta di una nuova ricerca o visualizzazione 
{: #k4_dashboard_add_visualization}

Completa la seguente procedura per aggiungere una ricerca o una visualizzazione esistente: 

1. Nella barra degli strumenti della pagina Dashboard, fai clic sul pulsante **Aggiungi visualizzazione** ![Aggiungi visualizzazione](images/k4_dash_add_visualization_icon.jpg "Aggiungi visualizzazione").

    **Nota**: puoi aggiungere visualizzazioni e ricerche. 

2. Seleziona la scheda **Visualizzazioni** per aggiungere una visualizzazione o seleziona la scheda **Ricerche** per aggiungere una ricerca.

3. Fai clic sulla ricerca o visualizzazione che desideri aggiungere.

    Viene aggiunto un pannello per questa ricerca o visualizzazione al dashboard.



## Salvataggio di un dashboard Kibana
{: #k4_dashboard_save}

Completa la seguente procedura per salvare un dashboard Kibana dopo averlo personalizzato:

1. Nella barra degli strumenti, fai clic sul pulsante **Salva** ![Salva dashboard](images/k4_dash_save_icon.jpg "Salva dashboard").

2. Immetti un nome per il dashboard.

    **Nota:** un dashboard con un nome che contiene spazi vuoti non verrà salvato.

3. Accanto al nome campo, fai clic sull'icona **Salva**.


## Eliminazione di un dashboard Kibana
{: #k4_dashboard_delete}

Per eliminare una visualizzazione, completa la seguente procedura nella pagina Impostazioni:

1. Nella pagina Impostazioni, seleziona la scheda **Oggetti**.

2. Nella scheda **Visualizzazioni**, seleziona le visualizzazioni che desideri eliminare.

3. Fai clic su **Elimina**.


## Caricamento di un dashboard Kibana
{: #k4_dashboard_reload}

Completa la seguente procedura per caricare un dashboard salvato:

1. Nella barra degli strumenti della pagina Dashboard, fai clic sul pulsante **Carica dashboard salvato** ![Carica dashboard salvato](images/k4_dash_load_icon.jpg "Carica dashboard salvato").

2. Seleziona il dashboard che desideri caricare. 


## Esportazione di un dashboard Kibana 
{: #k4_dashboard_export}

Per esportare un dashboard come un file JSON, completa la seguente procedura nella pagina Impostazioni:

1. Nella pagina Impostazioni, seleziona la scheda **Oggetti**.

2. Nella scheda **Dashboard**, seleziona il dashboard che desideri esportare.

3. Fai clic su **Esporta**.

4. Salva il file.


## Importazione di un dashboard Kibana
{: #k4_dashboard_import}

Per importare un dashboard come un file JSON, completa la seguente procedura nella pagina Impostazioni: 

1. Nella pagina Impostazioni, seleziona la scheda **Oggetti**.

2. Nella scheda **Dashboard**, seleziona **Importa**.

3. Seleziona un file e fai clic su **Apri**. 

Il dashboard viene aggiunto all'elenco dei dashboard.


## Condivisione di un dashboard Kibana 
{: #k4_dashboard_share}

Completa la seguente procedura per condividere un dashboard:

1. Nella barra degli strumenti della pagina Dashboard, fai clic sul pulsante **Condividi dashboard** ![Condividi dashboard](images/k4_dash_share_icon.jpg "Condividi dashboard").

2. Scegli una delle seguenti azioni: 

    * **Incorpora questo dashboard**: seleziona questa opzione per condividere il dashboard tramite la tua origine HTML. 
    
        Fai clic sul pulsante di copia ![Copia negli appunti](images/k4_copy_to_clipboard.jpg "Copia negli appunti") per copiare il codice HTML che puoi utilizzare per incorporare il dashboard nella tua origine HTML. 
        
        **Nota**: per visualizzare il dashboard, gli utenti devono poter accedere a Kibana.
	
    * **Condividi un link**: seleziona questa opzione per condividere il dashboard in Kibana con altri utenti.



