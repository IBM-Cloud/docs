---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Création et appel d'actions {{site.data.keyword.openwhisk_short}}
{: #openwhisk_actions}

*Dernière mise à jour : 22 mars 2016*

Les actions sont des fragments de code sans état qui s'exécutent sur la plateforme {{site.data.keyword.openwhisk}}. Il peut s'agir d'une
fonction JavaScript, d'une fonction Swift ou d'un programme exécutable personnalisé conditionné dans un conteneur Docker. Par exemple, une action peut
être utilisée pour détecter les visages dans une image, agréger un ensemble d'appels API ou publier un tweet.
{:shortdesc}

Les actions peuvent être appelées explicitement ou s'exécuter en réponse à un événement. Dans tous les cas, l'exécution d'une action génère un enregistrement d'activation identifié par un ID d'activation unique. L'entrée
pour une action et le résultat d'une action constituent un dictionnaire de paires clé-valeur, où la clé est une chaîne et la valeur est une valeur JSON
valide.

Les actions peuvent être composées d'appels à d'autres actions ou à une séquence définie d'actions.

## Création et appel d'actions JavaScript
{: #openwhisk_create_action_js}

Les sections ci-après expliquent comment utiliser des actions dans JavaScript. Vous allez commencer par créer et appeler une action simple,
puis vous apprendrez à ajouter des paramètres à une action et à appeler cette action avec des paramètres, à définir des paramètres par défaut et à les
appeler, à créer des actions asynchrones et enfin, à utiliser des séquences d'actions.


### Création et appel d'une action JavaScript simple
{: #openwhisk_single_action_js}

Suivez les étapes et les exemples ci-dessous pour créer votre première action JavaScript.

1. Créez un fichier JavaScript avec le contenu ci-après. Dans cet exemple, le nom de fichier est 'hello.js'.
  
  ```
  function main() {
      return {payload: 'Hello world'};
  }
  ```
  {: codeblock}

  Le fichier JavaScript peut contenir des fonctions supplémentaires. Toutefois, par convention, une fonction appelée `main` doit
exister pour fournir le point d'entrée de l'action.

2. Créez une action à partir de la fonction JavaScript ci-dessous. Dans cet exemple, l'action s'appelle 'hello'.

  ```
  wsk action create hello hello.js
  ```
  {: pre}
  ```
  ok: created action hello
  ```
  {: screen}

3. Répertoriez les actions que vous avez créées :
  
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  hello       private
  ```
  {: screen}

  Vous pouvez voir l'action `hello` que vous venez de créer.

4. Une fois l'action créée, vous pouvez l'exécuter dans le cloud dans {{site.data.keyword.openwhisk_short}} avec la commande 'invoke'. Vous
pouvez appeler des actions avec un appel *bloquant* ou *non bloquant* en spécifiant un indicateur dans la commande. Un appel
bloquant attend la fin de l'exécution de l'action avant de renvoyer un résultat. Cet exemple utilise le paramètre de blocage `-blocking` :

  ```
  wsk action invoke --blocking hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
  response:
  {
      "result": {
          "payload": "Hello world"
      },
      "status": "success",
      "success": true
  }
  ```
  {: screen}

  La commande génère deux informations importantes :
  * L'ID d'activation (`44794bd6aab74415b4e42a308d880e5b`)
  * Le résultat de l'appel

  Dans ce cas, le résultat est la chaîne `Hello world` renvoyée par la fonction JavaScript. L'ID d'activation peut être utilisé pour
extraire les journaux ou le résultat de l'appel ultérieurement.  

5. Si vous n'avez pas besoin du résultat de l'action immédiatement, vous pouvez omettre l'indicateur `--blocking` pour effectuer
un appel non bloquant. Vous pouvez afficher le résultat ultérieurement avec l'ID d'activation. Exemple :

  ```
  wsk action invoke hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: screen}

  ```
  wsk activation result 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: pre}
  ```
  {
      "payload": "Hello world"
  }
  ```
  {: screen}

6. Si vous oubliez de noter l'ID d'activation, vous pouvez afficher la liste des activations demandées, de la plus récente à la plus ancienne. Exécutez
la commande suivante pour obtenir la liste de vos activations :

  ```
  wsk activation list
  ```
  {: pre}
  ```
  activations
  44794bd6aab74415b4e42a308d880e5b         hello
  6bf1f670ee614a7eb5af3c9fde813043         hello
  ```
  {: screen}

### Transmission de paramètres à une action
{: #openwhisk_adding_parameters_js}

Des paramètres peuvent être transmis à l'action lorsqu'elle est appelée.

1. Utilisez des paramètres dans l'action. Par exemple, mettez à jour le fichier 'hello.js' avec le contenu suivant :
  
  ```
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

  Les paramètres d'entrée sont transmis sous forme de paramètre d'objet JSON à la fonction `main`. Remarquez la façon dont les
paramètres `name` et `place` sont extraits de l'objet `params` dans cet exemple.

2. Mettez à jour l'action `hello` et appelez-la en lui transmettant les valeurs de paramètre `name` et
`place`. Exemple :
  
  ```
  wsk action update hello hello.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Vermont'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  Remarquez l'utilisation de l'option `--param` pour spécifier un nom et une valeur de paramètre, ainsi que de l'option
`--result` pour afficher le résultat de l'appel seulement.

### Définition de paramètres par défaut
{: #openwhisk_binding_actions}

Les actions peuvent être appelées avec plusieurs paramètres nommés. Souvenez-vous : l'action `hello` de l'exemple précédent attend
deux paramètres, le nom d'une personne (*name*) et l'endroit d'où elle vient (*place*).

Plutôt que de transmettre tous les paramètres à une action à chaque fois, vous pouvez lier certains paramètres. L'exemple suivant lie le paramètre
*place* pour que l'action prenne par défaut la valeur "Vermont" pour le paramètre place :
 
1. Mettez à jour l'action avec l'option `--param` pour lier des valeurs de paramètre.

  ```
  wsk action update hello --param place 'Vermont'
  ```
  {: pre}

2. Appelez l'action en ne transmettant cette fois que le paramètre `name`.

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  Notez que vous n'avez pas eu besoin de spécifier le paramètre place lorsque vous avez appelé l'action. Toutefois, vous pouvez remplacer les
paramètres liés en spécifiant la valeur de paramètre au moment de l'appel.

3. Appelez l'action en transmettant les valeurs `name` et `place`. Cette dernière remplace la valeur liée à
l'action.

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Washington, DC'
  ```
  {: pre}
  ```
  {  
      "payload": "Hello, Bernie from Washington, DC"
  }
  ```
  {: screen}

### Création d'actions asynchrones
{: #openwhisk_asynchrony_js}

Il se peut que les fonctions JavaScript dont l'exécution continue dans une fonction de rappel doivent renvoyer le résultat d'activation après le
retour de la fonction `main`. Pour ce faire, utilisez les fonctions `whisk.async()` et `whisk.done()` dans votre action.

1. Sauvegardez le contenu ci-dessous dans un fichier appelé `asyncAction.js`.

  ```
  function main() {
      setTimeout(function() {
          return whisk.done({done: true});
      }, 20000);
      return whisk.async();
  }
  ```
  {: codeblock}

  Remarquez que la fonction `main` renvoie des informations immédiatement et que la valeur de retour `whisk.async()`
indique que cette activation doit continuer de s'exécuter.

  Dans ce cas, la fonction JavaScript `setTimeout()` attend vingt secondes avant d'appeler la fonction de rappel, où
l'appel à `whisk.done()` indique que l'activation est terminée.

2. Exécutez les commandes suivantes pour créer l'action et l'appeler :

  ```
  wsk action create asyncAction asyncAction.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result asyncAction
  ```
  {: pre}
  ```
  {
      "done": true
  }
  ```
  {: screen}

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
  {: screen}


  ```
  wsk activation get b066ca51e68c4d3382df2d8033265db0
  ```
  {: pre}
 ```
  {
      "start": 1455881628103,
      "end":   1455881648126,
      ...
  }
  ```
  {: screen}

  En comparant les horodatages de début (`start`) et de fin (`end`) dans l'enregistrement d'activation, vous
pouvez déterminer que l'activation a duré un peu plus de vingt secondes.


### Utilisation d'actions pour appeler une API externe
{: #openwhisk_apicall_action}

Jusqu'à présent, les exemples ont été des fonctions JavaScript autonomes. Vous pouvez également créer une action qui appelle une API externe.

Cet exemple appelle un service météorologique Yahoo afin de prendre connaissance des conditions en cours à un endroit spécifique. 

1. Sauvegardez le contenu ci-dessous dans un fichier appelé `weather.js`.
  ```
    var request = require('request');
    
    function main(msg) {
        var location = msg.location || 'Vermont';
        var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';
    
        request.get(url, function(error, response, body) {
            var condition = JSON.parse(body).query.results.channel.item.condition;
            var text = condition.text;
            var temperature = condition.temp;
            var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
            whisk.done({msg: output});
        });
    
        return whisk.async();
    }
  ```
  {: codeblock}

  Notez que l'action dans l'exemple utilise la bibliothèque JavaScript `request` pour envoyer une demande HTTP à l'API Yahoo
Weather, et extrait des zones du résultat JSON. La section [Références](./openwhisk_reference.html#runtime_ref_runtime_environment)
présente en détail les packages Node.js que vous pouvez utiliser dans vos actions.
  
  Cet exemple illustre également la nécessité d'actions asynchrones. L'action renvoie `whisk.async()` pour indiquer que le résultat
de cette action n'est pas encore disponible au retour de la fonction. A la place, le résultat est disponible dans le rappel `request` une
fois l'appel HTTP terminé, et est transmis sous forme d'argument à la fonction `whisk.done()`.

2. Exécutez les commandes suivantes pour créer l'action et l'appeler :
  ```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location 'Brooklyn, NY'
  ```
  {: pre}
  ```
  {
      "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
  }
  ```
  {: screen}

### Création de séquences d'actions
{: #openwhisk_create_action_sequence}

Vous pouvez créer une action qui assemble des actions dans une séquence.

Plusieurs actions d'utilitaire sont fournies dans un package appelé `/whisk.system/util`, que vous pouvez utiliser pour créer votre
première séquence. Pour en savoir plus sur les packages, voir la section [Packages](./openwhisk_packages.html).

1. Affichez les actions du package `/whisk.system/util`.
  
  ```
  wsk package get --summary /whisk.system/util
  ```
  {: pre}
  ```
  package /whisk.system/util
   action /whisk.system/util/cat: Concatenate array of strings, and split lines into an array
   action /whisk.system/util/head: Filter first K array elements and discard rest
   action /whisk.system/util/date: Get current date and time
   action /whisk.system/util/sort: Sort array
  ```
  {: screen}

  Dans cet exemple, vous allez utiliser les actions `cat` et `sort`.

2. Créez une séquence d'actions pour que le résultat d'une action soit transmis sous forme d'argument à l'action suivante.
  
  ```
  wsk action create monAction --sequence /whisk.system/util/cat,/whisk.system/util/sort
  ```
  {: pre}

  Cette séquence d'action convertit des lignes de texte en tableau et trie les lignes.

3. Avant d'appeler la séquence d'actions, créez un fichier texte appelé 'haiku.txt' contenant quelques lignes de texte :

  ```
  Over-ripe sushi,
  The Master
  Is full of regret.
  ```
  {: codeblock}

4. Appelez l'action :
  
  ```
  wsk action invoke --blocking --result monAction --param payload "$(cat haiku.txt)"
  ```
  {: pre}
  ```
  {
      "length": 3,
      "lines": [
          "Is full of regret.",
          "Over-ripe sushi,",
          "The Master"
      ]
  }
  ```
  {: screen}

  Vous constatez que les lignes sont triées dans le résultat.

**Remarque** : pour plus d'informations sur l'appel de séquences d'actions avec plusieurs paramètres nommés, voir
[Définition de paramètres par défaut](./openwhisk_actions.html##openwhisk_binding_actions).

## Création d'actions Swift
{: #openwhisk_actions_swift}

Le processus de création d'actions Swift est similaire au processus de création d'actions JavaScript. Les sections ci-après expliquent comment créer
et appeler une action Swift unique, et comment ajouter des paramètres à cette action.

Vous pouvez aussi utiliser le [bac à sable Swift](https://swiftlang.ng.bluemix.net) en ligne pour tester votre code Swift sans avoir
à installer Xcode sur votre machine.

### Création et appel d'une action
{: #openwhisk_actions_invoke_swift}

Une action est simplement une fonction Swift de niveau supérieur. Par exemple, créez un fichier appelé `hello.swift` avec le contenu
suivant :

```
  func main(args: [String:Any]) -> [String:Any] {
      if let name = args["name"] as? String {
          return [ "greeting" : "Hello \(name)!" ]
      } else {
          return [ "greeting" : "Hello stranger!" ]
      }
  }
```
{: codeblock}

Notez qu'à l'instar des actions JavaScript, les actions Swift consomment et produisent toujours un dictionnaire.

Vous pouvez créer une action {{site.data.keyword.openwhisk_short}} appelée `helloSwift` depuis cette fonction comme suit :

```
wsk action create helloSwift hello.swift
```
{: pre}

Si vous utilisez la ligne de commande et un fichier source `.swift`, il n'est pas nécessaire de spécifier que vous créez une action
Swift (et non une action JavaScript) ; l'outil le détermine à partir de l'extension de fichier.

L'appel d'action est identique pour les actions Swift et les actions JavaScript :

```
wsk action invoke --blocking --result helloSwift --param name World
```
{: pre}

```
  {
      "greeting": "Hello World!"
  }
```
{: screen}

**Attention :** les actions Swift s'exécutent dans un environnement Linux. Swift on Linux est en cours de développement et
{{site.data.keyword.openwhisk_short}} utilise généralement l'édition disponible la plus récente, qui n'est pas nécessairement stable. De plus, il se peut que la version de Swift qui est utilisée avec {{site.data.keyword.openwhisk_short}} ne corresponde pas aux versions de Swift
provenant d'éditions stables de Xcode sous MacOS.

## Création d'actions Docker
{: #openwhisk_actions_docker}

Avec les actions {{site.data.keyword.openwhisk_short}} Docker, vous pouvez écrire vos actions dans n'importe quel langage.

Votre code est compilé dans une fichier binaire exécutable et imbriqué dans une image Docker. Le programme binaire interagit avec le système en prenant l'entrée provenant de `stdin` et en répondant par le biais de `stdout`.

Au préalable, vous devez disposer d'un compte Docker Hub.  Pour configurer un ID et un compte Docker gratuits, visitez [Docker Hub](https://hub.docker.com){: new_window}.

Pour les instructions qui suivent, on suppose que l'ID utilisateur est "janesmith" et que le mot de passe est "janes_password".  Si l'on
suppose que l'interface de ligne de commande a déjà été configurée, trois étapes sont requises pour configurer un fichier binaire personnalisé
qu'{{site.data.keyword.openwhisk_short}} utilisera.  Ensuite, l'image Docker téléchargée peut être utilisée en tant qu'action.

1. Téléchargez le squelette Docker. Vous pouvez le télécharger via l'interface de ligne de commande comme suit :

  ```
  wsk sdk install docker
  ```
  {: pre}
  ```
  A présent, le squelette Docker est installé dans le répertoire en cours.
  ```
  {: screen}

  ```
  ls dockerSkeleton/
  ```
  {: pre}
  ```
  Dockerfile      README.md       buildAndPush.sh client          server
  ```
  {: screen}

  Le squelette est un modèle de conteneur Docker dans lequel vous pouvez injecter votre code sous la forme de fichiers binaires personnalisés.

2. Configurez votre fichier binaire personnalisé dans le squelette Docker. Le squelette inclut déjà un programme C que vous pouvez utiliser.

  ```
  cat ./dockerSkeleton/client/example.c
  ```
  {: pre}
  {: pre}
  ```
  #include <stdio.h>
  
  int main(int argc, char *argv[]) {
      printf("Hello %s from arbitrary C program!\n",
             (argc == 1) ? "anonymous" : argv[1]);
  }
  ```
  {: screen}

  Vous pouvez modifier ce fichier en fonction de vos besoins.

3. Générez l'image Docker et téléchargez-la à l'aide d'un script fourni. Vous devez d'abord exécuter `docker
login` pour l'authentification, puis exécuter le script avec le nom d'image de votre choix.

  ```
  docker login -u janesmith -p janes_password
  ```
  {: pre}
  ```
  cd dockerSkeleton
  ```
  {: pre}
  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}

  Notez qu'une partie du fichier example.c est compilée dans le cadre du processus de génération de l'image Docker ; par conséquent, il n'est pas
nécessaire que C soit compilé sur votre machine.

4. Pour créer une action depuis une image Docker plutôt que depuis un fichier JavaScript fourni, ajoutez `--docker` et remplacez le
nom de fichier JavaScript par le nom d'image Docker.

  ```
  wsk action create --docker example janesmith/blackboxdemo
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result example --param payload Rey
  ```
  {: pre}
  ```
  {
      "msg": "Hello Rey from arbitrary C program!\n"
  }
  ```
  {: screen}


Des informations sur la création d'actions Docker sont disponibles dans la section
[Références](./openwhisk_reference.html#openwhisk_ref_docker).


## Surveillance de la sortie des actions
{: #openwhisk_actions_polling}

Des actions {{site.data.keyword.openwhisk_short}} peuvent être appelées par d'autres utilisateurs en réponse à divers événements, ou dans
le cadre d'une séquence d'actions. Dans ces cas, il peut être utile de surveiller les appels.

Vous pouvez utiliser l'interface de ligne de commande {{site.data.keyword.openwhisk_short}} pour surveiller la sortie des actions, au fur et
à mesure qu'elles sont appelées.

1. Emettez la commande suivante depuis un interpréteur de commandes :
  ```
  wsk activation poll
  ```
  {: pre}

  Cette commande démarre une boucle d'interrogation qui consulte en permanence les journaux des activations.

2. Passez dans une autre fenêtre et appelez une action :

  ```
  wsk action invoke /whisk.system/samples/helloWorld --param payload Bob
  ```
  {: pre}
  ```
  ok: invoked /whisk.system/samples/helloWorld with id 7331f9b9e2044d85afd219b12c0f1491
  ```
  {: screen}

3. Observez le journal d'activation dans la fenêtre d'interrogation :

  ```
  Activation: helloWorld (7331f9b9e2044d85afd219b12c0f1491)
    2016-02-11T16:46:56.842065025Z stdout: hello bob!
  ```
  {: screen}

  De même, à chaque fois que vous exécutez l'utilitaire d'interrogation, vous pouvez consulter en temps réel les journaux des actions qui
s'exécutent pour vous dans {{site.data.keyword.openwhisk_short}}.

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
  {: screen}

2. Vérifiez que l'action n'apparaît plus dans la liste des actions.
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  ```
  {: screen}
