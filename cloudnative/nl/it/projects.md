---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Progetti
{: #projects}

La {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} combina l'interfaccia utente dell'applicazione, i dati e i servizi in un *progetto* completo. Creando un progetto, tutte le parti necessarie della tua applicazione e le funzionalità aggiunte sono conservate nel server {{site.data.keyword.Bluemix_notm}}. Puoi scaricare il tuo codice dell'applicazione e le credenziali e i programmi di inizializzazione necessari se i servizi sono configurati nel tuo progetto. Puoi visualizzare tutti i tuoi progetti selezionando **Progetti**.  

Puoi visualizzare le informazioni aggiuntive su un solo progetto selezionandolo nella pagina **Progetti**. Questa visualizza la pagina **Panoramica del progetto**, che include i servizi che sono configurati e disponibili per il progetto. I servizi sono funzionalità separate che estendono la tua applicazione aggiungendo una funzione. Poiché vengono aggiunte individualmente, puoi aggiungere i servizi di cui hai bisogno, come i servizi push, di autenticazione, dei dati e  di archiviazione o altri servizi. Quando aggiungi un servizio al tuo progetto nella pagina **Panoramica progetto** e segui le istruzioni per configurarlo, viene automaticamente associato alla tua applicazione. Per ulteriori informazioni sulla Pagina progetto, vedi [Pagina Panoramica progetto](project_overview_page.html).

Per creare il tuo progetto, devi selezionare un [modello](patterns.html), seguito da uno [starter](starters.html).


## Pagina Panoramica progetto
{: #project_overview}

Puoi visualizzare e lavorare con un unico progetto {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} selezionandolo dalla pagina **Progetti**, che aprirà la pagina Panoramica progetto.
{: shortdesc}

La pagina **Panoramica progetto** visualizza un tile per ogni funzionalità configurata o disponibile per la configurazione con il progetto selezionato. Il tile visualizza il tipo di funzionalità e un pulsante *azioni* con tre punti allineati verticalmente. Le funzionalità che potrebbero essere disponibili o configurate includono, ad esempio, {{site.data.keyword.mobilepushshort}}, Analytics o Data e Storage. Le funzionalità compatibili dipendono dal tipo di progetto e dalle funzionalità che sono disponibili in quella regione, pertanto non tutte le funzionalità potranno essere associate a ogni progetto.  

Quando un tipo di funzionalità non è ancora associata al progetto, sul tile viene visualizzato un pulsante **Crea**.  Le opzioni del pulsante delle azioni comprendono la creazione di un'istanza del servizio o di aggiungerne una esistente quando la funzionalità non è ancora associata. La selezione di **Aggiungi esistente** fornisce un elenco di istanze del servizio di quel tipo nel tuo spazio. 

Se la funzionalità è già associata a questo progetto, il nome dell'istanza del servizio associato viene visualizzato sul tile dopo il tipo di funzionalità. Questo rende più facile individuare l'istanza del servizio correlata a questo progetto sulla tua {{site.data.keyword.dev_console}}. Se la funzionalità è già associata al progetto, le azioni disponibili sul relativo pulsante sono **Visualizza** e **Rimuovi**. La rimozione di un'istanza del servizio rimuove solo l'associazione a tale progetto e non elimina l'istanza del servizio dalla tua {{site.data.keyword.dev_console}}. Per eliminare un'istanza del servizio, fai clic sulla pagina **Web e mobile > Servizi** per visualizzare ed eliminare le tue istanze del servizio.

Seleziona **Richiama codice** sul tile **Codice** per scaricare il codice per il tuo progetto. Per ulteriori informazioni sul download del codice, vedi [Richiama codice](get_code.html).


## Aggiornamento del tuo progetto per utilizzare un nuovo starter
{: #update-starter}

1. Dalla pagina **Progetti** o **Panoramica progetto**, fai clic sull'icona **Menu overflow** e seleziona **Aggiorna starter**.

2. Scegli un nuovo starter e fai clic su **Aggiorna**.

3. Fai clic su **Richiama codice** nella pagina **Panoramica progetto** per selezionare il tuo linguaggio. 

   In alternativa puoi fare clic sulla pagina **Codice**.


## Aggiornamento del tuo progetto per generare un nuovo linguaggio 
{: #update-language}

1. Dalle pagine **Progetti** o **Panoramica progetto**, fai clic sull'icona **Menu overflow** e seleziona **Aggiorna starter**. 

2. Seleziona un nuovo linguaggio e fai clic su **Aggiorna**.

3. Fai clic su **Richiama codice** nella pagina **Panoramica progetto** per selezionare il tuo linguaggio. 
