---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Utilisation de vos propres données 
Après avoir créé, entraîné et interrogé un discrimant du service
{{site.data.keyword.nlclassifierfull}} avec les données figurant dans l'exemple
[Initiation](/doc/natural-language-classifier/getting-started.html),
créez un discriminant qui fonctionne avec vos propres données.
Vous allez assembler et fournir ces données d'apprentissage.
{:shortdesc}

## Structure des données d'apprentissage 
Vous pouvez fournir les données permettant d'entraîner
{{site.data.keyword.nlclassifiershort}} au format CSV.


Au format CSV, chaque ligne dans le fichier représente un exemple d'enregistrement. Chaque
enregistrement comporte deux colonnes ou plus. La première colonne est le texte
représentatif à classifier. Les autres colonnes comportent les classes à appliquer à ce
texte.
L'image ci-dessous représente un fichier CSV contenant quatre enregistrements. Chaque
enregistrement dans l'exemple inclut le texte entré et une classe, séparés par une
virgule :


![](images/train_sample.png)

Cet exemple est petit. De véritables données d'apprentissage incluent beaucoup
plus d'enregistrements.


Téléchargez le fichier
<a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a>
pour afficher un exemple de fichier de données d'apprentissage.


### Métadonnées supplémentaires 

En plus du texte et des classes, la demande de création d'un discriminant inclut
des informations supplémentaires. Les métadonnées identifient la langue des données, et
vous pouvez également inclure un nom permettant d'identifier le discriminant.


### Format de fichier de données d'apprentissage CSV 

Veillez à ce que les données d'apprentissage CSV respectent les exigences de format
suivantes :


- Les données doivent être codées en UTF-8. 
- Séparez les valeurs textuelles et chaque valeur de classe par une virgule.
Chaque enregistrement (ligne) doit se terminer par un caractère de fin de ligne,
c'est-à-dire un caractère spécial ou une séquence de caractères indiquant la fin de la ligne. 
- Chaque enregistrement doit comporter une valeur textuelle et au moins une valeur
de classe.

- Les valeurs de classe ne peuvent pas comporter de tabulation ni de
caractère de fin de ligne.

- Les valeurs textuelles ne peuvent pas comporter de tabulation ni de nouvelle
ligne sans traitement spécial.
Pour conserver les tabulations ou les nouvelles lignes, mettez les tabulations en
échappement avec `\t` et les nouvelles lignes avec
`\r`, `\n` ou `\r\n`.

	Par exemple, `Texte exemple\tavec tabulation` est valide, alors que
`Texte exemple    avec tabulation` ne l'est pas.
- Placez toujours les valeurs textuelles et de classe entre guillemets dans les
données d'apprentissage si elles comportent les caractères suivants :

	- Des virgules : `"Texte exemple, avec virgule"`.
	- Des guillemets. De plus, les guillemets doivent être mis en échappement avec
des guillemets : `"Texte exemple avec ""guillemets""`.

## Limites de taille 
Il existe des limites minimale et maximale pour les données d'apprentissage :


-   Les données d'apprentissage doivent comporter entre 5 et 15000 enregistrements
(lignes).

-   La longueur totale maximale d'une valeur textuelle est de 1024 caractères.


## Langues 
La langue par défaut est l'anglais, mais vous pouvez spécifier la langue des données d'apprentissage lorsque vous créez le discriminant. La langue des données d'apprentissage doit correspondre à celle du texte que vous prévoyez de classifier. Pour des détails, voir la [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/watson/developercloud/natural-language-classifier/api/v1/){:new_window}.

Le discriminant prend en charge l'anglais (en), l'arabe (ar), le français (fr),
l'allemand (de), le japonais (ja), l'italien (it), le portugais (Brésil) (pt) et
l'espagnol (es). 

## Instruction pour un apprentissage réussi 
Les instructions ci-après ne sont pas imposées par l'API. Cependant, le
discriminant est plus performant lorsque les données d'apprentissage les respectent :


- Limitez la longueur du texte d'entrée à moins de 60 mots. 
- Limitez le nombre de classes à plusieurs centaines de classes.
Des versions ultérieures du service pourront prendre en charge des nombres de
classes plus élevés. 
- Assurez-vous que chaque classe correspond à au moins 5 à 10 enregistrements,
où chaque enregistrement de texte est associé à une classe seulement. Ce nombre permet
un apprentissage suffisant pour la classe.

- Evaluez la nécessité d'utiliser plusieurs classes. Deux raisons fréquentes motivent
l'utilisation de plusieurs classes :

	- Lorsque le texte est vague, l'identification d'une seule classe n'est pas
toujours claire.

	- Lorsque des experts interprètent le texte de différentes façons, plusieurs
classes prennent en charge les interprétations.


	Toutefois, si de nombreux textes dans vos données d'apprentissage incluent
plusieurs classes, ou si certains textes sont associés à plus de trois classes, il
peut être nécessaire d'affiner les classes. Par exemple, déterminez si les classes sont
hiérarchiques. Si tel est le cas, incluez le noeud feuille comme classe.
-  Incluez des termes standard comportant des traits d'union lorsqu'ils font
partie des données d'apprentissage (`qualité-prix` ou
`travail à
mi-temps`).

	Toutefois, n'associez pas de mots adjacents pour créer de nouveaux termes
qui n'existent pas dans la langue des données d'apprentissage. Par exemple, au lieu de
définir `le-petit` ou
`chaperon_rouge`, définissez les expressions
pertinentes à l'aide
de mots distincts (`le petit` et `chaperon rouge`) avec la classe appropriée.


## Construction des données d'apprentissage 
L'apprentissage automatique est un processus d'apprentissage de certaines
propriétés à partir d'un ensemble de données, puis d'application des propriétés à de
nouvelles données.
Le service {{site.data.keyword.nlclassifiershort}} applique ce processus. Il
est entraîné pour connecter des classes prédéfinies à des exemples de texte, puis
applique ces classes à de nouvelles entrées.


Par conséquent, les performances du discriminant entraîné dépendent des données
d'apprentissage. Chaque valeur textuelle dans les données doit représenter les sortes
de texte que le discriminant doit prévoir.
Chaque classe dont vous prévoyez le renvoi doit également figurer dans les données
d'apprentissage, et les classes que vous associez à chaque texte doivent être correctes.


Par exemple, lorsque les textes figurant dans vos données d'apprentissage sont des
questions, utilisez des questions classiques représentatives des questions posées par vos utilisateurs.
Vous pouvez collecter ces textes à partir des données utilisateur réelles ou demander à
des spécialistes de votre domaine de créer les textes.


Cette nature représentative et précise des données est importante car elle a un
impact sur tous les processus et les résultats du discriminant.
De plus, plus le nombre d'enregistrements inclus dans les données d'apprentissage est
élevé, plus le discriminant aura une chance de trouver une correspondance.

