---

copyright:

  years: 2015, 2017
lastupdated: "2017-04-11"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestione di organizzazioni
In qualità di proprietario dell'account o di gestore dell'organizzazione, puoi eseguire attività di gestione dell'organizzazione, che includono la rinominazione dell'organizzazione, l'eliminazione di un'organizzazione o uno spazio, l'aggiornamento dei ruoli e la gestione della quota e dei domini.
{:shortdesc}

Per gestire le tue organizzazioni, dalla barra dei menu della console, fai clic su **Gestisci > Account > Organizzazioni**. 

**Nota:** puoi visualizzare le risorse di una sola organizzazione alla volta. Se sei membro di più organizzazioni, puoi passare da un'organizzazione all'altra utilizzando il link delle preferenze dell'account utente nella barra dei menu della console.

## Rinominazione di organizzazioni
{: #orgrename}

Per rinominare la tua organizzazione, completa la seguente procedura:
1. Fai clic su **Gestione** > **Account** > **Organizzazioni**.
2. Identifica l'organizzazione che vuoi rinominare e fai clic su **Visualizza dettagli**.
3. Fai clic su **Modifica organizzazione**.
4. Fai clic su **Modifica** accanto al nome dell'organizzazione.
5. Immetti il nuovo nome per l'organizzazione e fai clic su **Salva**.

## Eliminazione di organizzazioni e spazi
{: #deleteorgs}

In qualità di proprietario dell'account, contatta il [Supporto {{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} per eliminare un'organizzazione.

**Nota**: le operazioni di eliminazione sono irreversibili. Perdi tutte le applicazioni e tutti i servizi associati all'organizzazione.

Completa la seguente procedura per eliminare un'organizzazione o uno spazio:
1. Fai clic su **Gestione** > **Account** > **Organizzazioni**.
2. Identifica l'organizzazione che vuoi modificare e fai clic su **Visualizza dettagli**.
3. Identifica lo spazio che vuoi eliminare e fai clic su **Modifica spazio**.
4. Fai clic su **Modifica spazio**.

## Modifica dei ruoli utente
{: #listmembers}

Completa la seguente procedura per modificare i ruoli degli utenti per una specifica organizzazione:
1. Fai clic su **Gestione** &gt; **Account** &gt; **Organizzazioni**.
2. Identifica l'organizzazione per cui vuoi visualizzare i membri e fai clic su **Visualizza dettagli**.
3. Fai clic su **Modifica organizzazione**.
4. Puoi visualizzare i membri della tua organizzazione e i loro ruoli nella scheda **UTENTI**.

Completa la seguente procedura per modificare i ruoli degli utenti per uno specifico spazio:
1. Fai clic su **Gestione** &gt; **Account** &gt; **Organizzazioni**.
2. Identifica l'organizzazione per cui vuoi visualizzare i membri e fai clic su **Visualizza dettagli**.
3. Identifica lo spazio per cui vuoi visualizzare i membri e fai clic su **Modifica spazio**.
4. Puoi visualizzare i membri del tuo spazio e i loro ruoli nella scheda **UTENTI**.

## Gestione della quota
{: #managequota}

In qualità di proprietario dell'account o di gestore dell'organizzazione {{site.data.keyword.Bluemix_notm}}, puoi visualizzare la quota utilizzata e assegnata per un'organizzazione. La quota rappresenta i limiti di risorse per l'organizzazione, che viene assegnata quando l'organizzazione viene creata. A seconda che si disponga di un account di prova o di un account fatturabile, le risorse disponibili per un'organizzazione sono diverse. Applicazioni o servizi in uno spazio all'interno dell'organizzazione contribuiscono tutti all'utilizzo della quota assegnata.

Per visualizzare la quota utilizzata e assegnata per un'organizzazione, completa la seguente procedura:
1. Fai clic su **Gestione** &gt; **Account** &gt; **Organizzazioni**.
2. Identifica l'organizzazione per cui vuoi visualizzare la quota e fai clic su **Visualizza dettagli**.
3. Fai clic su **Modifica organizzazione**.
4. Se hai degli spazi definiti in più di un'organizzazione, seleziona la specifica regione che vuoi visualizzare.
5. Fai clic su **QUOTA**. 
6. Per impostazione predefinita, si apre la pagina della quota **Cloud Foundry**. Puoi visualizzare i dettagli della quota per le seguenti risorse:
 * MEMORIA
 * SERVIZI
 * PIANO
 * PREZZO
7. Fai clic su **Contenitori** per visualizzare l'assegnazione della quota utilizzate e disponibile per i contenitori. L'assegnazione del contenitore varia a seconda del piano prezzi. Puoi visualizzare i dettagli della quota per le seguenti risorse:
 * MEMORIA
 * IP PUBBLICO
 * CONDIVISIONI FILE
8. Fai clic su **Server virtuali** per visualizzare le macchine virtuali.

**Nota:** i contenitori non sono disponibili nella regione {{site.data.keyword.Bluemix_notm}} Sydney. 

Per ulteriori informazioni sui contenitori, vedi [Quota](/docs/containers/container_planning.html#container_planning_quota) nella documentazione dei contenitori.
Per modificare la quota assegnata a un'organizzazione, devi aprire un ticket di supporto. Per ulteriori informazioni sull'apertura di un ticket di supporto, vedi [Richiesta di assistenza clienti](/docs/support/index.html#contacting-support). 

## Gestione dei domini
{: #managedomains}

In qualità di proprietario dell'account o di gestore dell'organizzazione, puoi visualizzare il dominio di sistema e aggiungere domini personalizzati per le applicazioni create all'interno di un'organizzazione e dei relativi spazi. In qualità di gestore spazio, la scheda **Domini** per uno spazio è un elenco di sola lettura dei domini assegnati allo spazio.

1. Fai clic su **Gestione** &gt; **Account** &gt; **Organizzazioni**.
2. Identifica l'organizzazione per cui vuoi visualizzare o modificare i domini.
3. Seleziona **Visualizza dettagli** per tale organizzazione.
4. Fai clic su **Modifica organizzazione**.
5. Fai clic su **DOMINI**.

Se aggiungi un dominio personalizzato, devi configurare il server DNS per far sì che il tuo dominio personalizzato punti al dominio di sistema {{site.data.keyword.Bluemix_notm}}. In questo modo, quando {{site.data.keyword.Bluemix_notm}} riceve una richiesta per il tuo dominio personalizzato, può correttamente instradarla alla tua applicazione. Il dominio di sistema è sempre disponibile per uno spazio e a uno spazio è anche possibile assegnare dei domini personalizzati. Le applicazioni create in uno spazio possono utilizzare qualsiasi dominio elencato per quello spazio. Per ulteriori informazioni sulla creazione e l'utilizzo dei domini personalizzati, consulta [Utilizzo di un dominio personalizzato](/docs/manageapps/updapps.html#domain).
