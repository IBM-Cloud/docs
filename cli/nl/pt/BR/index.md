---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Ferramentas de CLI e de desenvolvimento
{: #cli}

*Última atualização: 30 de março de 2016*

Com o {{site.data.keyword.Bluemix_short}}, você tem acesso a poderosas ferramentas, tais como uma interface da linha de comandos unificada e plug-ins de CLI. Todos esses downloads de CLI estão disponíveis para suportar sua experiência no {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## ![Interfaces de linha de comandos](./images/CLI.svg) Interfaces de linha de comandos
{: #downloads}

Faça download e instale as interfaces da linha de comandos para suportar sua experiência com o {{site.data.keyword.Bluemix_notm}}. A ferramenta de linha de comandos cf do Cloud Foundry é um pré-requisito para todas as outras ferramentas {{site.data.keyword.Bluemix_notm}} CLI. A ferramenta de linha de comandos do {{site.data.keyword.Bluemix_notm}} fornece experiência estendida para gerenciar seu ambiente {{site.data.keyword.Bluemix_notm}} além dos aplicativos Cloud Foundry.

Ambas as ferramentas da CLI usam a porta 433 por padrão. Se você tiver proxy HTTP entre as ferramentas da CLI e o ambiente {{site.data.keyword.Bluemix_notm}}, deverá configurar a variável de ambiente `http-proxy` com a URL e a porta do proxy HTTP reais, se houver alguma. Veja [Usando a CLI com um servidor proxy HTTP](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window} para obter mais detalhes.


| *{{site.data.keyword.Bluemix_notm}}: bx* | *Cloud Foundry: cf* |
|---------------------|---------------|
| [Fazer download da CLI](http://clis.ng.bluemix.net/) <br> [View Docs](./reference/bluemix_cli/index.html)|  [Fazer download da CLI](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [View Docs](./reference/cfcommands/index.html) |


## ![Plug-ins da interface de linha de comandos](./images/CLI_Plugin.svg) Plug-ins da interface de linha de comandos

Estenda facilmente sua interface de linha de comandos do {{site.data.keyword.Bluemix_notm}} com mais comandos. Para acessar os plug-ins da interface de linha de comandos do {{site.data.keyword.Bluemix_notm}}, veja o [ Repositório de plug-in da CLI](http://plugins.ng.bluemix.net/).

### Amplie a interface da linha de comandos do {{site.data.keyword.Bluemix_notm}}: bx

1. Para instalar plug-ins da CLI do {{site.data.keyword.Bluemix_notm}} a partir do registro do {{site.data.keyword.Bluemix_notm}}, configure o terminal de registro de plug-in:
```
bluemix plugin repo-add bluemix-bx-staging http://plugins.ng.bluemix.net
```
2. Execute o comando a seguir para instalar um
plug-in:
```
bluemix plugin install plugin_name -r bluemix-bx-staging
```

| *{{site.data.keyword.activedeployshort}} CLI* | *{{site.data.keyword.autoscaling}} CLI* | *Grupos de segurança de rede* |
|-----|-----|-----|
| Plug-in name: active-deploy <br> [Visualizar docs](../services/ActiveDeploy/cli.html#cli) | Plug-in name: auto-scaling <br> [View Docs](./plugins/auto-scaling/index.html) |  Nome do plug-in: nsg <br> [Visualizar docs](./plugins/networksecuritygroups/index.html)  |


### Estender sua interface de linha de comandos do Cloud Foundry: cf

1. Para instalar plug-ins da CLI cf a partir do registro do {{site.data.keyword.Bluemix_notm}}, configure o terminal de registro de plug-in:
```
cf add-plugin-repo bluemix-cf-staging http://plugins.ng.bluemix.net
```
2. Execute o comando a seguir para instalar um
plug-in:
```
cf install-plugin plugin_name -r bluemix-cf-staging
```

| *Active Deploy* | *Admin Console* | *Development Mode* |
|-----------------|-----------------|-----------------|
| Plug-in name: active-deploy <br>  [Visualizar docs](../services/ActiveDeploy/cli.html#cli) |  Plug-in name: bluemix-admin <br> [View Docs](../cli/plugins/bluemix_admin/index.html) | Nome do plug-in: dev_mode <br> [View Docs](./plugins/dev_mode/index.html) |

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| Plug-in name: ibm-containers <br> [Visualizar docs](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | Plug-in name: VPN <br> [View Docs](./plugins/vpn/index.html) |

<!-- View docs link for bluemix-admin plug-in cannot go live until December time frame. Check in with Michelle -->


## ![Ferramentas de desenvolvimento integradas](./images/Integrated_Dev_Tools.svg) Ferramentas de desenvolvimento integradas

Faça download e instale os plug-ins para integrar seus serviços do {{site.data.keyword.Bluemix_notm}} favoritos.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Plug-in do Eclipse Egit](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse Plug-in](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse Plug-in](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse Plug-in](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer
Eclipse Plug-in](../services/rules/index.html#rulov002) |
