---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Utilizzo delle toolchain in {{site.data.keyword.Bluemix_notm}} dedicato
{: #toolchains-using_dedicated}

Ultimo aggiornamento: 13 settembre 2016
{: .last-updated}

Puoi utilizzare una toolchain per essere produttivo nella tua attività di sviluppo, distribuzione e  nelle operazioni giornaliere. Dopo che hai configurato una toolchain, puoi aggiungere, eliminare o configurare le integrazioni dello strumento e gestire l'accesso alla toolchain.
{: shortdesc}

## Configurazione di un'integrazione dello strumento
{: #configuring_a_tool_integration_dedicated}

Se hai differito la configurazione di un'integrazione dello strumento quando hai creato una toolchain, viene visualizzato un pulsante **Configure** nel relativo tile. Se hai configurato un'integrazione dello strumento quando hai creato una toolchain, puoi aggiornare le impostazioni di configurazione.

1. Nel dashboard, nella scheda **DEVOPS**, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nell'angolo in alto a destra della tua pagina di panoramica, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**.
1. Se hai bisogno di configurare un'integrazione dello strumento per la prima volta, nel suo tile, fai clic su **Configure**.

  ![Pulsante configura](images/toolchain_tile_configure.png)

 Quando hai terminato la configurazione dell'integrazione dello strumento, fai clic su **Save Integration**.
 
1. Se hai bisogno di aggiornare la configurazione dell'integrazione dello strumento, nel suo tile, fai clic sul menu per accedere alle opzioni di configurazione.

  ![Menu Configurazione](images/toolchain_tile_menu.png)
 
 Quando hai terminato di aggiornare le impostazioni, fai clic su **Save Integration**.

## Aggiunta di un'integrazione dello strumento
{: #adding_a_tool_integration_dedicated}

Puoi aggiungere e configurare le integrazioni dello strumento per la tua toolchain.

1. Nel dashboard, nella scheda **DEVOPS**, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nell'angolo in alto a destra della tua pagina di panoramica, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**.
1. Per visualizzare un elenco delle integrazioni dello strumento da aggiungere, fai clic sul pulsante di aggiunta (+).
1. Fai clic sull'integrazione dello strumento da aggiungere.
1. Immetti tutte le informazioni necessarie per configurare l'integrazione dello strumento. 
1. Fai clic su **Create Integration** per aggiungere l'integrazione dello strumento alla tua toolchain.

## Eliminazione di un'integrazione dello strumento
{: #deleting_a_tool_integration}

Se elimini un'integrazione dello strumento dalla tua toolchain, l'eliminazione non può essere annullata. 

1. Nel dashboard, nella scheda **DEVOPS**, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nell'angolo in alto a destra della tua pagina di panoramica, fai clic su **View Toolchain**. Quindi, fai clic su **Integrazioni dello strumento**.
1. Nel tile per l'integrazione dello strumento da eliminare, fai clic sul menu per accedere alle opzioni di configurazione.
1. Per eliminare l'integrazione dello strumento dalla tua toolchain, fai clic su **Delete**.
1. Conferma facendo clic su **Delete**. 

## Gestione dell'accesso
{: #managing_access_dedicated}

Puoi consentire agli utenti di accedere alla toolchain aggiungendoli all'organizzazione (org) a cui è associata la toolchain. Ogni toolchain è associata a un'organizzazione specifica e ogni utente che è membro di tale organizzazione può accedere alle toolchain associate. Per visualizzare l'organizzazione con cui stai correntemente lavorando, fai clic sull'icona **{{site.data.keyword.avatar}}** ![Icona Avatar](../icons/i-avatar-icon.svg) nella barra del menu. Per accedere a un diversa serie di toolchain, passa a un'altra organizzazione.

Quando aggiungi utenti ai tuoi spazi o organizzazioni {{site.data.keyword.Bluemix}}, gli utenti possono accedere a GitHub Enterprise utilizzando i loro ID e password {{site.data.keyword.Bluemix_notm}}. Quando gli utenti accedono, vengono creati degli account per loro. Quando aggiungi utenti ai tuoi spazi o organizzazioni {{site.data.keyword.Bluemix_notm}}, vengono automaticamente aggiunti al repository GitHub Enterprise. Qualcuno che dispone dei privilegi da amministratore per il repository li deve aggiungere. Per ulteriori informazioni, consulta [Using Dedicated GitHub Enterprise (il link si apre in una nuova finestra)](../services/ghededicated/index.html){: new_window}.

Per aggiungere un utente, completa la seguente procedura: 

1. Nel dashboard, nella scheda **DEVOPS**, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. Quindi, fai clic su **Manage**. In alternativa, nell'angolo in alto a destra della tua pagina di panoramica, fai clic su **View Toolchain**. Quindi, fai clic su **Manage**.  
1. Fai clic sul link alla tua organizzazione. 
1. Nella pagina Manage Organizations, fai clic su **Invite a User** e immetti l'indirizzo email dell'utente.
1. Se desideri fornire le autorizzazioni avanzate per gestire gli utenti in {{site.data.keyword.Bluemix_notm}}, seleziona una o più delle seguenti caselle di spunta **Manager**, **Billing Manager** o **Auditor**.
1. Fai clic su **INVITE**.
1. Fai clic su **SAVE**.

## Eliminazione di una toolchain
{: #deleting_a_toolchain_dedicated}

Puoi eliminare una toolchain e specificare quali delle integrazioni dello strumento associate desideri eliminare. Quando elimini una toolchain, l'eliminazione non può essere annullata.

1. Nel dashboard, nella scheda **DEVOPS**, fai clic sulla toolchain per aprirne la pagina Integrazioni dello strumento. Quindi, fai clic su **Manage**. In alternativa, nell'angolo in alto a destra della tua pagina di panoramica, fai clic su **View Toolchain**. Quindi, fai clic su **Manage**.
1. Fai clic su **Delete Toolchain** e rivedi o modifica le integrazioni dello strumento che stai eliminando.
1. Conferma l'eliminazione digitando il nome della toolchain e facendo clic su **Delete**.

 **Suggerimento**: quando elimini un'integrazione dello strumento GitHub Enterprise, il repository GitHub Enterprise associato non viene eliminato da GitHub Enterprise. Devi rimuovere manualmente il repository da GitHub Enterprise.
