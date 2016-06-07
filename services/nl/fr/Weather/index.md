---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Premiers pas avec Insights for Weather
{: #insights_weather_overview}

*Dernière mise à jour : 19 mai 2016*

A l'aide d'{{site.data.keyword.weatherfull}}, incorporez les données météorologiques de The Weather Company (TWC) à vos applications {{site.data.keyword.Bluemix}}.
{:shortdesc}

**Remarque :** Le service Insights for Weather n'est actuellement pas disponible pour le Japon.

Avant de commencer, créez une application Web {{site.data.keyword.Bluemix_notm}} dans le tableau de bord avec un environnement d'exécution tel que Liberty for Java. Attendez que votre application soit mise à disposition, puis ajoutez le service Insights for Weather à votre application.

Lorsque vous liez votre application à Insights for Weather, vous fournissez des données d'identification uniques à une instance du service. Votre application utilise ces données d'identification avec les [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window} pour extraire des données météorologiques.

Procédez comme suit pour extraire les données d'identification de `VCAP_SERVICES` et intégrer l'instance du service à votre application.

1. Accédez à la page des propriétés de votre application.
2. Accédez à la section **Variables d'environnement**. Les informations `VCAP_SERVICES` pour chacun de vos services s'affichent.
3. Notez le nom d'utilisateur et le mot de passe du service Insights for Weather.
Pour essayer les [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window}, vous devez entrer ces données d'identification lorsque vous êtes invité à vous connecter.
Votre entrée `VCAP_SERVICES` est semblable à l'exemple suivant :

```
{
   "weatherinsights": [
     {
      "name": "Insights for Weather",
      "label": "weatherinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "twcservice.mybluemix.net",
         "password": "7abcxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }
   ]
}
```

**Remarque :** Chaque région est indépendante. Vous ne pouvez pas utiliser les données d'identification qui vous ont été fournies pour le service dans une région pour vous authentifier auprès d'un service d'une autre région.
Si vous n'indiquez pas les données d'identification valides, un message "Unauthorized" (Non autorisé) est généré dans le corps de réponse. 

# rellinks
{: #rellinks}
## samples
{: #samples}
* [Insights for Weather demo](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [What's the weather like in Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## api
{: #api}
* [REST API](https://twcservice.{APPDomain}/rest-api/){: new_window}

## compatible runtimes
{: #buildpacks}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## general
{: #general}
* [Ajout d'un service à votre application](../reqnsi.html){: new_window}
* [Développement de bout en bout](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}}Fiche des prix](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}}Prérequis](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
