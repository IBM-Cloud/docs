---



copyright:

  years: 2015, 2017
lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 開始使用 {{site.data.keyword.Bluemix_notm}} CLI
{: #getting-started}

{{site.data.keyword.Bluemix_notm}} CLI 提供統一方式，可讓您使用指令行介面與應用程式、容器、基礎架構以及其他服務互動。 

**限制**：Cygwin 不支援 {{site.data.keyword.Bluemix_notm}} CLI，因此請不要在 Cygwin 指令行視窗中使用 {{site.data.keyword.Bluemix_notm}} CLI。

**附註**：如果您的網路在執行 CLI 的主機與 {{site.data.keyword.Bluemix_notm}} 之間包含 HTTP Proxy 伺服器，則必須在 HTTP_PROXY 環境變數指定 Proxy 伺服器的主機名稱或 IP 位址。

**附註：**{{site.data.keyword.Bluemix_notm}} CLI 工具已將 Cloud Foundry 指令行介面組合在其安裝中。不過，如果您有自己的 cf cli 安裝，則不容許混合使用 {{site.data.keyword.Bluemix_notm}} CLI 指令 `bx xxx` 與 Cloud Foundry CLI 指令 `cf xxx`。如果您要使用 cf cli 來管理 Cloud Foundry 資源，請改為使用 `bluemix cf`。在後端中，它會使用 {{site.data.keyword.Bluemix_notm}} CLI 在共用環境定義中執行組合 Cloud Foundry CLI 的指令。此外，不容許 `bluemix cf api/login/logout/target`，請改為使用 `bluemix api/login/logout/target`。

## 安裝 {{site.data.keyword.Bluemix_notm}} CLI
{: #install_bluemix_cli}


若為 Mac OS 及 Windows，請下載 [{{site.data.keyword.Bluemix_notm}} CLI 套件](/docs/cli/index.html#downloads)，然後執行安裝程式。

若為 Linux，請遵循下列步驟：

  1. 下載並解壓縮套件。例如：

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

  2. 移至 `Bluemix_CLI` 目錄，然後使用 root 許可權來執行 `./install_bluemix_cli` 指令。您可以使用 root 使用者身分執行此指令，或使用 `sudo` 指令來取得 root 許可權。例如：

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

您現在可以開始使用 {{site.data.keyword.Bluemix_notm}} CLI，或安裝其他外掛程式。

## 安裝外掛程式
{: #install_plug-in}

{{site.data.keyword.Bluemix_notm}} CLI 支援外掛程式延伸架構以整合內建指令以外的其他指令。


您可以在本端或從遠端伺服器，從儲存庫安裝外掛程式。{{site.data.keyword.Bluemix_notm}} 的儲存庫可管理 {{site.data.keyword.Bluemix_notm}} CLI 外掛程式及 Cloud Foundry CLI 外掛程式：

   * [{{site.data.keyword.Bluemix_notm}} CLI 外掛程式儲存庫](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![外部鏈結圖示](../../../icons/launch-glyph.svg)，其管理 {{site.data.keyword.Bluemix_notm}} CLI 的外掛程式。

若要從儲存庫安裝，請採取下列步驟：

  1. 尋找儲存庫中的外掛程式。安裝 {{site.data.keyword.Bluemix_notm}} CLI 之後，依預設會新增正式儲存庫 `Bluemix`。您可以使用 `bluemix plugin repo-plugins` 指令來列出 `Bluemix` 儲存庫中的外掛程式。例如：

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. 使用 `bluemix plugin install` 指令，從 `Bluemix` 儲存庫安裝外掛程式。例如：

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```


若要從本端環境安裝外掛程式，請採取下列步驟：

  1. 下載外掛程式。例如：

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

  2. 對於 UNIX 型系統，您必須使用 `chmod` 指令，將下載的檔案設為可執行檔。例如：

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. 使用 `bluemix plugin install` 指令，以安裝外掛程式。例如：

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

若要從遠端伺服器安裝，請採取下列步驟：

  1. 使用 `bluemix plugin install` 指令，直接從遠端 URL 安裝外掛程式。例如：

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```


您現在已準備好使用 {{site.data.keyword.Bluemix_notm}} 指令行。執行 `bluemix help`，以查看指令及說明的清單。 
