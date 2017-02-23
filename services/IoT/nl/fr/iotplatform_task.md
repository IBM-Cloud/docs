---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connexion de terminaux
{: #iotplatform_task}

Avant de pouvoir commencer à recevoir des données depuis vos terminaux IoT, vous devez les connecter à {{site.data.keyword.iot_full}}. Connecter un terminal à {{site.data.keyword.iot_short_notm}} implique de l'enregistrer auprès de {{site.data.keyword.iot_short_notm}} et d'utiliser les informations d'enregistrement pour configurer le terminal afin qu'il se connecte à {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Avant de commencer
{: #byb}

Avant de commencer le processus de connexion, vous devez vous assurer que vos terminaux sont conformes aux exigences suivantes relatives à la communication avec {{site.data.keyword.iot_short_notm}} :

- Votre terminal doit pouvoir communiquer à l'aide des protocoles HTTP ou MQTT. 
- Les messages de terminal doivent être conformes aux exigences de contenu de message de {{site.data.keyword.iot_short_notm}}. 

Pour plus d'informations, voir [Développement de terminaux sur Watson IoT Platform](https://console.ng.bluemix.net/docs/services/IoT/devices/device_dev_index.html).

Pour connecter votre terminal à {{site.data.keyword.iot_short_notm}}, procédez comme suit :

## Etape 1 : Enregistrement de votre terminal auprès de {{site.data.keyword.iot_short_notm}}  
{: #iotplatform_subtask1}

Enregistrer un terminal implique de le classifier en tant que type de terminal, de lui donner un nom et de fournir des informations le concernant. Vous indiquez ensuite un jeton de connexion ou vous acceptez un jeton qui est généré par {{site.data.keyword.iot_short_notm}}.

Vous pouvez ajouter un seul terminal à la fois depuis le tableau de bord {{site.data.keyword.iot_short_notm}} ou vous pouvez utiliser l'[API {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Bulk_Operations/post_bulk_devices_add) pour ajouter un ou plusieurs terminaux à la fois.

Pour ajouter un terminal depuis le tableau de bord {{site.data.keyword.iot_short_notm}} :

1. Cliquez sur la vignette du service {{site.data.keyword.iot_short_notm}} dans votre tableau de bord {{site.data.keyword.Bluemix}} pour ouvrir le tableau de bord de service ou accédez directement au tableau de bord à l'aide de l'URL suivante :

 `https://org_id.internetofthings.ibmcloud.com/dashboard/#/overview `

    Où *org_id* est l'ID de votre organisation {{site.data.keyword.Bluemix}}.

2. Sur la page de service, cliquez sur **Lancer le tableau de bord** pour commencer à administrer votre organisation {{site.data.keyword.iot_short_notm}}.

3. Dans le tableau de bord Présentation, à partir du panneau de menu, sélectionnez **Terminaux**, puis cliquez sur **Ajouter un terminal**.
5. Sélectionnez ou créez un type de terminal pour le terminal que vous ajoutez.  
Chaque terminal connecté à {{site.data.keyword.iot_short_notm}} doit être associé à un type de terminal. Les types de terminal sont des groupes de terminaux ayant des caractéristiques communes.  
Lorsque vous ajoutez votre premier terminal à votre organisation {{site.data.keyword.iot_short_notm}}, aucun type de terminal n'est disponible dans le menu **Type de terminal**. Vous devez d'abord créer un type de terminal :
 1. Cliquez sur **Créer un type de terminal**.
 2. Entrez un nom de type de terminal, par exemple, `my_device_type`, et une description pour le type de terminal.   
 **Important :** Le nom du type de terminal ne doit pas dépasser 36 caractères et peut uniquement contenir les caractères suivants :
 <ul>
  <li>Caractères alphanumériques (a-z, A-Z, 0-9)</li>
  <li>Traits d'union (-)</li>
  <li>Traits de soulignement (&lowbar;)</li>
  <li>Points (.)</li>
  </ul>
 3. Facultatif : Entrez des métadonnées et des attributs de type de terminal.    
 **Astuce :** Vous pouvez ajouter et éditer des attributs et des métadonnées ultérieurement.
 4. Cliquez sur **Créer** pour ajouter le nouveau type de terminal.
10. Cliquez sur **Suivant** pour commencer le processus d'ajout de votre terminal avec le type de terminal sélectionné.
11. Entrez un ID de terminal, tel que `my_first_device`.  
L'ID de terminal permet d'identifier le terminal dans le tableau de bord {{site.data.keyword.iot_short_notm}} et représente également un paramètre requis pour la connexion de votre terminal à {{site.data.keyword.iot_short_notm}}.  
**Important :** L'ID de terminal ne doit pas dépasser 36 caractères et peut uniquement contenir les caractères suivants :
 <ul>
 <li>Caractères alphanumériques (a-z, A-Z, 0-9)</li>
 <li>Traits d'union (-)</li>
 <li>Traits de soulignement (&lowbar;)</li>
 <li>Points (.)</li>  
 </ul>
 **Astuce :** Pour les terminaux connectés à un réseau, l'ID de terminal pourrait être par exemple l'adresse MAC du terminal sans aucun deux-points de séparation.  
12. Facultatif : Cliquez sur **Zones supplémentaires** pour ajouter des informations de terminal, par exemple, le numéro de série, le fabricant, le modèle, etc.  
 **Astuce :** Vous pouvez ajouter et éditer ces informations ultérieurement.
12. Facultatif : Entrez les métadonnées JSON de terminal.  
 **Astuce :** Vous pouvez ajouter et éditer des métadonnées de terminal ultérieurement.
13. Cliquez sur **Suivant** pour finaliser l'ajout de votre terminal.
14. Vérifiez que les informations récapitulatives sont correctes, puis cliquez sur **Ajouter** pour ajouter la connexion.  
**Astuce :** Vous avez la possibilité d'accepter un jeton d'authentification généré automatiquement ou de fournir vous-même un jeton d'authentification.  
Si vous choisissez de créer votre propre jeton, celui-ci doit comporter uniquement des caractères alphanumériques et les caractères spéciaux suivants :
 - Trait d'union (-)
 - Trait de soulignement (&lowbar;)
 - Point d'exclamation (!)
 - Perluète (&)
 - Arobase (@)
 - Point d'interrogation (?)
 - Astérisque (\*)
 - Signe Plus (+)
 - Point (.)
 - Parenthèses ouvrantes et fermantes.  

 **Important :** Le jeton ne doit pas contenir des séquences de caractères répétés, des mots de dictionnaire, des noms d'utilisateur ni d'autres séquences prédéfinies.
15. Sur la page Informations sur le terminal, copiez et sauvegardez les informations de terminal suivantes :  
 - ID d'organisation, par exemple, `tubo8x`
 - Type de terminal, par exemple, `my_device_type`
 - ID de terminal, par exemple, `my_first_device`
 - Méthode d'authentification, par exemple, `token`
 - Jeton d'authentification, par exemple, `PtBVriRqIg4uh)_-Kl`  
  **Astuce :** Vous aurez besoin d'un ID d'organisation, d'un jeton d'authentification, d'un type de terminal et d'un ID de terminal pour configurer votre terminal afin qu'il se connecte à {{site.data.keyword.iot_short_notm}}.  

Félicitations, vous avez enregistré votre terminal. Vous pouvez maintenant configurer votre terminal pour qu'il se connecte à {{site.data.keyword.iot_short_notm}}.

## Etape2 : Connexion de vos terminaux à {{site.data.keyword.iot_short_notm}}
{: #iotplatform_subtask2}

Après avoir enregistré un terminal auprès de {{site.data.keyword.iot_short_notm}}, vous pouvez utiliser les informations d'enregistrement pour connecter le terminal et commencer à recevoir des données de terminal.

{{site.data.keyword.iot_short_notm}} prend en charge un grand nombre de types de terminal. Le processus de base permettant de connecter un terminal inclut généralement les étapes suivantes :
- Configurer votre terminal pour la messagerie MQTT et utiliser l'ID d'organisation, le jeton d'authentification, le type de terminal et l'ID de terminal pour l'authentification.  
- Envoyer des messages de terminal à votre organisation {{site.data.keyword.iot_short_notm}} à l'aide du protocole MQTT.

**Astuce :** Un grand nombre de recettes de connexion sont disponibles pour les terminaux couramment utilisés. Pour obtenir une liste de recettes, voir les [recettes de connexion de terminal](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/) disponibles sur IBM.com.

Les informations suivantes sont requises lors de la connexion de votre terminal :
- URL : *org_id*.messaging.internetofthings.ibmcloud.com  
Où *org_id* est l'ID de votre organisation {{site.data.keyword.iot_short_notm}}.
- Port :
 - 1883
 - 8883 (chiffré)
 - 443 (websockets)
- Identificateur de terminal : d:*org_id*:*device_type*:*device_id*  
Cette combinaison de paramètres identifie votre terminal de manière unique.
- Nom d'utilisateur : use-token-auth  
Cette valeur indique que vous utilisez l'autorisation à base de jeton. 
- Mot de passe : *Authentication token*  
Cette valeur est le jeton unique que vous avez défini ou qui a été affecté à votre terminal lorsque vous l'avez enregistré.
- Format de sujet d'événement : iot-2/evt/*event_id*/fmt/*format_string*  
 Où *event_id* spécifie le nom d'événement affiché dans {{site.data.keyword.iot_short_notm}} et *format_string* est le format de l'événement, par exemple, JSON.
- Format de message : JSON
   
 {{site.data.keyword.iot_short_notm}} prend en charge plusieurs formats, tels que JSON et texte.

Pour plus d'informations sur la connexion de votre terminal, voir [Connectivité MQTT pour les terminaux](devices/mqtt.html) dans la documentation technique.
La section [Connectivité](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Connectivity/post_device_types_deviceType_devices_deviceId_events_eventName) de la documentation d'API contient également les informations requises.

## Recettes relatives à la connexion de terminaux

Les recettes suivantes décrivent le flux complet utilisé pour enregistrer et connecter des terminaux à Watson IoT Platform.

- [How to Register Devices in IBM Watson IoT Platform](https://developer.ibm.com/recipes/tutorials/how-to-register-devices-in-ibm-iot-foundation/)

- [Connecting Raspberry Pi as a Device to Watson IoT using Node-RED](https://developer.ibm.com/recipes/tutorials/deploy-watson-iot-node-on-raspberry-pi/)

- [Connect an Arduino Uno device to the IBM Watson IoT Platform](https://developer.ibm.com/recipes/tutorials/connect-an-arduino-uno-device-to-the-ibm-internet-of-things-foundation/)

- [Connecting a Sense HAT to Watson IoT using Node-RED](https://developer.ibm.com/recipes/tutorials/connecting-a-sense-hat-to-watson-iot-using-node-red/)

- [Connecting Raspberry Pi with Windows IoT Core as a Device to Watson IoT Platform](https://developer.ibm.com/recipes/tutorials/connecting-raspberry-pi-with-windows-iot-core-as-a-device-to-watson-iot-using-node-red/)
