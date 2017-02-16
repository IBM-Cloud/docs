---



copyright:

  years: 2015，2017

lastupdated: "2017-01-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI- und Dev-Tools
{: #cli}

Mit {{site.data.keyword.Bluemix_short}} haben Sie Zugriff auf leistungsfähige Tools wie zum Beispiel eine einheitliche Befehlszeilenschnittstelle und CLI-Plug-ins. Alle diese CLI-Downloads werden zur Unterstützung Ihrer Arbeit mit {{site.data.keyword.Bluemix_notm}} zur Verfügung gestellt.
{:shortdesc}

## ![](./images/CLI.svg) Befehlszeilenschnittstellen
{: #downloads}

Sie können Befehlszeilenschnittstellen herunterladen und installieren, die Sie beim Arbeiten mit {{site.data.keyword.Bluemix_notm}} unterstützen.

Das Cloud Foundry-Befehlszeilentool 'cf' ist eine Voraussetzung für alle anderen CLI-Tools von {{site.data.keyword.Bluemix_notm}}. Das {{site.data.keyword.Bluemix_notm}}-Befehlszeilentool stellt neben Cloud Foundry-Anwendungen umfassende Erfahrung zur Verwaltung Ihrer {{site.data.keyword.Bluemix_notm}}-Umgebung bereit.

Beide CLI-Tools verwenden standardmäßig den Port 443. Wenn sich ein HTTP-Proxy zwischen den CLI-Tools und der {{site.data.keyword.Bluemix_notm}}-Umgebung befindet, müssen Sie die Umgebungsvariable `http-proxy` mit der tatsächlichen URL und dem Port (falls vorhanden) des HTTP-Proxys konfigurieren. Details hierzu finden Sie unter [Using the CLI with an HTTP Proxy Server ![Symbol für externen Link](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window}.


| *{{site.data.keyword.Bluemix_notm}}: bx* | *Cloud Foundry: cf* |
|---------------------|---------------|
| [CLI herunterladen](http://clis.ng.bluemix.net/) <br> [Dokumentation anzeigen](/docs/cli/reference/bluemix_cli/index.html)|  [CLI herunterladen ![Symbol für externen Link](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [Dokumentation anzeigen](/docs/cli/reference/cfcommands/index.html) |
{: caption="Table 1. CLI download" caption-side="top"}


## ![](./images/CLI_Plugin.svg) Befehlszeilenschnittstelle-Plug-ins

Sie können die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle ohne großen Aufwand durch zusätzliche Befehle erweitern. Zugriff auf die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstellen-Plug-ins erhalten Sie über das [Plug-in-Repository für die Bluemix CLI ![Symbol für externen Link](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/).

### Erweitern Sie die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle: bx
{: cli_bluemix_ext}

* Zum Installieren von {{site.data.keyword.Bluemix_notm}}-CLI-Plug-ins über die {{site.data.keyword.Bluemix_notm}}-Registry müssen Sie den Plug-in-Registry-Endpunkt festlegen:

```
bluemix plugin repo-add bluemix-bx https://plugins.ng.bluemix.net
```
{: codeblock}

* Anschließend führen Sie den folgenden Befehl aus, um ein Plug-in zu installieren:

```
bluemix plugin install plugin_name -r bluemix-bx
```
{: codeblock}


| *{{site.data.keyword.activedeployshort}}-CLI* | *{{site.data.keyword.autoscaling}} CLI* | *IBM Containers*  |
|-----|-----|-----|
| Plug-in-Name: active-deploy <br> [Dokumentation anzeigen](/docs/services/ActiveDeploy/cli.html#cli) | Plug-in-Name: auto-scaling <br> [Dokumentation anzeigen](/docs/cli/plugins/auto-scaling/index.html) |  Plug-in-Name: IBM-Containers  <br> [Dokumentation anzeigen](/docs/cli/plugins/containers/index.html) |
{: caption="Table 2. Plug-ins" caption-side="top"}

|  *Privates Netzpeering* | *VPN*  |
|-----|-----|
| Plug-in-Name: private-network-peering  <br> [Dokumentation anzeigen](/docs/cli/plugins/pnp/index.html) |Plug-in-Name: VPN  <br> [Dokumentation anzeigen](/docs/cli/plugins/bx_vpn/index.html) |
{: caption="Table 3. Plug-ins" caption-side="top"}


### Erweitern Sie die Cloud Foundry-Befehlszeilenschnittstelle: cf
{: cli_cf_ext}

* Zum Installieren von CLI-Plug-ins über die {{site.data.keyword.Bluemix_notm}}-Registry müssen Sie den Plug-in-Registry-Endpunkt festlegen:

```
cf add-plugin-repo bluemix-cf https://plugins.ng.bluemix.net
```
{: codeblock}

* Anschließend führen Sie den folgenden Befehl aus, um ein Plug-in zu installieren:

```
cf install-plugin plugin_name -r bluemix-cf
```
{: codeblock}


| *Active Deploy* | *Admin Console* |
|-----------------|-----------------|
| Plug-in-Name: active-deploy <br>  [Dokumentation anzeigen](/docs/services/ActiveDeploy/cli.html#cli) |  Plug-in-Name: bluemix-admin <br> [Dokumentation anzeigen](/docs/cli/plugins/bluemix_admin/index.html) |
{: caption="Table 4. Plug-ins" caption-side="top"}


| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| Plug-in-Name: ibm-containers <br> [Dokumentation anzeigen](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | Plug-in-Name: VPN <br> [Dokumentation anzeigen](/docs/cli/plugins/vpn/index.html) |
{: caption="Table 5. Plug-ins" caption-side="top"}


## ![](./images/Integrated_Dev_Tools.svg) Integrierte Entwicklungstools

Sie können Plug-ins herunterladen und installieren, um Ihre bevorzugten {{site.data.keyword.Bluemix_notm}}-Services zu integrieren.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* | *Eclipse Tools for Bluemix* |
|-------------|----------|----------|----------|----------|
| [Eclipse-Plug-in EGit ![Symbol für externen Link](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [Eclipse-Plug-in RTC ![Symbol für externen Link](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Eclipse-Plug-in Liberty ![Symbol für externen Link](../icons/launch-glyph.svg)](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse-Plug-in ![Symbol für externen Link](../icons/launch-glyph.svg)](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Eclipse-Plug-in Rule Designer ![Symbol für externen Link](../icons/launch-glyph.svg)](/docs/services/rules/index.html#rulov002) | [Eclipse-Plug-in für Bluemix ![Symbol für externen Link](../icons/launch-glyph.svg)](https://console.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){: new_window} |
{: caption="Table 6. Plug-ins" caption-side="top"}
