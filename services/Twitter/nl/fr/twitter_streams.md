---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Flux Decahose et PowerTrack {: #decahose_powertrack}

{{site.data.keyword.twittershort}} permet d'accéder aux flux Decahose et PowerTrack de Twitter, en fonction de l'inscription aux plans {{site.data.keyword.Bluemix_notm}}. 
Ces deux flux en temps réel ont des caractéristiques différentes pour répondre à vos besoins.
{:shortdesc}

Le flux Decahose fournit un échantillon aléatoire de 10 % du flux Firehose de Twitter. Les tweets sont dérivés de Twitter en temps réel et le flux est déterminé par les algorithmes d'échantillonnage de Twitter. Pour la plupart des analyses statistiques, un échantillon aléatoire de 10 %  est suffisamment précis. Les données Decahose étant indexées pour une période de 2 ans, les réponses aux requêtes ne peuvent retourner des tweets dont l'ancienneté dépasse 2 ans. L'accès au flux Decahose est disponible dans le plan gratuit et le plan payant, tandis que l'accès au flux PowerTrack est réservé aux utilisateurs du plan payant.

Le flux PowerTrack permet en outre de filtrer les tweets entrants à partir de règles définies par l'utilisateur, dans un suivi nommé "track". Les utilisateurs du plan payant peuvent créer jusqu'à 1000 règles par compte. Pour filtrer le flux de façon plus précise, il est possible de combiner plusieurs suivis dans un suivi agrégé (complexe). Les sections qui suivent décrivent les différents états des suivis, leurs propriétés et les actions qui peuvent leur être appliquées (édition, suppression...).

**Remarque** : l'indexation du flux PowerTrack est limitée à 1 million de tweets par mois calendaire. Une fois la limite atteinte, l'indexation s'arrête pour le mois. Au début du mois suivant, vous pouvez réactiver vos suivis. Ils ne s'activent pas automatiquement. Pour tirer le meilleur parti du flux, il est fortement recommandé de gérer attentivement les suivis. Ainsi, les flux redondants peuvent être désactivés.

## Types de suivi {: #track_types}

Les utilisateurs du plan payant peuvent créer des suivis personnalisables pour filtrer les messages collectés dans le flux de données
PowerTrack.  {{site.data.keyword.twittershort}}
prend en charge les deux types de suivi ci-dessous.

<dl>
<dt>Rule</dt>
<dd>Tous les messages collectés dans ce suivi correspondent à au moins une des règles associées au suivi. Ce type de suivi permet d'ajouter, d'éditer et de supprimer des règles.

L'ensemble de la [syntaxe des règles de GNIP PowerTrack](http://support.gnip.com/apis/powertrack2.0/rules.html) est prise en charge dans les suivis basés sur des règles. Toutes les requêtes doivent se conformer au [langage d'interrogation](twitter_rest_apis.html#querylanguage "langage d'interrogation") {{site.data.keyword.twittershort}}.
</dd>

<dt>Aggregated</dt>
<dd>Combinaison d'un ou de plusieurs suivis basés sur des règles ou complexes. Les suivis complexes servent à regrouper différents suivis de votre choix. Vous pouvez y ajouter ou y supprimer des suivis individuels. En revanche, vous ne pouvez pas y ajouter de règles individuelles. Vous devez pour cela utiliser un suivi basé sur des règles. Les suivis complexes n'ont pas d'état, mais les suivis basés sur des règles qui les composent sont actifs
(**Active**) ou inactifs (**Inactive**).</dd>
</dl>

## Propriétés des suivis {: #track_properties}
Les suivis ont les propriétés ci-dessous. Certaines propriétés ne s'appliquent pas à la fois aux suivis basés sur des règles et aux suivis agrégés (complexes). Ainsi, la propriété relative aux règles ne s'applique pas aux suivis agrégés (complexes).

<dl>
<dt>createdDate</dt>
<dd>Indique quand le suivi a été créé (format `YYYYMMDDHHMM`).</dd>

<dt>endDate</dt>
<dd>Indique quand le suivi arrête de collecter les messages. Il doit s'agir d'une valeur dans le futur, entrée dans l'un des formats suivants : `YYYY-MM-DD` ou `YYYY-MM-DDTHH:MM:SSZ`. La spécification d'une date dans le passé renvoie une erreur HTTP 400.

Cette propriété ne s'applique pas aux suivis complexes.</dd>

<dt>id</dt>
<dd>Référence d'ID unique affectée au suivi au moment de sa création. L'ID est représenté au format chaîne GUID (3F2504E0-4F89-41D3-9A0C-0305E82C3301, par exemple) pour les suivis agrégés (complexes) et basés sur les règles.</dd>

<dt>name</dt>
<dd>Nom descriptif du suivi. L'unicité de cette propriété n'est pas garantie.</dd>

<dt>rules</dt>
<dd>Ensemble des règles, comprenant des mots clés de requête et d'autres paramètres, qui définissent les filtres de suivi. Cette propriété s'applique aux suivis basés sur des règles, mais pas aux suivis complexes.</dd>

<dt>state</dt>
<dd>Doit être **Active** ou **Inactive**. Un suivi actif collecte les messages, tandis qu'un suivi inactif ne les collecte pas. Vous pouvez modifier l'état d'un suivi à tout moment.

Cette propriété ne s'applique pas aux suivis complexes.</dd>

<dt>trackIds</dt>
<dd>Ensemble d'ID de suivi. Cette propriété s'applique uniquement aux suivis complexes.</dd>

<dt>type</dt>
<dd>Indique s'il s'agit d'un suivi basé sur des règles (**Rule**) ou d'un suivi complexe (**Aggregated**).

Pour plus d'informations sur les propriétés du suivi, y compris sur les opérations de suivi et le schéma de modèle, voir la documentation de l'API REST {{site.data.keyword.twittershort}}.</dd>
</dl>

