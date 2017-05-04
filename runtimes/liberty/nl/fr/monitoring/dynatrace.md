---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Utilisation de Dynatrace
{: #using_dynatrace}

Dynatrace est un service tiers qui offre une fonction de surveillance pour votre appli.

Pour plus d'informations sur les fonctions offertes par le service Dynatrace, voir [Dynatrace Application Monitoring](http://www.dynatrace.com/en/products/application-monitoring.html).

Si votre application est configurée pour utiliser Dynatrace, par défaut, l'environnement d'exécution Liberty acquiert un fichier JAR d'agent Dynatrace à partir d'un site Dynatrace et exécute l'agent Dynatrace avec votre application. Avec ce comportement par défaut, la configuration minimale nécessaire pour utiliser Dynatrace consiste à créer un service fourni par l'utilisateur qui pointe vers votre collecteur Dynatrace.

## Création d'un service fourni par l'utilisateur qui pointe vers votre collecteur Dynatrace

Tout d'abord, vous devez configurez un collecteur Dynatrace.  Ensuite, vous devez créer un service fourni par l'utilisateur afin de transmettre des informations qui permettront à l'agent Dynatrace de se connecter au collecteur Dynatrace. Pour mieux comprendre la relation entre les composants Dynatrace, voir [Dynatrace Architecture](https://community.dynatrace.com/community/display/DOCDT63/Architecture).

1. Configurez un collecteur Dynatrace.
  * Pour obtenir les instructions relatives au téléchargement et à la configuration du collecteur Dynatrace, voir le [site Web Dynatrace](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace).
  * Vérifiez que le collecteur est configuré dans un emplacement accessible pour l'agent Dynatrace qui s'exécute avec votre appli dans Bluemix.
2. Créez un service fourni par l'utilisateur qui pointe vers le collecteur Dynatrace en cours d'exécution. **REMARQUE** Le nom du service fourni par l'utilisateur doit contenir la chaîne **dynatrace**.
Peu importe la casse des caractères. Par exemple, utilisez la commande suivante, dans laquelle **my-dynatrace-collector** contient **dynatrace** :

        $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
        {: codeblock}

    Dans cet exemple, my-dynatrace-collector est le nom donné au service, DynatraceCollectorIPaddress est l'adresse IP du collecteur Dynatrace que vous avez configuré et le paramètre profile fait référence au nom de profil Dynatrace facultatif associé à cette application surveillée.
La valeur par défaut de profile est Monitoring. Vous pouvez spécifier des paramètres optionnels, comme dans l'exemple suivant :

        $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                                              "options" : {"param-dynatrace-1": "valeur",
                                                           "param-dynatrace-2": "valeur"}}'
        {: codeblock}

    Pour plus d'informations sur les options disponibles, voir [Agent Setting section of Agent Configuration](https://community.dynatrace.com/community/display/DOCDT62/Agent+Configuration) sur le site Web de la communauté Dynatrace. Par exemple, vous pouvez utiliser l'option exclude pour exclure des classes de la surveillance par Dynatrace. Pour plus d'informations sur la configuration du service fourni par l'utilisateur, voir [DynaTrace Agent Framework](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md).

3. Après avoir envoyé par commande push votre appli à Bluemix, associez le service fourni par l'utilisateur que vous avez créé à cette appli. Utilisez par exemple la commande suivante :

        $ cf bs myApp my-dynatrace-collector
        {: codeblock}

    **Remarque** : Vous devez reconstituer votre application après avoir associé le service.

## Configuration facultative
{: #optional_configuration}

Vous pouvez choisir d'acquérir et d'héberger vous-même le fichier JAR d'agent Dynatrace.  Dans ce cas, les étapes de configuration supplémentaires suivantes sont nécessaires.
1. Procurez-vous et hébergez le fichier JAR d'agent Dynatrace de sorte que le pack de construction Liberty puisse le télécharger.
2. Configurez votre application Liberty de sorte qu'elle puisse télécharger l'agent Dynatrace.

### Hébergement de l'agent Dynatrace
{: #hosting_dynatrace_agent}
L'agent Dynatrace doit être hébergé sur un serveur Web, et le pack de construction liberty doit pouvoir télécharger le fichier JAR d'agent à partir de ce serveur. Le serveur doit être configuré avec un fichier `index.yml` qui indique les détails concernant le fichier JAR d'agent. Pour configurer l'agent Dynatrace, procédez comme suit :
  1. Téléchargez le fichier JAR de l'agent Dynatrace. Pour obtenir les instructions relatives au téléchargement du fichier JAR de l'agent Dynatrace, voir [Dynatrace Server Platform Installers](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace) sur le site Web de la communauté Dynatrace. Le fichier JAR d'agent approprié pour une exécution sur Bluemix est **dynatrace-agent-unix.jar**, version **6.+**.
  2. Hébergez le fichier JAR d'agent dans un emplacement à partir duquel le pack de construction Liberty peut le télécharger. Vous pouvez l'héberger directement sur Bluemix à l'aide des fonctions disponibles sur le serveur, ou vous pouvez l'héberger sur un emplacement disponible publiquement.
     * Prenez soin de fournir un fichier `index.yml` à l'emplacement d'hébergement. Le fichier `index.yml` doit contenir une entrée composée de l'ID de version du fichier JAR d'agent suivi d'un signe deux-points et de l'URL complète de l'emplacement de ce fichier JAR d'agent. Par exemple :

            ---
               6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
            {: codeblock}
     
     * Le fichier **dynatrace-agent-6.3.0-unix.jar** doit être disponible à l'emplacement spécifié dans le fichier `index.yml`. L'emplacement du fichier JAR et celui du fichier `index.yml` peuvent être le même répertoire.

### Configuration de l'appli Liberty
{: #configuring_liberty_app}

L'appli Liberty que vous souhaitez surveiller doit être configurée pour localiser le serveur qui héberge le fichier JAR d'agent que vous avez précédemment configuré. 
Vous pouvez configurer l'appli avec la variable d'environnement **JBP_CONFIG_DYNATRACEAPPMONAGENT**. La variable d'environnement **JBP_CONFIG_DYNATRACEAPPMONAGENT** indique au pack de construction l'emplacement à partir duquel il doit télécharger l'agent Dynatrace. Pour définir la variable d'environnement, procédez comme suit :

1. Affectez à la variable **JBP_CONFIG_DYNATRACEAPPMONAGENT** la valeur *"repository_root: URL_of_server_hosting_index.yml"*. Par exemple, après avoir envoyé par commande push votre application, exécutez la commande suivante :
  
        $ cf se myApp JBP_CONFIG_DYNATRACEAPPMONAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
        {: codeblock}

    Dans cet exemple, *my-dynatrace-agent-host.mybluemix.net* est l'URL du fichier `index.yml` hébergé par le serveur que vous avez précédemment configuré.

2. Après avoir défini la variable d'environnement, reconstituez votre application. Consultez le fichier journal de préproduction (staging). Il doit contenir
un message indiquant le bon déroulement du téléchargement de l'agent Dynatrace à partir du serveur sur lequel il est hébergé. Par exemple :
```
    Downloading dynatrace-agent-6.3.0-unix.jar 6.3.0 from https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)
```
{: codeblock}

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
