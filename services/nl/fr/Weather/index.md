---

Copyright :
  Années : 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Premiers pas avec Insights for Weather
{: #insights_weather_overview}

*Dernière mise à jour : 6 avril 2016*

A l'aide d'{{site.data.keyword.weatherfull}}, incorporez les données météorologiques de The Weather Company (TWC) à vos applications {{site.data.keyword.Bluemix}}.
{:shortdesc}

Les instructions suivantes vous guident dans le processus de création d'une application, de liaison de l'application au service Insights for Weather et d'extraction des données d'identification du service en vue de l'interaction avec les [API REST](https://twcservice.{APPDomain}/rest-api/).

### Création d'une application
{: #create_an_app}

Pour les besoins de la démonstration, vous allez créer une application à l'aide du contexte d'exécution
Liberty for Java, mais la procédure générale s'applique à d'autres environnements. 

1. Si vous n'avez pas d'application existante, dans le tableau de bord, cliquez sur **Créer une appli**.
2. Lorsque vous êtes invité à choisir votre modèle d'appli, cliquez sur **Web**.
3. Lorsque vous êtes invité à choisir un environnement de départ, cliquez sur **Liberty for Java**.
4. Cliquez sur **Continue**.
5. Dans la zone **Nom de l'appli**, entrez le nom de votre appli.
6. Cliquez sur **Terminer**. Attendez que votre application soit mise à disposition.

### Ajout du service Insights for Weather
{: #add_insights_for_weather_service}

Suivez les étapes ci-après pour ajouter le service Insights for Weather à votre application.
1. Ouvrez le menu **Catalogue**.
2. Dans la section **Données & analyse**, cliquez sur la vignette **Insights for Weather**. 
3. Dans la liste déroulante **Appli**, sélectionnez votre appli.
4. Cliquez sur **Utiliser**.
5. Lorsque vous y êtes invité, cliquez sur **Reconstituer** pour redémarrer votre application.

### Extraction des données d'identification d'Insights for Weather
{: #retrieve_weather_credentials}

Lorsque vous liez votre application à Insights for Weather, vous fournissez des données d'identification uniques à une instance du service. Ces données d'identification sont stockées dans l'entrée `VCAP_SERVICES` de l'application et sont indispensables pour la prise en charge de l'interaction entre les services. 

1. Accédez à la page des propriétés de votre application.
2. Accédez à la section **Variables d'environnement**. Les informations `VCAP_SERVICES` pour chacun de vos services s'affichent. 
3. Notez le nom d'utilisateur (username) et le mot de passe (password) du service Insights for Weather.
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

# rellinks
## samples
* [Insights for Weather demo](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [What's the weather like in Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## api
* [REST API](https://twcservice.{APPDomain}/rest-api/){: new_window}

## compatible runtimes {:id="buildpacks"}
* [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## general
* [A propos d'Insights for Weather](https://console.{DomainName}/docs/services/Weather/weather_overview.html){: new_window}
* [Ajout d'un service à votre application](https://console.{DomainName}/docs/services/reqnsi.html#add_service){: new_window}
* [Développement de bout en bout](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}}Fiche des prix](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}}Prérequis](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
