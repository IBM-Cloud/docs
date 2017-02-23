---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Intégrations de service externe
{: #ref-index}

L'intégration de service externe vous permet d'accéder à des données et des opérations à partir de services tiers ou externes au sein de votre organisation {{site.data.keyword.iot_full}}.

## Jasper
{: #jasper}

Jasper est une plateforme de gestion et d'administration des terminaux SIM. Elle est intégrée au tableau de bord {{site.data.keyword.iot_short_notm}}, ce qui permet d'administrer des terminaux Jasper via votre tableau de bord d'organisation {{site.data.keyword.iot_short_notm}}.

### Opérations prises en charge pour Jasper

L'intégration Jasper fournie par notre plateforme assure la prise en charge des opérations Jasper suivantes

- Affichage de l'ensemble des données Jasper
  - Affiche le statut, le plan tarifaire, l'utilisation mensuelle des données à ce jour, l'utilisation mensuelle des SMS à ce jour, l'utilisation mensuelle de la voix à ce jour, les limites de dépassement, les dates d'ajout et les dates de modification.
- Modification de l'état d'activation d'un terminal SIM
  - Sélectionnez : Inventory, Activation Ready, Activated, Deactivated et Retired.
- Affichage de l'utilisation du terminal SIM
  - Affiche la date de début du cycle, les données facturables et le total des données, les SMS facturables et le total des SMS, la voix facturable et le total pour la voix.
  - La date de début du cycle peut être définie au format AAAA-MM-JJ.
- Envoi d'un SMS à un terminal SIM
- Modification du plan tarifaire

Les opérations prises en charge sont accessibles dans le menu d'exploration d'un terminal connecté via Jasper, après l'exécution des étapes de configuration ci-dessous.

### API REST pour Jasper
Pour accéder à l'API REST pour Jasper, voir la section Jasper Extension dans la documentation [{{site.data.keyword.iot_short_notm}} HTTP REST API ![](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Jasper_Extension){: new_window}. 

### Configuration pour Jasper

Pour connecter votre terminal Jasper à votre organisation {{site.data.keyword.iot_short_notm}}, deux étapes de configuration doivent être exécutées au préalable. Vous devez connecter votre instance {{site.data.keyword.iot_short_notm}} à votre service Jasper, puis configurer les terminaux {{site.data.keyword.iot_short_notm}}.


1. Activez l'extension Jasper. Pour activer l'intégration de Jasper à votre organisation {{site.data.keyword.iot_short_notm}}, procédez comme suit :
  1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, sélectionnez **Extensions**.
  2. Sur la page **Extensions**, cliquez sur **Ajouter une extension**.
  3. Cliquez sur **Ajouter** en regard de Jasper.
  4. Entrez votre nom d'utilisateur, mot de passe, clé d'accès et ID de domaine Jasper.
  5. Cliquez sur **Terminé**.

2. Configurez vos terminaux
Vous pouvez configurer les terminaux connectés à votre organisation {{site.data.keyword.iot_short_notm}} et à votre compte Jasper afin d'afficher les données provenant de Jasper dans le tableau de bord {{site.data.keyword.iot_short_notm}}.  
**Important :** La configuration de Jasper ne peut pas être appliquée dans le cadre du processus d'ajout de terminal. Seuls les terminaux précédemment connectés peuvent être configurés avec Jasper.  
Pour configurer vos terminaux connectés via Jasper, procédez comme suit :
 1. Sur l'onglet Terminaux de votre tableau de bord {{site.data.keyword.iot_short_notm}}, localisez le terminal connecté via Jasper à configurer.
 2. Sélectionnez le terminal pour ouvrir la vue *Exploration du terminal*.
 3. Faites défiler l'écran jusqu'à *Configuration d'une extension*.
 4. Entrez la configuration d'extension au format JSON ci-dessous, puis cliquez sur **Confirmation des modifications** pour sauvegarder votre configuration.  

```json
    {
        "jasper": {
            "iccid": "string"
        }
    }

```

Une fois l'organisation correctement configurée, la section *Extensions* s'affiche sous la section *Configuration des extensions* dans la vue *Exploration du terminal*.

## AT&T
{: #att}

### Opérations prises en charge pour AT&T

L'extension AT&T permet d'effectuer les opérations AT&T suivantes

- Affichage de l'ensemble des données AT&T
  - Affiche le statut, le plan tarifaire, l'utilisation mensuelle des données à ce jour, l'utilisation mensuelle des SMS à ce jour, l'utilisation mensuelle de la voix à ce jour, les limites de dépassement, les dates d'ajout et les dates de modification.
- Modification de l'état d'activation d'un terminal SIM
  - Sélectionnez : Inventory, Activation Ready, Activated, Deactivated et Retired.
- Affichage de l'utilisation du terminal SIM
  - Affiche la date de début du cycle, les données facturables et le total des données, les SMS facturables et le total des SMS, la voix facturable et le total pour la voix.
  - La date de début du cycle peut être définie au format AAAA-MM-JJ.
- Envoi d'un SMS à un terminal SIM
- Modification du plan tarifaire

### API REST pour AT&T
Pour accéder à l'API REST pour AT&T, voir la section AT&T Extension dans la documentation [{{site.data.keyword.iot_short_notm}} HTTP REST API ![](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/AT&T_Extension){: new_window}. 

### Configuration pour AT&T

Pour connecter votre organisation {{site.data.keyword.iot_short_notm}} à &T, vous devez effectuer une configuration d'organisation et une configuration de terminal.

Pour configurer votre plateforme {{site.data.keyword.iot_short_notm}}, procédez comme suit :

1. Activez l'extension AT&T. Pour activer l'intégration d'AT&T à votre organisation {{site.data.keyword.iot_short_notm}}, procédez comme suit :
  1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, sélectionnez **Extensions**.
  2. Sur la page **Extensions**, cliquez sur **Ajouter une extension**.
  3. Cliquez sur **Ajouter** en regard de AT&T.
  4. Entrez votre nom d'utilisateur, mot de passe, clé d'accès et ID de domaine AT&T.
  5. Cliquez sur **Terminé**.

Pour connecter votre organisation {{site.data.keyword.iot_short_notm}} à votre compte AT&T, deux étapes de configuration doivent être exécutées au préalable. Exécutez la configuration de l'organisation, puis configurez vos terminaux.


2. Configurez vos terminaux
Vous pouvez configurer les terminaux connectés à votre organisation {{site.data.keyword.iot_short_notm}} et à votre compte AT&T afin d'afficher les données provenant d'AT&T dans le tableau de bord {{site.data.keyword.iot_short_notm}}.  
**Important :** La configuration d'AT&T ne peut pas être appliquée dans le cadre du processus d'ajout de terminal. Seuls les terminaux précédemment connectés peuvent être configurés avec AT&T.  
Pour configurer vos terminaux connectés via AT&T, procédez comme suit :
 1. Sur l'onglet Terminaux de votre tableau de bord {{site.data.keyword.iot_short_notm}}, localisez le terminal connecté via AT&T à configurer.
 2. Sélectionnez le terminal pour ouvrir la vue *Exploration du terminal*.
 3. Faites défiler l'écran jusqu'à *Configuration d'une extension*.
 4. Entrez la configuration d'extension au format JSON ci-dessous, puis cliquez sur **Confirmation des modifications** pour sauvegarder votre configuration.  

```json
    {
        "atnt": {
            "iccid": "string"
        }
    }

```

Une fois l'organisation correctement configurée, la section *Extensions* s'affiche sous la section *Configuration des extensions* dans la vue *Exploration du terminal*.

## ARM mbed Connector
{: #arm}

ARM mbed Connector vous permet de connecter votre terminal ARM mbed à votre {{site.data.keyword.iot_short_notm}}. L'extension ARM mbed permet au portail ARM mbed et à {{site.data.keyword.iot_short_notm}} d'envoyer et de recevoir des données depuis le portail ARM mbed.

### Configuration de l'installation


1. Activez l'extension ARM mbed Connector. Pour ce faire, procédez comme suit :
  1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, sélectionnez **Paramètres** et accédez à **Extensions**.
  2. Dans le menu **Extensions**, cliquez sur **Ajouter une extension**.
  3. Cliquez sur **Ajouter** en regard de l'extension ARM mbed Connector.
  4. Entrez votre clé d'accès et ID de domaine ARM mbed. Ces informations se trouvent sur le portail ARM mbed (https://connector.mbed.com).
  5. Vérifiez que les données d'identification sont correctes en cliquant sur le bouton **Vérifier la connexion**.
  6. Cliquez sur **Terminé**.

### Format de contenu

Il existe deux types de messages entrants à partir de la plateforme ARM mbed, des notifications et des réponses asynchrones. {{site.data.keyword.iot_short_notm}} peut envoyer des commandes à des terminaux qui sont connectés à la plateforme ARM mbed.

#### Notifications

Des notifications sont générées par les modifications apportées aux données de terminal ou de capteur. Après le traitement du message par{{site.data.keyword.iot_short_notm}}, le message est envoyé à la rubrique d'événement de terminal comme le ferait un terminal connecté directement à {{site.data.keyword.iot_short_notm}}. Le type d'événement utilisé pour les notifications émises par les terminaux connectés à la plateforme ARM mbed est `notify`.

L'exemple de code suivant illustre le format de contenu d'une notification envoyée par l'API de plateforme ARM mbed :

```
{
  "ep":<endpoint/deviceID>,
  "path":<resource path>,
  "ct":<content type>,
  "payload":<Base64 encoded payload>,
  "max-age":<how long the payload is valid, in seconds>
}
```

#### Réponses asynchrones

Lorsque {{site.data.keyword.iot_short_notm}} envoie une commande à un terminal connecté à la plateforme ARM mbed, le terminal renvoie un message de confirmation à {{site.data.keyword.iot_short_notm}}. Ce message de confirmation est appelé *réponse asynchrone* et utilise le type d'événement `asyncResponse`.

L'exemple de code suivant illustre le format de contenu d'une réponse asynchrone envoyée par le service cloud ARM mbed :

```
{
  "id":<transaction id>,
  "status":<200 is command was sucessfully executed. Check other HTTP response codes>,
  "ct":<content type>,
  "max-age":<how long the payload is valid, in seconds>,
  "payload":<base64 encoded payload>,
  "ep":<endpoint/deviceID affected by the command>,
  "path":<resource path affected by the command>
}
```

#### Envoi de commandes à la plateforme ARM mbed

{{site.data.keyword.iot_short_notm}} peut envoyer des commandes à des terminaux connectés à la plateforme ARM mbed. Les commandes envoyées à la plateforme ARM mbed doivent utiliser le format JSON suivant :

```
{
  "method":<PUT or POST>,
  "deviceId":<endpoint/deviceId>,
  "resourceId":<resource path>,
  "payload": <Base64 encoded payload>
}
```
La méthode choisie est sensible à la casse. Le début '/' du chemin d'accès à la ressource doit être ignorée.


Le contenu doit être publié dans la rubrique suivante :

```
iot-2/type/<device_type>/id/<deviceId>/cmd/<command_type>/fmt/<command_format>
```


## Orange
{: #orange}

L'extension Orange vous permet d'afficher des données de carte SIM à partir de terminaux qui sont connectés à votre instance {{site.data.keyword.iot_short_notm}} et sur lesquels une carte SIM Orange est installée.

https://developer.ibm.com/iotplatform/2016/03/30/watson-iot-platform-integration-with-orange-beta/

### Opérations prises en charge pour Orange

Si vous disposez d'un terminal connecté à votre service {{site.data.keyword.iot_short_notm}} et dotée d'une carte SIM Orange, vous pouvez utiliser l'extension Orange pour afficher les données de carte SIM suivantes :

- Numéro de série SIM
- statut d'activation
- Dernier changement de statut
- Dernière actualisation de statut
- Statut d'emplacement

### API REST pour Orange
Pour accéder à l'API REST pour Orange, voir la section Orange Extension dans la documentation[{{site.data.keyword.iot_short_notm}} HTTP REST API ![](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Orange_Extension){: new_window}. 

### Configuration pour Orange

Pour activer l'extension Orange :

1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, sélectionnez **Extensions**.
2. Sur la page **Extensions**, cliquez sur **Ajouter une extension**.
3. Cliquez sur **Ajouter** en regard de l'extension Orange.
4. Entrez votre nom d'utilisateur et votre mot de passe Orange.
6. Cliquez sur **Terminé**.

Une fois l'extension Orange activée, chaque terminal doté d'une carte SIM Orange doit être configurée pour afficher des données SIM Orange.

1. Sur l'onglet Terminaux de votre tableau de bord {{site.data.keyword.iot_short_notm}}, localisez le terminal SIM Orange à configurer.
2. Sélectionnez le terminal, puis faites défiler l'écran jusqu'à *Configuration d'une extension*.
3. Entrez la configuration d'extension au format JSON ci-dessous, puis cliquez sur **Confirmation des modifications** pour sauvegarder votre configuration.

```  
    {
        "orange": {
            "serialnumber": "<serial number of Orange SIM>"
        }
    }

```
Une fois l'organisation correctement configurée, la section *Extensions* s'affiche sous la section *Configuration des extensions* dans la vue *Exploration du terminal*.

## Stockage des données d'historique
{: #historical_data}

L'extension de stockage de données historiques vous permet de localiser et configurer des services de stockage de message compatibles, par exemple, [{{site.data.keyword.cloudantfull}}](../../cloudant_connector.html) ou [{{site.data.keyword.messagehub_full}}](../../message_hub.html) pour vos données IoT.

## Packages de gestion des terminaux personnalisés
{: #device_mgmt}

La gestion des terminaux est une fonction principale du service {{site.data.keyword.iot_short_notm}} ; elle peut toutefois être étendue pour développer des fonctions supplémentaires. Les packages de gestion des terminaux personnalisés doivent être composés d'un document JSON valide et définir au moins une action de gestion des terminaux personnalisée. 

Pour plus d'informations sur les fonctions de gestion des terminaux personnalisées, y compris un exemple du format JSON requis, voir [Extensions personnalisées de gestion des terminaux](../../devices/device_mgmt/custom_actions.html){: new_window}.

### Ajout d'un package de gestion des terminaux personnalisé 

Vous pouvez ajouter un package de gestion des terminaux personnalisé à l'aide du tableau de nord {{site.data.keyword.iot_short_notm}} ou de l'API. 

Pour ajouter un package de gestion des terminaux personnalisé à l'aide du tableau de bord {{site.data.keyword.iot_short_notm}} :

1. Depuis votre tableau de bord {{site.data.keyword.iot_short_notm}}, cliquez sur **Paramètres** dans la barre de navigation. 
2. Cliquez sur **Packages de gestion des terminaux personnalisés**.
3. Cliquez sur le bouton **Ajouter un package**. 
4. Sélectionnez votre fichier de package et cliquez sur **Ouvrir**.

Pour ajouter un package de gestion des terminaux personnalisé à l'aide de l'API, voir la [documentation de l'API {{site.data.keyword.iot_short_notm}} ![](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.

## Chaîne de blocs
{: #blockchain}

{{site.data.keyword.iot_short_notm}} avec chaîne de blocs permet aux terminaux IoT de fournir des données aux transactions de chaîne de blocs, ainsi, les données sont stockées dans le grand livre non modifiable de chaîne de blocs et sont utilisées dans des règles métier de contrat intelligent. {{site.data.keyword.iot_short_notm}} mappe les données de terminal au format de données qui est requis par le contrat intelligent de la chaîne de blocs et les transmet à une matrice de chaîne de blocs pour stockage dans le grand livre de chaîne de blocs.

### Opérations prises en charge pour la chaîne de blocs
- Déclenchement des mises à jour de contrat intelligent avec des événements de terminal.
- Exécution d'une logique métier de contrat intelligent pour mettre à jour un état de grand livre avec des données d'événement de terminal.
- Surveillance de l'état de chaîne de blocs, de transactions et de grand livre à l'aide de l'interface utilisateur de surveillance.

### Configuration pour la chaîne de blocs

L'intégration de chaîne de blocs à {{site.data.keyword.iot_short_notm}} est une offre de services qui n'est pas activée par défaut dans {{site.data.keyword.iot_short_notm}}. Pour activer la fonction dans votre organisation, procédez comme suit :
 1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, sélectionnez **Extensions**.
 2. Sur la page **Extensions**, cliquez sur **Ajouter une extension**.
 3. Cliquez sur **Ajouter** en regard de l'extension Blockchain.
 4. Dans le titre Blockchain, cliquez sur **Configuration**.
 3. Dans la section **Activer Blockchain**, cliquez sur le lien **En savoir plus** pour accéder à la page [IoT Blockchain Services Offering ![](../../../../icons/launch-glyph.svg)](http://www.ibm.com/internet-of-things/iot-news/announcements/private-blockchain/){: new_window}.
 4. Cliquez sur **Démarrez votre projet de chaîne de blocs** pour renseigner et soumettre le formulaire *Explorez le potentiel d'IoT et de Blockchain*.   
 5. Lorsque votre demande est approuvée, IBM vous contacte pour activer l'intégration de chaîne de blocs à votre organisation. 
 6. Revenez au tableau de bord {{site.data.keyword.iot_short_notm}} pour que votre organisation puisse terminer la configuration en suivant les étapes décrites dans [Intégration de chaîne de blocs {{site.data.keyword.iot_short_notm}}](../../bl_blockchain_integration.html).



## The Weather Company
{: #weathercompany}

L'extension The Weather Company associe des données météorologiques à vos terminaux {{site.data.keyword.iot_short_notm}} existants. Les données météorologiques de The Weather Company apparaissent dans la vue de détails du terminal si une demande de mise à jour d'emplacement a été émise par l'API ou si le terminal a déjà défini son emplacement à l'aide d'un message de gestion de terminaux.

**Remarque :** Seuls les terminaux gérés peuvent définir leurs propres emplacements. Les emplacements de tous les terminaux non gérés doivent être définis manuellement à l'aide de l'API. Pour plus d'informations sur la définition d'un emplacement de terminal, voir [Demandes de mise à jour d'emplacement](../../devices/device_mgmt/index.html#update-location).

### API REST pour The Weather Company
Pour accéder à l'API REST pour The Weather Company, voir la section
Device Location Weather dans la documentation [{{site.data.keyword.iot_short_notm}} HTTP REST API ![](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window}. 

### Données météorologiques

Pour afficher les données météorologiques extraites pour un emplacement de terminal, localisez le terminal dans le panneau **Devices** et cliquez dessus. Dans la vue de détails du terminal, faites défiler l'écran jusqu'à la section **Extensions**. Les données météorologiques suivantes sont répertoriées :

- Météo en cours.
- Température en cours.
- Températures maximale et minimale prévues.
- Humidité relative.
- Pression.
- Visibilité.
- Vitesse du vent.
- Direction du vent.
- Latitude.
- Longitude.

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->
