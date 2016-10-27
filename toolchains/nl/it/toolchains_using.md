---

copyright:
  anni: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Utilizzo di toolchain in {{site.data.keyword.Bluemix_notm}} pubblico
{: #toolchains-using}

*Ultimo aggiornamento: 12 agosto 2016*
{: .last-updated}

L'utilizzo di una toolchain ti consente un maggior rendimento nelle tue attività quotidiane di sviluppo, distribuzione e operative. Dopo aver impostato una toolchain, puoi aggiungere, eliminare o configurare le integrazioni dello strumento e gestire l'accesso alla toolchain.
{: shortdesc}

**Importante**: questa funzionalità è sperimentale. Le toolchain potrebbero non essere stabili e potrebbero essere modificate secondo modalità non compatibili con le versioni precedenti. Non se ne consiglia l'utilizzo negli ambienti di produzione. Le toolchain sono disponibili solo nella regione Stati Uniti Sud.

## Configurazione di un'integrazione dello strumento
{: #configuring_a_tool_integration}

Se durante la creazione di una toolchain hai rimandato la configurazione di un'integrazione dello strumento, sul tile relativo viene mostrato il pulsante **Configura**. Se alla creazione della toolchain hai configurato un'integrazione dello strumento, puoi aggiornare le impostazioni di configurazione.

1. Nel dashboard DevOps, sulla scheda **Toolchain**, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nella pagina Panoramica dell'applicazione, sul tile Fornitura continua, fai clic su **Visualizza toolchain** e quindi su **Integrazioni strumento**.
1. Se devi configurare un'integrazione dello strumento per la prima volta, fai clic su **Configura** sul relativo tile.

  ![Pulsante Configura](images/toolchain_tile_configure.png)

 Una volta terminata la configurazione dell'integrazione dello strumento, fai clic su **Salva integrazione**.
 
1. Se devi aggiornare la configurazione di un'integrazione dello strumento, dal relativo tile, fai clic sul menu per accedere alle opzioni di configurazione.

  ![Menu di Configurazione](images/toolchain_tile_menu.png)
 
 Una volta terminato l'aggiornamento delle impostazioni, fai clic su **Salva integrazione**.

## Aggiunta di un'integrazione dello strumento
{: #adding_a_tool_integration}

Puoi aggiungere e configurare integrazioni dello strumento per la tua toolchain.

1. Nel dashboard DevOps, sulla scheda **Toolchain**, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nella pagina Panoramica dell'applicazione, sul tile Fornitura continua, fai clic su **Visualizza toolchain** e quindi su **Integrazioni strumento**.
1. Per visualizzare un elenco di integrazioni dello strumento da aggiungere, fai clic sul pulsante di aggiunta (+).
1. Fai clic su un'integrazione dello strumento che desideri aggiungere.
1. Immetti le informazioni richieste per configurare l'integrazione dello strumento. 
1. Fai clic su **Crea integrazione** per aggiungere l'integrazione dello strumento alla tua toolchain.

## Eliminazione di un'integrazione dello strumento
{: #deleting_a_tool_integration}

Se elimini un'integrazione dello strumento dalla tua toolchain, l'operazione di eliminazione non può essere annullata. 

1. Nel dashboard DevOps, sulla scheda **Toolchain**, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nella pagina Panoramica dell'applicazione, sul tile Fornitura continua, fai clic su **Visualizza toolchain** e quindi su **Integrazioni strumento**.
1. Nel tile dell'integrazione dello strumento che vuoi eliminare, fai clic sul menu per accedere alle opzioni di configurazione.
1. Per eliminare l'integrazione dello strumento dalla tua toolchain, fai clic su **Elimina**.
1. Conferma l'operazione facendo clic su **Elimina**.  

## Gestione dell'accesso
{: #managing_access}

Puoi concedere agli utenti l'accesso a una toolchain aggiungendoli all'organizzazione (org) a cui è associata la toolchain. Ogni toolchain è associata a una specifica organizzazione e qualsiasi utente membro di tale organizzazione può accedere alle toolchain associate. Fai clic sull'icona **{{site.data.keyword.avatar}}** ![icona Avatar](../icons/i-avatar-icon.svg) nella barra dei menu per aprire il widget Account e supporto e visualizzare l'organizzazione in cui stai lavorando. Passa a un'organizzazione differente per accedere a una serie diversa di toolchain.

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. Nel dashboard DevOps, sulla scheda **Toolchain**, fai clic sulla toolchain da gestire e seleziona quindi **Gestisci**. In alternativa, nella pagina Panoramica dell'applicazione, sul tile Fornitura continua, fai clic su **Visualizza toolchain** e quindi su **Gestisci**.  
1. Fai clic sul link della tua organizzazione. 
1. Nella pagina Gestisci organizzazioni, fai clic su **Invita un utente** e immetti l'indirizzo e-mail dell'utente. 
1. Se vuoi concedere autorizzazioni avanzate per gestire gli utenti nelle organizzazioni {{site.data.keyword.Bluemix_notm}}, seleziona una o più caselle di spunta tra **Gestore**, **Gestore fatturazione** o **Revisore**.
1. Fai clic su **INVITA**.
1. Fai clic su **SALVA**.

## Eliminazione di una toolchain
{: #deleting_a_toolchain}

Puoi eliminare una toolchain e specificare quali integrazioni dello strumento associate desideri rimuovere. Quando elimini una toolchain, l'operazione di eliminazione non può essere annullata.

1. Nel dashboard DevOps, sulla scheda **Toolchain**, fai clic sulla toolchain da eliminare e seleziona quindi **Gestisci**. In alternativa, nella pagina Panoramica dell'applicazione, sul tile Fornitura continua, fai clic su **Visualizza toolchain** e quindi su **Gestisci**.
1. Fai clic su **Elimina toolchain** ed esamina o modifica le integrazioni dello strumento da eliminare.
1. Conferma l'eliminazione immettendo il nome della toolchain e facendo clic su **Elimina**.  

 **Suggerimento**: quando elimini un'integrazione dello strumento GitHub, il repository GitHub associato non viene eliminato da GitHub e dovrai rimuoverlo manualmente.
