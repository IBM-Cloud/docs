---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

**Important : Le service {{site.data.keyword.amafull}} est remplacé par le service {{site.data.keyword.appid_full}}.**

# Authentification des utilisateurs à l'aide des données d'identification Facebook
{: #facebook-auth-overview}

Vous pouvez configurer le service {{site.data.keyword.amafull}} pour protéger des ressources en utilisant
Facebook comme fournisseur d'identité. Les utilisateurs de votre application mobile ou Web peuvent utiliser leurs données d'identification Facebook
pour l'authentification.

{:shortdesc}

**Important** : il n'est pas nécessaire d'installer séparément le SDK client fourni par Facebook. Le SDK Facebook est installé automatiquement par les gestionnaires de dépendances lors de la configuration du SDK client de {{site.data.keyword.amashort}} Facebook.

## Flux des demandes {{site.data.keyword.amashort}}
{: #mca-facebook-sequence}

### Flux de demande client mobile

Le diagramme suivant représente l'intégration entre {{site.data.keyword.amashort}} et Facebook pour l'authentification, depuis une application client mobile.

![Diagramme de flux de demande de client mobile](images/mca-sequence-facebook.jpg)

* Utilisez le SDK client {{site.data.keyword.amashort}} pour envoyer une requête à vos ressources de back end protégées par le SDK serveur
{{site.data.keyword.amashort}}.
* Le SDK serveur de {{site.data.keyword.amashort}} détecte une demande non autorisée et renvoie une demande d'autorisation HTTP 401.
* Le SDK client de {{site.data.keyword.amashort}} détecte automatiquement l'erreur HTTP 401 et lance le processus d'authentification.
* Le SDK client {{site.data.keyword.amashort}} contacte le service {{site.data.keyword.amashort}} et réclame un en-tête d'autorisation.
* Le service {{site.data.keyword.amashort}} demande au client de s'authentifier auprès de Facebook en fournissant une demande d'authentification.
* Le SDK client de {{site.data.keyword.amashort}} utilise le SDK Facebook pour lancer le processus d'authentification. Lorsque l'authentification aboutit, le SDK Facebook renvoie un jeton d'accès Facebook.
* Le jeton d'accès Facebook est considéré comme une réponse à la demande d'authentification. Il est envoyé au service {{site.data.keyword.amashort}}.
* Le service valide la réponse à la demande d'authentification auprès des serveurs Facebook.
* Si la validation aboutit, le service {{site.data.keyword.amashort}} génère un en-tête d'autorisation et le renvoie au SDK client de {{site.data.keyword.amashort}}. L'en-tête d'autorisation contient deux jetons : un jeton qui contient des informations sur les droits d'accès, et un autre jeton qui contient des informations sur l'utilisateur, l'appareil et l'application.
* A partir de ce moment, toutes les demandes faites avec le SDK client de {{site.data.keyword.amashort}} contiennent un nouvel en-tête d'autorisation.
* Le SDK client de {{site.data.keyword.amashort}} renvoie automatiquement la demande d'origine qui avait déclenché le flux d'autorisation.
* Le SDK serveur {{site.data.keyword.amashort}} extrait l'en-tête d'autorisation de la requête, la valide auprès du service
{{site.data.keyword.amashort}} et octroie l'accès à une ressource de back end.

### Flux de demande d'une application Web {{site.data.keyword.amashort}}
{: #mca-facebook-web-sequence}

Le flux de demande d'une application Web {{site.data.keyword.amashort}} est similaire à celui d'un client d'une application mobile. Toutefois,
{{site.data.keyword.amashort}} protège l'application et non pas une ressource de back end {{site.data.keyword.Bluemix_notm}}.

  * La requête initiale est envoyée par l'application Web (depuis un formulaire de connexion, par exemple).
  * La redirection finale vise la zone protégée de l'application Web elle-même et non pas une ressource de back end protégée.


## Création d'une application sur le site Web Facebook for Developers
{: #facebook-appID}

Pour commencer à utiliser Facebook en tant que fournisseur d'identité, créez une application sur le site Web Facebook for Developers. Durant ce processus, un ID d'application Facebook est créé. Il s'agit d'un identificateur unique utilisé par Facebook pour savoir quelle application tente de se connecter.

Vous aurez besoin de cette valeur pour
configurer l'authentification Facebook
pour votre application mobile ou Web.

1. Accédez au site [Facebook for Developers ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developers.facebook.com){: new_window}.

1. Ouvrez la liste déroulante **Mes applications** et sélectionnez **Ajouter une application**.

1. Entrez des valeurs dans les zones relatives au nom d'affichage et aux valeurs e-mail de contact puis choisissez une catégorie dans la liste déroulante.

1. Cliquez sur la commande de création d'un nouvel ID d'application.

1. Un contrôle de sécurité peut apparaître. Effectuez l'action requise.

1. La page relative à la configuration du produit s'affiche. Copiez l'**ID d'appli** qui s'affiche.

## Etapes suivantes
{: #next-steps}

* [Activation de l'authentification Facebook pour les applications Android](facebook-auth-android.html)
* [Activation de l'authentification Facebook pour les applications iOS (SDK Swift)](facebook-auth-ios-swift-sdk.html)
* [Activation de l'authentification Facebook pour les applications Cordova](facebook-auth-cordova.html)
