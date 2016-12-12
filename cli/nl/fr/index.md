---



copyright:

  years: 2015，2016

lastupdated: "2016-10-24"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Interface de ligne de commande et outils de développement
{: #cli}

Avec {{site.data.keyword.Bluemix_short}}, vous avez accès à des outils puissants, tels qu'une interface de ligne de commande (CLI) unifiée et des plug-in CLI. Chacun de ces téléchargements d'interface de ligne de commande est accessible afin d'optimiser votre expérience avec {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## ![](./images/CLI.svg) Interfaces de ligne de commande
{: #downloads}

Téléchargez et installez des interfaces de ligne de commande pour votre expérience
{{site.data.keyword.Bluemix_notm}}.

L'outil de ligne de commande cf Cloud Foundry est un élément prérequis pour tous les outils d'interface de ligne de commande
{{site.data.keyword.Bluemix_notm}}. L'outil de ligne de commande
{{site.data.keyword.Bluemix_notm}} permet de gérer l'environnement {{site.data.keyword.Bluemix_notm}} en plus des applications Cloud
Foundry.

Les deux outils de ligne de commande utilisent par défaut le port 443. Si un proxy HTTP est interposé entre les outils CLI et l'environnement
{{site.data.keyword.Bluemix_notm}}, vous devez configurer la variable d'environnement `http-proxy` en spécifiant l'URL
réelle et le port du proxy HTTP s'il est présent. Voir [Using the CLI with an HTTP Proxy
Server](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window} pour plus d'informations.


| *{{site.data.keyword.Bluemix_notm}} : bx* | *Cloud Foundry : cf* |
|---------------------|---------------|
| [Télécharger l'interface de ligne de commande](http://clis.ng.bluemix.net/) <br> [Afficher la documentation](./reference/bluemix_cli/index.html)|  [Télécharger l'interface de ligne de commande](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [Afficher la documentation](./reference/cfcommands/index.html) |


## ![](./images/CLI_Plugin.svg) Plug-in d'interface de ligne de commande

Etendez facilement votre interface de ligne de commande {{site.data.keyword.Bluemix_notm}} avec des commandes supplémentaires. Pour accéder
aux plug-in de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, voir le
[référentiel de plug-in de l'interface de ligne de commande](https://plugins.ng.bluemix.net/).

### Etendez votre interface de ligne de commande {{site.data.keyword.Bluemix_notm}} : bx
{: cli_bluemix_ext}

* Pour installer des plug-in d'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} depuis le registre {{site.data.keyword.Bluemix_notm}}, définissez le noeud
final du registre des plug-in :

```
bluemix plugin repo-add bluemix-bx https://plugins.ng.bluemix.net
```
{: codeblock}

* Ensuite, exécutez la commande suivante pour installer un plug-in :

```
bluemix plugin install nom_plug-in -r bluemix-bx
```
{: codeblock}


| *{{site.data.keyword.activedeployshort}} interface de ligne de commande* | *{{site.data.keyword.autoscaling}} interface de ligne de commande* | *Network Security Groups* |
|-----|-----|-----|
| Nom du plug-in : active-deploy <br> [Afficher la documentation](/docs/services/ActiveDeploy/cli.html#cli) | Nom du plug-in : auto-scaling <br> [Afficher la documentation](./plugins/auto-scaling/index.html) |  Nom du plug-in : nsg <br> [Afficher la documentation](./plugins/networksecuritygroups/index.html)  |


### Etendez votre interface de ligne de commande Cloud Foundry : cf
{: cli_cf_ext}

* Pour installer des plug-in d'interface de ligne de commande cf depuis le registre {{site.data.keyword.Bluemix_notm}}, définissez le noeud
final du registre des
plug-in :

```
cf add-plugin-repo bluemix-cf https://plugins.ng.bluemix.net
```
{: codeblock}

* Ensuite, exécutez la commande suivante pour installer un plug-in :

```
cf install-plugin nom_plug-in -r bluemix-cf
```
{: codeblock}


| *Active Deploy* | *Console d'administration* |
|-----------------|-----------------|
| Nom du plug-in : active-deploy <br>  [Afficher la documentation](/docs/services/ActiveDeploy/cli.html#cli) |  Nom du plug-in : bluemix-admin <br> [Afficher la documentation](/docs/cli/plugins/bluemix_admin/index.html) |

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *réseau privé virtuel (VPN)* |
|-----------------|-----------------|
| Nom du plug-in : ibm-containers <br> [Afficher la documentation](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | Nom du plug-in : VPN <br> [Afficher la documentation](./plugins/vpn/index.html) |


## ![](./images/Integrated_Dev_Tools.svg) Outils de développement intégrés

Téléchargez et installez des plug-in afin d'intégrer les services {{site.data.keyword.Bluemix_notm}} que
vous préférez.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Plug-in Egit Eclipse](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [Plug-in RTC Eclipse](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Plug-in Liberty Eclipse](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Plug-in Eclipse](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Plug-in Rules Designer Eclipse](/docs/services/rules/index.html#rulov002) |
