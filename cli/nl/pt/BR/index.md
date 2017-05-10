---



copyright:

  years: 2015, 2017

lastupdated: "2017-02-14"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Downloads
{: #cli}

Com o {{site.data.keyword.Bluemix_short}}, você tem acesso a poderosas ferramentas, tais como uma interface da linha de comandos unificada e plug-ins de CLI. Todos esses downloads de CLI estão disponíveis para suportar sua experiência no {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## ![](./images/CLI.svg) Interface da linha de comandos
{: #downloads notoc}

Faça download e instale a ferramenta de linha de comandos para suportar sua experiência com o {{site.data.keyword.Bluemix_notm}}.

A CLI do {{site.data.keyword.Bluemix_notm}} fornece uma experiência de linha de comandos para gerenciar seu ambiente {{site.data.keyword.Bluemix_notm}}. Ela também inclui uma interface da linha de comandos Cloud Foundry, cf, em sua instalação, para gerenciar aplicativos e serviços do Cloud Foundry. 

Ambas as ferramentas da CLI usam a porta 443 por padrão. Se você tem o proxy HTTP entre as ferramentas da CLI e o ambiente {{site.data.keyword.Bluemix_notm}}, deve-se configurar a variável de ambiente `HTTP_PROXY` com a URL e a porta do proxy HTTP reais, se houver alguma. Veja [Usando a CLI com um Servidor proxy HTTP ![Ícone de link externo](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window} para obter mais detalhes.

[Fazer download da CLI do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg)](http://clis.ng.bluemix.net/){: new_window} <br> 
[Visualizar docs](/docs/cli/reference/bluemix_cli/index.html)

## ![](./images/CLI_Plugin.svg) Plug-ins da interface de linha de comandos
{: #cliplugins notoc}

Estenda facilmente sua interface de linha de comandos do {{site.data.keyword.Bluemix_notm}} com mais comandos. Para acessar os plug-ins da interface da linha de comandos do {{site.data.keyword.Bluemix_notm}}, veja o [Repositório de plug-in da CLI ![Ícone de link externo](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window}.

### Amplie a interface da linha de comandos do {{site.data.keyword.Bluemix_notm}}: bx
{: #cli_bluemix_ext notoc}


Depois de instalar a ferramenta cli do {{site.data.keyword.Bluemix_notm}}, o [Repositório de plug-in da CLI ![Ícone de link externo](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window} é pré-configurado com um alias de repositório `Bluemix` por padrão. É possível instalar plug-ins disponíveis diretamente.

```
bluemix plugin install plugin_name -r Bluemix
```

| *{{site.data.keyword.activedeployshort}} CLI* | *{{site.data.keyword.autoscaling}} CLI* | *IBM Bluemix Container Service*  |
|-----|-----|-----|
| Plug-in name: active-deploy <br> [View Docs](/docs/services/ActiveDeploy/cli.html#cli) | Plug-in name: auto-scaling <br> [View Docs](/docs/cli/plugins/auto-scaling/index.html) | Plug-in name: container-service  <br> [View Docs](/docs/containers/cs_cli_devtools.html) |
{: caption="Tabela 2. Plug-ins" caption-side="top"}

|  *Peer de rede privada* | *VPN*  |
|-----|-----|
| Nome do plug-in:
private-network-peering  <br> [Visualizar docs](/docs/cli/plugins/pnp/index.html) | Plug-in name: VPN  <br> [Visualizar docs](/docs/cli/plugins/bx_vpn/index.html) |
{: caption="Tabela 3. Plug-ins" caption-side="top"}

Também é possível incluir plug-ins de outros repositórios que obedeçam à arquitetura de cli do {{site.data.keyword.Bluemix_notm}}.
1. Para instalar plug-ins da CLI do {{site.data.keyword.Bluemix_notm}} de outro repositório, configure o terminal de registro de plug-in:
```
bluemix plugin repo-add bluemix-other-repo [repo_url]
```
em que `repo_url` é a URL de HTTPS do repositório de plug-in.

2. Execute o comando a seguir para instalar um
plug-in:
```
bluemix plugin install plugin_name -r bluemix-other-repo
```


### Estender a interface da linha de comandos do Cloud Foundry: bx cf
{: #cli_cf_ext notoc}

Depois de instalar a ferramenta de linha de comandos do {{site.data.keyword.Bluemix_notm}}, uma interface da linha de comandos do Cloud Foundry também é instalada dentro do diretório da CLI do Bluemix. Execute os comandos da CLI do Cloud Foundry usando `bluemix cf`.

* Para instalar plug-ins da CLI cf a partir do registro do {{site.data.keyword.Bluemix_notm}}, configure o terminal de registro de plug-in:

```
bluemix cf add-plugin-repo bluemix-cf-repo https://plugins.ng.bluemix.net
```
{: codeblock}

* Em seguida, execute o comando a seguir para instalar um plug-in:

```
bluemix cf install-plugin plugin_name -r bluemix-cf-repo
```
{: codeblock}

| *Active Deploy* | *Admin Console* |
|-----------------|-----------------|
| Plug-in name: active-deploy <br>  [View Docs](/docs/services/ActiveDeploy/cli.html#cli) |  Plug-in name: bluemix-admin <br> [View Docs](/docs/cli/plugins/bluemix_admin/index.html) |
{: caption="Tabela 4. Plug-ins" caption-side="top"}

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| Plug-in name: ibm-containers <br> [Visualizar docs ![Ícone de link externo](../icons/launch-glyph.svg)](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic){: new_window} | Plug-in name: VPN <br> [Visualizar docs](/docs/cli/plugins/vpn/index.html) |
{: caption="Tabela 5. Plug-ins" caption-side="top"}

## ![](./images/Integrated_Dev_Tools.svg) Ferramentas de desenvolvimento integradas
{: #ide notoc}

Faça download e instale os plug-ins para integrar seus serviços do {{site.data.keyword.Bluemix_notm}} favoritos.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* | *API Connect* | *Eclipse Tools for Bluemix* |
|-------------|----------|----------|----------|----------|----------|
| [Plug-in do Eclipse Egit ![Ícone de link externo](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window}  <br> [Plug-in do Eclipse do RTC ![Ícone de link externo](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Plug-in do Eclipse do Liberty ![Ícone de link externo](../icons/launch-glyph.svg)](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Plug-in do Eclipse ![Ícone de link externo](../icons/launch-glyph.svg)](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer
Eclipse Plug-in](../services/rules/index.html#rulov002) | [Kit de ferramentas do desenvolvedor ![Ícone de link externo](../icons/launch-glyph.svg)](https://nextstage.torolab.ibm.com/apimanagement/getting-started/ ){: new_window} | [Plug-in do Eclipse do Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html) |
{: caption="Tabela 6. Plug-ins" caption-side="top"}
