---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connexion d'application

Pour connecter votre application à {{site.data.keyword.iot_full}}, vous devez utiliser des clés d'API et des jetons ou lier votre application directement à {{site.data.keyword.iot_short_notm}} dans {{site.data.keyword.Bluemix_notm}}. Pour accorder des droits d'accès, utilisez le tableau de bord des accès.
{:shortdesc}

## Connexion à l'aide d'une clé d'API
{: #api-key}
Les clés d'API vous permettent de connecter des applications à votre organisation {{site.data.keyword.iot_short_notm}}. Les applications requièrent une clé d'API pour se connecter à une organisation, ainsi qu'un jeton d'authentification unique qui doit être utilisé avec cette clé d'API.  

Pour plus d'informations sur les connexions d'application, voir [MQTT Connectivity for Applications ![](../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/applications/mqtt.html){: new_window} dans la documentation du développeur. 

Pour créer une paire clé d'API/jeton d'authentification :  
1.	Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, accédez à **Applications > Clés d'API**.  
2.	Cliquez sur **Générer une clé d'API**.  
**Important :** Prenez note de la paire clé d'API/jeton d'authentification. Les jetons d'authentification ne peuvent pas être récupérés. Si vous perdez ou oubliez ce jeton, vous devrez réenregistrer la clé d'API afin de générer un nouveau jeton d'authentification.
 - `a-organization_id-a84ps90Ajs` est un exemple de clé d'API  
 - `MP$08VKz!8rXwnR-Q*` est un exemple de jeton  
3.	Ajoutez un commentaire permettant d'identifier la clé d'API dans le tableau de bord, par exemple, Clé utilisée pour connecter mon application.
4.	Cliquez sur **Terminer**.



## Connexion via une liaison dans Bluemix
{: #bluemix-binding}
Vous pouvez lier des applications à votre organisation {{site.data.keyword.iot_short_notm}} à partir de {{site.data.keyword.Bluemix_notm}}. Lorsque vous liez l'application, celle-ci peut uniquement communiquer avec les instances de service figurant dans le même espace ou la même organisation. Toutes les données nécessaires à l'application pour communiquer avec l'instance de service se trouvent dans la variable d'environnement VCAP_SERVICES. Si votre application est liée à plusieurs services, la variable VCAP_SERVICES inclut les informations de connexion pour chaque instance de service.  

Toutefois, vous pouvez utiliser des instances de service provenant d'autres espaces ou d'autres organisations, à l'instar d'une application externe. Au lieu de créer une liaison, utilisez les données d'identification afin de configurer directement votre instance d'application. Pour plus d'informations, voir [Demande d'une nouvelle instance de service](https://console.{DomainName}/docs/services/reqnsi.html#req_instance) dans la documentation {{site.data.keyword.Bluemix_notm}}.

Pour voir les détails relatifs aux applications Bluemix qui sont liées à l'instance de service Bluemix associée à votre organisation, accédez à **Applications > Applications Bluemix**.  
