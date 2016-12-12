---



copyright:

  years: 2015，2016

lastupdated: "2016-10-24"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Ferramentas de CLI e de desenvolvimento
{: #cli}

Com o {{site.data.keyword.Bluemix_short}}, você tem acesso a poderosas ferramentas, tais como uma interface da linha de comandos unificada e plug-ins de CLI. Todos esses downloads de CLI estão disponíveis para suportar sua experiência no {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## ![](./images/CLI.svg) Interfaces da linha de comandos
{: #downloads}

Faça download e instale as interfaces da linha de comandos para suportar sua experiência com o {{site.data.keyword.Bluemix_notm}}.

A ferramenta de linha de comandos cf do Cloud Foundry é um pré-requisito para todas as ferramentas da CLI do {{site.data.keyword.Bluemix_notm}}. A ferramenta de linha de comandos do {{site.data.keyword.Bluemix_notm}} fornece experiência estendida para gerenciar seu ambiente {{site.data.keyword.Bluemix_notm}} além dos aplicativos Cloud Foundry.

Ambas as ferramentas da CLI usam a porta 443 por padrão. Se você tiver proxy HTTP entre as ferramentas da CLI e o ambiente {{site.data.keyword.Bluemix_notm}}, deverá configurar a variável de ambiente `http-proxy` com a URL e a porta do proxy HTTP reais, se houver alguma. Veja [Usando a CLI com um servidor proxy HTTP](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window} para obter mais detalhes.


| *{{site.data.keyword.Bluemix_notm}}: bx* | *Cloud Foundry: cf* |
|---------------------|---------------|
| [Fazer download da CLI](http://clis.ng.bluemix.net/) <br> [View Docs](./reference/bluemix_cli/index.html)|  [Fazer download da CLI](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [View Docs](./reference/cfcommands/index.html) |


## ![](./images/CLI_Plugin.svg) Plug-ins da interface de linha de comandos

Estenda facilmente sua interface de linha de comandos do {{site.data.keyword.Bluemix_notm}} com mais comandos. Para acessar os plug-ins da interface de linha de comandos do
{{site.data.keyword.Bluemix_notm}}, consulte o [Repositório de plug-in da CLI](https://plugins.ng.bluemix.net/).

### Amplie a interface da linha de comandos do {{site.data.keyword.Bluemix_notm}}: bx
{: cli_bluemix_ext}

* Para instalar plug-ins da CLI do {{site.data.keyword.Bluemix_notm}} a partir do registro do {{site.data.keyword.Bluemix_notm}}, configure o terminal de registro de plug-in:

```
bluemix plugin repo-add bluemix-bx https://plugins.ng.bluemix.net
```
{: codeblock}

* Em seguida, execute o comando a seguir para instalar um plug-in:

```
bluemix plugin install plugin_name -r bluemix-bx
```
{: codeblock}


| *{{site.data.keyword.activedeployshort}} CLI* | *{{site.data.keyword.autoscaling}} CLI* | *Grupos de segurança de rede* |
|-----|-----|-----|
| Plug-in name: active-deploy <br> [Visualizar docs](/docs/services/ActiveDeploy/cli.html#cli) | Plug-in name: auto-scaling <br> [View Docs](./plugins/auto-scaling/index.html) |  Nome do plug-in: nsg <br> [Visualizar docs](./plugins/networksecuritygroups/index.html)  |


### Estender sua interface de linha de comandos do Cloud Foundry: cf
{: cli_cf_ext}

* Para instalar plug-ins da CLI cf a partir do registro do {{site.data.keyword.Bluemix_notm}}, configure o terminal de registro de plug-in:

```
cf add-plugin-repo bluemix-cf https://plugins.ng.bluemix.net
```
{: codeblock}

* Em seguida, execute o comando a seguir para instalar um plug-in:

```
cf install-plugin plugin_name -r bluemix-cf
```
{: codeblock}


| *Active Deploy* | *Admin Console* |
|-----------------|-----------------|
| Plug-in name: active-deploy <br>  [Visualizar docs](/docs/services/ActiveDeploy/cli.html#cli) |  Plug-in name: bluemix-admin <br> [Visualizar docs](/docs/cli/plugins/bluemix_admin/index.html) |

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| Plug-in name: ibm-containers <br> [Visualizar docs](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | Plug-in name: VPN <br> [View Docs](./plugins/vpn/index.html) |


## ![](./images/Integrated_Dev_Tools.svg) Ferramentas de desenvolvimento integradas

Faça download e instale os plug-ins para integrar seus serviços do {{site.data.keyword.Bluemix_notm}} favoritos.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Plug-in do Eclipse Egit](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse Plug-in](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse Plug-in](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse Plug-in](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer
Eclipse Plug-in](/docs/services/rules/index.html#rulov002) |
