---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Création de déclencheurs et de règles
{: #openwhisk_triggers}
*Dernière mise à jour : 22 février 2016*

Les déclencheurs et les règles {{site.data.keyword.openwhisk}} apportent des capacités gérées par des événements sur la
plateforme. Les événements provenant de sources d'événements externes et internes sont canalisés via un déclencheur, et des règles autorisent vos actions
à réagir à ces événements.
{: shortdesc}

## Déclencheurs

Les déclencheurs constituent un canal nommé pour une classe d'événements. Voici des exemples de déclencheur :
- Déclencheur d'événements de mise à jour d'emplacement
- Déclencheur de mises à jour de document sur un site Web
- Déclencheur de courriers électroniques entrants

Les déclencheurs peuvent être *exécutés* (activés) à l'aide d'un dictionnaire de paires clé-valeur. Parfois, ce dictionnaire est
appelé *événement*. Comme pour les actions, chaque exécution de déclencheur génère un ID d'activation.

Les déclencheurs peuvent être exécutés explicitement par un utilisateur ou pour le compte d'un utilisateur par une source d'événements d'externe.
Un
*flux* est pratique pour configurer une source d'événements externe afin d'exécuter des événements déclencheurs qui peuvent être consommés par {{site.data.keyword.openwhisk_short}}. Voici
des exemples de flux :
- Flux de modifications de données Cloudant qui exécute un déclencheur à chaque fois qu'un document dans une base de données est ajouté ou modifié
- Flux Git qui exécute un déclencheur pour chaque validation dans un référentiel Git

## Règles

Une règle associe un déclencheur à une action, chaque exécution du déclencheur entraînant l'appel de l'action correspondante avec l'événement
déclencheur en entrée.

Avec le jeu de règles approprié, un événement déclencheur unique peut appeler plusieurs actions, ou une action peut être appelée en réponse à des
événements provenant de plusieurs déclencheurs.

Par exemple, imaginez un système avec les actions suivantes :
- L'action `classifyImage`, qui détecte les objets dans une image et les classe
- L'action `thumbnailImage`, qui crée une version miniature d'une image

De plus, supposez que deux sources d'événements exécutent les déclencheurs suivants :
- Le déclencheur `newTweet`, qui est exécuté lorsqu'un nouveau tweet est publié
- Le déclencheur `imageUpload`, qui est exécuté lorsqu'une image est téléchargée sur un site Web

Vous pouvez configurer des règles pour qu'un événement déclencheur unique appelle plusieurs actions, et pour que plusieurs déclencheurs appellent
la même action :
- La règle `newTweet -> classifyImage`
- La règle `imageUpload -> classifyImage`
- La règle `imageUpload -> thumbnailImage`

Les trois règles établissent le comportement suivant : les images dans les tweets et les images téléchargées sont classées, les images téléchargées
sont classées, et une version miniature est générée. 

## Création et exécution de déclencheurs
{: #openwhisk_triggers}

Des déclencheurs peuvent être exécutés lorsque certains événements surviennent, ou manuellement.

Par exemple, créez un déclencheur pour envoyer les mises à jour de l'emplacement d'utilisateur, et exécutez manuellement le déclencheur.

1. Entrez la commande suivante pour créer le déclencheur :
 
  ```
  wsk trigger create locationUpdate
  ```
  {: pre}
 
  ```
  ok: created trigger locationUpdate
  ```
  {: screen}

2. Vérifiez que le déclencheur a été créé en affichant la liste des déclencheurs.

  ```
  wsk trigger list
  ```
  {: pre}
 
  ```
  triggers
  /someNamespace/locationUpdate                            private
  ```
  {: screen}

  Jusqu'à présent, vous avez créé un "canal" nommé dans lequel des événements peuvent être déclenchés.

3. Ensuite, exécutez un événement déclencheur en spécifiant le nom du déclencheur et des paramètres :

  ```
  wsk trigger fire locationUpdate --param name "Donald" --param place "Washington, D.C."
  ```
  {: pre}

  ```
  ok: triggered locationUpdate with id fa495d1223a2408b999c3e0ca73b2677
  ```
  {: screen}

   Pour l'instant, les événements que vous exécutez dans le déclencheur statusUpdate n'ont pas d'effet. Pour être utile, le déclencheur requiert une
règle qui l'associe à une action.


## Utilisation de règles pour associer des déclencheurs et des actions
{: #openwhisk_rules}

Des règles sont utilisées pour associer un déclencheur à une action. A chaque fois qu'un événement déclencheur est exécuté, l'action est appelée
avec les paramètres d'événement.

Par exemple, créez une règle qui appelle l'action hello à chaque fois qu'une mise à jour d'emplacement est publiée. 

1. Créez un fichier 'hello.js' avec le code d'action à utiliser :
  ```
  function main(params) {
     return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

2. Vérifiez que le déclencheur et l'action existent.
  ```
  wsk trigger update locationUpdate
  ```
  {: pre}
  
  ```
  wsk action update hello hello.js
  ```
  {: pre}

3. Créez et activez la règle. Les trois paramètres sont le nom de la règle, le déclencheur et l'action.
  ```
  wsk rule create --enable maRègle locationUpdate hello
  ```
  {: pre}

4. Exécutez le déclencheur locationUpdate. A chaque fois que vous déclenchez un événement, l'action hello est appelée avec les paramètres
d'événement.
  ```
  wsk trigger fire locationUpdate --param name "Donald" --param place "Washington, D.C."
  ```
  {: pre}
  
  ```
  ok: triggered locationUpdate with id d5583d8e2d754b518a9fe6914e6ffb1e
  ```
  {: screen}

5. Assurez-vous que l'action a été appelée en vérifiant l'activation la plus récente.
  ```
  wsk activation list --limit 1 hello
  ```
  {: pre}
  
  ```
  activations
  9c98a083b924426d8b26b5f41c5ebc0d             hello
  ```
  {: screen}
  
  ```
  wsk activation result 9c98a083b924426d8b26b5f41c5ebc0d
  ```
  {: pre}
  ```
  {
     "payload": "Hello, Donald from Washington, D.C."
  }
  ```
  {: screen}

  Vous constatez que l'action hello a reçu le contenu de l'événement et a renvoyé la chaîne attendue.

  Vous pouvez créer plusieurs règles qui associent le même déclencheur à des actions différentes.
