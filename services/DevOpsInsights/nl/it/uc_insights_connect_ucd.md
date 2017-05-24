---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connessione dei server IBM UrbanCode Deploy a Delivery Insights
{: #connect_ucd}

Per visualizzare i dati da un server IBM UrbanCode Deploy in Delivery Insights, devi installare una patch sul server e collegarlo a DevOps Connect.
{:shortdesc}

## Prima di cominciare

- Visualizza i [prerequisiti](uc_insights_prereqs.html), inclusa la configurazione di un'istanza di DevOps Connect.
- Il tuo server IBM UrbanCode Deploy deve essere alla versione 6.2 o successive.

## Procedura 

1. Installa la patch nel tuo server IBM UrbanCode Deploy. Tutte le versioni di IBM UrbanCode Deploy richiedono una patch per comunicare con DevOps Connect. 
  1. Scarica la patch corretta per la tua versione di IBM UrbanCode Deploy andando alla seguente pagina e scaricando la patch corretta:
  [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. Estrai il file. Contiene uno o più file di patch che devi aggiungere al server.

  1. Arresta il server. Consulta [Starting and stopping the server](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.install.doc/topics/run_server.html).

  1. Posiziona il file di patch nella cartella <code><em>application_data</em>/patches</code>, dove <code><em>application_data</em></code> è la cartella dei dati dell'applicazione del server. La cartella dei dati dell'applicazione del server predefinita è `/opt/ibm-ucd/server/appdata` su Linux e `C:\Program Files\ibm-ucd\server\appdata` su Windows. Nei sistemi ad elevata disponibilità, la cartella dei dati dell'applicazione è sempre su un'unità di rete condivisa a cui può accedere ogni server.

  1. Facoltativo: mentre il server viene arrestato, per incrementare le prestazioni dei dati importati da questo server, esegui i seguenti comandi SQL nel database:  
  ```
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time); 
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);
  ```
  Utilizza il nome del tuo database per `MyUCDDatabase`.
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. Avvia il server. 

    **Nota:** potresti dover attendere più a lungo del normale per l'avvio del server IBM UrbanCode Deploy. Se alla fine il server non si avvia o se non funziona correttamente, elimina i file di patch e riavvialo. I file di patch non influenzano in modo permanente il server.

1. Alcune versioni di IBM UrbanCode Deploy richiedono una patch aggiuntiva per il collegamento del server a DevOps Connect. Se stai utilizzando dalla versione 6.2 di IBM UrbanCode Deploy alla 6.2.1.2, devi installare la seguente patch aggiuntiva nel server:
  1. Scarica la the patch:  [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar).
  1. Arresta il server. 
  1. Posiziona il file di patch nella cartella <code><em>application_data</em>/patches</code>.
  1. Avvia il server.

1. Crea un'integrazione tra DevOps Connect e il server IBM UrbanCode Deploy:  
  **Importante:** la prima volta che esegui l'integrazione, DevOps Connect richiama i dati dei precedenti 90 giorni. Se hai una grande quantità di dati di distribuzione, questo processo può impiegare molto tempo. Per richiamare i dati per meno di 90 giorni, consulta [Risoluzione dei problemi](uc_insights_connect_ucd.html#troubleshooting).
  1. In IBM UrbanCode Deploy, crea un token di autenticazione. Consulta [Token](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.admin.doc/topics/security_token.html).
  1. In DevOps Connect, fai clic su **Integrations** e su **Add New**.
  1. Specifica un nome e una descrizione per l'integrazione. L'ubicazione predefinita di DevOps Connect è `https://hostname:8443/`, dove `hostname` è il nome host del sistema che ospita DevOps Connect.
  1. Dall'elenco **Integration Type**, seleziona **IBM UrbanCode Deploy for Cloud Reporting**.
  1. Nel campo **Server URI**, immetti l'URL pubblico del server IBM UrbanCode Deploy, come ad esempio `https://my_UCD.example.com:8447`.
  1. Nel campo **Authentication Token**, immetti o incolla il token di autenticazione che è stato generato da IBM UrbanCode Deploy.
  1. Nel campo **Admin User**, immetti un elenco separato da virgole di ID IBM per fornire l'accesso all'interfaccia DevOps Connect.
  1. Facoltativo: fai clic su **Run Integration** per eseguire l'integrazione immediatamente. Per impostazione predefinita, le integrazioni sono eseguite ogni minuto.
  1. Fai clic su **Save**.

  ![Configurazione dell'integrazione in DevOps Connect](images/uc_insights_dc_integration.gif)

Ora i tuoi dati sono sincronizzati con Delivery Insights. Puoi ora creare e visualizzare i report che si basano su tali dati.

## Risoluzione dei problemi
{: #troubleshooting}

In molti componenti e applicazioni, le richieste del processo sono archiviate nel tuo database del server IBM UrbanCode Deploy, si possono verificare degli errori durante il processo di richiamo. Viene registrato un messaggio simile al seguente nel log dell'output del server:

`ORA-01652: impossibile estendere il segmento temperatura da 128 nello spazio tabella TEMP`

Per risolvere questo problema, modifica il file `plugin.properties` del plugin per ridurre il numero di giorni validi dei dati da richiamare. Il file `plugin.properties` è nella directory `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` nel computer in cui hai installato DevOps Connect. Modifica la seguente riga per rimuovere il carattere del numero (#) e ridurre il numero di giorni:

`#numDaysToRetrieve=90`

Ad esempio, modifica la riga con il seguente testo per richiamare solo i precedenti 30 giorni validi di dati:

`numDaysToRetrieve=30`

Salva il file e quindi riesegui l'integrazione. Verifica i log del server per assicurarti per non si verifichi più l'errore.
