{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Initiation à Insights for Twitter {: #insights_twitter_overview}

*Dernière mise à jour : 13 mai 2016*
{: .last-updated}

Utilisez {{site.data.keyword.twitterfull}} pour incorporer un contenu Twitter depuis les flux [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window} ou [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window} de  Twitter dans vos applications {{site.data.keyword.Bluemix}}.
{:shortdesc}

Pour commencer à utiliser {{site.data.keyword.twittershort}}, créez d'abord votre application Web Bluemix avec un contexte d'exécution Liberty for Java puis ajoutez le service {{site.data.keyword.twittershort}} à votre application. Quand le service {{site.data.keyword.twittershort}} est lié à votre application, l'instance de service est provisionnée avec des données d'identification uniques. Votre application utilise ces données d'identification avec des API REST pour rechercher et consommer du contenu Twitter. Procédez comme suit pour extraire les données d'identification de VCAP_SERVICES et intégrer l'instance de service à votre application.

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

<!--
## Adding Insights for Twitter to your application {: #adding_twitter}

The following instructions guide you through the process of creating an application, binding the application to the {{site.data.keyword.twittershort}} service, and retrieving the service credentials to interact with REST API operations in the provided API reference documentation.

### Create an application
For demonstration purposes, you'll create an application using the Liberty for Java&trade;  runtime, but the general process described below can be applied to other runtimes. If you don't have an existing application, click **CREATE AN APP** in the dashboard. When asked to confirm the type of app, click **WEB**.

1. Open the **Catalog** menu.
2. From the **Runtimes** section, click **Liberty for Java**.
3. Click **Create**.
4. In the **App Name** field, specify the name of your app.
5. Click **Finish**. Wait for your application to provision.

### Add the Insights for Twitter service
Follow these steps to add the {{site.data.keyword.twittershort}} service to your app.

1. Open the **Catalog** menu.
2. From the **Data & Analytics** section, click the {{site.data.keyword.twittershort}} tile.
3. In the **App** field, select the name of your app.
4. Click **Create**.
5. When prompted, click **Restage** to restart your application.
-->

# rellinks
{: #rellinks}
## Exemples
{: #samples}
* [Démonstration de recherche Decahose interactive](https://cdetestapp.mybluemix.net/){: new_window}
* [developerWorks : Build a Twitter search engine with Insights for Twitter on Bluemix](http://www.ibm.com/developerworks/cloud/library/cl-twitter-search-insights-bluemix-trs/index.html){: new_window}
* [Analyzing "American Sniper" box office success with IBM Insights for Twitter &  dashDB in Bluemix (YouTube)](https://www.youtube.com/watch?v=Gfk5quglXvI){: new_window}
* [IBM-Bluemix / places-insights-lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}

## api
{: #api}
* [API REST](https://cdeservice.{APPDomain}/rest-api/){: new_window}

## contextes d'exécution compatibles
{: #buildpacks}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Swift](https://console.{DomainName}/docs/runtimes/swift/index.html){: new_window}
* [Tomcat](https://console.{DomainName}/docs/runtimes/tomcat/index.html){: new_window}

## généralités
{: #general}
* [Nouveautés dans les services {{site.data.keyword.Bluemix_notm}}](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){: new_window}
* [Ajout d'un service à votre application](../reqnsi.html){: new_window}
* [Développement de bout en bout](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [Fiche des prix {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){: new_window}
* [Configuration requise pour {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}

