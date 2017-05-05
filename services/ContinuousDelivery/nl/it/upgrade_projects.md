---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-21"

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Aggiorna il tuo progetto {{site.data.keyword.jazzhub_short}} a una toolchain
{: #upgrade_projects}

{{site.data.keyword.jazzhub}} si sta trasformando in {{site.data.keyword.contdelivery_full}}. Come parte di tale cambiamento, i progetti saranno aggiornati in toolchain. 

Puoi aggiornare il tuo progetto o attendere che venga aggiornato automaticamente. Per un'esperienza ottimale, aggiorna il tuo progetto il prima possibile in modo da poter controllare quale sia il nome della tua toolchain e in quale organizzazione venga creata.  
{: shortdesc}

## Toolchain
{: #compare_toolchains}

Le toolchain sono simili ai progetti, con alcune importanti differenze:

- I progetti possono avere solo un repository (repo) e una pipeline. Le toolchain possono avere quanti repository e pipeline necessiti.
- Le toolchain possono includere gli strumenti che non sono disponibili nei progetti, come Slack, Sauce Labs, PagerDuty e {{site.data.keyword.DRA_full}}.
- L'accesso alle toolchain è gestito tramite le organizzazioni Bluemix standard. L'appartenenza viene mantenuta al livello dell'organizzazione, in modo diverso dai progetti, in cui l'appartenenza era mantenuta al livello del progetto.

Puoi trovare ulteriori informazioni sulle toolchain in [YouTube![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://youtu.be/2SIPE1e7NJ4){: new_window} o da [Introduzione a {{site.data.keyword.contdelivery_short}}](/docs/services/ContinuousDelivery/index.html).
[![Link esterno a YouTube](images/CD_video.png)](https://youtu.be/2SIPE1e7NJ4){: new_window}    

## Prerequisiti
{: #upgrade_prereqs}    

- Per accedere alla tua toolchain del progetto aggiornata, hai bisogno di un ID Bluemix. Prima di eseguire l'aggiornamento, devi verificare di disporre di un ID Bluemix attivo. Se non ne hai uno, [registrati](https://console.ng.bluemix.net/registration/).
- Assicurati che il tuo proprietario del progetto dei servizi DevOps sia corretto. La toolchain che viene creata dal tuo progetto sarà parte dell'organizzazione Bluemix di tale proprietario.

**Importante:** Eclipse Orion {{site.data.keyword.webide}} nella toolchain è separato da {{site.data.keyword.webide}} che è associato al tuo progetto. Se utilizzi {{site.data.keyword.webide}} e hai delle modifiche non eseguite, eseguile prima dell'aggiornamento.  


## Aggiornamento da un progetto a una toolchain
{: #project_to_toolchain}

Quando il tuo progetto è pronto per essere aggiornato, viene visualizzato un messaggio nella scheda del progetto e nella pagina della panoramica.

![Immagine della scheda con l'etichetta pronto per l'aggiornamento](images/card-project-to-upgrade.png)

![Ora del messaggio pronto per l'aggiornamento](images/banner-ready-to-upgrade.png)

**Suggerimento:** puoi trovare i progetti che sono pronti per l'aggiornamento dal menu nella pagina dei progetti personali: 

![Immagine della voce del menu progetti per l'aggiornamento](images/menu-projects-to-upgrade.png)

## Avvio del processo di aggiornamento
{: #start_upgrade}

Prima di avviare il processo di aggiornamento, puoi guardarlo in esecuzione in [YouTube![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://youtu.be/oaZVGveVxBg){: new_window}.
[![Link esterno a YouTube](images/migration-video2.png)](https://youtu.be/oaZVGveVxBg){: new_window}    
Per aggiornare il tuo progetto in una toolchain, completa la seguente procedura:

1. Per avviare il processo di aggiornamento, nel messaggio informativo, fai clic su **upgrade now**. Viene aperta la pagina "Project upgrade toolchain". 

   ![Esempio di una pagina di aggiornamento](images/project-upgrade-toolchain.png)

   Per una panoramica sul processo di aggiornamento, leggi la descrizione in questa pagina. In questo caso, poiché il progetto ha utilizzato un repository in GitHub.com, la toolchain sarà collegata allo stesso repository GitHub. La toolchain includerà una nuova pipeline che contiene le stesse fasi e lavori della pipeline del progetto. In aggiunta, la toolchain conterrà un puntatore a Eclipse Orion {{site.data.keyword.webide}} che viene eseguito in {{site.data.keyword.contdelivery_short}}.

2. Per personalizzare la toolchain, puoi configurare alcune impostazioni:

   - Per modificare il nome della toolchain, modifica il campo **Name**.

      ![Campo nome](images/name-change.png)

   - Per modificare in quale organizzazione {{site.data.keyword.Bluemix_notm}} creare la toolchain, seleziona l'organizzazione dal tuo menu dell'account:

      ![Scelta organizzazione Bluemix](images/bluemix-organization-chooser.png)

   Poiché le toolchain sono gestite al livello dell'organizzazione, assicurati di selezionare un'organizzazione quando i membri del progetto necessitano di accedere alla toolchain già esistente o non possono essere aggiunti. 
  
3. Fai clic su **Crea**. La nuova toolchain è stata creata e ne viene visualizzata la pagina della panoramica.

   ![Panoramica della toolchain aggiornata](images/new-toolchain-page.png)

   - Per accedere al tuo repository GitHub o al programma di traccia dei problemi associato, fai clic su **GitHub** o **Issues**.
   
   - Per accedere alla tua pipeline, fai clic su **Delivery Pipeline**.  
   
   - Per accedere a {{site.data.keyword.webide}}, che contiene i contenuti del tuo repository che è stato selezionato nello spazio di lavoro, fai clic su **Eclipse Orion {{site.data.keyword.webide}}**. 

## Rivisitazione del tuo progetto
{: #revisit_projects}

Sei ora pronto ad utilizzare la tua nuova toolchain. Il tuo progetto è ora etichettato come "Aggiornato" e nella pagina della panoramica, viene visualizzato un messaggio di conferma.

![Immagine della scheda del progetto con l'etichetta Aggiornato](images/card-upgraded-project.png)

![Progetto aggiornato](images/banner-upgraded.png)

Puoi visualizzare quali progetti sono stati aggiornati selezionando **Upgraded Projects** dal menu nella pagina dei progetti personali:

![Immagine della voce di menu progetti aggiornati](images/menu-upgraded-projects.png)

Se hai bisogno di annullare l'aggiornamento, elimina la tua toolchain. Quindi, quando ritorni nella pagina della panoramica del progetto, il messaggio di aggiornamento viene nuovamente visualizzato e puoi rieseguire l'aggiornamento quando sei pronto.

## Passi successivi
{: #upgrade_next_steps}   

1. Conferma che l'aggiornamento è stato completato controllando il messaggio nella pagina della panoramica del progetto:    

   ![Progetto aggiornato](images/banner-upgraded.png)    

2. Fornisci ai tuoi membri del team l'accesso alla toolchain.    
    - Ogni membro del team deve avere un account Bluemix valido. I membri del team che non hanno un account valido devono [registrarsi ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/registration){:new_window}.
    - Aggiungi i membri del team all'organizzazione (org) a cui appartiene la toolchain.
3. Utilizza gli strumenti dalla tua toolchain invece degli strumenti dal tuo progetto {{site.data.keyword.jazzhub_short}}. Ad esempio, per modificare il codice da un browser, utilizza la Web IDE dalla tua toolchain.    

## Risoluzione dei problemi 
{: #upgrade_troubleshoot}    

Se hai domande o problemi, invia un'email a [hub@jazz.net](mailto:hub@jazz.net). Nella tua email, includi gli URL al tuo progetto {{site.data.keyword.jazzhub_short}} e alla tua toolchain {{site.data.keyword.contdelivery_short}}.

