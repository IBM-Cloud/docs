---

copyright:
 years: 2015, 2016

---

# Utilisation des API REST
{: #push-api-rest}

Vous pouvez utiliser une API REST (Representational State Transfer) pour les notifications push. Vous pouvez aussi utiliser le logiciel SDK et les [API Push](https://mobile.{DomainName}/imfpushrestapidocs/) pour développer davantage vos applications client.

Avec l'API REST Push, les applications serveur de back end et les clients peuvent accéder à des fonctions Push.

- Enregistrements de périphérique
- Enregistrements
- Messages
- Abonnements
- Balises

Afin d'obtenir l'adresse URL de base pour l'API REST :

1. Créez une application de back end dans la section Conteneurs boilerplate du catalogue Bluemix, qui lie automatiquement le service Push à cette application. Si vous avez déjà créé une application de back end, veillez à lier l'application au service Push Notifications. 

1. Sur la page principale du tableau de bord Bluemix, accédez dans la zone **Applications**, puis cliquez sur votre appli.

3. Cliquez sur OPTIONS POUR APPLICATION MOBILE. Les valeurs de route et d'identificateur global unique de l'application sont affichées en haut de la page des détails de votre application.



## En-tête Accept-Language
{: #push-api-rest-accept}

L'en-tête "Accept-Language" spécifie la langue à utiliser pour les messages d'erreur qui sont générés par l'[API REST Push](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}. Les langues suivantes sont prises en charge pour les messages d'erreur : chinois (simplifié), chinois (traditionnel), anglais (Etats-Unis), allemand, français, italien, japonais, coréen, portugais et espagnol.

## Valeur confidentielle d'application
{: #push-api-rest-secret}

Lorsqu'une application est liée au service Push Notifications, le service génère une valeur confidentielle d'application (une clé unique) et la transmet dans l'en-tête de réponse. Si vous utilisez l'API REST IBM Push Notifications for Bluemix, consultez la référence de l'API REST pour savoir quelles sont les API que vous devez sécuriser. Pour obtenir des informations sur l'API REST, voir la référence de l'API REST.

L'en-tête de demande doit contenir la valeur confidentielle d'application. Si tel n'est pas le cas, le serveur renvoie le code d'erreur 401 Unauthorized. Lorsque Push Notifications est ajouté à une application, un ID d'application spécifique est créé. Dans le cadre de la réponse, vous obtenez un en-tête appelé appSecret (valeur confidentielle d'application) qui est utilisé pour créer des balises ou envoyer des messages. L'opération est effectuée via des services dans le catalogue ou le conteneur boilerplate.

Pour obtenir la valeur confidentielle d'application :

1. Cliquez sur le *nom d'application* qui est lié au service Push.
2. Cliquez sur le lien **Afficher les données d'identification** pour afficher la valeur confidentielle d'application (ID d'application).

L'écran **Afficher les données d'identification** affiche des informations sur la valeur confidentielle d'application :

```
{
 "imfpush_Dev": [
   {
     "name": "testapp1",
     "label": "imfpush_Dev",
     "plan": "Basic",
     "credentials": {
       "url": "http://imfpush.ng.bluemix.net/imfpush/v1/apps/b615b280-b37e-4042-8815-38a758f234e2",
       "admin_url": "//mobile.ng.bluemix.net/imfpushdashboard/?appGuid=b615b280-b37e-4042-8815-38a758f234e2",
       "appSecret": "8dac71a5-2219-42b3-a9f3-dbb828ba1f04"  
       }
   }
 ]
}
``` 

##Filtres des API REST Push
{: #push-api-rest-filters}

Les filtres définissent un critère de recherche permettant de restreindre les données qui sont renvoyées depuis une API GET de Push. Appliquez les filtres au résultat de l'opération Get à filtrer. Le filtre restreint le nombre d'entrées qui sont incluses dans le résultat. Par exemple, vous pouvez utiliser un filtre pour rechercher une balise qui commence par "test". Vous pouvez générer un filtre avec la syntaxe ci-dessous.

**name**
Nom de la zone à laquelle le filtre est appliqué.

**operator**
== (correspondance exacte) ou =@ (contient une sous-chaîne) qui décrit la correspondance de filtre à utiliser.

**expression**
Valeurs à inclure dans le résultat.

Dans une expression, les virgules et les barres obliques inversées doivent être précédées d'une barre oblique inversée.

Si vous utilisez plusieurs filtres, vous pouvez les combiner avec la logique AND ou OR.

- Pour la logique AND, utilisez plusieurs filtres dans la requête.
- Pour la logique OR, utilisez une virgule (,) dans l'expression de filtre.
- Pour la logique AND et OR : une requête simple peut comporter les deux logiques, AND et OR. Chaque filtre est évalué individuellement avant que les filtres ne soient combinés dans une expression AND.

Pour l'API GET de périphérique, les combinaisons suivantes sont prises en charge :
- Le nom est la zone de plateforme.
- Sauf pour platform, l'opérateur peut être == ou =@
- Pour platform, l'opérateur doit être ==. Si l'opérateur =@ est utilisé, la valeur peut être une sous-chaîne.
- Si l'opérateur == est utilisé, la valeur doit être une chaîne qui correspond exactement.

Pour l'API GET d'abonnement, les combinaisons suivantes sont prises en charge :

- Le nom peut être l'une des zones suivantes : tagName ou deviceId
- Sauf pour platform, l'opérateur peut être == ou =@
- Pour platform, l'opérateur doit être ==
- Si l'opérateur =@ est utilisé, la valeur peut être une sous-chaîne. Si l'opérateur == est utilisé, la valeur doit être une chaîne qui correspond exactement.
- Pour l'API GET de balise, les combinaisons suivantes sont prises en charge :
- Le nom peut être l'une des zones suivantes : “name” ou “description”
- Si l'opérateur =@ est utilisé, la valeur peut être une sous-chaîne.
- Si l'opérateur == est utilisé, la valeur doit être une chaîne qui correspond exactement.
