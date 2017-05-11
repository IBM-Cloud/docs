---



copyright:

  years: 2015, 2017

lastupdated: "2017-02-14"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Téléchargements
{: #cli}

Avec {{site.data.keyword.Bluemix_short}}, vous avez accès à des outils puissants, tels qu'une interface de ligne de commande (CLI) unifiée et des plug-in CLI. Chacun de ces téléchargements d'interface de ligne de commande est accessible afin d'optimiser votre expérience avec {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## ![](./images/CLI.svg) Interface de ligne de commande
{: #downloads notoc}

Téléchargez et installez l'outil de ligne de commande pour permettre la prise en charge de votre expérience {{site.data.keyword.Bluemix_notm}}

L'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} fournit une expérience de ligne de commande permettant de gérer votre environnement {{site.data.keyword.Bluemix_notm}}. Elle inclut également une interface de ligne de commande Cloud Foundry, cf, dans son installation, pour la gestion des applications et des services Cloud Foundry.  

Les deux outils de ligne de commande utilisent par défaut le port 443. Si un proxy HTTP est interposé entre les outils CLI et l'environnement {{site.data.keyword.Bluemix_notm}}, vous devez configurer la variable d'environnement `HTTP_PROXY` en spécifiant l'URL réelle et le port du proxy HTTP s'il est présent. Pour plus de détails, voir [Using the CLI with an HTTP Proxy Server ![icône de lien externe](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window}.

[Télécharger l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../icons/launch-glyph.svg)](http://clis.ng.bluemix.net/){: new_window} <br> 
[Afficher la documentation](/docs/cli/reference/bluemix_cli/index.html)

## ![](./images/CLI_Plugin.svg) Plug-in d'interface de ligne de commande
{: #cliplugins notoc}

Etendez facilement votre interface de ligne de commande {{site.data.keyword.Bluemix_notm}} avec des commandes supplémentaires. Pour accéder aux plug-in de l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, voir le [référentiel de plug-in de l'interface de ligne de commande![icône de lien externe](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window}.

### Etendez votre interface de ligne de commande {{site.data.keyword.Bluemix_notm}} : bx
{: #cli_bluemix_ext notoc}


Après l'installation de l'outil d'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}, le [référentiel de plug-in d'interface de ligne de commande ![Icône de lien externe](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window} est pré-configuré avec un alias de référentiel `Bluemix` par défaut. Vous pouvez installer directement les plug-ins disponibles.

```
bluemix plugin install plugin_name -r Bluemix
```

| *{{site.data.keyword.activedeployshort}} interface de ligne de commande* | *{{site.data.keyword.autoscaling}} interface de ligne de commande* | *Service IBM Bluemix Container*  |
|-----|-----|-----|
| Nom du plug-in : active-deploy <br> [Afficher la documentation](/docs/services/ActiveDeploy/cli.html#cli) | Nom du plug-in : auto-scaling <br> [Afficher la documentation](/docs/cli/plugins/auto-scaling/index.html) | Nom du plug-in : container-service  <br> [Afficher la documentation](/docs/containers/cs_cli_devtools.html) |
{: caption="Tableau 2. Plug-ins" caption-side="top"}

|  *Appairage de réseaux privés* | *réseau privé virtuel (VPN)*  |
|-----|-----|
| Nom du plug-in : private-network-peering  <br> [Afficher la documentation](/docs/cli/plugins/pnp/index.html) | Nom du plug-in : VPN  <br> [Afficher la documentation](/docs/cli/plugins/bx_vpn/index.html) |
{: caption="Tableau 3. Plug-ins" caption-side="top"}

Vous pouvez également ajouter des plug-ins à partir d'autres référentiels conformes à l'architecture d'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}.  
1. Pour installer des plug-ins d'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} depuis un autre référentiel, définissez le noeud
final du registre des plug-ins : 
```
bluemix plugin repo-add bluemix-other-repo [repo_url]
```
où `repo_url` est l'URL HTTPS du référentiel de plug-ins.

2. Exécutez la commande suivante pour installer un plug-in :
```
bluemix plugin install plugin_name -r bluemix-other-repo
```


### Etendez l'interface de ligne de commande Cloud Foundry : bx cf
{: #cli_cf_ext notoc}

Après l'installation de l'outil de ligne de commande {{site.data.keyword.Bluemix_notm}}, une interface de ligne de commande Cloud Foundry est également installée dans le répertoire d'interface de ligne de commande Bluemix. Exécutez les commandes d'interface de ligne de commande Cloud Foundry à l'aide de `bluemix cf`.

* Pour installer des plug-ins d'interface de ligne de commande cf depuis le registre {{site.data.keyword.Bluemix_notm}}, définissez le noeud
final du registre des
plug-ins :

```
bluemix cf add-plugin-repo bluemix-cf-repo https://plugins.ng.bluemix.net
```
{: codeblock}

* Ensuite, exécutez la commande suivante pour installer un plug-in :

```
bluemix cf install-plugin plugin_name -r bluemix-cf-repo
```
{: codeblock}

| *Active Deploy* | *Console d'administration* |
|-----------------|-----------------|
| Nom du plug-in : active-deploy <br>  [Afficher la documentation](/docs/services/ActiveDeploy/cli.html#cli) |  Nom du plug-in : bluemix-admin <br> [Afficher la documentation](/docs/cli/plugins/bluemix_admin/index.html) |
{: caption="Tableau 4. Plug-ins" caption-side="top"}

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *réseau privé virtuel (VPN)* |
|-----------------|-----------------|
| Nom du plug-in : ibm-containers <br> [Afficher la documentation ![Icône de lien externe](../icons/launch-glyph.svg)](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic){: new_window} | Nom du plug-in : VPN <br> [Afficher la documentation](/docs/cli/plugins/vpn/index.html) |
{: caption="Tableau 5. Plug-ins" caption-side="top"}

## ![](./images/Integrated_Dev_Tools.svg) Outils de développement intégrés
{: #ide notoc}

Téléchargez et installez des plug-in afin d'intégrer les services {{site.data.keyword.Bluemix_notm}} que
vous préférez.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* | *API Connect* | *Eclipse Tools for Bluemix* |
|-------------|----------|----------|----------|----------|----------|
| [Egit Eclipse Plug-in ![icône de lien externe](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window}  <br> [RTC Eclipse Plug-in ![icône de lien externe](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse Plug-in ![icône de lien externe](../icons/launch-glyph.svg)](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse Plug-in ![icône de lien externe](../icons/launch-glyph.svg)](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Plug-in Rules Designer Eclipse](../services/rules/index.html#rulov002) | [Developer Toolkit ![Icône de lien externe](../icons/launch-glyph.svg)](https://nextstage.torolab.ibm.com/apimanagement/getting-started/ ){: new_window} | [Plug-in Bluemix Eclipse](/docs/manageapps/eclipsetools/eclipsetools.html) |
{: caption="Tableau 6. Plug-ins" caption-side="top"}
