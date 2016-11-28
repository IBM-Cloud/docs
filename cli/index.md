---



copyright:

  years: 2015，2016

lastupdated: "2016-11-28"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI and dev tools
{: #cli}

With {{site.data.keyword.Bluemix_short}}, you have access to powerful tools such as a unified command line interface and CLI plug-ins. Each of these CLI downloads are all available to support your {{site.data.keyword.Bluemix_notm}} experience.
{:shortdesc}

## ![](./images/CLI.svg) Command line interfaces
{: #downloads}

Download and install command line interfaces to support your {{site.data.keyword.Bluemix_notm}} experience.

The Cloud Foundry cf command line tool is a prerequisite for all {{site.data.keyword.Bluemix_notm}} CLI tools. {{site.data.keyword.Bluemix_notm}} command line tool provides extended experience to manage your {{site.data.keyword.Bluemix_notm}} environment besides Cloud Foundry applications.

Both CLI tools use 443 port by default. If you have HTTP proxy between the CLI tools and {{site.data.keyword.Bluemix_notm}} environment, you must configure the  `http-proxy` environment variable with the actual HTTP proxy url and port if there is any. See [Using the CLI with an HTTP Proxy Server](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window} for more details.


| *{{site.data.keyword.Bluemix_notm}}: bx* | *Cloud Foundry: cf* |
|---------------------|---------------|
| [Download CLI](http://clis.ng.bluemix.net/) <br> [View Docs](./reference/bluemix_cli/index.html)|  [Download CLI](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [View Docs](./reference/cfcommands/index.html) |


## ![](./images/CLI_Plugin.svg) Command line interface plug-ins

Easily extend your {{site.data.keyword.Bluemix_notm}} command line interface with more commands. To access the {{site.data.keyword.Bluemix_notm}} command line interface plug-ins, see the [CLI Plug-in Repository](https://plugins.ng.bluemix.net/).

### Extend your {{site.data.keyword.Bluemix_notm}} command line interface: bx
{: cli_bluemix_ext}

* To install {{site.data.keyword.Bluemix_notm}} CLI plug-ins from the {{site.data.keyword.Bluemix_notm}} registry, set the plug-in registry endpoint:

```
bluemix plugin repo-add bluemix-bx https://plugins.ng.bluemix.net
```
{: codeblock}

* Then, run the following command to install a plug-in:

```
bluemix plugin install plugin_name -r bluemix-bx
```
{: codeblock}


| *{{site.data.keyword.activedeployshort}} CLI* | *{{site.data.keyword.autoscaling}} CLI* | *IBM Containers*  |
|-----|-----|-----|
| Plug-in name: active-deploy <br> [View Docs](/docs/services/ActiveDeploy/cli.html#cli) | Plug-in name: auto-scaling <br> [View Docs](/docs/plugins/auto-scaling/index.html) |  Plug-in name: IBM-Containers  <br> [View Docs](/docs/plugins/containers/index.html) |

| *Network Security Groups* |  *Private network peering* | *VPN*  |  
|-----|-----|-----|
| Plug-in name: network-security-groups <br> [View Docs](/docs/plugins/networksecuritygroups/index.html) | Plug-in name: private-network-peering  <br> [View Docs](/docs/plugins/pnp/index.html) |Plug-in name: VPN  <br> [View Docs](/docs/plugins/bx_vpn/index.html) |


### Extend your Cloud Foundry command line interface: cf
{: cli_cf_ext}

* To install cf CLI plug-ins from the {{site.data.keyword.Bluemix_notm}} registry, set the plug-in registry endpoint:

```
cf add-plugin-repo bluemix-cf https://plugins.ng.bluemix.net
```
{: codeblock}

* Then, run the following command to install a plug-in:

```
cf install-plugin plugin_name -r bluemix-cf
```
{: codeblock}


| *Active Deploy* | *Admin Console* |
|-----------------|-----------------|
| Plug-in name: active-deploy <br>  [View Docs](/docs/services/ActiveDeploy/cli.html#cli) |  Plug-in name: bluemix-admin <br> [View Docs](/docs/cli/plugins/bluemix_admin/index.html) |

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| Plug-in name: ibm-containers <br> [View Docs](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | Plug-in name: VPN <br> [View Docs](./plugins/vpn/index.html) |


## ![](./images/Integrated_Dev_Tools.svg) Integrated development tools

Download and install plug-ins to integrate your favorite {{site.data.keyword.Bluemix_notm}} services.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Egit Eclipse Plug-in](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse Plug-in](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse Plug-in](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse Plug-in](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse Plug-in](/docs/services/rules/index.html#rulov002) |
