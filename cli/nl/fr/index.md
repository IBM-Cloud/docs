---



copyright:

  years: 2015，2017

lastupdated: "2017-01-12"


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

L'outil de ligne de commande cf Cloud Foundry est un élément prérequis pour tous les outils d'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}. L'outil de ligne de commande {{site.data.keyword.Bluemix_notm}} permet de gérer l'environnement {{site.data.keyword.Bluemix_notm}} en plus des applications Cloud
Foundry.

Les deux outils de ligne de commande utilisent par défaut le port 443. Si un proxy HTTP est interposé entre les outils CLI et l'environnement {{site.data.keyword.Bluemix_notm}}, vous devez configurer la variable d'environnement `http-proxy` en spécifiant l'URL réelle et le port du proxy HTTP s'il est présent. Pour plus de détails, voir [Using the CLI with an HTTP Proxy Server ![icône de lien externe](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window}.


| *{{site.data.keyword.Bluemix_notm}} : bx* | *Cloud Foundry : cf* |
|---------------------|---------------|
| [Télécharger l'interface de ligne de commande](http://clis.ng.bluemix.net/) <br> [Afficher la documentation](/docs/cli/reference/bluemix_cli/index.html)|  [Télécharger l'interface de ligne de commande ![icône de lien externe ](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [Afficher la documentation](/docs/cli/reference/cfcommands/index.html) |
{: caption="Table 1. CLI download" caption-side="top"}


## ![](./images/CLI_Plugin.svg) Plug-in d'interface de ligne de commande

Etendez facilement votre interface de ligne de commande {{site.data.keyword.Bluemix_notm}} avec des commandes supplémentaires. Pour accéder aux plug-in de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, voir le [référentiel de plug-in de l'interface de ligne de commande![icône de lien externe](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/).

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


| *{{site.data.keyword.activedeployshort}} interface de ligne de commande* | *{{site.data.keyword.autoscaling}} interface de ligne de commande* | *Service IBM Bluemix Container*  |
|-----|-----|-----|
| Nom du plug-in : active-deploy <br> [Afficher la documentation](/docs/services/ActiveDeploy/cli.html#cli) | Nom du plug-in : auto-scaling <br> [Afficher la documentation](/docs/cli/plugins/auto-scaling/index.html) |  Nom du plug-in : container-service  <br> [Afficher la documentation](/docs/containers/cs_cli_devtools.html) |
{: caption="Table 2. Plug-ins" caption-side="top"}

|  *Appairage de réseaux privés* | *réseau privé virtuel (VPN)*  |
|-----|-----|
| Nom du plug-in : private-network-peering  <br> [Afficher la documentation](/docs/cli/plugins/pnp/index.html) |Nom du plug-in : VPN  <br> [Afficher la documentation](/docs/cli/plugins/bx_vpn/index.html) |
{: caption="Table 3. Plug-ins" caption-side="top"}


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
{: caption="Table 4. Plug-ins" caption-side="top"}


| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *réseau privé virtuel (VPN)* |
|-----------------|-----------------|
| Nom du plug-in : ibm-containers <br> [Afficher la documentation](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | Nom du plug-in : VPN <br> [Afficher la documentation](/docs/cli/plugins/vpn/index.html) |
{: caption="Table 5. Plug-ins" caption-side="top"}


## ![](./images/Integrated_Dev_Tools.svg) Outils de développement intégrés

Téléchargez et installez des plug-in afin d'intégrer les services {{site.data.keyword.Bluemix_notm}} que
vous préférez.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* | *Eclipse Tools for Bluemix* |
|-------------|----------|----------|----------|----------|
| [Egit Eclipse Plug-in ![icône de lien externe](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse Plug-in ![icône de lien externe](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse Plug-in ![icône de lien externe](../icons/launch-glyph.svg)](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse Plug-in ![icône de lien externe](../icons/launch-glyph.svg)](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse Plug-in ![icône de lien externe](../icons/launch-glyph.svg)](/docs/services/rules/index.html#rulov002) | [Bluemix Eclipse Plug-in ![icône de lien externe](../icons/launch-glyph.svg)](https://console.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){: new_window} |
{: caption="Table 6. Plug-ins" caption-side="top"}
