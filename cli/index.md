{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI and dev tools
{: #cli}

*Last updated: 16 February 2016*

With {{site.data.keyword.Bluemix_short}}, you have access to powerful tools such as a unified command line interface and CLI plug-ins. Each of these CLI downloads are all available to support your {{site.data.keyword.Bluemix_notm}} experience.
{:shortdesc}

## ![Command line interfaces](./images/CLI.svg) Command line interfaces
{: #downloads}

Download and install command line interfaces to support your {{site.data.keyword.Bluemix_notm}} experience. The Cloud Foundry cf command line tool is a prerequisite for all other {{site.data.keyword.Bluemix_notm}} CLI tools. {{site.data.keyword.Bluemix_notm}} command line tool provides extended experience to manage your {{site.data.keyword.Bluemix_notm}} environment besides Cloud Foundry applications.

| *{{site.data.keyword.Bluemix_notm}}: bx* | *Cloud Foundry: cf* |
|---------------------|---------------|
| [Download CLI](http://clis.{DomainName}/) <br> [View Docs](./reference/bluemix_cli/index.html)|  [Download CLI](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [View Docs](./reference/cfcommands/index.html) |

<!-- audience blue staging only begin comment -->

|*{{site.data.keyword.Bluemix_notm}}: cloud-cli* |  
|---------------|
| [Mac Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/cloud-cli/Bluemix_cloud_cli.pkg){: new_window} <br> [Windows Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/cloud-cli/Bluemix_cloud_cli.exe){: new_window} <br> [Linux Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/cloud-cli/Bluemix_cloud_cli_linux_64.tar.gz){: new_window} <br> [View Docs](#cloudcli) | 

<!-- audience blue staging only end comment -->


## ![Command line interface plug-ins](./images/CLI_Plugin.svg) Command line interface plug-ins

Easily extend your {{site.data.keyword.Bluemix_notm}} command line interface with more commands. To access the {{site.data.keyword.Bluemix_notm}} command line interface plug-ins, see the [CLI Plug-in Repository](http://plugins.{DomainName}/).

### Extend your {{site.data.keyword.Bluemix_notm}} command line interface: bx

1. To install {{site.data.keyword.Bluemix_notm}} CLI plug-ins from the {{site.data.keyword.Bluemix_notm}} registry, set the plug-in registry endpoint:
```
bluemix plugin repo-add bluemix-bx-staging http://plugins.stage1.ng.bluemix.net
```
2. Run the following command to install a plug-in:
```
bluemix plugin install plugin_name -r bluemix-bx-staging
```

| *{{site.data.keyword.activedeployshort}} CLI* | *{{site.data.keyword.autoscaling}} CLI* | *Catalog Manager*  |
|-----|-----|-----|
| Plug-in name: active-deploy <br> [View Docs](../services/ActiveDeploy/cli.html#cli) | Plug-in name: auto-scaling <br> [View Docs](./plugins/auto-scaling/index.html) | Plug-in name: catalog-manager  <br> [View Docs](./plugins/catalogmanager/index.html) |

| *Network Security Groups* |  *VPN*  |
|-----|-----|
| Plug-in name: network-security-groups <br> [View Docs](./plugins/networksecuritygroups/index.html) | Plug-in name: VPN  <br> [View Docs](./plugins/bx_vpn/index.html) |


### Extend your Cloud Foundry command line interface: cf

1. To install cf CLI plug-ins from the {{site.data.keyword.Bluemix_notm}} registry, set the plug-in registry endpoint:
```
cf add-plugin-repo bluemix-cf-staging http://plugins.stage1.ng.bluemix.net
```
2. Run the following command to install a plug-in:
```
cf install-plugin plugin_name -r bluemix-cf-staging
```

| *Active Deploy* | *Admin Console* | *Development Mode* |
|-----------------|-----------------|-----------------|
| Plug-in name: active-deploy <br>  [View Docs](../services/ActiveDeploy/cli.html#cli) |  Plug-in name: bluemix-admin <br> [View Docs](../cli/plugins/bluemix_admin/index.html) | Plug-in name: dev_mode <br> [View Docs](./plugins/dev_mode/index.html) |

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| Plug-in name: ibm-containers <br> [View Docs](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | Plug-in name: VPN <br> [View Docs](./plugins/vpn/index.html) |

<!-- View docs link for bluemix-admin plug-in cannot go live until December time frame. Check in with Michelle -->


## ![Integrated development tools](./images/Integrated_Dev_Tools.svg) Integrated development tools

Download and install plug-ins to integrate your favorite {{site.data.keyword.Bluemix_notm}} services.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Egit Eclipse Plug-in](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse Plug-in](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse Plug-in](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse Plug-in](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse Plug-in](../services/rules/index.html#rulov002) |
