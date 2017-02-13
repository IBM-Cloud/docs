---

copyright:
  year: 2016, 2017
lastupdated: "2017-01-08"

---

# Activation de l'authentification Google pour les applications Web
{: #google-auth-web}

Utilisez Google Sign-In pour authentifier les utilisateurs sur votre application Web.


## Avant de commencer
{: #before-you-begin}

Vous devez disposer des éléments suivants :
* Une application Web.
* Une instance d'une application {{site.data.keyword.Bluemix_notm}} qui est protégée par le service {{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).

## Configuration d'une application Google pour votre site Web
Pour commencer à utiliser Google en tant que fournisseur d'identité, vous devez créer un projet dans [Google Developer Console](https://console.developers.google.com). Une partie de la création d'une projet consiste à obtenir un ID client et une valeur confidentielle Google. L'ID client et la valeur confidentielle Google sont les identificateurs uniques de votre application utilisés par l'authentification Google et nécessaires pour configurer l'application {{site.data.keyword.Bluemix_notm}}.

1. Créez un projet en utilisant l'API Google+.
1. Créez les données d'identification en utilisant **OAuth**. Pour ce faire, vous devez :
    * Sélectionner le type d'application correspondant à une application Web.
    * Fournir la valeur relative aux identificateurs URI de redirection autorisés :

     https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback
1. Terminez la procédure de création des données d'identification et prenez note de l'ID client et de la valeur confidentielle Google.


## Configuration de {{site.data.keyword.amashort}} pour l'authentification Google
Maintenant que vous disposez d'un ID d'application et d'une valeur confidentielle Google, vous pouvez activer l'authentification Google dans le tableau de bord {{site.data.keyword.amashort}}.

1. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.
1. Cliquez sur la vignette {{site.data.keyword.amashort}}. Le tableau de bord {{site.data.keyword.amashort}} se charge.
1. Cliquez sur la vignette Google.
1. Entrez l'ID client et la valeur confidentielle Google et enregistrez.


## Utilisation de {{site.data.keyword.amashort}} pour l'authentification Web Google
Pour démarrer le processus d'autorisation :

1. Effectuez une redirection depuis votre application Web vers le noeud final suivant du serveur d'autorisation :  
  https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  en utilisant les paramètres de requête suivants :
	```
   response_type='authorization_code'
   client_id= <bluemix_app_guid>
   redirect_uri= <uri which you want to return to after getting a grant code>
   scope= ‘openid’
   state= <state>
	```

  Le paramètre `state`, qui n'est pas utilisé pour l'instant, n'a pas besoin d'être renseigné.

  L'URI de paramètre `redirect_uri` permet une redirection après une authentification aboutie ou échouée avec Google.
  La réponse retournée après une redirection contient le code d'autorisation dans les paramètres de requête de la demande.
1. Effectuez une demande `POST` vers le noeud final de jeton du serveur d'autorisation :

 https://imf-newauthserver.bluemix.net/oauth/v2/token


  en utilisant les paramètres de requête suivants :

	```
  	grant_type=’authorization_code’
    client_id= < bluemix_app_guid >
    redirect_uri= <redirect_uri >
    code= <authorization code>
	```
  Le paramètre `redirect_uri` doit correspondre au paramètre `redirect_uri` de l'étape 1 et la valeur `<authorization code>` est reçue depuis la réponse.
  Prenez soin d'envoyer cette demande `POST` dans les 10 minutes, puisque le code d'accord n'est valide que pendant 10 minutes maximum.

Le corps de la réponse `POST` doit contenir les paramètres `access_token` et `id_token` codés en base 64.

## Test de l'authentification

Vous pouvez maintenant commencer à effectuer des demandes dans vos ressources protégées.
Toute demande de ce type doit contenir le jeton d'accès dans la zone d'en-tête de demande d'autorisation.
