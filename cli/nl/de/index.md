---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI- und Dev-Tools
{: #cli}

*Letzte Aktualisierung: 30. March 2016*

Mit {{site.data.keyword.Bluemix_short}} haben Sie Zugriff auf leistungsfähige Tools wie zum Beispiel eine einheitliche Befehlszeilenschnittstelle und CLI-Plug-ins. Alle diese CLI-Downloads werden zur Unterstützung Ihrer Arbeit mit {{site.data.keyword.Bluemix_notm}} zur Verfügung gestellt.
{:shortdesc}

## ![Befehlszeilenschnittstellen](./images/CLI.svg) Befehlszeilenschnittstellen
{: #downloads}

Sie können Befehlszeilenschnittstellen herunterladen und installieren, die Sie beim Arbeiten mit {{site.data.keyword.Bluemix_notm}} unterstützen. Das Cloud Foundry-Befehlszeilentool 'cf' ist eine Voraussetzung für alle anderen Befehlszeilenschnittstellentools von {{site.data.keyword.Bluemix_notm}}. Das {{site.data.keyword.Bluemix_notm}}-Befehlszeilentool stellt neben Cloud Foundry-Anwendungen umfassende Erfahrung zur Verwaltung Ihrer {{site.data.keyword.Bluemix_notm}}-Umgebung bereit.

Beide CLI-Tools verwenden standardmäßig den Port 433. Wenn sich ein HTTP-Proxy zwischen den CLI-Tools und der {{site.data.keyword.Bluemix_notm}}-Umgebung befindet, müssen Sie die Umgebungsvariable `http-proxy` mit der tatsächlichen URL und dem Port (falls vorhanden) des HTTP-Proxys konfigurieren. Details hierzu finden Sie in [Using the CLI with an HTTP Proxy Server](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window}.


| *{{site.data.keyword.Bluemix_notm}}: bx* | *Cloud Foundry: cf* |
|---------------------|---------------|
| [CLI herunterladen](http://clis.ng.bluemix.net/) <br> [Dokumentation anzeigen](./reference/bluemix_cli/index.html)|  [CLI herunterladen](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [Dokumentation anzeigen](./reference/cfcommands/index.html) |


## ![Befehlszeilenschnittstellen-Plug-ins](./images/CLI_Plugin.svg) Befehlszeilenschnittstelle-Plug-ins

Sie können die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle ohne großen Aufwand durch zusätzliche Befehle erweitern. Zugriff auf die {{site.data.keyword.Bluemix_notm}} -Befehlszeilenschnittstellen-Plug-ins erhalten Sie über das [-CLI-Plug-in-Repository](http://plugins.ng.bluemix.net/).

### Erweitern Sie die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle: bx

1. Zum Installieren von {{site.data.keyword.Bluemix_notm}}-CLI-Plug-ins über die {{site.data.keyword.Bluemix_notm}}-Registry müssen Sie den Plug-in-Registry-Endpunkt festlegen:
```
bluemix plugin repo-add bluemix-bx-staging http://plugins.ng.bluemix.net
```
2. Führen Sie den folgenden Befehl aus, um ein Plug-in zu installieren:
```
bluemix plugin install plugin_name -r bluemix-bx-staging
```

| *{{site.data.keyword.activedeployshort}}-CLI* | *{{site.data.keyword.autoscaling}} CLI* | *Network Security Groups* |
|-----|-----|-----|
| Plug-in-Name: active-deploy <br> [Dokumentation anzeigen](../services/ActiveDeploy/cli.html#cli) | Plug-in-Name: auto-scaling <br> [Dokumentation anzeigen](./plugins/auto-scaling/index.html) |  Plug-in-Name: nsg <br> [Dokumentation anzeigen](./plugins/networksecuritygroups/index.html)  |


### Erweitern Sie die Cloud Foundry-Befehlszeilenschnittstelle: cf

1. Zum Installieren von CLI-Plug-ins über die {{site.data.keyword.Bluemix_notm}}-Registry müssen Sie den Plug-in-Registry-Endpunkt festlegen:
```
cf add-plugin-repo bluemix-cf-staging http://plugins.ng.bluemix.net
```
2. Führen Sie den folgenden Befehl aus, um ein Plug-in zu installieren:
```
cf install-plugin plugin_name -r bluemix-cf-staging
```

| *Active Deploy* | *Admin Console* | *Development Mode* |
|-----------------|-----------------|-----------------|
| Plug-in-Name: active-deploy <br>  [Dokumentation anzeigen](../services/ActiveDeploy/cli.html#cli) |  Plug-in-Name: bluemix-admin <br> [Dokumentation anzeigen](../cli/plugins/bluemix_admin/index.html) | Plug-in-Name: dev_mode <br> [Dokumentation anzeigen](./plugins/dev_mode/index.html) |

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| Plug-in-Name: ibm-containers <br> [Dokumentation anzeigen](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | Plug-in-Name: VPN <br> [Dokumentation anzeigen](./plugins/vpn/index.html) |

<!-- View docs link for bluemix-admin plug-in cannot go live until December time frame. Check in with Michelle -->


## ![Integrierte Entwicklungstools](./images/Integrated_Dev_Tools.svg) Integrierte Entwicklungstools

Sie können Plug-ins herunterladen und installieren, um Ihre bevorzugten {{site.data.keyword.Bluemix_notm}}-Services zu integrieren.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Egit Eclipse-Plug-in](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse-Plug-in](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse-Plug-in](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse-Plug-in](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse-Plug-in](../services/rules/index.html#rulov002) |
