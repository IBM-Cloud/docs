{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI- und Dev-Tools
{: #cli}

*Letzte Aktualisierung: 19. Januar 2016*

Mit {{site.data.keyword.Bluemix_short}} haben Sie Zugriff auf leistungsfähige Tools wie zum Beispiel eine einheitliche Befehlszeilenschnittstelle und CLI-Plug-ins. Alle diese CLI-Downloads werden zur Unterstützung Ihrer Arbeit mit {{site.data.keyword.Bluemix_notm}} zur Verfügung gestellt.
{:shortdesc}

## ![Befehlszeilenschnittstellen](./images/CLI.png) Befehlszeilenschnittstellen
{: #downloads}

Sie können Befehlszeilenschnittstellen herunterladen und installieren, die Sie beim Arbeiten mit {{site.data.keyword.Bluemix_notm}} unterstützen. Die Befehlszeilenschnittstelle 'cf' von Cloud Foundry ist die Voraussetzung für alle anderen Befehlszeilenschnittstellentools von {{site.data.keyword.Bluemix_notm}}.


| *Cloud Foundry: cf* |	*{{site.data.keyword.Bluemix_notm}}: bx* | 
|---------------------|---------------|
| [CLI herunterladen](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [Dokumentation anzeigen](./reference/cfcommands/index.html) | [CLI herunterladen](http://clis.{DomainName}/){: new_window} <br> [Dokumentation anzeigen](./reference/bluemix_cli/index.html)| 

| *{{site.data.keyword.Bluemix_notm}} Live Sync: bl* |
|---------------|---------------|
| [Mac Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.pkg){: new_window} <br> [Windows Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.exe){: new_window} <br> [Dokumentation anzeigen](./reference/bl/index.html) |


## ![Befehlszeilenschnittstellen-Plug-ins](./images/CLI_Plugin.png) Befehlszeilenschnittstelle-Plug-ins

Sie können die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle ohne großen Aufwand durch zusätzliche Befehle erweitern. Zugriff auf die {{site.data.keyword.Bluemix_notm}} -Befehlszeilenschnittstellen-Plug-ins erhalten Sie über das [{{site.data.keyword.Bluemix_notm}}-CLI-Plug-in-Repository](http://plugins.{DomainName}/){: new_window}.

1. Zum Installieren von CLI-Plug-ins über die {{site.data.keyword.Bluemix_notm}}-Registry müssen Sie den Plug-in-Registry-Endpunkt festlegen:
```
cf add-plugin-repo bluemix-cf http://plugins.ng.bluemix.net
```
2. Führen Sie den folgenden Befehl aus, um ein Plug-in zu installieren:
```
cf install-plugin plugin_name -r bluemix-cf
```

| *Active Deploy* | *Admin Console* | *Development Mode* | 
|-----------------|-----------------|-----------------|
| Plug-in-Name: active-deploy <br>  [Dokumentation anzeigen](../services/ActiveDeploy/index.html#cli) |  Plug-in-Name: bluemix-admin<br> [Dokumentation anzeigen](../cli/plugins/bluemix_admin/index.html) | Plug-in-Name: development-name <br> [Dokumentation anzeigen](./plugins/dev_mode/index.html) | 

### Erweitern Sie die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle: bx
1. Zum Installieren von {{site.data.keyword.Bluemix_notm}}-CLI-Plug-ins über die {{site.data.keyword.Bluemix_notm}}-Registry müssen Sie den Plug-in-Registry-Endpunkt festlegen:
```
bluemix plugin repo-add bluemix-bx http://plugins.ng.bluemix.net
```
2. Führen Sie den folgenden Befehl aus, um ein Plug-in zu installieren:
```
bluemix plugin install plugin_name -r bluemix-bx
```

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *{{site.data.keyword.autoscaling}} CLI* | *VPN* |
|-----|----|----|
| Plug-in-Name: ibm-containers <br> [Dokumentation anzeigen](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | Plug-in-Name: auto-scaling <br> [Dokumentation anzeigen](./plugins/auto-scaling/index.html) |Plug-in-Name: VPN <br> [Dokumentation anzeigen](./plugins/vpn/index.html) |

## ![Integrierte Entwicklungstools](./images/Integrated_Dev_Tools.png) Integrierte Entwicklungstools


Sie können Plug-ins herunterladen und installieren, um Ihre bevorzugten {{site.data.keyword.Bluemix_notm}}-Services zu integrieren.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Egit Eclipse-Plug-in](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse-Plug-in](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse-Plug-in](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse-Plug-in](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse-Plug-in](../services/rules/index.html#rulov002) |
