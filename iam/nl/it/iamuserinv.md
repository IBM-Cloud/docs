---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-17"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Invito di utenti
{: #iamuserinv}

Puoi invitare gli utenti con le applicazioni, i servizi {{site.data.keyword.Bluemix_notm}} e l'infrastruttura {{site.data.keyword.Bluemix_notm}} da una sola ubicazione. Per invitare gli utenti e gestire gli inviti in sospeso, devi essere un proprietario dell'account, un gestore dell'organizzazione o devi avere la autorizzazioni dell'infrastruttura per aggiungere gli utenti. Puoi invitare gli utenti, annullare gli inviti e reinviare un invito in sospeso a un utente invitato. Puoi invitare un solo utente o, se stai fornendo lo stesso accesso a tutti i membri in un gruppo di utenti, puoi invitare più utenti contemporaneamente.
{:shortdesc}

Per invitare gli utenti o per gestire gli inviti utente nel tuo account, completa la seguente procedura:

1. Dalla barra dei menu, fai clic su **Gestisci** &gt; **Sicurezza** &gt; **Identità e accesso** &gt; **Utenti**.La finestra Utenti visualizza un elenco di utenti con i rispettivi indirizzi email e stato corrente negli account che gestisci. 
2. Fai clic su **Invita utenti**. 
3. Specifica l'indirizzo e-mail o l'ID IBM dell'utente. Se stai fornendo a più utenti lo stesso accesso, puoi selezionare **Invita più utenti** per immettere un elenco di utenti da invitare. Separa la voci ID utente con le virgole. 
4. Aggiungi una o più delle opzioni di accesso che gestisci. Devi assegnare almeno un'opzione di accesso e configurare le impostazioni per l'utente in ogni opzione di accesso che assegni. Per tutte le ulteriori opzioni di accesso che non aggiungi e configuri, viene assegnato il valore predefinito *nessun accesso*. Potresti visualizzare una o tutte le seguenti opzioni di accesso, a seconda delle opzioni che sei autorizzato a gestire: **Servizi abilitati per l'accesso e l'identità**, **Accesso Cloud Foundry**, **Accesso infrastruttura**. Per ulteriori informazioni, vedi [Assegnazione dell'accesso utente](/docs/iam/assignaccess.html).

Se determini che un utente non ha bisogno dell'accesso, puoi annullare un invito per tutti gli utenti visualizzati in uno stato **Elaborazione** o **In sospeso** nella colonna **Stato**. Se un utente invitato non riceve un invito, puoi reinviare l'invito a tutti gli utenti nello stato **In sospeso**.
