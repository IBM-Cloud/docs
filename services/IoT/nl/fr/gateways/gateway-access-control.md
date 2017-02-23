---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

# Contrôle d'accès aux passerelles (bêta)

**Important** : Cette fonction est actuellement disponible dans le cadre d'une version bêta limitée. 

Les terminaux de passerelle sont habilitées à agir pour compte d'autres terminaux. Les groupes de ressources de passerelle définissent les terminaux d'une organisation pour le compte desquels les passerelles sont autorisées à agir. Les passerelles peuvent se voir attribuer le rôle *Passerelle standard*. Les passerelles standard peuvent uniquement publier ou s'abonner à des messages pour le compte de terminaux présents dans leur groupe de ressources.
{: #shortdesc}


## Affectation d'un rôle à une passerelle

L'affectation d'un rôle à une passerelle est obligatoire pour la création d'un groupe de ressources pour cette dernière. Les passerelles sans groupe de ressources peuvent agir pour le compte de tous les terminaux de l'organisation. L'affectation du rôle *Passerelles standard* crée automatiquement un nouveau groupe de ressources pour la passerelle. Dès lors qu'une passerelle est affectée à un groupe de ressources, elle peut uniquement agir pour le compte des terminaux de ce groupe de ressources et pour elle-même, même si son rôle est modifié. 

Pour affecter un rôle à une passerelle, utilisez l'API suivante :

```
PUT /authorization/devices/{deviceId}/roles
```

Pour connaître les détails du schéma de demande, voir la [documentation de l'API {{site.data.keyword.iot_full}}](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/put_authorization_devices_deviceId_roles).

## Ajout et retrait de terminaux dans un groupe de ressources

Pour qu'une passerelle dotée du rôle *Passerelle standard* puisse agir pour le compte d'un terminal, celui-ci doit être membre du groupe de ressources affecté à la passerelle. Pour ajouter un grand nombre de terminaux à la fois à un groupe de ressources, utilisez l'API suivante :

```
 PUT /bulk/devices/{groupId}/add
```

Le groupe auquel ajouter des terminaux doit être spécifié dans le chemin de la demande, et les terminaux à ajouter doivent être spécifiés dans le corps de la demande. Pour plus d'informations sur le schéma de demande et les réponses, voir la [documentation de l'API {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/put_bulk_devices_groupId_add).

Pour retirer plusieurs terminaux d'un groupe de ressources, utilisez l'API suivante :

```
PUT /bulk/devices/{groupId}/remove
```

Les terminaux spécifiés dans le corps de la demande seront retirés du groupe spécifié dans le chemin de la demande. Pour plus d'informations sur le schéma de demande et la réponse, voir la [documentation de l'API {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/put_bulk_devices_groupId_remove).

## Recherche d'un groupe de ressources

Des étiquettes de recherche peuvent être associées à des groupes de ressources. Les étiquettes de recherche peuvent être utilisées pour extraire les détails d'un groupe de ressources à l'aide de l'API suivante : 

```
GET /groups
```

Cette API renvoie les groupes de ressources associés à l'étiquette de recherche utilisée. Si aucune étiquette de recherche n'est spécifiée, tous les groupes de ressources sont renvoyés. <!-- For more information about the request schema, response, and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

L'API suivante permet de rechercher un ID de groupe de ressources :

```
GET /authorization/devices/{deviceId}
```

Cette API renvoie l'identificateur unique du ou des groupes de ressources dont ce terminal est membre. Pour plus d'informations sur cette API, voir la [documentation de l'API {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/get_authorization_devices_deviceId).

## Analyse d'un groupe de ressources

Les groupes de ressources peuvent être analysés dans divers paramètres afin de renvoyer les propriétés complètes de tous les terminaux du groupe, les identificateurs uniques de tous les terminaux du groupe ou les propriétés du groupe de ressources. 

Pour renvoyer les propriétés complètes de tous les terminaux du groupe de ressources spécifié, utilisez l'API suivante :

```
GET /bulk/devices/{groupId}
```

Cette API renvoie la liste des propriétés complètes de tous les membres du groupe de ressources spécifié. Pour plus d'informations sur le schéma de demande, les réponses, et pour savoir comment parcourir les résultats, voir la [documentation de l'API {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/get_bulk_devices_groupId).

Pour renvoyer uniquement les identificateurs uniques des membres du groupe de ressources, utilisez l'API suivante :

```
GET /bulk/devices/{groupId}/ids
```

Cette API renvoie les identificateurs uniques de tous les terminaux qui sont membres du groupe de ressources. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Pour renvoyer les propriétés du groupe de ressources, utilisez l'API suivante :

```
GET /groups/{groupId}
```

Cette API renvoie les propriétés du groupe de ressources (nom, description, étiquettes de recherche et identificateur unique) spécifié dans le chemin, mais ne renvoie pas la liste de membres du groupe de ressources. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## Création et suppression d'un groupe de ressources

Des groupes de ressources sont créés et supprimés indépendamment des passerelles de connexion. Pour créer un groupe de ressources, utilisez l'API suivante :

```
POST /groups
```

Cette API crée un groupe de ressources et renvoie les détails du groupe. <!-- For details on the request schema and the responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Pour supprimer un groupe de ressources, utilisez l'API suivante :

```
DELETE /groups/{groupId}
```

Cette API supprime le groupe de ressources spécifié. Les terminaux qui étaient membres du groupe sont retirés de celui-ci, mais les terminaux proprement dits ne sont pas affectés. <!-- For more information, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## Mise à jour des propriétés de groupe



  - /groups/{groupId}
    - PUT : met à jour les propriétés du groupe spécifié. 

## Extraction et mise à jour de propriétés de terminal

Il existe plusieurs façons d'extraire des propriétés de terminal à l'aide d'une API et chaque API renvoie des informations différentes. Pour extraire les propriétés de terminal de tous les terminaux connectés à votre organisation {{site.data.keyword.iot_short_notm}}, utilisez l'API suivante : 

```
GET /authorization/devices:

```

Cette API renvoie les propriétés de tous les terminaux connectés à l'organisation, y compris les propriétés relatives au contrôle d'accès (rôle, état, date d'expiration). <!-- For more information on responses and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Pour extraire des propriétés de terminal sans extraire les informations relatives au contrôle d'accès, utilisez l'API suivante :

```
GET /authorization/devices/{deviceId}
```

Cette API renvoie toutes les propriétés de terminal du terminal spécifié sans renvoyer les informations relatives au contrôle d'accès. <!-- For more information, see the [{{site.data.keyword.iot_short_notm}} device model documentation](LINK TO DEVICE MODEL) and [API documentation](LINK TO CORRECT API). -->

Pour extraire les informations de contrôle d'accès d'un terminal spécifique, utilisez l'API suivante :

```
GET /authorization/devices/{deviceId}/roles:
```

Cette API extrait les informations de contrôle d'accès du terminal spécifié sans renvoyer les autres propriétés de terminal. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Il existe deux façons de mettre à jour des propriétés de terminal. Les propriétés peuvent être mises à jour sans modifier les propriétés de contrôle d'accès ou les propriétés de contrôle d'accès peuvent être mises à jour directement. 

Pour mettre à jour des propriétés de terminal sans affecter le propriétés de contrôle d'accès, utilisez l'API suivante :

```
PUT /authorization/devices/{deviceId}
```

Cette API ne met à jour que les propriétés du terminal qui ne sont pas associées au contrôle d'accès. <!-- For more information on request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Pour mettre à jour uniquement les propriétés de contrôle d'accès du terminal spécifié, utilisez l'API suivante :

```
PUT /authorization/devices/{deviceId}/withroles:
```

Cette API ne met à jour que les propriétés de contrôle d'accès du terminal spécifié. <!-- For more information on the request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->
