---

copyright:
  years: 2016, 2017
  lastupdated: "2017-04-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Création et appel d'actions {{site.data.keyword.openwhisk_short}}
{: #openwhisk_actions}


Les actions sont des fragments de code sans état qui s'exécutent sur la plateforme {{site.data.keyword.openwhisk}}. Une action peut être écrite en tant que fonction JavaScript, Swift ou Python, méthode Java ou programme exécutable personnalisé dans un conteneur Docker. Par exemple, une action peut être utilisée pour détecter les visages dans une image, répondre à une modification de base de données, agréger un ensemble d'appels API ou publier un tweet.
{:shortdesc}
Les actions peuvent être appelées explicitement ou s'exécuter en réponse à un événement. Dans tous les cas, chaque exécution d'une action génère un enregistrement d'activation identifié par un ID d'activation unique. L'entrée pour une action et le résultat d'une action constituent un dictionnaire de paires clé-valeur, où la clé est une chaîne et la valeur est une valeur JSON valide. Les actions peuvent également être composées d'appels à d'autres actions ou à une séquence définie d'actions.

Apprenez à créer, appeler et déboguer des actions dans votre environnement de développement préféré :
* [JavaScript](#openwhisk_create_action_js)
* [Swift](#openwhisk_actions_swift)
* [Python](#openwhisk_actions_python)
* [Java](#openwhisk_actions_java)
* [Docker](#openwhisk_actions_docker)

Découvrez également les opérations suivantes :

* [Surveillance de la sortie des actions](#openwhisk_actions_polling)
* [Affichage de la liste des actions](#openwhisk_listing_actions)
* [Suppression d'actions](#openwhisk_delete_action)
* [Accès aux métadonnées d'action dans le corps de l'action](#openwhisk_action_metadata)


## Création et appel d'actions JavaScript
{: #openwhisk_create_action_js}

Les sections ci-après expliquent comment utiliser des actions dans JavaScript. Vous commencez par créer et appeler une action simple. Ensuite, vous ajoutez des paramètres à une action et vous appelez cette action avec des paramètres. Vient ensuite les phases de définition et d'appel des paramètres par défaut. Ensuite, vous créez des actions asynchrones et, enfin, vous gérez des séquences d'actions.


### Création et appel d'une action JavaScript simple
{: #openwhisk_single_action_js}

Suivez les étapes et les exemples ci-dessous pour créer votre première action JavaScript.

1. Créez un fichier JavaScript avec le contenu ci-après. Dans cet exemple, le nom de fichier est 'hello.js'.

  ```javascript
  function main() {
      return {payload: 'Hello world'};
  }
  ```
    {: codeblock}

  Le fichier JavaScript peut contenir des fonctions supplémentaires. Toutefois, par convention, une fonction appelée `main` doit exister pour fournir le point d'entrée de l'action.

2. Créez une action à partir de la fonction JavaScript ci-dessous. Dans cet exemple, l'action s'appelle 'hello'.

  ```
  wsk action create hello hello.js
  ```
      {: pre}
  ```
  ok: created action hello
  ```

3. Répertoriez les actions que vous avez créées :

  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  hello       private
  ```

  Vous pouvez voir l'action `hello` que vous venez de créer.

4. Une fois l'action créée, vous pouvez l'exécuter dans le cloud dans OpenWhisk avec la commande 'invoke'. Vous pouvez appeler des actions avec un appel *bloquant* (style demande/réponse) ou *non bloquant* en spécifiant un indicateur dans la commande. Une demande d'appel bloquante *attend* que le résultat de l'activation soit disponible. Le délai d'attente est inférieur à 60 secondes ou à la [limite de temps](./openwhisk_reference.html#openwhisk_syslimits) configurée de l'action. Le résultat de l'activation est renvoyé s'il est disponible avant la fin du délai d'attente. Sinon, le traitement de l'activation continue dans le système et un ID d'activation est renvoyé de sorte que les résultats puissent être consultés ultérieurement, comme dans le cas des demandes non bloquantes (voir [ici](#openwhisk_actions_polling) pour des astuces sur les activations de la surveillance).

  Cet exemple utilise le paramètre de blocage, `--blocking`:

  ```
  wsk action invoke --blocking hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
  ```
  ```json
    {
      "result": {
          "payload": "Hello world"
      },
      "status": "success",
      "success": true
  }
  ```

  La commande génère deux informations importantes :
  * L'ID d'activation (`44794bd6aab74415b4e42a308d880e5b`)
  * Le résultat de l'appel s'il est disponible avant la fin du délai d'attente

  Dans ce cas, le résultat est la chaîne `Hello world` renvoyée par la fonction JavaScript. L'ID d'activation peut être utilisé pour extraire les journaux ou le résultat de l'appel ultérieurement.  

5. Si vous n'avez pas besoin du résultat de l'action immédiatement, vous pouvez omettre l'indicateur `--blocking` pour effectuer un appel non bloquant. Vous pouvez afficher le résultat ultérieurement avec l'ID d'activation. Exemple :

  ```
  wsk action invoke hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 6bf1f670ee614a7eb5af3c9fde813043
  ```

  ```
  wsk activation result 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: pre}
  ```json
    {
      "payload": "Hello world"
  }
  ```

6. Si vous oubliez de noter l'ID d'activation, vous pouvez afficher la liste des activations demandées, de la plus récente à la plus ancienne. Exécutez la commande suivante pour obtenir la liste de vos activations :

  ```
  wsk activation list
  ```
  {: pre}
  ```
  activations
  44794bd6aab74415b4e42a308d880e5b         hello
  6bf1f670ee614a7eb5af3c9fde813043         hello
  ```

### Transmission de paramètres à une action

Des paramètres peuvent être transmis à l'action lorsqu'elle est appelée.

1. Utilisez des paramètres dans l'action. Par exemple, mettez à jour le fichier 'hello.js' avec le contenu suivant :

  ```javascript
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' de ' + params.place};
  }
  ```
  {: codeblock}

  Les paramètres d'entrée sont transmis sous forme de paramètre d'objet JSON à la fonction `main`. Remarquez la façon dont les paramètres `name` et `place` sont extraits de l'objet `params` dans cet exemple.

2. Mettez à jour l'action `hello` et appelez-la en lui transmettant les valeurs de paramètre `name` et `place`. Exemple :

  ```
  wsk action update hello hello.js
  ```
  {: pre}

3.  Les paramètres peuvent être indiqués de manière explicite sur la ligne de commande, ou fournis par un fichier contenant les paramètres souhaités.

  Pour transmettre les paramètres directement via la ligne de commande, indiquez une paire clé/valeur pour l'indicateur `--param` :
  ```
  wsk action invoke --blocking --result hello --param name Bertrand --param place Paris
  ```
  {: pre}

  Pour utiliser un fichier indiquant le contenu des paramètres, créez un fichier contenant les paramètres au format JSON. Le nom de fichier doit être ensuite transmis à l'indicateur `param-file` :

  Exemple de fichier de paramètres nommé parameters.json :
  ```json
    {
      "name": "Bertrand",
      "place": "Paris"
  }
  ```
  {: codeblock}

  ```
  wsk action invoke --blocking --result hello --param-file parameters.json
  ```
  {: pre}

  ```json
    {
      "payload": "Hello, Bertrand de Paris"
  }
  ```

  Remarquez l'utilisation de l'option `--result` pour afficher le résultat de l'appel seulement.

### Définition de paramètres par défaut
{: #openwhisk_binding_actions}

Les actions peuvent être appelées avec plusieurs paramètres nommés. Souvenez-vous : l'action `hello` de l'exemple précédent attend deux paramètres, le nom d'une personne (*name*) et l'endroit d'où elle vient (*place*).

Plutôt que de transmettre tous les paramètres à une action à chaque fois, vous pouvez lier certains paramètres. L'exemple suivant lie le paramètre *place* pour que l'action prenne par défaut la valeur "Paris" pour le paramètre place :

1. Mettez à jour l'action avec l'option `--param` pour lier des valeurs de paramètre, ou en transmettant un fichier contenant les paramètres à `--param-file`.

  Pour indiquer les paramètres par défaut de manière explicite sur la ligne de commande, indiquez une paire clé/valeur pour l'indicateur `param` :

  ```
  wsk action update hello --param place Paris
  ```
  {: pre}

  La transmission des paramètres à partir d'un fichier nécessite la création d'un fichier comportant le contenu souhaité au format JSON.
  Le nom de fichier doit être ensuite transmis à l'indicateur `-param-file` :

  Exemple de fichier de paramètres nommé parameters.json :
  ```json
    {
      "place": "Paris"
  }
  ```
  {: codeblock}

  ```
  wsk action update hello --param-file parameters.json
  ```
  {: pre}

2. Appelez l'action en ne transmettant cette fois que le paramètre `name`.

  ```
  wsk action invoke --blocking --result hello --param name Bertrand
  ```
  {: pre}
  ```json
    {
      "payload": "Hello, Bertrand de Paris"
  }
  ```

  Notez que vous n'avez pas eu besoin de spécifier le paramètre place lorsque vous avez appelé l'action. Toutefois, vous pouvez remplacer les paramètres liés en spécifiant la valeur de paramètre au moment de l'appel.

3. Appelez l'action en transmettant les valeurs `name` et `place`. Cette dernière remplace la valeur liée à l'action.

  Utilisation de l'indicateur `--param` :

  ```
  wsk action invoke --blocking --result hello --param name Bertrand --param place "Marseille"
  ```
  {: pre}

  Utilisation de l'indicateur `--param-file` :

  Fichier parameters.json :
  ```json
    {
    "name": "Bertrand",
    "place": "Paris"
  }
  ```
  {: codeblock}
  ```
  wsk action invoke --blocking --result hello --param-file parameters.json
  ```
  {: pre}
  
  ```json
    {  
      "payload": "Hello, Bertrand de Marseille"
  }
  ```

### Création d'actions asynchrones
{: #openwhisk_asynchrony_js}

Il se peut que les fonctions JavaScript qui s'exécutent de manière asynchrone doivent renvoyer le résultat d'activation après le retour de la fonction `main`. Pour cela, vous pouvez renvoyer une promesse (objet Promise) dans votre action.

1. Sauvegardez le contenu ci-dessous dans un fichier appelé `asyncAction.js`.

  ```javascript
  function main(args) {
       return new Promise(function(resolve, reject) {
         setTimeout(function() {
           resolve({ done: true });
         }, 2000);
      })
   }
  ```
  {: codeblock}

  Notez que la fonction `main` renvoie une promesse (objet Promise), indiquant que l'activation n'est pas encore terminée, mais que cela est prévu.

  Dans ce cas, la fonction JavaScript `setTimeout()` attend deux secondes avant d'appeler la fonction de rappel.  Cela représente le code asynchrone et s'insère dans la fonction de rappel de la promesse (objet Promise).

  La fonction de rappel de la promesse (objet Promise) prend deux arguments, resolve et reject, qui sont tous les deux des fonctions.  L'appel vers `resolve()` satisfait la promesse (objet Promise) et indique que l'activation a abouti.

  Un appel vers `reject()` peut être utilisé pour rejeter la promesse (objet Promise) et signaler que l'activation ne s'est pas terminée normalement.

2. Exécutez les commandes suivantes pour créer l'action et l'appeler :

  ```
  wsk action create asyncAction asyncAction.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result asyncAction
  ```
  {: pre}
  ```json
    {
      "done": true
  }
  ```

  Notez que vous avez effectué un appel bloquant d'une action asynchrone.

3. Procédez à l'extraction du journal d'activation pour savoir combien de temps a duré l'activation :

  ```
  wsk activation list --limit 1 asyncAction
  ```
  {: pre}
  ```
  activations
  b066ca51e68c4d3382df2d8033265db0             asyncAction
  ```


  ```
  wsk activation get b066ca51e68c4d3382df2d8033265db0
  ```
  {: pre}
 ```json
    {
      "start": 1455881628103,
      "end":   1455881648126
  }
  ```

  Prenez connaissance des horodatages de `start` et de `end` dans l'enregistrement d'activation : vous constatez que cette activation a pris un peu plus de deux secondes pour s'exécuter.

### Utilisation d'actions pour appeler une API externe
{: #openwhisk_apicall_action}

Jusqu'à présent, les exemples ont été des fonctions JavaScript autonomes. Vous pouvez également créer une action qui appelle une API externe.

Cet exemple appelle un service météorologique Yahoo afin de prendre connaissance des conditions en cours à un endroit spécifique.

1. Sauvegardez le contenu ci-dessous dans un fichier appelé `weather.js`.

  ```javascript
  var request = require('request');

  function main(params) {
      var location = params.location || 'Paris';
        var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';

      return new Promise(function(resolve, reject) {
          request.get(url, function(error, response, body) {
              if(error) {
                  reject(error);    
                }
                else {
                  var condition = JSON.parse(body).query.results.channel.item.condition;
                    var text = condition.text;
                    var temperature = condition.temp;
                    var output = 'Il fait ' + temperature + ' degrés à ' + location + ', ' + text;
                    resolve({msg: output});
                }
          });
      });
  }
  ```
  {: codeblock}

  Notez que l'action dans l'exemple utilise la bibliothèque JavaScript `request` pour envoyer une demande HTTP à l'API Yahoo Weather, et extrait des zones du résultat JSON. La section [Références](./openwhisk_reference.html#openwhisk_ref_javascript_environments) présente en détail les packages Node.js que vous pouvez utiliser dans vos actions.

  Cet exemple illustre également la nécessité d'actions asynchrones. L'action renvoie une promesse (objet Promise) pour indiquer que le résultat de cette action n'est pas encore disponible au retour de la fonction. A la place, le résultat est disponible dans le rappel `request` une fois l'appel HTTP terminé, et est transmis sous forme d'argument à la fonction `resolve()`.

2. Exécutez les commandes suivantes pour créer l'action et l'appeler :

  ```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location "New York"
  ```
  {: pre}
  ```json
    {
      "msg": "Il fait 28 degrés à New York, nuageux"
  }
  ```

### Conditionnement d'une action dans un module Node.js
{: #openwhisk_js_packaged_action}

Comme alternative à l'écriture de l'ensemble du code de votre action dans un seul fichier source JavaScript, vous pouvez écrire une action en tant que package `npm`. Prenez par exemple un répertoire contenant les fichiers suivants :

D'abord, `package.json` :

```json
    {
  "name": "my-action",
  "main": "index.js",
  "dependencies" : {
    "left-pad" : "1.1.3"
  }
}
```
{: codeblock}

Ensuite, `index.js` :

```javascript
function myAction(args) {
    const leftPad = require("left-pad")
    const lines = args.lines || [];
    return { padded: lines.map(l => leftPad(l, 30, ".")) }
}

exports.main = myAction;
```
{: codeblock}

Notez que l'action est exposée via `exports.main` ; le gestionnaire d'action lui-même peut avoir n'importe quel nom, tant que celui-ci est conforme à la signature habituelle pour l'acceptation et le renvoi d'un objet (ou d'une promesse d'objet (`Promise`)). D'après la convention Node.js, vous devez soit nommer ce fichier `index.js`, soit indiquer le nom de fichier que vous préférez en
tant que propriété `main` dans package.json.

Pour créer une action OpenWhisk depuis ce package :

1. Installez d'abord toutes les dépendances localement :

  ```
  npm install
  ```
  {: pre}

2. Créez une archive `.zip` contenant tous les fichiers (notamment toutes les dépendances) :

  ```
  zip -r action.zip *
  ```
  {: pre}

    > Remarque : l'utilisation d'une action Windows Explorer pour créer le fichier zip génére une structure incorrecte. Les actions zip d'OpenWhisk nécessitent que `package.json` soit placé à la racine du fichier zip, alors que Windows Explorer le place dans un dossier imbriqué. L'option la plus sûre consiste à utiliser la commande `zip` de ligne de commande, comme illustré ci-dessus.


3. Créez l'action :

  ```
  wsk action create packageAction --kind nodejs:6 action.zip
  ```
  {: pre}

  Notez que lorsque vous créez une action depuis une archive `.zip` via l'outil d'interface de ligne de commande, vous devez fournir explicitement une valeur pour l'indicateur `--kind`.

4. Vous pouvez appeler l'action à l'instar de n'importe quelle autre action :

  ```
  wsk action invoke --blocking --result packageAction --param lines "[\"et maintenant\", \"quelque chose de complètement\", \"différent\" ]"
  ```
  {: pre}
  ```json
    {
      "padded": [
          ".......................et maintenant",
          "......quelque chose de complètement",
          ".....................différent"
      ]
  }
  ```


Enfin, notez qu'alors que la plupart des packages `npm` installent des sources JavaScript avec la commande `npm install`, certains installent et compilent également des artefacts binaires. Actuellement, le téléchargement de fichier archive ne prend pas en charge les dépendances binaires et n'admet que les dépendances JavaScript. Par conséquent, il se peut que des appels d'action échouent si l'archive inclut des dépendances binaires.

## Création de séquences d'actions
{: #openwhisk_create_action_sequence}

Vous pouvez créer une action qui assemble des actions dans une séquence.

Plusieurs actions d'utilitaire sont fournies dans un package appelé `/whisk.system/utils`, que vous pouvez utiliser pour créer votre première séquence. Pour en savoir plus sur les packages, voir la section [Packages](./openwhisk_packages.html).

1. Affichez les actions du package `/whisk.system/utils`.

  ```
  wsk package get --summary /whisk.system/utils
  ```
  {: pre}
  ```
  package /whisk.system/utils: Building blocks that format and assemble data
   action /whisk.system/utils/head: Extract prefix of an array
   action /whisk.system/utils/split: Split a string into an array
   action /whisk.system/utils/sort: Sorts an array
   action /whisk.system/utils/echo: Returns the input
   action /whisk.system/utils/date: Current date and time
   action /whisk.system/utils/cat: Concatenates input into a string
  ```


  Vous utiliserez dans cet exemple les actions `split` et `sort`.

2. Créez une séquence d'actions pour que le résultat d'une action soit transmis sous forme d'argument à l'action suivante.

  ```
  wsk action create sequenceAction --sequence /whisk.system/utils/split,/whisk.system/utils/sort
  ```
  {: pre}

  Cette séquence d'actions convertit des lignes de texte en tableau et trie les lignes.

3. Appelez l'action :

  ```
  wsk action invoke --blocking --result sequenceAction --param payload "Sushis périmés,\nLe maître\nest plein de regrets."
  ```
  {: pre}
  ```json
    {
      "length": 3,
      "lines": [
          "Est plein de regrets.,
          "Le maître",
          "Sushis périmés,"
      ]
  }
  ```


  Vous constatez que les lignes sont triées dans le résultat.

**Remarque** : les paramètres transmis entre les actions dans la séquence sont explicites, sauf les paramètres par défaut.
Par conséquent, les paramètres qui sont transmis à la séquence d'actions sont disponibles pour la première action de la séquence seulement.
Le résultat de la première action dans la séquence devient l'objet JSON d'entrée de la deuxième action de la séquence (et ainsi de suite).
Cet objet ne comporte pas les paramètres transmis initialement à la séquence sauf si la première action les inclut explicitement dans son résultat.
Les paramètres d'entrée d'une action sont fusionnés avec ses paramètres par défaut, les premiers étant prioritaires et remplaçant tout paramètre par défaut correspondant.
Pour plus d'informations sur l'appel de séquences d'actions avec plusieurs paramètres nommés, voir [Définition de paramètres par défaut](./openwhisk_actions.html#openwhisk_binding_actions).

## Création d'actions Python
{: #openwhisk_actions_python}

Le processus de création d'actions Python est similaire au processus de création d'actions JavaScript. Les sections ci-après vous expliquent comment créer et appeler une action Python unique, et comment ajouter des paramètres à cette action.

### Création et appel d'une action
{: #openwhisk_actions_python_invoke}

Une action est simplement une fonction Python de premier niveau. Par exemple, créez un fichier nommé `hello.py` contenant le code source suivant :

```python
def main(args):
    name = args.get("name", "stranger")
    greeting = "Hello " + name + "!"
    print(greeting)
        return {"greeting": greeting}
```
{: codeblock}

Les actions Python consomment et produisent toujours un dictionnaire. Par défaut, la méthode d'entrée pour l'action est `main`, mais elle peut être spécifiée explicitement en créant l'action avec l'interface CLI `wsk` en utilisant `--main`, comme pour n'importe quel type d'action.

Vous pouvez créer une action OpenWhisk appelée `helloPython` depuis cette fonction comme suit :

```
wsk action create helloPython hello.py
```
{: pre}
L'interface CLI infère automatiquement le type d'action d'après l'extension du fichier source. Pour les fichiers source `.py`, l'action est lancée dans un environnement d'exécution Python 2.7. Vous pouvez également créer une action opérant avec Python 3.6 en mentionnant spécifiquement le paramètre `--kind python:3`. Reportez-vous aux informations de référence Python [](./openwhisk_reference.html#openwhisk_ref_python_environments) pour une comparaison de Python 2.7 et 3.6.

L'appel d'action est identique pour les actions Python et pour les actions JavaScript :

```
wsk action invoke --blocking --result helloPython --param name World
```
{: pre}

```json
    {
      "greeting": "Hello World!"
  }
```


## Création d'actions Swift

Le processus de création d'actions Swift est similaire au processus de création d'actions JavaScript. Les sections ci-après expliquent comment créer et appeler une action Swift unique, et comment ajouter des paramètres à cette action.

Vous pouvez aussi utiliser le [bac à sable Swift](https://swiftlang.ng.bluemix.net) en ligne pour tester votre code Swift sans avoir à installer Xcode sur votre machine.

### Création et appel d'une action

Une action est simplement une fonction Swift de premier niveau. Par exemple, créez un fichier appelé `hello.swift` avec le contenu suivant :

```swift
func main(args: [String:Any]) -> [String:Any] {
    if let name = args["name"] as? String {
        return [ "greeting" : "Hello \(name)!" ]
    } else {
        return [ "greeting" : "Hello stranger!" ]
    }
}
```
{: codeblock}

Les actions Swift consomment et produisent toujours un dictionnaire.

Vous pouvez créer une action {{site.data.keyword.openwhisk_short}} appelée `helloSwift` depuis cette fonction comme suit :

```
wsk action create helloSwift hello.swift
```
{: pre}

Lorsque vous utilisez la ligne de commande et un fichier source `.swift`, il n'est pas nécessaire de spécifier que vous créez une action Swift (et non une action JavaScript) ; l'outil le détermine à partir de l'extension de fichier.

L'appel d'action est identique pour les actions Swift et les actions JavaScript :

```
wsk action invoke --blocking --result helloSwift --param name World
```
{: pre}

```json
    {
      "greeting": "Hello World!"
  }
```

**Attention :** les actions Swift s'exécutent dans un environnement Linux. Swift on Linux est en cours de développement et
{{site.data.keyword.openwhisk_short}} utilise généralement l'édition disponible la plus récente, qui n'est pas nécessairement stable. De plus, il se peut que la version de Swift qui est utilisée avec {{site.data.keyword.openwhisk_short}} ne corresponde pas aux versions de Swift provenant d'éditions stables de Xcode sous MacOS.

### Package d'une action sous forme d'exécutable Swift
{: #openwhisk_actions_swift_zip}

Lorsque vous créez une action Swift d'OpenWhisk avec un fichier source Swift, celui-ci doit être compilé dans un binaire avant d'exécuter l'action. Après quoi, les appels ultérieurs de l'action sont beaucoup plus rapides jusqu'à ce que le conteneur hébergeant votre action soit purgé. Ce délai est dénommé délai de démarrage à froid.

Pour éviter ce délai, vous pouvez compiler votre fichier Swift en binaire, puis le télécharger dans OpenWhisk sous forme de fichier zip. Comme vous avez besoin de l'échafaudage OpenWhisk, la manière la plus facile de créer le binaire consiste à le générer dans le même environnement que celui où il sera exécuté. Pour ce faire, procédez comme suit :

- Exécutez un conteneur d'actions Swift interactif.
```
docker run --rm -it -v "$(pwd):/owexec" openwhisk/swift3action bash
```
{: pre}

    Ceci vous positionne dans un shell bash dans le conteneur Docker. Exécutez les commandes suivantes depuis ce shell :

- Installez zip pour création facile du package binaire
  ```
  apt-get install -y zip
  ```
  {: pre}
- Copiez le code source et préparez-le pour sa construction
  ```
  cp /owexec/hello.swift /swift3Action/spm-build/main.swift 
  ```
  {: pre}
  ```
  cat /swift3Action/epilogue.swift >> /swift3Action/spm-build/main.swift
  ```
  {: pre}
  ```
  echo '_run_main(mainFunction:main)' >> /swift3Action/spm-build/main.swift
  ```
  {: pre}
- zBuild et liaison
  ```
  /swift3Action/spm-build/swiftbuildandlink.sh
  ```
  {: pre}
- Créez l'archive zip
  ```
  cd /swift3Action/spm-build
  ```
  {: pre}
  ```
  zip /owexec/hello.zip .build/release/Action
  ```
- Quittez le conteneur Docker
  ```
  exit
  ```
  {: pre}
Vous avez créé ainsi le fichier hello.zip dans le même répertoire que hello.swift. 
-Téléchargez-le dans OpenWhisk avec le nom d'action helloSwiftly :
  ```
  wsk action update helloSwiftly hello.zip --kind swift:3
  ```
  {: pre}
- Pour vous convaincre du gain en rapidité, exécutez 
  ```
  wsk action invoke helloSwiftly --blocking
  ``` 
  {: pre}

Le temps pris pour l'exécution de l'action figure dans la propriété "duration" et vous pouvez le comparer avec son exécution via une étape de compilation dans l'action hello.

## Création d'actions Java
{: #openwhisk_actions_java}

Le processus de création d'actions Java est similaire au processus de création d'actions JavaScript et Swift. Les sections ci-après expliquent comment créer et appeler une action Java unique, et comment ajouter des paramètres à cette action.

Pour compiler, tester et archiver des fichiers Java, vous devez disposer d'un kit [JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) installé en local.

### Création et appel d'une action
{: #openwhisk_actions_java_invoke}

Une action Java est un programme Java doté d'une méthode nommée `main` qui possède l'exacte signature suivante :
```java
public static com.google.gson.JsonObject main(com.google.gson.JsonObject);
```
{: codeblock}

Par exemple, créez un fichier Java nommé `Hello.java` avec le contenu suivant :

```java
import com.google.gson.JsonObject;
public class Hello {
    public static JsonObject main(JsonObject args) {
        String name = "stranger";
        if (args.has("name"))
            name = args.getAsJsonPrimitive("name").getAsString();
        JsonObject response = new JsonObject();
        response.addProperty("greeting", "Hello " + name + "!");
        return response;
    }
}
```
{: codeblock}

Compilez ensuite `Hello.java` dans un fichier JAR
`hello.jar` comme suit :
```
javac Hello.java
```
{: pre}
```
jar cvf hello.jar Hello.class
```
{: pre}

**Remarque :**
[google-gson](https://github.com/google/gson) doit exister dans votre variable Java CLASSPATH lors de la compilation du fichier Java.

Vous pouvez créer une action OpenWhisk nommée `helloJava` à partir de ce fichier JAR comme suit :

```
wsk action create helloJava hello.jar --main Hello
```

Lorsque vous utilisez la ligne de commande et un fichier source `.jar`, il n'est pas nécessaire de spécifier que vous créez une action Java ; l'outil le détermine à partir de l'extension de fichier.

Vous devez indiquer le nom de la classe principale avec `--main`. Une classe principale est éligible quand elle implémente une méthode `main` statique comme décrit ci-dessus. Si la classe ne figure pas dans le package par défaut, utilisez le nom de classe Java entièrement qualifié, par exemple, `--main com.example.MyMain`.

L'appel d'action est identique pour les actions Java et les actions Swift et JavaScript :

```
wsk action invoke --blocking --result helloJava --param name World
```
{: pre}

```json
    {
      "greeting": "Hello World!"
  }
```

## Création d'actions Docker

Avec les actions {{site.data.keyword.openwhisk_short}} Docker, vous pouvez écrire vos actions dans n'importe quel langage.

Votre code est compilé dans un fichier binaire exécutable et imbriqué dans une image Docker. Le programme binaire interagit avec le système en prenant l'entrée provenant de `stdin` et en répondant par le biais de `stdout`.

Au préalable, vous devez disposer d'un compte Docker Hub.  Pour configurer un ID et un compte Docker gratuits, visitez [Docker Hub](https://hub.docker.com){: new_window}.

Dans les instructions qui suivent, l'ID utilisateur Docker est `jeannedupont` et le mot de passe est `jeanne_motdepasse`.  Si l'on part du principe que l'interface de ligne de commande est déjà configurée, trois étapes doivent être effectuées pour configurer un fichier binaire personnalisé pouvant être utilisé par {{site.data.keyword.openwhisk_short}}. Ensuite, l'image Docker téléchargée peut être utilisée en tant qu'action.

1. Téléchargez le squelette Docker. Vous pouvez le télécharger via l'interface de ligne de commande comme suit :

  ```
  wsk sdk install docker
  ```
  ```
  {: pre}
  ```
  A présent, le squelette Docker est installé dans le répertoire en cours.
  ```

  ```
  ls dockerSkeleton/
  ```
  {: pre}
  ```
  Dockerfile      README.md       buildAndPush.sh example.c
  ```

  Le squelette est un modèle de conteneur Docker dans lequel vous pouvez injecter votre code sous la forme de fichiers binaires personnalisés.

2. Placez votre fichier binaire personnalisé dans le squelette de boîte noire. Le squelette inclut déjà un programme C que vous pouvez utiliser.

  ```
  cat dockerSkeleton/example.c
  ```
  {: pre}
  ```c
  #include <stdio.h>
  int main(int argc, char *argv[]) {
      printf("Exemple de message de journal d'un programme C arbitraire !\n");
      printf("{ \"msg\": \"Bonjour du programme C arbitraire !\", \"args\": %s }",
             (argc == 1) ? "undefined" : argv[1]);
  }
  ```
  {: codeblock}

  Vous pouvez modifier ce fichier en fonction de vos besoins ou ajouter un code et des dépendances supplémentaires à l'image Docker.
  Dans ce cas, vous devrez peut-être adapter le fichier `Dockerfile` d'après vos besoins pour construire votre exécutable.
  Le binaire doit être situé dans le conteneur sous `/action/exec`.

  Le fichier exécutable reçoit un argument simple depuis la ligne de commande. Il s'agit d'une sérialisation
de chaîne de l'objet JSON représentant les arguments de l'action. Le programme peut consigner les entrées de journal dans `stdout` ou `stderr`.
  Par convention, la dernière ligne de la sortie doit être un objet JSON sous forme de chaîne représentant le résultat de l'action.
3. Générez l'image Docker et téléchargez-la à l'aide d'un script fourni. Vous devez d'abord exécuter `docker login` pour vous authentifier, puis lancer le script en spécifiant le nom de l'image choisie.

  ```
  docker login -u jeannedupont -p jeanne_motdepasse
  ```
  {: pre}
  ```
  cd dockerSkeleton
  ```
  {: pre}
  ```
  ./buildAndPush.sh jeannedupont/blackboxdemo
  ```
  {: pre}

  Notez qu'une partie du fichier example.c est compilée dans le cadre de la procédure de génération de l'image Docker, de sorte que vous n'avez pas besoin d'une compilation C sur votre machine.
  En fait, sauf si vous le compilez sur une machine hôte compatible, il se peut que le fichier binaire ne puisse pas s'exécuter dans le conteneur car les formats ne concorderont pas.

  Vous pouvez à présent utiliser votre conteneur Docker sous forme d'action {{site.data.keyword.openwhisk_short}}.
  ```
  wsk action create --docker example jeannedupont/blackboxdemo
  ```
  {: pre}

  Notez l'utilisation de `--docker` lors de la création d'une action. Actuellement, on suppose que toutes les images Docker sont hébergées dans Docker Hub.
  L'action peut être appelée comme n'importe quelle autre action {{site.data.keyword.openwhisk_short}}.

  ```
  wsk action invoke --blocking --result example --param payload Rey
  ```
  {: pre}
  ```json
    {
      "args": {
          "payload": "Rey"
      },
      "msg": "Bonjour du programme C arbitraire !"
  }
  ```

  Pour mettre à jour l'action Docker, exécutez buildAndPush.sh afin de télécharger l'image la plus récente dans le dockerhub. Ainsi, le système pourra extraire votre nouvelle image Docker à la prochaine exécution du code pour votre action.
  Si aucun conteneur n'est en cours d'exécution, les nouveaux appels utilisent la nouvelle image Docker.
  Toutefois, s'il existe un conteneur en cours d'exécution utilisant une version précédente de votre image Docker, les nouveaux appels continuent d'utiliser cette image sauf si vous exécutez `wsk action update`. Cette commande indique au système que pour les nouveaux appels, il doit exécuter une commande docker pull afin d'obtenir votre nouvelle image Docker.

  ```
  ./buildAndPush.sh jeannedupont/blackboxdemo
  ```
  {: pre}
  ```
  wsk action update --docker example jeannedupont/blackboxdemo
  ```
  {: pre}

  Pour plus d'informations sur la création d'actions Docker, reportez-vous à la section [References](./openwhisk_reference.html#openwhisk_ref_docker).
## Examen de la sortie de l'action
{: #openwhisk_actions_polling}

Des actions {{site.data.keyword.openwhisk_short}} peuvent être appelées par d'autres utilisateurs, en réponse à divers événements, ou dans le cadre d'une séquence d'actions. Dans ces cas, il peut être utile de surveiller les appels.

Vous pouvez utiliser l'interface CLI {{site.data.keyword.openwhisk_short}} pour examiner la sortie des actions lorsqu'elles sont appelées.
1. Lancez la commande suivante depuis un interpréteur de commandes :
  ```
  wsk activation poll
  ```
  {: pre}

  Cette commande déclenche une boucle d'interrogation qui consulte en permanence les journaux après des activations.

2. Basculez dans une autre fenêtre et appelez une action :

  ```
  wsk action invoke /whisk.system/samples/helloWorld --param payload Bob
  ```
  {: pre}
  ```
  ok: invoked /whisk.system/samples/helloWorld with id 7331f9b9e2044d85afd219b12c0f1491
  ```

3. Observez le journal d'activation dans la fenêtre d'interrogation :

  ```
  Activation: helloWorld (7331f9b9e2044d85afd219b12c0f1491)
    2016-02-11T16:46:56.842065025Z stdout: hello bob!
  ```

  De même, chaque fois que vous exécutez l'utilitaire d'interrogation (poll), vous pouvez consulter en temps réel les journaux de n'importe quelle action s'exécutant pour votre compte dans OpenWhisk.


## Liste des actions
{: #openwhisk_listing_actions}

Vous pouvez répertorier toutes les actions que vous avez créées en utilisant la commande :

```
wsk action list
```
{: pre}

Au fur et à mesure que vous créez d'autres actions, cette liste s'allonge et il peut être opportun de regrouper les actions associées dans des [packages](./openwhisk_packages.html). Pour filtrer votre liste d'actions en n'affichant que celles d'un package spécifique, utilisez la commande suivante : 

```
wsk action list [NOM PACKAGE]
```
  {: pre}
  ## Suppression d'actions
{: #openwhisk_delete_action}

Vous pouvez procéder à un nettoyage en supprimant les actions que vous ne voulez pas utiliser.

1. Exécutez la commande suivante pour supprimer une action :
  ```
  wsk action delete hello
  ```
  {: pre}
  ```
  ok: deleted hello
  ```

2. Vérifiez que l'action ne figure plus dans la liste des actions.
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  ```
  {: pre}
  ## Accès aux métadonnées de l'action dans le corps de l'action
{: #openwhisk_action_metadata}

L'environnement de l'action contient plusieurs propriétés spécifiques à l'action en cours d'exécution.
Elles permettent à l'action de fonctionner à l'aide d'un programme avec des actifs OpenWhisk via l'API REST,
ou de définir une alarme interne lorsque l'action est sur le point d'utiliser la totalité de son budget temps alloué.
Ces propriétés sont accessibles via l'environnement système de tous les contextes d'exécution pris en charge : actions Node.js, Python, Swift, Java et Docker lorsque le squelette Docker OpenWhisk est employé.

* `__OW_API_HOST` Hôte d'API pour le déploiement OpenWhisk exécutant cette action
* `__OW_API_KEY` Clé d'API pour le sujet appelant l'action, il peut s'agir d'une clé d'API restreinte
* `__OW_NAMESPACE` Espace de nom pour _activation_ (ne peut pas être identique à celui pour l'action)
* `__OW_ACTION_NAME` Nom qualifié complet de l'action en cours d'exécution
* `__OW_ACTIVATION_ID` ID d'activation de l'instance d'action en cours d'exécution
* `__OW_DEADLINE` Délai approximatif au bout duquel cette action aura consommé la totalité de son quota de durée (mesurée en millisecondes sur l'époque)
