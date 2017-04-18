---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---

Le service {{site.data.keyword.amafull}} est remplacé par le service {{site.data.keyword.appid_full}}.

# Authentification personnalisée d'application Web
{: #custom-web}

Ajoutez une authentification personnalisée à votre application Web

## Avant de commencer
{: #before-you-begin}

Vous devez disposer des éléments suivants :
* Une application Web avec un noeud final `/apps/:Guid/<RealmName>/handleChallengeAnswer`, qui retourne une identité utilisateur une fois l'authentification effectuée. La structure JSON d'identité utilisateur doit être la suivante :

   ```json
  userIdentity: {
  userName: <username>,
  displayName: <displayName>;
 };
```
* Une instance d'une application {{site.data.keyword.Bluemix_notm}} qui est protégée par le service {{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).



## Configuration d'une application {{site.data.keyword.amashort}} pour authentification personnalisée


1. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.
1. Cliquez sur la vignette {{site.data.keyword.amashort}}. Le tableau de bord {{site.data.keyword.amashort}} se charge.
1. Cliquez sur la vignette Personnalisé.
1. Renseignez les zones **domaine personnalisé**, **URL du fournisseur d'identité personnalisé** et
**redirect_uri**. Cliquez sur Enregistrer.

## Utilisation de {{site.data.keyword.amashort}} pour authentification Web personnalisée

Pour démarrer le processus d'autorisation :

1. Redirigez l'utilisateur depuis votre application Web vers le noeud final suivant du serveur d'autorisation :

    https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  en utilisant les paramètres de requête suivants :
   ```
   response_type=’authorization_code’
   client_id= <bluemix\_app\_guid>
   redirect_uri= <uri for the redirect after getting an authorization code>
   scope= ‘openid’
   state= <state>
   ```

    Le paramètre `state`, qui n'est pas utilisé pour l'instant, n'a pas besoin d'être renseigné.

    Le paramètre `redirect_uri` détermine la redirection après une authentification aboutie ou échouée de votre fournisseur d'identité personnalisé.

1. Après redirection au noeud final d'autorisation, vous accédez à un formulaire de connexion. Entrez le nom d'utilisateur et le mot de passe pour initier l'authentification face à votre fournisseur d'identité ainsi qu'une redirection vers l'URI `redirect_uri`.
La réponse retournée après une authentification réussie contient le code d'autorisation dans les paramètres de requête de la demande.

4. Effectuez une requête `POST` sur le noeud final de jeton du serveur d'autorisation :

 https://imf-newauthserver.bluemix.net/*oauth/v2/token

 en utilisant les paramètres de requête suivants :
 ```
 grant_type = 'authorization_code'
 client_id = <bluemix_app_guid>
 redirect_uri = <redirect_uri>
 code = <authorization code>
 ```
  Le paramètre `redirect_uri` doit correspondre au paramètre `redirect_uri` de l'étape 1. Le code d'autorisation a été retourné par la demande à l'étape 2.

  Prenez soin d'envoyer cette demande `POST` dans les 10 minutes, puisque le code d'accord n'est valide que pendant 10 minutes maximum.

Le corps de la réponse `POST` contient les paramètres *access_token* et *id_token* codés en base 64.

## Test de l'authentification


Vous pouvez maintenant commencer à effectuer des demandes dans vos ressources protégées.
Toutes ces demandes doivent contenir le paramètre `access_token`.
Envoyez le jeton d'accès vers la zone d'en-tête `the-Authorization-request`.
