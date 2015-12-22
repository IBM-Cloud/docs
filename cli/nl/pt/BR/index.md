{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Ferramentas CLI e de desenvolvimento
{: #cli}

*Última atualização: 10 de novembro de 2015*

Ferramentas poderosas do {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

## ![Interfaces de linha de comandos](./images/CLI.png) Interfaces de linha de comandos
{: #downloads}

Faça download e instale as interfaces da linha de comandos para suportar sua experiência com o {{site.data.keyword.Bluemix_notm}}. A interface da linha de comandos Cloud Foundry cf
é um pré-requisito para todas as outras ferramentas CLI do {{site.data.keyword.Bluemix_notm}}.


| *Cloud Foundry: cf* |	*{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}: ICE* | *{{site.data.keyword.Bluemix_notm}} Live Sync:
bl* |
|---------------------|---------------|---------------|
| [Fazer download da CLI](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [View Docs](./reference/cfcommands/index.html) |[Fazer download do Docker](https://docs.docker.com/installation/){: new_window} <br> [Mac Installer do ICE](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.pkg){: new_window} <br> [Windows Installer do ICE](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.exe){: new_window} <br> [Linux Installer do ICE](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.tar.gz){: new_window} <br> [Visualizar docs](../containers/container_cli_ice_ov.html) | [Mac Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.pkg){: new_window} <br> [Windows Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.exe){: new_window} <br> [View Docs](./reference/bl/index.html) |


## ![Plug-ins da interface de linha de comandos](./images/CLI_Plugin.png) Plug-ins da interface de linha de comandos

Estenda facilmente sua interface de linha de comandos do {{site.data.keyword.Bluemix_notm}} com mais comandos. Para acessar os plug-ins da interface de linha de comandos do {{site.data.keyword.Bluemix_notm}}, veja o [{{site.data.keyword.Bluemix_notm}} Repositório de plug-in da CLI](http://plugins.{DomainName}/){: new_window}.

1. Para instalar plug-ins da CLI cf a partir do registro do {{site.data.keyword.Bluemix_notm}}, configure o terminal de registro de plug-in:
```
cf add-plugin-repo bluemix-cf-staging http://plugins.ng.bluemix.net
```
2. Execute o comando a seguir para instalar um
plug-in:
```
cf install-plugin plugin_name -r bluemix-cf-staging
```

| *Active Deploy* |  *Development Mode* | 
|-----------------|-----------------|
| Plug-in name: active-deploy <br>  [View Docs](../services/ActiveDeploy/index.html#cli) |  Nome do plug-in: development-name <br> [View Docs](./plugins/dev_mode/index.html) | 

### Estender sua interface de linha de comandos do {{site.data.keyword.Bluemix_notm}}: bx
1. Para instalar plug-ins da CLI do {{site.data.keyword.Bluemix_notm}} a partir do registro do {{site.data.keyword.Bluemix_notm}}, configure o terminal de registro de plug-in:
```
bluemix plugin repo-add bluemix-bx-staging http://plugins.ng.bluemix.net
```
2. Execute o comando a seguir para instalar um
plug-in:
```
bluemix plugin install plugin_name -r bluemix-bx-staging
```

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* |
|-----|
| Plug-in name: ibm-containers <br> [View Docs](https://www.{{DomainName}}/docs/containers/container_cli_cfic.html#container_cli_cfic) |

## ![Ferramentas de desenvolvimento integradas](./images/Integrated_Dev_Tools.png) Ferramentas de desenvolvimento integradas


Faça download e instale os plug-ins para integrar seus serviços do {{site.data.keyword.Bluemix_notm}} favoritos.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Plug-in do Eclipse Egit](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse Plug-in](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse Plug-in](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse Plug-in](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer
Eclipse Plug-in](../services/rules/index.html#rulov002) |
