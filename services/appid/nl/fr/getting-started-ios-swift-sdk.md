---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}


# Configuration du SDK Swift iOS
{: #getting-started-ios}

Construisez vos applications Swift avec le SDK client d'{{site.data.keyword.appid_short}}, initialisez le SDK, authentifiez les utilisateurs et soumettez des demandes à des ressources protégées et non protégées.
{:shortdesc}


## Avant de commencer
{: #before-you-begin}

Vous devez disposer des éléments suivants :
  * Une instance d'{{site.data.keyword.appid_short_notm}}.
  * Votre ID titulaire.
    * Dans l'onglet **Données d'identification pour le service** de votre tableau de bord du service, cliquez sur **Afficher les données d'identification**. Votre ID titulaire est affiché dans la zone **TenantID**. Cette valeur est utilisée pour initialiser votre application.
  * Votre région {{site.data.keyword.Bluemix_notm}}.
  Vous pouvez identifier votre région en recherchant dans l'interface utilisateur. Cette valeur est utilisée pour initialiser votre application.
    <table> <caption> Tableau 1. Régions {{site.data.keyword.Bluemix_notm}} et valeurs de SDK correspondantes</caption>
    <tr>
      <th> Région Bluemix</th>
      <th> Valeur du SDK </th>
    </tr>
    <tr>
      <td> Sud des Etats-Unis</td>
      <td> BMSClient.Region.usSouth </td>
    </tr>
    <tr>
      <td> Sydney </td>
      <td> BMSClient.Region.sydney </td>
    </tr>
    <tr>
      <td> Royaume-Uni </td>
      <td> BMSClient.Region.unitedKingdom </td>
    </tr>
  </table>

  * Projet Xcode (version 8.1 ou ultérieure).
  * CocoaPods (version 1.1.0 ou ultérieure).


## Installation du SDK client d'{{site.data.keyword.appid_short_notm}}
{: #install-appid-sdk}

Le SDK client d'{{site.data.keyword.appid_short_notm}} est distribué avec CocoaPods, un gestionnaire de dépendances pour les projets Swift et Cocoa Objective-C . CocoaPods télécharge des artefacts et les rend disponibles dans votre projet.

1. Créez un projet Xcode ou ouvrez un projet existant.
2. Ouvrez ou créez le fichier Pod dans le répertoire du projet.
3. Sous la cible de votre projet, ajoutez une dépendance pour le pod 'BluemixAppID'. Vérifiez que la commande `use_frameworks!` est également présente sous votre cible.
  Exemple :

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {:pre}

4. Pour télécharger la dépendance `BluemixAppID`, exécutez la commande suivante :

  ```swift
  pod install --repo-update
  ```
  {:pre}

6. Ouvrez votre projet Xcode et activez le partage de chaîne de certificats. Sous **Paramètres du projet**, cliquez sur **Fonctions** > **Partage de chaîne de certificats**.
7. Sous **Paramètres du projet** > **Information** > **Types d'URL**, ajoutez un type d'URL. Renseignez les deux zones de texte **Identificateur** et **Schéma d'URL** avec cette valeur : $(PRODUCT_BUNDLE_IDENTIFIER)


## Initialisation du SDK client d'{{site.data.keyword.appid_short_notm}}
{: #initialize-client-sdk}

1. Ajoutez l'importation suivante à votre fichier AppDelegate.swift:

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. Initialisez le SDK client en transmettant les paramètres d'ID du titulaire et de région à la méthode initialize. Bien que ceci ne soit pas obligatoire, le code d'initialisation est souvent placé dans la méthode application:didFinishLaunchingWithOptions: du AppDelegate (délégué d'application) dans votre application Swift.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.<region>)
  ```
  {:pre}

  * Remplacez ״tenantId״ par l'ID du titulaire pour votre service App ID.
  * Remplacez ״region״ par votre région {{site.data.keyword.appid_short_notm}}.

3. Ajoutez le code suivant à votre fichier AppDelegate.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {;pre}

## Authentification des utilisateurs à l'aide du widget de connexion
{: #authenticate-login}

Une fois que le SDK client d'{{site.data.keyword.appid_short_notm}} est initialisé, vous pouvez authentifier vos utilisateurs en exécutant le widget de connexion. La configuration par défaut du widget de connexion utilise Facebook, Google, ou les deux, comme options d'authentification. Si vous n'en configurez qu'une seule, le widget de connexion ne se lance pas et l'utilisateur est redirigé vers l'écran d'authentification du fournisseur d'identité (IDP) configuré.



1. Ajoutez l'importation suivante au fichier dans lequel vous comptez utiliser le SDK.

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. Exécutez la commande suivante pour lancer le widget.

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //Utilisateur authentifié
      }

      public func onAuthorizationCanceled() {
          //Authentification annulée par l'utilisateur
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Une exception s'est produite
      }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {:pre}

## Accès aux attributs utilisateur
{: #accessing}

En obtenant un jeton d'accès, vous pouvez accéder au noeud final des attributs utilisateur protégés. Ceci est réalisé en utilisant les méthodes d'API suivantes :

  ```
  func setAttribute(key: String, value: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func setAttribute(key: String, value: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  ```
  {:pre}

Lorsqu'un jeton d'accès n'est pas transmis explicitement, {{site.data.keyword.appid_short_notm}} utilise le dernier jeton reçu.

Vous pouvez, par exemple utiliser le code ci-dessous pour définir un nouvel attribut ou prévaloir sur un attribut existant :

  ```
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Attributs reçus comme dictionnaire
      } else {
          // Une erreur s'est produite
      }
  })
  ```
  {:pre}


### Connexion anonyme
{: #anonymous notoc}

{{site.data.keyword.appid_short_notm}} vous permet d'effectuer une connexion anonyme. Voir [Identité anonyme](/docs/services/appid/user-profile.html#anonymous).

  ```
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //Utilisateur authentifié
      }

      public func onAuthorizationCanceled() {
          //Authentification annulée par l'utilisateur
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Une erreur s'est produite
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())`
  ```
  {:pre}

### Authentification progressive
{: #progressive notoc}

Lorsqu'il dispose d'un jeton d'accès anonyme, l'utilisateur peut devenir un utilisateur identifié en transmettant ce jeton à la méthode loginWidget.launch :

  ```
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {:pre}

Après une connexion anonyme, une authentification progressive a lieu même si le widget de connexion est appelé sans transmission d'un jeton d'accès vu que le service a utilisé le dernier jeton d'accès reçu. Si vous désirez effacer vos jetons stockés, exécutez la commande suivante :

  ```
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {:pre}



## Etapes suivantes
{: #next-steps}

{{site.data.keyword.appid_short_notm}} fournit une configuration par défaut lorsque vous mettez en place initialement vos fournisseurs d'identité. Vous ne pouvez utiliser la configuration par défaut qu'en mode développement. Avant de publier votre application, mettez à jour la configuration [Facebook](/docs/services/appid/identity-providers.html#facebook) et [Google](/docs/services/appid/identity-providers.html#google) par défaut en spécifiant vos propres données d'identification.
