---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Gestione delle traduzioni
{: #globalizationpipeline_managingtranslations}


Dopo aver creato i bundle e avviato la generazione delle traduzioni per la tua applicazione, il contenuto generato della machine può essere utilizzato così come è oppure modificato ulteriormente. Puoi inoltre scegliere di utilizzare una machine translation differente dalla predefinita. Questa sezione descrive come modificare il motore della machine translation che esegue le traduzioni per i bundle, come eseguire una modifica post traduzione umana e anche come puoi assegnare i ruoli utente e le restrizioni di accesso alle persone che avranno bisogno di accedere alle tue traduzioni.
{:shortdesc}

## Configurazione della machine translation
{: #globalizationpipeline_service_to_service}

{{site.data.keyword.GlobalizationPipeline_full}} supporta la capacità di integrare servizi machine translation alternativi per eseguire la machine translation dei tuoi bundle. L'aggiunta di un servizio alternativo può essere utile se il motore predefinito utilizzato dalla {{site.data.keyword.GlobalizationPipeline_short}} non offre una lingua specifica di cui hai bisogno o se preferisci le machine translation generate da un motore differente. L'utilizzo e gli addebiti dei servizi alternativi sono inclusi nei termini di tali servizi.

Per aggiungere e configurare un servizio machine translation alternativo per {{site.data.keyword.GlobalizationPipeline_short}}, seleziona la scheda **Machine Translation Configuration** dal dashboard {{site.data.keyword.GlobalizationPipeline_short}}.

* Per aggiungere un servizio machine translation nel catalogo {{site.data.keyword.Bluemix_notm}}, (**Watson Language Translator**), il servizio deve prima essere aggiunto nello spazio {{site.data.keyword.Bluemix_notm}}.

* Per aggiungere un servizio di terze parti, seleziona il pulsante per tale servizio nella scheda **Machine Translation Configuration** e fornisci le credenziali utente necessarie per accedere al servizio.

Dopo aver aggiunto un servizio machine translation a {{site.data.keyword.GlobalizationPipeline_short}}, segui i rimanenti passi per completare l'integrazione di tale servizio.

1. Fai clic su **Enable** per abilitare l'integrazione con tale servizio.

2. Fai clic su **Update Languages** per visualizzare un elenco aggiornato di lingue di destinazione supportate.

3. Dall'elenco delle lingue di destinazione, seleziona il motore della machine translation per la quale eseguire la traduzione.

4. Fai clic su **Save** per ritornare alla scheda **Machine Translation Configuration**.

Dopo aver configurato un servizio alternativo con {{site.data.keyword.GlobalizationPipeline_short}}, tutte le lingue che sono state assegnate a tale motore inizieranno ad essere generate utilizzando quel motore. 

Per arrestare l'utilizzo di un motore della machine translation alternativo:

1. Dalla scheda **Machine Translation Configuration**, fai clic sul pulsante **Disable** per il servizio per cui vuoi arrestare l'utilizzo.

Quando un servizio machine translation alternativo è disabilitato, tutte le traduzioni generate dal servizio rimarranno nel tuo bundle. Tuttavia, la traduzione in una lingua di destinazione particolare, può non essere disponibile per gli aggiornamenti futuri se la lingua di destinazione non è più supportata dal motore della machine translation che è al momento abilitato.

<!-- Review comment: When you disable an engine, do you need to go back and reconfigure the languages?? Does it go back to the default engine? What happens? -->

## Visualizzazione e modifica delle traduzioni
{: #globalizationpipeline_translations}

Il servizio {{site.data.keyword.GlobalizationPipeline_short}} fornisce le funzionalità di modifica di post traduzione umana. Un traduttore professionista o qualcuno esperto nelle lingue di destinazione può apportare modifiche alle traduzioni generate. Puoi eseguire modifiche per migliorare la qualità o la consistenza della traduzione o per sostituire una formulazione preferita. Ad esempio, potresti desiderare di sovrascrivere la traduzione di un nome prodotto.

Per visualizzare e modificare le traduzioni per la lingua di destinazione:

1. Dalla pagina **Bundle details**, seleziona una lingua di destinazione o fai clic sull'icona **View the translations** ![Seleziona l'icona view translations per visualizzare le traduzioni di una lingua di destinazione](images/viewProjectDetailIcon.png) dalla colonna delle azioni.
2. Le traduzioni sono presentate in una tabella che mostra la chiave, l'origine e le informazioni di traduzione.
 * **Chiave:** Rappresenta un attributo nel file di risorsa che dispone di un valore associato.
 * **Origine:** Rappresenta una stringa traducibile inclusa nel file di risorsa caricato.
 * **Traduzione:** Rappresenta la versione tradotta del valore di origine.
3. Nella colonna delle azioni, fai clic sull'icona **Modify the translation** ![Seleziona l'icona Modify the translation per modificare le traduzioni di una coppia chiave/valore particolare.](images/editIcon.png) per modificare un valore machine-translated.
4. Modifica la traduzione e fai clic su **Update** per aggiornare il valore tradotto originale con quello da te modificato.

![La finestra di dialogo di modifica della traduzione fornisce un modo semplice di modificare le traduzioni.](images/editTranslation.png) 

***Suggerimento:*** quando utilizzi bundle molto grandi che includono molte chiavi traducibili, la ricerca di un valore particolare può essere difficile. Nella pagina di traduzione della lingua di destinazione, puoi velocemente ricerca le chiavi, l'origine e le traduzioni utilizzando la casella **Search for...**.

![Utilizza la casella di ricerca fornita nella pagina di traduzione della lingua di destinazione per ricercare le chiavi, l'origine, le traduzioni o tutti e tre nella lingua di destinazione.](images/search.png) 


## Aggiunta di utenti API
{: #globalizationpipeline_users}

Così come gestisci le tue traduzioni, potresti desiderare di fornire l'accesso a ulteriori utenti API in base alle attività che hanno bisogno di eseguire. Ad esempio, puoi voler abilitare un traduttore a modificare la traduzione, ma non a modificare le informazioni del bundle.

| Tipo di ruolo | Visualizza la traduzioni? | Modifica le traduzioni? | Modifica le informazioni del bundle? |
|-----------|--------------------|--------------------|----------------------------|
| Lettore | Sì | No | No |
| Traduttore | Sì | Sì | No |
| Amministratore | Sì | Sì | Sì |

Se crei più utenti API, puoi limitare il loro accessi a uno o più bundle o fornire loro l'accesso a tutti i bundle disponibili.

Per fornire l'accesso a un utente API a un bundle in un'istanza del servizio {{site.data.keyword.GlobalizationPipeline_short}}:

1. Nel dashboard {{site.data.keyword.GlobalizationPipeline_short}}, fai clic sulla scheda ** API Users**.
2. Fai clic su **New API User**.
3. Immetti un **nome di visualizzazione** e un **commento** per descrivere il nuovo utente API.
4. Scegli un **tipo** per il nuovo utente API.
5. Scegli di fornire l'accesso all'utente API a tutti i bundle o solo ai bundle selezionati.
6. Fai clic su **Save**.

![Completa il forum per creare un nuovo utente API.](images/newUser.png)

Vengono generati e visualizzati un ID utente e una password. Copia e salva queste credenziali; dopo che hai chiuso la finestra non puoi accedere nuovamente ad esse. Le credenziali possono essere utilizzate per il servizio RESTful tramite [SDK](https://github.com/IBM-Bluemix/gp-common). 

Per reimpostare la password dell'utente API:

1. Nel dashboard {{site.data.keyword.GlobalizationPipeline_short}}, fai clic sulla scheda ** API Users**.
2. Fai clic sull'icona **Reset Password** ![Seleziona questa icona per reimpostare la password degli utenti API](images/resetPW.png) per reimpostare la password per un ID utente specifico. 
3. Fai clic su **Yes**. 
