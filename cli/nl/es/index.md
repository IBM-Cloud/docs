{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Herramientas de CLI y de desarrollo
{: #cli}

*Última actualización: 19 de enero de 2016*

Con {{site.data.keyword.Bluemix_short}}, tiene acceso a potentes herramientas como, por ejemplo, una interfaz de línea de mandatos unificada y plug-ins de CLI. Cada una de estas descargas de CLI están disponibles para dar soporte a su experiencia de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## ![Interfaces de línea de mandatos](./images/CLI.png) Interfaces de línea de mandatos
{: #downloads}

Descargue e instale las interfaz de línea de mandatos que dan soporte a su experiencia de
{{site.data.keyword.Bluemix_notm}}. La interfaz de línea de mandatos cf de Cloud Foundry es un requisito previo para las demás herramientas de CLI de {{site.data.keyword.Bluemix_notm}}.


| *Cloud Foundry: cf* |	*{{site.data.keyword.Bluemix_notm}}: bx* | 
|---------------------|---------------|
| [Descargue CLI](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [Ver docs](./reference/cfcommands/index.html) | [Descargue CLI](http://clis.{DomainName}/){: new_window} <br> [Ver docs](./reference/bluemix_cli/index.html)| 

| *{{site.data.keyword.Bluemix_notm}} Live Sync:
bl* |
|---------------|---------------|
| [Instalador Mac](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.pkg){: new_window} <br> [Instalador Windows](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.exe){: new_window} <br> [Ver docs](./reference/bl/index.html) |


## ![Plugins de interfaces de línea de mandatos](./images/CLI_Plugin.png) Plugins de interfaces de línea de mandatos

Amplíe fácilmente su interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}} con más mandatos. Para acceder a los plugins de interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}}, consulte el [Repositorio de plugins de CLI {{site.data.keyword.Bluemix_notm}}](http://plugins.{DomainName}/){: new_window}.

1. Para instalar plugins CLI cf desde el registro de {{site.data.keyword.Bluemix_notm}}, establezca el punto final del registro de plug-ins:
```
cf add-plugin-repo bluemix-cf http://plugins.ng.bluemix.net
```
2. Ejecute el mandato siguiente para instalar un plugin:
```
cf install-plugin plugin_name -r bluemix-cf
```

| *Active Deploy* | *Consola de administración* | *Modalidad de desarrollo* | 
|-----------------|-----------------|-----------------|
| Nombre del plugin: active-deploy <br>  [Ver docs](../services/ActiveDeploy/index.html#cli) |  Nombre del plugin: bluemix-admin <br> [Ver docs](../cli/plugins/bluemix_admin/index.html) | Nombre del plugin: development-name <br> [Ver docs](./plugins/dev_mode/index.html) | 

### Amplíe su interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}}: bx
1. Para instalar los plugins de CLI de {{site.data.keyword.Bluemix_notm}} desde el registro de {{site.data.keyword.Bluemix_notm}}, establezca el punto final de registro del plug-in:
```
bluemix plugin repo-add bluemix-bx http://plugins.ng.bluemix.net
```
2. Ejecute el mandato siguiente para instalar un plugin:
```
bluemix plugin install plugin_name -r bluemix-bx
```

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *{{site.data.keyword.autoscaling}} CLI* | *VPN* |
|-----|----|----|
| Nombre del plugin: ibm-containers <br> [Ver docs](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | Nombre del plugin: escalado automático <br> [Ver docs](./plugins/auto-scaling/index.html) |Nombre del plugin: VPN <br> [Ver docs](./plugins/vpn/index.html) |

## ![Herramientas para el desarrollo integrado](./images/Integrated_Dev_Tools.png) Herramientas para el desarrollo integrado


Descargue e instale plugins para integrar sus servicios favoritos de {{site.data.keyword.Bluemix_notm}}.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Plugin de Egit Eclipse](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [Plugin de RTC Eclipse](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Plugin de Liberty Eclipse](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Plugin de Eclipse](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Plugin de Rules Designer
Eclipse](../services/rules/index.html#rulov002) |
