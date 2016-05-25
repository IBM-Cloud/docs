---

Copyright :
  Années : 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Options pour l'envoi par commande push d'applications Liberty
{: #options_for_pushing}

*Dernière mise à jour : 23 mars 2016*

Le comportement du serveur Liberty dans Bluemix est contrôlé par le pack de construction Liberty. Les packs de construction peuvent fournir un environnement d'exécution complet pour une classe d'applications spécifique. Ils sont cruciaux pour assurer la portabilité entre les clouds et une contribution à une architecture de cloud ouverte. Le
pack de construction Liberty fournit un conteneur WebSphere Liberty capable d'exécuter des applications Java EE 7 et OSGi. Il prend en charge les
infrastructures populaires telles que Spring et inclut l'environnement d'exécution Java IBM JRE. WebSphere Liberty permet un développement d'application rapide qui est adapté au cloud. Le pack de construction Liberty prend en charge plusieurs applications déployées sur un même serveur Liberty. Dans le cadre de l'intégration du pack de construction Liberty  dans Bluemix, celui-ci fait en sorte que les variables d'environnement pour la liaison de services soient indiquées sous forme de variables de configuration sur le serveur Liberty.

Vous pouvez utiliser les méthodes suivantes pour déployer vos applications Liberty sur Bluemix :

* Envoi par commande push d'une application autonome
* Envoi par commande push d'un répertoire de serveur
* Envoi par commande push d'un package de serveur

Important : quand vous déployez une application avec le pack de construction Liberty, attribuez une valeur d'au moins 512 Mo comme limite de mémoire pour vos applications. Pour plus d'informations, voir [Limites mémoire et pack de construction Liberty](memoryLimits.html).

## Applications autonomes
{: #stand_alone_apps}

Les applications autonomes, par exemple, des fichiers WAR ou EAR, peuvent être déployées sur Liberty dans Bluemix.

Pour déployer une application autonome, exécutez la commande cf push avec le paramètre -p qui indique le fichier WAR ou EAR.
Par exemple :

```
    $ cf push <yourappname> -p myapp.war
```
{: #codeblock}

Lorsqu'une application autonome est déployée, une configuration Liberty par
défaut est fournie pour l'application. Cette configuration par défaut active
les fonctions Liberty suivantes :

* beanValidation-1.1
* [cdi-1.2](optionsForPushing.html#cdi12)
* ejbLite-3.2
* el-3.0
* jaxrs-2.0
* jdbc-4.1
* jndi-1.0
* jpa-2.1
* jsf-2.2
* jsonp-1.0
* jsp-2.3
* managedBeans-1.0
* servlet-3.1
* websocket-1.1
* icap:managementConnector-1.0
* appstate-1.0

Ces fonctions correspondent aux fonctions du profil Web Java EE 7. Vous pouvez spécifier un autre jeu de fonctions Liberty en définissant la variable d'environnement
JBP_CONFIG_LIBERTY. Par exemple, pour n'activer que les fonctions jsp-2.3 et websocket-1.1, exécutez la commande suivante et
reconstituez l'application :

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: {features: [jsp-2.3, websocket-1.1]}"
```
{: #codeblock}

Remarque : Pour optimiser vos résultats, définissez les fonctions Liberty avec la variable d'environnement JBP_CONFIG_LIBERTY ou déployez votre application en tant que [répertoire de serveur](optionsForPushing.html#server_directory) ou [package de serveur](optionsForPushing.html#packaged_server) avec un fichier server.xml personnalisé. La définition de cette variable d'environnement garantit que votre application n'utilisera que la fonction dont elle a besoin et qu'elle ne sera pas
affectée par les modifications apportées
au jeu de fonctions Liberty par défaut du pack de construction. Si vous devez fournir une configuration Liberty supplémentaire en plus du jeu de fonctions,
utilisez l'option de [répertoire de serveur](optionsForPushing.html#server_directory) ou de
[package de serveur](optionsForPushing.html#packaged_server) pour déployer votre application.

Si vous avez déployé un fichier WAR, l'application Web est accessible sous la racine de contexte, telle que définie dans le fichier ibm-web-ext.xml imbriqué. Si le fichier ibm-web-ext.xml n'existe pas ou ne spécifie pas de racine de contexte, l'application est accessible sous le contexte racine. Exemple :

```
    http://<nom_de_votre_app>.mybluemix.net/
```
{: #codeblock}

Si vous avez déployé un fichier EAR, l'application Web imbriquée est accessible
sous la racine de contexte comme indiqué dans le descripteur de déploiement du
fichier EAR. Exemple :

```
    http://<yourappname>.mybluemix.net/acme/
```
{: #codeblock}

Le fichier de configuration Liberty par défaut
server.xml complet est le suivant :
```
    <server>
       <featureManager>
          <feature>beanValidation-1.1</feature>
          <feature>cdi-1.2</feature>
          <feature>ejbLite-3.2</feature>
          <feature>el-3.0</feature>
          <feature>jaxrs-2.0</feature>
          <feature>jdbc-4.1</feature>
          <feature>jndi-1.0</feature>
          <feature>jpa-2.1</feature>
          <feature>jsf-2.2</feature>
          <feature>jsonp-1.0</feature>
          <feature>jsp-2.3</feature>
          <feature>managedBeans-1.0</feature>
          <feature>servlet-3.1</feature>
          <feature>websocket-1.1</feature>
          <feature>icap:managementConnector-1.0</feature>
          <feature>appstate-1.0</feature>
       </featureManager>

       <application name='myapp' location='myapp.war' type='war' context-root='/'/>
       <httpEndpoint id='defaultHttpEndpoint' host='*' httpPort='${port}'/>
       <webContainer trustHostHeaderPort='true' extractHostHeaderPort='true'/>
       <include location='runtime-vars.xml'/>
       <logging logDirectory='${application.log.dir}' consoleLogLevel='INFO'/>
       <httpDispatcher enableWelcomePage='false'/>
       <applicationMonitor dropinsEnabled='false' updateTrigger='mbean'/>
       <config updateTrigger='mbean'/>
       <cdi12 enableImplicitBeanArchives='false'/>
       <appstate appName='myapp' markerPath='${home}/../.liberty.state'/>
    </server>
```
{: #codeblock}

### CDI 1.2
{: #cdi12}

Pour des raisons de performance, lors du déploiement des fichiers WAR et EAR seulement,
l'[examen
des archives de bean implicites CDI 1.2](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_cdi_behavior.html) est désactivé par défaut. L'examen des archives de bean implicites peut être activé avec la variable d'environnement JBP_CONFIG_LIBERTY.
Par exemple :

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: { implicit_cdi: true }"
```    
{: #codeblock}

Important : Pour que les modifications que vous apportez aux variables d'environnement soient appliquées, vous devez reconstituer votre
application :

```
    $ cf restage myapp
```
{: #codeblock}

## Répertoire de serveur
{: #server_directory}

Dans certains cas, vous devez fournir une configuration de serveur Liberty personnalisée avec votre application. Cette configuration personnalisée peut s'avérer nécessaire lorsque vous déployez un fichier EAR ou WAR et que le fichier server.xml par défaut ne comporte pas certains des paramètres requis par votre application.

Si vous avez installé le profil Liberty sur votre poste de travail et que vous avez déjà créé un serveur Liberty avec votre application, vous pouvez envoyer par commande push le contenu de ce répertoire à Bluemix.
Par exemple, si votre serveur Liberty se nomme defaultServer, exécutez la commande suivante :

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer
```
{: #codeblock}

Si aucun profil Liberty n'est
installé sur votre poste de travail, vous pouvez suivre la procédure ci-après pour créer un répertoire de serveur avec votre application :

1. Créez un répertoire nommé defaultServer.
2. Créez un répertoire apps dans le répertoire defaultServer.
3. Copiez le fichier WAR ou EAR dans le répertoire defaultServer/apps.
4. Dans le répertoire defaultServer, créez un fichier server.xml avec l'exemple de contenu exemple ci-après.  De plus :
  * Prenez soin de mettre à jour l'attribut location ou type de l'élément d'application afin de le faire
correspondre au nom de fichier et au type de votre application.
  * Le fichier server.xml dans le diagramme affiche un jeu minimal de fonctions. Vous devrez ajuster le jeu de fonctions en fonction des besoins de
votre application.


```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
        </featureManager>

        <httpEndpoint id="defaultHttpEndpoint" host="*" httpPort="8080" />

        <application name="myapp" context-root="/" type="war" location="myapp.war"/>
    </server>
```
{: #codeblock}

Lorsque le répertoire de serveur est prêt, vous pouvez le déployer sur Bluemix.

```
    $ cf push <yourappname> -p defaultServer
```
{: #codeblock}

Remarque : Les
applications Web déployées avec le répertoire de serveur sont accessibles sous la [racine de contexte, comme spécifié par le profil Liberty](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/twlp_dep_war.html?cp=SSAW57_8.5.5%2F1-3-11-0-5-6). Par exemple :

```
    http://<yourappname>.mybluemix.net/acme/
```
{: #codeblock}

## Package de serveur
{: #packaged_server}

Vous pouvez également envoyer par commande push un fichier de package de serveur à Bluemix. Pour créer le fichier de package de serveur, utilisez la commande server
package de Liberty. Outre les fichiers de l'application et de configuration, le
fichier de package de serveur peut contenir des ressources partagées et les
fonctions utilisateur Liberty requises par l'application.

Pour conditionner un serveur Liberty, utilisez la commande ./bin/server package à partir du répertoire d'installation de Liberty. Indiquez le nom de votre serveur et précisez l'option '––include=usr' option.
Par exemple, si le serveur Liberty se nomme defaultServer, exécutez la commande suivante :

```
    $ wlp/bin/server package defaultServer --include=usr
```
{: #codeblock}

Cette commande génère un fichier serverName.zip dans le répertoire du serveur. Vous pouvez ensuite envoyer par commande push le fichier
compressé à Bluemix à l'aide de la commande cf push.
Par exemple :

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer/defaultServer.zip
```
{: #codeblock}

Remarque : Les applications Web déployées avec le package de serveur sont accessibles sous la
racine
de contexte, comme spécifié par le profil Liberty.

### Modification du fichier server.xml
{: #modifications_of_serverxml}

Lors de l'envoi par commande push d'un package de serveur ou d'un répertoire de serveur
Liberty, le pack de construction Liberty détecte le fichier server.xml, en même temps que votre application. Le pack de construction Liberty apporte les modifications suivantes au fichier server.xml.

* Le pack de construction vérifie que le fichier contient exactement un élément httpEndpoint.
* Le pack de construction vérifie que l'attribut httpPort dans l'élément httpEndpoint pointe sur une variable système qui se nomme ${port}. Le
pack de construction remplace également l'attribut host.
* Le pack de construction définit l'attribut logDirectory de l'élément logging de telle sorte qu'il pointe sur un répertoire de journal système.
* Le pack de construction fait en sorte qu'un fichier runtime-vars.xml soit fusionné sur une base logique avec votre fichier server.xml. Plus spécifiquement, il ajoute la ligne *&lt;include location="runtime-vars.xml" /&gt;* à votre fichier server.xml.

### Variables référençables
{: #referenceable_variables}

Les variables suivantes sont définies dans le fichier runtime-vars.xml et référencées depuis un fichier server.xml envoyé par commande push. Toutes les variables sont sensibles à la casse.

* ${port} : port HTTP sur lequel le serveur Liberty est à l'écoute.
* ${vcap_console_port} : port sur lequel la console vcap s'exécute (généralement identique à ${port}).
* ${vcap_app_port} : port sur lequel le serveur app est à l'écoute (généralement identique à ${port}).
* ${vcap_console_ip} : adresse IP de la console vcap (généralement, adresse IP sur laquelle le serveur Liberty est à l'écoute).
* ${application_name} : nom de l'application, tel que défini via les options de la commande cf push.
* ${application_version} : version de cette instance de l'application, représentée par un UUID (identificateur unique universel), tel que b687ea75-49f0-456e-b69d-e36e8a854caa. Cette variable est actualisée avec chaque envoi par commande push successif de l'application contenant du nouveau code ou des modifications des artefacts de l'application.
* ${host} : adresse IP de l'agent DEA qui exécute l'application (généralement, identique à ${vcap_console_ip}).
* ${application_uris}: matrice JSON des noeuds finaux pouvant être utilisés pour accéder à cette application, par exemple : myapp.mydomain.com.
* ${start} : date et heure de démarrage de l'application, sous un format similaire à 2013-08-22 10:10:18 -0400.

### Accès aux informations des services liés
{: #accessing_info_of_bound_services}

Si vous voulez lier un service à votre application, des informations sur le service, notamment les données d'identification de connexion,
sont incluses dans
la [variable
d'environnement VCAP_SERVICES](http://docs.run.pivotal.io/devguide/deploy-apps/environment-variable.html#VCAP-SERVICES) que Cloud Foundry définit pour l'application. Pour les [services configurés
automatiquement](autoConfig.html), le pack de construction Liberty génère ou met à jour des entrées de liaison de service dans le fichier server.xml. Le contenu des
entrées de liaison de service peuvent être dans l'un des formats suivants :

* cloud.services.&lt;service-name&gt;.&lt;property&gt;, qui décrit les informations telles que le nom, le type et le plan du service.
* cloud.services.&lt;service-name&gt;.connection.&lt;property&gt;, qui décrit les informations de connexion du service.

L'ensemble d'informations habituel est le suivant :
* name : Nom du service. Par exemple, mysql-e3abd.
label: Type de service créé. Par exemple, mysql-5.5.
* plan : Plan de service, tel qu'indiqué par l'identificateur unique de ce plan. Par exemple, 100.
connection.name : Identificateur unique de la connexion, prend la forme d'un identificateur unique universel (UUID). Par exemple, d01af3a5fabeb4d45bb321fe114d652ee.
* connection.hostname : Nom d'hôte du serveur qui exécute le service. Par exemple, mysql-server.mydomain.com.
* connection.host : Adresse IP du serveur qui exécute le service. Par exemple, 9.37.193.2.
* connection.port : Port sur lequel le service est à l'écoute de connexions entrantes. Par exemple, 3306,3307.
* connection.user : Nom d'utilisateur employé pour authentifier cette application auprès du service. Le nom d'utilisateur est généré automatiquement par Cloud Foundry. Par exemple :unHwANpjAG5wT.
* connection.username : Alias de connection.user.
* connection.password : Mot de passe utilisé pour authentification de cette application auprès du service. Le mot de passe est généré automatiquement par Cloud Foundry. Par exemple :pvyCY0YzX9pu5.

Pour les services liés qui ne sont pas configurés automatiquement par le pack de construction
Liberty, l'application doit gérer elle-même l'accès à la ressource back end.

# rellinks
## general
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
