---



copyright:

  years: 2015, 2017
lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Einführung in die {{site.data.keyword.Bluemix_notm}}-CLI
{: #getting-started}

Die {{site.data.keyword.Bluemix_notm}}-Befehlszeilenschnittstelle (CLI) stellt eine einheitliche Möglichkeit zur Interaktion mit Ihren Anwendungen, Containern, Infrastrukturen und weiteren Services über eine Befehlszeilenschnittstelle bereit. 

**Einschränkung:** Die {{site.data.keyword.Bluemix_notm}}-CLI wird nicht von Cygwin unterstützt. Die {{site.data.keyword.Bluemix_notm}}-CLI darf daher nicht im Fenster mit der Cygwin-Befehlszeile verwendet werden.

**Hinweis:** Wenn sich in Ihrem Netz zwischen dem Host, auf dem die CLI ausgeführt wird, und {{site.data.keyword.Bluemix_notm}} ein HTTP-Proxy-Server befindet, müssen Sie den Hostnamen oder die IP-Adresse des Proxy-Servers in der Umgebungsvariablen HTTP_PROXY angeben.

**Hinweis:** In der Installation des {{site.data.keyword.Bluemix_notm}}-CLI-Tools ist eine Cloud Foundry-Befehlszeilenschnittstelle enthalten. Es ist jedoch nicht zulässig, {{site.data.keyword.Bluemix_notm}}-CLI-Befehle `bx xxx` und Cloud Foundry-CLI-Befehle `cf xxx` gemischt zu verwenden, wenn Sie eine eigene CF-CLI-Installation haben. Verwenden Sie stattdessen `bluemix cf`, wenn Sie Cloud Foundry-Ressourcen mit der CF-CLI verwalten wollen. Dadurch werden im Back-End Befehle aus der enthaltenen Cloud Foundry-CLI in einem gemeinsam genutzten Kontext mit der {{site.data.keyword.Bluemix_notm}}-CLI ausgeführt.  Darüber hinaus ist der Befehl `bluemix cf api/login/logout/target` nicht zulässig. Verwenden Sie stattdessen den Befehl `bluemix api/login/logout/target`.

## {{site.data.keyword.Bluemix_notm}}-CLI installieren
{: #install_bluemix_cli}


Laden Sie unter Mac OS und Windows das [{{site.data.keyword.Bluemix_notm}}-CLI-Paket](/docs/cli/index.html#downloads) herunter und führen Sie anschließend das Installationsprogramm aus.

Führen Sie unter Linux die folgenden Schritte aus:

  1. Laden Sie das Paket herunter und extrahieren Sie es. Beispiel:

  ```
  ~$ tar -xvf Bluemix_CLI.tar.gz
  Bluemix_CLI/
  Bluemix_CLI/update_global_config
  Bluemix_CLI/install_bluemix_cli
  Bluemix_CLI/bx/
  Bluemix_CLI/bx/bash_autocomplete
  Bluemix_CLI/bx/zsh_autocomplete
  Bluemix_CLI/bin/
  Bluemix_CLI/bin/bluemix
  ~$
  ```

  2. Navigieren Sie in das Verzeichnis `Bluemix_CLI` und führen Sie den Befehl `./install_bluemix_cli` mit Rootberechtigung aus. Sie können den Befehl als Rootbenutzer ausführen oder den Befehl `sudo` verwenden, um die Rootberechtigung zu erhalten. Beispiel:

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

Sie können nun mit der Verwendung der {{site.data.keyword.Bluemix_notm}}-CLI beginnen oder weitere Plug-ins installieren.

## Plug-ins installieren
{: #install_plug-in}

Die {{site.data.keyword.Bluemix_notm}}-CLI unterstützt ein Plug-in-Erweiterungsframework, mit dem über die bereits integrierten Befehle hinaus weitere Befehle integriert werden können.


Sie können ein Plug-in aus dem Repository lokal oder von einem fernen Server installieren. {{site.data.keyword.Bluemix_notm}} enthält Repositorys, in denen Plug-ins für die {{site.data.keyword.Bluemix_notm}}-CLI und die Cloud Foundry-CLI gehostet werden:

   * [Plug-in-Repository für die {{site.data.keyword.Bluemix_notm}}-CLI](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![Symbol für externen Link](../../../icons/launch-glyph.svg) - Diese Komponente hostet Plug-ins für die {{site.data.keyword.Bluemix_notm}}-CLI.

Führen Sie die folgenden Schritte aus, um die Installation vom Repository aus durchzuführen:

  1. Suchen Sie das Plug-in im Repository. Nach der Installation der {{site.data.keyword.Bluemix_notm}}-CLI wird standardmäßig das offizielle Repository `Bluemix` hinzugefügt. Sie können die Plug-ins im Repository `Bluemix` mit dem Befehl `bluemix plugin repo-plugins` auflisten. Beispiel:

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. Installieren Sie das Plug-in über das `Bluemix`-Repository mit dem Befehl `bluemix plugin install`. Beispiel:

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```


Führen Sie die folgenden Schritte aus, um in Ihrer lokalen Umgebung ein Plug-in zu installieren:

  1. Laden Sie das Plug-in herunter. Beispiel:

  ```
  ~$ wget http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2--2016-02-18 14:02:12-- http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2
  Resolving public.dhe.ibm.com... 9.17.248.112
  Connection to public.dhe.ibm.com|9.17.248.112|:80... connected.
  HTTP request sent, awaiting response... 200 OK
  Length: 9857792 (9.4M) [text/plain]
  Saving to: 'auto-scaling-darwin-amd64-0.2.2'

  auto-scaling-darwin-0.2.2 100%[===================>] 9.40M 518KB/s in 22s

  2016-02-18 14:02:34 (443 KB/s) - `auto-scaling-darwin-amd64-0.2.2' saved [9857792/9857792]
  ```

  2. Auf UNIX-ähnlichen Systemen müssen Sie aus der heruntergeladenen Datei eine ausführbare Datei machen. Verwenden Sie hierfür den Befehl `chmod`. Beispiel:

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. Installieren Sie das Plug-in mit dem Befehl `bluemix plugin install`. Beispiel:

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

Führen Sie die folgenden Schritte aus, um die Installation von einem fernen Server aus durchzuführen:

  1. Installieren Sie das Plug-in über eine remote URL direkt mit dem Befehl `bluemix plugin install`. Beispiel:

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```


Sie können nun die {{site.data.keyword.Bluemix_notm}}-Befehlszeilen verwenden. Führen Sie den Befehl `bluemix help` aus, um eine Liste der Befehle mit Beschreibungen anzuzeigen. 
