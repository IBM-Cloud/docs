---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Utilizzo delle toolchain
{: #toolchains-using}

Le toolchain aperte sono disponibili negli ambienti pubblico e dedicato in {{site.data.keyword.Bluemix}}. Puoi utilizzare una toolchain per essere produttivo nella tua attività di sviluppo, distribuzione e  nelle operazioni giornaliere. Dopo che hai configurato una toolchain, puoi aggiungere, eliminare o configurare le integrazioni dello strumento e gestire l'accesso alla toolchain. In {{site.data.keyword.Bluemix_notm}} pubblico, le toolchain sono disponibili solo nella regione degli Stati Uniti Sud. {: shortdesc}

## Configurazione di un'integrazione dello strumento
{: #configuring_a_tool_integration}

Se hai differito la configurazione di un'integrazione dello strumento quando hai creato una toolchain, viene visualizzato un pulsante **Configure** nella relativa scheda. Se hai configurato un'integrazione dello strumento quando hai creato una toolchain, puoi aggiornare le impostazioni di configurazione.

1. Nel dashboard DevOps, nella pagina **Toolchain**, fai clic su una toolchain per aprirne la pagina Panoramica. In alternativa, nella pagina della panoramica dell'applicazione, nella scheda di fornitura continua, fai clic su **Visualizza toolchain** e quindi su **Panoramica**.
1. Se hai bisogno di configurare un'integrazione dello strumento per la prima volta, nella sua scheda, fai clic su **Configure**. 

  ![Pulsante configura](images/toolchain_tile_configure.png)

 Quando hai terminato la configurazione dell'integrazione dello strumento, fai clic su **Save Integration**.

1. Se hai bisogno di aggiornare la configurazione dell'integrazione dello strumento, nella sua scheda, fai clic sul menu per accedere alle opzioni di configurazione. 

  ![Menu Configurazione](images/toolchain_tile_menu.png)

 **Suggerimento**: alcune delle integrazioni dello strumento sono preconfigurate e non richiedono alcun parametro di configurazione. Puoi aggiornare le impostazioni di configurazione solo per le integrazioni dello strumento che hai configurato.

 Quando hai terminato di aggiornare le impostazioni, fai clic su **Save Integration**.

## Aggiunta di un'integrazione dello strumento
{: #adding_a_tool_integration}

Puoi aggiungere e configurare le integrazioni dello strumento per la tua toolchain. Le integrazioni dello strumento disponibili sono diverse a seconda se utilizzi {{site.data.keyword.Bluemix_notm}} Pubblico o {{site.data.keyword.Bluemix_notm}} Dedicato.

1. Nel dashboard DevOps, nella pagina **Toolchain**, fai clic su una toolchain per aprirne la pagina Panoramica. In alternativa, nella pagina della panoramica dell'applicazione, nella scheda di fornitura continua, fai clic su **Visualizza toolchain** e quindi su **Panoramica**.
1. Per visualizzare un elenco di integrazioni dello strumento da aggiungere, fai clic su **Aggiungi uno strumento**.
1. Fai clic sull'integrazione dello strumento che desideri aggiungere.
1. Immetti tutte le informazioni necessarie per configurare l'integrazione dello strumento.
1. Fai clic su **Create Integration** per aggiungere l'integrazione dello strumento alla tua toolchain.

## Eliminazione di un'integrazione dello strumento
{: #deleting_a_tool_integration}

Se elimini un'integrazione dello strumento dalla tua toolchain, l'eliminazione non può essere annullata.

1. Nel dashboard DevOps, nella pagina **Toolchain**, fai clic su una toolchain per aprirne la pagina Panoramica. In alternativa, nella pagina della panoramica dell'applicazione, nella scheda di fornitura continua, fai clic su **Visualizza toolchain** e quindi su **Panoramica**.
1. Nella scheda per l'integrazione dello strumento che desideri eliminare, fai clic sul menu per accedere alle opzioni di configurazione. 
1. Per eliminare l'integrazione dello strumento dalla tua toolchain, fai clic su **Delete**.
1. Conferma facendo clic su **Delete**.  

## Gestione dell'accesso
{: #managing_access}

Puoi consentire agli utenti di accedere alla toolchain aggiungendoli all'organizzazione (org) a cui è associata la toolchain e all'elenco del controllo dell'accesso per la toolchain. Ogni toolchain è associata a un'organizzazione specifica e ogni utente che è membro di tale organizzazione può essere aggiunto per accedere alle toolchain associate. L'organizzazione con cui stai attualmente lavorando è visualizzata nella barra dei menu. Per accedere a un diversa serie di toolchain, passa a un'altra organizzazione.

Se stai utilizzando {{site.data.keyword.Bluemix_notm}} Dedicato per {{site.data.keyword.ghe_short}}, quando aggiungi gli utenti alla tua organizzazione o ai tuoi spazi {{site.data.keyword.Bluemix_notm}}, gli utenti possono accedere a {{site.data.keyword.ghe_short}} utilizzando i loro ID e password {{site.data.keyword.Bluemix_notm}}. Quando gli utenti accedono, vengono creati degli account per loro. Quando aggiungi utenti ai tuoi spazi o organizzazioni {{site.data.keyword.Bluemix_notm}}, vengono automaticamente aggiunti al repository {{site.data.keyword.ghe_short}}. Qualcuno che dispone dei privilegi da amministratore per il repository li deve aggiungere. Per ulteriori informazioni, vedi [Using Dedicated GitHub Enterprise](/docs/services/ghededicated/index.html){: new_window}. Se stai utilizzando la tua propria versione gestita di {{site.data.keyword.ghe_short}}, segui le procedure interne. 

###Suggerimenti per la gestione dell'accesso a una toolchain

* Per gestire l'accesso alla toolchain, nel dashboard DevOps, nella pagina **Toolchain**, fai clic sulla toolchain da gestire e quindi fai clic su **Manage**. In alternativa, nella pagina della panoramica dell'applicazione, nella scheda di fornitura continua, fai clic su **View Toolchain** e quindi su **Manage**.

* Per concedere l'accesso a tutti i membri dell'organizzazione della toolchain, fai clic su **Add org**. Tutti i membri di tale organizzazione possono visualizzare la toolchain.

* Puoi concedere i privilegi da amministratore a un'organizzazione o un utente. Gli amministratori possono modificare ed eliminare la toolchain. Per concedere i privilegi da amministratore, seleziona la casella di spunta **ADMIN** per l'organizzazione o l'utente.

* Se selezioni la casella di spunta **ADMIN** per un'organizzazione, tutti i membri di tale organizzazione diventano amministratori. Se aggiungi membri all'organizzazione dopo aver concesso i privilegi da amministratore all'organizzazione, a questi membri viene fornito lo stesso accesso degli altri membri nell'organizzazione.

* Per concedere l'accesso a un utente che è membro dell'organizzazione della toolchain, immetti l'ID dell'utente e fai clic su **Add user**. L'utente può visualizzare la toolchain.

* Per concedere l'accesso a un utente che non è membro dell'organizzazione della toolchain, completa la seguente procedura: 

   a. Dalla barra del menu, fai clic su **Manage > Account > Organizations**.

   b. Fai clic su **Invite Team Members**.
   
   c. Seleziona l'organizzazione in cui desideri invitare l'utente e fai clic su **Next**.
   
   d. Seleziona gli spazi a cui desideri l'utente possa accedere.
   
   e. Seleziona il ruolo da assegnare agli spazi selezionati nell'organizzazione. 
   
     **Nota**: per impostazione predefinita, i gestori dell'organizzazione hanno tutti i privilegi da amministratore per tutte le toolchain associate ad essa. Per concedere tutti i privilegi da amministratore all'utente, seleziona il ruolo **Gestore**. I ruoli Gestore della fatturazione e Revisore non influenzano l'accesso alla toolchain. Puoi modificare i ruoli successivamente nella pagina della directory del team. Per ulteriori informazioni, vedi [Gestione dei membri dei team e dei ruoli](/docs/admin/users_roles.html){: new_window}.
   
   f. Seleziona l'opzione per confermare che ti assumi la responsabilità finanziaria per tutti gli addebiti che si verificano nell'account.
   
   g. Immetti l'indirizzo email dell'utente che desideri invitare e fai clic su **Send**.

   h. Dopo che l'utente è un membro dell'organizzazione, ritorna alla pagina di gestione della toolchain e aggiungi l'utente alla toolchain.  


## Eliminazione di una toolchain
{: #deleting_a_toolchain}

Puoi eliminare una toolchain e specificare quali delle integrazioni dello strumento associate desideri eliminare. Quando elimini una toolchain, l'eliminazione non può essere annullata.

1. Nel dashboard DevOps, nella pagina **Toolchain**, fai clic sulla toolchain da eliminare. In alternativa, nella pagina della panoramica dell'applicazione, nella scheda di fornitura continua, fai clic su **View Toolchain**. 
1. Fai clic sul menu **More Actions**, accanto a **View app**.
1. Fai clic su **Delete** e rivedi o modifica le integrazioni dello strumento che stai eliminando. 
1. Conferma l'eliminazione digitando il nome della toolchain e facendo clic su **Delete**.  

 **Suggerimento**: quando elimini GitHub, {{site.data.keyword.ghe_short}} o i repository Git e l'integrazione dello strumento del tracciamento del problema, il repository associato non viene eliminato da GitHub, {{site.data.keyword.ghe_short}} o dai repository Git e dal tracciamento del problema. Devi rimuovere il repository manualmente.
