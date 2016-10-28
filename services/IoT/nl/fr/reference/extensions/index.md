---

copyright :
  années : 2015, 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Intégrations de service externe
{: #ref-index}
Dernière mise à jour : 13 septembre 2016
{: .last-updated}

L'intégration de service externe vous permet d'accéder à des données et des opérations à partir de services tiers ou externes au sein de votre organisation {{site.date.keyword.iot_full}}. 

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



### Configuration pour Jasper

Pour connecter votre terminal Jasper à votre organisation {{site.data.keyword.iot_short_notm}}, deux étapes de configuration doivent être exécutées au préalable. Vous devez connecter votre instance {{site.data.keyword.iot_short_notm}} à votre service Jasper, puis configurer les terminaux {{site.data.keyword.iot_short_notm}}. 


1. Activez l'extension Jasper. Pour activer l'intégration de Jasper à votre organisation {{site.data.keyword.iot_short_notm}}, procédez comme suit :
  1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, sélectionnez **Extensions**.
  2. Sur la page **Extensions**, cliquez sur **Ajouter une extension**.
  3. Cliquez sur **Ajouter** en regard de AT&T.
  4. Entrez votre nom d'utilisateur, mot de passe, clé d'accès et ID de domaine AT&T.
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
Vous pouvez configurer les terminaux connectés à votre organisation {{site.data.keyword.iot_short_notm}}  et à votre compte AT&T afin d'afficher les données provenant d'AT&T dans le tableau de bord {{site.data.keyword.iot_short_notm}}.
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

<!--
## ARM mbed connector
{: #arm}

The ARM mbed connector is an extension that allows you to connect your ARM mbed device to your {{site.data.keyword.iot_short_notm}}. The ARM mbed extension is allows the ARM mbed portal and the {{site.data.keyword.iot_short_notm}} to send and receive data from the ARM mbed portal.

### Setup Configuration


1. Enable the ARM mbed connector extension. To enable the ARM mbed connector extension complete the following steps:
  1. From the {{site.data.keyword.iot_short_notm}} dashboard, select **Settings** and navigate to **Extensions**.
  2. In the **Extensions** menu, click **Add Extension**.
  3. Click **Add** next to ARM mbed connector extension.
  4. Enter your ARM mbed access key and domain ID. You can find these by using the ARM mbed portal at https://connector.mbed.com.
  5. Check the credentials are correct by clicking the **Check Connection** button.
  6. Click **Done**.

### Payload Format

There are two types of incoming messages from the ARM mbed platform, notifications and asynchronous responses. The {{site.data.keyword.iot_short_notm}} can send commands to devices that are connected to the ARM mbed platform.

#### Notifications

Notifications are generated by changes in device or sensor data. After the {{site.data.keyword.iot_short_notm}} processes the message, it is to the device event topic in the same way as a device connected directly to the {{site.data.keyword.iot_short_notm}}. The event type used for notifications originating on devices connected to the ARM mbed platform is `notify`.

The following code sample shows the payload format for a notification sent by the ARM mbed platform API:

```
{
  "ep":<endpoint/deviceID>,
  "path":<resource path>,
  "ct":<content type>,
  "payload":<Base64 encoded payload>,
  "max-age":<how long the payload is valid, in seconds>
}
```

#### Asynchronous responses

When the {{site.data.keyword.iot_short_notm}} sends a command to a device connected to the ARM mbed platform, the device sends a confirmation message back to the {{site.data.keyword.iot_short_notm}}. This confirmation message is called an _asynchronous response_ and uses the event type `asyncResponse`.

The following code sample shows the payload format for an asynchronous response sent by the ARM mbed cloud service:

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

#### Sending commands to the ARM mbed platform

The {{site.data.keyword.iot_short_notm}} can send commands to devices connected to the ARM mbed platform. Commands sent to the ARM mbed platform it must use the following JSON format.

```
{
  "method":<PUT or POST>,
  "deviceId":<endpoint/deviceId>,
  "resourceId":<resource path>,
  "payload": <Base64 encoded payload>
}
```

The payload should be published to the following topic:

```
iot-2/type/<device_type>/id/<deviceId>/cmd/<command_type>/fmt/<command_format>
```
-->

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


## Extensions Gestion des terminaux
{: #device_mgmt}

La gestion des terminaux est une fonction principale du service {{site.data.keyword.iot_short_notm}} ; elle peut toutefois être étendue pour développer des fonctions supplémentaires. 

L'extension Gestion des terminaux vous permet d'installer des fonctions personnalisées pour la gestion des terminaux. Pour plus d'informations sur les fonctions de gestion des terminaux personnalisées, voir [Extensions personnalisées de gestion des terminaux](../../devices/device_mgmt/custom_actions.html){: new_window}.

## Chaîne de blocs
{: #blockchain}

{{site.data.keyword.iot_short_notm}} avec chaîne de blocs permet aux terminaux IoT de fournir des données aux transactions de chaîne de blocs, ainsi, les données sont stockées dans le grand livre non modifiable de chaîne de blocs et sont utilisées dans des règles métier de contrat intelligent. {{site.data.keyword.iot_short_notm}} mappe les données de terminal au format de données qui est requis par le contrat intelligent de la chaîne de blocs et les transmet à une matrice de chaîne de blocs pour stockage dans le grand livre de chaîne de blocs. 

### Opérations prises en charge pour la chaîne de blocs
- Déclenchement des mises à jour de contrat intelligent avec des événements de terminal. 
- Exécution d'une logique métier de contrat intelligent pour mettre à jour un état de grand livre avec des données d'événement de terminal. 
- Surveillance de l'état de chaîne de blocs, de transactions et de grand livre à l'aide de l'interface utilisateur de surveillance. 

### Configuration pour la chaîne de blocs

L'intégration de chaîne de blocs à {{site.data.keyword.iot_short_notm}} est une offre de services qui n'est pas activée par défaut dans {{site.data.keyword.iot_short_notm}}. Pour activer la fonction dans votre environnement, procédez comme suit : 
 1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, sélectionnez **Paramètres** et accédez à **Extensions**.
 2. Cliquez sur le lien **Informations complémentaires** en regard de l'extension de chaîne de blocs pour accéder à la page des offres de services IoT Blockchain. 
 3. Remplissez et soumettez le formulaire de demande de service.
L'approbation du service prend généralement une journée. Une fois votre demande approuvée, vous recevez un courrier électronique contenant les instructions permettant d'activer l'intégration de chaîne de blocs dans votre organisation {{site.data.keyword.iot_short_notm}}. 
 5. Revenez au tableau de bord {{site.data.keyword.iot_short_notm}} pour que votre organisation puisse terminer la configuration. Pour plus d'informations, voir [Intégration de chaîne de blocs {{site.data.keyword.iot_short_notm}}](../../bl_blockchain_integration.html).
