---



copyright:

  years: 2015, 2017
lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} CLI 入门
{: #getting-started}

{{site.data.keyword.Bluemix_notm}} CLI 提供了一种统一的方式，供您通过命令行界面与应用程序、容器、基础架构和其他服务进行交互。 

**限制**：Cygwin 不支持 {{site.data.keyword.Bluemix_notm}} CLI，因此请勿在 Cygwin 命令行窗口中使用 {{site.data.keyword.Bluemix_notm}} CLI。

**注**：如果您的网络中有 HTTP 代理服务器位于运行 CLI 的主机和 {{site.data.keyword.Bluemix_notm}} 之间，那么必须在 HTTP_PROXY 环境变量中指定该代理服务器的主机名或 IP 地址。

**注：**{{site.data.keyword.Bluemix_notm}} CLI 工具在其安装中捆绑了 Cloud Foundry 命令行界面。但是，如果您有自己的 cf CLI 安装，那么不允许混合使用 {{site.data.keyword.Bluemix_notm}} CLI 命令 `bx xxx` 和 Cloud Foundry CLI 命令 `cf xxx`。如果要使用 cf CLI 来管理 Cloud Foundry 资源，请改为使用 `bluemix cf`。它会在与 {{site.data.keyword.Bluemix_notm}} CLI 共享的上下文中，在后端运行捆绑的 Cloud Foundry CLI 的命令。此外，也不允许使用 `bluemix cf api/login/logout/target`，请改为使用 `bluemix api/login/logout/target`。

## 安装 {{site.data.keyword.Bluemix_notm}} CLI
{: #install_bluemix_cli}


对于 Mac OS 和 Windows，请下载 [{{site.data.keyword.Bluemix_notm}} CLI 包](/docs/cli/index.html#downloads)，并运行安装程序。

对于 Linux，请执行以下步骤：

  1. 下载包，并对其解压缩。例如：

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

  2. 转至 `Bluemix_CLI` 目录，然后使用根权限运行 `./install_bluemix_cli` 命令。可以通过 root 用户身份运行此命令，也可以使用 `sudo` 命令来获取根权限。例如：

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

现在，可以开始使用 {{site.data.keyword.Bluemix_notm}} CLI 或安装其他插件。

## 安装插件
{: #install_plug-in}

除了内置命令外，{{site.data.keyword.Bluemix_notm}} CLI 还支持通过插件扩展框架来集成其他命令。


您可以在本地或从远程服务器通过存储库安装插件。{{site.data.keyword.Bluemix_notm}} 具有用于托管 {{site.data.keyword.Bluemix_notm}} CLI 插件和 Cloud Foundry CLI 插件的存储库：

   * [{{site.data.keyword.Bluemix_notm}} CLI 插件存储库](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![外部链接图标](../../../icons/launch-glyph.svg)，用于托管 {{site.data.keyword.Bluemix_notm}} CLI 的插件。

要从存储库进行安装，请执行以下步骤：

  1. 在存储库中找到插件。安装了 {{site.data.keyword.Bluemix_notm}} CLI 后，缺省情况下将添加官方存储库 `Bluemix`。可以使用 `bluemix plugin repo-plugins` 命令列出 `Bluemix` 存储库中的插件。例如：

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. 使用 `bluemix plugin install` 命令从 `Bluemix` 存储库安装插件。例如：

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```


要在本地环境中安装插件，请执行以下步骤：

  1. 下载插件。例如：

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

  2. 对于类 UNIX 系统，必须使用 `chmod` 命令使下载的文件成为可执行文件。例如：

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. 使用 `bluemix plugin install` 命令安装插件。例如：

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

要从远程服务器进行安装，请执行以下步骤：

  1. 使用 `bluemix plugin install` 命令直接通过远程 URL 安装插件。例如：

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```


现在，您已准备好使用 {{site.data.keyword.Bluemix_notm}} 命令行。请运行 `bluemix help` 以查看命令列表及其描述。 
