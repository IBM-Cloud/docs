---

copyright:
  anni: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Utilizzo di toolchain su {{site.data.keyword.Bluemix_notm}} dedicato
{: #toolchains-using_dedicated}

Ultimo aggiornamento: 26 agosto 2016
{: .last-updated}

L'utilizzo di una toolchain ti consente un maggior rendimento nelle tue attività quotidiane di sviluppo, distribuzione e operative. Dopo aver impostato una toolchain, puoi aggiungere, eliminare o configurare le integrazioni dello strumento e gestire l'accesso alla toolchain.
{: shortdesc}

**Importante**: questa funzionalità è sperimentale. Le toolchain potrebbero non essere stabili e potrebbero essere modificate secondo modalità non compatibili con le versioni precedenti. Non se ne consiglia l'utilizzo negli ambienti di produzione.  

## Configurazione di un'integrazione dello strumento
{: #configuring_a_tool_integration_dedicated}

Se durante la creazione di una toolchain hai rimandato la configurazione di un'integrazione dello strumento, sul tile relativo viene mostrato il pulsante **Configura**. Se alla creazione della toolchain hai configurato un'integrazione dello strumento, puoi aggiornare le impostazioni di configurazione.

1. Nel Dashboard, sulla scheda **DEVOPS**, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nell'angolo superiore destro della pagina Panoramica dell'applicazione, fai clic su **Visualizza toolchain**. Fai quindi clic su **Integrazioni strumento**.
1. Se devi configurare un'integrazione dello strumento per la prima volta, fai clic su **Configura** sul relativo tile.

  ![Pulsante Configura](images/toolchain_tile_configure.png)

 Una volta terminata la configurazione dell'integrazione dello strumento, fai clic su **Salva integrazione**.
 
1. Se devi aggiornare la configurazione di un'integrazione dello strumento, dal relativo tile, fai clic sul menu per accedere alle opzioni di configurazione.

  ![Menu di Configurazione](images/toolchain_tile_menu.png)
 
 Una volta terminato l'aggiornamento delle impostazioni, fai clic su **Salva integrazione**.

## Aggiunta di un'integrazione dello strumento
{: #adding_a_tool_integration_dedicated}

Puoi aggiungere e configurare integrazioni dello strumento per la tua toolchain.

1. Nel Dashboard, sulla scheda **DEVOPS**, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nell'angolo superiore destro della pagina Panoramica dell'applicazione, fai clic su **Visualizza toolchain**. Fai quindi clic su **Integrazioni strumento**.
1. Per visualizzare un elenco di integrazioni dello strumento da aggiungere, fai clic sul pulsante di aggiunta (+).
1. Fai clic sull'integrazione dello strumento da aggiungere.
1. Immetti le informazioni richieste per configurare l'integrazione dello strumento. 
1. Fai clic su **Crea integrazione** per aggiungere l'integrazione dello strumento alla tua toolchain.

## Eliminazione di un'integrazione dello strumento
{: #deleting_a_tool_integration}

Se elimini un'integrazione dello strumento dalla tua toolchain, l'operazione di eliminazione non può essere annullata. 

1. Nel Dashboard, sulla scheda **DEVOPS**, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. In alternativa, nell'angolo superiore destro della pagina Panoramica dell'applicazione, fai clic su **Visualizza toolchain**. Fai quindi clic su **Integrazioni strumento**.
1. Nel tile dell'integrazione dello strumento da eliminare, fai clic sul menu per accedere alle opzioni di configurazione.
1. Per eliminare l'integrazione dello strumento dalla tua toolchain, fai clic su **Elimina**.
1. Conferma l'operazione facendo clic su **Elimina**. 

## Gestione dell'accesso
{: #managing_access_dedicated}

Puoi concedere agli utenti l'accesso a una toolchain aggiungendoli all'organizzazione (org) a cui è associata la toolchain. Ogni toolchain è associata a una specifica organizzazione e qualsiasi utente membro di tale organizzazione può accedere alle toolchain associate. Per visualizzare l'organizzazione in cui stai lavorando, fai clic sull'icona **{{site.data.keyword.avatar}}** ![icona Avatar](../icons/i-avatar-icon.svg) nella barra dei menu. Per accedere a una serie di toolchain diversa, passa a un'altra organizzazione. 

Quando aggiungi gli utenti alla tua organizzazione e agli spazi {{site.data.keyword.Bluemix}}, gli utenti possono accedere a GitHub Enterprise utilizzando i propri ID e password {{site.data.keyword.Bluemix_notm}}. Nel momento in cui gli utenti effettuano l'accesso, gli account vengono creati automaticamente. Quando aggiungi gli utenti alla tua organizzazione e agli spazi {{site.data.keyword.Bluemix_notm}}, questi non vengono aggiunti automaticamente al repository GitHub Enterprise. Tali utenti devono essere aggiunti da qualcuno che dispone dei privilegi di amministratore. Per ulteriori informazioni, vedi [Using Dedicated GitHub Enterprise](../services/ghededicated/index.html){: new_window}.

Per aggiungere un utente, utilizza la seguente procedura: 

1. Nel Dashboard, sulla scheda **DEVOPS**, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. Fai quindi clic su **Gestisci**. In alternativa, nell'angolo superiore destro della pagina Panoramica dell'applicazione, fai clic su **Visualizza toolchain**. Fai quindi clic su **Gestisci**.   
1. Fai clic sul link alla tua organizzazione. 
1. Nella pagina Gestisci organizzazioni, fai clic su **Invita un utente** e immetti l'indirizzo e-mail dell'utente. 
1. Se vuoi concedere autorizzazioni avanzate per gestire gli utenti nelle organizzazioni {{site.data.keyword.Bluemix_notm}}, seleziona una o più caselle di spunta tra **Gestore**, **Gestore fatturazione** o **Revisore**.
1. Fai clic su **INVITA**.
1. Fai clic su **SALVA**.

## Eliminazione di una toolchain
{: #deleting_a_toolchain_dedicated}

Puoi eliminare una toolchain e specificare quali integrazioni dello strumento associate desideri rimuovere. Quando elimini una toolchain, l'operazione di eliminazione non può essere annullata.

1. Nel Dashboard, sulla scheda **DEVOPS**, fai clic sulla toolchain per aprire la pagina Integrazioni strumento. Fai quindi clic su **Gestisci**. In alternativa, nell'angolo superiore destro della pagina Panoramica dell'applicazione, fai clic su **Visualizza toolchain**. Fai quindi clic su **Gestisci**. 
1. Fai clic su **Elimina toolchain** ed esamina o modifica le integrazioni dello strumento da eliminare.
1. Conferma l'eliminazione immettendo il nome della toolchain e facendo clic su **Elimina**.

 **Suggerimento**: quando elimini un'integrazione dello strumento GitHub Enterprise, il repository GitHub Enterprise associato non viene eliminato da GitHub Enterprise  e dovrai rimuoverlo manualmente.
