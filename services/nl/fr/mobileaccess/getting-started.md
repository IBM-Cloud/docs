---

Copyright : 2015, 2016

---

# Initiation
{: #getting-started}
Pour commencer à utiliser {{site.data.keyword.amashort}}, vous pouvez soit ajouter le service {{site.data.keyword.amashort}} à une application {{site.data.keyword.Bluemix}} existante, soit créer une nouvelle appli avec le conteneur boilerplate.  

## Création d'une instance du service {{site.data.keyword.amashort}}
{: #service-instance}

Vous pouvez créer une instance d'un service {{site.data.keyword.amashort}} à partir du catalogue {{site.data.keyword.Bluemix}}.  Si vous n'utilisez pas le conteneur boilerplate pour créer un nouveau système de back end mobile, vous devez configurer le SDK serveur sur votre système de back end existant.


  * **Nouvelle appli** : Les instructions des sections suivantes décrivent la création d'une nouvelle appli qui génère un système de back end mobile et le protège avec le SDK serveur de {{site.data.keyword.amashort}}. Cliquez sur le conteneur boilerplate **MobileFirst Services Starter** pour créer une application avec le service {{site.data.keyword.amashort}}.
  * **Appli existante** : Cliquez sur l'icône {{site.data.keyword.amashort}} et créez une instance du service qui soit liée à une application existante. Pour configurer le SDK serveur sur votre appli existante, voir [Protection des ressources de cloud](protecting-resources.html).


## Création d'un système de back end mobile dans le mobile MobileFirst Services Starter
{: #create-backend}
Lorsque vous utilisez MobileFirst Services Starter, vous obtenez une instance du contexte d'exécution Node.js
qui s'exécute sur IBM {{site.data.keyword.Bluemix_notm}} pour implémenter votre logique de back end personnalisée. Un ensemble de services mobiles de base qui fournissent des fonctions de sécurité, de données, d'envoi par commande push et de surveillance est lié à cette application
Node.js. Une fois l'application {{site.data.keyword.Bluemix_notm}} Node.js créée, vous pouvez configurer votre environnement de développement
et commencer à utiliser les logiciels SDK de {{site.data.keyword.Bluemix_notm}} Mobile Services. Vous pouvez utiliser les logiciels SDK pour accéder aux services qui sont liés à votre application en cloud à l'aide de simples appels d'API.

1. Dans le catalogue {{site.data.keyword.Bluemix_notm}}, ouvrez la section **Conteneurs boilerplate** et cliquez sur **MobileFirst Services Starter**.
1. Entrez des informations sur votre système de back end mobile, y compris l'espace, le nom, l'hôte et le plan du service.
1. Cliquez sur **CREER**.



## Etapes suivantes
{: #next-steps}
Plusieurs noeuds finaux de l'application Node.js que vous avez créée avec le conteneur boilerplate sont protégées avec {{site.data.keyword.amashort}}. Pour en savoir plus sur l'application de back end mobile par défaut, voir  [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop).

Vous pouvez configurer l'utilisation du logiciel SDK {{site.data.keyword.amashort}} dans votre appli mobile.  Lorsque le SDK est configuré, vous pouvez commencer à configurer l'authentification et la surveillance dans votre appli.  Suivez les instructions correspondant à votre plateforme de développement d'application mobile :

* [Android](getting-started-android.html)
* [iOS (SDK Swift)](getting-started-ios.html)
* [iOS (SDK Objective-C)](getting-started-ios.html)
* [Cordova](getting-started-cordova.html)
