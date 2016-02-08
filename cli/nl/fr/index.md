{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Interface de ligne de commande et outils de développement
{: #cli}

*Dernière mise à jour : 19 janvier 2016*

Avec {{site.data.keyword.Bluemix_short}}, vous avez accès à des outils puissants, tels qu'une interface de ligne de commande (CLI) unifiée et des plug-in CLI. Chacun de ces téléchargements d'interface de ligne de commande est accessible afin d'optimiser votre expérience avec {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## ![Interfaces de ligne de commande](./images/CLI.png) Interfaces de ligne de commande
{: #downloads}

Téléchargez et installez des interfaces de ligne de commande pour votre expérience
{{site.data.keyword.Bluemix_notm}}. L'interface de ligne de commande cf Cloud Foundry constitue un élément
prérequis pour tous les autres outils d'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.


| *Cloud Foundry : cf* |	*{{site.data.keyword.Bluemix_notm}} : bx* | 
|---------------------|---------------|
| [Télécharger l'interface de ligne de commande](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [Afficher la documentation](./reference/cfcommands/index.html) | [Télécharger l'interface de ligne de commande](http://clis.{DomainName}/){: new_window} <br> [Afficher la documentation](./reference/bluemix_cli/index.html)| 

| *{{site.data.keyword.Bluemix_notm}} Live Sync : bl* |
|---------------|---------------|
| [Programme
d'installation Mac](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.pkg){: new_window} <br> [Programme d'installation Windows](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.exe){: new_window} <br> [Afficher la documentation](./reference/bl/index.html) |


## ![Plug-in d'interface de ligne de commande](./images/CLI_Plugin.png) Plug-in d'interface de ligne de commande

Etendez facilement votre interface de ligne de commande {{site.data.keyword.Bluemix_notm}} avec des commandes supplémentaires. Pour accéder
aux plug-in de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, voir le
[référentiel de plug-in de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](http://plugins.{DomainName}/){: new_window}.

1. Pour installer des plug-in d'interface de ligne de commande cf depuis le registre {{site.data.keyword.Bluemix_notm}}, définissez le noeud
final du registre des
plug-in :
```
cf add-plugin-repo bluemix-cf http://plugins.ng.bluemix.net
```
2. Exécutez la commande suivante pour installer un plug-in :
```
cf install-plugin nom_plug-in -r bluemix-cf
```

| *Active Deploy* | *Console d'administration* | *Mode développement* | 
|-----------------|-----------------|-----------------|
| Nom du plug-in : active-deploy <br>  [Afficher la documentation](../services/ActiveDeploy/index.html#cli) |  Nom du plug-in : bluemix-admin <br> [Afficher la documentation](../cli/plugins/bluemix_admin/index.html) | Nom du plug-in :
development-name <br> [Afficher la documentation](./plugins/dev_mode/index.html) | 

### Etendez votre interface de ligne de commande {{site.data.keyword.Bluemix_notm}} : bx
1. Pour installer des plug-in d'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} depuis le registre {{site.data.keyword.Bluemix_notm}}, définissez le noeud
final du registre des plug-in :
```
bluemix plugin repo-add bluemix-bx http://plugins.ng.bluemix.net
```
2. Exécutez la commande suivante pour installer un plug-in :
```
bluemix plugin install nom_plug-in -r bluemix-bx
```

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *{{site.data.keyword.autoscaling}} interface CLI* | *réseau privé virtuel (VPN)* |
|-----|----|----|
| Nom du plug-in : ibm-containers <br> [Afficher la documentation](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | Nom du plug-in : auto-scaling <br> [Afficher la documentation](./plugins/auto-scaling/index.html) |Nom du plug-in : VPN <br> [Afficher la documentation](./plugins/vpn/index.html) |

## ![Outils de développement intégrés](./images/Integrated_Dev_Tools.png) Outils de développement intégrés


Téléchargez et installez des plug-in afin d'intégrer les services {{site.data.keyword.Bluemix_notm}} que
vous préférez.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Plug-in Egit Eclipse](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [Plug-in RTC Eclipse](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Plug-in
Liberty Eclipse](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Plug-in
Eclipse](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Plug-in Rules Designer Eclipse](../services/rules/index.html#rulov002) |
