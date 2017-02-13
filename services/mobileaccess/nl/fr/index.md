---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à {{site.data.keyword.amashort}}
{: #gettingstarted}

Ajoutez une fonctionnalité de sécurité à votre application mobile avec le service {{site.data.keyword.amafull}}. Vous pouvez configurer une autorisation client pour accéder à des ressources de back end protégées s'exécutant sur {{site.data.keyword.Bluemix}}. Utilisez des fournisseurs d'identité (Google et Facebook) ou des identités personnalisées pour authentifier les utilisateurs et accorder un accès aux ressources de back-end protégées et aux applications Web.
{:shortdesc}

**Remarque :** Le service {{site.data.keyword.amashort}} était dénommé auparavant Advanced Mobile Access.


Mise en route du service {{site.data.keyword.amashort}} :

1. Utilisez l'une des options suivantes pour créer un service lié ou non lié :
 * Créez une application {{site.data.keyword.Bluemix_notm}} à l'aide du conteneur boilerplate de **MobileFirst Services Starter** dans le catalogue. Cela crée un service {{site.data.keyword.amashort}} lié à une application back end {{site.data.keyword.Bluemix_notm}}.
 * Créez un service {{site.data.keyword.amashort}} à l'aide de la console {{site.data.keyword.amashort}}.  Vous pouvez lier le service à une
application back end existante et le configurer dans la console {{site.data.keyword.amashort}}.

   Quand vous utilisez MobileFirst Services Starter, vous obtenez une instance du contexte d'exécution Node.js qui s'exécute sur IBM {{site.data.keyword.Bluemix_notm}} pour implémenter votre logique de back end personnalisée. Un ensemble de services mobiles de base qui fournissent des fonctions de sécurité, de données, de push et de surveillance et sont liés à cette appli Node.js. Une fois l'application Node.js {{site.data.keyword.Bluemix_notm}} créée, vous pouvez configurer votre environnement de développement et commencer à utiliser les logiciels SDK de {{site.data.keyword.Bluemix_notm}} Mobile Services. Vous pouvez utiliser les logiciels SDK pour accéder aux services qui sont liés à votre application en cloud à l'aide de simples appels d'API.

	Pour plus d'informations sur la création et l'utilisation de projets, d'applications et de
services, voir [tableau de bord IBM Bluemix Mobile](https://console.{DomainName}/docs/mobile/index.html).

2. Sécurisez les ressources côté serveur.

   Protégez vos ressources de back end mobile s'exécutant sous les contextes d'exécution Node.js ou Liberty for Java&trade; avec sécurité OAuth activée pour les applications mobiles. Pour plus d'informations, voir [Protection des ressources](protecting-resources.html).
   Pour plus d'informations sur l'application de back end mobile par défaut, reportez-vous à l'exemple d'application [bms-hellotodo-strongloop ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop "Icône de lien externe"){: new_window}.

3. Configurez votre environnement principal de développement {{site.data.keyword.amashort}}.

  ####Développement client
  {: #client-development}

	Vous pouvez ajouter le SDK {{site.data.keyword.amashort}} à votre application Android, iOS ou Cordova existante, comme suit :
   * Android : Exemple ([Configuration du SDK Android](getting-started-android.html)) [ ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "Icône de lien externe"){: new_window}
    * iOS (SDK Swift) : Exemple ([Configuration du SDK Swift iOS](getting-started-ios-swift-sdk.html)) [![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "Icône de lien externe"){: new_window}    
   * Cordova : Exemple ([configuration du plug-in Cordova](getting-started-cordova.html)) [ ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication "Icône de lien externe"){: new_window}


 ####Développement Web
 {: #web-development}

   Le service {{site.data.keyword.amashort}} peut protéger votre application Web, sans requérir de SDK spécial. Vous pouvez exploiter divers fournisseurs d'identité, en sus de la protection assurée par le service {{site.data.keyword.amashort}}. L'intégration {{site.data.keyword.amashort}} permet à toute application Web, quelle que soit la technologie qu'elle implémente, de tirer parti du protocole OAuth2. Pour plus d'informations sur la configuration de votre application Web {{site.data.keyword.amashort}} pour accéder au service {{site.data.keyword.amashort}}  via des fournisseurs d'identité différents, voir :

   * [Activation de l'authentification Facebook pour les applications Web](facebook-auth-web.html)
   * [Activation de l'authentification Google pour les applications Web](google-auth-web.html)
   * [Activation de l'authentification custom pour les applications Web](custom-auth-web.html)

**Facultatif :** configurez un fournisseur d'identité pour votre application. Vous ne pouvez configurer qu'un fournisseur d'identité par application. La configuration d'un fournisseur d'identité permet aux utilisateurs de votre application mobile de se connecter avec leur compte Facebook ou Google+ existant. Ou bien, vous pouvez définir le mode de connexion des utilisateurs en créant une authentification personnalisée.
   * [Authentification des utilisateurs à l'aide des données d'identification Facebook](facebook-auth-overview.html)
   * [Authentification des utilisateurs avec des données d'identification Google](google-auth-overview.html)
   * [Authentification des utilisateurs en utilisant un fournisseur d'identité personnalisé](custom-auth.html)

## Tutoriels et exemples
{: #samples}

* [Exemple android-helloauthentication ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "Icône de lien externe"){: new_window}
* [Exemple ios-helloauthentication (SDK Swift) ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "Icône de lien externe"){: new_window}

## Logiciel SDK
{: #sdk}

* [SDK Core (Android) ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core "Icône de lien externe"){: new_window}

* [Exemple ios-helloauthentication (SDK Swift) ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "Icône de lien externe"){: new_window}

* [Exemple simple - Authentification personnalisée ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "Icône de lien externe"){: new_window}

* [Exemple avancé - Authentification personnalisée ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management "Icône de lien externe"){: new_window}


