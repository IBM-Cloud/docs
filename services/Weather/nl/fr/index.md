---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Initiation à {{site.data.keyword.weather_short}}
{: #insights_weather_overview}

A l'aide d'{{site.data.keyword.weatherfull}}, incorporez les données météorologiques de The Weather Company (TWC) à vos applications {{site.data.keyword.Bluemix}}.
{:shortdesc}

**Attention :** Actuellement, il est **impossible** d'acheter ou d'utiliser le service {{site.data.keyword.weather_short}} dans les régions ou pays suivants : Afghanistan, Arménie, Azerbaïdjan, Bahreïn, Bangladesh, Bhoutan, Brunei, Cambodge, Chine, Chypre, Géorgie, Indonésie, Iran, Irak, Japon, Jordanie, Kazakhstan, Koweït, Kirghizistan, Laos, Liban, Malaisie, Maldives, Mongolie, Birmanie, Népal, Oman, Pakistan, Philippines,
Qatar, Russie, Arabie Saoudite, Singapour, Corée du Sud, Sri Lanka, Syrie, Tadjikistan, Timor-Leste, Turquie, Turkménistan, Émirats arabes unis, Ouzbékistan, Vietnam, Yémen. Cette liste est mise à jour lorsque des informations supplémentaires sont disponibles.

Si vous possédez déjà une application qui utilise le service [Insights for Weather](https://console.{DomainName}/docs/services/InsightsWeather/index.html){: new_window}, elle continuera de fonctionner sans aucune modification pendant une période de 90 jours après l'introduction d'{{site.data.keyword.weather_short}}. Pour bénéficier des nouvelles API et du modèle de tarification amélioré, vous pouvez faire migrer votre application vers le nouveau service.


Avant de commencer, créez une application Web {{site.data.keyword.Bluemix_notm}} dans le tableau de bord avec un environnement d'exécution tel que Liberty for Java. Attendez que votre application soit mise à disposition, puis ajoutez le service {{site.data.keyword.weather_short}} à cette dernière.

Lorsque vous liez votre application à {{site.data.keyword.weather_short}}, vous mettez à disposition des données d'identification uniques pour une instance du service. Votre application utilise ces données d'identification avec les [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window} pour extraire des données météorologiques.

Procédez comme suit pour extraire les données d'identification de `VCAP_SERVICES` et intégrer l'instance du service à votre application.

1. Accédez à la page des propriétés de votre application.
2. Accédez à la section **Variables d'environnement**. Les informations `VCAP_SERVICES` pour chacun de vos services s'affichent.
3. Notez le nom d'utilisateur et le mot de passe du service {{site.data.keyword.weather_short}}.
Pour essayer les [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window}, vous devez entrer ces données d'identification lorsque vous êtes invité à vous connecter.
Votre entrée `VCAP_SERVICES` est semblable à l'exemple suivant :

```
{
{
   "weatherinsights": [
      {
         "name": "Weather Company Data for IBM Bluemix",
         "label": "weatherinsights",
         "plan": "Free",
         "credentials": {
            "username": "d40845df-8125-441f-8e7c-e650726ce721",
            "password": "tDV0HGZz3O",
            "host": "twcservice.mybluemix.net",
            "port": 443,
            "url": "https://d40845df-8125-441f-8e7c-e650726ce721:tDV0HGZz3O@twcservice.mybluemix.net"
         }
      }
   ]
}
```

**Remarque :** Chaque région est indépendante. Vous ne pouvez pas utiliser les données d'identification qui vous ont été fournies pour le service dans une région pour vous authentifier auprès d'un service d'une autre région.
Si vous n'indiquez pas les données d'identification valides, un message *Unauthorized* (Non autorisé) est généré dans le corps de réponse.

# rellinks
{: #rellinks}
## samples
{: #samples}
* [Application de démonstration d'{{site.data.keyword.weather_short}}](http://weather-company-data-demo.{APPDomain}){: new_window}
* [Vidéo d'analyse approfondie d'{{site.data.keyword.weather_short}}](https://youtu.be/pZHXIibziUo){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [Exemple d'application {{site.data.keyword.Bluemix_notm}} + Weather](https://github.com/IBM-Bluemix/insights-weather){: new_window}
* [IBM Cloud - Serveurs non virtualisés, données des taxis New-Yorkais et Insights for Weather (tutoriel YouTube)](https://www.youtube.com/watch?v=Uwmzpx9DZ5c){: new_window}

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
* [Ajout d'un service à votre application](/docs/services/reqnsi.html){: new_window}
* [Développement de bout en bout](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}}Fiche des prix](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}}Prérequis](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
