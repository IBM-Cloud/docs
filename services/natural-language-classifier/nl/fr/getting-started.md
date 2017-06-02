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

# Initiation 
{: #natural-language-classifier}

Le service {{site.data.keyword.nlclassifierfull}} peut aider votre application à comprendre la langue de textes courts et à effectuer des prévisions concernant leur traitement. Un discriminant effectue son apprentissage à partir de vos exemples de données,
puis peut renvoyer des informations pour les textes pour lesquels il n'est pas entraîné.
{:shortdesc}

Vous pouvez créer et entraîner un discriminant {{site.data.keyword.nlclassifiershort}} en moins de quinze minutes.


## Etape 1 : Connexion, création du service et obtention de vos données d'identification 

Si vous connaissez déjà vos données d'identification pour l'instance de service {{site.data.keyword.nlclassifiershort}}, ignorez cette étape.
{: tip}

1.  Accédez au [service {{site.data.keyword.nlclassifiershort}}](https://console.{DomainName}/catalog/services/natural-language-classifier/) et créez un compte gratuit ou connectez-vous à votre compte {{site.data.keyword.Bluemix_notm}}. 
1.  Une fois connecté, dans la page {{site.data.keyword.nlclassifiershort}}, entrez `Classifier-tutorial` dans la zone **Nom du service** pour identifier cette instance du service, puis cliquez sur **Créer**.
1.  Copiez vos données d'identification :
    1.  Cliquez sur **Données d'identification pour le service**.
    2.  Cliquez sur **Afficher les données d'identification** dans la section "Données d'identification pour le service". 
    3.  Copiez les valeurs `username` et `password`. 

## Etape 2 : Création et entraînement d'un discriminant 
Le discriminant effectue son apprentissage à partir d'exemples avant de pouvoir renvoyer des informations pour des textes qu'il n'a jamais vus auparavant. Les exemples de données sont appelés "données d'apprentissage". Vous les téléchargez lorsque vous créez un discriminant.

1.  Téléchargez l'exemple <code><a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a></code>. Il s'agit des données d'apprentissage qui sont utilisées dans la [démonstration ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](http://natural-language-classifier-demo.mybluemix.net){:new_window}.

	Le fichier est au format CSV et comporte deux colonnes. La première colonne contient l'entrée de texte. La deuxième colonne contient la classe
pour ce texte : temperature ou condition. Affichez le fichier pour visualiser les entrées.
2.  Emettez la commande curl suivante pour appeler la méthode `POST
/classifiers/`, qui envoie par téléchargement les données d'apprentissage
et crée le discriminant :

    -   Remplacez `{username}` et
`{password}` par les données d'identification pour le service que
vous avez copiées à l'étape précédente.

    -   Modifiez l'emplacement training\_data pour désigner le répertoire dans
lequel vous avez sauvegardé le fichier `weather_data_train.csv`. 

	```bash
	curl -i -u "{username}":"{password}" -F training_data=@{path_to_file}/weather_data_train.csv -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers"
	```
	{: pre}

	La réponse inclut un nouvel ID de discriminant et un statut. Exemple :

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

	L'apprentissage commence immédiatement et doit être terminé pour que vous puissiez
interroger le discriminant.
3.  Vérifiez le statut d'apprentissage régulièrement jusqu'à ce qu'il s'agisse
d'`Available`. Avec ces exemples de données, l'apprentissage prend
environ 6 minutes :

	- Emettez un appel `GET /classifiers/{classifier_id}` pour
extraire le statut du discriminant. Dans l'exemple suivant, remplacez
`{username}`, `{password}` et
`{classifier_id}` par vos informations :

		```bash
		curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
		```
		{: pre}

## Etape 3 : Classification du texte 
Maintenant que le discriminant est entraîné, vous pouvez l'interroger.


1.  Classifiez des questions relatives à la météo pour déterminer la façon
dont le discriminant que vous venez d'entraîner répond. Voici un exemple d'appel. Remplacez
`{username}`, `{password}` et
`{classifier_id}` par vos informations : 

	```bash
	curl -G -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}/classify" --data-urlencode "text=How hot will it be today?"
	```
	{: pre}

	L'API renvoie une réponse qui inclut le nom de la classe que le
discriminant considère comme la plus fiable.
D'autres paires classe-fiabilité sont répertoriées par ordre décroissant de fiabilité :


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

	Le niveau de fiabilité correspond à un pourcentage, et les valeurs les
plus élevées représentent des niveaux de fiabilité élevés.
La réponse peut inclure jusqu'à dix classes. 

	Si vous disposez de moins de dix classes dans vos données d'apprentissage, la somme de
tous les niveaux de fiabilité est de 100 %. Dans ces exemples de données
d'apprentissage, deux classes seulement sont définies ; par conséquent, deux classes
seulement peuvent être renvoyées.
2.  Examinez la classe supérieure pour les questions afin de déterminer
dans quelle
mesure le discriminant les prévoit.


	Voici d'autres exemples de question à classifier :


	-   Is it hot outside? (Fait-il chaud dehors ?) 
	-   Will it be windy? (Y'aura-t-il du vent ?) 
	-   Will we see some sun? (Y'aura-t-il du soleil ?) 
	-   What is the expected high for today? (Quelle est la température maximale
prévue pour
aujourd'hui ?) 
	-   Will it be foggy tomorrow morning? (Y'aura-t-il du brouillard demain matin ?) 

	L'un des exemples de question inclut un terme ("foggy") que
le discriminant
ne connaît pas. Ce dernier peut obtenir de bon résultats avec ces termes
"manquants"
sans que vous n'ayez à effectuer de tâches supplémentaires pour les identifier.
Essayez d'autres questions incluant des mots qui ne figurent pas dans les données
d'apprentissage, par exemple "sleet" (grésil) ou "storm" (orage).


Vous avez terminé ! Vous avez créé, entraîné et interrogé un discriminant dans le
service {{site.data.keyword.nlclassifiershort}}. 

## Supprimez le discriminant du tutoriel 

Pour pouvoir créer vos propres discriminants avec vos propres données
d'apprentissage, il est recommandé de supprimer ce discriminant du tutoriel. Pour ce
faire, appelez la méthode `DELETE /classifiers/{classifier_id}`. 

Comme précédemment, remplacez `{username}`,
`{password}` et `{classifier_id}` par vos informations
dans la commande suivante :


```bash
curl -X DELETE -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
```
{: pre}

La réponse à la commande est un objet JSON vide.


## Etapes suivantes 
Vous avez compris les principes de base de l'utilisation du service {{site.data.keyword.nlclassifiershort}}. A
présent, approfondissez vos connaissances :

- Apprenez à
[utiliser vos propres
données](/docs/natural-language-classifier/using-your-data.html) pour entraîner un discriminant. 
- Lisez la documentation sur l'API dans la [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/natural-language-classifier/api/){:new_window}.
- Interagissez avec l'API dans l'[explorateur d'API ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://watson-api-explorer.mybluemix.net/apis/natural-language-classifier-v1){:new_window}.
- Intéressez-vous à l'[application de démarrage Node.js](https://github.com/watson-developer-cloud/natural-language-classifier-nodejs){:new_window} pour un exemple d'application Web. 
