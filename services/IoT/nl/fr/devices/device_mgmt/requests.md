---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}  
{:codeblock: .codeblock}
{:pre: .pre}


# Demandes de gestion des terminaux
{: #requests}


{{site.data.keyword.iot_full}} fournit des actions qui peuvent être lancées pour un ou plusieurs terminaux. Ces actions peuvent être lancées à l'aide du tableau de bord ou de l'API REST. Les types d'action disponibles sont les **actions sur les terminaux** et les **actions sur le microprogramme**.

## Lancement de demandes de gestion des terminaux à l'aide du tableau de bord
{: #initiating-dm-dashboard}

Les demandes peuvent être lancées via le tableau de bord en utilisant l'onglet **Actions** de la page Terminaux. Cliquez sur le bouton **Lancer une action** pour sélectionner une action, choisir des terminaux et spécifier d'éventuels paramètres supplémentaires pris en charge par l'action que vous avez sélectionnée.

## Lancement de demandes de gestion des terminaux à l'aide de l'API REST
{: #initiating-dm-api}

Les demandes peuvent être lancées à l'aide de l'exemple d'API REST suivant :  

`POST https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Pour plus d'informations sur le corps d'une demande de gestion des terminaux, voir la [documentation de l'API ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.

## Actions sur les terminaux
{: #device-actions}

Un terminal peut spécifier qu'il prend en charge des actions sur les terminaux lorsqu'il publie une demande de gestion. Une demande d'action sur les terminaux indique à {{site.data.keyword.iot_short_notm}} que le terminal peut répondre à des actions de réamorçage et de réinitialisation de terminal.


## Actions sur les terminaux - réamorçage
{: #device-actions-reboot}

Vous pouvez lancer une action de réamorçage de terminaux à l'aide du tableau de bord {{site.data.keyword.iot_short_notm}} ou de l'API REST.

Pour lancer une opération de réamorçage de terminaux à l'aide de l'API REST, exécutez une demande POST sur :

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Fournissez les informations suivantes :

- L'action `device/reboot`
- Une liste de terminaux à réamorcer (5 000 terminaux au maximum)

Exemple de demande de réamorçage de terminaux :

```
{
    "action": "device/reboot",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

Une fois qu'une demande est lancée, un message MQTT est publié sur tous les terminaux spécifiés dans le corps de la demande de réamorçage. Pour chaque terminal, une réponse doit être renvoyée afin d'indiquer si l'action de réamorçage peut être lancée. Si cette opération peut être lancée immédiatement, affectez au paramètre `rc` la valeur `202`. Si la tentative de réamorçage échoue, affectez au paramètre `rc` la valeur `500` et définissez le paramètre `message` en conséquence. Si le réamorçage n'est pas pris en charge, affectez au paramètre `rc` la valeur `501` et, le cas échéant, définissez le paramètre `message` en conséquence.

L'action de réamorçage est terminée lorsque le terminal envoie une demande Gérer le terminal après avoir été réamorcé.

### Sujet pour une demande de réamorçage de terminaux

Le serveur publie une demande de réamorçage sur un terminal dans le sujet suivant :

```
iotdm-1/mgmt/initiate/device/reboot
```

### Format de message pour une demande de réamorçage de terminaux


Format de demande :

```
Message entrant depuis le serveur :

Topic: iotdm-1/mgmt/initiate/device/reboot
{
    "reqId": "string"
}
```

Format de réponse :

```
Message sortant depuis le terminal :

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```

## Actions sur les terminaux - réinitialisation avec les paramètres d'usine
{: #device-actions-factory-reset}

Vous pouvez lancer une action de réinitialisation avec les paramètres d'usine à l'aide du tableau de bord {{site.data.keyword.iot_short_notm}} ou de l'API REST.

Pour lancer une réinitialisation avec les paramètres d'usine à l'aide de l'API REST, exécutez une demande POST sur :

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Les informations suivantes sont fournies :

- L'action `device/factoryReset`
- Une liste de terminaux à réinitialiser avec les paramètres d'usine (5 000 terminaux au maximum)

L'exemple suivant illustre une demande de réinitialisation de terminal :

```
{
    "action": "device/factoryReset",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

Lorsqu'une demande de réinitialisation de terminal est lancée, un message MQTT est publié sur tous les terminaux qui sont spécifiés dans le corps de la demande. Pour chaque terminal, une réponse doit être renvoyée pour indiquer si l'action de réinitialisation avec les paramètres d'usine peut être lancée. Le code de réponse a pour valeur `202` si cette action peut être lancée immédiatement. Si la tentative de réinitialisation avec les paramètres d'usine échoue, affectez au paramètre `rc` la valeur `500` et définissez le paramètre `message` en conséquence. Si l'action de réinitialisation avec les paramètres d'usine n'est pas prise en charge, affectez au paramètre `rc` la valeur `501` et, le cas échéant, définissez le paramètre `message` en conséquence.

L'action de réinitialisation avec les paramètres d'usine est terminée lorsque le terminal envoie une demande Gérer le terminal après avoir été réinitialisé avec les paramètres d'usine.

### Sujet pour une demande de réinitialisation avec les paramètres d'usine

Le serveur publie la demande suivante sur un terminal :

```
iotdm-1/mgmt/initiate/device/factory_reset
```


### Format de message pour une demande de réinitialisation avec les paramètres d'usine


Format de demande :

```
La rubrique suivante présente le message entrant à partir du serveur :

Topic: iotdm-1/mgmt/initiate/device/factory_reset
{
    "reqId": "string"
}
```

Format de réponse :

```
La rubrique suivante présente un message sortant à partir du terminal :

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```


## Actions sur le microprogramme
{: #firmware-actions}

Le niveau de microprogramme identifié sur un terminal est stocké dans l'attribut `deviceInfo.fwVersion`. Les attributs `mgmt.firmware` sont utilisés pour effectuer une mise à jour de microprogramme et observer son statut.

**Important :** Le terminal géré doit prendre en charge l'observation de l'attribut `mgmt.firmware` afin de prendre en charge les actions sur le microprogramme. 

Le processus de mise à jour du microprogramme est scindé en deux actions distinctes :
- Téléchargement du microprogramme
- Mise à jour du microprogramme

Le statut de chacune des actions sur le microprogramme est stocké dans un attribut distinct sur le terminal. L'attribut `mgmt.firmware.state` décrit le statut du téléchargement de microprogramme. Le tableau suivant décrit les valeurs possibles que vous pouvez définir pour l'attribut `mgmt.firmware.state` :

 |Valeur |Etat  | Signification |
 |:---|:---|:---|
 |0  | Inactif        | Le terminal n'est pas en train de télécharger un microprogramme. |  
 |1  | Téléchargement en cours | Le terminal est en train de télécharger un microprogramme. |
 |2  | Téléchargé  | Le terminal a téléchargé une mise à jour de microprogramme et est prêt à l'installer. |


L'attribut `mgmt.firmware.updateStatus` décrit le statut de la mise à jour de microprogramme. Les valeurs possibles pour l'attribut `mgmt.firmware.updateStatus` sont les suivantes :

|Valeur |Etat | Signification |  
|:---|:---|:---|
|0 | Réussite | Le microprogramme a été mis à jour. |
|1 | En cours | La mise à jour du microprogramme a été lancée mais n'est pas encore terminée.|
|2 | Mémoire insuffisante | Une erreur de mémoire insuffisante a été détectée lors de l'opération.|
|3 | Connexion perdue     | La connexion a été interrompue pendant le téléchargement du microprogramme. |
|4 | Echec de la vérification | Le microprogramme a échoué au test de vérification. |
|5 | Image non prise en charge   | L'image du microprogramme téléchargé n'est pas prise en charge par le terminal. |
|6 | URI non valide         | Le terminal n'a pas pu télécharger le microprogramme à partir de l'URI indiqué. |

## Actions sur le microprogramme - téléchargement
{: #firmware-actions-download}

Vous pouvez lancer une action de téléchargement de microprogramme à l'aide du tableau de bord {{site.data.keyword.iot_short_notm}} ou de l'API REST.

Pour lancer un téléchargement de microprogramme à l'aide de l'API REST, exécutez une demande POST sur :

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Les informations suivantes sont fournies :

- L'action `firmware/download`
- Une liste de terminaux qui doivent recevoir l'image (5 000 terminaux au maximum)
- L'URI de l'image de microprogramme (facultatif) 
- La chaîne de vérification permettant de valider l'image (facultatif)
- Le nom du microprogramme (facultatif)
- La version du microprogramme (facultatif)

L'exemple suivant illustre la demande de téléchargement de microprogramme sur laquelle se basent tous les exemples de message suivants :

```
{
   "action" : "firmware/download",
   "parameters" : [{
         "name" : "uri",
         "value" : "some uri for firmware location"
      }, {
         "name" : "name",
         "value" : "some firmware name"
      }, {
         "name" : "verifier",
         "value" : "some validation code"
      }, {
         "name" : "version",
         "value" : "some firmware version"
      }
   ],
   "devices" : [{
         "typeId" : "someType",
         "deviceId" : "someId"
      }
   ]
}
```

Si aucun des paramètres facultatifs n'est défini, la première étape du processus suivant est ignorée.

Le serveur de gestion des terminaux dans {{site.data.keyword.iot_short_notm}} utilise le protocole de gestion des terminaux pour envoyer une demande aux terminaux, ce qui lance le téléchargement de microprogramme. Le processus de téléchargement se décompose comme suit :

1. Une demande de mise à jour des détails de microprogramme est envoyée au sujet `iotdm-1/device/update`.
La demande de mise à jour permet au terminal de vérifier si le microprogramme demandé est différent de celui actuellement installé. En cas de différence, affectez au paramètre `rc` la valeur `204`, ce qui permet le passage au statut `Modifié`.  
L'exemple suivant illustre le message qui doit s'afficher pour l'exemple de demande de téléchargement de microprogramme envoyée précédente, ainsi que la réponse envoyée lorsqu'une différence est détectée :
```
   Demande entrante depuis {{site.data.keyword.iot_short_notm}} :

   Topic: iotdm-1/device/update
   Message:
   {
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194",
      "d" : {
         "fields" : [{
               "field" : "mgmt.firmware",
               "value" : {
                  "version" : "some firmware version",
                  "name" : "some firmware name",
                  "uri" : "some uri for firmware location",
                  "verifier" : "some validation code",
                  "state" : 0,
                  "updateStatus" : 0,
                  "updatedDateTime" : ""
               }
            }
         ]
      }
   }

   Réponse sortante depuis le terminal :

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 204,
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194"
   }
   ```
   Cette réponse déclenche la demande suivante.
2. La demande d'observation du statut de téléchargement du microprogramme `iotdm-1/observe` est envoyée.
Elle vérifie que le terminal est prêt à lancer le téléchargement de microprogramme. Si le téléchargement peut être lancé immédiatement, affectez au paramètre `rc` la valeur `200` (`Ok`), à l'attribut `mgmt.firmware.state` la valeur `0` (`Inactif`) et à l'attribut `mgmt.firmware.updateStatus` la valeur `0` (`Inactif`). Le code suivant est un exemple d'échange entre {{site.data.keyword.iot_short_notm}} et le terminal :
   ```
   Demande entrante depuis {{site.data.keyword.iot_short_notm}} :

   Topic: iotdm-1/observe
   Message:
   {
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
      "d" : {
         "fields" : [ {
            "field" : "mgmt.firmware"
            }
         ]
      }
   }

   Réponse sortante depuis le terminal :

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 200,
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8"
   }
   ```
Cet échange déclenche la dernière étape.  

3. La demande de téléchargement est envoyée au sujet `iotdm-1/mgmt/initiate/firmware/download` :

   La demande de téléchargement indique à un terminal qu'il peut lancer le téléchargement de microprogramme. Si l'action peut être lancée immédiatement, affectez au paramètre `rc` la valeur `202`. Le code suivant illustre un exemple de lancement d'une demande de téléchargement :

   ```
   Demande entrante depuis {{site.data.keyword.iot_short_notm}} :

   Topic: iotdm-1/mgmt/initiate/firmware/download
   Message:
   {
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }

   Réponse sortante depuis le terminal :

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 202,
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }
   ```

Une fois qu'un téléchargement de microprogramme est lancé de cette façon, le terminal doit envoyer un rapport sur le statut du téléchargement à {{site.data.keyword.iot_short_notm}}. Le terminal envoie un rapport sur le statut en publiant un message au sujet `iotdevice-1/notify`, où l'attribut `mgmt.firmware.state` a pour valeur `1` (`Téléchargement en cours`) ou `2` (`Téléchargé`).
Les exemples suivants illustrent le lancement du téléchargement de microprogramme :

```
Message sortant depuis le terminal :

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "123456789",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 1
             }
      } ]
   }
}


Patientez...


Message sortant depuis le terminal :

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "1234567890",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 2
             }
      } ]
   }
}
```



Une fois la notification publiée avec la valeur  `2` affectée à l'attribut `mgmt.firmware.state`, une demande est déclenchée sur le sujet `iotdm-1/cancel`. Cette demande annule l'observation de l'attribut `mgmt.firmware`.
Lorsqu'une réponse pour laquelle la valeur `200` est affectée au paramètre `rc` est envoyée, le téléchargement de microprogramme est terminé. Le code suivant fournit un exemple :

```
Demande entrante depuis {{site.data.keyword.iot_short_notm}} :

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware"
         }
      ]
   }
}


Message sortant depuis le terminal :

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

Les informations suivantes sont utiles pour le traitement des erreurs :

- Si l'attribut `mgmt.firmware.state` n'a pas pour valeur `0` ("Inactif"), envoyez une erreur avec le code de réponse `400` et un texte de message facultatif.
- Si l'attribut `mgmt.firmware.uri` n'est pas défini ou ne correspond pas à un URI valide, affectez au paramètre `rc` la valeur `400`.
- Si la tentative de téléchargement de microprogramme échoue, affectez au paramètre `rc` la valeur `500` et, le cas échéant, définissez le paramètre `message` en conséquence.
- Si le téléchargement de microprogramme n'est pas pris en charge, affectez au paramètre `rc` la valeur `500` et, le cas échéant, définissez le paramètre `message` en conséquence.
- Lorsqu'une demande d'exécution est reçue par le terminal, remplacez la valeur `0` (Inactif) de l'attribut `mgmt.firmware.state` par `1` Téléchargement en cours).
- Lorsque le téléchargement a abouti, affectez au paramètre `mgmt.firmware.state` la valeur `2` (Téléchargé).
- Si une erreur se produit pendant le téléchargement, affectez à l'attribut `mgmt.firmware.state` la valeur `0` (Inactif) et affectez à l'attribut `mgmt.firmware.updateStatus` l'une des valeurs de statut d'erreur suivantes :
  - 2 (Mémoire insuffisante)
  - 3 (Connexion perdue)
  - 6 (URI non valide)
- Si un vérificateur de microprogramme a été défini, le terminal tente de vérifier l'image du microprogramme. Si la vérification de l'image échoue, affectez à l'attribut `mgmt.firmware.state` la valeur `0` (Inactif) et affectez à l'attribut `mgmt.firmware.updateStatus` la  valeur de statut d'erreur `4` (Echec de la vérification).

## Actions sur le microprogramme - mise à jour
{: #firmware-actions-update}

L'installation du microprogramme téléchargé est lancée à l'aide de l'API REST en exécutant une demande POST sur :

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Les informations suivantes sont fournies :

- L'action `firmware/update`
- La liste des terminaux qui doivent recevoir l'image, tous du même type
- L'URI de l'image de microprogramme (facultatif) 
- La chaîne de vérification permettant de valider l'image (facultatif)
- Le nom du microprogramme (facultatif)
- La version du microprogramme (facultatif)

Le code suivant est un exemple de demande :

```
   {
      "action" : "firmware/update",
      "devices" : [{
            "typeId" : "someType",
            "deviceId" : "someId"
         }
      ]
   }

```

Si aucun des paramètres facultatifs n'est défini, le premier message reçu par le terminal est une demande de mise à jour de terminal. Cette demande de mise à jour de terminal est semblable au premier message de la demande de téléchargement de microcode.

Pour surveiller le statut de la mise à jour de microprogramme, {{site.data.keyword.iot_short_notm}} commence par déclencher une demande d'observation sur le sujet`iotdm-1/observe`. Lorsque le terminal est prêt à lancer le processus de mise à jour, il envoie une réponse pour laquelle le paramètre `rc` a pour valeur `200`, l'attribut`mgmt.firmware.state` a pour valeur `0` et l'attribut `mgmt.firmware.updateStatus` a pour valeur `0`.

Le code suivant fournit un exemple :

```
Demande entrante depuis {{site.data.keyword.iot_short_notm}} :

Topic: iotdm-1/observe
Message:
{
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
      "d" : {
      "fields" : [
         {
            "field" : "mgmt.firmware"
         }
      ]
   }
}

Réponse sortante depuis le terminal :

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```



Une fois la mise à jour de microprogramme téléchargée, le serveur de gestion des terminaux dans {{site.data.keyword.iot_short_notm}} utilise le protocole de gestion des terminaux pour demander aux terminaux spécifiés de lancer l'installation du microprogramme à l'aide du sujet `iotdm-1/mgmt/initiate/firmware/update`.
Si cette opération peut être lancée immédiatement, affectez au paramètre `rc` la valeur `202`.
Si le téléchargement du microprogramme n'a pas abouti, affectez au paramètre `rc` la valeur `400`.

Le code suivant fournit un exemple :

```
Demande entrante depuis {{site.data.keyword.iot_short_notm}} :

Topic: iotdm-1/mgmt/initiate/firmware/update
Message:
{
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}

Réponse sortante depuis le terminal :

Topic: iotdevice-1/response
Message:
{
   "rc" : 202,
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}
```

Pour terminer la demande de mise à jour de microprogramme, le terminal envoie un rapport sur le statut de la mise à jour à {{site.data.keyword.iot_short_notm}} en utilisant un message de statut publié sur son sujet `iotdevice-1/notify`.
Lorsque la mise à jour d'un microprogramme est terminée, l'attribut `mgmt.firmware.updateStatus` prend la valeur `0` (réussite) et l'attribut `mgmt.firmware.state` prend la valeur `0` (Inactif). A ce stade, l'image de microprogramme téléchargée peut être supprimée du terminal, et l'attribut `deviceInfo.fwVersion` prend la valeur de l'attribut `mgmt.firmware.version`.

Le code suivant fournit un exemple de message de notification :

```
Message sortant depuis le terminal :

Topic: iotdevice-1/notify
Message:
{
   "d" : {
      "fields": [
         {
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```

Lorsque {{site.data.keyword.iot_short_notm}} reçoit une notification lui indiquant que la mise à jour de microprogramme est terminée, il déclenche une dernière demande sur le sujet `iotdm-1/cancel` pour annuler l'observation de l'attribut `mgmt.firmware`.


Lorsqu'une réponse pour laquelle la valeur `200` est affectée au paramètre `rc` est envoyée, la demande de mise à jour de microprogramme est terminée, comme illustré dans l'exemple suivant :

```
Demande entrante depuis {{site.data.keyword.iot_short_notm}} :

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [
         {
            "field" : "mgmt.firmware"
         }
      ]
   }
}


Message sortant depuis le terminal :

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

La liste suivante fournit des informations utiles pour le traitement du processus et des erreurs :

- Si la tentative de mise à jour de microprogramme échoue, affectez au paramètre `rc` la valeur `500` et, le cas échéant, définissez le paramètre `message` en conséquence.
- Si la mise à jour de microprogramme n'est pas prise en charge, affectez au paramètre `rc` la valeur `501` et, le cas échéant, définissez le paramètre `message` en conséquence.
- Si l'attribut `mgmt.firmware.state` n'a pas pour valeur `2` (Téléchargé), envoyez une erreur avec la valeur `400` affectée au paramètre `rc` et un texte de message facultatif.
- Sinon, affectez à l'attribut `mgmt.firmware.updateStatus` la valeur `1` (En cours), et l'installation du microprogramme démarrera.
- Si l'installation du microprogramme échoue, affectez à l'attribut `mgmt.firmware.updateStatus` l'une des valeurs suivantes :
  - `2` (Mémoire insuffisante)
  - `5` (Image non prise en charge)


**Important :** Tous les paramètres répertoriés avec l'attribut `mgmt.firmware` doivent être définis en même temps de sorte que s'il existe une observation en cours pour `mgmt.firmware`, un seul message de notification soit envoyé.

## Recettes relatives aux actions sur les terminaux et aux actions sur un microprogramme

Les recettes suivantes décrivent le flux complet requis pour effectuer des actions sur les terminaux et sur un microprogramme.

- [Device Management in WIoT Platform – Roll Back & Factory Reset ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}

- [Device Initiated Firmware Update ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-device-initiated-firmware-upgrade/){: new_window}

- [Platform Initiated Firmware Update ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [Platform Initiated Firmware Update with Background Execution ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [Firmware Roll Back & Factory Reset ![Icône de lien externe](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}
