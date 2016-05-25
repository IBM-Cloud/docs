---

copyright :
   years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Agrégation des API
{: #api_aggregation}

*Dernière mise à jour : 31 mars 2016*

Certaines API d'Insights for Weather peuvent être agrégées. Une agrégation permet d'associer plusieurs appels d'API atomiques dans la même demande HTTP.
{: shortdesc}

Un appel d'API atomique fait référence aux API qui disposent d'un alias pour les agrégations. Si cet alias est disponible, il est indiqué dans le guide d'utilisation de l'API, à la section relative au format de l'URL. Par exemple, l'API de prévisions standard journalière dispose de l'alias d'agrégation`v2fcstdaily10`, qui peut être utilisé pour extraire les prévisions journalières sur 10 jours dans le contexte d'une demande agrégée.

Les agrégations sont soumises aux restrictions suivantes :

* La taille globale de la réponse non compressée pour l'ensemble de l'agrégation doit être inférieure à 1 mégaoctet.
* La longueur des adresses URL doit être inférieure à environ 4096 caractères (y compris le protocole, le nom d'hôte,
le chemin d'accès et la chaîne de la requête).
* Vous pouvez agréger jusqu'à 10 API atomiques.

**Remarque :** Si la demande ou la réponse ne respecte pas l'une de ces restrictions, vous recevez une
réponse d'erreur avec un code HTTP 500 (généralement 500 ou 502, bien que d'autres codes soient possibles).


## URL d'agrégation d'API
L'URL d'agrégation d'API commence par `/v2/aggregate/`, suivi des alias séparés par des points-virgules.
Par exemple, pour agréger l'API de prévisions journalières sur 10 jours (`v2fcstdaily10`) et les observations en cours (`v2obscurrent`), utilisez la syntaxe suivante :

```
/v2/aggregate/v2fcstdaily10;v2obscurrent
```

## Règles des paramètres de requête des API atomiques et des agrégations
Des paramètres de requête sont requis pour toutes les demandes. Les paramètres de requête des agrégations sont transmis de la même manière que ceux des appels d'API atomique, avec quelques règles supplémentaires. Les sections suivantes décrivent la façon dont ils peuvent être appliqués pour former différentes agrégations.

### Définissez des paramètres de requête qui s'appliquent à toutes les API atomiques

La forme la plus simple d'une agrégation est
lorsque les paramètres de requête s'appliquent à toutes les API atomiques. Dans ce cas, les paramètres de requête ont le format standard suivant : `?param1=value1&amp;param2=value2`.

L'exemple qui suit applique `geocode=31.44,84.33&amp;language=en&amp;units=e` à la demande pour les API atomiques `v2fcstdaily10` et `v2obscurrent` :


```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?geocode=31.44,84.33&amp;language=en&amp;units=e
```

### Précisez quelles API atomiques reçoivent quels paramètres de requête

Si vous devez définir des paramètres pour certaines API atomiques, les paramètres de requête peuvent utiliser la notation positionnelle de `?R1.param1=value1&amp;R2.param2=value2`. Ce format utilise `param1` pour la première API atomique et `param2` pour la seconde API atomique. 

L'exemple qui suit applique `geocode=31.44,84.33&amp;language=en&amp;units=e` à `v2fcstdaily10` et  `geocode=44.44,50.23&amp;language=en&amp;units=e` à `v2obscurrent`.

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?R1.geocode=31.44,84.33&amp;R2.geocode=44.44,50.23&amp;language=en&amp;units=e
```

### Regroupez les paramètres de requête de certaines API atomiques

Vous pouvez regrouper des paramètres à l'aide d'une
notation positionnelle dans laquelle ils sont séparés par des virgules : `?R1,R2.param1=value1&amp;param2=value2`.
Ce format utilise `param1` pour la première et la deuxième API atomiques et `param2` pour toutes les API atomiques. 

L'exemple qui suit applique `geocode=34.06,84.21&amp;language=enUS&amp;units=e` à `v2fcstdaily10` et `v2obscurrent`. Il applique `geocode= 33.06,81.11&amp;language=enUS&amp;units=e` à `v2loc` :

```
https://twcservice.mybluemix.net/api/weather/v2 /aggregate/v2fcstdaily10;v2obscurrent;v2loc ?R1,R2.geocode= 34.06,84.21 &amp;R3.geocode= 33.06,81.11 &amp;language=enUS&amp;units=e
```

### Demandez la même ressource plusieurs manières

Vous pouvez demander la même ressource de plusieurs manières, par
exemple dans plusieurs langues ou avec plusieurs unités de mesure. Avec ce format, l'API atomique peut être répétée dans la demande `/v2/aggregate/v2fcstdaily10;v2fcstdaily10`, et la notation positionnelle des paramètres peut être utilisée pour indiquer la manière d'interroger telle ou telle API : `?R1.param1=value1&amp;R2.param1=value2`. Dans ce cas, l'utilisateur reçoit la même ressource, mise en forme ou traduite de différentes manières.

L'exemple qui suit applique `geocode=31.44,84.33&amp;language=en&amp;units=e` à la première occurrence de `v2fcstdaily10` et `geocode=31.44,84.33&amp;language=fr&amp;units=m` à la seconde occurrence de `v2fcstdaily10` :

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?geocode=31.44,84.33&amp;R1.language=en&amp;R2.language=fr&amp;R1.units=e&amp;R2.units=m
```

L'exemple qui suit applique `geocode=31.44,84.33&amp;language=en&amp;units=e` à la première occurrence de `v2fcstdaily10` et
`geocode=33.54,85.43&amp;language=en&amp;units=e` à la seconde occurrence de `v2fcstdaily10` pour extraire les mêmes données pour plusieurs lieux :


```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?R1.geocode=31.44,84.33&amp;R2.geocode=33.54,85.43&amp;language=en&amp;units=e
```




