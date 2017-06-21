---

copyright:
  years: 2017
lastupdated: "2017-05-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visualizzazione dei dati dai server IBM UrbanCode Deploy
{: #connect_ucd}

Per visualizzare i dati da un server IBM UrbanCode Deploy in Delivery Insights, devi configurare un'istanza di DevOps Connect, devi installare una patch sul server e devi quindi connetterlo a DevOps Connect.
{:shortdesc}

## Prerequisiti
{: #prereqs}

Per visualizzare le informazioni dai tuoi server IBM UrbanCode Deploy in {{site.data.keyword.DRA_short}}, devi ospitare un'istanza di DevOps Connect su un sistema che può collegarsi ai tuoi server IBM UrbanCode Deploy. Questo sistema può essere un computer fisico o una macchina virtuale. 

Il sistema che ospita DevOps Connect deve avere i seguenti prerequisiti:
- Il sistema deve avere una Java Runtime Environment (JRE) alla versione 8 o successiva.
- La variabile `PATH` di sistema deve includere l'ubicazione della JRE.
- Il sistema deve consentire a DevOps Connect di creare le connessioni in uscita a IBM Bluemix.

Inoltre, il tuo server IBM UrbanCode Deploy deve essere alla versione 6.2 o successive.

## Configurazione del servizio {{site.data.keyword.DRA_short}}
{: #configure_service}

Se non hai una toolchain o {{site.data.keyword.DRA_short}}, devi prima configurare {{site.data.keyword.DRA_short}}:
1. Dal catalogo {{site.data.keyword.Bluemix}}, fai clic su **{{site.data.keyword.DRA_short}}**, seleziona un piano dei prezzi e fai clic su **Create**.
1. Fai clic sulla scheda **Manage** e quindi su **Gain insights into UrbanCode deployments** fai clic su **Start Here**. In background, Delivery Insights crea una toolchain per la tua organizzazione. Le toolchain sono raccolte di integrazioni dello strumento, in questo caso IBM UrbanCode Deploy, e {{site.data.keyword.DRA_short}} fanno parte della tua toolchain. Per ulteriori informazioni sulle toolchain, vedi [Gestione delle toolchain](../ContinuousDelivery/toolchains_working.html).

Se già disponi di una toolchain, segui questa procedura per aggiungere Delivery Insights:
1. Se ancora non hai lo strumento {{site.data.keyword.DRA_short}}, aggiungilo alla tua toolchain.
1. Nella tua toolchain, fai clic sullo strumento {{site.data.keyword.DRA_short}}.
1. Vai alla pagina **Settings > Delivery Insights Setup**.

Ora puoi attenerti alle istruzioni nella pagina **Delivery Insights Setup** per installare DevOps Connect e connetterlo a {{site.data.keyword.DRA_short}}, come descritto nella prossima sezione.

## Installazione di DevOps Connect e sua connessione a {{site.data.keyword.DRA_short}}
{: #install_connect}

1. Nella pagina **Delivery Insights Setup**, segui le istruzioni per configurare DevOps Connect e collegare i tuoi server IBM UrbanCode Deploy. Questi passi includono:
{: #set_up_connect}
  1. Configurare un sistema per eseguire DevOps Connect, come descritto in [Prerequisiti](uc_insights_connect_ucd.html#prereqs).
  1. Scaricare DevOps Connect, che viene fornito in un file JAR eseguibile.
  1. Copiare lo script dalla pagina **Delivery Insights Setup** ed eseguirlo. Questo comando avvia DevOps Connect con un token che gli consente di connettersi alla tua organizzazione su {{site.data.keyword.Bluemix}}.
  1. Connetti i tuoi server IBM UrbanCode Deploy a DevOps Connect, come descritto nella prossima sezione.

## Connessione dei server IBM UrbanCode Deploy a DevOps Connect
{: #connect_ucd_to_connect}

1. Installa la patch nel tuo server IBM UrbanCode Deploy. Tutte le versioni di IBM UrbanCode Deploy richiedono una patch per comunicare con DevOps Connect. 
  1. Scarica la patch corretta per la tua versione di IBM UrbanCode Deploy andando alla seguente pagina e scaricando la patch corretta:
  [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. Estrai il file. Contiene uno o più file di patch che devi aggiungere al server.

  1. Arresta il server. Consulta [Starting and stopping the server](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.4/com.ibm.udeploy.install.doc/topics/run_server.html).

  1. Posiziona il file di patch nella cartella <code><em>application_data</em>/patches</code>, dove <code><em>application_data</em></code> è la cartella dei dati dell'applicazione del server. La cartella dei dati dell'applicazione del server predefinita è `/opt/ibm-ucd/server/appdata` su Linux e `C:\Program Files\ibm-ucd\server\appdata` su Windows. Nei sistemi ad elevata disponibilità, la cartella dei dati dell'applicazione è sempre su un'unità di rete condivisa a cui può accedere ogni server.

  1. Facoltativo: mentre il server viene arrestato, per incrementare le prestazioni dei dati importati da questo server, esegui i seguenti comandi SQL nel database:  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time);`  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);`  
  Utilizza il nome del tuo database per `MyUCDDatabase`.
  
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. Avvia il server. 

    **Nota:** potresti dover attendere più a lungo del normale per l'avvio del server IBM UrbanCode Deploy. Nel caso in cui il server non si avvii, o se non funziona correttamente, elimina i file di patch e procedi quindi a riavviarlo. I file di patch non influenzano in modo permanente il server.

1. Alcune versioni di IBM UrbanCode Deploy richiedono una patch aggiuntiva per il collegamento del server a DevOps Connect. Se stai utilizzando dalla versione 6.2 di IBM UrbanCode Deploy alla 6.2.1.2, devi installare la seguente patch aggiuntiva nel server:
  1. Scarica la the patch:  [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar).
  1. Arresta il server.
  1. Posiziona il file di patch nella cartella <code><em>application_data</em>/patches</code>.
  1. Avvia il server.

1. Crea un'integrazione tra DevOps Connect e il server IBM UrbanCode Deploy:  

  **Importante:** la prima volta che esegui l'integrazione, DevOps Connect richiama i dati dei precedenti 90 giorni. Se hai una grande quantità di dati di distribuzione, questo processo può impiegare molto tempo. Per richiamare i dati per meno di 90 giorni, consulta [Risoluzione dei problemi](uc_insights_connect_ucd.html#troubleshooting).
  1. In IBM UrbanCode Deploy, crea un token di autenticazione. Consulta [Token](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.4/com.ibm.udeploy.admin.doc/topics/security_token.html).
  1. In DevOps Connect, fai clic su **Integrations** e su **Add New**.
  1. Specifica un nome e una descrizione per l'integrazione. L'ubicazione predefinita di DevOps Connect è `https://hostname:8443/`, dove `hostname` è il nome host del sistema che ospita DevOps Connect.
  1. Dall'elenco **Integration Type**, seleziona **IBM UrbanCode Deploy for Cloud Reporting**.
  1. Nel campo **Server URI**, immetti l'URL pubblico del server IBM UrbanCode Deploy, come ad esempio `https://my_UCD.example.com:8447`.
  1. Nel campo **Authentication Token**, immetti o incolla il token di autenticazione che è stato generato da IBM UrbanCode Deploy.
  1. Nel campo **Admin User**, immetti un elenco separato da virgole di ID IBM per fornire l'accesso all'interfaccia DevOps Connect.
  1. Facoltativo: fai clic su **Run Integration** per eseguire l'integrazione immediatamente. Per impostazione predefinita, le integrazioni sono eseguite ogni minuto.
  1. Fai clic su **Save**.

  ![Configurazione dell'integrazione in DevOps Connect](images/uc_insights_dc_integration.gif)

Ora i tuoi dati sono sincronizzati con Delivery Insights. Puoi ora creare e visualizzare i report che si basano su tali dati. Associa quindi gli ambienti sui tuoi server IBM UrbanCode Deploy agli ambienti logici in Delivery Insights.

## Associazione degli ambienti ai report
{: #mapping}

### Ambienti logici

Delivery Insights raggruppa i tuoi ambienti IBM UrbanCode Deploy (detti anche *ambienti fisici*) in uno o più ambienti logici. In questo modo puoi raccogliere gli ambienti in gruppi che abbiano senso per te e per la tua organizzazione. Ad esempio, se disponi di molti ambienti di produzione per molte applicazioni, puoi raggruppare tutti questi ambienti in un solo ambiente logico e combinare le metriche per tutti questi ambienti in un solo dashboard dell'ambiente di produzione. L'associazione avviene per stringa di ricerca, così puoi raggruppare gli ambienti in qualsiasi modo abbia senso per i tuoi server IBM UrbanCode Deploy.

### Ambienti logici predefiniti

Per impostazione predefinita, i tuoi report includono gli ambienti logici che corrispondono agli ambienti IBM UrbanCode Deploy utilizzando le stringhe. Ad esempio, tutti gli ambienti con "dev" nel nome sono associati all'ambiente logico DEV e tutti gli ambienti con "prod" all'ambiente logico PROD.

![Gli ambienti logici predefiniti](images/uc_insights_mapping.gif)

### Associazione degli ambienti agli ambienti logici

Puoi associare manualmente gli ambienti fisici agli ambienti logici o puoi utilizzare i modelli per associarli in modo dinamico.

Per associare gli ambienti fisici agli ambienti logici utilizzando un modello, segui questa procedura:

1. In {{site.data.keyword.DRA_short}}, fai clic su **Delivery Insights > Map Environments**.
1. Fai clic su un ambiente logico esistente o su **Add Logical Environment**.
1. Nelle impostazioni dell'ambiente logico, in **Patterns**, fai clic su **Add Pattern**.
1. Specifica un modello per i nomi dell'ambiente. Puoi utilizzare l'asterisco (*) come carattere jolly. Ad esempio, il modello `env` corrisponde agli ambienti `env1`, `env2` e `env`.
1. Verifica che l'ambiente logico contenga gli ambienti che desideri.

Per associare gli ambienti logici manualmente, fai clic su **Add Manually** e seleziona gli ambienti da aggiungere o rimuovere.

![Configurazione dell'integrazione in DevOps Connect](images/uc_insights_mapping_manually.gif)

Ora che hai associato gli ambienti agli ambienti logici, puoi aggregare le informazioni di report in base a tali ambienti logici.

## Creazione dei report

Per creare un report, apri {{site.data.keyword.DRA_short}}, fai clic su **Delivery Insights > Reports** e quindi su **Add Report**. 

Dall'interno del report, puoi aggiungere le schede alla sezione **Metrics**, filtrare l'attività in **Recent application activity** e aggiungere i grafici alla sezione **Report Details**. Ogni grafico nella sezione **Report Details** è filtrabile e personalizzabile individualmente. Per visualizzare i dati non elaborati di un grafico, nella parte in alto a destra del grafico, fai clic sul pulsante delle impostazioni del grafico e quindi su **Report Data**.

Per modificare l'ordine dei grafici, nella parte in alto a destra della pagina, fai clic sul pulsante delle impostazioni e quindi su **Edit Chart Layout**. Adesso puoi trascinare e rilasciare i grafici per impostare l'ordine nel report.

## Condivisione di report
Per impostazione predefinita, puoi soltanto visualizzare i tuoi report Delivery Insights. Puoi condividere i report con altri utenti nella tua organizzazione Bluemix. Per condividere un report con qualcuno nella tua organizzazione Bluemix, aprilo e nella parte in alto ad destra, fai clic sul pulsante delle impostazioni e su **Share**.  

![Condivisione di un report](images/uc_insights_sharing.gif).

## Creazione dei report di controllo

I report di controllo visualizzano un elenco completo di tutte le attività che soddisfano i filtri che hai configurato, come un PDF. Per creare un report di controllo, fai clic su **Delivery Insights > Create Audit Report**. Quindi, specifica le informazioni per il report, incluso il nome. Inoltre, configura il contesto del report, come ad esempio un'applicazione, un ambiente logico o un ambiente su un server IBM UrbanCode Deploy (un ambiente fisico). Da lì, seleziona i dati da visualizzare nel report e fai clic su **Create**. 

## Risoluzione dei problemi
{: #troubleshooting}

In molti componenti e applicazioni, le richieste del processo sono archiviate nel tuo database del server IBM UrbanCode Deploy, si possono verificare degli errori durante il processo di richiamo. Viene registrato un messaggio simile al seguente nel log dell'output del server:

`ORA-01652: impossibile estendere il segmento temperatura da 128 nello spazio tabella TEMP`

Per risolvere questo problema, modifica il file `plugin.properties` del plugin per ridurre il numero di giorni validi dei dati da richiamare. Il file `plugin.properties` è nella directory `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` nel computer in cui hai installato DevOps Connect. Modifica la seguente riga per rimuovere il carattere del numero (#) e ridurre il numero di giorni:

`#numDaysToRetrieve=90`

Ad esempio, modifica la riga con il seguente testo per richiamare solo i precedenti 30 giorni validi di dati:

`numDaysToRetrieve=30`

Salva il file e quindi riesegui l'integrazione. Verifica i log del server per assicurarti per non si verifichi più l'errore.
