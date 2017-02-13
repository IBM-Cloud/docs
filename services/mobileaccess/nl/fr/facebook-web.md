---

copyright:
  year: 2016, 2017
lastupdated: "2017-01-08"

---

# Activation de l'authentification Facebook pour les applications Web
{: #facebook_web}

Utilisez Facebook pour authentifier les utilisateurs sur votre application Web.

## Avant de commencer
{: #facebook-auth-android-before}
Vous devez disposer des éléments suivants :
* Une application Web.  
* Une instance d'une application {{site.data.keyword.Bluemix_notm}} qui est protégée par le service {{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).
* Un ID et une valeur confidentielle d'application Facebook. Pour plus d'informations, voir [Acquisition d'un ID d'application Facebook sur le site Web Facebook for Developer](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).


## Configuration d'une application Facebook pour votre site Web
Pour utiliser Facebook comme fournisseur d'identité dans votre site Web, vous devez ajouter et configurer la plateforme de site Web sur votre application Facebook.

1. Ouvrez votre application Facebook dans le portail Facebook Developer.
1. Prenez note de l'ID d'application et de la valeur confidentielle. Vous en aurez besoin pour configurer votre projet Web pour l'authentification Facebook.
1. Depuis la page **Paramètres**, cliquez sur la commande d'ajout de plateforme et choisissez l'option relative au site Web.
1. Enregistrez les changements.
1. Cliquez sur la commande de connexion à Facebook dans la barre latérale de gauche.
1. Entrez le noeud final de rappel du serveur d'autorisation dans la zone relative aux URI de redirection OAuth valides : https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback. Enregistrez les changements.




# Configuration de {{site.data.keyword.amashort}} pour l'authentification Facebook
Une fois que vous disposez de votre ID d'application et de la valeur confidentielle Facebook, et que votre application Facebook a été configurée pour servir les clients Web, vous pouvez activer l'authentification Facebook dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.

1. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.
1. Cliquez sur la vignette {{site.data.keyword.amashort}}. Le tableau de bord {{site.data.keyword.amashort}} se charge.
1. Cliquez sur la vignette Facebook.
1. Entrez l'ID d'application et la valeur confidentielle Facebook et enregistrez.




## Utilisation de Mobile Client Access pour l'authentification Web Facebook

Pour démarrer le processus d'autorisation :

1. Effectuez une redirection depuis votre application Web vers le noeud final suivant du serveur d'autorisation : https://imf-newauthserver.bluemix.net/oauth/v2/authorization.

1. Ajoutez les paramètres de requête suivants :
   ```
    response_type='authorization_code'
    client_id= <bluemix_app_guid>
    redirect_uri= <uri for redirecting after receiving the authorization code>
    scope= 'openid'
    state= <state>
    ```


  Le paramètre `state`, qui n'est pas utilisé pour l'instant, n'a pas besoin d'être renseigné.
  Le paramètre `redirect_uri` est l'identificateur URI qui permet une redirection après une authentification aboutie ou échouée avec Facebook.

1. Après la redirection au noeud final d'autorisation, Facebook vous soumettra un formulaire de connexion  . Entrez le nom d'utilisateur et le mot de passe pour effectuer la redirection vers l'URI `redirect_uri`.
   La réponse retournée après une redirection contient le code d'autorisation dans les paramètres de requête de la demande.

1. Effectuez une demande `POST` vers le noeud final de jeton du serveur d'autorisation :

  https://imf-newauthserver.bluemix.net/oauth/v2/token

  en utilisant les paramètres de requête suivants :
  ```
  grant_type='authorization_code'
  client_id= <bluemix_app_guid>
  code= <authorization code>
  ```
Le paramètre `redirect_uri` doit correspondre au paramètre `redirect_uri` de l'étape 2.
La valeur `code` correspond au code d'autorisation reçu en réponse à la fin de l'étape 3.
Prenez soin d'envoyer cette demande `POST` dans les 10 minutes, puisque le code d'autorisation  n'est valide que pendant 10 minutes maximum.

  Le corps de la réponse `POST` doit contenir les paramètres `access_token` et `id_token` codés en base 64.

## Test de l'authentification
Vous pouvez maintenant commencer à effectuer des demandes dans vos ressources protégées.
Toute demande de ce type doit contenir le paramètre `access_token` dans la zone d'en-tête de demande d'autorisation.
