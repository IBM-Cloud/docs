---

Copyright :
  Années : 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Tomcat
{: #tomcat_runtime}
*Dernière mise à jour : 19 mars 2016*

Le contexte d'exécution Tomcat sur {{site.data.keyword.Bluemix}} repose sur le pack java_buildpack.
{: shortdesc}

Pour utiliser le contexte d'exécution Tomcat sur {{site.data.keyword.Bluemix}}, vous devez spécifier le pack java_buildpack avec l'option -b. Par exemple :
<pre>
    cf push &lt;myApp&gt; -p &lt;pathToMyApp&gt; -b java_buildpack
</pre>

Pour plus d'informations sur le contexte d'exécution Tomcat, voir le fichier [Readme java-buildpack](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md).

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} propose une application de démarrage Tomcat.  L'application de démarrage Tomcat est une application Tomcat simple qui fournit un modèle que vous pouvez utiliser. Vous pouvez expérimenter cette application de démarrage et effectuer des modifications puis les envoyer par commande push vers l'environnement Bluemix. Voir [Utilisation des applications de démarrage](../../cfapps/starter_app_usage.html) pour obtenir de l'aide.

## Versions de contexte d'exécution
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
La version par défaut en cours de Tomcat est 8.0.30.  La version par défaut en cours de Java est 1.8.0_65.
Pour plus d'informations, voir les informations sur les [éditions java-buildpack](https://github.com/cloudfoundry/java-buildpack/releases).

# rellinks
## general
* [java-buildpack](https://github.com/cloudfoundry/java-buildpack)
