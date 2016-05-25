---

 

copyright:

  years: 2015，2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 开发方式 CLI
{: #devmodecli}

*上次更新时间：2016 年 4 月 11 日*

通过 Bluemix 开发方式命令行界面 (dev_mode CLI)，您可以更新正在云中运行的应用程序。dev_mode CLI 构建为 cf CLI 插件并同时支持 Liberty 和 IBM Node.js 应用程序。
{: shortdesc}
 

可以使用 dev_mode CLI 执行以下任务：
- 将应用程序在开发方式和正常方式之间切换。
- 逐步更新应用程序文件，而无需新的推送。
- 在现有容器中启动、停止或重新启动应用程序。

## 安装 dev_mode 插件
**先决条件：**开始之前，请安装 Cloud Foundry CLI。有关详细信息，请参阅[使用 Cloud Foundry 命令行界面开始编码](https://github.com/cloudfoundry/cli)。 


使用以下其中一种方法来安装 dev_mode 命令行工具：
- 本地安装。
  1. 从 [IBM Bluemix CLI Plugin Repository](http://plugins.{DomainName}) 下载适用于您的平台的 dev_mode 插件。
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

## 查看 dev_mode 命令
**要显示所有 dev_mode CLI 命令，请使用以下命令：**

```
cf plugins
```

## dev_mode CLI 命令索引
{: #dev_mode_cmds_index}

使用下表中的索引可查看常用 dev_mode CLI 命令：

<table summary="dev_mode 命令索引">
 <thead>
 <th colspan="4">dev_mode 命令</th>
 </thead>
 <tbody> 
 <tr> 
 <td>[help](#help)</td> 
 <td>[mode](#mode)</td> 
 <td>[status](#status)</td>
 <td>[update-file](#update_file)</td>
 </tr> 
 <tr> 
 <td>[delete-file](#delete_file)</td>
 <td>[start-inplace](#start_inplace)</td>
 <td>[stop-inplace](#stop_inplace)</td>
 <td>[restart-inplace](#restart_inplace)</td>
 </tr>
  </tbody> 
 </table> 
*表 1. dev_mode 命令*



## help
{: #help}

显示有关命令的帮助。

```
cf help <commandName>
```


## mode
{: #mode}

更改应用程序方式。

```
cf mode <appName> <dev|normal>
```
<strong>命令选项</strong>：<dl>
   <dt>dev</dt>
   <dd>开发方式。</dd>
   <dt>normal</dt>
   <dd>生产方式。</dd>
   </dl>


## status
{: #status}

显示应用程序方式和运行时状态。
```
cf status <appName>
```



## update-file
{: #update_file}

更新云中的应用程序文件。

```
cf update-file <remotePath> <localPath> [command_options]
```


<strong>命令选项</strong>：<dl>
   <dt>expand</dt>
   <dd>指示上传的文件是否必须从 zip 文件中截取。</dd>
   <dt>restart</dt>
   <dd>文件更新后，重新启动应用程序运行时。</dd>
   </dl>


  
## delete-file
{: #delete_file}

删除云中的应用程序文件。

```
cf delete-file <remotePath> [command_options]
```


<strong>命令选项</strong>：<dl>
   <dt>restart</dt>
   <dd>文件更新后，重新启动应用程序运行时。</dd>
  </dl>


## start-inplace
{: #start_inplace}
在现有容器中启动应用程序。

```
cf start-inplace <appName>
```



## stop-inplace
{: #stop_inplace}
在现有容器中停止应用程序。

```
cf stop-inplace <appName>
```



## restart-inplace
{: #restart_inplace}

在现有容器中重新启动应用程序。

```
cf restart-inplace <appName>
```



# 相关链接
{: #rellinks}

## 相关链接
{: #general}

<!-- Include a link to your full product documentation, pricing sheet, IBM Bluemix prerequisites -->


* [CLI 和开发工具](../../index.html#cli){:new_window}


