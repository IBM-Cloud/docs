---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-10-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Modèle de terminal
{: #device_model}

Le modèle de terminal décrit les métadonnées et les caractéristiques de gestion d'un terminal. La base de données de terminaux d'{{site.data.keyword.iot_full}} représente la principale source d'informations sur les terminaux. Les applications et les terminaux gérés peuvent envoyer des mises à jour, y compris les modifications d'emplacement ou la progression d'une mise à jour de microprogramme, à la base de données de terminaux. Dès que ces mises à jour sont reçues par {{site.data.keyword.iot_short_notm}}, la base de données est mise à jour et les informations sont disponibles pour les applications.

**Remarque :** A l'exception de l'[extension des terminaux](#devicemanagementextension), la totalité du modèle de terminal est disponible pour les terminaux gérés et non gérés. Toutefois, un terminal non géré ne peut pas mettre à jour directement son modèle de terminal dans la base de données.

## Identification du terminal
{: #device_id}

Des attributs `typeId` et `deviceId` sont affectés à chaque terminal. En général, `typeId` représente le modèle de votre terminal, tandis que `deviceId` peut représenter son numéro de série. Dans votre organisation {{site.data.keyword.iot_short_notm}}, la combinaison des attributs `typeId` et `deviceId` doit être unique pour chaque terminal.

Outre ces attributs, {{site.data.keyword.iot_short_notm}} construit un autre identificateur pour chaque terminal. Cet identificateur s'appelle `clientId`. L'attribut `clientId` est basé sur l'attribut `organizationId` et sur les valeurs `typeId` et `deviceId` spécifiques du terminal. L'attribut `clientId` permet d'identifier de manière unique chaque terminal. Les caractères pouvant être utilisés dans ces identificateurs sont restreints de manière à assurer la compatibilité de ces derniers avec les protocoles de communication et les API REST.

Les identificateurs de terminal facultatifs suivants peuvent également être utilisés :

- deviceInfo.manufacturer
- deviceInfo.serialNumber
- deviceInfo.model
- deviceInfo.deviceClass
- deviceInfo.description

Pour obtenir plus d'informations sur les identificateurs, ainsi que des descriptions comparées des identificateurs utilisés dans d'autres normes de gestion des terminaux, voir [Attributs](#attributes).


## Identificateurs et types de terminal
{: #id_and_device_types}

Chaque terminal qui est connecté à {{site.data.keyword.iot_short_notm}} est associé à un type de terminal. Les types de terminal sont des groupes de terminaux ayant des caractéristiques ou des comportements communs.

Un type de terminal possède un ensemble d'attributs. Lorsqu'un terminal est ajouté à {{site.data.keyword.iot_short_notm}}, les attributs définis dans son type de terminal sont utilisés en tant que modèle. Si une valeur est associée au terminal, elle est utilisée. Si aucune valeur n'est associée au terminal, la valeur de type de terminal est utilisée. Par exemple, le type de terminal peut inclure une valeur pour l'attribut `deviceInfo.fwVersion` indiquant la version du microprogramme installé au moment de la fabrication du terminal. Cette valeur est copiée à partir du type de terminal sur les terminaux au moment de leur ajout. Lorsqu'un terminal est ajouté, si l'attribut `deviceInfo.fwVersion` possède déjà une valeur, celle-ci n'est pas remplacée.

Lorsqu'un attribut de type de terminal est mis à jour, seuls les nouveaux terminaux enregistrés héritent des modifications apportées au modèle de type de terminal.

## Attributs
{: #attributes}

Le tableau ci-dessous présente la liste des attributs qui peuvent s'appliquer aux terminaux de {{site.data.keyword.iot_short_notm}}. Les attributs en italique peuvent également s'appliquer à des types de terminal.

Légende :
  - API : Peut être mis à jour à l'aide d'API
  - DMA : Peut être mis à jour à l'aide de l'agent de gestion des terminaux
  - R : Accessible en lecture seule
  - E : Accessible en écriture et en lecture
  - A : Ajout

Attribut                        | Type       | Description                                       | API | AGT   
------------- | ------------- | ------------- | ------------- | -------------  |
 clientId                         | Chaîne     | ID client utilisé avec des connexions MQTT          |  R  |   -  
 *typeId*                         | Chaîne     | Type de terminal                                       |  R  |   -  
 deviceId                         | Chaîne     | ID de terminal                                         |  R  |    -
 classId                          | Chaîne     | Classe de terminal ("Terminal" ou "Passerelle")           |  R  |   -  
 gatewayTypeId                    | Chaîne     | ID de type de la passerelle utilisée par ce terminal       |  R  |    -
 gatewayId                        | Chaîne     | ID de terminal de la passerelle utilisée par ce terminal     |  R  |   -  
 status.alert                     | Booléen    | Indique si le terminal inclut une alerte                   |  W  |  -   
 *deviceInfo.serialNumber*        | Chaîne     | Numéro de série du terminal                   |  W  |  W    
 *deviceInfo.manufacturer*        | Chaîne     | Fabricant du terminal                    |  W  |  W   
 *deviceInfo.model*               | Chaîne     | Modèle du terminal                           |  W  |  W  
 *deviceInfo.deviceClass*         | Chaîne     | Classe du terminal                           |  W  |  W  
 *deviceInfo.description*         | Chaîne     | Nom descriptif du terminal                |  W  |  W  
 *deviceInfo.fwVersion*           | Chaîne     | Version du microprogramme actuellement identifiée sur le terminal    |  W  |  W  
 *deviceInfo.hwVersion*           | Chaîne     | Version du matériel du terminal                |  W  |  W  
 *deviceInfo.descriptiveLocation* | Chaîne     | Emplacement descriptif, par exemple, une salle, un numéro de bâtiment ou une région géographique      |  W  |  W  
 *metadata*                       | Complexe    | Métadonnées à format libre                                |  W  |  W  
 added.auth.id                    | Chaîne     | ID qui a ajouté le terminal                          |  R  |   -  
 added.dateTime                   | Chaîne     | ISO8601 date-time : Date et heure auxquelles le terminal a été ajouté |  R  |    -
 refs.diag.errorCodes             | Chaîne     | URI de l'extension de diagnostics des codes d'erreur, s'il existe |  R  |   -  
 refs.diag.logs                   | Chaîne     | URI de l'extension de diagnostics des journaux, s'il existe        |  R  |   -  
 refs.location                    | Chaîne     | URI de l'extension d'emplacement, s'il existe             |  R  |   -  
 refs.mgmt                        | Chaîne     | URI de l'extension de gestion des terminaux, s'il existe                 |  R  |    -



## Attributs étendus
{: #extended_attributes}

Outre les attributs principaux répertoriés précédemment dans la section Attributs, il existe un certain nombre d'attributs supplémentaires traités en tant qu'extensions du modèle de terminal de base. Des requêtes simples relatives au terminal renvoient des informations provenant du modèle de terminal de base mais pas des extensions. Les informations des extensions doivent être spécifiquement demandées.


Nom d'extension    | Préfixe des attributs | Objet      
------------- | ------------- | -------------                                         
 Diagnostics       | diag                 | Journaux des erreurs et informations de diagnostic                 
 Emplacement          | location             | Emplacement du terminal, pouvant être régulièrement mis à jour
 Gestion des terminaux | mgmt                 | Actions de gestion des terminaux, par exemple la mise à jour du microprogramme       


### Extension Diagnostics


Les attributs de diagnostic sont facultatifs et sont disponibles uniquement pour les terminaux qui incluent des informations du journal des erreurs. Ces attributs permettent de diagnostiquer des incidents liés aux terminaux et non pas de traiter les incidents de connectivité avec {{site.data.keyword.iot_short_notm}}. La quantité d'informations stockées dans les attributs de diagnostic peut être importante et les requêtes portant sur ces informations doivent être spécifiques.

Les informations des journaux de diagnostic sont stockées sous la forme de tableau d'entrées. Chaque entrée se compose d'un message, d'un niveau de gravité, d'un horodatage et d'un tableau d'octets facultatif pour les données. Vous pouvez ajouter des entrées à l'aide d'une API. Toutefois, l'ajout d'entrées peut entraîner la perte d'entrées précédentes afin que la taille des journaux de diagnostics reste gérable.


Attribut            | Type       | Description                                                 | API | AGT
------------- | ------------- | ------------- | ------------- | -------------
 diag.errorCodes[]    | Tableau d' </br> entier(s)  | Tableau de codes d'erreur                                        |  A  |  A  
 diag.log[]           | Tableau      | Tableau de données de diagnostic                                    |  A  |  A  
 diag.log[].message   | Chaîne     | Message de diagnostic                                          |  -   |    -
 diag.log[].timestamp | Chaîne     | ISO8601 date-time : Date et heure de l'entrée de journal               |  -   |    -
 diag.log[].logData   | Chaîne     | byte : Données de diagnostic codées en base 64                      |  -   |    -
 diag.log[].severity  | Nombre     | Niveau de gravité du message, à savoir 0 : informations, 1 : avertissement, 2 : erreur |  -   |    -


### Extension Emplacement

Les attributs d'emplacement sont facultatifs et sont disponibles uniquement pour les terminaux qui incluent des informations d'emplacement. Les informations d'emplacement sont stockées séparément pour permettre une utilisation des mécanismes de stockage mieux adaptée aux informations dynamiques. Cela peut s'avérer essentiel dans le cas d'informations fréquemment mises à jour, par exemple sur un terminal mobile.

Dans les solutions où les mises à jour d'emplacement sont particulièrement fréquentes, l'emplacement doit être traité avec le contenu des événements du terminal pour permettre des fréquences de mise à jour plus élevées et simplifier les mécanismes de stockage d'historique et les analyses de données.


Attribut                 | Type   | Description                                             | API | AGT
------------- | ------------- | ------------- | ------------- | -------------
 location.longitude        | Nombre | Longitude en degrés décimaux à l'aide de WGS84                |  W  |  W  
 location.latitude         | Nombre | Latitude en degrés décimaux à l'aide de WGS84                 |  W  |  W  
 location.elevation        | Nombre | Elévation en mètres à l'aide de WGS84                         |  W  |  W  
 location.measuredDateTime | Chaîne |ISO8601 date-time : Date et heure de la mesure d'emplacement |  W  |  W  
 location.updatedDateTime  | Chaîne | ISO8601 date-time : Date et heure                        |  R  |   
 location.accuracy         | Nombre | Précision de la position en mètres                      |  W  |  W  


### Extension Gestion des terminaux
{: #devicemanagementextension}

Les attributs de gestion ne sont présents que pour les terminaux gérés. Lorsqu'un terminal géré passe en mode veille, il devient non géré et les attributs `mgmt.` sont supprimés. Les attributs `mgmt.` sont définis par {{site.data.keyword.iot_short_notm}} suite au traitement des demandes de gestion des terminaux. Ces attributs ne peuvent pas être directement écrits à l'aide de l'API.

Les terminaux possèdent un cycle de vie de gestion défini par leur statut de terminaux gérés. Sur le terminal, l'agent de gestion des terminaux est chargé d'envoyer une demande Gérer le terminal à l'aide du protocole de gestion des terminaux. Pour traiter les terminaux obsolètes dans des parcs de terminaux importants, vous pouvez contraindre un terminal géré à envoyer régulièrement une demande Gérer le terminal. Un terminal géré passe en mode veille si cette demande n'est pas envoyée à {{site.data.keyword.iot_short_notm}} pendant une période spécifiée. Pour faciliter l'utilisation de cette fonction, un paramètre de durée de vie facultatif peut être associé à la demande Gérer le terminal. Lorsque {{site.data.keyword.iot_short_notm}} reçoit une demande Gérer le terminal avec le paramètre de durée de vie défini, il calcule la date et l'heure avant lesquelles une autre demande Gérer le terminal doit être émise et il stocke ces informations dans l'attribut `mgmt.dormantDateTime`.


Attribut                     | Type    | Description                             | API | AGT
------------- | ------------- | ------------- | ------------- | -------------
 mgmt.dormant                   | Booléen | Indique si le terminal est passé en mode veille                  |  R  |  -
 mgmt.dormantDateTime           | Chaîne  | ISO8601 date-time : Date et heure auxquelles le terminal géré passe en mode veille   |  R  |  -   
 mgmt.lastActivityDateTime      | Chaîne  | ISO8601 date-time : Date et heure de la dernière activité, mises à jour régulièrement    |  R  |    -
 mgmt.supports.deviceActions    | Booléen | Indique si le terminal prend en charge les actions Réamorcer et Réinitialiser avec les paramètres d'usine  |  R  |   -  
 mgmt.supports.firmwareActions  | Booléen | Indique si le terminal prend en charge les actions de téléchargement et de mise à jour du microprogramme    |  R  |     -
 mgmt.firmware.version          | Chaîne  | Version du microprogramme installé sur le terminal              |  R  |  W  
 mgmt.firmware.name             | Chaîne  | Nom du microprogramme utilisé sur le terminal      |  R  |  W  
 mgmt.firmware.uri              | Chaîne  | URI à partir duquel l'image du microprogramme peut être téléchargée |  R  |  W  
 mgmt.firmware.verifier         | Chaîne  | Vérificateur, par exemple un total de contrôle, permettant de valider l'intégrité de l'image du microprogramme |  R  |  W  
 mgmt.firmware.state            | Nombre  | Indique l'état du téléchargement du microprogramme               |  R  |  W  
 mgmt.firmware.updateStatus     | Nombre  | Indique le statut de la mise à jour                     |  R  |  W  
 mgmt.firmware.updatedDateTime  | Chaîne  | ISO8601 date-time : Date de la dernière mise à jour                 |  R  |    -
