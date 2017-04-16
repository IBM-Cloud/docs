---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilisation des API REST Insights for Twitter
{: #rest_apis}

Le service {{site.data.keyword.twittershort}} comporte des API RESTful permettant de rechercher et de consommer un contenu Twitter. Le tableau [Langage d'interrogation](twitter_rest_apis.html#querylanguage){: new.window} répertorie les termes de requête qui sont pris en charge par les API de service. Des exemples sont fournis pour montrer la façon dont les requêtes peuvent être construites.
{:shortdesc}

## Documentation de l'API REST {: #rest_api}
La documentation de l'API REST est construite avec Swagger, ce qui vous permet de tester les
opérations de l'API et d'afficher instantanément les résultats afin de générer vos applications plus vite.
Les opérations suivantes sont actuellement disponibles pour l'API :

* Recherche : trouve des tweets dans le flux Decahose ou PowerTrack filtré.
* Décompte : retourne le nombre de tweets selon une requête donnée.
* Vérification : détermine si une liste de messages est conforme aux règles et aux utilisateurs.
* Suivis : fournit aux utilisateurs du plan payant un assortiment de noeuds finaux pour gérer les filtres PowerTrack.

Pour plus d'informations sur les API REST prises en charge et leurs ressources, voir la documentation de référence relative à l'[API REST](https://cdeservice.{APPDomain}/rest-api/){: new_window}. Sélectionnez la région dans laquelle votre application existe. Chaque région est indépendante. Vous ne pouvez pas utiliser les données d'identification qui vous ont été fournies pour le service dans une région pour vous authentifier dans une autre région.

Dans la documentation de référence, cliquez sur **List Operations** pour afficher le détail de chaque opération. Après avoir cliqué sur le bouton **Try it out!** , vous pouvez être invité à fournir des données d'identification. Vous devez fournir le nom d'utilisateur et le mot de passe tirés de vos variables d'environnement **VCAP_SERVICES**. Vous trouverez ces informations en ouvrant votre application et en cliquant sur **Variables d'environnement** dans la table des matières.

**Remarque** : une entrée incorrecte des données d'identification génère le message "Non autorisé" dans le corps de la réponse.

**Important** : les suivis actifs créés en utilisant la fonction **Try it out!** collectent les tweets de Twitter, qui sont alors pris en compte dans votre relevé mensuel. Lorsque des suivis deviennent inutiles, faites-les passer à l'état **Inactive** ou supprimez-les tout simplement.


## Langage d'interrogation {: #querylanguage}

Avec {{site.data.keyword.twittershort}}, vous pouvez rechercher un contenu Twitter à l'aide d'un ensemble
riche de paramètres de requête et de filtres afin d'obtenir des résultats plus précis.

Les opérateurs booléens ci-dessous sont admis dans vos requêtes. 

| **Opérateur**        | **Description**                                                                                                                   | **Exemples**      |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------|-------------------|
| terme1 **AND** terme2 | Renvoie les tweets qui contiennent terme1 et terme2. Un espace vierge entre deux termes étant traité en tant qu'opérateur AND, l'opérateur peut être omis. | `#ibm twitter`      |
| terme1 **OR** terme2  | Renvoie les tweets qui contiennent terme1 ou terme2.    | `#money OR revenue` |
| -terme1              | Renvoie les tweets qui ne contiennent pas terme1.  |`ibm -apple`  |

*Tableau 1. Opérateurs booléens*

Priorité des opérateurs : "-" a priorité sur "AND" et "AND" a priorité sur "OR". Vous devez utiliser des parenthèses pour que la
priorité des opérateurs soit explicite. Ainsi, `large animals` -(`giraffes` OR `bears`) recherche les tweets qui contiennent les termes "large" et "animals", mais exclut les tweets qui comportent les termes "giraffes" et "bears".

Le tableau ci-dessous répertorie les termes de requête pris en charge actuellement.

| **Terme** 	| **Description** 	| **Exemples** 	|
|----------------------------------------------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|---------------------------------------------	|
| mot clé 	| Recherche les tweets dont le corps contient "keyword". La recherche ne distingue pas les minuscules des majuscules. 	| analyse 	|
| "expression exacte" 	| Recherche les tweets qui contiennent l'expression exacte. 	| "IBM and analytics" 	|
| `#hashtag` 	| Recherche les tweets qui comporte le hashtag *#hashtag*. 	| `#insight2015` 	|
| `bio_lang:language` 	| Recherche les tweets des utilisateurs dont les paramètres de langue du profil correspondent au code de langue indiqué.  Voir `lang:` pour une liste des langues prises en charge. 	| `bio_lang:en` 	|
| `bio_location:"location"` 	| Recherche les tweets des utilisateurs dont le paramètre de résidence du profil contient la référence `location` spécifiée. 	| `bio_location:"New York"` 	|
| `country_code:country-code` 	| Recherche les utilisateurs dont les étiquettes de localisation et de lieu correspondent au code pays indiqué. </br>**Pour connaître la liste des codes pays pris en charge, voir **: http://en.wikipedia.org/wiki/ISO_3166-1 	| `country_code:us` 	|
| `followers_count: lowerLimit,upperLimit` 	| Recherche les tweets des utilisateurs qui ont un nombre de suiveurs compris dans la plage définie. upperLimit est facultatif et les deux limites sont inclusives.  	| `followers_count:500` 	|
| `friends_count: lowerLimit,upperLimit` 	| Recherche les tweets des utilisateurs qui suivent un nombre d'utilisateurs compris dans la plage définie. upperLimit est facultatif et les deux limites sont inclusives.  	| `friends_count:1000,3000` 	|
| `from:twitterHandle` 	| Recherche les tweets des utilisateurs dont le nom d'utilisateur préféré est *twitterHandle*. Ne doit pas contenir le symbole &commat;. 	| `from:alexlang11` 	|
| `has:children` 	| Recherche les tweets des utilisateurs qui ont des enfants. 	| `has:children` 	|
| `is:married` 	| Recherche les tweets des utilisateurs qui sont mariés. 	| `is:married` 	|
| `is:verified` 	| Recherche les tweets dont l'auteur a été vérifié par Twitter. 	| `analytics is:verified` 	|
| `lang:language-code` 	| Recherche les tweets dans une langue particulière. Les codes de langue pris en charge sont les suivants : <ul><li>`ar` (arabe)</li><li>`zh` (chinois)</li><li>`da` (danois)</li><li>`dl` (néerlandais)</li><li>`en` (anglais)</li><li>`fi` (finnois)</li><li>`fr` (français)</li><li>`de` (allemand)</li><li>`el` (grec)</li><li>`he` (hébreu)</li><li>`id` (indonésien)</li><li>`it` (italien)</li><li>`ja` (japonais)</li><li>`ko` (coréen)</li><li>`no` (norvégien)</li><li>`fa` (persan)</li><li>`pl` (polonais)</li><li>`pt` (portugais)</li><li>`ru` (russe)</li><li>`es` (espagnol)</li><li>`sv` (suédois)</li><li>`th` (thaï)</li><li>`tr` (turc)</li><li>`uk` (ukrainien)</li></ul>    | `lang:de` (pour rechercher des tweets en allemand) 	|
| `listed_count: lowerLimit,upperLimit` 	| Recherche les tweets dont la liste Twitter de l'auteur est comprise dans la plage définie. upperLimit est facultatif et les deux limites sont inclusives.  	| `listed_count:1000,3000` 	|
| `point_radius:[longitude latitude radius]` 	| Recherche les tweets d'une zone géographique, en fonction de la longitude, de la latitude et d'un rayon. </br></br>Toutes les coordonnées sont représentées en degrés décimaux. La `longitude`  doit être comprise entre -180 et +180, tandis que la `latitude` doit être comprise entre -90 et +90. La spécification d'une valeur en dehors des plages prises en charge retourne une erreur. Les valeurs doivent être saisies sous forme de nombres à virgule flottante. Les nombres entiers ne sont pas pris en charge. </br></br>Le rayon de la zone doit être défini en miles (mi) ou en kilomètres (km). 	| `point_radius:[41.128611 -73.707778 5.0mi]` 	|
| `posted:startTime  posted:startTime,endTime` 	| Recherche les tweets qui ont été postés à ou après "startTime". "endTime" est facultatif et les deux limites sont inclusives. Les
horodatages doivent être exprimés dans l'un des formats suivants :  </br>"yyyy-mm-dd" ou "yyyy-mm-ddTHH:MM:SSZ" </br>  Le fuseau horaire est au format UTC (Coordinated
Universal Time). Quand vous spécifiez des heures, des minutes et des secondes, elles doivent être encadrées par "T" et "Z", comme dans le format indiqué. 	| `posted:2014-12-01,2014-12-12` 	|
| `sentiment:sentiment-value` 	| Recherche les tweets exprimant un sentiment particulier. Les valeurs prises en charge sont les suivantes : </br><dl>positive</dl> <dlentry>Le tweet contient plus de phrases de sentiment positives que négatives.</dlentry> </br></br><dl>negative</dl> <dlentry>Le tweet contient plus de phrases de sentiment négatives que positives.</dlentry>  </br></br><dl>neutral</dl>  <dlentry>Le tweet ne contient pas de sentiment ou est dans une langue qui ne propose pas de détection de sentiment.</dlentry> </br></br><dl>ambivalent</dl>  <dlentry>Le tweet contient un nombre égal de phrases de sentiments positives et négatives.</dlentry> 	| `sentiment:positive` 	|
| `statuses_count: lowerLimit,upperLimit` 	| Recherche les tweets des utilisateurs qui ont posté un nombre de statuts compris dans la plage définie. upperLimit est facultatif et les deux limites sont inclusives.  	| `statuses_count:1000,3000` 	|
| `time_zone:timeZone` 	| Recherche les tweets des utilisateurs dont les paramètres du profil correspondent au fuseau horaire indiqué. 	| `time_zone:"Eastern Time (US & Canada)"` 	|
| `time_zone:city` 	| Recherche les tweets des utilisateurs dont les paramètres du profil correspondent à la ville indiquée. 	| `time_zone:"Dublin"` 	|
*Tableau 2. Termes de requête*

Tous les termes de requête pris en charge peuvent être combinés avec les opérateurs booléens décrits ci-dessus. Par exemple,

`ibm -apple followers_count:500`
