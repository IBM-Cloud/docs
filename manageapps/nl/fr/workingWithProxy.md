---

copyright:
  years: 2016, 2017
lastupdated: "2016-07-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Utilisation d'un proxy
{: #working_with_proxy}



Dans certains environnements, tels que [Bluemix dédié](/docs/dedicated/index.html#dedicated) et
[Bluemix local](/docs/local/index.html#local), un proxy peut faire l'objet d'une configuration qui affecte le comportement de votre application lors de la constitution et de l'exécution.

Vous pouvez configurer votre application pour qu'elle fonctionne avec le proxy en utilisant les variables d'environnement suivantes :
  * [http_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [https_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [no_proxy](http://www.gnu.org/software/wget/manual/html_node/Proxies.html)

Vous pouvez définir ces variables d'environnement à l'aide de *cf se* ou du fichier *manifest.yml*.  Si votre application nécessite de télécharger des ressources depuis internet lors de la constitution et qu'une variable d'environnement de proxy est définie, selon la façon dont les variables d'environnement de proxy sont configurées, ces ressources seront téléchargées via le proxy configuré.

Par exemple, vous disposez d'une application nodejs que vous exécutez dans un environnement avec la valeur *yourProxyURL* affectée à *http_proxy*.  De plus, vous souhaitez autoriser npm à télécharger des modules de noeud depuis internet. Pour cela, vous pouvez affecter la valeur *npmjs.org* à *no_proxy*.

**Remarque** : il peut arriver que votre application bénéficie du proxy durant l'exécution.  Cela dépend entièrement de l'application et absolument pas du pack de construction ni d'aucune des trois variables d'environnement.

## Applications Java
{: #java_apps}

Pour [Liberty for Java](/docs/runtimes/liberty/index.html) et les applications [java_buildpack](/docs/runtimes/tomcat/index.html), les paramètres de proxy peuvent être transférés à l'exécution via la variable d'environnement **JAVA_OPTS**.  Par exemple, vous pouvez exécuter la commande suivante :
```
   $ cf se myApp JAVA_OPTS "-Dhttp.proxyHost=yourProxyURL -Dhttp.proxyPort=yourProxyPort"
```
{: codeblock}

et reconstituer votre application.  Votre application utilise ensuite les paramètres de proxy spécifiés lors de l'exécution. Pour plus d'informations sur les options de proxy Java, voir [Java Networking and Proxies](https://docs.oracle.com/javase/8/docs/technotes/guides/net/proxies.html).

# rellinks
{: #rellinks}
## general
{: #general}
* [Liberty for Java](/docs/runtimes/liberty/index.html)
* [SDK for Nodejs](/docs/runtimes/nodejs/index.html)
