---

copyright:
  2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Utilisation du logiciel SDK pour applications mobiles {{site.data.keyword.openwhisk_short}}
{: #openwhisk_mobile_sdk}
*Dernière mise à jour : 28 mars 2016*

{{site.data.keyword.openwhisk}} met à disposition un logiciel SDK pour périphériques iOS et watchOS 2 qui permet aux applications mobiles
d'exécuter des déclencheurs distants et d'appeler des actions distantes facilement. Actuellement, il n'existe pas de version pour Android, mais les
développeurs Android peuvent utiliser l'API REST {{site.data.keyword.openwhisk}} directement.
{: shortdesc}

Le logiciel SDK pour applications mobiles est écrit en langage Swift 2.2 et prend en charge iOS 9 et les éditions ultérieures.

## Ajout du logiciel SDK à votre application
{: #openwhisk_add_sdk}
Vous pouvez installer le logiciel SDK pour applications mobiles à l'aide de CocoaPods, Carthage, ou depuis le répertoire source.

### Installation à l'aide de CocoaPods 

Le logiciel SDK {{site.data.keyword.openwhisk_short}} pour les applications mobiles est disponible pour sa distribution publique via
CocoaPods. Si CocoaPods est installé, entrez les lignes suivantes dans un fichier appelé 'Podfile' dans le répertoire de projet de l'application de
démarrage : 

```
source 'https://github.com/openwhisk/openwhisk-podspecs.git'

use_frameworks!

target 'MyApp' do
     platform :ios, '9.0'
     pod 'OpenWhisk'
end

target 'MyApp WatchKit Extension' do
     platform :watchos, '2.0'
     pod 'OpenWhisk-Watch'
end
```
{: codeblock}

Sur la ligne de commande, entrez "pod install" afin d'installer le logiciel SDK pour une application iOS avec une extension watchOS 2.  Utilisez le
fichier d'espace de travail que CocoaPods crée pour votre application afin d'ouvrir le projet dans Xcode.

### Installation à l'aide de Carthage

Créez un fichier dans le répertoire de projet de votre application et appelez-le 'Cartfile'. Entrez les lignes suivantes dans le fichier Cartfile :
```
github "openwhisk//openwhisk-client-swift.git" ~> 0.1.0 # Ou version la plus récente
```
{: codeblock}

Sur la ligne de commande, entrez 'carthage update --platform ios'. Carthage télécharge et génère le logiciel SDK, crée un répertoire appelé Carthage
dans le répertoire de projet de votre application, et place un fichier OpenWhisk.framework dans Carthage/build/iOS. Ajoutez OpenWhisk.framework aux
infrastructures imbriquées dans votre projet Xcode.

### Installation depuis le code source

Le code source est disponible sur le site https://github.com/openwhisk//openwhisk-client-swift.git. Ouvrez le projet à l'aide du fichier OpenWhisk.xcodeproj
dans Xcode.  Il contient deux schémas, "OpenWhisk" et "OpenWhiskWatch", ciblés pour iOS et WatchOS2 respectivement.  Générez le projet pour les cibles dont vous
avez besoin et ajoutez les infrastructures résultantes à votre application (généralement, dans ~/Library/Developer/Xcode/DerivedData/nom de votre
application).

## Installation de l'exemple d'application de démarrage
{: #openwhisk_install_sdkstart}

Vous pouvez utiliser l'interface de ligne de commande {{site.data.keyword.openwhisk_short}} pour télécharger un exemple de code qui
imbrique l'infrastructure du logiciel SDK {{site.data.keyword.openwhisk_short}}.  

Pour installer l'exemple d'application de démarrage, entrez la commande suivante :
```
wsk sdk install iOS
```
Elle télécharge un fichier zip contenant l'application de démarrage.  Un fichier Pod se trouve dans le répertoire de projet.  Exécutez "pod install" depuis
un terminal pour installer le logiciel SDK.
{: pre}

## Initiation au logiciel SDK
{: #openwhisk_sdk_getstart}

Pour être opérationnel rapidement, créez un objet WhiskCredentials avec vos données d'identification pour l'API
{{site.data.keyword.openwhisk_short}}, puis créez une instance {{site.data.keyword.openwhisk_short}}.

Par exemple, en langage Swift 2.1, utilisez l'exemple de code suivant pour créer un objet de données d'identification :

```
let credentialsConfiguration = WhiskCredentials(accessKey: "maClé", accessToken: "monJeton")

let whisk = Whisk(credentials: credentialsConfiguration!)
```
{: codeblock}

Dans l'exemple précédent, vous transmettez les paramètres `maClé` et `monJeton` que vous obtenez d'{{site.data.keyword.openwhisk_short}}. Vous
pouvez extraire la clé et le jeton avec la commande de l'interface de ligne de commande suivante :

```
wsk property get --auth
```
{: pre}
```
whisk auth        kkkkkkkk-kkkk-kkkk-kkkk-kkkkkkkkkkkk:tttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttt
```
{: screen}

Les chaînes qui figurent avant et après le signe deux-points sont votre clé et votre jeton, respectivement.

## Appel d'une action {{site.data.keyword.openwhisk_short}}
{: #openwhisk_sdk_invoke}


Pour appeler une action distante, vous pouvez appeler `invokeAction` avec le nom d'action. Vous pouvez spécifier l'espace de nom
auquel l'action appartient ou ne rien indiquer pour accepter l'espace de nom par défaut.  Utilisez un dictionnaire pour transmettre des paramètres à
l'action, en fonction des besoins.

Par exemple :

```
// Dans cet exemple, nous appelons une action qui affiche un message dans la console OpenWhisk
var params = Dictionary<String, String>()
params["payload"] = "Hi from mobile"

do {
    try whisk.invokeAction(name: "helloConsole", package: "monpackage", namespace: "monEspaceNom", parameters: params, hasResult: false, callback: {(reply, error) -> Void in
        if let error = error {
            //faire quelque chose
            print("Error invoking action \(error.localizedDescription)")
        } else {
            print("Action invoked!")
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

Pour exécuter un déclencheur distant, vous pouvez appeler la méthode `fireTrigger`. Transmettez les paramètres requis en utilisant
un dictionnaire.

```
// Dans cet exemple, nous exécutons un déclencheur lorsque notre emplacement change d'un certain nombre de degrés

var locationParams = Dictionary<String, String>()
locationParams["payload"] = "{\"lat\":41.27093, \"lon\":-73.77763}"

do {
    try whisk.fireTrigger(name: "locationChanged", package: "monpackage", namespace: "monEspaceNom", parameters: locationParams, callback: {(reply, error) -> Void in

        if let error = error {
            print("Error firing trigger \(error.localizedDescription)")
        } else {
            print("Trigger fired!")
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

Si l'action renvoie un résultat, associez hasResult à la valeur true dans l'appel invokeAction. Le résultat de l'action est renvoyé dans le
dictionnaire de réponse. Exemple :

```
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

Par défaut, le logiciel SDK renvoie seulement l'ID d'activation et tout résultat généré par l'action appelée. Pour obtenir les métadonnées de
l'objet de réponse entier, qui inclut le code de statut de la réponse HTTP, utilisez le paramètre suivant :

```
whisk.verboseReplies = true
```
{: codeblock}

## Configuration du logiciel SDK
{: #openwhisk_sdk_configure}

Vous pouvez configurer le logiciel SDK pour qu'il fonctionne dans différentes installations d'{{site.data.keyword.openwhisk_short}} à l'aide
du paramètre baseURL. Exemple :

```
whisk.baseURL = "http://localhost:8080"
```
{: codeblock}

Dans cet exemple, vous utilisez une installation qui s'exécute sur localhost:8080.  Si vous ne spécifiez pas le paramètre baseUrl, le logiciel SDK
pour applications mobiles utilise l'instance qui s'exécute sur https://openwhisk.ng.bluemix.net.

Vous pouvez transmettre un paramètre NSURLSession personnalisé si vous nécessitez un traitement réseau spécial. Par exemple, il se peut que vous
disposiez de votre propre installation d'{{site.data.keyword.openwhisk_short}}, qui utilise des certificats autosignés :

```
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

Toutes les actions et tous les déclencheurs possèdent un nom qualifié complet qui est composé d'un espace de nom, d'un package et d'un
nom d'action ou de déclencheur. Le logiciel SDK peut accepter ces noms qualifiés complets en tant que paramètres lorsque vous appelez une action ou
exécutez un
déclencheur. Le
logiciel SDK fournit également une fonction qui accepte les noms qualifiés complets similaires à
`/mon_espace_nom/mon_package/nom_action_ou_déclencheur`. La chaîne de nom qualifié prend en charge des valeurs par défaut sans nom pour
les espaces de nom et les packages dont tous les utilisateurs {{site.data.keyword.openwhisk_short}} disposent ; par conséquent, les règles
d'analyse suivantes s'appliquent :

- Dans qName = "foo", l'espace de nom est l'espace de nom par défaut, le package est le package par défaut et l'action/le déclencheur est "foo"
- Dans qName = "monpackage/foo", l'espace de nom est l'espace de nom par défaut, le package est monpackage et l'action/le déclencheur est "foo"
- Dans qName = "/monEspaceNom/foo", l'espace de nom est monEspaceNom, le package est le package par défaut et l'action/le déclencheur est "foo"
- Dans qName = "/monEspaceNom/monpackage/foo, l'espace de nom est monEspaceNom, le package est monpackage et l'action/le déclencheur est "foo"

Toutes les autres combinaisons génèrent une erreur WhiskError.QualifiedName. Par conséquent, lorsque vous utilisez des noms qualifiés, vous
devez encapsuler l'appel dans une construction "`do/try/catch`".

### Bouton du logiciel SDK

Pour des raisons pratiques, le logiciel SDK inclut un élément `WhiskButton` qui étend l'élément `UIButton` afin
qu'il puisse appeler des actions.  Pour utiliser l'élément `WhiskButton`, suivez l'exemple ci-dessous.

```
var whiskButton = WhiskButton(frame: CGRectMake(0,0,20,20))

whiskButton.setupWhiskAction("helloConsole", package: "monpackage", namespace: "_", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)

let myParams = ["name":"value"]

// A appeler lorsque vous détectez un événement d'appui, par exemple dans un élément IBAction, pour appeler l'action
whiskButton.invokeAction(parameters: myParams, callback: { reply, error in
    if let error = error {
        print("Oh no, error: \(error)")
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
           print("Oh no, error: \(error)")
       } else {
           print("Success: \(reply)")
       }
   }
} catch {
   print("Error setting up button \(error)")
}
```
{: codeblock}
