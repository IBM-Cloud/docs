---



copyright:

  years: 2015, 2017

lastupdated: "2017-05-15"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Descargas
{: #cli}

Con {{site.data.keyword.Bluemix_short}}, tiene acceso a potentes herramientas como, por ejemplo, una interfaz de línea de mandatos unificada y plug-ins de CLI. Cada una de estas descargas de CLI están disponibles para dar soporte a su experiencia de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## ![](./images/CLI.svg) Interfaz de línea de mandatos
{: #downloads notoc}

Descargue e instale la herramienta de línea de mandatos para dar soporte a su experiencia en {{site.data.keyword.Bluemix_notm}}.

La interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}} proporciona una forma de gestionar su entorno de {{site.data.keyword.Bluemix_notm}} a través de la misma. También incluye en su instalación una interfaz de línea de mandatos de Cloud Foundry, cf, para gestionar los servicios y las aplicaciones de Cloud Foundry. 

De forma predeterminada, ambas herramientas de CLI utilizan el puerto 443. Si tiene el proxy HTTP entre las herramientas de interfaz de línea de mandatos (CLI) y el entorno de {{site.data.keyword.Bluemix_notm}}, debe configurar la variable de entorno `HTTP_PROXY` con el puerto y el URL de proxy HTTP real en el caso de que exista. Consulte [Utilización de la CLI cf con un servidor proxy HTTP ![icono de enlace externo](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window} para obtener más detalles.

[Descargar la interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}} ![Icono de enlace externo](../icons/launch-glyph.svg)](http://clis.ng.bluemix.net/){: new_window} <br> 
[Ver docs](/docs/cli/reference/bluemix_cli/index.html)

## ![](./images/CLI_Plugin.svg) Plugins de la interfaz de línea de mandatos
{: #cliplugins notoc}

Amplíe fácilmente su interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}} con más mandatos. Para acceder
a los plugins de la interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}}, consulte el
[Repositorio de plugin de la CLI ![icono de enlace externo](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window}.

### Amplíe su interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}}: bx
{: #cli_bluemix_ext notoc}


Después de instalar la herramienta de interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}}, el repositorio de plugins de interfaz de línea de mandatos de [ ![Icono de enlace externo](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window} se configura de forma previa y predeterminada con un alias de repositorio `Bluemix`. Puede instalar los plugins disponibles de forma directa.

```
bluemix plugin install plugin_name -r Bluemix
```

| *{{site.data.keyword.autoscaling}} CLI* |  *Servicio de contenedor de IBM Bluemix*  |
|-----|-----|-----|
| Nombre del plugin: escalado automático <br> [Ver docs](/docs/cli/plugins/auto-scaling/index.html) |  Nombre del plugin: container-service  <br> [Ver docs](/docs/containers/cs_cli_devtools.html) |
{: caption="Tabla 2. Plugins" caption-side="top"}

|  *Igualdad de red privada* | *VPN*  |
|-----|-----|
| Nombre del plugin: private-network-peering  <br> [Ver docs](/docs/cli/plugins/pnp/index.html) | Nombre del plugin: VPN  <br> [Ver docs](/docs/cli/plugins/bx_vpn/index.html) |
{: caption="Tabla 3. Plugins" caption-side="top"}

También puede añadir plugins desde otros repositorios que satisfagan la arquitectura de interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}}.
1. Si desea instalar plugins de interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}} desde otro repositorio, establezca el punto final de registro del plugin:
```
bluemix plugin repo-add bluemix-other-repo [url_repo]
```
donde `url_repo` es el url https del repositorio de plugins.

2. Ejecute el mandato siguiente para instalar un plugin:
```
bluemix plugin install plugin_name -r bluemix-other-repo
```


### Interfaz de línea de mandatos extendida de Cloud Foundry: bx cf
{: #cli_cf_ext notoc}

Después de instalar la herramienta de línea de mandatos de {{site.data.keyword.Bluemix_notm}}, también se instala una interfaz de línea de mandatos de Cloud Foundry dentro del directorio de la interfaz de línea de mandatos de Bluemix. Ejecute los mandatos de la interfaz de línea de mandatos de Cloud Foundry mediante `bluemix cf`.

* Para instalar plugins CLI cf desde el registro de {{site.data.keyword.Bluemix_notm}}, establezca el punto final del registro de plug-ins:

```
bluemix cf add-plugin-repo bluemix-cf-repo https://plugins.ng.bluemix.net
```
{: codeblock}

* A continuación, ejecute el mandato siguiente para instalar un plugin:

```
bluemix cf install-plugin plugin_name -r bluemix-cf-repo
```
{: codeblock}

| *Consola de administración* |
-----------------|
|  Nombre del plugin: bluemix-admin <br> [Ver docs](/docs/cli/plugins/bluemix_admin/index.html) |
{: caption="Tabla 4. Plugins" caption-side="top"}

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| Nombre del plugin: ibm-containers <br> [Ver docs ![Icono de enlace externo](../icons/launch-glyph.svg)](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic){: new_window} | Nombre del plugin: VPN <br> [Ver docs](/docs/cli/plugins/vpn/index.html) |
{: caption="Tabla 5. Plugins" caption-side="top"}

## ![](./images/Integrated_Dev_Tools.svg) Herramientas para el desarrollo integrado
{: #ide notoc}

Descargue e instale plugins para integrar sus servicios favoritos de {{site.data.keyword.Bluemix_notm}}.

| *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* | *Conexión de API* | *Eclipse Tools for Bluemix* |
|----------|----------|----------|----------|----------|
| [Plugin Liberty Eclipse ![icono de enlace externo](../icons/launch-glyph.svg)](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Plugin Eclipse ![icono de enlace externo](../icons/launch-glyph.svg)](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Plugin de Rules Designer Eclipse](../services/rules/index.html#rulov002) | [Kit de utilidades del desarrollador](/docs/services/apiconnect/apic_003.html#apic_001 ) | [Plugin Bluemix Eclipse](/docs/manageapps/eclipsetools/eclipsetools.html) |
{: caption="Tabla 6. Plugins" caption-side="top"}
