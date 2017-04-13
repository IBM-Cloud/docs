---



copyright:

  years: 2015, 2017
lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Getting started with {{site.data.keyword.Bluemix_notm}} CLI
{: #getting-started}

{{site.data.keyword.Bluemix_notm}} CLI provides a unified way for you to interact with your applications, containers, infrastructures and other services by using a command line interface. 

**Restriction**: The {{site.data.keyword.Bluemix_notm}} CLI is not supported by Cygwin, so do not use the {{site.data.keyword.Bluemix_notm}} CLI in the Cygwin command line window.

**Note**: If your network contains an HTTP proxy server between the host that runs the CLI and {{site.data.keyword.Bluemix_notm}}, you must specify the host name or IP address of the proxy server in the HTTP_PROXY environment variable.

**Note:** {{site.data.keyword.Bluemix_notm}} CLI tool bundled a Cloud Foundry command line interface in its installation. However, it is not allowed to mix-use {{site.data.keyword.Bluemix_notm}} CLI commands `bx xxx` and Cloud Foundry CLI commands `cf xxx` if you have your own cf cli installation. Instead, use `bluemix cf` if you want to use cf cli to manage Cloud Foundry resources. In the back end, it runs commands of the bundled Cloud Foundry CLI in a shared context with the {{site.data.keyword.Bluemix_notm}} CLI.  Besides,  `bluemix cf api/login/logout/target` is not allowed, use `bluemix api/login/logout/target` instead.

## Installing {{site.data.keyword.Bluemix_notm}} CLI
{: #install_bluemix_cli}


For Mac OS and Windows, download the [{{site.data.keyword.Bluemix_notm}} CLI package](/docs/cli/index.html#downloads), and run the installer.

For Linux, follow these steps:

  1. Download the package, and extract it. For example:

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

  2. Go to the `Bluemix_CLI` directory, and run the `./install_bluemix_cli` command with root permission. You can run the command as a root user or use the `sudo` command to get the root permission. For example:

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

You can now start using {{site.data.keyword.Bluemix_notm}} CLI or install additional plug-ins.

## Installing a plug-in
{: #install_plug-in}

{{site.data.keyword.Bluemix_notm}} CLI supports a plug-in extension framework to integrate other commands besides the built-in ones.


You can install a plug-in from the repository,  locally or from a remote server. {{site.data.keyword.Bluemix_notm}} has repositories that host {{site.data.keyword.Bluemix_notm}} CLI plug-ins and Cloud Foundry CLI plug-ins:

   * [{{site.data.keyword.Bluemix_notm}} CLI plug-ins repository](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![External link icon](../../../icons/launch-glyph.svg), which hosts plug-ins  for {{site.data.keyword.Bluemix_notm}} CLI.

To install from the repository, take the following steps:

  1. Find the plug-in in the repository. After you have installed {{site.data.keyword.Bluemix_notm}} CLI, the official repository `Bluemix` is added by default. You can list the plug-ins in the `Bluemix` repository by using the `bluemix plugin repo-plugins` command. For example:

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. Install the plug-in from the `Bluemix` repository by using the `bluemix plugin install` command. For example:

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```


To install a plug-in from your local environment, take the following steps:

  1. Download the plug-in. For example:

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

  2. For UNIX-like systems, you must make the downloaded file executable by using the `chmod` command. For example:

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. Install the plug-in by using the `bluemix plugin install` command. For example:

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

To install from a remote server, take the following steps:

  1. Install the plug-in from a remote URL directly by using the `bluemix plugin install` command. For example:

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```


You're now ready to use {{site.data.keyword.Bluemix_notm}} commmand lines. Run `bluemix help` to see the list of commands and  desciptions. 
