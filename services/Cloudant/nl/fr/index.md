---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à Cloudant
{: #getting-started-with-cloudant}
Dernière mise à jour : 12 août 2016
{: .last-updated}

{{site.data.keyword.cloudant}} est une base de données DBaaS (Document DataBase as a Service) qui stocke des données au format JSON.
Elle a été conçue afin d'être évolutive, hautement disponible et durable.
Elle est fournie avec un large éventail d'options d'indexation telles que map-reduce, Cloudant Query, la recherche en texte intégral et le traitement des données géospatiales.
Ses fonctions de réplication facilitent la synchronisation des données entre les clusters de base de données, les ordinateurs de bureau et les périphériques
mobiles.
{:shortdesc}

Vous pouvez lancer la console {{site.data.keyword.cloudant}} depuis la page de lancement du service sur le tableau de bord Bluemix.

Pour utiliser ce service, procédez comme suit :
<ol>
<li>Créez une instance de service en utilisant le tableau de bord Bluemix ou l'interface de ligne de commande CloudFoundry.
<p>Pour créer une instance en utilisant le tableau de bord, procédez comme suit :
<ol>
<li>Connectez-vous à Bluemix.</li>
<li>Sur le tableau de bord, cliquez sur le lien '<code>Utilisation des données</code>' du panneau Données et analyse.</li>
<li>Cliquez sur le bouton '<code>Nouveau service</code>'.</li>
<li>Dans la liste des services,
cliquez sur le bouton {{site.data.keyword.cloudant}}.</li>
<li>Sur la page d'informations {{site.data.keyword.cloudant}}, cliquez sur le bouton permettant de <code>choisir {{site.data.keyword.cloudant}}</code>'.</li>
<li>Sur la page de catalogue {{site.data.keyword.cloudant}}, renseignez les détails pour le service dont vous avez besoin.
Cliquez sur le bouton '<code>Créer</code>' quand vous êtes prêt à poursuivre.</li>
<li>Quand l'instance Cloudant a été créée, le tableau de bord associé à cette instance vous est proposé.
Cliquez sur le lien '<code>Données d'identification pour le service</code>' pour afficher tous les détails nécessaires pour accéder à votre instance.</li>
</ol>
</p>
<p>Pour créer une instance en utilisant l'interface de ligne de commande CloudFoundry, procédez comme suit :
<ol>
<li>Installez l'outil CloudFoundry <code>cf</code> sur votre système.
Des instructions sur la façon de procéder sont disponibles dans le guide <a href="https://console.ng.bluemix.net/docs/cli/index.html">Bluemix
Interface de ligne de commande et outils de développement</a>.</li>
<li>Créer une nouvelle instance de service en utilisant la commande <br/>
<pre><code>cf create-service</code></pre></li>
<li>Une liste des services disponibles s'affiche.
Choisissez-en un puis entrez un nom d'instance unique et planifiez le service.
Un nom aléatoire est suggéré pour l'instance mais vous pouvez le modifier, si vous préférez.</li>
<li>Une fois le service créé, vous pouvez obtenir une liste de tous les services que vous avez créés :<br/>
<pre><code>cf services</code></pre></li>
<li>Avant d'utiliser un service dans une application, vous devez lier le service à votre application.
Pour ce faire, utilisez la commande :<br/>
<pre><code>cf bind-service</code></pre>
Dans la liste résultante, sélectionnez l'une des applications et l'un des services.
La commande <code>cf</code> vous prévient quand l'action de liaison a été exécutée.</li>
</ol>
</p>
</li>
<li><p>Une fois que vous avez créé une instance de service, des données JSON similaires aux suivantes apparaissent et peuvent être consultées dans le
tableau de bord Bluemix :<br/>
<pre><code>{
  "cloudantNoSQLDB": {
    "name": "Cloudant-3s",
    "label": "cloudantNoSQLDB",
    "plan": "shared",
    "credentials": {
      "username": "nom-utilisateur",
      "password": "mot-de-passe",
      "host": "myhost-bluemix.cloudant.com",
      "port": 443,
      "url": "https://nom-utilisateur:mot-de-passe@myhost-bluemix.cloudant.com"
    }
  }
}</code></pre></p>
{: screen}
<p>Les données sont également ajoutées à la variable d'environnement <code>VCAP_SERVICES</code> de toute application Bluemix à laquelle le service
est lié.</p>
<p>Les données d'identification du service sont stockées dans un objet JSON contenant les zones suivantes :
<ul>
<li><code>key</code> : nom du service (cloudantNoSQLDB)</li>
<li><code>name</code> : nom fourni par l'utilisateur de l'instance de service</li>
<li><code>host</code> : nom d'hôte du serveur</li>
<li><code>port</code> : numéro de port sur lequel le service s'exécute, généralement 443</li>
<li><code>username</code> : nom d'utilisateur pour l'authentification</li>
<li><code>password</code> : mot de passe pour l'authentification</li>
<li><code>url</code> : adresse URL de l'instance de service</li>
</ul></li>
<li><p>Dans vos applications Bluemix, lisez les données d'identification depuis la variable d'environnement <code>VCAP_SERVICES</code>.</p>
<p>Dans les applications qui s'exécutent hors de Bluemix ou dans une région géographique différente au sein de Bluemix,
vous pouvez extraire les données d'identification depuis le tableau de bord Bluemix et les ajouter à la configuration de votre application.</p>
</li>
<li>Pour accéder à la base de données, le mécanisme de base consiste à envoyer des demandes à l'hôte et au port donnés via HTTPS, en indiquant le nom d'utilisateur et le mot
de
passe pour l'authentification.
Vos demandes peuvent être envoyées via une large gamme de langages d'application et de plateformes, incluant :
<ul>
<li><a href="https://github.com/cloudant/sync-android">Android</a></li>
<li><a href="https://github.com/cloudant/CDTDatastore">Apple iOS</a></li>
<li><a href="https://github.com/cloudant/java-cloudant">Java</a></li>
<li><a href="https://github.com/cloudant/objective-cloudant">Objective C et Swift</a></li>
<li><a href="https://github.com/cloudant/python-cloudant">Python</a></li>
</ul>
... et bien d'autres encore.
Pour plus d'informations, voir la page d'accueil <a href="https://cloudant.com/for-developers/">destinée aux développeurs Cloudant</a>
et la liste des <a href="http://docs.cloudant.com/libraries.html">bibliothèques client</a>.
</li>
<li>Quand votre application est prête, vous pouvez la déployer dans votre environnement Bluemix pour vérification.
Pour déployer une application, utilisez la commande : <br/>
<pre><code>cf push</code></pre></li>
<li>Pour supprimer la liaison d'une instance de service d'une application, utilisez la commande : <br/>
<pre><code>cf unbind-service</code></pre></li>
<li>Pour supprimer une instance de service, utilisez la commande : <br/>
<pre><code>cf delete-service</code></pre></li>
</ol>

Des informations supplémentaires sur l'authentification auprès de la base de données et l'envoi de demandes sont
disponibles dans la [référence d'API](https://docs.cloudant.com/api.html).

# Liens connexes
{: #rellinks}

## Tutoriels et exemples
{: #samples}

* [Bibliothèques client Cloudant](https://docs.cloudant.com/libraries.html)
* [Utilisation de Cloudant avec Liberty dans Bluemix](https://developer.ibm.com/bluemix/2014/07/08/cloudant_on_bluemix/)
* [Guides Cloudant](https://docs.cloudant.com/guides.html)

## Référence d'API
{: #api}

* [Référence d'API Cloudant](https://docs.cloudant.com/api.html)

## Liens connexes
{: #general}

* [Site Web et tableau de bord Cloudant](https://cloudant.com/)
* [Blogue Cloudant](https://cloudant.com/blog)
