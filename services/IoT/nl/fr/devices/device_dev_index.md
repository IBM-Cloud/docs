---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Développement de terminaux sur {{site.data.keyword.iot_short_notm}}
{: #device_dev_index}

Un terminal peut être n'importe quel élément doté d'une connexion à internet et qui peut envoyer des données au cloud ou en recevoir. Vous pouvez utiliser des terminaux pour envoyer des informations d'événement sous forme de relevés de capteur au cloud et pour accepter des commandes d'applications situées dans le cloud.

Les terminaux publient des données sur {{site.data.keyword.iot_short_notm}} à l'aide d'événements. Le terminal contrôle le contenu de l'événement et affecte un nom à chaque événement qu'il envoie. Lorsque {{site.data.keyword.iot_short_notm}} reçoit un événement d'un terminal, les données d'identification de la connexion sur laquelle l'événement a été reçu sont utilisées pour déterminer le terminal à partir duquel l'événement a été envoyé. Cette architecture empêche un terminal de simuler les droits d'accès d'un autre terminal.

Pour plus d'informations sur les concepts clés, y compris les terminaux, voir [Concepts importants dans Watson IoT Platform](https://console.ng.bluemix.net/docs/services/IoT/iotplatform_overview.html#watsoniotplatform_importantconcepts).


# Connexion de votre terminal à {{site.data.keyword.iot_short_notm}}
{: #device_connect}
Vous pouvez connecter votre terminal à {{site.data.keyword.iot_short_notm}} à l'aide des protocoles HTTP ou MQTT. Utilisez HTTP si vous souhaitez configurer un scénario de question-réponse, comme lorsqu'une personne effectue un achat et reçoit un accusé de réception. Utilisez MQTT si vous souhaitez configurer un scénario d'événement, comme lorsqu'une personne sonne à une porte et déclenche une alerte dans un terminal mobile.

Un terminal doit être enregistré auprès d'une organisation avant de pouvoir se connecter à {{site.data.keyword.iot_full}}. Pour établir une connexion sécurisée à {{site.data.keyword.iot_short_notm}}, vous devez vous inscrire pour obtenir un compte Bluemix et créer votre propre organisation {{site.data.keyword.iot_short_notm}}. Vous pouvez ensuite enregistrer votre terminal à l'aide de l'ID de cette organisation. Les terminaux enregistrés s'identifient eux-mêmes auprès de {{site.data.keyword.iot_short_notm}} avec un identificateur de terminal unique, par exemple, l'adresse MAC, et un jeton d'authentification qui est accepté pour ce terminal uniquement. Une fois la connexion sécurisée établie, utilisez Bluemix pour créer vos propres applications. Essayez d'utiliser Node-RED pour connecter vos applications entre elles.

Si vous souhaitez connecter votre terminal sans l'enregistrer, par exemple, pour exécuter une démonstration de faisabilité, vous pouvez utiliser l'ID d'organisation spécial `QuickStart`. `QuickStart` est une instance de bac à sable publique de {{site.data.keyword.iot_short_notm}} qui s'exécute dans le cloud. Si vous n'avez pas besoin d'établir une connexion sécurisée, vous pouvez utiliser `QuickStart` pour tester votre connectivité de terminal et l'expérimenter avec {{site.data.keyword.iot_short_notm}}. Lorsque vous avez terminé votre expérimentation, reconnectez votre terminal de manière sécurisée à votre propre instance d'ID organisation spécifique à l'aide de TLS et de votre jeton d'authentification.

Pour plus d'informations sur la connexion de votre terminal à {{site.data.keyword.iot_short_notm}} à l'aide du protocole HTTP, voir [API REST HTTP pour les terminaux](https://console.ng.bluemix.net/docs/services/IoT/devices/api.html).
Pour plus d'informations sur la connexion de votre terminal à {{site.data.keyword.iot_short_notm}} à l'aide du protocole MQTT, voir [Connectivité MQTT pour les terminaux](https://console.ng.bluemix.net/docs/services/IoT/devices/mqtt.html).

# Initiation au développement de terminaux
{: #get_started}
Si vous possédez un terminal déjà activé pour {{site.data.keyword.iot_short_notm}}, vous pouvez commencer à l'utiliser.

Si votre terminal n'est pas activé, consultez les recettes disponibles sur [developerWorks](https://developer.ibm.com/recipes/). Parcourez les recettes existantes pour voir s'il en existe une pour votre terminal, et utilisez cette recette pour vous aider à commencer à développer. Vous pouvez même publier vos propres recettes si vous le souhaitez.

Si vous ne trouvez pas de recette pour votre terminal, IBM fournit un certain nombres de guides et d'API de programmation qui vous aideront à démarrer. Ces guides contiennent des bibliothèques client, des exemples et des informations dont vous pouvez vous servir pour générer et développer du code afin d'intégrer et de connecter vos terminaux et vos applications à {{site.data.keyword.iot_short_notm}}. Les guides de programmation suivants sont disponibles :

- Java
- Node.js
- Embedded C
- ARM mBed C++
- Python
- C#
- Node-RED

Pour plus d'informations et pour accéder à des liens vers les guides de programmation disponibles, voir [Bibliothèques client pour le développement {{site.data.keyword.iot_short_notm}}](../iot_platform_client_lib.html).

Si vous ne trouvez pas le guide de programmation {{site.data.keyword.iot_short_notm}} qui vous convient, vous pouvez écrire votre propre programme et utiliser le protocole MQTT ou HTTP pour connecter votre terminal à {{site.data.keyword.iot_short_notm}}.

MQTT est une norme ouverte gérée par les normes OASIS reconnues par l'ISO. Pour plus d'informations, voir[OASIS Message Queuing Telemetry Transport ![Icône de lien externe](../../../icons/launch-glyph.svg "External link icon")](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=mqtt){: new_window}.

Une grande variété de bibliothèques client MQTT est disponible pour de nombreux systèmes, y compris les environnements suivants :
- http://www.eclipse.org/paho/
- https://github.com/mqtt/mqtt.github.io/wiki/software?id=software

Pour plus d'informations sur MQTT, voir [Messagerie MQTT](https://console.ng.bluemix.net/docs/services/IoT/reference/mqtt/index.html?pos=3).
