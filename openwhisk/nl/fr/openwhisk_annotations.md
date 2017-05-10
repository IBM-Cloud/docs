---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Annotations sur des actifs OpenWhisk

Les actions, les déclencheurs, les règles et les packages OpenWhisk (collectivement désignés comme les actifs) peuvent être décorés d'`annotations`. Des annotations sont associées à des actifs comme des paramètres avec une `clé` qui définit un nom et une `valeur` qui définit la valeur. Il est pratique de les définir à partir de l'interface de ligne de commande via `--annotation` ou `-a` (forme abrégée).
{: shortdesc}

Raison : Des annotations ont été ajoutées à OpenWhisk pour permettre de s'exercer sans modifier le schéma d'actif sous-jacent. Avant la rédaction du présent document, nous avions délibérément choisi de ne pas définir les `annotations` autorisées. Toutefois, alors que nous commençons à faire un usage plus intensif des annotations pour communiquer les modifications sémantiques, il s'avère indispensable de les documenter.

A ce jour, l'utilisation la plus répandue des annotations consiste à documenter des actions et des packages. Vous verrez qu'un grand nombre de packages du catalogue OpenWhisk comportent des annotations, par exemple, une description de la fonctionnalité offerte par leurs actions, des spécifications précisant quels sont les paramètres requis lors de la liaison de packages et quels les paramètres d'appel et si un paramètre est un "secret" (par exemple, un mot de passe) ou non. Nous avons inventé ces annotations selon les besoins, par exemple, pour autoriser l'intégration d'interface utilisateur.

Voici un exemple d'ensemble d'annotations pour une action `echo` qui renvoie ses arguments d'entrée non modifiés (par exemple, `function main(args) { return args }`). Cette action peut s'avérer utile pour la journalisation des paramètres d'entrée, par exemple, dans le cadre d'une séquence ou d'une règle.

```
wsk action create echo echo.js \
    -a description 'An action which returns its input. Useful for logging input to enable debug/replay.' \
    -a parameters  '[{ "required":false, "description": "Any JSON entity" }]' \
    -a sampleInput  '{ "msg": "Five fuzzy felines"}' \
    -a sampleOutput '{ "msg": "Five fuzzy felines"}'
```
{: pre}

Les annotations que nous avons utilisées pour décrire les packages sont les suivantes :

- `description` : description concise du package
- `parameters` : tableau décrivant les paramètres définis dans la portée du package (détaillés ci-après)

Les annotations que nous avons utilisées pour décrire les actions sont les suivantes : 

- `description` : description concise de l'action
- `parameters` : tableau décrivant les actions requises pour exécuter l'action
- `sampleInput` : exemple illustrant le schéma d'entrée avec des valeurs typiques
- `sampleOutput` : exemple illustrant le schéma de sortie, généralement pour l'exemple `sampleInput`

Les annotations que nous avons utilisées pour décrire les paramètres sont les suivantes :

- `name` : nom du paramètre
- `description` : description concise du paramètre
- `doclink` : lien vers de la documentation supplémentaire relative au paramètre (utile pour les jetons OAuth par exemple) 
- `required` : true pour les paramètres requis et false pour les paramètres facultatifs
- `bindTime` : true si le paramètre doit être spécifié lorsqu'un package est lié
- `type` : type du paramètre, `password`, `array` (mais peut être utilisé plus largement)

Les annotations ne sont *pas* vérifiées. Par conséquent, s'il est concevable d'utiliser les annotations, par exemple, pour déduire si une composition de deux actions dans une séquence est légale, pour l'instant, le système n'effectue pas cette action.

## Annotations spécifiques aux actions Web
{: #openwhisk_annotations_webactions}

Nous avons récemment enrichi l'API centrale en lui adjoignant de nouvelles fonctionnalités. Pour permettre aux packages et aux actions d'exploiter ces fonctionnalités, nous avons introduit les nouvelles annotations suivantes dont la sémantique est significative. La valeur `true` doit être affectée de manière explicite à ces annotations pour que celles-ci aient un effet. Si vous remplacez la valeur `true` par `false`, l'actif associé sera exclu de la nouvelle API. En effet, si la valeur true ne leur est pas affectée, les annotations n'ont aucune signification dans lesystème. Les annotations sont les suivantes :

- `final` : ne s'applique qu'à une action. Rend non modifiables tous les paramètres d'action qui sont déjà définis. Un paramètre d'action véhiculant l'annotation ne peut pas être remplacé par des paramètres d'appel une fois que la valeur du paramètre est définie via le package qui le contient ou la définition d'action.
- `web-export` : ne s'applique qu'à une action. Si elle est présente, cette annotation rend l'action qui lui correspond accessible aux appels REST *sans* authentification. Nous appelons ces annotations des [*actions Web*](openwhisk_webactions.html) car elles permettent d'utiliser des actions OpenWhisk à partir d'un navigateur, par exemple. Il est important de noter que le *propriétaire* de l'action Web supporte le coût lié à son exécution dans le système (le *propriétaire* de l'action possède également l'enregistrement des activations).
- `require-whisk-auth` : s'applique uniquement à une action. Si une action comporte l'annotation `web-export` et que cette annotation indique également `true`, la route n'est accessible qu'à un sujet authentifié. Il est important de noter que le *propriétaire* de l'action Web supporte le coût lié à son exécution dans le système (le *propriétaire* de l'action possède également l'enregistrement des activations).
- `raw-http` : s'applique uniquement à une action accompagnée d'une annotation `web-export`. Si celle-ci est présente, les paramètres de demande et de corps de la demande HTTP sont transmis à l'action en tant que propriétés réservées.

