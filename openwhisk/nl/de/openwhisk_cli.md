---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}}-Befehlszeilenschnittstelle (CLI)

{{site.data.keyword.openwhisk_short}} bietet eine leistungsfähige Befehlszeilenschnittstelle (CLI, Command Line Interface) an, über die alle Aspekte des Systems vollständig verwaltet werden können.

## {{site.data.keyword.openwhisk_short}}-CLI einrichten 

Sie können Ihren Namensbereich und Ihren Berechtigungsschlüssel über die {{site.data.keyword.openwhisk_short}}-Befehlszeilenschnittstelle einrichten.
Navigieren Sie zu [CLI konfigurieren](https://new-console.{DomainName}/openwhisk/cli){: new_window} und gehen Sie gemäß den Anweisungen für die Installation vor.

Zwei erforderliche Eigenschaften müssen für die Verwendung der CLI konfiguriert werden:

1. **API-Host:** Name oder IP-Adresse der {{site.data.keyword.openwhisk_short}}-Bereitstellung, die verwendet werden soll.
2. **Berechtigungsschlüssel:** Benutzername und Kennwort für den Zugriff auf die {{site.data.keyword.openwhisk_short}}-API.

Führen Sie den folgenden Befehl aus, um den API-Host festzulegen:

```
wsk property set --apihost openwhisk.ng.bluemix.net
```
{: pre} 

Wenn Sie Ihren Berechtigungsschlüssel kennen, können Sie die CLI zur Verwendung dieses Schlüssels konfigurieren. 

Führen Sie den folgenden Befehl aus, um den Berechtigungsschlüssel festzulegen:

```
wsk property set --auth <Berechtigungsschlüssel>
```
{: pre}

**Tipp:** Die OpenWhisk-CLI speichert standardmäßig die festgelegten Eigenschaften in `~/.wskprops`. die Speicherposition dieser Datei kann durch das Festlegen der Umgebungsvariablen `WSK_CONFIG_FILE` geändert werden.  

Versuchen Sie, [eine Aktion zu erstellen und auszuführen](./index.html#openwhisk_start_hello_world), um Ihre CLI-Konfiguration zu überprüfen.

## {{site.data.keyword.openwhisk_short}}-Befehlszeilenschnittstelle (CLI) verwenden

Wenn Sie Ihre Umgebung konfiguriert haben, können Sie mit der Verwendung der {{site.data.keyword.openwhisk_short}}-Befehlszeilenschnittstelle zu folgenden Zwecken beginnen:

* Sie können Code-Snippets oder Aktionen in {{site.data.keyword.openwhisk_short}} ausführen. Siehe [Aktionen erstellen und aufrufen](./openwhisk_actions.html).
* Sie können Ihre Aktionen durch Auslöser und Regeln so einrichten, dass sie auf Ereignisse reagieren. Siehe [Auslöser und Regeln erstellen](./openwhisk_triggers_rules.html).
* Sie können sich informieren, wie Aktionen in Paketen gebündelt und externe Ereignisquellen konfiguriert werden. Siehe [Pakete verwenden und erstellen](./openwhisk_packages.html).
* Sie können den Katalog der Pakete durchsuchen und Ihre Anwendungen durch externe Services wie zum Beispiel eine [Cloudant-Ereignisquelle](./openwhisk_cloudant.html) erweitern. Siehe [Für OpenWhisk eingerichtete Services verwenden](./openwhisk_catalog.html).

## CLI für die Verwendung eines HTTPS-Proxy konfigurieren

Die CLI kann so eingerichtet werden, dass ein HTTPS-Proxy verwendet werden kann. Um einen HTTPS-Proxy einzurichten, muss die Umgebungsvariable `HTTPS_PROXY` erstellt werden. Die Variable muss auf die Adresse des HTTPS-Proxy festgelegt werden und der Port muss das folgende Format haben:
`{PROXY IP}:{PROXY PORT}`.
