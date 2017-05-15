---



copyright:

  years: 2015, 2017

lastupdated: "2017-02-14"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Download
{: #cli}

Con {{site.data.keyword.Bluemix_short}}, hai accesso a potenti strumenti, quali un'interfaccia riga di comando unificata e i plug-in delle CLI. Ciascuno di questi download di CLI è disponibile a supporto della tua esperienza {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Interfaccia riga di comando ![](./images/CLI.svg) 
{: #downloads notoc}

Scarica e installa lo strumento di riga di comando per supportare la tua esperienza {{site.data.keyword.Bluemix_notm}}.

La CLI {{site.data.keyword.Bluemix_notm}} offre un'esperienza della riga di comando per gestire il tuo ambiente {{site.data.keyword.Bluemix_notm}}. Con la sua installazione è inclusa inoltre un'interfaccia riga di comando Cloud Foundry, denominata cf, per la gestione delle applicazioni e dei servizi Cloud Foundry. 

Questi strumenti CLI utilizzano entrambi la porta 443 per impostazione predefinita. Se è presente un proxy HTTP tra gli strumenti CLI e l'ambiente {{site.data.keyword.Bluemix_notm}}, devi configurare la variabile di ambiente `HTTP_PROXY` con la porta e l'url del proxy HTTP effettivi laddove disponibili. Per ulteriori dettagli, consulta [Utilizzo della CLI con un server proxy HTTP ![icona link esterno](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window}s.

[Scarica la CLI {{site.data.keyword.Bluemix_notm}} ![icona link esterno](../icons/launch-glyph.svg)](http://clis.ng.bluemix.net/){: new_window} <br> 
[Visualizza documenti](/docs/cli/reference/bluemix_cli/index.html)

## ![](./images/CLI_Plugin.svg) Plug-in di interfaccia riga di comando
{: #cliplugins notoc}

Estendi facilmente la tua interfaccia riga di comando {{site.data.keyword.Bluemix_notm}} con più comandi. Per accedere ai plug-in di interfaccia riga di comando
{{site.data.keyword.Bluemix_notm}}, consulta il [Repository di plug-in CLI![icona link esterno](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window}.

### Estendi la tua interfaccia riga di comando {{site.data.keyword.Bluemix_notm}}: bx
{: #cli_bluemix_ext notoc}


Dopo aver installato lo strumento CLI {{site.data.keyword.Bluemix_notm}}, il [Repository di plug-in CLI![icona link esterno](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window} viene preconfigurato con un repository alias `Bluemix` per impostazione predefinita. Puoi installare direttamente i plug-in disponibili.

```
bluemix plugin install plugin_name -r Bluemix
```

| *{{site.data.keyword.activedeployshort}} CLI* | *{{site.data.keyword.autoscaling}} CLI* | *Servizio IBM Bluemix Container*  |
|-----|-----|-----|
| Nome del plug-in: active-deploy <br> [Visualizza documenti](/docs/services/ActiveDeploy/cli.html#cli) | Nome del plug-in: auto-scaling <br> [Visualizza documenti](/docs/cli/plugins/auto-scaling/index.html) | Nome del plug-in: container-service  <br> [Visualizza documenti](/docs/containers/cs_cli_devtools.html) |
{: caption="Tabella 2. Plug-in" caption-side="top"}

|  *Peering della rete privata* | *VPN*  |
|-----|-----|
| Nome del plug-in: private-network-peering  <br> [Visualizza documenti](/docs/cli/plugins/pnp/index.html) | Nome del plug-in: VPN  <br> [Visualizza documenti](/docs/cli/plugins/bx_vpn/index.html) |
{: caption="Tabella 3. Plug-in" caption-side="top"}

Puoi anche aggiungere i plug-in da altri repository conformi all'architettura della CLI {{site.data.keyword.Bluemix_notm}}.
1. Per installare i plug-in CLI {{site.data.keyword.Bluemix_notm}} da un altro repository, imposta l'endpoint del registro di plug-in:
```
bluemix plugin repo-add bluemix-other-repo [repo_url]
```
dove `repo_url` è l'URL HTTPS del repository di plug-in.

2. Esegui il seguente comando per installare un plug-in:
```
bluemix plugin install plugin_name -r bluemix-other-repo
```


### Estendi l'interfaccia riga di comando Cloud Foundry: bx cf
{: #cli_cf_ext notoc}

Dopo aver installato lo strumento riga di comando {{site.data.keyword.Bluemix_notm}}, viene installata anche un'interfaccia riga di comando Cloud Foundry all'interno della directory della CLI Bluemix. Esegui i comandi della CLI Cloud Foundry utilizzando `bluemix cf`.

* Per installare i plug-in CLI dal registro {{site.data.keyword.Bluemix_notm}}, imposta l'endpoint di registro di plug-in:

```
bluemix cf add-plugin-repo bluemix-cf-repo https://plugins.ng.bluemix.net
```
{: codeblock}

* Immetti quindi il seguente comando per installare un plug-in:

```
bluemix cf install-plugin plugin_name -r bluemix-cf-repo
```
{: codeblock}

| *Active Deploy* | *Console di gestione* |
|-----------------|-----------------|
| Nome del plug-in: active-deploy <br>  [Visualizza documenti](/docs/services/ActiveDeploy/cli.html#cli) |  Nome del plug-in: bluemix-admin <br> [Visualizza documenti](/docs/cli/plugins/bluemix_admin/index.html) |
{: caption="Tabella 4. Plug-in" caption-side="top"}

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| Nome del plug-in: ibm-containers <br> [Visualizza documenti ![icona link esterno](../icons/launch-glyph.svg)](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic){: new_window} | Nome del plug-in: VPN <br> [Visualizza documenti](/docs/cli/plugins/vpn/index.html) |
{: caption="Tabella 5. Plug-in" caption-side="top"}

## ![](./images/Integrated_Dev_Tools.svg) Strumenti di sviluppo integrati
{: #ide notoc}

Scarica e installa i plug-in per integrare i tuoi servizi {{site.data.keyword.Bluemix_notm}} preferiti.

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* | *API Connect* | *Eclipse Tools for Bluemix* |
|-------------|----------|----------|----------|----------|----------|
| [Plug-in Eclipse Egit![icona link esterno](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window}  <br> [Plugin RTC Eclipse ![icona link esterno](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Plugin Liberty Eclipse ![icona link esterno](../icons/launch-glyph.svg)](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Plugin Eclipse ![icona link esterno](../icons/launch-glyph.svg)](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Plug-in Eclipse Rules Designer](../services/rules/index.html#rulov002) | [Toolkit sviluppatori ![icona link esterno](../icons/launch-glyph.svg)](https://nextstage.torolab.ibm.com/apimanagement/getting-started/ ){: new_window} | [Plug-in Bluemix Eclipse](/docs/manageapps/eclipsetools/eclipsetools.html) |
{: caption="Tabella 6. Plug-in" caption-side="top"}
