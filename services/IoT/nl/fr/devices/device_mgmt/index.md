---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Protocole de gestion des terminaux
{: #index}

## Introduction
{: #introduction}

{{site.data.keyword.iot_full}} reconnaît deux classes de terminal : les **terminaux gérés** et les **terminaux non gérés**.

Les **terminaux gérés** sont définis comme des terminaux qui contiennent un agent de gestion des terminaux. Un agent de gestion des terminaux est un bloc de logique qui permet au terminal d'interagir avec le service de gestion des terminaux de {{site.data.keyword.iot_short_notm}} via le protocole de gestion des terminaux. Les terminaux gérés peuvent effectuer des opérations de gestion des terminaux, y compris des mises à jour d'emplacement, des mises à jour et des téléchargements de microprogramme, des redémarrages et des réinitialisations avec les paramètres d'usine.

Le protocole de gestion des terminaux définit un ensemble d'opérations prises en charge. Un agent de gestion des terminaux peut prendre en charge un sous-ensemble des opérations, mais les opérations **manage** et **unmanage** doivent être prises en charge. Un terminal qui prend en charge des opérations d'action sur le microprogramme doit également prendre en charge l'observation.

Le protocole de gestion des terminaux est construit par dessus le protocole de messagerie MQTT. Pour plus d'informations sur l'interaction entre le protocole de gestion des terminaux et MQTT, voir [Connectivité MQTT pour les terminaux](../mqtt.html).


### Cycle de vie de gestion des terminaux

1. Un terminal et le type de terminal qui lui est associé sont créés dans {{site.data.keyword.iot_short_notm}} à l'aide du tableau de bord ou de l'API REST.
2. Un terminal se connecte à {{site.data.keyword.iot_short_notm}} et utilise l'opération **managed devices** pour devenir un terminal géré.
3. Vous pouvez consulter et manipuler les métadonnées pour un terminal à l'aide des opérations sur les terminaux. Ces opérations, par exemple, la mise à jour de microprogramme et le redémarrage de terminal, sont décrites dans la documentation sur le modèle de terminal. Pour plus d'informations sur le modèle de terminal, voir [Modèle de terminal](https://console.ng.bluemix.net/docs/services/IoT/reference/device_model.html).
4. Un terminal peut communiquer des mises à jour sur son emplacement, des informations de diagnostic et des codes d'erreurs à l'aide du protocole de gestion des terminaux.
5. Pour traiter les terminaux défectueux parmi un nombre important de terminaux, la demande d'opération sur les **terminaux gérés** inclut un paramètre de durée de vie facultatif. Ce paramètre correspond au nombre de secondes durant lesquelles le terminal doit effectuer une autre demande sur les **terminaux gérés** pour éviter d'être classé comme étant en veille et devenir un terminal non géré.
6. Lorsqu'un terminal est déclassé, vous pouvez le retirer de {{site.data.keyword.iot_short_notm}} à l'aide du tableau de bord ou de l'API REST.

Voir la recette [Connect Raspberry Pi as Managed Device to IBM Watson IoT Platform ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/){: new_window}.

### Récapitulatif des codes retour


Le tableau suivant répertorie les codes retour qui sont générés aux cours des différentes étapes du cycle de vie de la gestion des terminaux.

|Code retour |Message |
|:---|:---|
|200   |Réussite de l'opération|
|202   |Accepté (pour le lancement de commandes)|
|204   |Modifié (pour les mises à jour d'attributs)|
|400   |Demande erronée (par exemple, si un terminal ne se trouve pas à l'état approprié pour cette commande)|
|404   |Attribut introuvable (également utilisé si l'opération a été publiée dans un sujet non valide)|
|409   |La ressource n'a pas pu être mise à jour en raison d'un conflit (par exemple, lorsque la ressource est mise à jour par deux demandes simultanées, la tentative de mise à jour peut être effectuée ultérieurement)|
|500   |Erreur inattendue du terminal|
|501   |Opération non mise en oeuvre|


## Demandes Gérer le terminal
{: #manage_device_request}

Un terminal utilise la demande Gérer le terminal pour devenir un terminal géré. La demande Gérer le terminal doit être la première demande de gestion des terminaux envoyée par le terminal après la connexion à {{site.data.keyword.iot_short_notm}}. Un agent de gestion des terminaux envoie généralement ce type de demande chaque fois qu'il démarre ou redémarrer.

**Important :** La prise en charge de cette opération est obligatoire pour tous les terminaux gérés.


### Sujet pour une demande Gérer le terminal

Un terminal publie une demande Gérer le terminal sur le sujet suivant :

```
iotdevice-1/mgmt/manage
```

Le serveur répond à une demande Gérer le terminal sur le sujet suivant :

```
iotdm-1/response
```




### Format de message pour une demande Gérer le terminal


Dans une demande Gérer le terminal, la zone `d` et tous ses sous-ensembles sont facultatifs. Les valeurs de zone `metadata` et `deviceInfo` remplacent les attributs correspondants pour le terminal émetteur, s'ils sont envoyés.

La zone `lifetime` facultative spécifie le nombre de secondes durant lesquelles le terminal doit envoyer une autre demande Gérer le terminal afin d'éviter d'être classé comme en veille et devenir un terminal non géré. Si la zone `lifetime` est omise ou définie avec la valeur `0`, le terminal géré n'est pas classé comme en veille. La valeur minimale prise en charge pour la zone `lifetime` est `3600` secondes, autrement dit, 1 heure.

Les zones facultatives `supports.deviceActions` et `supports.firmwareActions` indiquent les fonctions de l'agent de gestion des terminaux. Si `supports.deviceActions` est défini, l'agent prend en charge les actions de redémarrage et de réinitialisation avec les paramètres d'usine. Pour un terminal qui ne fait pas la distinction entre un redémarrage et une réinitialisation avec les paramètres d'usine, il est acceptable d'utiliser le même comportement pour les deux actions. Si `supports.firmwareActions` est défini, l'agent prend en charge les actions de téléchargement de microprogramme et de mise à jour de microprogramme.

L'exemple suivant illustre le format de demande :

```
Message sortant depuis le terminal :

Topic: iotdevice-1/mgmt/manage
{
    "d": {
        "metadata":{},
        "lifetime": number,
        "supports": {
            "deviceActions": boolean,
            "firmwareActions": boolean
        },
        "deviceInfo": {
            "serialNumber": "string",
            "manufacturer": "string",
            "model": "string",
            "deviceClass": "string",
            "description" :"string",
            "fwVersion": "string",
            "hwVersion": "string",
            "descriptiveLocation": "string"
        }
    },
    "reqId": "string"
}
```

L'exemple suivant illustre le format de réponse :

```
Message entrant depuis le serveur :

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```


### Codes de réponse pour une demande Gérer le terminal

|Code de réponse |Message |
|:---|:---|
|200   |L'opération a abouti.|
|400   |Le message d'entrée ne correspond pas au format attendu ou l'une des valeurs n'est pas comprise dans la plage valide.|
|404   |Le nom de sujet est incorrect ou le terminal n'est pas dans la base de données.|
|409   |Un conflit s'est produit au cours de la mise à jour de la base de données de terminaux. Pour résoudre ce conflit, simplifiez l'opération si nécessaire.|


## Demandes d'annulation de la gestion des terminaux
{: #manage-unmanage}


Un terminal utilise une demande Annuler la gestion du terminal lorsqu'il n'a plus besoin d'être géré. Lorsqu'un terminal devient non géré, {{site.data.keyword.iot_short_notm}} n'envoie plus de nouvelles demandes de gestion des terminaux au terminal. Les terminaux non gérés continuent de publier des codes d'erreur, des messages de journal et des messages d'emplacement.
**Important :** La prise en charge de cette opération est obligatoire pour tous les terminaux gérés.

### Sujet pour une demande Annuler la gestion du terminal


Un terminal publie une demande Annuler la gestion du terminal sur le sujet suivant :

```
iotdevice-1/mgmt/unmanage
```

Le serveur répond à une demande Annuler la gestion du terminal sur le sujet suivant :

```
iotdm-1/response
```

### Format de message pour une demande Annuler la gestion du terminal

Format de demande :

```
Message sortant depuis le terminal :

Topic: iotdevice-1/mgmt/unmanage
{
    "reqId": "string"
}
```

Format de réponse :

```
Message entrant depuis le serveur :

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Codes de réponse pour une demande Annuler la gestion du terminal

|Code de réponse |Message |
|:---|:---|
|200   |L'opération a abouti.|
|400   |Le message d'entrée ne correspond pas au format attendu ou l'une des valeurs n'est pas comprise dans la plage valide.|
|404   |Le nom de sujet est incorrect ou le terminal n'est pas dans la base de données.|
|409   |Un conflit s'est produit au cours de la mise à jour de la base de données de terminaux. Pour résoudre ce conflit, simplifiez l'opération si nécessaire.|


## Demandes Mettre à jour l'emplacement
{: #update-location}

Un terminal utilise une demande Mettre à jour l'emplacement pour gérer les données d'emplacement d'un terminal. Les métadonnées d'emplacement d'un terminal peuvent être mises à jour dans {{site.data.keyword.iot_short_notm}} en procédant comme suit :

### Mises à jour d'emplacement de terminal automatiques
- Le terminal informe {{site.data.keyword.iot_short_notm}} de la mise à jour de l'emplacement. Le terminal extrait cet emplacement à partir d'un récepteur GPS et envoie un message de gestion des terminaux à l'instance {{site.data.keyword.iot_short_notm}} pour mettre à jour son emplacement. L'horodatage capture l'heure à laquelle l'emplacement a été extrait du récepteur GPS. L'horodatage est valide même si le message de mise à jour d'emplacement est envoyé avec du retard. Si l'horodatage est omis dans le message de gestion des terminaux, la date et l'heure de la réception du message sont utilisées pour mettre à jour les métadonnées d'emplacement.

### Mises à jour d'emplacement de terminal manuelles à l'aide de l'API REST
- Vous pouvez définir manuellement les métadonnées d'emplacement pour un terminal statique à l'aide de l'API REST {{site.data.keyword.iot_short_notm}} lorsque le terminal est enregistré. Vous pouvez également modifier l'emplacement ultérieurement. Le paramètre d'horodatage est facultatif, mais, s'il n'est pas spécifié, la date du jour et l'heure en cours sont utilisées dans les métadonnées d'emplacement du terminal.

### Mises à jour d'emplacement déclenchées par des terminaux

Les terminaux qui peuvent déterminer leur emplacement peuvent choisir d'informer le serveur de gestion des terminaux {{site.data.keyword.iot_short_notm}} de toute modification de leur emplacement.

### Sujet pour une demande Mettre à jour l'emplacement déclenchée par un terminal :


Un terminal publie une demande Mettre à jour l'emplacement sur le sujet suivant :

```
iotdevice-1/device/update/location
```

Le serveur répond à une demande Mettre à jour l'emplacement sur le sujet suivant :

```
iotdm-1/response
```

### Mise à jour d'emplacement déclenchée par des utilisateurs ou des applications


Lorsqu'un utilisateur ou une application met à jour l'emplacement d'un terminal géré actif, celui-ci extrait un message de mise à jour.




### Sujet pour une demande Mettre à jour l'emplacement déclenchée par des utilisateurs ou des applications


Le serveur publie une demande Mettre à jour l'emplacement sur le sujet suivant :

```
iotdm-1/device/update
```

### Format de message pour une demande Mettre à jour l'emplacement


La zone `measuredDateTime` contient la date à laquelle l'emplacement a été mesuré. La zone `updatedDateTime` contient la date à laquelle les informations de terminal ont été mises à jour. Pour des raisons d'efficacité, {{site.data.keyword.iot_short_notm}} effectue parfois des mises à jour par lots des informations d'emplacement, de sorte que les mises à jour soient légèrement retardées. La latitude et la longitude doivent être spécifiés en degrés décimaux à l'aide de World Geodetic System 1984 (WGS84).

Chaque fois qu'un emplacement est mis à jour, les valeurs fournies pour latitude, longitude, elevation et uncertainty sont considérées comme une seule mise à jour de valeurs multiples. Les valeurs définies pour latitude et longitude sont obligatoires et doivent être indiquées pour chaque mise à jour.  Les valeurs définies pour elevation et uncertainty sont facultatives et peuvent être omises.

Si une valeur facultative est indiquée pour une mise à jour, puis omise lors d'une mise à jour ultérieure, la valeur précédente est supprimée par la mise à jour plus récente. Chaque mise à jour est considérée comme un ensemble complet à valeurs multiples.

### Mises à jour d'emplacement déclenchées par un terminal


Format de demande :

```
Message sortant depuis le terminal :

Topic: iotdevice-1/device/update/location
{
    "d": {
        "longitude": number,
        "latitude": number,

        "elevation": number,
        "measuredDateTime": "string in ISO8601 format",
        "updatedDateTime": "string in ISO8601 format",
        "accuracy": number
    },
    "reqId": "string"
}
```

Format de réponse :

```
Message entrant depuis le serveur :

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Codes de réponse pour une demande Mettre à jour l'emplacement

|Code de réponse |Message |
|:---|:---|
|200   |L'opération a abouti.|
|400   |Le message d'entrée ne correspond pas au format attendu ou l'une des valeurs n'est pas comprise dans la plage valide.|
|404   |Le nom de sujet est incorrect ou le terminal n'est pas dans la base de données.|
|409   |Un conflit s'est produit au cours de la mise à jour de la base de données de terminaux. Pour résoudre ce conflit, simplifiez l'opération si nécessaire.|


### Mises à jour d'emplacement déclenchées par des utilisateurs ou des applications


L'exemple suivant illustre le format de contenu :

```
Message entrant depuis le serveur :

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
            {
                "field": "location",
                "value": {
                    "latitude": number,
                    "longitude": number,
                    "elevation": number,
                    "accuracy": number,
                    "measuredDateTime": "string in ISO8601 format"
                }
            }
        ]
    }
}
```

**Remarque :** Le paramètre `reqID` n'est pas utilisé, car le terminal n'est pas tenu de répondre.

## Demandes Mettre à jour les attributs du terminal
{: #update-attributes}

En utilisant l'API REST, {{site.data.keyword.iot_short_notm}} peut envoyer une demande à un terminal afin de mettre à jour la valeur d'un ou de plusieurs des attributs de terminal suivants :


|Attribut | Informations complémentaires|
|:---|:---|
|location  | Voir [Mise à jour d'emplacement](index.html#update-location)|
|metadata  | Facultatif|
|deviceInfo | Facultatif|
|mgmt.firmware | Voir [Processus de mise à jour de microprogramme](requests.html#firmware-actions-update)|

### Sujet pour une demande Mettre à jour les attributs du terminal


Le serveur publie la demande Mettre à jour les attributs du terminal sur le sujet suivant :

```
iotdm-1/device/update
```


### Format de message pour une demande Mettre à jour les attributs du terminal


L'exemple suivant illustre le format de contenu pour la demande :

```
Message entrant depuis le serveur :

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
            {
                "field": "location",
                "value": ""
            }
        ]
    }
}
```


## Demandes Ajout un code d'erreur
{: #diag-add-error-code}

Les terminaux peuvent choisir d'informer le serveur de gestion des terminaux {{site.data.keyword.iot_short_notm}} de toute modification apportée à leur statut d'erreur en utilisant une demande Ajouter un code d'erreur.

### Sujet pour une demande Ajouter un code d'erreur


Un terminal publie une demande Ajouter un code d'erreur sur le sujet suivant :

```
iotdevice-1/add/diag/errorCodes
```

### Format de message pour une demande Ajouter un code d'erreur


La valeur associée à `errorCode` correspond au code d'erreur de terminal actuel ; elle doit être ajoutée à {{site.data.keyword.iot_short_notm}}.

Format de demande :

```
Message sortant depuis le terminal :

Topic: iotdevice-1/add/diag/errorCodes
{
    "d": {
        "errorCode": number
    },
    "reqId": "string"
}
```

Format de réponse :

```
Message entrant depuis le serveur :

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Codes de réponse pour une demande Ajouter un code d'erreur

|Code de réponse |Message |
|:---|:---|
|200   |L'opération a abouti.|
|400   |Le message d'entrée ne correspond pas au format attendu ou l'une des valeurs n'est pas comprise dans la plage valide.|
|404   |Le nom de sujet est incorrect ou le terminal n'est pas dans la base de données.|
|409   |Un conflit s'est produit au cours de la mise à jour de la base de données de terminaux. Pour résoudre ce conflit, simplifiez l'opération si nécessaire.|


## Demandes Effacer des codes d'erreur
{: #diag-clear-error-codes}

Les terminaux peuvent demander à {{site.data.keyword.iot_short_notm}} d'effacer tous les codes d'erreur pour le terminal en utilisant une demande Effacer des codes d'erreur.

### Sujet pour une demande Effacer des codes d'erreur


Un terminal publie cette demande sur le sujet suivant :

```
iotdevice-1/clear/diag/errorCodes
```

### Format de message pour une demande Effacer des codes d'erreur


Format de demande :

```
Message sortant depuis le terminal :

Topic: iotdevice-1/clear/diag/errorCodes
{
    "reqId": "string"
}
```

Format de réponse :

```
Message entrant depuis le serveur :

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Codes de réponse pour une demande Effacer des codes d'erreur

|Code de réponse |Message |
|:---|:---|
|200   |L'opération a abouti.|
|400   |Le message d'entrée ne correspond pas au format attendu ou l'une des valeurs n'est pas comprise dans la plage valide.|
|404   |Le nom de sujet est incorrect ou le terminal n'est pas dans la base de données.|
|409   |Un conflit s'est produit au cours de la mise à jour de la base de données de terminaux. Pour résoudre ce conflit, simplifiez l'opération si nécessaire.|


## Demandes Ajouter un journal
{: #diag-add-log}

Les terminaux peuvent choisir d'informer le support de gestion des terminaux {{site.data.keyword.iot_short_notm}} que des modifications ont été apportées en ajoutant une nouvelle entrée de journal. Les entrées de journal incluent un message de journal, un horodatage, un niveau de gravité et des données de diagnostic binaires codées en base 64.

### Sujet pour une demande Ajouter un journal
Un terminal publie cette demande sur le sujet suivant :

```
iotdevice-1/add/diag/log
```


### Format de message pour une demande Ajouter un journal

Le tableau suivant décrit le format des attributs de message sortant :

|Attribut |Description |
|:---|:---|
|`message`|Spécifie un message de diagnostic qui doit être ajouté à {{site.data.keyword.iot_short_notm}}|
|`timestamp`|Spécifie la date et l'heure de l'entrée de journal au format ISO8601 |
|`data`|Spécifie des données de diagnostic facultatives codées en base 64|
|`severity`|Spécifie le niveau de gravité du message (0 : informations, 1 : avertissement, 2 : erreur)|


Format de demande :

```
Message sortant depuis le terminal :

Topic: iotdevice-1/add/diag/log
{
    "d": {
        "message": string,
        "timestamp": string,
        "data": string,
        "severity": number
    },
    "reqId": "string"
}
```

Format de réponse :

```
Message entrant depuis le serveur :

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```


### Codes de réponse pour une demande Ajouter un journal

|Code de réponse |Message |
|:---|:---|
|200   |L'opération a abouti.|
|400   |Le message d'entrée ne correspond pas au format attendu ou l'une des valeurs n'est pas comprise dans la plage valide.|
|404   |Le nom de sujet est incorrect ou le terminal n'est pas dans la base de données.|
|409   |Un conflit s'est produit au cours de la mise à jour de la base de données de terminaux. Pour résoudre ce conflit, simplifiez l'opération si nécessaire.|

## Demandes Effacer des journaux
{: #diag-clear-logs}

Les terminaux peuvent demander à {{site.data.keyword.iot_short_notm}} d'effacer toutes les entrées de journal pour le terminal en utilisant une demande Effacer des journaux.

### Sujet pour une demande Effacer des journaux


Un terminal publie une demande Effacer des journaux sur le sujet suivant :

```
iotdevice-1/clear/diag/log
```

### Format de message pour une demande Effacer des journaux


Format de demande :

```
Message sortant depuis le terminal :

Topic: iotdevice-1/clear/diag/log
{
    "reqId": "string"
}
```

Format de réponse :

```
Message entrant depuis le terminal :

Topic: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Codes de réponse pour une demande Effacer des journaux

|Code de réponse |Message |
|:---|:---|
|200   |L'opération a abouti.|
|400   |Le message d'entrée ne correspond pas au format attendu ou l'une des valeurs n'est pas comprise dans la plage valide.|
|404   |Le nom de sujet est incorrect ou le terminal n'est pas dans la base de données.|
|409   |Un conflit s'est produit au cours de la mise à jour de la base de données de terminaux. Pour résoudre ce conflit, simplifiez l'opération si nécessaire.|

## Demandes Observer les modifications d'attributs
{: #observations-observe}

{{site.data.keyword.iot_short_notm}} peut envoyer une demande Observer les modifications d'attributs à un terminal afin d'observer les modifications apportées à un ou plusieurs attributs de terminal. Lorsque le terminal reçoit la demande, il doit envoyer une demande de notification à {{site.data.keyword.iot_short_notm}} chaque fois que les valeurs des attributs observés sont modifiées.

**Important :** Les terminaux doivent implémenter des opérations d'observation, de notification et d'annulation afin d'assurer la prise en charge des demandes de type [Actions sur le microprogramme - mettre à jour](requests.html#firmware-actions-update).

### Sujet pour une demande Observer les modifications d'attributs


Le serveur publie une demande Observer les modifications d'attributs sur le sujet suivant :

```
iotdm-1/observe
```

### Format de message pour une demande Observer les modifications d'attributs


Le tableau `fields` est un tableau contenant les noms d'attributs du terminal, établis à partir du modèle de terminal. Si une zone complexe, telle que `mgmt.firmware`, est spécifiée, il est prévu que ses zones sous-jacentes soient mises à jour en même temps de sorte qu'un seul message de notification soit généré.

Le paramètre `message` qui est utilisé dans la réponse peut être spécifié si la valeur du paramètre `rc` est différente de `200`. Si une valeur de paramètre spécifiée ne peut être extraite, le paramètre `rc` doit prendre la valeur `404` si le terminal est introuvable, ou la valeur `500` pour toute autre raison. Lorsque des valeurs de paramètres sont introuvables, le tableau `fields` doit contenir des éléments pour lesquels `field` a pour valeur le nom de chaque paramètre qui n'a pas pu être lu. Le paramètre `value` doit être omis. Pour que la valeur du paramètre de code de réponse soit `200`, les paramètres `field` et `value` doivent être spécifiés, `value` étant la valeur en cours d'un attribut identifié par la valeur du paramètre `field`.

Format de demande :

```
Message entrant depuis le serveur :

Topic: iotdm-1/observe
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

Format de réponse :

```
Message sortant depuis le terminal :

Topic: iotdevice-1/response
{
    "rc": number,
    "message": "string",
    "d": {
        "fields": [
            {
                "field": "field_name",
                "value": "field_value"
            }
        ]
    },
    "reqId": "string"
}
```


## Demandes Annuler l'observation d'attributs
{: #observations-cancel}

{{site.data.keyword.iot_short_notm}} peut envoyer une demande de type Annuler l'observation d'attributs à un terminal afin d'annuler l'observation en cours d'un ou de plusieurs attributs de terminal. La partie `fields` de la demande est un tableau de noms d'attribut de terminal établis à partir du modèle d'attribut, par exemple, les paramètres `location`, `mgmt.firmware` ou `mgmt.firmware.state`.

Le paramètre `message` doit être spécifié si la valeur du paramètre `rc` est différente de `200`.

**Important :** Les terminaux doivent implémenter des opérations d'observation, de notification et d'annulation afin d'assurer la prise en charge des demandes de type [Actions sur le microprogramme - mettre à jour](requests.html#firmware-actions-update).

### Sujet pour une demande Annuler l'observation d'attributs


Le serveur publie une demande Annuler l'observation d'attributs sur le sujet suivant :

```
iotdm-1/cancel
```


### Format de message pour une demande Annuler l'observation d'attributs


Format de demande :

```
Message entrant depuis le serveur :

Topic: iotdm-1/cancel
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

Format de réponse :

```
Message sortant depuis le terminal :

Topic: iotdevice-1/response
{
    "rc": number,
    "message": "string",
    "reqId": "string"
}
```



## Demandes Notifier les modifications d'attributs
{: #observations-notify}

{{site.data.keyword.iot_short_notm}} peut créer une demande d'observation portant sur un attribut spécifique ou un ensemble de valeurs en utilisant une demande de type Notifier les modifications d'attributs. Lorsque la valeur de l'attribut ou des attributs est modifiée, le terminal doit envoyer une notification contenant la valeur la plus récente.

La valeur du paramètre `field_name` correspond au nom de l'attribut qui a été modifié, et le paramètre `field_value` correspond à la valeur en cours de l'attribut. L'attribut peut être une zone complexe. Si plusieurs valeurs d'une zone complexe sont mises à jour à la suite d'une seule opération, un seul message de notification est envoyé.

Lorsque le traitement de la demande de notification aboutit, la valeur du paramètre `rc` est `200`. Si la demande est incorrecte, la valeur du paramètre `rc` est `400`. Si le paramètre spécifié dans la demande de notification n'est pas observé, la valeur du paramètre `rc` est `404`.

**Important :** Les terminaux doivent implémenter des opérations d'observation, de notification et d'annulation afin d'assurer la prise en charge des demandes de type [Actions sur le microprogramme - mettre à jour](requests.html#firmware-actions-update).


### Sujet pour une demande Notifier les modifications d'attributs


Un terminal publie une demande Notifier les modifications d'attributs sur le sujet suivant :

```
iotdevice-1/notify
```


### Format de message pour une demande Notifier les modifications d'attributs


Format de demande :

```
Message sortant depuis le terminal :

Topic: iotdevice-1/notify
{
    "d": {
        "field": "field_name",
        "value": "field_value"
    }
    "reqId": "string"
}
```

Format de réponse :

```
Message entrant depuis le serveur :

Topic: iotdm-1/response
{
    "rc": number,
    "reqId": "string"
}
```

### Codes de réponse pour une demande Notifier les modifications d'attributs

|Code de réponse |Message |
|:---|:---|
|200   |L'opération a abouti.|
|400   |Le message d'entrée ne correspond pas au format attendu ou l'une des valeurs n'est pas comprise dans la plage valide.|
|404   |Le nom de sujet est incorrect, le terminal n'est pas dans la base de données ou il n'existe aucune observation pour la zone qui a été signalée.|
|409   |Un conflit s'est produit au cours de la mise à jour de la base de données de terminaux. Pour résoudre ce conflit, simplifiez l'opération si nécessaire.|
|500   |Une erreur interne s'est produite.|
