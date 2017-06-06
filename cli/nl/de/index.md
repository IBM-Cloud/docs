---



copyright:

  years: 2015, 2017

lastupdated: "2017-05-15"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Downloads
{: #cli}

Mit {{site.data.keyword.Bluemix_short}} haben Sie Zugriff auf leistungsfähige Tools wie zum Beispiel eine einheitliche Befehlszeilenschnittstelle und CLI-Plug-ins. Alle diese CLI-Downloads werden zur Unterstützung Ihrer Arbeit mit {{site.data.keyword.Bluemix_notm}} zur Verfügung gestellt.
{:shortdesc}

## ![](./images/CLI.svg) Befehlszeilenschnittstelle (CLI)
{: #downloads notoc}

Laden Sie das Befehlszeilentool herunter und installieren Sie es, um Ihre Arbeit in {{site.data.keyword.Bluemix_notm}} zu unterstützen.

Die {{site.data.keyword.Bluemix_notm}}-CLI stellt eine Befehlszeilenbedienung zur Verwaltung Ihrer {{site.data.keyword.Bluemix_notm}}-Umgebung bereit. Sie enthält außerdem eine Cloud Foundry-Befehlszeilenschnittstelle (cf) in ihrer Installation, die zur Verwaltung von Cloud Foundry-Anwendungen und -Services verwendet werden kann. 

Beide CLI-Tools verwenden standardmäßig den Port 443. Wenn sich ein HTTP-Proxy zwischen den CLI-Tools und der {{site.data.keyword.Bluemix_notm}}-Umgebung befindet, müssen Sie die Umgebungsvariable `HTTP_PROXY` mit der tatsächlichen URL und dem Port (falls vorhanden) des HTTP-Proxys konfigurieren. Details hierzu finden Sie in den Informationen zur [Verwendung der CLI mit einem HTTP-Proxy-Server ![Symbol für externen Link](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window}.

[{{site.data.keyword.Bluemix_notm}}-CLI herunterladen ![Symbol für externen Link](../icons/launch-glyph.svg)](http://clis.ng.bluemix.net/){: new_window} <br> 
[Dokumentation anzeigen](/docs/cli/reference/bluemix_cli/index.html)

## ![](./images/CLI_Plugin.svg) Befehlszeilenschnittstelle-Plug-ins
{: #cliplugins notoc}

Sie können die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle ohne großen Aufwand durch zusätzliche Befehle erweitern. Zugriff auf die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstellen-Plug-ins erhalten Sie über das [Plug-in-Repository für die Bluemix CLI ![Symbol für externen Link](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window}.

### Erweitern Sie die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle: bx
{: #cli_bluemix_ext notoc}


Wenn Sie das {{site.data.keyword.Bluemix_notm}}-CLI-Tool installieren, wird das [CLI-Plug-in-Repository ![Symbol für externen Link](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window} standardmäßig mit dem Repository-Aliasnamen `Bluemix` vorkonfiguriert. Sie können verfügbare Plug-ins direkt installieren.

```
bluemix plugin install Plug-in-Name -r Bluemix
```

| *{{site.data.keyword.autoscaling}}-CLI* |  *IBM Bluemix Container Service*  |
|-----|-----|-----|
| Plug-in-Name: auto-scaling <br> [Dokumentation anzeigen](/docs/cli/plugins/auto-scaling/index.html) |  Plug-in-Name: container-service  <br> [Dokumentation anzeigen](/docs/containers/cs_cli_devtools.html) |
{: caption="Tabelle 2. Plug-ins" caption-side="top"}

|  *Privates Netzpeering* | *VPN*  |
|-----|-----|
| Plug-in-Name: private-network-peering  <br> [Dokumentation anzeigen](/docs/cli/plugins/pnp/index.html) | Plug-in-Name: VPN  <br> [Dokumentation anzeigen](/docs/cli/plugins/bx_vpn/index.html) |
{: caption="Tabelle 3. Plug-ins" caption-side="top"}

Sie können außerdem Plug-ins aus anderen Repositorys hinzufügen, die mit der {{site.data.keyword.Bluemix_notm}}-CLI-Architektur konform sind.
1. Zum Installieren von {{site.data.keyword.Bluemix_notm}}-CLI-Plug-ins aus einem anderen Repository legen Sie den Plug-in-Registry-Endpunkt fest:
```
bluemix plugin repo-add bluemix-other-repo [repo_url]
```
Dabei ist `repo_url` die HTTPS-URL des Plug-in-Repositorys.

2. Führen Sie den folgenden Befehl aus, um ein Plug-in zu installieren:
```
bluemix plugin install Plug-in-Name -r bluemix-other-repo
```


### Erweitern Sie die Cloud Foundry-Befehlszeilenschnittstelle: bx cf
{: #cli_cf_ext notoc}

Nach der Installation des {{site.data.keyword.Bluemix_notm}}-Befehlszeilentools ist auch eine Cloud Foundry-Befehlszeilenschnittstelle im Bluemix-CLI-Verzeichnis installiert. Führen Sie die Cloud Foundry-CLI-Befehle mit `bluemix cf` aus.

* Zum Installieren von CLI-Plug-ins über die {{site.data.keyword.Bluemix_notm}}-Registry müssen Sie den Plug-in-Registry-Endpunkt festlegen:

```
bluemix cf add-plugin-repo bluemix-cf-repo https://plugins.ng.bluemix.net
```
{: codeblock}

* Anschließend führen Sie den folgenden Befehl aus, um ein Plug-in zu installieren:

```
bluemix cf install-plugin Plug-in-Name -r bluemix-cf-repo
```
{: codeblock}

| *Administrationskonsole* |
-----------------|
|  Plug-in-Name: bluemix-admin <br> [Dokumentation anzeigen](/docs/cli/plugins/bluemix_admin/index.html) |
{: caption="Tabelle 4. Plug-ins" caption-side="top"}

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| Plug-in-Name: ibm-containers <br> [Dokumentation anzeigen ![Symbol für externen Link](../icons/launch-glyph.svg)](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic){: new_window} | Plug-in-Name: VPN <br> [Dokumentation anzeigen](/docs/cli/plugins/vpn/index.html) |
{: caption="Tabelle 5. Plug-ins" caption-side="top"}

## ![](./images/Integrated_Dev_Tools.svg) Integrierte Entwicklungstools
{: #ide notoc}

Sie können Plug-ins herunterladen und installieren, um Ihre bevorzugten {{site.data.keyword.Bluemix_notm}}-Services zu integrieren.

| *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* | *API Connect* | *Eclipse Tools for Bluemix* |
|----------|----------|----------|----------|----------|
| [Eclipse-Plug-in Liberty ![Symbol für externen Link](../icons/launch-glyph.svg)](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse-Plug-in ![Symbol für externen Link](../icons/launch-glyph.svg)](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse Plug-in](../services/rules/index.html#rulov002) | [ Developer Toolkit ](/docs/services/apiconnect/apic_003.html#apic_001 ) | [Bluemix Eclipse Plug-in](/docs/manageapps/eclipsetools/eclipsetools.html) |
{: caption="Tabelle 6. Plug-ins" caption-side="top"}
