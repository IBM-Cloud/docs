---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilisation et création de packages {{site.data.keyword.openwhisk_short}}
{: #openwhisk_packages}

Dans {{site.data.keyword.openwhisk_short}}, vous pouvez utiliser des packages afin de regrouper des actions connexes et de les partager.

Un package peut inclure des *actions* et des *flux*.
- Une action est un élément de code qui s'exécute sur {{site.data.keyword.openwhisk_short}}. Par exemple, le package Cloudant inclut des actions permettant de lire et d'écrire des enregistrements dans une base de données Cloudant.
- Un flux est utilisé pour configurer une source d'événements externe afin d'exécuter des événements déclencheurs. Par exemple, le package Alarm inclut un flux qui peut exécuter un déclencheur à la fréquence spécifiée.

Chaque entité {{site.data.keyword.openwhisk_short}}, notamment les packages, appartient à un *espace de nom*, et le nom qualifié complet d'une entité est `/nom_espace_nom[/nom_package]/nom_entité`. Reportez-vous aux [conventions de dénomination](./openwhisk_reference.html#openwhisk_entities) pour plus d'informations.

Les sections ci-après expliquent comment parcourir les packages et utiliser les déclencheurs et les flux qu'ils contiennent. De plus, si vous souhaitez ajouter vos propres packages au catalogue, lisez les sections relatives à la création et au partage de packages.

## Parcours des packages
{: #openwhisk_packagedisplay}

Plusieurs packages sont enregistrés dans {{site.data.keyword.openwhisk_short}}. Vous pouvez obtenir la liste des packages qui se trouvent dans un espace de nom, répertorier les entités qui se trouvent dans un package, et obtenir la description de chaque entité d'un package.

1. Obtenez la liste des packages qui se trouvent dans l'espace de nom `/whisk.system`.

  ```
  wsk package list /whisk.system
  ```
  {: pre}
  ```
  packages
  /whisk.system/cloudant                                                 shared
  /whisk.system/alarms                                                   shared
  /whisk.system/watson                                                   shared
  /whisk.system/websocket                                                shared
  /whisk.system/weather                                                  shared
  /whisk.system/system                                                   shared
  /whisk.system/utils                                                    shared
  /whisk.system/slack                                                    shared
  /whisk.system/samples                                                  shared
  /whisk.system/github                                                   shared
  /whisk.system/pushnotifications                                        shared
  ```

2. Obtenez la liste des entités qui se trouvent dans le package `/whisk.system/cloudant`.

  ```
  wsk package get --summary /whisk.system/cloudant
  ```
  {: pre}
  ```
  package /whisk.system/cloudant: Cloudant database service
     (params: {{site.data.keyword.Bluemix_notm}}ServiceName host username password dbname includeDoc overwrite)
   action /whisk.system/cloudant/read: Read document from database
   action /whisk.system/cloudant/write: Write document to database
   feed   /whisk.system/cloudant/changes: Database change feed
  ```

  Cette sortie indique que le package Cloudant fournit deux actions, `read` et `write`, ainsi qu'un flux de déclencheur appelé `changes`. Le flux `changes` entraîne l'exécution de déclencheurs lorsque des documents sont ajoutés à la base de données Cloudant spécifiée.

  Le package Cloudant définit également les paramètres `username`, `password`, `host` et `port`. Ceux-ci doivent être spécifiés pour que les actions et les flux aient un sens. Par exemple, les paramètres autorisent les actions sur un compte Cloudant spécifique.

3. Obtenez une description de l'action `/whisk.system/cloudant/read`.

  ```
  wsk action get --summary /whisk.system/cloudant/read
  ```
  {: pre}
  ```
  action /whisk.system/cloudant/read: Read document from database
     (params: dbname includeDoc id)
  ```

  Cette sortie indique que l'action Cloudant `read` requiert trois paramètres, notamment la base de données et l'ID de document à extraire.


## Appel d'actions dans un package
{: #openwhisk_package_invoke}

Vous pouvez appeler des actions dans un package, à l'instar des autres actions. Les quelques étapes suivantes expliquent comment appeler l'action `greeting` dans le package `/whisk.system/samples` avec différents paramètres.

1. Obtenez une description de l'action `/whisk.system/samples/greeting`.

  ```
  wsk action get --summary /whisk.system/samples/greeting
  ```
  {: pre}
  ```
  action /whisk.system/samples/greeting: Print a friendly greeting
     (params: name place)
  ```

  Remarquez que l'action `greeting` admet deux paramètres : `name` et `place`.

2. Appelez l'action sans paramètre.

  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting
  ```
  {: pre}
  ```json
    {
      "payload": "Hello, stranger from somewhere!"
  }
  ```

  La sortie est un message générique car aucun paramètre n'a été spécifié.

3. Appelez l'action avec des paramètres.

  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting --param name Mork --param place Ork
  ```
  {: pre}
  ```json
    {
      "payload": "Hello, Mork from Ork!"
  }
  ```

  Remarquez que la sortie utilise les paramètres `name` et `place` qui ont été transmis à l'action.


## Création et utilisation de liaisons de package
{: #openwhisk_package_bind}

Vous pouvez utiliser les entités d'un package directement, mais il se peut que vous transmettiez les mêmes paramètres à l'action à chaque fois. Dans ce cas, établissez une liaison à un package et spécifiez des paramètres par défaut. Ces paramètres sont hérités par les actions du package.

Par exemple, dans le package `/whisk.system/cloudant`, vous pouvez définir les valeurs par défaut `username`, `password` et `dbname` dans une liaison de package ; elles seront transmises automatiquement aux actions du package.

Dans l'exemple simple ci-dessous, vous établissez une liaison au package `/whisk.system/samples`.

1. Etablissez la liaison au package `/whisk.system/samples` et définissez une valeur de paramètre `place` par défaut.

  ```
  wsk package bind /whisk.system/samples valhallaSamples --param place Valhalla
  ```
  {: pre}
  ```
  ok: created binding valhallaSamples
  ```

2. Obtenez une description de la liaison de package.

  ```
  wsk package get --summary valhallaSamples
  ```
  {: pre}
  ```
  package /myNamespace/valhallaSamples
   action /myNamespace/valhallaSamples/greeting: Returns a friendly greeting
   action /myNamespace/valhallaSamples/wordCount: Count words in a string
   action /myNamespace/valhallaSamples/helloWorld: Demonstrates logging facilities
   action /myNamespace/valhallaSamples/curl: Curl a host url
  ```

  Remarquez que toutes les actions dans le package `/whisk.system/samples` sont disponibles dans la liaison de package `valhallaSamples`.

3. Appelez une action dans la liaison de package.

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Valhalla!"
  }
  ```

  Remarquez dans le résultat que l'action hérite du paramètre `place` que vous avez défini lorsque vous avez créé la liaison de package `valhallaSamples`.

4. Appelez une action et remplacez la valeur de paramètre par défaut.

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin --param place Asgard
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Asgard!"
  }
  ```

  Remarquez que la valeur de paramètre `place` qui est spécifiée avec l'appel d'action remplace la valeur par défaut définie dans la liaison de package `valhallaSamples`.


## Création et utilisation d'un flux de déclencheur
{: #openwhisk_package_trigger}

Les flux sont pratiques pour configurer une source d'événements externe afin de déclencher ces événements dans un déclencheur {{site.data.keyword.openwhisk_short}}. Cet exemple explique comment utiliser un flux dans le package Alarms afin d'exécuter un déclencheur toutes les secondes, et comment utiliser une règle permettant d'appeler une action toutes les secondes.

1. Obtenez une description du flux dans le package `/whisk.system/alarms`.

  ```
  wsk package get --summary /whisk.system/alarms
  ```
  {: pre}
  ```
  package /whisk.system/alarms
   feed   /whisk.system/alarms/alarm
  ```

  ```
  wsk action get --summary /whisk.system/alarms/alarm
  ```
  {: pre}
  ```
  action /whisk.system/alarms/alarm: Fire trigger when alarm occurs
     (params: cron trigger_payload)
  ```

  Le flux `/whisk.system/alarms/alarm` admet deux paramètres :
  - `cron` : spécification crontab indiquant à quel moment exécuter le déclencheur.
  - `trigger_payload` : valeur de paramètre de contenu à définir dans chaque événement déclencheur.

2. Créez un déclencheur qui s'exécute toutes les huit secondes.

  ```
  wsk trigger create everyEightSeconds --feed /whisk.system/alarms/alarm -p cron "*/8 * * * * *" -p trigger_payload "{\"name\":\"Mork\", \"place\":\"Ork\"}"
  ```
  {: pre}
  ```
  ok: created trigger feed everyEightSeconds
  ```

3. Créez un fichier 'hello.js' avec le code d'action suivant :

  ```javascript
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

4. Vérifiez que l'action existe.

  ```
  wsk action update hello hello.js
  ```
  {: pre}

5. Créez une règle qui appelle l'action `hello` à chaque fois que le déclencheur `everyEightSeconds` s'exécute.

  ```
  wsk rule create myRule everyEightSeconds hello
  ```
  {: pre}
  ```
  ok: created rule myRule
  ```

6. Vérifiez que l'action est appelée en interrogeant les journaux d'activation.

  ```
  wsk activation poll
  ```
  {: pre}

  Vous devriez voir des activations toutes les huit secondes pour le déclencheur, la règle et l'action. L'action reçoit les paramètres `{"name":"Mork", "place":"Ork"}` à chaque appel.


## Création d'un package
{: #openwhisk_packages_create}

Un package est utilisé pour organiser un ensemble d'actions et de flux connexes.
Il permet également de partager des paramètres entre toutes les entités du package.

Pour créer un package personnalisé contenant une action simple, procédez comme suit.

1. Créez un package appelé "custom".

  ```
  wsk package create custom
  ```
  {: pre}
  ```
  ok: created package custom
  ```

2. Obtenez un récapitulatif du package.

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /monEspaceNom/custom
  ```

  Remarquez que le package est vide.

3. Créez un fichier appelé `identity.js` contenant le code d'action ci-après. Cette action renvoie tous les paramètres d'entrée.

  ```javascript
  function main(args) { return args; }
  ```
  {: codeblock}

4. Créez une action `identity` dans le package `custom`.

  ```
  wsk action create custom/identity identity.js
  ```
  {: pre}
  ```
  ok: created action custom/identity
  ```

  La création d'une action dans un package requiert que vous ajoutiez le nom de package comme préfixe au nom d'action. L'imbrication de package n'est pas autorisée. Un package ne peut contenir que des actions et ne peut pas comporter d'autres packages.

5. Obtenez à nouveau un récapitulatif du package.

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /monEspaceNom/custom
   action /monEspaceNom/custom/identity
  ```

  A présent, vous pouvez voir l'action `custom/identity` dans votre espace de nom.

6. Appelez l'action dans le package.

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```json
  {}
  ```


Vous pouvez définir des paramètres par défaut pour toutes les entités d'un package. Pour ce faire, définissez des paramètres au niveau du package, qui sont hérités par toutes les actions dans le package. Voici un exemple :

1. Mettez à jour le package `custom` avec deux paramètres : `city` et `country`.

  ```
  wsk package update custom --param city Austin --param country USA
  ```
  {: pre}
  ```
  ok: updated package custom
  ```

2. Affichez les paramètres dans le package et l'action, et remarquez comment l'action `identity` dans le package hérite des paramètres du package.

  ```
  wsk package get custom parameters
  ```
  {: pre}
  ```
  ok: got package custom, displaying field parameters
  ```
  ```json
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```

  ```
  wsk action get custom/identity parameters
  ```
  {: pre}
  ```
  ok: got action custom/identity, , displaying field parameters
  ```
  ```json
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```

3. Appelez l'action identity sans paramètre afin de vérifier qu'elle hérite effectivement des paramètres.

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```json
    {
      "city": "Austin",
      "country": "USA"
  }
  ```

4. Appelez l'action identity avec des paramètres. Les paramètres d'appel sont fusionnés avec les paramètres du package ; ils les remplacent.

  ```
  wsk action invoke --blocking --result custom/identity --param city Dallas --param state Texas
  ```
  {: pre}
  ```json
    {
      "city": "Dallas",
      "country": "USA",
      "state": "Texas"
  }
  ```


## Partage d'un package
{: #openwhisk_packages_share}

Une fois que les actions et les flux qui constituent un package ont été débogués et testés, le package peut être partagé avec tous les utilisateurs d'{{site.data.keyword.openwhisk_short}}. Le partage du package permet aux utilisateurs de lier le package, d'appeler des actions du package et de créer des actions de séquence et des règles {{site.data.keyword.openwhisk_short}}.

1. Partagez le package avec tous les utilisateurs :

  ```
  wsk package update custom --shared yes
  ```
  {: pre}
  ```
  ok: updated package custom
  ```

2. Affichez la propriété `publish` du package pour vérifier qu'elle est désormais associée à la valeur true.

  ```
  wsk package get custom publish
  ```
  {: pre}
  ```
  ok: got package custom, displaying field publish
  ```
  ```json
  true
  ```


Désormais, d'autres utilisateurs peuvent se servir de votre package `custom`, et notamment établir une liaison au package ou appeler directement une action qu'il contient. Pour ce faire, ils doivent connaître les noms qualifiés complets du package. Les actions et les flux qui se trouvent dans un package partagé sont *publics*. Si le package est privé, son contenu est également privé.

1. Obtenez une description du package pour afficher les noms qualifiés complets du package et de l'action.

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /monEspaceNom/custom
   action /monEspaceNom/custom/identity
  ```

  Dans l'exemple précédent, vous utilisiez l'espace de nom `monEspaceNom` et cet espace de nom figure dans le nom qualifié complet.
