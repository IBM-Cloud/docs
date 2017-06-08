---



copyright:

  years: 2016, 2017
lastupdated: "2017-03-17"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Passaggio all'ID IBM
L'autenticazione in SoftLayer utilizza adesso un ID IBM per fornire un singolo accesso per tutti i {{site.data.keyword.Bluemix_notm}}. Gli account SoftLayer esistenti verranno abilitati a passare all'autenticazione tramite ID IBM. Una procedura guidata di migrazione ti guiderà in questo passaggio. 
{:shortdesc}

Quando inizi il processo di passaggio a un ID IBM, puoi sempre annullare il passaggio prima di completare il processo. Tuttavia, ogni volta che accedi, viene visualizzato il prompt per passare a un ID IBM. Ogni account SoftLayer che prevedi di collegare a un account {{site.data.keyword.Bluemix_notm}} deve appartenere a un unico ID IBM con un indirizzo e-mail univoco.

Per passare dal tuo account SoftLayer esistente a un ID IBM, completa la seguente procedura:
1. Accedi al tuo account SoftLayer e fai clic su **OK** quando viene visualizzato il prompt per passare a un ID IBM. 

   Se sei un utente master e non visualizzi un prompt per passare a un ID IBM nel {{site.data.keyword.slportal}}, [contatta il supporto IBM](/docs/support/index.html#contacting-support) per assistenza.
  
   Se hai già eseguito l'accesso e hai fatto clic su **Dopo** nel prompt, ma vuoi passare all'autenticazione con l'ID IBM nella sessione corrente, vai alla pagina Modifica profilo utente e fai clic su **Passa a ID IBM**.

2. Segui le istruzioni della procedura guidata per creare il tuo ID IBM. 

   Immetti un indirizzo e-mail che non sia attualmente utilizzato da nessun ID IBM. Questo indirizzo e-mail viene utilizzato come nome utente per il nuovo ID IBM ed è l'indirizzo a cui viene inviato il tuo codice di registrazione una volta che l'ID IBM è stato creato. Puoi aggiornare l'indirizzo e-mail associato all'ID IBM in un secondo momento, ma non puoi modificare il nome utente.

3. Quando ricevi il tuo codice di registrazione, fai clic sul link nell'e-mail o copia l'URL in un browser e immetti il codice di registrazione. 

   Il codice di registrazione è valido per sette giorni e puoi utilizzarlo solo una volta.
  
4. Una volta inoltrato il codice di registrazione, utilizza il tuo ID IBM per accedere al {{site.data.keyword.slportal}}.

   Al prompt di accesso dell'account, vai alla sezione **Accesso account ID IBM** e fai clic su **Accedi con ID IBM**. Non utilizzare i campi **Nome utente** e **Password** che utilizzavi in precedenza con il tuo ID SoftLayer.

Se sei un nuovo cliente, quando controlli il tuo ordine ti verrà chiesto il tuo ID IBM esistente o di creare un nuovo ID IBM. 
  * Per utilizzare un ID IBM esistente, immetti il nome utente o l'indirizzo e-mail dell'ID IBM se è univoco (vale a dire, che non sia condiviso tra più ID IBM).
  
  * Per creare un nuovo ID IBM, immetti un indirizzo e-mail che non sia attualmente utilizzato da nessun ID IBM. Questo indirizzo e-mail è il nome utente per l'ID IBM ed è l'indirizzo a cui viene inviato il tuo codice di registrazione una volta che l'ID IBM è stato creato. Puoi aggiornare l'indirizzo e-mail associato all'ID IBM in un secondo momento, ma non puoi modificare il nome utente. 
  
Per risolvere eventuali problemi con l'accesso con il tuo ID IBM, vedi [Risoluzione dei problemi di accesso a Bluemix](/docs/troubleshoot/ts_accessing.html#accessing).

## Abilitazione degli account utente per l'autenticazione tramite ID IBM
{: #link_accounts_resellers}

In alcuni casi, prima che un utente possa passare a un ID IBM, un rivenditore o un distributore deve abilitare l'account ad utilizzare l'autenticazione tramite ID IBM. 

  * L'autenticazione tramite ID IBM deve essere abilitata per ogni account utente esistente che vuoi collegare a un account Bluemix. Quindi, ogni utente deve completare il processo di passaggio a un ID IBM utilizzando la procedura guidata di migrazione, come descritto nella sezione precedente. Contatta il [supporto IBM](/docs/support/index.html#contacting-support) per abilitare un account SoftLayer esistente all'utilizzo dell'autenticazione tramite ID IBM.  
  
  * Per assicurarti che i nuovi account utente vengano creati con un ID IBM, l'attributo `CREATE_NEW_ACCOUNT_WITH_IBMid_AUTHENTICATION` deve essere impostato sull'account utente master immediato. Contatta il [supporto IBM](/docs/support/index.html#contacting-support) o il tuo fornitore per impostare l'attributo per i tuoi account.  

## Collegamento degli account utente ID IBM
{: #link_user_accounts}

Dopo che i tuoi account utente sono passati all'autenticazione tramite ID IBM, i rivenditori e i distributori possono collegare gli account SoftLayer e {{site.data.keyword.Bluemix_notm}} per utilizzare insieme le risorse dell'infrastruttura e della piattaforma.

**Nota**:
  * L'utente master dell'account che viene collegato deve avere un ID IBM.
  * Ogni account utente che colleghi a un account {{site.data.keyword.Bluemix_notm}} deve appartenere a un unico ID IBM con un indirizzo e-mail univoco. Anche se un singolo ID IBM può possedere più account SoftLayer, devi modificare l'utente master in modo da essere un ID IBM univoco per ogni account. Contatta il [supporto IBM SoftLayer![Icona link esterno](../icons/launch-glyph.svg)](https://knowledgelayer.softlayer.com/topic/support){: new_window} per modificare l'utente master di un account SoftLayer.
  * Quando aggiungi nuovi utenti a un account collegato, devi aggiungerli a entrambi agli account SoftLayer e {{site.data.keyword.Bluemix_notm}} affinché possano accedere a tutte le funzionalità nella console unificata. 
  
Completa la seguente procedura per collegare tutti gli account all'account {{site.data.keyword.Bluemix_notm}}:
1. Per il collegamento a un account {{site.data.keyword.Bluemix_notm}} esistente o per crearne uno nuovo, accedi al tuo account SoftLayer come utente master e fai clic sul link {{site.data.keyword.Bluemix_notm}}.

   L'ID IBM che è l'utente master dell'account SoftLayer deve essere il proprietario dell'account {{site.data.keyword.Bluemix_notm}} a cui ti colleghi. 
   
2. Segui le istruzioni nella procedura guidata, inclusa l'aggiunta di utenti nell'account SoftLayer all'account {{site.data.keyword.Bluemix_notm}}.
3. Dopo aver collegato l'account, informa l'utente finale di ogni account di migrare all'ID IBM utilizzando la procedura descritta nella sezione precedente.

**Raccomandazione**: migra solo gli account dell'utente finale all'ID IBM. Non migrare gli account dell'azienda che sono account principali per gli account utente finale e non contengono alcuna risorsa. Gli utenti degli account dell'azienda che eseguono la migrazione all'ID IBM perdono la possibilità di accedere al portale BAP (Brand Agent Portal).  
  
