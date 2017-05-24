---

copyright:
  years: 2015, 2017
lastupdated: "2017-5-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Aggiorna il tuo progetto {{site.data.keyword.jazzhub_short}} a una toolchain
{: #upgrade_projects}

{{site.data.keyword.jazzhub}} si sta trasformando in {{site.data.keyword.contdelivery_full}}. Come parte di tale cambiamento, i progetti saranno aggiornati in toolchain.

Puoi aggiornare il tuo progetto o attendere che venga aggiornato automaticamente. Per un'esperienza ottimale, assicurati di soddisfare i [prerequisiti](#upgrade_prereqs) e aggiorna il tuo progetto il prima possibile in modo da poter controllare quale sia il nome della tua toolchain e in quale organizzazione viene creata.
{: shortdesc}

## Toolchain
{: #compare_toolchains}

Le toolchain sono simili ai progetti, con alcune importanti differenze:

- I progetti possono avere solo un repository (repo) e una pipeline. Le toolchain possono avere quanti repository e pipeline necessiti.
- Le toolchain possono includere gli strumenti che non sono disponibili nei progetti, come Slack, Sauce Labs, PagerDuty e {{site.data.keyword.DRA_full}}.
- L'accesso alle toolchain è gestito tramite le organizzazioni {{site.data.keyword.Bluemix_notm}} standard. L'appartenenza viene mantenuta al livello dell'organizzazione, in modo diverso dai progetti, in cui l'appartenenza era mantenuta al livello del progetto.

Puoi trovare ulteriori informazioni sulle toolchain in [YouTube![Icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://youtu.be/2SIPE1e7NJ4){: new_window} o da [Introduzione a {{site.data.keyword.contdelivery_short}}](/docs/services/ContinuousDelivery/index.html).
[![Link esterno a YouTube](images/CD_video.png)](https://youtu.be/2SIPE1e7NJ4){: new_window}

## Prerequisiti
{: #upgrade_prereqs}

- Per accedere alla tua toolchain del progetto aggiornata, hai bisogno di un ID {{site.data.keyword.Bluemix_notm}}. Prima di eseguire l'aggiornamento, devi verificare di disporre di un ID {{site.data.keyword.Bluemix_notm}} attivo. Se non ne hai uno, [registrati](https://console.ng.bluemix.net/registration/).
- Assicurati che il tuo proprietario del progetto {{site.data.keyword.jazzhub_short}} sia corretto. La toolchain che viene creata dal tuo progetto farà parte dell'organizzazione {{site.data.keyword.Bluemix_notm}} di tale proprietario.
- Se intendi avviare l'aggiornamento, assicurati di essere membro di ogni organizzazione e spazio a cui distribuisce la pipeline. L'aggiornamento può essere avviato da qualsiasi amministratore del progetto. Tuttavia, se l'amministratore che avvia l'aggiornamento non è un membro di ogni organizzazione e spazio a cui distribuisce la pipeline, la pipeline non può essere creata. La persona che avvia l'aggiornamento diventa il proprietario del repository nella toolchain.
- Eclipse Orion {{site.data.keyword.webide}} nella toolchain è distinto dal {{site.data.keyword.webide}} che è associato al tuo progetto. Se utilizzi {{site.data.keyword.webide}} e hai delle modifiche non eseguite, eseguile prima dell'aggiornamento.


## Aggiornamento da un progetto a una toolchain
{: #project_to_toolchain}

**Importante:** i progetti in hub.jazz.net e le toolchain sono entrambi ospitati nella regione Stati Uniti Sud. Se il tuo progetto è stato configurato per distribuire le applicazioni in una regione differente, le distribuirà comunque a tale regione dopo essere stato aggiornato a una toolchain. 

Quando il tuo progetto è pronto per essere aggiornato, viene visualizzato un messaggio nella scheda del progetto e nella pagina della panoramica.

![Immagine della scheda con l'etichetta pronto per l'aggiornamento](images/card-project-to-upgrade.png)

![Ora del messaggio pronto per l'aggiornamento](images/banner-ready-to-upgrade.png)

**Suggerimento:** puoi trovare i progetti che sono pronti per l'aggiornamento dal menu nella pagina dei progetti personali:

![Immagine della voce del menu progetti per l'aggiornamento](images/menu-projects-to-upgrade.png)

Quando avvii l'aggiornamento, le fasi della pipeline nel tuo progetto vengono bloccate. Non potrai eseguirle o modificarle. Se ripristini l'aggiornamento eliminando la toolchain, la pipeline viene sbloccata.

Se il tuo progetto utilizza un repository Git ospitato su JazzHub, una volta avviato l'aggiornamento, il repository viene bloccato per garantire l'integrità dei dati che vengono spostati nella toolchain. Se ripristini l'aggiornamento eliminando la toolchain, il repository su JazzHub viene sbloccato.

## Avvio del processo di aggiornamento
{: #start_upgrade}

Prima di avviare il processo di aggiornamento, puoi guardarlo in esecuzione in [YouTube![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://youtu.be/LSr2e3uvyLs){: new_window}.
[![Link esterno a YouTube](images/migration-video2.png)](https://youtu.be/LSr2e3uvyLs){: new_window}

Per aggiornare il tuo progetto in una toolchain, completa la seguente procedura:

1. Per avviare il processo di aggiornamento, nel messaggio informativo, fai clic su **upgrade now**. Viene aperta la pagina "Project upgrade toolchain".

   ![Esempio di una pagina di aggiornamento](images/project-upgrade-toolchain.png)

   Per una panoramica sul processo di aggiornamento, leggi la descrizione in questa pagina. La toolchain includerà una nuova pipeline che contiene le stesse fasi e lavori della pipeline del progetto. In aggiunta, la toolchain conterrà un puntatore a Eclipse Orion {{site.data.keyword.webide}} che viene eseguito in {{site.data.keyword.contdelivery_short}}.

   In questo esempio, poiché il progetto utilizza un repository pubblico su github.com, la toolchain sarà collegata allo stesso repository GitHub. Se il tuo progetto utilizza un repository Git ospitato su JazzHub, il contenuto di tale repository sarà clonato in un nuovo repository in {{site.data.keyword.gitrepos}}, che fa parte di {{site.data.keyword.contdelivery_short}}. Per informazioni dettagliate su come viene trattato ogni tipo di repository, vedi la seguente tabella.

|Repository del progetto |Tipo di progetto	|Repository della toolchain |
|:----------|:------------------------------|:------------------|
|github.com 		|Privato o pubblico 		|Lo stesso repository github.com con {{site.data.keyword.Bluemix_notm}} pubblico.	|
|hub.jazz.net/git		|Privato o pubblico 		|Un nuovo repository in {{site.data.keyword.gitrepos}} con {{site.data.keyword.Bluemix_notm}} pubblico.	|
{: caption="Tabella 1. Repository del progetto associati ai repository della toolchain" caption-side="top"}

2. Per personalizzare la toolchain, puoi configurare alcune impostazioni:

   - Per modificare il nome della toolchain, modifica il campo **Name**.

      ![Campo nome](images/name-change.png)

   - Per modificare in quale organizzazione {{site.data.keyword.Bluemix_notm}} creare la toolchain, seleziona l'organizzazione dal tuo menu dell'account:

      ![Scelta organizzazione Bluemix](images/bluemix-organization-chooser.png)

   Poiché le toolchain sono gestite al livello dell'organizzazione, assicurati di selezionare un'organizzazione quando i membri del progetto necessitano di accedere alla toolchain già esistente o non possono essere aggiunti.

3. Se nel tuo progetto hai utilizzato Track & Plan, puoi trasferire i tuoi dati Track & Plan a Problemi GitHub.

   ![Opzioni di Track and Plan](images/upgrade-tutorial-track-and-plan.png)

   - Indica se vuoi migrare i tuoi dati Track & Plan.
   - Per impostazione predefinita, tutti i tuoi dati Track & Plan vengono migrati. Se preferisci migrare solo gli elementi di lavoro che fanno parte di una determinata query, specifica tale query.
   - Seleziona qualsiasi attributo di elemento di lavoro che vuoi associare alle etichette in Problemi GitHub.

4. Fai clic su **Crea**. La nuova toolchain è stata creata e ne viene visualizzata la pagina della panoramica.

   ![Panoramica della toolchain aggiornata](images/new-toolchain-page.png)

   - Per accedere al tuo repository GitHub o al programma di traccia dei problemi associato, fai clic su **GitHub** o **Issues**.
   - Per accedere alla tua pipeline, fai clic su **Delivery Pipeline**.
   - Per accedere a {{site.data.keyword.webide}}, che contiene i contenuti del tuo repository che sono stati selezionati nello spazio di lavoro, fai clic su **Eclipse Orion {{site.data.keyword.webide}}**.

   Se ritorni al tuo progetto durante l'aggiornamento, il messaggio del banner potrebbe indicare che l'aggiornamento è in corso, soprattutto se il processo di aggiornamento prevede l'importazione del codice sorgente a un nuovo repository o l'importazione degli elementi di lavoro Track &amp; Plan come problemi.

   ![Messaggio sul progetto che viene aggiornato a un toolchain](images/project-being-upgraded-banner.png)

## Rivisitazione del tuo progetto
{: #revisit_projects}

Sei ora pronto ad utilizzare la tua nuova toolchain. Il tuo progetto è ora etichettato come "Aggiornato" e nella pagina della panoramica, viene visualizzato un messaggio di conferma.

![Immagine della scheda del progetto con l'etichetta Aggiornato](images/card-upgraded-project.png)

![Progetto aggiornato](images/banner-upgraded.png)

Puoi visualizzare quali progetti sono stati aggiornati selezionando **Upgraded Projects** dal menu nella pagina dei progetti personali:

![Immagine della voce di menu progetti aggiornati](images/menu-upgraded-projects.png)

Se hai bisogno di annullare l'aggiornamento, elimina la tua toolchain. Puoi eliminare la toolchain dal menu **More Actions** nella pagina della panoramica della toolchain:

![immagine dell'azione Delete nel menu More Actions](images/upgrade-tutorial-delete-toolchain.png)

Quando ritorni al tuo progetto, il messaggio di aggiornamento viene nuovamente visualizzato e puoi rieseguire l'aggiornamento quando sei pronto.

## Passi successivi
{: #upgrade_next_steps}

1. Conferma che l'aggiornamento è stato completato aggiornando il tuo browser e controllando che il messaggio nella pagina della panoramica del progetto indichi che il progetto è stato aggiornato a questa toolchain:

   ![Messaggio nel banner che indica che il progetto è stato aggiornato](images/banner-upgraded.png)

   **Nota:** se il messaggio indica "upgrade now," l'aggiornamento non è riuscito. Fai clic sul link **upgrade now** per riprovare.

   ![Messaggio nel banner che indica che il progetto è pronto per l'aggiornamento](images/banner-ready-to-upgrade.png)

2. Fornisci ai tuoi membri del team l'accesso alla toolchain.
    - Ogni membro del team deve avere un account {{site.data.keyword.Bluemix_notm}} valido. I membri del team che non hanno un account valido devono [registrarsi ![Icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/registration){:new_window}.
    - Concedi l'accesso alla toolchain ai membri dell'organizzazione dalla pagina di gestione della toolchain. Per ulteriori informazioni sul controllo dell'accesso alle toolchain, consulta [Gestione dell'accesso ![icona link esterno](../../icons/launch-glyph.svg "External link icon")](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){:new_window}.
    - Se un utente non è un membro dell'organizzazione a cui appartiene la toolchain, aggiungilo all'organizzazione utilizzando la pagina Gestisci organizzazioni.
      Per ulteriori informazioni sulla gestione delle organizzazioni, consulta [Gestione di organizzazioni e spazi ![icona link esterno](../../icons/launch-glyph.svg "External link icon")](/docs/admin/orgs_spaces.html#orgsspacesusers){:new_window}.

3. Utilizza gli strumenti dalla tua toolchain invece degli strumenti dal tuo progetto {{site.data.keyword.jazzhub_short}}. Ad esempio, per modificare il codice da un browser, utilizza la Web IDE dalla tua toolchain.

4. Se stai utilizzando {{site.data.keyword.gitrepos}}, effettua l'autenticazione utilizzando il token di accesso personale o una chiave SSH. Per ulteriori informazioni sulle chiavi SSH, vedi [Creazione di un token di accesso personale o di una chiave SSH per l'autenticazione](/docs/services/ContinuousDelivery/git_working.html#git_authentication). Per effettuare l'autenticazione da un client Git esterno tramite https, segui questa procedura:
    1. Vai alla pagina [Access Tokens ![icona link esterno ](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/profile/personal_access_tokens){:new_window} delle tue impostazioni utente {{site.data.keyword.gitrepos}}.
    2. Crea un token di accesso personale che utilizzi come ambito **api**.
    3. Vai alla pagina [Account ![icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/profile/account){:new_window} e cerca il tuo nome utente per {{site.data.keyword.gitrepos}}. Il tuo nome utente è elencato nella sezione "Change username" e viene mostrato come prima parte dell'URL per ogni repository personale che crei.
    4. Per effettuare l'autenticazione con {{site.data.keyword.gitrepos}} da un client Git esterno tramite https, utilizza il tuo nome utente e il token di accesso personale.
    5. Se vuoi riutilizzare il repository locale del tuo repository Git JazzHub, punta il repository al nuovo repository in {{site.data.keyword.gitrepos}}. Da una shell in un terminale, passa alla directory in cui viene clonato il repository Git JazzHub Git. Immetti il comando `git remote set-url`: `git remote set-url origin https://git.ng.bluemix.net/<userid>/<name-of-new-repo>`

        **Suggerimento:** per controllare su quali nomi remoti sono impostati determinati URL remoti, utilizza il comando `git remote -v`. Il nome remoto predefinito è `origin`. Se hai una configurazione più avanzata, la forma del comando è la seguente: `git remote set-url <remote-name-that-uses-jazzhub-repo> https://git.ng.bluemix.net/<userid>/<name-of-new-repo>`

5. Una volta che la tua toolchain è configurata e hai iniziato a utilizzarla, valuta la possibilità di effettuare tutti o una parte dei seguenti passi per garantire che nessuno utilizzi il tuo progetto:
    - Aggiungi un suffisso al nome del tuo progetto per indicare che non deve essere utilizzato. Potresti aggiungere `_DO_NOT_USE` alla fine del nome progetto.
    - Aggiorna la descrizione del progetto per indicare che non è più utilizzato e aggiungi un puntatore alla toolchain. 
    - Rimuovi i membri dal progetto.
    - Elimina il progetto quando non ti serve più.

6. Facoltativo: per esplorare la maturità di sviluppo del progetto, le procedure del tuo team e la qualità del tuo codice di base, aggiungi IBM Cloud {{site.data.keyword.DRA_short}} alla toolchain. {{site.data.keyword.DRA_short}} applica le analisi di sviluppatori, dei team e di distribuzione ai progetti DevOps. Per ulteriori informazioni, vedi [Introduzione a {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).


## Risoluzione dei problemi
{: #upgrade_troubleshoot}

Se hai domande o problemi, vai al [forum di supporto](https://developer.ibm.com/answers/questions/ask/?smartspace=devops-services). Nel post del forum, includi gli URL al tuo progetto {{site.data.keyword.jazzhub_short}} e alla tua toolchain {{site.data.keyword.contdelivery_short}} e contrassegna il post con la tag `devops-services`.
