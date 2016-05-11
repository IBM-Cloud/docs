---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Herramientas de CLI y de desarrollo
{: #cli}

*Última actualización: 30 de marzo de 2016*

Con {{site.data.keyword.Bluemix_short}}, tiene acceso a potentes herramientas como, por ejemplo, una interfaz de línea de mandatos unificada y plug-ins de CLI. Cada una de estas descargas de CLI están disponibles para dar soporte a su experiencia de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## ![Interfaces de línea de mandatos](./images/CLI.svg) Interfaces de línea de mandatos
{: #downloads}

Descargue e instale las interfaz de línea de mandatos que dan soporte a su experiencia de
{{site.data.keyword.Bluemix_notm}}. La herramienta de línea de mandatos cf de Cloud Foundry es un requisito previo para las demás herramientas de CLI de {{site.data.keyword.Bluemix_notm}}. La herramienta de línea de mandatos de {{site.data.keyword.Bluemix_notm}} proporciona
una experiencia ampliada para gestionar su entorno de {{site.data.keyword.Bluemix_notm}} aparte de las aplicaciones de Cloud Foundry.

Las dos herramientas de interfaz de línea de mandatos utiliza ¡n el puerto 433 de forma predeterminada. Si tiene el proxy HTTP entre las herramientas de interfaz de línea de mandatos (CLI) y el entorno de {{site.data.keyword.Bluemix_notm}}, debe configurar la variable de entorno `http-proxy` con el puerto y el URL de proxy HTTP real en el caso de que exista. Consulte [Utilización de la CLI cf con un servidor proxy HTTP](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window} para obtener más detalles.


| *{{site.data.keyword.Bluemix_notm}}: bx* | *Cloud Foundry: cf* |
|---------------------|---------------|
| [Descargue CLI](http://clis.ng.bluemix.net/) <br> [Ver docs](./reference/bluemix_cli/index.html)|  [Descargue CLI](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [Ver docs](./reference/cfcommands/index.html) |


## ![Plugins de interfaces de línea de mandatos](./images/CLI_Plugin.svg) Plugins de interfaces de línea de mandatos

Amplíe fácilmente su interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}} con más mandatos. Para acceder
a los plugin de la interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}}, consulte el
[Repositorio de plugin de la CLI](http://plugins.ng.bluemix.net/).

### Amplíe su interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}}: bx

1. Para instalar los plugins de CLI de {{site.data.keyword.Bluemix_notm}} desde el registro de {{site.data.keyword.Bluemix_notm}}, establezca el punto final de registro del plug-in:
```
bluemix plugin repo-add bluemix-bx-staging http://plugins.ng.bluemix.net
```
2. Ejecute el mandato siguiente para instalar un plugin:
```
bluemix plugin install plugin_name -r bluemix-bx-staging
```

| *{{site.data.keyword.activedeployshort}} CLI* | *{{site.data.keyword.autoscaling}} CLI* | *Grupos de seguridad de red* |
|-----|-----|-----|
| Nombre del plugin: active-deploy <br> [Ver docs](../services/ActiveDeploy/cli.html#cli) | Nombre del plugin: escalado automático <br> [Ver docs](./plugins/auto-scaling/index.html) |  Nombre de plugin: nsg <br> [Ver docs](./plugins/networksecuritygroups/index.html)  |


### Ampliar la interfaz de línea de mandatos de Cloud Foundry : cf

1. Para instalar plugins CLI cf desde el registro de {{site.data.keyword.Bluemix_notm}}, establezca el punto final del registro de plug-ins:
```
cf add-plugin-repo bluemix-cf-staging http://plugins.ng.bluemix.net
```
2. Ejecute el mandato siguiente para instalar un plugin:
```
cf install-plugin plugin_name -r bluemix-cf-staging
```

| *Active Deploy* | *Consola de administración* | *Modalidad de desarrollo* |
|-----------------|-----------------|-----------------|
| Nombre del plugin: active-deploy <br>  [Ver docs](../services/ActiveDeploy/cli.html#cli) |  Nombre del plugin: bluemix-admin <br> [Ver docs](../cli/plugins/bluemix_admin/index.html) | Nombre del plugin: dev_mode <br> [Ver docs](./plugins/dev_mode/index.html) |

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| Nombre del plugin: ibm-containers <br> [Ver docs](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | Nombre del plugin: VPN <br> [Ver docs](./plugins/vpn/index.html) |

<!-- View docs link for bluemix-admin plug-in cannot go live until December time frame. Check in with Michelle -->


## ![Herramientas para el desarrollo integrado](./images/Integrated_Dev_Tools.svg) Herramientas para el desarrollo integrado

Descargue e instale plugins para integrar sus servicios favoritos de {{site.data.keyword.Bluemix_notm}}.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Plugin de Egit Eclipse](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [Plugin de RTC Eclipse](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Plugin de Liberty Eclipse](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Plugin de Eclipse](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Plugin de Rules Designer
Eclipse](../services/rules/index.html#rulov002) |
