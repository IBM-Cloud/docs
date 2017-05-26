---

copyright:

years: 2015, 2017

lastupdated: "2017-03-16"


---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Connexion de passerelles
{: #IoT_connectGateway}

Avant de pouvoir commencer à recevoir des données depuis des terminaux connectés à vos passerelles, vous devez connecter la passerelle à {{site.data.keyword.iot_full}}. Connecter une passerelle à {{site.data.keyword.iot_short_notm}} implique de créer un type de terminal de passerelle et d'enregistrer la passerelle auprès de {{site.data.keyword.iot_short_notm}}. Vous pouvez ensuite utiliser les informations d'enregistrement pour connecter la passerelle à {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

Les passerelles représentent une classe spécialisée de terminal dans {{site.data.keyword.iot_short_notm}}. Les passerelles servent de points d'accès à {{site.data.keyword.iot_short_notm}} pour les autres terminaux.


## Avant de commencer
{: #Prerequisites}

Les terminaux de passerelle possèdent des autorisations supplémentaires par rapport aux terminaux réguliers et peuvent exécuter les fonctions suivantes :
- Enregistrer de nouveaux terminaux sur {{site.data.keyword.iot_short_notm}}
- Envoyer et recevoir leurs propres données de détection, tout comme un terminal connecté
- Envoyer et recevoir des données pour le compte des terminaux qui leur sont connectés
- Exécuter un agent de gestion des terminaux, de manière à pouvoir le gérer, et gérer les terminaux qui lui sont connectés  
Pour les informations du développeur de passerelle, voir [Connectivité MQTT pour les passerelles](mqtt.html).

Vous pouvez également utiliser des passerelles pour exécuter des fonctions Edge Analytics sur les données envoyées par les terminaux de passerelle. Pour plus d'informations, voir[Edge analytics](../edge_analytics.html) et [Installation de l'agent Edge Analytics](#edge).

## Etape 1 : Enregistrement de votre passerelle auprès de {{site.data.keyword.iot_short_notm}}  
{: #register_gateway}

Enregistrer une passerelle implique de classifier le terminal en tant que type de passerelle, de donner un nom à la passerelle et de fournir des informations la concernant. Vous indiquez ensuite un jeton de connexion ou vous acceptez un jeton qui est généré par {{site.data.keyword.iot_short_notm}}.


**Astuce :** Vous pouvez ajouter une seule passerelle à la fois depuis le tableau de bord {{site.data.keyword.iot_short_notm}} ou vous pouvez utiliser l'[API d'administration d'organisation ![Icône de lien externe](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html#!/Device_Bulk_Configuration/post_bulk_devices_add){: new_window} pour ajouter une ou plusieurs passerelles à la fois.

Pour ajouter une passerelle depuis le tableau de bord {{site.data.keyword.iot_short_notm}} :

1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, sélectionnez **Terminaux**.
2. Cliquez sur **Ajouter un terminal**.
3. Sélectionnez ou créez un type de terminal pour le terminal que vous ajoutez.  
Chaque terminal connecté à {{site.data.keyword.iot_short_notm}} doit être associé à un type de terminal. Les types de terminaux sont des groupes de terminaux ayant des caractéristiques communes.  
 1. Cliquez sur **Créer un type de terminal**, puis sur **Créer un type de passerelle**.
 2. Entrez un nom de type de terminal, par exemple, `my_gateway_type`, et une description pour le type de passerelle.   
 **Important :** Le nom du type de terminal ne doit pas dépasser 36 caractères et peut uniquement contenir les caractères suivants :
 <ul>
  <li>Caractères alphanumériques (a-z, A-Z, 0-9)</li>
  <li>Traits d'union (-)</li>
  <li>Traits de soulignement (&lowbar;)</li>
  <li>Points (.)</li>
  </ul>3. Facultatif : Entrez des métadonnées et des attributs de type de passerelle.    
 **Astuce :** Vous pouvez ajouter et éditer des attributs et des métadonnées ultérieurement.
 4. Cliquez sur **Créer** pour ajouter le nouveau type de passerelle.
10. Cliquez sur **Suivant** pour commencer le processus d'ajout de votre terminal de passerelle avec le type de passerelle sélectionné.
11. Entrez un ID de terminal, tel que `my_gateway_device`.  
L'ID de terminal permet d'identifier le terminal de passerelle dans le tableau de bord {{site.data.keyword.iot_short_notm}} et représente également un paramètre requis pour la connexion de votre terminal de passerelle à {{site.data.keyword.iot_short_notm}}.  
**Important :** L'ID de terminal ne doit pas dépasser 36 caractères et peut uniquement contenir les caractères suivants :
 <ul>
 <li>Caractères alphanumériques (a-z, A-Z, 0-9)</li>
 <li>Traits d'union (-)</li>
 <li>Traits de soulignement (&lowbar;)</li>
 <li>Points (.)</li>  
 </ul>
 **Astuce :** Pour les terminaux connectés à un réseau, l'ID de terminal pourrait être par exemple l'adresse MAC du terminal sans aucun deux-points de séparation.  
12. Facultatif : Cliquez sur **Zones supplémentaires** pour ajouter des informations de terminal de passerelle, par exemple, le numéro de série, le fabricant, le modèle, etc.  
 **Astuce :** Vous pouvez ajouter et éditer ces informations ultérieurement.
12. Facultatif : Entrez les métadonnées JSON de terminal.  
 **Astuce :** Vous pouvez ajouter et éditer des métadonnées de terminal ultérieurement.
13. Cliquez sur **Suivant** pour terminer l'ajout de votre terminal de passerelle.
14. Vérifiez que les informations récapitulatives sont correctes, puis cliquez sur  **Ajouter** pour ajouter le terminal de passerelle.  
**Astuce :** Vous avez la possibilité d'accepter un jeton d'authentification généré automatiquement ou de fournir vous-même un jeton d'authentification. Si vous choisissez de créer votre propre jeton, assurez-vous qu'il comporte entre 8 et 36 caractères et qu'il contient une combinaison de minuscules et de majuscules, des nombres, un trait d'union, un tiret de soulignement ou un point. Le jeton ne doit pas contenir des séquences de caractères répétés, des mots de dictionnaire, des noms d'utilisateur ni d'autres séquences prédéfinies.
15. Sur la page Informations sur le terminal, copiez et sauvegardez les informations de terminal suivantes :  
 - ID d'organisation, par exemple, `tubo8x`
 - Type de terminal, par exemple, `my_gateway_type`
 - ID de terminal. **Astuce :** Pour les terminaux connectés à un réseau, cela pourrait être par exemple l'adresse MAC sans aucun deux-points de séparation.
 - Méthode d'authentification, par exemple, `token`
 - Jeton d'authentification, par exemple, `PtBVriRqIg4uh)_-Kl`  
  **Astuce :** Vous aurez besoin d'un ID d'organisation, d'un jeton d'authentification, d'un type de terminal et d'un ID de terminal pour configurer votre terminal afin qu'il se connecte à {{site.data.keyword.iot_short_notm}}.  

Félicitations, vous avez enregistré votre terminal de passerelle. Vous pouvez maintenant configurer votre terminal de passerelle pour qu'il se connecte à {{site.data.keyword.iot_short_notm}}.

Pour obtenir les instructions étape par étape qui illustrent le flux requis pour enregistrer une passerelle, voir la recette [How to Register Gateways in IBM Watson IoT Platform ![Icône de lien externe](../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/how-to-register-gateways-in-ibm-watson-iot-platform/){:new_window}.

## Etape2 : Connexion de votre passerelle à {{site.data.keyword.iot_short_notm}}
{: #connect_gateway}

Après avoir enregistré une passerelle auprès de {{site.data.keyword.iot_short_notm}}, utilisez les informations d'enregistrement pour connecter la passerelle à {{site.data.keyword.iot_short_notm}} et commencer à recevoir des données depuis des terminaux qui sont connectés à la passerelle.

Pour plus d'informations sur la connexion de votre passerelle à {{site.data.keyword.iot_short_notm}}, voir [Connectivité MQTT pour les passerelles](mqtt.html).

**Astuce :** Il existe une gamme de recettes disponibles pour la connexion de terminaux à {{site.data.keyword.iot_short_notm}}. Pour obtenir une liste de recettes, voir les [recettes de connexion de terminal ![Icône de lien externe](../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){:new_window} disponibles sur le site IBM.com.


## Etape 3 : Connexion de terminaux via la passerelle
{: #gateway_devices}

Les terminaux qui sont connectés à la passerelle sont automatiquement ajoutés à {{site.data.keyword.iot_short_notm}} lorsque la passerelle publie des messages depuis le terminal. Le type de terminal et le terminal proprement dit sont créés automatiquement lorsque la passerelle publie un message pour la combinaison de type de terminal et d'ID de terminal qui n'existe pas.

Pour plus d'informations sur l'enregistrement automatique de terminal et la publication et la réception de donnés pour les terminaux connectés, voir [Connectivité MQTT pour les passerelles](mqtt.html).


Lorsqu'un terminal se connecte à votre passerelle, il s'affiche sur le tableau de bord de votre organisation {{site.data.keyword.iot_short_notm}}.

Pour obtenir un flux détaillé et une description, voir la recette [Connecting Raspberry Pi as a Gateway to Watson IoT ![Icône de lien externe](../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/connecting-raspberry-pi-as-a-gateway-to-watson-iot-using-node-red/){:new_window}.

**Remarque :** Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, les terminaux et les passerelles qui sont directement connectés à {{site.data.keyword.iot_short_notm}} affichent une icône de statut sur le tableau de bord pour indiquer qu'ils sont connectés. Le tableau de bord affiche les terminaux qui sont connectés indirectement via une passerelle comme des terminaux étant déconnectés car il ne reconnaît pas les terminaux qui sont connectés via la passerelle.


## Installation d'Edge Analytics Agent
{: #edge}

Edge Analytics Agent (EAA) est un composant logiciel qui s'intègre par dessus un moteur de flux de données optimisé pour le traitement de la périphérie afin d'exécuter des opérations Edge Analytics sur une passerelle en téléchargeant et en gérant des règles Edge Analytics depuis le tableau de bord {{site.data.keyword.iot_short_notm}}. Pour plus d'informations sur Edge Analytics, voir [Edge Analytics](../edge_analytics.html).

### Installation d'EAA
{: #eaa_install}

Pour installer l'agent EAA sur votre passerelle :
1. Dans le tableau de bord {{site.data.keyword.iot_short}}, accédez à **Règles**.
2. Cliquez sur **Télécharger un agent Edge** pour accéder à la [communauté IBM Edge Analytics ![Icône de lien externe](../../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true){:new_window}.
3. Accédez à la section **Fichiers** et téléchargez les répertoires compressés appropriés pour votre type de passerelle.  
La solution Edge Analytics est disponible en tant que logiciel SDK pour les terminaux qui prennent en charge Java en tant que DSLink pour les terminaux de passerelle Cisco.
4. Pour plus d'informations sur l'installation et la configuration du composant logiciel EAA sur votre passerelle, voir les informations suivantes :
 - Logiciel SDK  
 Voir le PDF et le fichier Readme, ainsi que les liens de vidéo disponibles dans la communauté.  
 La recette [Edge Recipe for SDK - Getting Started (SDK) ![Icône de lien externe](../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/getting-started-with-the-ibm-edge-analytics-sdk-in-watson-iot-platform/){:new_window}.
 - DSLink  
 La recette [Getting started with Edge Analytics in Watson IoT Platform ![Icône de lien externe](../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/?post_type=pnext_tutorial&p=19472){:new_window}.

### Paramètres de configuration de l'agent EAA
{: #eaa_configuration}

Vous pouvez utiliser le fichier config.properties de l'agent EAA pour définir des paramètres de configuration logicielle de base.

Pour mettre à jour la configuration de l'agent EAA :
1. Sur le système de passerelle sur lequel s'exécute l'agent EAA, localisez le fichier config.properties de ce dernier.  
Par exemple :
`../dglux-server/dslinks/ibm-watson-iot-edge-analytics-dslink-java-0.0.1/config.properties`
2. Avant de commencer à éditer les paramètres, faites une copie de sauvegarde du fichier.
3. Ouvrez le fichier config.properties pour l'éditer.
4. Editez les paramètres de configuration pour votre environnement :
 <dl>
 <dt>DataDirectSendEnable</dt>
 <dd>BOOLEAN (true|false)</br>
 TRUE (valeur par défaut) - Envoyer toutes les données à {{site.data.keyword.iot_short_notm}}.</br>
 FALSE - Envoyer les données à {{site.data.keyword.iot_short_notm}} uniquement si des règles sont définies sur le moteur. </dd>
 <dt>MonitorInterval</dt>
 <dd>INTEGER (milliseconds)</br>
 Durée (en millisecondes) avant l'envoi d'un nouveau message de surveillance à {{site.data.keyword.iot_short_notm}}. </br>
 Définissez une valeur faible pour communiquer des mesures de surveillance plus souvent. Définissez une valeur élevée pour que des informations de surveillance plus détaillées soient envoyées à {{site.data.keyword.iot_short_notm}}. </br>
 DEFAULT: 60000    </br>
 RECOMMENDED RANGE: [1000, 360000]</dd>
 <dt>MonitorLogDesample</dt>
 <dd>INTEGER  </br>
 Rapport de déséchantillonnage entre le nombre de messages de surveillance envoyés à {{site.data.keyword.iot_short_notm}} et le nombre de messages saisis dans le journal local. Par exemple, si `MonitorLogDesample` a pour valeur 10, une seule entrée de journal local est écrite pour chaque blocs de dix messages envoyés à {{site.data.keyword.iot_short_notm}}. </br>Un nombre élevé permet d'obtenir un journal local de petite taille. Un nombre faible fournit un journal local plus détaillé.</br>
 DEFAULT: 10</br>
 RECOMMENDED RANGE: [1, 100]</dd>
 <dt>MemoryAlertThreshold</dt>
 <dd>INTEGER (Megabytes)</br>
 Seuil de segment de mémoire de machine virtuelle Java libre à partir duquel un message de journal d'avertissement est envoyé au journal de diagnostics {{site.data.keyword.iot_short_notm}}. L'alerte est gérée par la surveillance. </br>Une valeur faible réduit le nombre de messages d'alerte envoyés à {{site.data.keyword.iot_short_notm}}. Une valeur élevée génère un avertissement précoce si le serveur EAA rencontre des problèmes de mémoire.</br>**Astuce :** Vous pouvez utiliser des règles [Cloud Analytics](../cloud_analytics.html) pour configurer des actions de règle, telles que des notifications par courrier électronique qui vous informent en cas de problèmes de mémoire. Pour plus d'informations sur les propriétés disponibles que vous pouvez utiliser pour générer des règles, voir [Mesures de diagnostic Edge Analytics Agent](../edge_analytics.html#eaa_metrics).</br>
  DEFAULT: 10</br>
 RECOMMENDED RANGE: [10 or 5% of the total memory, 200]</dd>
 </dl>
5. Sauvegardez le fichier éditer, puis redémarrez l'agent EAA.

Exemple de fichier config.properties de l'agent EAA
```
#######################################################################
# Engine Parameters
#######################################################################
# DataDirectSendEnable
#                    - BOOLEAN(true|false) Set to true to forward all
#                      the data; Set to false to disable data direct
#                      send to IOTP when there is no rule set in the
#                      engine.
#                      DEFAULT: true
#######################################################################
DataDirectSendEnable=true

#######################################################################
# Monitoring Parameters
#######################################################################
# MonitorInterval    - INTEGER Time interval in milliseconds before a
#                      new monitoring message is generated. Set it to a
#                      small value to report the monitor metrics more
#                      frequently. Set it to a big value to have more
#                      detailed monitoring information on IoTP.
#                      DEFAULT: 60000    RECOMMEND: [1000, 360000]
# MonitorLogDesample - INTEGER The de-sampling ratio of the number of
#                      monitoring messages sent to IOTP vs. local log,
#                      i.e. number of monitoring messages N where
#                      EAA would output only one to the Info log for
#                      every N messages. Set it big to keep the size
#                      of the log small. Set it small to have detailed
#                      monitoring information in local log.
#                      DEFAULT: 10       RECOMMEND: [1, 100]
# MemoryAlertThreshold
#                    - INTEGER the free JVM heap memory in megabyte under
#                      which a log message would be generated and send to
#                      IOTP diagnosis log. The alert is driven by the
#                      monitoring. Set it small to eliminate unnecessary
#                      alert message on IoTP. Set it big to receive early
#                      alert when the system is likely to crash. Set to
#                      Min(Max(10MB, 5% of the total memory), 200MB) is
#                      recommended.
#                      DEFAULT: 10       RECOMMEND: [10, 200]
#######################################################################

MonitorInterval=60000
MonitorLogDesample=10
MemoryAlertThreshold=10
```
