---

 

copyright:

  years: 2015, 2016

 

---
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# 开发方式 CLI
{: #devmodecli}

*上次更新时间：2016 年 2 月 25 日*

开发方式 (dev_mode) 是一种 Bluemix 功能，您可以在应用程序于云中运行时将该功能与应用程序搭配使用。开发方式包括 dev_mode 命令行界面。dev_mode CLI 构建为 cf CLI 插件并同时支持 Liberty 和 IBM Node.js 应用程序。

dev_mode CLI 提供以下功能：
- 将应用程序在开发方式和正常方式之间切换。
- 逐步更新应用程序文件，而无需新的推送。
- 在现有容器中启动、停止或重新启动应用程序。

## 入门
**先决条件：**开始之前，请安装 Cloud Foundry CLI。请参阅[使用 Cloud Foundry 命令行界面开始编码](https://github.com/cloudfoundry/cli)，以获取详细信息。 


使用以下其中一种方法来安装 dev_mode 命令行工具：
- 本地安装。
  1. 从 [IBM Bluemix CLI Plugin Repository](http://plugins.ng.bluemix.net) 下载适用于您的平台的 dev_mode 插件。
  2. 通过使用 cf install-plugin 命令来安装 dev_mode 插件：
  
        ```
        cf install-plugin dev_mode-linux_amd64
        ```

- 从 Bluemix CLI 存储库进行安装。
  1. 通过使用以下命令将 bluemix-repo 存储库添加到 Cloud Foundry CLI 存储库：
  
        ```
        cf add-plugin-repo bluemix-repo http://plugins.ng.bluemix.net
        ```

  2. 键入 cf repo-plugins。dev_mode 插件会显示在 bluemix-repo 存储库中。
		
		```
        cf repo-plugins
        ```
  
  3. 通过使用以下命令将 dev_mode 插件安装到 Cloud Foundry CLI 插件：
  
        ```
        cf install-plugin dev_mode -r bluemix-repo
        ```

## 使用量
**要显示所有 dev_mode CLI 命令，请使用以下命令：**

```
cf plugins```

### dev_mode 命令

### mode

```
cf mode <appName> <dev|normal>
```

更改应用程序方式。

### 状态

```
cf status <appName>
```

显示应用程序方式和运行时状态。

### update-file

```
cf update-file <remotePath> <localPath> [command_options]
```

更新云中的应用程序文件。

命令选项：

**expand**

指示上传的文件是否必须从 zip 文件中截取。

**restart**

文件更新后，重新启动应用程序运行时。
  
### delete-file

```
cf delete-file <remotePath> [command_options]
```

删除云中的应用程序文件。

命令选项：

**restart**

文件删除后，重新启动应用程序运行时。

### start-inplace

```
cf start-inplace <appName>
```

在现有容器中启动应用程序。

### stop-inplace

```
cf stop-inplace <appName>
```

在现有容器中停止应用程序。

### restart-inplace

```
cf restart-inplace <appName>
```

在现有容器中重新启动应用程序。



### help

```
cf help <commandName>
```
显示有关命令的帮助。
