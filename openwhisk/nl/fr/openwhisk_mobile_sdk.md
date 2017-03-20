---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilisation du logiciel SDK pour applications mobiles {{site.data.keyword.openwhisk_short}}
{: #openwhisk_mobile_sdk}

{{site.data.keyword.openwhisk}} met à disposition un logiciel SDK pour périphériques iOS et watchOS qui permet aux applications mobiles d'exécuter des déclencheurs distants et d'appeler des actions distantes facilement. Actuellement, il n'existe pas de version pour Android, mais les développeurs Android peuvent utiliser l'API REST {{site.data.keyword.openwhisk}} directement.

Le logiciel SDK pour applications mobiles est écrit en langage Swift 3.0 et prend en charge iOS 10 et les éditions ultérieures. Vous pouvez générer le logiciel SDK pour applications mobiles avec Xcode 8.0. Les versions Legacy Swift 2.2/Xcode 7 du logiciel SDK sont disponibles jusqu'à la version 0.1.7, bien que celle-ci soit désormais dépréciée.

## Ajout du logiciel SDK à votre application
{: #openwhisk_add_sdk}

Vous pouvez installer le logiciel SDK pour applications mobiles à l'aide de CocoaPods, Carthage, ou depuis le répertoire source.

### Installation à l'aide de CocoaPods
{: #openwhisk_add_sdk_cocoapods}

Le logiciel SDK {{site.data.keyword.openwhisk_short}} pour les applications mobiles est disponible pour sa distribution publique via CocoaPods. En supposant que CocoaPods est installé, insérez les lignes suivantes dans un fichier nommé 'Podfile' sous le répertoire des projets d'applications de démarrage.

```
install! 'cocoapods', :deterministic_uuids => false
use_frameworks!

target 'MyApp' do
     pod 'OpenWhisk', :git => 'https://github.com/openwhisk/openwhisk-client-swift.git', :tag => '0.2.2'
end

target 'MyApp WatchKit Extension' do
     pod 'OpenWhisk', :git => 'https://github.com/openwhisk/openwhisk-client-swift.git', :tag => '0.2.2'
end
```
{: codeblock}

Depuis la ligne de commande, entrez `pod install`. Cette commande installe le logiciel SDK pour une application iOS avec une extension watchOS.  Utilisez le fichier d'espace de travail que CocoaPods a créé pour votre application afin d'ouvrir le projet dans Xcode.

Après l'installation, ouvrez l'espace de travail de votre projet.  L'avertissement suivant peut s'afficher lors de la génération : `Use Legacy Swift Language Version” (SWIFT_VERSION) is required to be configured correctly for targets which use Swift. Use the [Edit > Convert > To Current Swift Syntax…] menu to choose a Swift version or use the Build Settings editor to configure the build setting directly.`
Ce message apparaît si Cocoapods ne met pas à jour la version de Swift dans le projet Pods.  Pour résoudre le problème, sélectionnez le projet Pods et la cible {{site.data.keyword.openwhisk_short}}. Accédez aux paramètres de génération et associez le paramètre `Use Legacy Swift Language Version` à la valeur `no`. Vous pouvez aussi ajouter les instructions de postinstallation suivantes à la fin de votre fichier Pod :

```
post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['SWIFT_VERSION'] = '3.0'
    end
  end
end
```
{: codeblock}

### Installation à l'aide de Carthage
{: #openwhisk_add_sdk_carthage}

Créez un fichier dans le répertoire de projet de votre application et appelez-le 'Cartfile'. Insérez la ligne suivante dans le fichier :
```
github "openwhisk/openwhisk-client-swift.git" ~> 0.2.2 # Ou version la plus récente
```
{: codeblock}

Depuis la ligne de commande, entrez `carthage update --platform ios`. Carthage télécharge et génère le logiciel SDK, crée un répertoire appelé Carthage dans le répertoire de projet de votre application, et place un fichier {{site.data.keyword.openwhisk_short}}.framework dans Carthage/build/iOS.

Vous devez ensuite ajouter l'élément {{site.data.keyword.openwhisk_short}}.framework aux structures intégrées dans votre projet Xcode.

### Installation depuis le code source
{: #openwhisk_add_sdk_source}

Le code source est disponible sur le site https://github.com/openwhisk/openwhisk-client-swift.git.
Ouvrez le projet à l'aide de `OpenWhisk.xcodeproj` et de Xcode.
Le projet contient deux schémas, "OpenWhisk" et "OpenWhiskWatch", ciblant respectivement iOS et watchOS 2.
Générez le projet pour les cibles dont vous avez besoin et ajoutez les infrastructures résultantes à votre application (généralement, dans ~/Library/Developer/Xcode/DerivedData/nom de votre application).

## Installation de l'exemple d'application de démarrage
{: #openwhisk_install_sdkstart}

Vous pouvez utiliser l'interface de ligne de commande {{site.data.keyword.openwhisk_short}} pour télécharger un exemple de code qui imbrique l'infrastructure du logiciel SDK {{site.data.keyword.openwhisk_short}}.  

Pour installer l'exemple d'application de démarrage, entrez la commande suivante :
```bash
wsk sdk install iOS
```
{: pre}

Cette commande télécharge un fichier compressé contenant l'application de démarrage. Le répertoire de projet contient un fichier Pod.

Pour installer le logiciel SDK, entrez la commande suivante :
```bash
pod install
```
{: pre}

## Initiation au logiciel SDK
{: #openwhisk_sdk_getstart}

Pour être opérationnel rapidement, créez un objet WhiskCredentials avec vos données d'identification pour l'API
{{site.data.keyword.openwhisk_short}}, puis créez une instance {{site.data.keyword.openwhisk_short}} à partir de l'objet.

Par exemple, utilisez l'exemple de code suivant pour créer un objet de données d'identification :

```swift
let credentialsConfiguration = WhiskCredentials(accessKey: "myKey", accessToken: "myToken")

let whisk = Whisk(credentials: credentialsConfiguration!)
```
{: codeblock}

Dans l'exemple précédent, vous transmettez les paramètres `maClé` et `monJeton` que vous obtenez d'{{site.data.keyword.openwhisk_short}}. Vous
pouvez extraire la clé et le jeton avec la commande de l'interface de ligne de commande suivante :

```bash
wsk property get --auth
```
{: pre}
```
whisk auth        kkkkkkkk-kkkk-kkkk-kkkk-kkkkkkkkkkkk:tttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttt
```
{: screen}

Les chaînes qui précèdent le signe deux-points correspondent à votre clé et la chaîne figurant après le signe deux-points correspond à votre jeton.

## Appel d'une action {{site.data.keyword.openwhisk_short}}
{: #openwhisk_sdk_invoke}


Pour appeler une action distante, vous pouvez appeler `invokeAction` avec le nom d'action. Vous pouvez spécifier l'espace de noms auquel l'action appartient ou ne rien indiquer pour accepter l'espace de noms par défaut. Utilisez un dictionnaire pour transmettre des paramètres à l'action, en fonction des besoins.

Par exemple :

```swift
// Dans cet exemple, nous appelons une action imprimant un message dans la console {{site.data.keyword.openwhisk_short}}
var params = Dictionary<String, String>()
params["payload"] = "Hi from mobile"

do {
    try whisk.invokeAction(name: "helloConsole", package: "monpackage", namespace: "monEspaceNom", parameters: params, hasResult: false, callback: {(reply, error) -> Void in
        if let error = error {
            //Opération
            print("Erreur lors de l'appel de l'action \(error.localizedDescription)")
        } else {
            print("Une action a été appelée!")
        }

    })
} catch {
    print("Error \(error)")
}
```
{: codeblock}

Dans l'exemple précédent, vous appelez l'action `helloConsole` en utilisant l'espace de nom par défaut.

## Exécution d'un déclencheur {{site.data.keyword.openwhisk_short}}
{: #openwhisk_sdk_fire}

Pour exécuter un déclencheur distant, vous pouvez appeler la méthode `fireTrigger`. Transmettez les paramètres requis en utilisant un dictionnaire.

```swift
// Dans cet exemple, nous exécutons un déclencheur lorsque notre emplacement change d'un certain nombre de degrés

var locationParams = Dictionary<String, String>()
locationParams["payload"] = "{\"lat\":41.27093, \"lon\":-73.77763}"

do {
    try whisk.fireTrigger(name: "locationChanged", package: "monpackage", namespace: "monEspaceNom", parameters: locationParams, callback: {(reply, error) -> Void in

        if let error = error {
            print("Error firing trigger \(error.localizedDescription)")
        } else {
            print("Déclencheur exécuté !")
        }
    })
} catch {
    print("Error \(error)")
}
```
{: codeblock}

Dans l'exemple précédent, vous exécutez un déclencheur appelé `locationChanged`.

## Utilisation d'actions qui renvoient un résultat
{: #openwhisk_sdk_actionresult}

Si l'action renvoie un résultat, associez hasResult à la valeur true dans l'appel invokeAction. Le résultat de l'action est renvoyé dans le dictionnaire de réponse. Exemple :

```swift
do {
    try whisk.invokeAction(name: "actionWithResult", package: "monpackage", namespace: "monEspaceNom", parameters: params, hasResult: true, callback: {(reply, error) -> Void in

        if let error = error {
            //faire quelque chose
            print("Error invoking action \(error.localizedDescription)")

        } else {
            var result = reply["result"]
            print("Got result \(result)")
        }


    })
} catch {
    print("Error \(error)")
}
```
{: codeblock}

Par défaut, le logiciel SDK renvoie seulement l'ID d'activation et tout résultat généré par l'action appelée. Pour obtenir les métadonnées de l'objet de réponse entier, qui inclut le code de statut de la réponse HTTP, utilisez le paramètre suivant :

```swift
whisk.verboseReplies = true
```
{: codeblock}

## Configuration du logiciel SDK
{: #openwhisk_sdk_configure}

Vous pouvez configurer le logiciel SDK pour qu'il fonctionne dans différentes installations d'{{site.data.keyword.openwhisk_short}} à l'aide
du paramètre baseURL. Exemple :

```swift
whisk.baseURL = "http://localhost:8080"
```
{: codeblock}

Dans cet exemple, vous utilisez une installation qui s'exécute sur localhost:8080. Si vous ne spécifiez pas le paramètre baseUrl, le logiciel SDK pour applications mobiles utilise l'instance qui s'exécute sur https://openwhisk.ng.bluemix.net.

Vous pouvez transmettre un paramètre NSURLSession personnalisé si vous nécessitez un traitement réseau spécial. Par exemple, il se peut que vous disposiez de votre propre installation d'{{site.data.keyword.openwhisk_short}}, qui utilise des certificats autosignés :

```swift
// créez un délégué réseau qui fait confiance à tout
class NetworkUtilsDelegate: NSObject, NSURLSessionDelegate {
    func URLSession(session: NSURLSession, didReceiveChallenge challenge: NSURLAuthenticationChallenge, completionHandler: (NSURLSessionAuthChallengeDisposition, NSURLCredential?) -> Void) {
        completionHandler(NSURLSessionAuthChallengeDisposition.UseCredential, NSURLCredential(forTrust: challenge.protectionSpace.serverTrust!))
    }
}

// créez un paramètre NSURLSession qui utilise le délégué de confiance
let session = NSURLSession(configuration: NSURLSessionConfiguration.defaultSessionConfiguration(), delegate: NetworkUtilsDelegate(), delegateQueue:NSOperationQueue.mainQueue())

// définissez le logiciel SDK de sorte qu'il utilise ce paramètre urlSession à la place de celui qui est partagé par défaut
whisk.urlSession = session
```
{: codeblock}

### Prise en charge des noms qualifiés
{: #openwhisk_sdk_configure_qual}

Toutes les actions et tous les déclencheurs possèdent un nom qualifié complet qui est composé d'un espace de nom, d'un package et d'un nom d'action ou de déclencheur. Le logiciel SDK peut accepter ces éléments en tant que paramètres lorsque vous appelez une action ou exécutez un déclencheur. Le logiciel SDK fournit également une fonction qui accepte les noms qualifiés complets similaires à `/mon_espace_nom/mon_package/nom_action_ou_déclencheur`. La chaîne de nom qualifié prend en charge des valeurs par défaut sans nom pour les espaces de nom et les packages dont tous les utilisateurs {{site.data.keyword.openwhisk_short}} disposent ; par conséquent, les règles d'analyse suivantes s'appliquent :

- Dans qName = "foo", l'espace de nom est l'espace de nom par défaut, le package est le package par défaut et l'action/le déclencheur est "foo"
- Dans qName = "monpackage/foo", l'espace de nom est l'espace de nom par défaut, le package est monpackage et l'action/le déclencheur est "foo"
- Dans qName = "/monEspaceNom/foo", l'espace de nom est monEspaceNom, le package est le package par défaut et l'action/le déclencheur est "foo"
- Dans qName = "/monEspaceNom/monpackage/foo, l'espace de nom est monEspaceNom, le package est monpackage et l'action/le déclencheur est "foo"

Toutes les autres combinaisons génèrent une erreur WhiskError.QualifiedName. Par conséquent, lorsque vous utilisez des noms qualifiés, vous
devez encapsuler l'appel dans une construction "`do/try/catch`".

### Bouton du logiciel SDK
{: #openwhisk_sdk_configure_button}

Pour des raisons pratiques, le logiciel SDK inclut un élément `WhiskButton` qui étend l'élément `UIButton` afin qu'il puisse appeler des actions.  Pour utiliser l'élément `WhiskButton`, suivez l'exemple ci-dessous.

```swift
var whiskButton = WhiskButton(frame: CGRectMake(0,0,20,20))

whiskButton.setupWhiskAction("helloConsole", package: "monpackage", namespace: "_", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)

let myParams = ["name":"value"]

// Appelez cette action lorsque vous détectez un événement d'appui, par ex. une IBAction, pour appeler l'action
whiskButton.invokeAction(parameters: myParams, callback: { reply, error in
    if let error = error {
        print("Oh non, erreur: \(error)")
    } else {
        print("Success: \(reply)")
    }
})

// Vous pouvez aussi configurer un bouton "autonome" qui est à l'écoute des événements de clic sur lui-même et qui appelle une action

var whiskButtonSelfContained = WhiskButton(frame: CGRectMake(0,0,20,20))
whiskButtonSelfContained.listenForPressEvents = true
do {

   // utilisez une API de nom qualifié qui requiert do/try/catch
   try whiskButtonSelfContained.setupWhiskAction("monpackage/helloConsole", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)
   whiskButtonSelfContained.actionButtonCallback = { reply, error in

       if let error = error {
           print("Oh non, erreur: \(error)")
       } else {
           print("Success: \(reply)")
       }
   }
} catch {
   print("Error setting up button \(error)")
}
```
{: codeblock}
