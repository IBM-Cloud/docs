{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI- und Entwicklungstools
{: #cli}

*Letzte Aktualisierung: 10. November 2015*

Leistungsfähige Tools für {{site.data.keyword.Bluemix_short}}.{:shortdesc}

## ![Befehlszeilenschnittstellen](./images/CLI.png) Befehlszeilenschnittstellen
{: #downloads}

Sie können Befehlszeilenschnittstellen herunterladen und installieren, die Sie beim Arbeiten
mit {{site.data.keyword.Bluemix_notm}} unterstützen.
Die Befehlszeilenschnittstelle 'cf' von Cloud Foundry ist die Voraussetzung für
alle anderen Befehlszeilenschnittstellentools von {{site.data.keyword.Bluemix_notm}}. 


| *Cloud Foundry: cf* |	*{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}: ice* | *{{site.data.keyword.Bluemix_notm}} Live Sync: bl* |
|---------------------|---------------|---------------|
| [CLI herunterladen](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [Dokumentation anzeigen](./reference/cfcommands/index.html) |[Docker herunterladen](https://docs.docker.com/installation/){: new_window} <br> [ice: Mac Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.pkg){: new_window} <br> [ice: Windows Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.exe){: new_window} <br> [ice: Linux Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.tar.gz){: new_window} <br> [Dokumentation anzeigen](../containers/container_cli_ice_ov.html) | [Mac Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.pkg){: new_window} <br> [Windows Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.exe){: new_window} <br> [Dokumentation anzeigen](./reference/bl/index.html) |


## ![Befehlszeilenschnittstellen-Plug-ins](./images/CLI_Plugin.png) Befehlszeilenschnittstelle-Plug-ins

Sie können die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle ohne großen Aufwand durch zusätzliche Befehle erweitern.
Zugriff auf die {{site.data.keyword.Bluemix_notm}} -Befehlszeilenschnittstellen-Plug-ins erhalten Sie über das [{{site.data.keyword.Bluemix_notm}}-CLI-Plug-in-Repository](http://plugins.{DomainName}/){: new_window}.


1. Zum Installieren von CLI-Plug-ins über die {{site.data.keyword.Bluemix_notm}}-Registry müssen Sie den Plug-in-Registry-Endpunkt festlegen:
```
cf add-plugin-repo bluemix-cf-staging http://plugins.ng.bluemix.net
```
2. Führen Sie den folgenden Befehl aus, um ein Plug-in zu installieren:
```
cf install-plugin plugin_name -r bluemix-cf-staging
```

| *Active Deploy* |  *Development Mode* | 
|-----------------|-----------------|
| Plug-in-Name: active-deploy<br>  [Dokumentation anzeigen](../services/ActiveDeploy/index.html#cli) |  Plug-in-Name: development-name<br> [Dokumentation anzeigen](./plugins/dev_mode/index.html) | 

### Erweitern Sie die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle (bx).

1. Zum Installieren von {{site.data.keyword.Bluemix_notm}}-CLI-Plug-ins über die {{site.data.keyword.Bluemix_notm}}-Registry müssen Sie den Plug-in-Registry-Endpunkt festlegen:
```
bluemix plugin repo-add bluemix-bx-staging http://plugins.ng.bluemix.net
```
2. Führen Sie den folgenden Befehl aus, um ein Plug-in zu installieren:
```
bluemix plugin install plugin_name -r bluemix-bx-staging
```

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* |
|-----|
| Plug-in-Name: ibm-containers<br> [Dokumentation anzeigen](https://www.{{DomainName}}/docs/containers/container_cli_cfic.html#container_cli_cfic) |

## ![Integrierte Entwicklungstools](./images/Integrated_Dev_Tools.png) Integrierte Entwicklungstools


Sie können Plug-ins herunterladen und installieren, um Ihre bevorzugten
{{site.data.keyword.Bluemix_notm}}-Services zu integrieren.


| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Egit Eclipse-Plug-in](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window}<br> [RTC Eclipse-Plug-in](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse-Plug-in](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse-Plug-in](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse-Plug-in](../services/rules/index.html#rulov002) |
