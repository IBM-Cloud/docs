---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Tomcat
{: #tomcat_runtime}

L'environnement d'exécution Tomcat sur {{site.data.keyword.Bluemix}} repose sur le pack java_buildpack.
{: shortdesc}

Pour utiliser l'environnement d'exécution Tomcat sur {{site.data.keyword.Bluemix}}, vous devez spécifier le pack java_buildpack avec l'option -b. Par exemple :
<pre>
    cf push &lt;myApp&gt; -p &lt;pathToMyApp&gt; -b java_buildpack
</pre>

Pour plus d'informations sur l'environnement d'exécution Tomcat, voir le fichier [Readme java-buildpack](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md).

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} propose une application de démarrage Tomcat.  L'application de démarrage Tomcat est une application Tomcat simple qui fournit un modèle que vous pouvez utiliser. Vous pouvez expérimenter cette application de démarrage et effectuer des modifications puis les envoyer par commande push vers l'environnement Bluemix. Voir [Utilisation des applications de démarrage](/docs/cfapps/starter_app_usage.html) pour obtenir de l'aide.

## Versions d'environnement d'exécution
{: #runtime_versions}

Vous pouvez modifier la version de Tomcat que votre application doit utiliser en utilisant la variable d'environnement JBP_CONFIG_TOMCAT.
Vous pouvez modifier la version de Java que votre application doit utiliser en utilisant la variable d'environnement JBP_CONFIG_OPEN_JDK_JRE.
Ces deux variables d'environnement peuvent être définies dans le fichier manifeste de l'application.  Par exemple :
```
    env:
        JBP_CONFIG_TOMCAT: '{tomcat: { version: 8.0.+ }}'
        JBP_CONFIG_OPEN_JDK_JRE: '{jre: { version: 1.7.0_+ }}'
```
{: codeblock}
La version java_buildpack actuelle, v3.6, contient la version 8.30.0 Tomcat par défaut et la version Java 1.8.0_71 par défaut.
Pour plus d'informations, voir les informations sur les [éditions java-buildpack](https://github.com/cloudfoundry/java-buildpack/releases).

## Redirection HTTPS
{: #https_redirect}

L'environnement d'exécution Tomcat peut être configuré pour faire confiance aux proxys internes Bluemix et autoriser la redirection du trafic HTTP vers HTTPS (SSL).
Pour ce faire, modifiez le fichier server.xml et définissez l'élément RemoteIpValve Valve avec les options internalProxies et protocolHeader.

Le fichier [server.xml](https://github.com/cloudfoundry/java-buildpack/blob/master/resources/tomcat/conf/server.xml) de l'environnement d'exécution Tomcat inclus dans le pack de construction ne définit par défaut que l'option protocolHeader pour l'élément RemoteIpValve Valve.  Pour rediriger le trafic HTTP vers HTTPS dans Bluemix, configurez l'élément RemoteIpValve dans le fichier server.xml personnalisé comme suit :

```
 <Valve className='org.apache.catalina.valves.RemoteIpValve' protocolHeader='x-forwarded-proto' internalProxies='.*' />
```
{: codeblock}

Vous trouverez davantage d'options de configuration de RemoteIpValve dans la [documentation Tomcat![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://tomcat.apache.org/tomcat-8.0-doc/api/org/apache/catalina/valves/RemoteIpValve.html).

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [java-buildpack](https://github.com/cloudfoundry/java-buildpack)
