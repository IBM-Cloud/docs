---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Gestione dei bundle
{: #globalizationpipeline_workingwithbundles}


Ogni bundle che hai creato contiene la coppia di valore chiave dal tuo file di risorsa e la serie completa di traduzioni che sono state generate.
{:shortdesc}

I file di risorsa caricati possono essere in uno dei seguenti formati e devono avere il contenuto nel formato di coppie chiave/valore che rappresentano le stringhe IU dalla tua applicazione.


* Tipo di file: *File delle proprietà Java™ (.properties)*<br>
Esempio:
```js
logout=Logout 
back=Back 
examples=Menu 
home=Home 
web=Web 
enterprise=Enterprise 
extra=Resources 
about=About 
settings=Settings 
help=Help 
support=Support 
topics=Topics 
appExitMsg=Are you sure you want to quit the application?
```
* Tipo di file: *AMD I18N (.js)*<br>
Esempio:
```js
define({
    "root": {
       logout: "Logout",
       back: "Back",
       examples: "Menu",
       home: "Home",
       web: "Web",
       enterprise: "Enterprise",
       extra: "Resources",
       about: "About",
       settings: "Settings",
       help: "Help",
       support: "Support",
       topics: "Topics",
       appExitMsg: "Are you sure you want to quit the application?"
    }
});
``` 
* Tipo di file: *JSON (.json)*<br>
Esempio:
```js
{
  "logout": "Logout",
  "back": "Back",
  "examples": "Menu",
  "home": "Home",
  "web": "Web",
  "enterprise": "Enterprise",
  "extra": "Resources",
  "about": "About",
  "settings": "Settings",
  "help": "Help",
  "support": "Support",
  "topics": "Topics",
  "appExitMsg": "Are you sure you want to quit the application?"
}
``` 

In aggiunta, un file di risorsa deve anche rispettare queste linee guida:
* Ogni chiave può essere di 255 caratteri massimo.
* Ogni valore può essere di 8191 caratteri massimo.
* Ogni bundle può contenere al massimo 500 coppie chiave / valore.


## Traduzione di un bundle
{: #globalizationpipeline_translatingabundle}

Saranno tradotti solo i file di risorsa caricati. Puoi aggiungere un file di risorsa durante la [creazione di un bundle](index.html#globalizationpipeline_creatingbundles) o la [modifica con i dettagli del bundle](bundles.html#globalizationpipeline_modifyingbundles).

Dopo aver caricato un file di risorsa, puoi tradurne il contenuto in ognuna delle lingue fornite dal motore della machine translation predefinita. Facoltativamente puoi scegliere un motore della machine translation alternativo come descritto nella sezione [Configurazione di Machine translation](managing_translations.html#globalizationpipeline_service_to_service). Il motore predefinito supporta le seguenti lingue di destinazione

<table>
<thead>
<tr>
<th>Lingue di destinazione</th>
</tr>
</thead>
<tbody>
<tr>
<td>Cinese (semplificato)</td>
</tr>
<tr>
<td>Cinese (tradizionale)</td>
</tr>
<tr>
<td>Francese</td>
</tr>
<tr>
<td>Tedesco</td>
</tr>
<tr>
<td>Italiano</td>
</tr>
<tr>
<td>Giapponese</td>
</tr>
<tr>
<td>Coreano</td>
</tr>
<tr>
<td>Portoghese (brasiliano)</td>
</tr>
<tr>
<td>Spagnolo</td>
</tr>
</tbody>
</table>

**Nota:** il motore della machine translation predefinito di {{site.data.keyword.GlobalizationPipeline_short}} fornisce supporto solo per l'inglese come lingua di origine. Tuttavia, i motori della machine translation alternativi disponibili per la configurazione in {{site.data.keyword.GlobalizationPipeline_short}} supportano la traduzione di altre coppie di lingue di origine non in inglese/lingua.

Come hai creato i bundle, saranno aggiunti alla scheda **Bundles** per renderli più facilmente accessibili. Da qui, possono essere eseguite ulteriori attività sulle tue traduzioni.


## Selezionare un bundle da utilizzare
{: #globalizationpipeline_selectingabundle}

1. Fai clic sulla scheda **Bundles** per visualizzare tutti i bundle che hai creato.
2. Fai clic su un **Bundle ID** dall'elenco per visualizzare ulteriori dettagli su tale bundle o fai clic sull'icona **View the bundles detail** ![Seleziona l'icona View the bundles detail per aprire un bundle e lavorare con le sue traduzioni](images/viewProjectDetailIcon.png) nella colonna delle azioni.

![Visualizza tutti i bundle disponibili nella scheda Bundles.](images/translationBundles.png)

Dopo che hai selezionato un bundle da utilizzare, puoi visualizzare lo stato delle relative traduzioni, aggiungere o rimuovere le lingue, modificare le traduzioni o fornire gli aggiornamenti al file di risorsa.

Se non hai più bisogno di un bundle, puoi eliminarlo dalla scheda **Bundles**. Saranno inoltre eliminate tutte le traduzioni associate con il bundle.

## Modifica dei dettagli di un bundle
{: #globalizationpipeline_modifyingbundles}

Quando apri un bundle puoi visualizzarne tutti i dettagli. Sono elencate tutte le lingue di destinazione presenti nel bundle, con lo stato della traduzione corrente di ognuna di esse.

![La pagina dei dettagli del bundle mostra le informazioni su un bundle e le relative traduzioni.](images/bundleDetails.png)

Lo stato di ogni lingua nel bundle può essere In corso, Non riuscito o Tradotto:

| Stato | Descrizione |
|--------|-------------|
| In corso | La machine translation è ancora in corso. |
| Non riuscito | Si è verificato un errore durante la traduzione del file di risorsa nella lingua di destinazione. |
| Tradotto | La traduzione della lingua di destinazione è completa. |

Puoi aggiornare il file di risorsa che utilizza il bundle, aggiungere una lingua di destinazione al bundle, eliminare una lingua di destinazione da un bundle e scaricare le traduzioni generate per una lingua di destinazione.

### Aggiornamento del file di risorsa utilizzato dal bundle.

1. Affianco alla lingua di origine, fai clic sull'icona **Upload resources** ![Seleziona questa icona per caricare un nuovo file di risorsa](images/uploadIcon.png) nella colonna delle azioni.
2. Fai clic su **Browse** e seleziona il nuovo file di risorsa da caricare.
3. Seleziona il tipo di file di risorsa che stai caricando
 * File delle proprietà Java
 * AMD I18N
 * JSON
4. Fai clic su **Update** per caricare il nuovo file di risorsa.

La coppia chiave/valore presente nel nuovo o aggiornato file di risorsa, viene sincronizzata con i valori che erano già stati caricati. Sarà tradotto solo il contenuto nuovo o modificato.

### Aggiunta di una lingua di destinazione a un bundle

1. Fai clic sul pulsante **Add Language**.
2. Vengono visualizzate tutte le lingue di destinazione disponibili. Seleziona le lingue da aggiungere al bundle.

La traduzione delle lingue selezionate inizierà immediatamente.

### Eliminazione di una lingua di destinazione da un bundle

Quando elimini una lingua di destinazione da un bundle, rimuovi la lingua di destinazione e tutte le traduzioni associare dal progetto. Nella colonna delle azioni della lingua di destinazione da rimuovere, fai clic sull'icona **Remove this target language** ![Seleziona l'icona Remove this target language trash can](images/trashIcon.png).

### Scaricamento delle traduzioni generate per una lingua di destinazione.

{{site.data.keyword.GlobalizationPipeline_short}} fornisce varie opzioni per incorporare la traduzione di una una lingua di destinazione nella tua applicazione. Puoi scaricare la traduzione come un file di risorsa e includerlo nella creazione della tua applicazione. Puoi anche fare riferimento alla traduzione dinamica dalla {{site.data.keyword.GlobalizationPipeline_short}} utilizzando uno degli [SDK](https://github.com/IBM-Bluemix/gp-common) open source. 

<!-- For information on {{site.data.keyword.GlobalizationPipeline_full}} SDKs, see <link>. -->

Per scaricare la traduzione come un file di risorsa: 

1. Nella colonna **Azioni** della lingua di origine o di destinazione da scaricare, fai clic sull'icona **Download the translations** ![Seleziona l'icona di scaricamento per scaricare le chiavi di origine e le traduzioni per una lingua di destinazione](images/downloadIcon.png).
2. Seleziona un formato file.
3. Fai clic su **Download**.
