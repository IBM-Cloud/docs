---

Copyright :
  Années : 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilisation de Dynatrace
{: #using_dynatrace}

*Dernière mise à jour : 08 avril 2016*

Dynatrace est un service tiers qui offre une fonction de surveillance pour votre appli.

Pour plus d'informations sur les fonctions offertes par le service Dynatrace, voir [Dynatrace Application Monitoring](http://www.dynatrace.com/en/products/application-monitoring.html).

Lorsque vous activez le service Dynatrace à utiliser avec votre appli Liberty, procédez comme suit :

1. Procurez-vous et hébergez le fichier JAR d'agent Dynatrace de sorte que le pack de construction Liberty puisse le télécharger.
2. Configurez une instance du serveur Dynatrace de sorte que l'agent Dynatrace qui s'exécute avec votre appli Liberty puisse communiquer avec elle.
3. Configurez votre appli Liberty de sorte qu'elle puisse télécharger l'agent Dynatrace et se connecter au serveur Dynatrace.

## Hébergement de l'agent Dynatrace
{: #hosting_dynatrace_agent}
L'agent Dynatrace doit être hébergé sur un serveur Web, et le pack de construction liberty doit pouvoir télécharger le fichier JAR d'agent à partir de ce serveur. Le serveur doit être configuré avec un fichier index.yml qui indique les détails concernant le fichier JAR d'agent. Pour configurer l'agent Dynatrace, procédez comme suit :
  1. Téléchargez le fichier JAR de l'agent Dynatrace. Pour obtenir les instructions relatives au téléchargement du fichier JAR de l'agent Dynatrace, voir [Dynatrace Server Platform Installers](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace) sur le site Web de la communauté Dynatrace. Le fichier JAR d'agent approprié pour une exécution sur Bluemix est **dynatrace-agent-unix.jar** version **6.3.0+**.
  2. Hébergez le fichier JAR d'agent dans un emplacement à partir duquel le pack de construction Liberty peut le télécharger. Vous pouvez l'héberger directement sur Bluemix à l'aide des fonctions disponibles sur le serveur, ou vous pouvez l'héberger sur un emplacement disponible publiquement.
     * Prenez soin de fournir un fichier index.yml à l'emplacement d'hébergement. Le fichier index.yml doit contenir une entrée composée de l'ID de version du fichier JAR d'agent suivi d'un signe deux-points et de l'URL complète de l'emplacement de ce fichier JAR d'agent. Par exemple :
```
      ---
      6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
```
{: #codeblock}
     * A la fin de l'URL, le nom du fichier JAR doit être **dynatrace-agent-version-unix.jar**. La version doit être **6.3.0** ou **6.3.0_nnnn**, où nnnn est l'identificateur de micro-version. Notez que ces informations peuvent différer de celles incluses dans le nom du fichier JAR utilisé par Dynatrace. Par conséquent, vous devrez peut-être renommer le fichier JAR.       
     * Le fichier **dynatrace-agent-6.3.0-unix.jar** doit être disponible à l'emplacement spécifié dans le fichier index.yml. L'emplacement du fichier JAR et celui du fichier index.yml peuvent correspondre au même répertoire.

## Configuration du collecteur Dynatrace

Vous devrez ensuite configurer un collecteur Dynatrace accessible pour l'agent Dynatrace. Vous devrez également créer un service fourni par l'utilisateur afin de transmettre les informations permettant à l'agent Dynatrace de se connecter au collecteur Dynatrace. Pour mieux comprendre la relation entre les composants Dynatrace, voir [Dynatrace Architecture](https://community.dynatrace.com/community/display/DOCDT63/Architecture).

  1. Configurez un collecteur Dynatrace.
    * Pour obtenir les instructions relatives au téléchargement et à la configuration du collecteur Dynatrace, voir le [site Web Dynatrace](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace).
    * Vérifiez que le collecteur est configuré dans un emplacement accessible pour l'agent Dynatrace qui s'exécute avec votre appli dans Bluemix.
  2. Créez un service fourni par l'utilisateur qui pointe vers le collecteur Dynatrace en cours d'exécution. <b>REMARQUE</b> Le nom du service fourni par l'utilisateur doit contenir <b>dynatrace</b>.  Par exemple, utilisez la commande suivante :
```
    $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
```
{: #codeblock}
Dans cet exemple, my-dynatrace-collector est le nom donné au service, DynatraceCollectorIPaddress est l'adresse IP du collecteur Dynatrace que vous avez configuré et le paramètre profile fait référence au nom de profil Dynatrace facultatif associé à cette application surveillée. La valeur de profil par défaut est Monitoring. Vous pouvez définir des paramètres facultatifs tels que ceux illustrés dans l'exemple suivant :
```
    $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                                          "options" : {
                                                       "dynatrace-parameter-1": "value",
                                                       "dynatrace-parameter-2": "value"
                                         }}'
```
{: #codeblock}
Pour plus d'informations sur les options disponibles, voir [Agent Setting section of Agent Configuration](https://community.dynatrace.com/community/display/DOCDT62/Agent+Configuration) sur le site Web de la communauté Dynatrace. Par exemple, vous pouvez utiliser l'option exclude pour exclure des classes de la surveillance par Dynatrace. Pour plus d'informations sur la configuration du service fourni par l'utilisateur, voir [DynaTrace Agent Framework](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md).
  3. Après avoir envoyé par commande push votre appli à Bluemix, associez le service fourni par l'utilisateur que vous avez créé à cette appli. Par exemple, utilisez la commande suivante :
```
    $ cf bs myApp my-dynatrace-service
```
**Remarque** : Vous devez reconstituer votre application après avoir associé le service.

## Configuration de l'appli Liberty
{: #configuring_liberty_app}

L'appli Liberty que vous souhaitez surveiller doit être configurée pour localiser le serveur qui héberge le fichier JAR d'agent que vous avez précédemment configuré. Vous pouvez configurer l'appli avec la variable d'environnement **JBP_CONFIG_DYNATRACEAGENT**. La variable d'environnement **JBP_CONFIG_DYNATRACEAGENT** indique au pack de construction l'emplacement à partir duquel il doit télécharger l'agent Dynatrace. Pour définir la variable d'environnement, procédez comme suit :
<ol>
   <li> Affectez à la variable **JBP_CONFIG_DYNATRACEAGENT** la valeur *"repository_root: URL_of_server_hosting_index.yml"*. Par exemple, après avoir envoyé par commande push votre application, exécutez la commande suivante :
```
    $ cf se myApp JBP_CONFIG_DYNATRACEAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
```
{: #codeblock}
  Dans cet exemple, *my-dynatrace-agent-host.mybluemix.net* est l'URL du fichier index.yml hébergé par le serveur que vous avez précédemment configuré.
  </li>
  <li> Après avoir défini la variable d'environnement, reconstituez votre application. Le fichier staging_task.log de votre appli Liberty génère un message indiquant que le téléchargement de l'agent Dynatrace à partir du serveur sur lequel il est hébergé a abouti. Par exemple :
```
    Downloading dynatrace-agent-6.3.0-unix.jar 6.3.0 from https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)
```
{: #codeblock}
</li>
<li>Pour consulter le fichier staging_task.log, exécutez la commande suivante :
```
    $ cf files myAppName logs/staging_task.log
```
{: #codeblock}
</li>
</ol>

# rellinks
## general
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
