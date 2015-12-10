{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI e strumenti di sviluppo
{: #cli}

*Ultimo aggiornamento: 10 novembre 2015*

Potenti strumenti per {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

## ![Interfacce riga di comando](./images/CLI.png) Interfacce riga di comando
{: #downloads}

Scarica e installa le interfacce riga di comando a supporto della tua esperienza {{site.data.keyword.Bluemix_notm}}. L'interfaccia riga di comando cf Cloud Foundry
è un prerequisito per tutti gli altri strumenti CLI {{site.data.keyword.Bluemix_notm}}.


| *Cloud Foundry: cf* |	*{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}: ice* | *{{site.data.keyword.Bluemix_notm}} Live Sync:
bl* |
|---------------------|---------------|---------------|
| [Scarica CLI](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [Visualizza documenti](./reference/cfcommands/index.html) |[Scarica Docker](https://docs.docker.com/installation/){: new_window} <br> [Programma di installazione ice Mac](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.pkg){: new_window} <br> [Programma di installazione ice Windows](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.exe){: new_window} <br> [Programma di installazione ice Linux](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.tar.gz){: new_window} <br> [Visualizza documenti](../containers/container_cli_ice_ov.html) | [Programma di installazione Mac](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.pkg){: new_window} <br> [Programma di installazione Windows](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.exe){: new_window} <br> [Visualizza documenti](./reference/bl/index.html) |


## ![Plug-in di interfaccia riga di comando](./images/CLI_Plugin.png) Plug-in di interfaccia di riga di comando

Estendi facilmente la tua interfaccia riga di comando {{site.data.keyword.Bluemix_notm}} con più comandi. Per accedere ai plug-in di interfaccia
riga di comando {{site.data.keyword.Bluemix_notm}}, vedi [{{site.data.keyword.Bluemix_notm}} CLI Plug-in Repository](http://plugins.{DomainName}/){: new_window}.

1. Per installare i plug-in CLI dal registro {{site.data.keyword.Bluemix_notm}}, imposta l'endpoint di registro di plug-in:```
cf add-plugin-repo bluemix-cf-staging http://plugins.ng.bluemix.net
```
2. Esegui il seguente comando per installare un plug-in:
```
cf install-plugin nome_plugin -r bluemix-cf-staging
```

| *Active Deploy* |  *Modalità di sviluppo* | 
|-----------------|-----------------|
| Nome del plug-in: active-deploy <br>  [Visualizza documenti](../services/ActiveDeploy/index.html#cli) |  Nome del plug-in: development-name<br> [Visualizza documenti](./plugins/dev_mode/index.html) | 

### Estendi la tua interfaccia riga di comando {{site.data.keyword.Bluemix_notm}}: bx
1. Per installare i plug-in CLI {{site.data.keyword.Bluemix_notm}} dal registro {{site.data.keyword.Bluemix_notm}}, imposta l'endpoint di registro di plug-in:```
bluemix plugin repo-add bluemix-bx-staging http://plugins.ng.bluemix.net
```
2. Esegui il seguente comando per installare un plug-in:
```
bluemix plugin install nome_plugin -r bluemix-bx-staging
```

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* |
|-----|
| Nome del plug-in: ibm-containers <br> [Visualizza documenti](https://www.{{DomainName}}/docs/containers/container_cli_cfic.html#container_cli_cfic) |

## ![Strumenti di sviluppo integrati](./images/Integrated_Dev_Tools.png) Strumenti di sviluppo integrati


Scarica e installa i plug-in per integrare i tuoi servizi {{site.data.keyword.Bluemix_notm}} preferiti.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Plug-in Eclipse Egit](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [Plug-in Eclipse RTC](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Plug-in Eclipse Liberty](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Plug-in Eclipse](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Plug-in Eclipse Rules Designer](../services/rules/index.html#rulov002) |
