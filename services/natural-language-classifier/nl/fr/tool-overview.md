---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_wind{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Gestion des discriminants avec le kit d'outils

{: #managing-toolkit}

Vous pouvez gérer vos données d'apprentissage et vos discriminants à l'aide de
l'application Web {{site.data.keyword.nlclassifierfull}} Toolkit. Ce kit
d'outils propose une vue unifiée de tous les discriminants qui s'exécutent dans une même
instance de service {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Il s'agit d'une édition bêta du kit d'outils. La version bêta
de ce kit d'outils ne sera peut-être plus prise en charge dans les nouvelles éditions ou
lorsque le kit d'outils ne sera plus associé au statut bêta.
N'utilisez pas le kit d'outils en production. 

L'interface Web du kit d'outils simplifie l'apprentissage et le test des discriminants. Vos experts de domaine peuvent utiliser le kit d'outils pour mettre l'accent sur la qualité de vos données d'apprentissage. 

## Obtention de l'accès 
{: #getting-access}

Vous trouverez un lien vers le kit d'outils dans la page de tableau de bord du service {{site.data.keyword.Bluemix_notm}} pour votre instance de {{site.data.keyword.nlclassifiershort}}.

### Accédez vous-même au kit d'outils 

Pour accéder au lien vers le kit d'outils, suivez les étapes suivantes afin d'accéder au tableau de bord de votre **service** {{site.data.keyword.Bluemix_notm}} : 

1. Ouvrez votre vignette de service {{site.data.keyword.nlclassifiershort}} en vous connectant à votre tableau de bord [{{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/dashboard/services){: new_window}.

	-  Dans la zone **Services**, cliquez sur votre vignette de service {{site.data.keyword.nlclassifiershort}} pour ouvrir le tableau de bord de l'instance. (S'il n'existe pas de vignette de service, [créez une instance ![Icône de lien externe](../../icons/launch-glyph.svg)](https://console.{DomainName}/catalog/services/natural-language-classifier/){: new_window} du service {{site.data.keyword.nlclassifiershort}}.) 
1. Dans le tableau de bord du service, cliquez sur **Access the beta toolkit**.

	Ajoutez l'adresse URL à vos signets pour un accès ultérieur facile au kit d'outils. {: tip}

### Donnez l'accès à votre kit d'outils à d'autres 

Vous pouvez autoriser d'autres utilisateurs à vous servir de votre kit d'outils en
les
ajoutant dans {{site.data.keyword.Bluemix_notm}}.

1.  Dans {{site.data.keyword.Bluemix_notm}}, cliquez sur **Compte > Inviter des membres d'équipe**.
1.  Sélectionnez l'organisation contenant votre service de discriminant et cliquez sur **Suivant**.
1.  Sélectionnez l'espace contenant votre service de discriminant. 
1.  Sélectionnez le rôle d'espace **Développeur**. Pour des détails sur les rôles, voir la rubrique relative à la [gestion des membres d'équipe et des rôles](/docs/admin/users_roles.html).
1.  Entrez l'adresse électronique de l'utilisateur, puis cliquez sur **Envoyer**.
1.  Dans un courrier électronique distinct, envoyez l'adresse URL de votre kit d'outils (pour lequel vous avez enregistré un signet précédemment) aux utilisateurs. 

## Exemples d'utilisation
{: #example-uses}

Dans ces exemples, vous créez et modifiez des données d'apprentissage, testez un
discriminant de façon interactive ou à partir d'un ensemble de données de test, et mettez
à jour des données d'apprentissage à partir des résultats.


### Créez des données d'apprentissage dans le kit d'outils 

Familiarisez-vous avec le kit d'outils
{{site.data.keyword.nlclassifiershort}} en créant un petit ensemble de données
d'apprentissage à l'aide du kit d'outils.


Pour pouvoir créer un discriminant, vous avez besoin de données d'apprentissage. Vous
pouvez créer les données en entrant des textes et des classes ou télécharger des données
d'apprentissage depuis un fichier CSV dont le
[format de
fichier](/docs/services/natural-language-classifier/using-your-data.html) est approprié.
1. Dans la page **Training data** du kit d'outils, ajoutez un
texte. Si vous n'avez pas d'idée de texte, ajoutez "Où se trouve le distributeur le plus
proche ?". 
1. Affectez une classe au texte en la tapant. Pour l'exemple de distributeur,
entrez "emplacement". 
1. Continuez d'ajouter des textes et des classes à vos données d'apprentissage. Vous
pouvez affecter des classes à des textes comme suit :

	-   Cliquez sur une classe pour la sélectionner, puis cliquez sur **Add text**. Ou
bien, sélectionnez un texte, puis cliquez sur **Assign classes**.
	-   Sélectionnez une classe, puis faites glisser un texte sur la classe. Ou bien,
sélectionnez un texte, puis faites glisser une classe sur le texte.


	Vous pouvez gérer plusieurs classes ou textes à la fois en appuyant sur la touche Ctrl
et en cliquant sur les textes ou les classes de votre choix (sur un Mac, appuyez sur
Command). Faites
des essais.
1. Après avoir utilisé vos données d'apprentissage pendant un moment, cliquez
sur **Download training data** pour enregistrer les données en
tant que sauvegarde.


	Vous pouvez aussi télécharger ce fichier dans le kit d'outils pour réutiliser les données d'apprentissage ultérieurement. {: tip}
1. Une fois que vous avez affecté des classes à au moins cinq textes, vous pouvez créer un discriminant à partir de ces données d'apprentissage. Cliquez sur **Create classifier**. {{site.data.keyword.watson}} commence à entraîner le discriminant. 

### Testez votre discriminant et mettez à jour vos données d'apprentissage 

Une fois qu'un discriminant a été entraîné et est disponible, vous pouvez
vérifier dans quelle mesure il classifie correctement les textes qu'il n'a jamais vus
auparavant.
Vous pouvez tester une série de textes et améliorer les données d'apprentissage en
ajoutant les réponses de niveau de fiabilité incorrect ou faible.


1.  Dans la page **Classifiers**, cliquez sur **Test
and improve performance** pour le discriminant à tester. 
1.  Dans la page **Improve performance**, entrez un texte qui
ne figure pas dans vos données d'apprentissage et cliquez sur **Classify**. {{site.data.keyword.watson}}
renvoie les classes pertinentes et leurs niveaux de fiabilité.

1.  Ajoutez d'autres textes afin de tester les performances. 
1.  Examinez les réponses. Signalez ou approuvez les résultats à ajouter à vos
données d'apprentissage :

	- Si la classification n'est pas correcte, signalez le résultat. 
	- Si la réponse est correcte mais que le niveau de fiabilité est faible, ajoutez
le résultat à vos données d'apprentissage en cliquant sur **Approve**.
1.  Cliquez sur **Add to training data** pour ajouter les
réponses approuvées et signalées à vos données d'apprentissage.

1.  Dans la page **Training data**, examinez et mettez à jour
les classes qui sont affectées aux textes que vous avez signalés. 
1.  Pour mettre à jour votre discriminant avec ces nouvelles données
d'apprentissage, vous devez en créer un nouveau. Cliquez sur **Create
classifier**. Une fois que le nouveau discriminant est entraîné, testez-le
pour voir dans quelle mesure il a été amélioré.


### Téléchargez des données pour tester votre discriminant


La saisie de textes à classifier un par un est efficace pour effectuer des
tests
rapides. Toutefois, si vous disposez d'un *ensemble de tests*, vous pouvez
le télécharger dans le kit d'outils afin de classifier de nombreux textes en même
temps. Un ensemble de tests est un groupe d'exemples de texte qui ne figurent pas dans
vos données d'apprentissage. Vous l'utiliser pour vérifier les performances du
discriminant.


1.  Créez un fichier d'ensemble de tests : 
	- Le fichier peut utiliser le même format que les données d'apprentissage (en
d'autres termes, il peut inclure les classes appropriées) ou n'inclure que des
textes,
un par ligne. Veillez à ce que les textes (et les classes) respectent les exigences de
[format de
fichier](/docs/services/natural-language-classifier/using-your-data.html). 
    -   Sauvegardez le fichier avec l'extension `.csv`.

1.  Dans la page **Classifiers**, cliquez sur **Test
and improve performance** pour le discriminant à tester. 
1.  Dans la page **Improve performance**, cliquez sur **Use test data**. {{site.data.keyword.watson}}
télécharge les données, classifie chaque texte et renvoie une réponse. 
1.  Comparez les réponses à la classification correcte et recherchez les
niveaux de fiabilité faibles.

1.  Améliorez les données d'apprentissage en ajoutant d'autres exemples.
N'ajoutez pas d'exemples qui existent dans votre ensemble de tests si vous voulez
continuer à utiliser ce dernier pour évaluer les performances du discriminant.

