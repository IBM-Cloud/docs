---

 

copyright:

  2015，2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Scénario : Développement de bout en bout
{: #ee}

*Dernière mise à jour : 18 avril 2016*

La plateforme et l'interface utilisateur {{site.data.keyword.Bluemix}}, ainsi qu'une sélection d'outils associés,
vous permettent de construire, exécuter et déployer vos applications. Suivez ce scénario de développement de bout en bout pour
commencer.
{:shortdesc}

## Inscription
{: #ee_start}

Avant de commencer, vous vous inscrivez pour obtenir un ID IBM sur
[https://console.ng.bluemix.net/](https://console.ng.bluemix.net/). Ensuite, vous vous connectez à {{site.data.keyword.Bluemix_notm}} et commencez votre essai gratuit de 30 jours. {{site.data.keyword.Bluemix_notm}} fournit une franchise de 2 Go de mémoire d'exécution et 10 instances de
service dans le cadre de votre essai gratuit.

## Création de votre application Web via l'interface utilisateur {{site.data.keyword.Bluemix_notm}}
{: #ee_appui}

Une fois que vous êtes inscrit, vous commencez à construire votre première application à l'aide de l'interface utilisateur
{{site.data.keyword.Bluemix_notm}}.

Dans {{site.data.keyword.Bluemix_notm}}, les applications sont associées à des organisations et des espaces. Une
organisation appartient à plusieurs collaborateurs et est utilisée par plusieurs collaborateurs. Au départ, vous obtenez une organisation par défaut
dont le nom dépend de votre nom d'utilisateur, et dont vous êtes le seul collaborateur. Vous obtenez également un espace dans cette organisation. L'espace est un environnement dans lequel vous pouvez exécuter vos applications. Par exemple, vous pouvez disposer d'un espace de développement comme
environnement de développement, d'un espace de test comme environnement de test et d'un espace de production comme environnement de production. De plus, chaque
environnement appartient à une région. Avec {{site.data.keyword.Bluemix_notm}}, vous pouvez déployer vos
applications dans une région géographique spécifique pour un temps d'attente des réseaux plus court, la confidentialité des données et une meilleure
disponibilité. Voir Régions pour des détails.

Dans ce scénario, vous allez développer une application Web avec Node.js. Supposez que vous vous trouvez aux Etats-Unis et que la majorité des
utilisateurs de votre application se situent également aux Etats-Unis. Vous décidez de construire et d'exécuter votre application près de votre base
utilisateur pour pouvoir bénéficier d'un temps d'attente des réseaux plus court. Une fois connecté à {{site.data.keyword.Bluemix_notm}}, cliquez
sur le nom de votre compte dans le coin supérieur droit et sélectionnez la région **Sud des Etats-Unis**. Ensuite, procédez comme suit pour créer une application :

  1. Cliquez sur le bouton plus. 
  2. Sélectionnez **Calcul**>**Applications CF**>**SDK for Node.js**.
  3. Entrez un nom unique pour votre application, par exemple TestNode, et cliquez sur **Créer**. Le nom de
l'application doit être unique dans l'ensemble de l'environnement {{site.data.keyword.Bluemix_notm}}.
  
A présent, vous pouvez lire les instructions **Commencer le codage**. Vous pouvez suivre les instructions de téléchargement, de
modification et de déploiement du code de démarrage de TestNode.

L'application est affectée à une instance et à un quota de mémoire de 512 Mo par défaut. Vous pouvez augmenter la mémoire ou ajouter d'autres instances
pour assurer la haute disponibilité de votre application, avec par exemple trois instances et 1 Go de mémoire par instance. Cliquez sur **Afficher
la vue d'ensemble de l'application** pour spécifier vos instances d'application et votre quota de mémoire. Par exemple, entrez 3 pour les
instances et 1 Go pour le quota de mémoire, puis cliquez sur **Sauvegarder**. Vous pouvez aussi afficher les fichiers, les journaux et
les variables d'environnement afin de traiter les problèmes.

## Liaison d'un service via l'interface utilisateur {{site.data.keyword.Bluemix_notm}}
{: #ee_bindui}

Une fois votre application créée, vous devez vous connecter à une base de données avec l'application. Ainsi, vous pouvez stocker et examiner les
données d'application en utilisant le langage de requête de base de données. Dans le cadre de ce scénario, vous décidez d'utiliser le service
{{site.data.keyword.cloudant}} mis à disposition par {{site.data.keyword.Bluemix_notm}}.

Pour utiliser des services dans l'application, vous devez créer une instance de service et lier votre application à l'instance de service en
procédant comme suit :
  1. Cliquez sur **Ajouter un service ou une API** dans la page Vue d'ensemble de l'application.
  2. Dans le catalogue {{site.data.keyword.Bluemix_notm}}, sélectionnez le service {{site.data.keyword.cloudant}}.
  3. Entrez un nom unique pour l'instance de service ou utilisez le nom par défaut qui est généré par
{{site.data.keyword.Bluemix_notm}}, puis cliquez sur **Créer**.
  4. La fenêtre Reconstitution de l'application s'ouvre. Cliquez sur **Reconstituer** pour reconstituer votre application.
  
A présent, votre application est liée au service {{site.data.keyword.cloudant}}. Toutes les données nécessaires à l'application pour
communiquer avec l'instance de service se trouvent dans la variable d'environnement VCAP_SERVICES. Ainsi,
{{site.data.keyword.Bluemix_notm}} hébergeant plusieurs applications sur la même machine virtuelle, les applications ne peuvent pas utiliser le même numéro de port HTTP pour recevoir les demandes entrantes. Pour éviter tout conflit, un numéro de port unique est affecté à chaque application. Ce numéro de port est disponible dans la variable VCAP_APP_PORT.

Pour plus d'informations, cliquez sur **Variables d'environnement** dans la page Vue d'ensemble de l'application afin d'afficher la
liste complète de
VCAP_SERVICES :
```
{
   "cloudantNoSQLDB": [
      {
         "name": "Cloudant NoSQL DB-tx",
         "label": "cloudantNoSQLDB",
         "plan": "Partagé",
         "credentials": {
            "username": "d72837bb-b341-4038-9c8e-7f7232916197-bluemix",
            "password": "b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424",
            "host": "d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com",
            "port": 443,
            "url": "https://d72837bb-b341-4038-9c8e-7f7232916197-bluemix:b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424@d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com"
         }
      }
   ]
}
```

**Remarque :** cette variable d'environnement est la sérialisation d'un objet JSON avec une entrée pour chaque instance de
service à laquelle l'application est
liée. La quantité et le type des données fournies par chaque instance de service varient en fonction du service. Si votre application n'utilise pas de
service, VCAP_SERVICES est un objet JSON vide. Cette variable d'environnement est utilisée uniquement lorsque vous
ajoutez un service à votre application.

## Construction de votre application via l'interface de ligne de commande cf
{: #ee_cf}

{{site.data.keyword.Bluemix_notm}} met à disposition plusieurs outils, comme l'interface de ligne de commande cf et des outils Eclipse,
que vous pouvez utiliser pour coder avec votre application. Vous pouvez choisir l'interface de ligne de commande cf pour commencer à coder avec votre
application TestNode.

  1. Tout d'abord, téléchargez et développez le code de votre application.
  
    1. Accédez à la page Commencer le codage de votre application. Cliquez sur le bouton **Télécharger le code du module de démarrage**
pour télécharger le code de votre application.
    2. Procédez à l'extraction du fichier téléchargé dans un répertoire, par exemple `C:\test`.
    3. Développez le code dans votre environnement de développement intégré local.
	
  2. Installez l'interface de ligne de commande **cf**.
  
    1. Téléchargez le programme d'installation de l'outil de ligne de commande cf pour votre système d'exploitation.
    2. Suivez l'assistant de l'outil pour effectuer l'installation .
    3. Utilisez la commande **cf -v** pour vérifier la version de l'interface de ligne de commande cf. Exemple :
	
	```
	cf -v
	```
	
    **Condition requise :** assurez-vous de toujours utiliser la version la plus récente de l'outil de ligne de
commande
cf.
  3. Une fois que vous avez installé l'interface de ligne de commande **cf**, vous devez spécifier la région
{{site.data.keyword.Bluemix_notm}} que vous voulez utiliser avec la commande **cf api**. L'interface de ligne de commande
**cf** utilise *https://api.URL_Bluemix*, où *URL_Bluemix* est l'adresse URL de la région. L'adresse URL de la
région Sud des Etats-Unis est {{Domain}}. Entrez
la commande suivante pour vous connecter à {{site.data.keyword.Bluemix_notm}} :
  
  ```
  cf api https://api.ng.bluemix.net
  ```
  
  Pour plus d'informations sur la connexion à d'autres régions {{site.data.keyword.Bluemix_notm}}, voir Régions {{site.data.keyword.Bluemix_notm}}. Une fois que vous avez spécifié la région {{site.data.keyword.Bluemix_notm}}, les informations d'emplacement que
vous avez indiquées sont sauvegardées.
  
  4. Ensuite, vous pouvez vous connecter à {{site.data.keyword.Bluemix_notm}} avec la commande cf login.
  
  ```
  cf login -u votre_ID_utilisateur -p ***** -o nom_de_votre_organisation -s nom_de_votre_espace
  ```
  
  5. Une fois que vous êtes connecté à {{site.data.keyword.Bluemix_notm}},
vous êtes prêt à déployer votre application dans {{site.data.keyword.Bluemix_notm}}. Depuis le répertoire de votre application, `C:\test`, entrez la commande suivante :
  
  ```
  cf push TestNode
  ```
  
  Pour plus d'informations sur la commande **cf push**, voir Téléchargement de votre application.
  
  6. A présent, vous pouvez accéder à l'application en entrant l'adresse URL de l'application suivante dans un navigateur :
  ```
  http://TestNode.mybluemix.net
  ```

Vous pouvez aussi choisir d'autres outils pour construire votre application, comme des outils Eclipse. Pour plus d'informations, voir la page
Commencer le codage de votre application dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}.

## Liaison d'un service via l'interface de ligne de commande cf
{: #ee_cfbind}

Avec {{site.data.keyword.Bluemix_notm}}, vous pouvez ajouter un service en utilisant l'interface
utilisateur Bluemix, comme décrit précédemment dans ce scénario. Mais vous pouvez aussi lier un service en utilisant l'interface de ligne de commande
**cf**. Supposez que vous voulez ajouter le service {{site.data.keyword.cloudant}} à votre application TestNode via l'interface de ligne de commande cf.

Pour pouvoir utiliser le service {{site.data.keyword.cloudant}} dans votre application, vous devez créer
une instance de service Cloudant, lier votre application à l'instance de service, puis utiliser l'instance de service. La même procédure s'applique à tous
les autres services.

  1. Créez une instance de service Cloudant NoSQL DB.
  
  Créez une instance de service à l'aide de la commande cf create-service. Exemple :
  
  ```
  cf create-service cloudantNoSQLDB Shared cloudant100
  ```
  
  La commande cf services permet d'afficher la liste des instances de service déjà créées.
  
  ```
  cf services
  ```
  
  Lorsqu'une instance de service est créée, vous pouvez la lier et l'utiliser avec chacune de vos applications.
  
  2. Liez l'instance de service à votre application.
  
  Pour utiliser une instance de service, vous devez la lier à votre application. Pour ce faire, utilisez la commande cf bind-service en spécifiant le
nom de l'application et l'instance de service.
  
  ```
  cf bind-service TestNode cloudant100
  ```
  
  L'établissement d'une liaison entre une instance de service et une application permet à {{site.data.keyword.Bluemix_notm}} de signaler au service qu'une nouvelle application entrera en communication avec cette instance. En fonction des services, il est possible que {{site.data.keyword.Bluemix_notm}} traite l'application et l'instance de service de manière différente au cours du processus de liaison. Par exemple, certains services peuvent créer un locataire pour chaque application communiquant avec l'instance de service. Le service répond à {{site.data.keyword.Bluemix_notm}} en indiquant les informations (par exemple, les données d'identification) qui doivent être transmises à l'application en vue de l'établissement de la communication entre l'application et le service.

  **Remarque :** si l'application est en cours d'exécution lorsque la liaison à une instance de service est créée, la variable
d'environnement VCAP_SERVICES est
mise à jour lorsque cette application est à nouveau démarrée. Pour redémarrer votre application, utilisez la commande cf restart.
  
  3. Utilisez l'instance de service.
  
  Dans ce scénario, la variable d'environnement VCAP_SERVICES contient des informations, telles que les éléments suivants, qu'une application peut
utiliser pour se connecter à cette instance de {{site.data.keyword.cloudant}} :
  
  <dl><dt>username</dt>
  <dd>d72837bb-b341-4038-9c8e-7f7232916197-bluemix</dd>
  <dt>password</dt>
  <dd>b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424</dd>
  <dt>url</dt>
  <dd>https://d72837bb-b341-4038-9c8e-7f7232916197-bluemix:b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424@d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com</dd></dt></dl>
  
  Ainsi, votre application Node.js peut accéder à ces informations de la manière suivante :
  ```
  if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var cloudant = env['"cloudantNoSQLDB'][0].credentials;
  } else {
        var cloudant = {
                "username" : "user1",
                "password" : "secret",
                "url" : "https://user1:secret@localhost:25002"
                }
        };
  ```
  
  **Remarque :** comme illustré par cet exemple de code, pour vous connecter à une instance de service {{site.data.keyword.cloudant}}, vous pouvez commencer par
vérifier si la variable
d'environnement VCAP_SERVICES existe. Si c'est le cas, l'application peut utiliser les propriétés de la variable cloudant pour accéder à la base de
données. Par contre, si la variable d'environnement VCAP_SERVICES n'existe pas, l'instance de service {{site.data.keyword.cloudant}} locale est utilisée avec les valeurs par
défaut
fournies.
  
  4. Interagissez avec l'instance de service.
  
  Pour interagir avec l'instance de service, utilisez les données d'identification. Les actions que vous pouvez effectuer sont la lecture, l'écriture et la mise à  jour. L'exemple suivant montre comment insérer un objet JSON dans
l'instance de service {{site.data.keyword.cloudant}} :
  ```
  // créez un message
var create_message = function(req, res) {
  require('cloudantdb').connect(cloudant.url, function(err, conn) {
    var collection = conn.collection('messages');

    // créez un enregistrement de message
    var parsedUrl = require('url').parse(req.url, true);
    var queryObject = parsedUrl.query;
    var name = (queryObject["name"] || 'Bluemix');
    var message = { 'message': 'Hello, ' + name, 'ts': new Date()
};
    collection.insert(message, {safe:true}, function(err){
      if (err) { console.log(err.stack); }
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.write(JSON.stringify(message));
      res.end('\n');
    });
  });
}
  ```
  
  5. **Facultatif :** supprimez la liaison d'une instance de service ou supprimez une instance de service.
  
  Vous pouvez décider de supprimer la liaison d'une instance de service ou de supprimer une instance de service lorsqu'elle n'est plus utilisée, ou
lorsque vous avez besoin d'espace. Pour supprimer la liaison d'une instance de service depuis votre application, utilisez la commande **cf
unbind-service** ;
pour supprimer une instance de service, utilisez la commande **cf delete-service**.

  Pour plus d'informations sur les services, voir Services. Pour plus d'informations sur les options **cf** qui permettent de
gérer vos applications dans l'environnement {{site.data.keyword.Bluemix_notm}}, exécutez **cf --help** dans l'interface de ligne de commande **cf**.

  **Remarque :** avant de supprimer une instance de service, assurez-vous de ne plus en avoir besoin. Cette action entraîne la suppression de toutes les données associées à l'instance. La variable d'environnement VCAP_SERVICES d'une application liée à un service supprimé n'est pas mise à jour tant que cette application n'est pas
redémarrée.

## Calcul du coût de votre application
{: #ee_billing}

Votre essai gratuit de 30 jours est arrivé à expiration mais vous voulez continuer d'utiliser {{site.data.keyword.Bluemix_notm}}. Vous devez ajouter vos informations de carte de crédit afin de créer un compte Paiement à la carte ou un compte d'abonnement pour pouvoir continuer
à utiliser {{site.data.keyword.Bluemix_notm}}. Toutefois,
{{site.data.keyword.Bluemix_notm}} propose toujours des franchises pour la plupart des infrastructures de
contexte d'exécution et des services, même si vous convertissez votre compte en compte payant. {{site.data.keyword.Bluemix_notm}}
ne vous facture rien sauf si votre utilisation dépasse les franchises.

{{site.data.keyword.Bluemix_notm}} met à disposition un estimateur et une calculatrice pour que vous puissiez
afficher le coût de votre application. Vous pouvez afficher le coût de TestNode de plusieurs façons :

  * Dans votre tableau de bord, cliquez sur TestNode. Puis, sur la page de présentation, cliquez sur **Estimer le coût de cette
application** pour examiner la tarification de l'environnement d'exécution et du support de **SDK for Node.js**, et le prix mensuel
total de
votre application.
  
  * Ou bien, dans la page Fiche des prix, entrez l'utilisation mensuelle du contexte d'exécution et des services pour votre application, par
exemple 3 instances de **SDK for Node.js** avec 1 Go de mémoire pour chaque instance. Le prix mensuel est calculé et affiché.

Vous pouvez aussi calculer le coût de votre application manuellement en ajoutant les prix de vos contextes d'exécution et de vos services et en
déduisant les franchises. Pour plus d'informations, voir Calcul manuel de vos coûts.

## Suppression d'applications
{: #ee_removing}

Au fur et à mesure que vous construisez des applications, le quota peut approcher la limite. Toutefois, il se peut que certaines applications
qui ne sont plus utilisées soient comptabilisées dans ce quota. Il est facile de les supprimer à tout moment afin de libérer de l'espace dans
{{site.data.keyword.Bluemix_notm}}.

Dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, accédez à la page Vue d'ensemble de l'application, cliquez sur
l'icône **Menu** et supprimez
l'application que vous n'utilisez plus. Vous pouvez
aussi utiliser la commande **cf delete** pour supprimer des applications.
