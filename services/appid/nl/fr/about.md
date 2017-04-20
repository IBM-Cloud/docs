---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Fonctionnement
{: #about}

Cette rubrique fournit des informations sur les composants, l'architecture et le flux de demandes utilisé par {{site.data.keyword.appid_short_notm}}.
{:shortdesc}


Vous pouvez utiliser le service d'une des manières suivantes :

* Pour ajouter une authentification à vos applications mobiles et Web
* Pour accorder un accès aux ressources de back-end et aux applications Web protégées
* Pour protéger les applications Node.js et Swift hébergées sur {{site.data.keyword.Bluemix_notm}}
* Pour stocker des données utilisateur, telles que les préférences d'application ou des informations de leur profil social public
* Pour utiliser des données stockées afin de construire des applications personnalisées
* Pour protéger les ressources tant face aux utilisateurs authentifiés qu'aux utilisateurs anonymes

**Remarque** : les protocoles implémentés sont totalement compatibles avec Open Connect (OIDC).


## Composants
{: #components}

* Tableau de bord - Permet de télécharger des exemples fonctionnels, de consulter les journaux d'activité, de configurer divers types d'authentification et de fournisseurs d'identité
* SDK client - Permet de construire des applications mobiles et Web utilisant le service pour implémenter l'authentification d'utilisateur
    * Prérequis pour Android : API 25 (ou version ultérieure), Java 8.x, Android SDK Tools 25.2.5 (ou versions ultérieure), Android SDK Platform Tools 25.0.3 (ou version ultérieure), Android Build Tools version 25.0.2
    * Prérequis pour iOS : iOS9 (ou version ultérieure), MacOS 10.11.5, Xcode 8.2
* SDK serveur - Permet de protéger des ressources hébergées sur {{site.data.keyword.Bluemix_notm}}
    * Contextes d'exécution pris en charge : Node.js et Swift

## Présentation de l'architecture
{: #architecture}

Avec {{site.data.keyword.appid_short_notm}}, vous pouvez ajouter un niveau de sécurité à vos applications en demandant aux utilisateurs de se connecter. Vous pouvez également utiliser
le SDK serveur pour protéger vos ressources de back-end.

Le diagramme suivant résume le fonctionnement du service {{site.data.keyword.appid_short_notm}}.

![Diagramme de l'architecture {{site.data.keyword.appid_short_notm}}](/images/appid_architecture2.png)

Figure 1. Diagramme de l'architecture {{site.data.keyword.appid_short_notm}}

<dl>
  <dt> SDK client </dt>
    <dd> Le SDK client fournit une catégorie de demande pour communiquer avec vos ressources de cloud. Le SDK client démarre automatiquement le processus d'authentification lorsqu'il détecte une demande
d'autorisation. </dd>
  <dt> Bluemix </dt>
    <dd>  Le SDK serveur extrait de la demande le jeton d'accès et le valide auprès d'{{site.data.keyword.appid_short_notm}}. Une fois que l'authentification a réussi,
{{site.data.keyword.appid_short_notm}} renvoie l'autorisation et les jetons d'identité à votre application. </dd>
  <dt> Fournisseurs d'identité </dt>
    <dd> Vous pouvez configurer Facebook, Google ou les deux pour authentifier vos applications.  </dd>
</dl>


## Flux de demandes
{: #request}

Le diagramme ci-dessous illustre un flux de demandes depuis le SDK client vers votre application de back-end et les fournisseurs d'identité.

![Flux de demandes {{site.data.keyword.appid_short_notm}}](/images/appidflow.png)


* Utilisez le SDK client {{site.data.keyword.appid_short_notm}} pour soumettre une demande à vos ressources de back-end protégées par le SDK serveur {{site.data.keyword.appid_short_notm}}.
* Le SDK serveur {{site.data.keyword.appid_short_notm}} détecte les demandes dépourvues d'autorisation et renvoie une réponse HTTP 401 une portée d'autorisation.
* Le SDK client détecte automatiquement la réponse HTTP 401 et lance la procédure d'autorisation.
* Lorsque le SDK client contacte le service, le SDK serveur renvoie le widget de connexion si plusieurs fournisseurs d'identité ont été configurés. {{site.data.keyword.appid_short_notm}} appelle le fournisseur d'identité et lui présente son formulaire d'identification ou renvoie un code d'acceptation qui lui permet de s'authentifier si aucun fournisseur d'identité n'a été configuré.
* {{site.data.keyword.appid_short_notm}} demande à l'application client de s'authentifier en répondant à une demande d'authentification.
* Si Facebook ou Google sont configurés et que l'utilisateur se connecte, l'authentification est traitée par le flux du protocole d'autorisation OAuth du fournisseur d'identité correspondant.
* Si l'authentification se conclut par le même code d'accord, celui-ci est envoyé au noeud final du jeton. Le noeud final renvoie deux jetons : un code d'accès et un jeton d'identification. Dès lors, toutes les demandes effectuées avec le SDK client ont le nouvel en-tête d'autorisation obtenu.
* Le SDK client renvoie automatiquement la demande d'origine ayant déclenché le flux d'autorisation.
* Le SDK serveur extrait l'en-tête de l'autorisation depuis la demande, le valide auprès du service et octroie l'accès à une ressource de back-end.
