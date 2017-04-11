---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-01"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Kit d'outils de bouclier
{: #iot4i_shield_toolkit}
Les boucliers permettent de protéger la propriété et les utilisateurs en identifiant les risques et en créant les réponses automatisées appropriées. Utilisez
ou modifiez les boucliers inclus dans la bibliothèque de boucliers
{{site.data.keyword.iotinsurance_short}}, ou créez et implémentez vos propres
boucliers à l'aide des instructions et des exemples suivants.
{:shortdesc}

## A propos des boucliers
Un bouclier est un ensemble de règles et d'actions définies qui peuvent être déclenchées par certaines conditions présentes dans les entrées reçues de la part d'un capteur. Vous pouvez ainsi créer un bouclier avec une règle qui génère un message texte à envoyer lorsqu'un capteur détecte une fuite d'eau. 

## Utilisation des boucliers de la bibliothèque de boucliers {{site.data.keyword.iotinsurance_short}}

Vous trouverez de nombreux boucliers prédéfinis dans la [bibliothèque de boucliers {{site.data.keyword.iotinsurance_short}} ![Icône de lien externe](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-shields){: new_window}. Consultez le fichier Readme sur ce site pour obtenir les instructions de téléchargement et commencer à utiliser les boucliers.

## Création de vos propres boucliers
Cet exemple vous montre comment configurer votre environnement, définir un bouclier, créer un utilisateur et associer le bouclier à l'utilisateur.  De plus, vous pouvez éventuellement créer des promotions et des risques simulés.  

Des exemples de code permettant de créer un bouclier simple pour des fuites d'eau sont illustrés dans les sections ci-après. Un jeu complet d'exemple de code est disponible dans le [référentiel GitHub iot4i-api-examples-nodejs](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/).

### Conditions préalables
Avant de commencer, vérifiez que les conditions préalables suivantes sont réunies :

- [Node.js](https://nodejs.org/en/) installé sur votre ordinateur.  
- Un environnement d'exécution compatible avec Node.js tel qu'Eclipse.
- Le logiciel Git et l'accès au [référentiel de code source GitHub pour les exemples d'API](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).   Vous pouvez aussi télécharger l'[archive avec les fichiers de code source](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip).
- Le code source préparé.  
  Pour préparer le code source, procédez comme suit :
  1. Clonez ou téléchargez le [référentiel de code source GitHub](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs) sur votre ordinateur.
  2. Installez les éléments open source requis du projet en utilisant une ligne de commande pour accéder au dossier contenant les fichiers de code source clonés et en exécutant la commande `npm install`.

### Configuration de votre environnement
{: #environment}
Afin de configurer votre environnement pour l'envoi d'appels d'API REST, vous devez configurer l'URL pour l'API dans le fichier config.js. L'URL de regroupeur peut être ignorée dans ce contexte.

```
var config = module.exports = {
  api: "https//iot4insurance-api-<uniqueid>.mybluemix.net",
  aggregator: "https//iot4i-aggregator-<uniqueid>.mybluemix.net",
  credentials : {
    user: "Admin",
    pass: "<password from IoT4I service credentials>"
  }
};
```

### Création d'une définition de bouclier
{: #create_shield_def}

Méthode : POST  
API : /shield  
https://iot4i-docs-api.mybluemix.net/dist/#!/shield/addShield

Créez une définition de bouclier dans le fichier createShield.js.  L'exemple suivant illustre un bouclier simple qui détecte une fuite d'eau.

```
var shield = {
  "UUID": "26",
  "name": "demoShield",
  "type": "Environmental Measurements",
  "description": "Detect water leaks",
  "image": "shieldWater",
  "canBeDisabled": false,
  "hazardDetectionOnCloud": true,
  "jsCodeMethod": "demoShield",
  "actions": [
     "pushios"
  ],
  "potentialClaimAmount": "10",
  "shieldParameters": []
};

```

où :
- **UUID** est l'identificateur unique universel du bouclier.
- **actions** est une liste d'actions déclenchées lorsqu'un risque est créé. Dans cet exemple, les informations sur le risque sont envoyées à l'application de l'utilisateur à l'aide d'une notification push iOS.

### Création d'un code de bouclier
{: #create_shield_code}
Créez un code de bouclier dans le fichier shieldCode.js pour définir de quelle manière le moteur de bouclier traite un contenu.

L'exemple suivant illustre un code de bouclier pouvant servir au traitement d'un contenu de fuite d'eau pour le bouclier affiché dans les exemples précédents.

```
var shieldCode = {
  "name": "demoshield",
  "shieldUUID": "26",
  "type": "shield",
  "code": code.toString()
};

```

Chaque code de bouclier contient des ressource qui sont définies dans les instructions resource/shield.js. Chacune des ressources suivantes inclut un exemple qui peut être utilisé avec le bouclier, le contenu et l'utilisateur illustrés dans les exemples précédents.

  - Nom de bouclier  
  ```
  var DEMO_SHIELD_NAME = "demoshield";
  ```

  - Temps d'attente du bouclier - Temps d'attente, exprimé en millisecondes, entre les risques.  
  ```
  var DEMO_SHIELD_DELAY = 5000;
  ```

  - Identificateur unique universel de bouclier  
  ```
  var DEMO_SHIELD_UUID = 26;
  ```

  - Condition d'entrée - Condition et attributs requis pour que le moteur de bouclier puisse traiter le contenu. Dans l'exemple, la condition est que le contenu doit comporter l'attribut **liquid_detected**.  
  ```
  var demoEntryCondition = function(payload) {
    return (payload.liquid_detected)
  };
  ```

  - Safelet - Coeur du bouclier qui calcule et exécute un algorithme afin de déterminer si un risque est présent. Dans l'exemple suivant, le seul attribut requis est **liquid_detected**, mais des safelets peuvent être utilisés pour définir des algorithmes complexes.  
  ```
  var demoSafelet = function(payload) {
    return (payload.liquid_detected);
  };
  ```

  - Message - Message qui est envoyé à l'utilisateur si le risque est traité.
  ```
  var demoMessage = function(payload) {
    return (constructMessage(payload, DEMO_SHIELD_UUID, 'demoHazard', 'a demo shield activated!'));
  };
  ```

  - Exécution du bouclier - Fonction qui est utilisée pour exécuter directement le bouclier, au lieu d'attendre que le moteur de bouclier exécute automatiquement tous les boucliers appropriés.  
  ```
  var demoShield = function(payload) {
    var shield = getShieldByName(DEMO_SHIELD_NAME);
    return (commonShield (payload, shield));
  };
  ```

  - Enregistrement de bouclier - Fonction prédéfinie qui doit être appelée dans le code de bouclier pour enregistrer le bouclier dans le moteur de bouclier. La valeur**undefined** illustrée dans l'exemple représente la fonction de prétraitement, laquelle n'est pas nécessaire dans cet exemple. Dans certains boucliers, la fonction de prétraitement peut être utilisée pour réorganiser les données dans le contenu. Par exemple, si des relevés de température sont indiqués en Fahrenheit alors que le safelet nécessite des données exprimées en Celsius, la fonction de prétraitement peut servir à convertir les températures dans la valeur demandée.  
  ```
  registerShield(DEMO_SHIELD_UUID, DEMO_SHIELD_NAME, demoEntryCondition, undefined, demoSafelet, demoMessage, DEMO_SHIELD_DELAY);
  ```

### Création d'un utilisateur
{: #create_user}

Méthode : POST  
API : /user  
https://iot4i-docs-api.mybluemix.net/dist/#!/user/addUser

Créez un utilisateur dans le fichier createUser.js. L'exemple suivant montre comment créer un seul utilisateur :

```
var user = {
  "username": "user1",
  "fullname": "John Doe",
  "firstname": "John",
  "lastname": "Doe",
  "password": "user1234",
  "accessLevel": "100",
  "address": "42 Wallaby Way, Sydney",
  "email": "user@example.com",
  "deviceID": "user1",
  "deviceType": "wink",
  "type": "wink"
};

```

où :
- **username** est la clé unique de l'utilisateur permettant d'identifier chaque entité associée à l'utilisateur, par exemple, des terminaux, des boucliers et des promotions.
- **password** - Seul le hachage du mot de passe est stocké dans la base de données.
- **DeviceId** est l'identificateur utilisé pour enregistrer l'utilisateur dans {{site.data.keyword.iot_full}}. Cette valeur est identique au nom d'utilisateur (username)
- La valeur de **accessLevel** définit les noeuds finaux d'API auxquels l'utilisateur peut accéder :
  - 100 - application mobile
  - 10 - tableau de bord
  - 1 - administrateur système

### Création d'une association de bouclier
{: #create_shield_assoc}

Méthode : POST  
API : /user  
https://iot4i-docs-api.mybluemix.net/dist/#!/shieldassociation/addShieldAssociation

Créez dans le fichier createUserShieldAssociation.js une association de bouclier qui lie le bouclier à l'utilisateur.

L'exemple suivant illustre une association de bouclier pour le bouclier et l'utilisateur ayant été créés dans les sections précédentes :

```
var userShield = {
  "shieldUUID": "26",
  "username": "user1",
  "hazardDetectionOnCloud": true
};

```



### Création d'un risque simulé
{: #create_sim_hazard}

Méthode : POST  
API : /sendPayloadToMQTT  
https://iot4i-docs-api.mybluemix.net/dist/#!/global/sendPayloadToMQTT

Vous pouvez créer un contenu de risque simulé pour tester vos boucliers.

L'exemple suivant montre comment créer un contenu qui active le bouclier créé dans l'exemple précédent et envoie une alerte à l'utilisateur associé au bouclier :

```
var parameters {
  "payload": {
    "sensor_pod_id": "190107",
    "name": "Sensor",
    "manufacturer_device_model": "leakSMART",
    "device_manufacturer": "leaksmart",
    "model_name": "leakSMART Sensor",
    "upc_code": "waxman_sensor",
    "hub_id": "379652",
    "lat_lng": [null, null],
    "location": "",
    "status": "online",
    "liquid_detected": true,
    "usr": "user1",
    "activation": "2016-06-20T12:05:02.776Z"
  },
  "outputtype": "evt",
  "devicetype": "wink",
  "deviceid": "wink",
  "type": "wink"
};

```


### Création d'une promotion
{: #create_promotion}

{{site.data.keyword.iotinsurance_short}} peut envoyer des promotions au propriétaire d'un logement à l'aide de l'application mobile. Créez des promotions à l'aide du fichier createPromotion.js.

L'exemple suivant montre comment créer une promotion pour un plombier agréé :

```
var promotion = {
  "title": "Promotion 9",
  "description": "Contact one of our authorized plumbers to install your water leak detection solution.",
  "buttonTitle": "Call Now",
  "type": "1",
  "phone": "+015555555555",
  "username": "user1",  
};

```

Vous pouvez éventuellement déployer votre application mobile et utiliser [les instructions contenues dans le référentiel GitHub ioti-mobile](https://github.com/ibm-watson-iot/ioti-mobile) pour vous connecter avec l'ID utilisateur que vous avez créé dans la section précédente.

# Liens connexes
{: #rellinks}

## Référence d'API
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [Exemples d'API {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}

## Liens connexes
{: #general}
* [Forum de
support des développeurs](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Forum de support stackoverflow](http://stackoverflow.com/questions/tagged/ibm-bluemix)
