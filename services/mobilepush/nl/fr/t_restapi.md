---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilisation des API REST
{: #push-api-rest}
Dernière mise à jour : 16 janvier 2017
{: .last-updated}

Vous pouvez utiliser une interface de programmation d'application REST (Representational State Transfer) pour {{site.data.keyword.mobilepushshort}}. Vous
pouvez également utiliser le
SDK et l'[API Push ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lienexterne")](https://mobile.{DomainName}/imfpush/ "Icône de lien externe"){: new_window} pour développer plus encore vos applications client. 


Avec l'API REST Push, les applications serveur de back end et les clients peuvent accéder à des fonctions {{site.data.keyword.mobilepushshort}}.

- Enregistrements d'appareil
- Enregistrements
- Messages
- Abonnements
- Balises
- Webhooks

Pour obtenir l'URL de base pour l'API REST, procédez comme suit :

1. Créez une application de back end dans la section Conteneurs boilerplate du catalogue Bluemix®, en choisissant MobileFirst Services Starter, ce qui a pour effet de lier le service {{site.data.keyword.mobilepushshort}} à l'application. Vous pouvez aussi créer une instance de service de Push et la laisser non liée. 
1. Dans la page principale du tableau de bord Bluemix, accédez à la zone **Applications** et sélectionnez votre application.
3. Cliquez sur **OPTIONS POUR APPLICATION MOBILE**. Les valeurs de route et d'identificateur global unique de l'application sont affichées au début de la page des détails de votre application. L'écran Afficher les données d'identification affiche des informations sur la valeur confidentielle AppSecret. Vous pouvez obtenir la valeur confidentielle d'application depuis les options pour application mobile ainsi que la valeur confidentielle de client pour certaines des interfaces API.

Vous pouvez aussi utiliser la ligne de commande pour obtenir les données d'identification pour le service :

```
    cf create-service-key {push_instance_name} {key_name}

 cf service-key {push_instance_name} {key_name}
```
	{: codeblock}

## En-tête Accept-Language
{: #push-api-rest-accept}

L'en-tête "Accept-Language" spécifie la langue à utiliser pour les messages d'erreur générés par
l'[API REST
Push![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://mobile.{DomainName}/imfpush/ "Icône de lien externe"){: new_window}. Les langues suivantes sont prises en charge pour les messages d'erreur : chinois (simplifié), chinois (traditionnel), anglais (Etats-Unis), allemand, français, italien, japonais, coréen, portugais et espagnol.

## Valeur confidentielle d'application 
{: #push-api-rest-secret}

Quand une application est liée à {{site.data.keyword.mobilepushshort}}, le service génère une valeur confidentielle appSecret (clé unique) et la transmet dans l'en-tête de réponse. Si vous utilisez l'API REST IBM {{site.data.keyword.mobilepushshort}} for Bluemix, servez-vous de la référence de l'API REST pour savoir quelles sont les API que vous devez sécuriser. Pour
plus d'informations, reportez-vous à la rubrique [API REST Push
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://mobile.{DomainName}/imfpush/ "Icône de lien externe"){: new_window}.

L'en-tête de demande doit contenir la valeur appSecret. Si tel n'est pas le cas, le serveur renvoie le code d'erreur 401 Unauthorized. Quand {{site.data.keyword.mobilepushshort}} est ajouté à une application, un ID d'application spécifique est créé. Dans le cadre de la réponse, vous obtenez un en-tête intitulé appSecret (valeur confidentielle d'application) qui est utilisé pour créer des balises ou envoyer des messages. L'opération est effectuée via des services dans le catalogue ou le conteneur boilerplate.

Pour obtenir la valeur appSecret :

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
       "appSecret": "8dac71a5-2219-42b3-a9f3-dbb828ba1f04",
       }
     }
    ]
    }
```
	{: codeblock} 


##Filtres des API REST Push
{: #push-api-rest-filters}

Les filtres définissent un critère de recherche permettant de restreindre les données qui sont renvoyées depuis une API GET de {{site.data.keyword.mobilepushshort}}. Appliquez les filtres au résultat de l'opération Get à filtrer. Le filtre restreint le nombre d'entrées incluses dans le résultat. Ainsi, vous pouvez utiliser un filtre pour rechercher des balises commençant par "test". 

Les filtres peuvent être générés en utilisant la syntaxe suivante :

**nom** : nom de la zone sur laquelle le filtre est appliqué.

**opérateur** : == (correspondance exacte) ou =@ (contient une sous-chaîne) qui décrit la correspondance de filtre à utiliser.

**expression** : valeurs à inclure dans le résultat.

Dans une expression, les virgules et les barres obliques inversées doivent être précédées d'une barre oblique inversée.

Si vous utilisez plusieurs filtres, vous pouvez les combiner avec la logique AND ou OR.

- Pour la logique AND, utilisez plusieurs filtres dans la requête.
- Pour la logique OR, utilisez une virgule (,) dans l'expression de filtre.
- Pour la logique AND et OR : une requête simple peut comporter les deux logiques, AND et OR. Chaque filtre est évalué individuellement avant que les filtres ne soient combinés dans une expression AND.

Pour l'API GET d'appareil, les combinaisons suivantes sont prises en charge :
-Le nom est la zone de plateforme.
- Sauf pour platform, l'opérateur peut être == ou =@
- Pour platform, l'opérateur doit être ==. Si l'opérateur =@ est utilisé, la valeur peut être une sous-chaîne.
- Si l'opérateur == est utilisé, la valeur doit être une chaîne qui correspond exactement.

Pour l'API GET d'abonnement, les combinaisons suivantes sont prises en charge :

- Le nom peut être l'une des zones suivantes : tagName ou deviceId
- Sauf pour platform, l'opérateur peut être == ou =@
- Pour platform, l'opérateur doit être ==
- Si l'opérateur =@ est utilisé, la valeur peut être une sous-chaîne. Si l'opérateur == est utilisé, la valeur doit être une chaîne qui correspond exactement.
- Pour l'API GET d'étiquette, les combinaisons suivantes sont prises en charge :
- Le nom peut être l'une des zones suivantes : “name” ou “description”
- Si l'opérateur =@ est utilisé, la valeur peut être une sous-chaîne.
- Si l'opérateur == est utilisé, la valeur doit être une chaîne qui correspond exactement.


##Codes de réponse {{site.data.keyword.mobilepushshort}}
{: #push-api-response-codes}

Status: 405 Method Not Allowed - Appropriate method expected.
