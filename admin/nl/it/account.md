---



copyright:

  years: 2015, 2017
lastupdated: "2017-01-09"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestione del tuo account {{site.data.keyword.Bluemix_notm}}
{: #mngacct}

Vai al link **Account** per impostare le notifiche, visualizzare l'utilizzo del tuo account o la tua fattura.
{:shortdesc}

## Registrazione a {{site.data.keyword.Bluemix_notm}}
{: #signup}

Puoi registrarti per un account {{site.data.keyword.Bluemix_notm}} utilizzando un ID IBM esistente, creando un nuovo ID IBM o utilizzando un ID federato. Un ID federato è un ID all'interno di un dominio aziendale che è stato registrato con IBM, in modo che le credenziali di dominio e utente possano essere utilizzate per accedere alle applicazioni Web.  

Un ID federato può essere utilizzato per la registrazione a {{site.data.keyword.Bluemix_notm}} solo se la tua azienda ha già effettuato una registrazione con IBM.  La registrazione di un dominio aziendale con IBM consente agli utenti di accedere a prodotti e servizi IBM utilizzando le proprie credenziali aziendali esistenti. L'autenticazione viene quindi gestita dal provider di identità dell'azienda. Quando accedi a {{site.data.keyword.Bluemix_notm}} con un ID federato, ti viene richiesto di accedere tramite la pagina di accesso della tua azienda. Per informazioni sulla richiesta di registrazione del dominio della tua organizzazione o azienda con IBM o per ulteriori informazioni sul processo, consulta [IBMid Enterprise Federation Adoption Guide ![Icona link esterno](../icons/launch-glyph.svg)](https://ibm.box.com/v/IBMid-Federation-Guide){: new_window}. Quando richiedi di registrare gli ID federati, è necessario uno sponsor IBM, ad esempio un rappresentate di offerte o clienti.

| Metodi di registrazione | Dettagli |    
|-----------------|---------|
|ID IBM esistente | Se già disponi di un ID IBM, registrati a {{site.data.keyword.Bluemix_notm}} con le credenziali esistenti che utilizzi per i prodotti e servizi IBM. Durante la registrazione, ti viene richiesto di immettere un numero di telefono. |
|Nuovo ID IBM | Se non hai ancora un ID IBM, puoi scegliere di crearne uno. L'ID IBM ti consente di utilizzare un unico nome utente di accesso per tutti i prodotti e servizi IBM che vorrai utilizzare, incluso {{site.data.keyword.Bluemix_notm}}. Ti viene richiesto di immettere i tuoi dati personali, tra cui nome e cognome, numero di telefono e password per le nuove credenziali. Puoi utilizzare questo ID IBM per eseguire l'accesso quando utilizzi altri servizi e prodotti IBM.  |
|ID federato | Se la tua azienda ha richiesto di registrare le credenziali utente dal dominio aziendale con IBM, puoi registrarti a {{site.data.keyword.Bluemix_notm}} utilizzando le credenziali che usi già per l'accesso della tua azienda. Durante la registrazione, ti viene richiesto di immettere un numero di telefono. |
{:caption="Table 1. Sign up methods" caption-side="top"}

## Impostazione delle notifiche
{: #notifications}

Fai clic su **Account** &gt; **Notifiche** per impostare l'account generale e le notifiche di spesa. Le notifiche di spesa sono disponibili solo per i proprietari degli account {{site.data.keyword.Bluemix_notm}} Pagamento a consumo e Sottoscrizione.

Puoi impostare le notifiche email della piattaforma per gli incidenti e la manutenzione pianificata {{site.data.keyword.Bluemix_notm}} e puoi impostare le notifiche di spesa per avvisarti quando il tuo account è vicino alla soglia di spesa che hai specificato. Completa le seguenti attività per impostare differenti tipi di notifica per il tuo account.

### Configurazione delle notifiche della piattaforma

Fai clic su **Account** &gt; **Notifiche** &gt; **Piattaforma** per impostare le notifiche e-mail per gli incidenti e la manutenzione pianificata {{site.data.keyword.Bluemix_notm}}. Puoi selezionare o cancellare ogni opzione per abilitare o disabilitare la notifica email.

<!-- staging only

**Note**: You are always alerted by email about emergencies and pricing changes.

On the **Platform** tab you can also customize notifications for your orgs, spaces, or applications. Complete the following steps to add a customized notification:

<ol>
<li>Select **Add a Notification**.</li>
<li>Use the search field to find the org, application, service, or resource that you want to set a notification for, or expand the item in the pre-populated list.</li>
<li>Select *Email* to set the notification type.</li>
</ol>

staging only end -->

### Configurazione delle notifiche di spesa
{: #spendingnotifications}

Se sei il proprietario di un account {{site.data.keyword.Bluemix_notm}} Pagamento a consumo o Sottoscrizione, puoi impostare le notifiche di spesa via email. Imposta le notifiche per la spesa totale di account, runtime, contenitori e servizi, nonché la spesa per singoli servizi, tranne quelli di terze parti. Ricevi le notifiche quando raggiungi l'80%, il 90% e il 100% delle soglie di spesa da te specificate. Puoi modificare ogni notifica di spesa in qualsiasi momento, secondo le tue esigenze.

Completa la seguente procedura per impostare le notifiche via email per i limiti di spesa:

<ol>
<li>Fai clic su **Account** &gt; **Notifiche** &gt; **Spesa**.</li>
<li>Immetti un valore numerico per impostare la soglia di spesa per l'attivazione di una notifica per ciascun tipo di notifica:<br />
<ul>
<li>Totale account</li>
<li>Totale runtime</li>
<li>Totale servizi</li>
<li>Totale contenitore</li>
<li>Spesa per un servizio specifico</li>
</ul>
</li>
<li>Al termine dell'operazione, fai clic su **Salva**.</li>
</ol>

**Nota**: se hai un account di prova, puoi eseguire l'upgrade a un account Sottoscrizione o Pagamento a consumo per impostare i limiti di spesa. Per ulteriori informazioni sugli account Pagamento a consumo e Sottoscrizione, consulta [Modalità di fatturazione](/docs/pricing/index.html#pay-accounts).

## Visualizzazione dell'utilizzo
{: #acctusage}

In qualità di proprietario dell'account o gestore della fatturazione per un'organizzazione, puoi utilizzare la pagina Dashboard di utilizzo per visualizzare gli addebiti in
tempo reale per i runtime, i contenitori, i servizi e il supporto utilizzati al mese nelle tue organizzazioni. Puoi vedere i GB-ora di runtime e il consumo dei servizi in tutte le regioni oppure puoi
selezionare la visualizzazione di una specifica regione.

Per aprire la pagina Dashboard di utilizzo, fai clic su **Account** &gt; *nome_del_tuo_account* &gt; **Dashboard di utilizzo**. I gestori della fatturazione possono visualizzare i dettagli solo per le organizzazioni in cui ricoprono tale ruolo.

Al proprietario dell'account viene addebitato l'utilizzo totale sostenuto su tutte le organizzazioni alla fine di ciascun ciclo di fatturazione. In qualità di proprietario dell'account, puoi filtrare il riepilogo dell'utilizzo in base alla regione e all'organizzazione. Puoi anche fare clic su uno specifico mese per visualizzare il relativo utilizzo. Seleziona **Tutte le organizzazioni** dall'elenco **Organizzazione** per visualizzare l'utilizzo per tutte le organizzazioni nell'account.

## Aggiornamento delle informazioni di fatturazione
{: #account_billing}

In qualità di proprietario dell'account, puoi modificare, aggiungere o rimuovere le informazioni sulla carta di credito salvate che sono associate al tuo account {{site.data.keyword.Bluemix_notm}}. Fai clic su **Account** &gt; *nome_del_tuo_account* &gt; **Fatturazione**.

Se hai un account SoftLayer collegato al tuo account {{site.data.keyword.Bluemix_notm}}, vedi [Fatturazione per l'utilizzo di {{site.data.keyword.Bluemix_notm}} con account collegati](/docs/admin/softlayerlink.html#bill_usage) per ulteriori informazioni sulla fatturazione.
