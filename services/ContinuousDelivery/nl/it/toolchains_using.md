---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Utilizzo delle toolchain in {{site.data.keyword.Bluemix_notm}} pubblico
{: #toolchains-using}

Ultimo aggiornamento: 9 novembre 2016
{: .last-updated}

Puoi utilizzare una toolchain per essere produttivo nella tua attività di sviluppo, distribuzione e  nelle operazioni giornaliere. Dopo che hai configurato una toolchain, puoi aggiungere, eliminare o configurare le integrazioni dello strumento e gestire l'accesso alla toolchain. Le toolchain sono disponibili solo nella regione degli Stati Uniti Sud.
{: shortdesc}

## Configurazione di un'integrazione dello strumento
{: #configuring_a_tool_integration}

Se hai differito la configurazione di un'integrazione dello strumento quando hai creato una toolchain, viene visualizzato un pulsante **Configure** nel relativo tile. Se hai configurato un'integrazione dello strumento quando hai creato una toolchain, puoi aggiornare le impostazioni di configurazione.

1. Nel dashboard DevOps, nella pagina **Toolchain**, fai clic su una toolchain per aprirne la pagina Panoramica. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **Visualizza toolchain** e quindi su **Panoramica**.
1. Se hai bisogno di configurare un'integrazione dello strumento per la prima volta, nel suo tile, fai clic su **Configure**.

  ![Pulsante configura](images/toolchain_tile_configure.png)

 Quando hai terminato la configurazione dell'integrazione dello strumento, fai clic su **Save Integration**.
 
1. Se hai bisogno di aggiornare la configurazione dell'integrazione dello strumento, nel suo tile, fai clic sul menu per accedere alle opzioni di configurazione.

  ![Menu Configurazione](images/toolchain_tile_menu.png)
 
 Quando hai terminato di aggiornare le impostazioni, fai clic su **Save Integration**.

## Aggiunta di un'integrazione dello strumento
{: #adding_a_tool_integration}

Puoi aggiungere e configurare le integrazioni dello strumento per la tua toolchain.

1. Nel dashboard DevOps, nella pagina **Toolchain**, fai clic su una toolchain per aprirne la pagina Panoramica. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **Visualizza toolchain** e quindi su **Panoramica**.
1. Per visualizzare un elenco di integrazioni dello strumento da aggiungere, fai clic su **Aggiungi uno strumento**.
1. Fai clic sull'integrazione dello strumento che desideri aggiungere.
1. Immetti tutte le informazioni necessarie per configurare l'integrazione dello strumento. 
1. Fai clic su **Create Integration** per aggiungere l'integrazione dello strumento alla tua toolchain.

## Eliminazione di un'integrazione dello strumento
{: #deleting_a_tool_integration}

Se elimini un'integrazione dello strumento dalla tua toolchain, l'eliminazione non può essere annullata. 

1. Nel dashboard DevOps, nella pagina **Toolchain**, fai clic su una toolchain per aprirne la pagina Panoramica. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **Visualizza toolchain** e quindi su **Panoramica**.
1. Nel tile per l'integrazione dello strumento che desideri eliminare, fai clic sul menu per accedere alle opzioni di configurazione.
1. Per eliminare l'integrazione dello strumento dalla tua toolchain, fai clic su **Delete**.
1. Conferma facendo clic su **Delete**.  

## Gestione dell'accesso
{: #managing_access}

Puoi consentire agli utenti di accedere alla toolchain aggiungendoli all'organizzazione (org) a cui è associata la toolchain. Ogni toolchain è associata a un'organizzazione specifica e ogni utente che è membro di tale organizzazione può accedere alle toolchain associate. L'organizzazione in cui stai attualmente lavorando è visualizzata nella barra dei menu. Fai clic sull'organizzazione e passa a un'organizzazione differente per accedere a una serie diversa di toolchain.

1. Nel dashboard DevOps, nella pagina **Toolchain**, fai clic sulla toolchain da gestire e quindi fai clic su **Manage**. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain** e quindi su **Manage**.  
1. Fai clic sul link alla tua organizzazione. 
1. Nella pagina Manage Organizations, fai clic su **Invite a User** e immetti l'indirizzo email dell'utente.
1. Se desideri fornire le autorizzazioni avanzate per gestire gli utenti in {{site.data.keyword.Bluemix_notm}}, seleziona una o più delle seguenti caselle di spunta **Manager**, **Billing Manager** o **Auditor**.
1. Fai clic su **INVITE**.
1. Fai clic su **SALVA**. 

## Eliminazione di una toolchain
{: #deleting_a_toolchain}

Puoi eliminare una toolchain e specificare quali delle integrazioni dello strumento associate desideri eliminare. Quando elimini una toolchain, l'eliminazione non può essere annullata.

1. Nel dashboard DevOps, nella pagina **Toolchain**, fai clic sulla toolchain da eliminare e quindi su **Manage**. In alternativa, nella pagina della panoramica dell'applicazione, nel tile di fornitura continua, fai clic su **View Toolchain** e quindi su **Manage**.
1. Fai clic su **Delete Toolchain** e rivedi o modifica le integrazioni dello strumento che stai eliminando.
1. Conferma l'eliminazione digitando il nome della toolchain e facendo clic su **Delete**.  

 **Suggerimento**: quando elimini un'integrazione dello strumento GitHub, il repository GitHub associato non viene eliminato da GitHub. Devi rimuovere manualmente il repository da GitHub.


# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}

* [Create and use your first toolchain (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Create a custom toolchain (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Create an application with three microservices (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [Create a toolchain from a template on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Create a toolchain from an app on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Link correlati
{: #general}

* [Microservices toolchain (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (il link si apre in una nuova finestra)](https://www.ibm.com/devops/method){:new_window}
