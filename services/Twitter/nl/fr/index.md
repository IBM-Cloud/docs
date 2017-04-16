---

copyright:
  years: 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Initiation à Insights for Twitter {: #insights_twitter_overview}

Utilisez {{site.data.keyword.twitterfull}} pour incorporer un contenu Twitter depuis les flux [Decahose](http://support.gnip.com/gnip2.0/){: new_window} ou [PowerTrack](http://support.gnip.com/apis/powertrack2.0/){: new_window} de  Twitter dans vos applications {{site.data.keyword.Bluemix}}.
{:shortdesc}

Pour commencer à utiliser {{site.data.keyword.twittershort}}, créez d'abord votre application Web Bluemix avec un contexte d'exécution Liberty for Java puis ajoutez le service {{site.data.keyword.twittershort}} à votre application. Quand le service {{site.data.keyword.twittershort}} est lié à votre application, l'instance de service est provisionnée avec des données d'identification uniques. Votre application utilise ces données d'identification avec des API REST pour rechercher et consommer du contenu Twitter.  Procédez comme suit pour extraire les données d'identification de VCAP_SERVICES et intégrer l'instance de service à votre application.

1. Accédez à la page de présentation de votre application.
2. Accédez à la section **Variables d'environnement**. Les informations `VCAP_SERVICES` pour chacun de vos services s'affichent.
3. Notez les valeurs de nom d'utilisateur et de mot de passe depuis le service {{site.data.keyword.twittershort}}. Vous aurez besoin d'entrer ces données d'identification pour tester les opérations dans la documentation de référence de l'API REST. Ainsi, vos informations `VCAP_SERVICES` ressembleront à l'extrait de code suivant :

```
{  
   "twitterinsights": [    
     {      
      "name": "IBM Insights for Twitter-x3",
      "label": "twitterinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "cdeservice.mybluemix.net",
         "password": "7cunxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }  
   ]
}
```

# rellinks
{: #rellinks}
## Exemples
{: #samples}
* [Démonstration de recherche Decahose interactive](https://cdetestapp.mybluemix.net/){: new_window}
* [developerWorks : Build a Twitter search engine with Insights for Twitter on Bluemix](http://www.ibm.com/developerworks/cloud/library/cl-twitter-search-insights-bluemix-trs/index.html){: new_window}
* [Analyzing "American Sniper" box office success with IBM Insights for Twitter &  dashDB in Bluemix (YouTube)](https://www.youtube.com/watch?v=Gfk5quglXvI){: new_window}
* [IBM-Bluemix / places-insights-lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}

## API
{: #api}
* [API REST](https://cdeservice.{APPDomain}/rest-api/){: new_window}

## Contextes d'exécution compatibles
{: #buildpacks}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Swift](https://console.{DomainName}/docs/runtimes/swift/index.html){: new_window}
* [Tomcat](https://console.{DomainName}/docs/runtimes/tomcat/index.html){: new_window}

## Généralités
{: #general}
* [Nouveautés dans les services {{site.data.keyword.Bluemix_notm}}](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){: new_window}
* [Ajout d'un service à votre application](../reqnsi.html){: new_window}
* [Développement de bout en bout](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [Fiche des prix {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){: new_window}
* [Configuration requise pour {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}

