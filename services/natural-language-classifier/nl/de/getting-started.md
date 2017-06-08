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

# Einführung
{: #natural-language-classifier}

Der Service {{site.data.keyword.nlclassifierfull}} unterstützt Ihre Anwendung, sodass sie die Sprache kurzer Texte verstehen und Vorhersagen zu ihnen erstellen kann. Ein Klassifikationsmerkmal (Classifier) lernt anhand Ihrer Beispieldaten und kann anschließend Informationen zu Texten zurückgeben, anhand derer es nicht trainiert wurde.
{:shortdesc}

Sie können eine {{site.data.keyword.nlclassifiershort}}-Instanz in weniger als 15 Minuten erstellen und trainieren. 

## Schritt 1: Anmelden, Service erstellen und Berechtigungsnachweise abrufen

Wenn Sie Ihre Berechtigungsnachweise für die Instanz des Service '{{site.data.keyword.nlclassifiershort}}' bereits kennen, überspringen Sie diesen Schritt.
{: tip}

1.  Rufen Sie den [Service {{site.data.keyword.nlclassifiershort}}](https://console.{DomainName}/catalog/services/natural-language-classifier/) auf und erstellen Sie ein kostenloses Konto oder melden Sie sich bei Ihrem {{site.data.keyword.Bluemix_notm}}-Konto an. 
1.  Geben Sie nach der Anmeldung auf der Seite '{{site.data.keyword.nlclassifiershort}}' in das Feld **Servicename** die Zeichenfolge `Classifier-tutorial` ein, um diese Instanz des Service anzugeben und klicken Sie auf **Erstellen**. 
1.  Kopieren Sie Ihre Berechtigungsnachweise: 
    1.  Klicken Sie auf **Serviceberechtigungsnachweise**. 
    2.  Klicken Sie im Abschnitt 'Serviceberechtigungsnachweise' auf **Berechtigungsnachweise anzeigen**. 
    3.  Kopieren Sie die Werte für `username` und `password`. 

## Schritt 2: Klassifikationsmerkmal erstellen und trainieren 
Das Klassifikationsmerkmal muss zunächst anhand von Beispielen lernen, bevor es Informationen zu Texten zurückgeben kann, die es zuvor nicht gesehen hat. Die Beispieldaten werden als 'Trainingsdaten' bezeichnet. Sie laden die Trainingsdaten beim Erstellen eines Klassifikationsmerkmals hoch. 

1.  Laden Sie das Beispiel <code><a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a></code> herunter. Dies sind dieselben Trainingsdaten, die in der [Demo ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](http://natural-language-classifier-demo.mybluemix.net){:new_window} verwendet werden. 

	Die Datei hat das CSV-Format und weist zwei Spalten auf. Die erste Spalte ist die Texteingabe. Die zweite Spalte gibt die Klasse für diesen Text an: 'Temperatur' (temperature) oder 'Bedingung' (condition). Zeigen Sie die Datei an, um die Einträge zu sehen.
2.  Setzen Sie den folgenden cURL-Befehl ab, um die Methode `POST /classifiers/` aufzurufen, mit der die Trainingsdaten hochgeladen werden und das Klassifikationsmerkmal erstellt wird: 
    -   Ersetzen Sie `{username}` und `{password}` durch die Serviceberechtigungsnachweise, die Sie in einem früheren Schritt kopiert haben. 
    -   Ändern Sie die Position für 'training\_data', sodass auf die Position verwiesen wird, an der Sie die Datei `weather_data_train.csv` gespeichert haben. 

	```bash
	curl -i -u "{username}":"{password}" -F training_data=@{path_to_file}/weather_data_train.csv -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers"
	```
	{: pre}

	Die Antwort enthält eine neue Klassifikationsmerkmal-ID und einen neuen Status. Beispiel: 

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

	Das Training beginnt sofort und muss abgeschlossen sein, bevor Sie das Klassifikationsmerkmal abfragen können.
3.  Überprüfen Sie regelmäßig den Trainingsstatus, bis der Status `Verfügbar` angezeigt wird. Das Training mit diesen Beispieldaten dauert etwa 6 Minuten: 
	- Setzen Sie den Aufruf `GET /classifiers/{classifier_id}` ab, um den Status des Klassifikationsmerkmals abzurufen. Ersetzen Sie im folgenden Beispiel `{username}`, `{password}` und `{classifier_id}` durch Ihre Angaben: 

		```bash
		curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
		```
		{: pre}

## Schritt 3: Text klassifizieren
Das Klassifikationsmerkmal ist nun trainiert und Sie können es abfragen. 

1.  Klassifizieren Sie einige auf das Wetter bezogenen Fragen, um zu überprüfen, wie Ihr neu trainiertes Klassifikationsmerkmal antwortet. Im Folgenden finden Sie einen Beispielaufruf. Ersetzen Sie `{username}`, `{password}` und `{classifier_id}` durch Ihre Angaben: 

	```bash
	curl -G -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}/classify" --data-urlencode "text=How hot will it be today?"
	```
	{: pre}

	Die API gibt eine Antwort zurück, in der der Name der Klasse enthalten ist, die das Klassifikationsmerkmal mit der höchsten Konfidenz bewertet hat. Weitere Paare aus 'Klasse' und 'Konfidenz' werden hinsichtlich der Konfidenz in absteigender Reihenfolge aufgelistet: 

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

	Der Konfidenzwert wird durch einen Prozentsatz angegeben; höhere Werte stellen höhere Konfidenzwerte dar. Die Antwort enthält bis zu 10 Klassen. 

	Wenn in Ihren Trainingsdaten weniger als 10 Klassen vorhanden sind, beträgt die Summe aller Konfidenzwerte 100 Prozent. In diesen als Beispiel verwendeten Trainingsdaten sind nur zwei Klassen definiert; es können also nur zwei zurückgegeben werden.
2.  Überprüfen Sie die höchste Klasse anhand der Fragen, um zu sehen, welche Vorhersage das Klassifikationsmerkmal für sie vornimmt. 

	Hier einige weitere Beispielfragen, die klassifiziert werden können: 

	-   Is it hot outside?
	-   Will it be windy?
	-   Will we see some sun?
	-   What is the expected high for today?
	-   Will it be foggy tomorrow morning?

	In einer der Beispielfragen ist ein Begriff enthalten ('foggy' - neblig), für das das Klassifikationsmerkmal nicht trainiert ist. Das Klassifikationsmerkmal kann trotz 'fehlender' Begriffe eine gute Bewertung erzielen, ohne dass Sie sich zusätzlich mit der Ermittlung solcher Begriffe befassen müssen. Machen Sie einen Versuch mit anderen Fragen, in denen Wörter enthalten sind, die sich nicht in den Trainingsdaten befinden, beispielsweise 'sleet' (Graupelschauer) oder 'storm' (Sturm). 

Fertig! Sie haben im Service '{{site.data.keyword.nlclassifiershort}}' ein Klassifikationsmerkmal erstellt, trainiert und abgefragt. 

## Klassifikationsmerkmal des Lernprogramms löschen

Damit Sie Klassifikationsmerkmale mit eigenen Trainingsdaten und zu Ihrer eigenen Verwendung erstellen können, müssen Sie dieses Klassifikationsmerkmal aus dem Lernprogramm löschen. Rufen Sie zum Löschen des Klassifikationsmerkmals die Methode `DELETE /classifiers/{classifier_id}` auf. 

Ersetzen Sie im folgenden Befehl `{username}`, `{password}` und `{classifier_id}` wie zuvor durch Ihre Angaben. 

```bash
curl -X DELETE -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
```
{: pre}

Die Antwort auf den Befehl ist ein leeres JSON-Objekt. 

## Nächste Schritte
Sie verstehen nun die Grundlagen der Verwendung von {{site.data.keyword.nlclassifiershort}}. Gehen Sie nun einen Schritt weiter: 
- Erlernen Sie nun, wie Sie [eigene Daten verwenden können](/docs/natural-language-classifier/using-your-data.html), um ein Klassifikationsmerkmal zu trainieren. 
- Lesen Sie Informationen zur API in der [API-Referenz ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://www.ibm.com/watson/developercloud/natural-language-classifier/api/){:new_window}. 
- Interagieren Sie im [API-Explorer ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://watson-api-explorer.mybluemix.net/apis/natural-language-classifier-v1){:new_window} mit der API. 
- Sehen Sie sich die [Node.js-Starteranwendung](https://github.com/watson-developer-cloud/natural-language-classifier-nodejs){:new_window} an, um eine Beispiel-Web-App abzurufen. 
