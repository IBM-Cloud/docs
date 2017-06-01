---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_wind{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:download: .download}
{:tip: .tip}

# Introduzione 
{: #natural-language-classifier}

Il servizio {{site.data.keyword.nlclassifierfull}} può aiutare la tua applicazione a comprendere la lingua di brevi testi e fare delle previsioni su come gestirli. Un classificatore fornisce informazioni sui dati di esempio e può restituire le informazioni per i testi su cui non è preparato.
{:shortdesc}

Puoi creare e preparare un {{site.data.keyword.nlclassifiershort}} in meno di 15 minuti.

## Passo 1: accedi, crea il servizio e ottieni le tue credenziali

Se già conosci le tue credenziali per la tua istanza del servizio {{site.data.keyword.nlclassifiershort}}, salta questo passo.
{: tip}

1.  Passa al servizio [{{site.data.keyword.nlclassifiershort}}](https://console.{DomainName}/catalog/services/natural-language-classifier/) e registrati per un account gratuito o accedi al tuo account {{site.data.keyword.Bluemix_notm}}.
1.  Dopo aver eseguito l'accesso, nella pagina {{site.data.keyword.nlclassifiershort}} digita `Classifier-tutorial` nel campo **Service name** per identificare questa istanza del servizio e fai clic su **Create**.
1.  Copia le tue credenziali:
    1.  Fai clic su **Service Credentials**. 
    2.  Fai clic su **View Credentials** nella sezione "Service Credentials".
    3.  Copia i valori `username` e `password`.

## Passo 2: crea e prepara un classificatore
Il classificatore apprende dagli esempi prima di poter restituire informazioni per testi che non aveva visto precedentemente. I dati
di esempio sono indicati come "dati di formazione". Carichi i dati di formazione quando crei un classificatore.

1.  Scarica l'esempio <code><a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a></code>. Questi sono gli stessi dati di formazione utilizzati nella demo [ ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://natural-language-classifier-demo.mybluemix.net){:new_window}.

	Il file è in un formato CSV in due colonne. La prima colonna è l'input di testo. La seconda colonna è la classe per tale testo: temperatura o condizione. Visualizza il file per vedere le voci.
2.  Immetti il seguente comando curl per richiamare il metodo `POST /classifiers/`, che carica i dati di formazione e crea il classificatore:
    -   Sostituisci `{username}` e `{password}` con le credenziali del servizio copiate nel passo precedente.
    -   Modifica l'ubicazione dei dati di formazione in modo che punti dove hai salvato il file `weather_data_train.csv`.

	```bash
	curl -i -u "{username}":"{password}" -F training_data=@{path_to_file}/weather_data_train.csv -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers"
	```
	{: pre}

	La risposta include un nuovo stato e ID del classificatore. Ad esempio: 

	```
	{
	  "name": "TutorialClassifier",
	  "language": "en",
	  "status": "Training",
	  "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/10D41B-nlc-1",
	  "classifier_id": "10D41B-nlc-1",
	  "created": "2015-05-28T18:01:57.393Z",
	  "status_description": "The classifier instance is in its training phase, not yet ready to accept classify requests"
	}
	```
	{: screen}

	La preparazione inizia immediatamente e deve finire prima di poter eseguire la query del classificatore.
3.  Controlla lo stato di preparazione periodicamente finché visualizzi lo stato `Available`. Con questi dati di esempio, la preparazione dura circa 6 minuti:
	- Immetti una chiamata `GET /classifiers/{classifier_id}` per richiamare lo stato del classificatore. Nel seguente esempio, sostituisci `{username}`, `{password}` e `{classifier_id}` con le tue informazioni:

		```bash
		curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
		```
		{: pre}

## Passo 3: classifica il testo
Ora che il classificatore è stato preparato, puoi eseguirne la query.

1.  Classifica alcune domande correlate al meteo per controllare come risponde il tuo classificatore preparato più recentemente. Questa è una chiamata di esempio. Sostituisci `{username}`, `{password}` e `{classifier_id}` con le tue informazioni:

	```bash
	curl -G -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}/classify" --data-urlencode "text=How hot will it be today?"
	```
	{: pre}

	L'API restituisce una risposta che include il nome della classe con cui il classificatore ha la confidenza più elevata. Altre coppie di confidenza-classe sono elencate in ordine di confidenza:

	```
	{
	  "classifier_id": "10D41B-nlc-1",
	  "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1",
	  "text": "How hot will it be today?",
	  "top_class": "temperature",
	  "classes": [
	    {
	      "class_name": "temperature",
	      "confidence": 0.9998201258549781
	    },
	    {
	      "class_name": "conditions",
	      "confidence": 0.00017987414502176904
	    }
	  ]
	}
	```
	{: screen}

	Il valore della confidenza rappresenta una percentuale e il valore più alto rappresenta la confidenza più alta. La risposta include fino a 10 classi.

	Se hai meno di 10 classi nei tuoi dati di formazione, il totale di tutti i valori di confidenza è 100%. In questi dati di formazione di esempio, sono definite solo due classi, per cui ne possono essere restituite solo due.
2.  Verifica la classe più il alto per le domande per visualizzare come il classificatore le sta prevedendo.

	Queste sono alcune domande di esempio da classificare:

	-   Fa caldo fuori?
	-   Sarà ventoso?
	-   Si avrà il sole?
	-   Quale è la temperatura prevista più elevata per oggi?
	-   Sarà nebbioso domani mattina?

	Una delle domande di esempio include una termine ("nebbioso") per cui il classificatore non è preparato. Il classificatore può riuscire ad ottenere questi termini "mancanti" senza alcuna tua ulteriore azione per identificarli. Prova altre domande che includo parole non presenti nei dati di formazione, ad esempio "nevischio" o "tempesta".

L'operazione è terminata! Hai creato, preparato ed eseguito query di un classificatore nel servizio {{site.data.keyword.nlclassifiershort}}.

## Elimina il classificatore dell'esercitazione

Per poter creare i classificatori per il tuo proprio utilizzo e con i tuoi dati di formazione, potresti voler eliminare questo classificatore dall'esercitazione. Per eliminare il classificatore, richiama il metodo `DELETE /classifiers/{classifier_id}`.

Come prima, sostituisci `{username}`, `{password}` e `{classifier_id}` con le tue informazioni nel seguente comando.

```bash
curl -X DELETE -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
```
{: pre}

La risposta al comando è un oggetto JSON vuoto.

## Operazioni successive 
Hai una conoscenza di base su come utilizzare {{site.data.keyword.nlclassifiershort}}. Ora approfondisci:
- Impara come [utilizzare i tuoi propri dati](/docs/natural-language-classifier/using-your-data.html) per preparare un classificatore.
- Leggi le informazioni sull'API in [API reference ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/watson/developercloud/natural-language-classifier/api/){:new_window}.
- Interagisci con l'API in [API explorer ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://watson-api-explorer.mybluemix.net/apis/natural-language-classifier-v1){:new_window}.
- Cerca in [Node.js starter application](https://github.com/watson-developer-cloud/natural-language-classifier-nodejs){:new_window} un'applicazione web di esempio.
