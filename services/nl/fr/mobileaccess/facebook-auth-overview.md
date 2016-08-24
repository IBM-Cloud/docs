---

copyright:
  years: 2015, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Authentification des utilisateurs à l'aide des données d'identification Facebook
{: #facebook-auth-overview}

*Dernière mise à jour : 15 juin 2016*
{: .last-updated}

Vous pouvez configurer le service {{site.data.keyword.amashort}} pour protéger des ressources en utilisant
Facebook comme fournisseur d'identité. Les utilisateurs de votre application mobile ou Web peuvent utiliser leurs données d'identification Facebook
pour l'authentification.
{:shortdesc}

**Important** : il n'est pas nécessaire d'installer séparément le SDK fourni par Facebook. Celui-ci est installé automatiquement par les gestionnaires de dépendances lors de la configuration du SDK client de {{site.data.keyword.amashort}}.

## Flux des demandes {{site.data.keyword.amashort}}
{: #mca-facebook-sequence}

Le diagramme simplifié suivant représente l'intégration entre {{site.data.keyword.amashort}} et Facebook pour l'authentification.

![image](images/mca-sequence-facebook.jpg)

1. Utilisez le SDK client {{site.data.keyword.amashort}} pour envoyer une requête à vos ressources de back end protégées par le SDK serveur
{{site.data.keyword.amashort}}.
* Le SDK serveur de {{site.data.keyword.amashort}} détecte une demande non autorisée et renvoie une demande d'autorisation HTTP 401.
* Le SDK client de {{site.data.keyword.amashort}} détecte automatiquement l'erreur HTTP 401 et lance le processus d'authentification.
* Le SDK client {{site.data.keyword.amashort}} contacte le service {{site.data.keyword.amashort}} et réclame un en-tête d'autorisation.
* Le service {{site.data.keyword.amashort}} demande au client de s'authentifier auprès de Facebook en fournissant une demande d'authentification.
* Le SDK client de {{site.data.keyword.amashort}} utilise le SDK Facebook pour lancer le processus d'authentification. Lorsque l'authentification aboutit, le SDK Facebook renvoie un jeton d'accès Facebook.
* Le jeton d'accès Facebook est considéré comme une réponse à la demande d'authentification. Il est envoyé au service {{site.data.keyword.amashort}}.
* Le service valide la réponse à la demande d'authentification auprès des serveurs Facebook.
* Si la validation aboutit, le service {{site.data.keyword.amashort}} génère un en-tête d'autorisation et le renvoie au SDK client de {{site.data.keyword.amashort}}. L'en-tête d'autorisation contient deux jetons : un jeton qui contient des informations sur les droits d'accès, et un autre jeton qui contient des informations sur l'utilisateur, le périphérique et l'application.
* A partir de ce moment, toutes les demandes faites avec le SDK client de {{site.data.keyword.amashort}} contiennent un nouvel en-tête d'autorisation.
* Le SDK client de {{site.data.keyword.amashort}} renvoie automatiquement la demande d'origine qui avait déclenché le flux d'autorisation.
* Le SDK serveur {{site.data.keyword.amashort}} extrait l'en-tête d'autorisation de la requête, la valide auprès du service
{{site.data.keyword.amashort}} et octroie l'accès à une ressource de back end.

## Flux de requête d'une application Web {{site.data.keyword.amashort}}
{: #mca-facebook-sequence}
Le flux de requête d'une application Web {{site.data.keyword.amashort}} est similaire à celui d'un client d'une application mobile. Toutefois,
{{site.data.keyword.amashort}} protège l'application et non pas une ressource de back end {{site.data.keyword.Bluemix_notm}}.

  * La requête initiale est envoyée par l'application Web (depuis un formulaire de connexion, par exemple).
  * La redirection finale vise l'application Web elle-même et non pas une ressource de back end protégée. 



## Obtenez un ID d'application Facebook dans le portail des développeurs Facebook.
{: #facebook-appID}

Pour commencer à utiliser Facebook en tant que fournisseur d'identité, vous devez créer une application dans le portail Facebook Developer. Au cours de ce processus, vous obtenez un ID d'application Facebook, qui est un identificateur unique qui permet à Facebook de savoir quelle application tente de se connecter.

1. Ouvrez le [portail Facebook Developer](https://developers.facebook.com).

1. Cliquez sur **My Apps (Mes applis)** dans le menu supérieur et sélectionnez **Create a new app (Créer une appli)**.
Sélectionnez une application iOS ou Android et cliquez sur **Ignorer et créer un ID d'application** dans l'écran suivant.

1. Définissez le nom d'affichage de votre application et sélectionnez une catégorie. Cliquez sur **Create App ID (Créer l'ID d'appli)** pour continuer.

1. Copiez l'**ID d'appli** qui s'affiche. Il s'agit de votre ID d'application Facebook.  Vous aurez besoin de cette valeur pour
configurer l'authentification Facebook
avec votre application mobile ou Web.

## Etapes suivantes
{: #next-steps}

* [Activation de l'authentification Facebook pour les applications Android](facebook-auth-android.html)
* [Activation de l'authentification Facebook pour les applications iOS (SDK Swift)](facebook-auth-ios-swift-sdk.html)
* [Activation de l'authentification Facebook pour les applications iOS (SDK Objective-C - Déprécié)](facebook-auth-ios.html)
* [Activation de l'authentification Facebook pour les applications Cordova](facebook-auth-cordova.html)
