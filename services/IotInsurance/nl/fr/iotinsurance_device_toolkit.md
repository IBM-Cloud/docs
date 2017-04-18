---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# Utilisation du kit d'outils de terminal
{: #iot4i_connecting_devices}
Le kit d'outils de terminal d'{{site.data.keyword.iotinsurance_full}} vous permet de connecter des terminaux fabriqués par n'importe quel fournisseur de terminaux à votre service {{site.data.keyword.iotinsurance_short}}.
{:shortdesc}

Les terminaux peuvent envoyer des données directement à {{site.data.keyword.iot_full}} ou via le cloud du fournisseur de terminaux. Vous connectez les terminaux en enregistrant des utilisateurs autorisés, puis en configurant la génération et la réception d'événement de terminal. Pour connaître la liste des terminaux et des fournisseurs pris en charge, ainsi que les procédures d'intégration des exemples, voir [Terminaux et fournisseurs pris en charge](iotinsurance_supporteddevices.html).

Utilisez les instructions décrites dans les sections ci-après pour connecter vos terminaux.

## Enregistrement d'utilisateurs autorisés
{: #reg_users}
Lorsque le cloud du fournisseur de terminaux prend en charge OAuth comme protocole d'autorisation, {{site.data.keyword.iotinsurance_short}} peut faire office de client OAuth et se connecter au cloud du fournisseur. Un ID et une autorisation client obtenus auprès du fournisseur de terminaux sont nécessaires pour recevoir et mettre à jour des données pour le compte de l'utilisateur.  

### Flux OAuth
{: #oauth_flow}
Le diagramme suivant illustre un flux OAuth simplifié dans lequel {{site.data.keyword.iotinsurance_short}} est autorisé via un fournisseur OAuth, tel que Facebook. Dans le diagramme, {{site.data.keyword.iotinsurance_short}} demande un accès à un client OAuth, lequel redirige la demande d'accès vers le fournisseur OAuth. Le fournisseur produit un formulaire HTML dans lequel l'utilisateur {{site.data.keyword.iotinsurance_short}} entre un ID utilisateur et un mot de passe. A ce stade, le fournisseur accorde l'autorisation et renvoie éventuellement un code OAuth pour activer les mises à jour. Le diagramme illustre un flux de base ; les fournisseurs OAuth offrent généralement plusieurs noeuds finaux REST pour les étapes décrites dans le diagramme.  

![Flux de processus OAuth d'{{site.data.keyword.iotinsurance_short}}. Ce
diagramme est décrit dans le corps principal de la rubrique.](images/IoT4I_oauth_flow.svg "{{site.data.keyword.iotinsurance_short}} OAuth process flow")

### Flux d'enregistrement d'utilisateur
{: #user_reg_flow}

L'enregistrement d'utilisateur varie selon le fournisseur. Pour savoir comment obtenir les jetons d'accès au cloud requis et comment les enregistrer auprès d'{{site.data.keyword.iotinsurance_short}} à l'aide de l'API, voir [Terminaux et fournisseurs pris en charge](iotinsurance_supporteddevices.html).

#### Flux d'enregistrement mobile (*obsolète*)

**Remarque** : L'application mobile prend uniquement en charge Wink et les modifications apportées à {{site.data.keyword.amashort}} ont désactivé le flux d’enregistrement d'utilisateur décrit dans cette section. Ce flux est disponible uniquement pour les instances existantes de la version 1.0 d'{{site.data.keyword.iotinsurance_short}}.

Le diagramme ci-après illustre un flux d'enregistrement d'utilisateur simplifié. Dans cet exemple, une nouvelle demande d'enregistrement d'utilisateur est émise par un terminal mobile. La demande est traitée par {{site.data.keyword.amafull}}, lequel fournit un identificateur au système de support du client et envoie la demande au service d'enregistrement d'API. Ce dernier redirige la demande OAuth vers le cloud du fournisseur de terminaux, lequel vérifie l'authentification auprès du système de support du client. Le cloud du fournisseur de terminaux renvoie le code ou jeton d'autorisation au service d'enregistrement d'API. A ce stade, le service d'enregistrement crée l'utilisateur, ainsi qu'un jeton d'API unique dans{{site.data.keyword.iot_short_notm}} et dans {{site.data.keyword.cloudant}}.

![Flux d'enregistrement d'utilisateur d'{{site.data.keyword.iotinsurance_short}}. Ce
diagramme est décrit dans le corps principal de la rubrique.](images/IoT4I_reg_user.svg "{{site.data.keyword.iotinsurance_short}} User registration flow")

## Génération d'événements de terminal
{: #generating_device_events}
Les terminaux peuvent se connecter à {{site.data.keyword.iot_short_notm}} lorsque le fabricant fournit un code d'autorisation direct qui peut être utilisé avec la clé d'API générée lors de l'enregistrement d'utilisateur. Ce type de connexion est décrit dans la rubrique [Développement de terminaux sur {{site.data.keyword.iot_short_notm}}](https://console.{DomainName}/docs/services/IoT/devices/device_dev_index.html).

Lorsqu'un terminal est connecté via le cloud du fournisseur, les événements de terminal sont envoyés via une connexion qui utilise le noeud final REST fourni par le fournisseur de terminaux. Le jeton bearer OAuth obtenu lors de l'enregistrement d'utilisateur accorde l'autorisation nécessaire pour ces appels. Le transformateur {{site.data.keyword.iotinsurance_short}} extrait du cloud du fournisseur les informations utilisateur associées pour chaque terminal. Il inclut ensuite l'association utilisateur avec les données d'événement de terminal qu'il transmet à {{site.data.keyword.iot_short_notm}}.

Lorsque le terminal est directement connecté à {{site.data.keyword.iot_short_notm}}, le lien entre le terminal et l'utilisateur est stocké dans {{site.data.keyword.iot_short_notm}}. Le transformateur {{site.data.keyword.iotinsurance_short}} met ces informations en mémoire cache, puis enrichit les événements de terminal avec le lien vers l'utilisateur.

### Cloud-à-cloud - Flux d'événement de terminal
{: #device_event_flow}
Le diagramme ci-après illustre un flux d'événement de terminal simplifié. Dans cet exemple, un terminal détecte une fuite d'eau. Le transformateur {{site.data.keyword.iotinsurance_short}} interroge périodiquement le cloud du fournisseur à la recherche de modifications du statut du terminal. Lorsque l'événement est détecté, le transformateur l'envoie à {{site.data.keyword.iot_short_notm}}. Le moteur de bouclier {{site.data.keyword.iotinsurance_short}} analyse l'événement, génère une alerte, puis stocke cette dernière dans {{site.data.keyword.cloudant}}. {{site.data.keyword.iot_short_notm}} transfère l'alerte au moteur des actions {{site.data.keyword.iotinsurance_short}} pour analyse. Ensuite, le moteur des actions envoie l'alerte à l'application mobile du client via {{site.data.keyword.mobilepushshort}}.  

![Flux d'enregistrement d'événement de terminal {{site.data.keyword.iotinsurance_short}} Ce
diagramme est décrit dans le corps principal de la rubrique.](images/IoT4I_device_reg.svg "{{site.data.keyword.iotinsurance_short}} Device event registration flow")

### Configuration de l'interrogation du statut de terminal
{: #device_polling}
Le microservice de transformateur est chargé d'interroger et de recevoir les mises à jour de statut. Si l'API REST du fournisseur de terminaux prend en charge les mises à jour de terminal asynchrones, vous pouvez établir un abonnement qui permet au transformateur de recevoir les mises à jour de statut de terminal lorsqu'elles ont lieu. Sinon, vous pouvez configurer le transformateur pour qu'il interroge les mises à jour de statut de terminal.

Les appels de pseudo-fonction suivants sont utilisés pour définir le processus d'interrogation :

*Tableau 1 : Appels de pseudo-fonction*

Pseudo-fonction | Description
------------- | -------------
`getRegisteredUserDevices(userName)` | Extrait les terminaux utilisateur enregistrés disponibles qui utilisent le nom d'utilisateur.
`getProviderDevices(providerUserToken)` | Appelle l'API REST du fournisseur de terminaux pour obtenir le statut des terminaux utilisateur qui utilisent le jeton bearer utilisateur.
`findDevicesToAdd(), findDevicesToDel(), findDevicesToUpdate()` | Permet de retrouver les terminaux nouveaux, supprimés et modifiés en comparant les terminaux enregistrés avec ceux qui existent dans le fournisseur de terminaux.
` syncData()` | Permet de synchroniser les terminaux utilisateur en supprimant les anciens terminaux, en ajoutant de nouveaux terminaux et en mettant à jour les terminaux modifiés.  
 `notifyIoTP()` | Signale à {{site.data.keyword.iot_short_notm}} les modifications sous la forme d'événements MQTT.

Le transformateur publie les mises à jour de statut sur {{site.data.keyword.iot_short_notm}}, comme illustré dans l'exemple de code suivant :
```
// as specified in VCAP.services
var appClientConfig = {
  "org":iot_org,
  "id":iot_appid,
  "auth-key":iot_authkey,
  "auth-token":iot_authtoken
};

var appClient = new iotclient.IotfApplication(appClientConfig);
try {
  appClient.connect();
} catch (err) {
  console.log('IoT connect failed with error' +err);
}

...

// generate IoT event, note that the content is an arbitrary JSON object  
try {
  appClient.publishDeviceEvent("iOS",userToken.username, "status", "json", JSON.stringify(iotDevice));
} catch (err) {
  console.log('IoT publish failed with error' +err +'foruser' +userToken.username);
}

```

Le transformateur utilise {{site.data.keyword.cloudant}} pour accéder à des données utilisateur, telles que le jeton bearer, et pour stocker le dernier statut de terminal connu, afin de les comparer.  Les méthodes et fragments de code {{site.data.keyword.cloudant}} ci-dessous sont fournis à titre de référence.  

`getUserTokensByProvider` - Cette méthode permet d'obtenir tous les jetons utilisateur d'un fournisseur donné.

```
dbHelper.getUserTokensByProvider(provider, function (err,results) {
  if (!err) {
    console.log(results.token.length + " tokens retrieved for provider: " + Provider);
  } else {
    console.log("no tokens returned, err:",err);
  }
  });
```

`getDevicesByUser` - Cette méthode permet d'extraire tous les terminaux utilisateur enregistrés par nom d'utilisateur.
```
dbHelper.getDevicesByUser(username, function (err,results) {
  if (!err) {
    console.log(results.length + " devices retrieved for username: " + username);
  } else {
    console.log("no devices returned, err:",err);
  }
  });
```

`bulkUpdateDevices` - Cette méthode permet de mettre à jour ou d'ajouter un groupe de terminaux utilisateur.
```
dbHelper.bulkUpdateDevices(userDevices, function (err,results) {
  if (!err) {
    console.log(results.length + " devices updated");
    } else {
      console.log("no devices updated, err:",err);
    }
  });
```

`bulkDelDevices` - Cette méthode permet de supprimer un groupe de terminaux utilisateur.
```
dbhelper.bulkDelDevices(userDevices, function (err, results) {
  if (!err) {
    console.log(results.length + "devices deleted");
  } else {
    console.log("no devices deleted, err:",err);
  }
  });

```


## Déploiement d'une nouvelle instance de transformateur
{: #deploy_new_transformer}
Vous pouvez déployer une nouvelle instance de transformateur dans la même organisation et le même espace que votre instance d'{{site.data.keyword.iotinsurance_short}}.  

**Remarque :** Pour plus d'informations et obtenir de l'aide lors du déploiement d'une nouvelle instance de transformateur, voir [Contacter le service de support](../support/index.html#contacting-support).

Avant de commencer, téléchargez et installez l'interface de ligne de commande Cloud Foundry. Utilisez cette dernière pour modifier et déployer des instances de service sur {{site.data.keyword.iot_short_notm}}. Pour plus d'informations, voir [Téléchargement, modification et redéploiement de votre application Cloud Foundry à l'aide de l'interface de ligne de commande ![Icône de lien externe](../../icons/launch-glyph.svg)](https://www.ng.bluemix.net/docs/#starters/install_cli.html){:new_window}.

1. Dans l'interface de ligne de commande, passez dans le `répertoire contenant les sources et le fichier YML de descripteur de déploiement` en entrant la commande suivante :
```
$ cd directory_name
```
2. Répertoriez toutes les applications incluses dans {{site.data.keyword.iotinsurance_short}} et notez le nom du transformateur. Le nom se termine par `transformer`.

3. Arrêtez le transformateur {{site.data.keyword.iotinsurance_short}}. Exemple :
```
$ cf stop iot4i-dev-transformer
```
4. Répertoriez tous les services inclus dans {{site.data.keyword.iotinsurance_short}} et notez les noms des services {{site.data.keyword.iot_short_notm}} et {{site.data.keyword.cloudant}}.  Le nom du service {{site.data.keyword.iot_short_notm}} comprend les lettres `iotf`. Le nom du service {{site.data.keyword.cloudant}} comprend `cloudant`.

5. A l'aide des noms que vous avez notés lors des étapes précédentes, créez un fichier descripteur de déploiement semblable à celui illustré dans l'exemple suivant  
  ```
  applications:
  - path: .
    memory: 1024M
    instances: 1
    name: iot4i-dev-transformer
    no-route: false
    disk_quota: 1024M
    command: node index.js
    services:
    - iot4i-iotf-service
    - iot4i-cloudantNoSQLDB
    env:
       ENV: dev
       APIDOMAIN: iot4insurance-api-v.mybluemix.net
       NODE_MODULES_CACHE: false
  ```
6. Insérez votre transformateur dans {{site.data.keyword.Bluemix_notm}} à l'aide de la commande suivante, en remplaçant `newtransformer` par le nom de votre fichier descripteur de déploiement :
  ```
  $ cf push -f newtransformer.yml
  ```
7. Vous pouvez rechercher dans les journaux les messages de déploiement à l'aide de la commande suivante :
  ```
  $ cf logs iot4i-dev-transformer
  ```
