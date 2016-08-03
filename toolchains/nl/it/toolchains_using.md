---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Utilizzo delle toolchain
{: #toolchains-using}

*Ultimo aggiornamento: 4 maggio 2016*
{: .last-updated}

Puoi utilizzare una toolchain per essere produttivo nella tua attività di sviluppo, distribuzione e  nelle operazioni giornaliere. Dopo che hai configurato una toolchain, puoi aggiungere, eliminare o configurare le integrazioni dello strumento e gestire l'accesso alla toolchain.
{: shortdesc}

**Importante**: questa funzionalità è sperimentale. Le toolchain potrebbero non essere stabili e potrebbero venire modificate in modi che le rendono non compatibili con le versioni precedenti. Non sono raccomandate per l'utilizzo in ambienti di produzione. Per utilizzare le toolchain, devi effettuare una [richiesta di accesso](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window} monouso. Le toolchain sono disponibili solo nella regione degli Stati Uniti Sud.

## Configurazione di un'integrazione dello strumento
{: #configuring_a_tool_integration}

Puoi configurare un'integrazione dello strumento per la prima volta o aggiornare le impostazioni di configurazione per un'integrazione dello strumento che fa già parte della tua toolchain.

1. Nel Dashboard DevOps, nella scheda **Toolchains**, fai clic su una toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain** e quindi su **Integrazioni dello strumento**.
1. Se hai bisogno di configurare un'integrazione dello strumento per la prima volta, nel suo tile, fai clic su **Configure**.

  ![Pulsante configura](images/toolchain_tile_configure.png)

 Quando hai terminato la configurazione dell'integrazione dello strumento, fai clic su **Save Integration**.
 
1. Se hai bisogno di aggiornare la configurazione dell'integrazione dello strumento, nel suo tile, fai clic sul menu per accedere alle opzioni di configurazione.

  ![Menu Configurazione](images/toolchain_tile_menu.png)
 
 Quando hai terminato di aggiornare le impostazioni, fai clic su **Save Integration**.

 **Nota**: dopo che hai configurato il repository per un'integrazione dello strumento GitHub, può essere aggiornato l'url del repository ma il repository stesso non può essere modificato. Per utilizzare un repository differente, elimina l'integrazione dello strumento GitHub corrente dalla tua toolchain, aggiungi un'integrazione dello strumento GitHub alla tua toolchain e configurala per utilizzare il nuovo repository.

## Aggiunta di un'integrazione dello strumento
{: #adding_a_tool_integration}

Puoi aggiungere e configurare le integrazioni dello strumento per la tua toolchain.

1. Nel Dashboard DevOps, nella scheda **Toolchains**, fai clic su una toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain** e quindi su **Integrazioni dello strumento**.
1. Per visualizzare un elenco delle integrazioni dello strumento da aggiungere, fai clic sul pulsante di aggiunta (+).
1. Fai clic sull'integrazione dello strumento che desideri aggiungere.
1. Immetti tutte le informazioni necessarie per configurare l'integrazione dello strumento. 
1. Fai clic su **Create Integration** per aggiungere l'integrazione dello strumento alla tua toolchain.

## Eliminazione di un'integrazione dello strumento
{: #deleting_a_tool_integration}

Puoi eliminare un'integrazione dello strumento dalla tua toolchain. 

1. Nel Dashboard DevOps, nella scheda **Toolchains**, fai clic su una toolchain per aprirne la pagina Integrazioni dello strumento. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain** e quindi su **Integrazioni dello strumento**.
1. Nel tile per l'integrazione dello strumento che desideri eliminare, fai clic sul menu per accedere alle opzioni di configurazione.
1. Per eliminare l'integrazione dello strumento dalla tua toolchain, fai clic su **Delete**.
1. Conferma facendo clic su **Delete**.

## Gestione dell'accesso
{: #managing_access}

Puoi consentire agli utenti di accedere alla toolchain aggiungendoli all'organizzazione (org) a cui è associata la toolchain. Ogni toolchain è associata a un'organizzazione specifica e ogni utente che è membro di tale organizzazione può accedere alle toolchain associate. Se passi a un'organizzazione differente, puoi accedere a una serie diversa di toolchain.

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. Nel Dashboard DevOps, nella scheda **Toolchains**, fai clic sulla toolchain da gestire e quindi fai clic su **Manage**. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain** e quindi su **Manage**.  
1. Fai clic sul link alla tua organizzazione. 
1. Nella pagina Manage Organizations, fai clic su **Invite a User** e immetti l'indirizzo email dell'utente.
1. Se desideri fornire le autorizzazioni avanzate all'utente, seleziona una o più delle seguenti caselle di spunta **Manager**, **Billing Manager** o **Auditor**.
1. Fai clic su **INVITE**.
1. Fai clic su **SAVE**.

## Eliminazione di una toolchain
{: #deleting_a_toolchain}

Puoi eliminare una toolchain e specificare quali delle integrazioni dello strumento associate desideri eliminare.

1. Nel Dashboard DevOps, nella scheda **Toolchains**, fai clic sulla toolchain da eliminare e quindi fai clic su **Manage**. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain** e quindi su **Manage**.
1. Fai clic su **Delete Toolchain** e rivedi le integrazioni dello strumento che stai eliminando.
1. Conferma l'eliminazione digitando il nome della toolchain e facendo clic su **Delete**.

 **Suggerimento**: quando elimini un'integrazione dello strumento GitHub, il repository GitHub associato non viene eliminato da GitHub. Devi rimuovere manualmente il repository da GitHub.
