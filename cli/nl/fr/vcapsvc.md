
{:shortdesc: .shortdesc}

# Services VCAP

*Dernière mise à jour : 9 novembre 2015*


La variable d'environnement VCAP_SERVICES est un objet JSON qui contient des informations que vous pouvez utiliser pour interagir avec une
instance de service dans {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


## Extraction de la valeur de la variable d'environnement VCAP_SERVICES
{:retrieving}

La variable d'environnement VCAP_SERVICES est un objet JSON qui contient des informations que vous pouvez utiliser pour interagir avec une
instance de service dans {{site.data.keyword.Bluemix_notm}}. Ces informations incluent le nom de l'instance de service et l'adresse URL de connexion à l'instance de service. 
Les valeurs sont remplies dans la variable d'environnement VCAP_SERVICES lorsque votre application est liée à une instance de service dans
{{site.data.keyword.Bluemix_notm}}. 

La valeur de la variable d'environnement VCAP_SERVICES n'est disponible que lorsque vous liez une instance de service à votre application. Vous pouvez afficher les variables d'environnement de l'application avec le pilote de la console WebSocket. L'exemple ci-dessous illustre l'utilisation du pilote de la console WebSocket pour afficher les
variables d'environnement d'une application Node.js.

Tout d'abord, exécutez la commande permettant d'envoyer à nouveau par commande push votre application Node.js.
```
cf push -c "curl -s
https://raw.githubusercontent.com/dmikusa-pivotal/cf-debug-tools/master/debug-console.sh | bash" votreapp
```
Ensuite, entrez l'adresse URL suivante :
```
https://yourapp.{APPDomain}/bash.sh
```
Dans la page qui s'affiche, cliquez sur la coche pour connecter l'outil, puis émettez la commande env pour afficher les variables d'environnement de votre
application. Pour plus d'informations sur cf-debug-tools, voir [Debug
Tools for Cloud Foundry](https://github.com/dmikusa-pivotal/cf-debug-tools).


## Affichage des couches de l'infrastructure Bluemix 
{:viewinfra}


{{site.data.keyword.Bluemix_notm}} masque les couches du système d'exploitation et de
l'infrastructure pour que vous n'ayez pas à les gérer. Toutefois, il se peut que vous souhaitiez en savoir plus sur le système d'exploitation et le
middleware utilisés pour votre application.

Vous pouvez exécuter la commande cf stacks pour afficher les piles, ou systèmes de fichiers racine, disponibles dans lesquelles vos applications
seront déployées. Vous pouvez aussi spécifier la pile lorsque vous utilisez la commande cf push avec l'option *-s* et l'argument
*nom_pile*, où nom_pile est le système de fichiers racine, par exemple `lucid64` ou `cflinuxfs2`:
```
cf push nom_app -s nom_pile
```
Vous pouvez utiliser la commande `cf buildpacks` pour afficher les composants de middleware, par exemple le profil WebSphere Liberty et
SDK for Node.js, qui sont
disponibles en tant que contextes d'exécution dans lesquels votre application peut s'exécuter. De plus, vous pouvez spécifier l'environnement d'exécution pour votre application avec la commande
suivante :
```
cf push nom_app -b nom_pack_construction
```
