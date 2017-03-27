---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-10"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# 有关运行时的故障诊断
{: #runtimes}

使用 {{site.data.keyword.Bluemix}} 运行时的时候，可能会遇到问题。在许多情况下，只需执行几个简单的步骤即可解决这些问题。
{:shortdesc}


## 推送应用程序时使用过时的 buildpack
{: #ts_loading_bp}

您可能在推送应用程序时无法使用最新的 buildpack 组件。可以使用具有内置机制的 buildpack 来阻止装入过时的组件，或者可以在推送或重新编译打包应用程序之前，删除应用程序高速缓存目录中的内容。 

在更新 buildpack 后推送或重新编译打包应用程序时，不会自动装入最新的 buildpack 组件。结果应用程序就从高速缓存使用过时的 buildpack 组件。自上次推送应用程序以来已应用到 buildpack 的更新未实施。
{: tsSymptoms}

某些 buildpack 未配置为从因特网自动下载所有更新的组件以确保您始终使用最新的版本。
{: tsCauses} 

您可以使用具有内置机制来避免装入过时组件的 buildpack，例如以下 buildpack：
{: tsResolve}

  * [Cloud Foundry Java buildpack ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://github.com/cloudfoundry/java-buildpack){: new_window}. 此 buildpack 具有内置机制来确保使用 buildpack 的最新版本。有关此机制如何工作的更多信息，请参阅 [extending-caches.md ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}。 
  * [Cloud Foundry Node.js buildpack ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}。此 buildpack 通过使用环境变量来提供类似功能。要使 Node.js buildpack 每次都能够从因特网下载节点模型，请在 cf 命令行界面中键入以下命令： 	
  ```
  set NODE_MODULES_CACHE=false
  ```

如果您使用的 buildpack 不提供自动装入最新组件的机制，那么您可以手动删除高速缓存目录中的内容，并重新推送应用程序。请使用以下步骤：

 1. 检出空 buildpack 的分支，例如 https://github.com/ryandotsmith/null-buildpack。有关如何检出分支的信息，请参阅 [Git Basics - Getting a Git Repository ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}。  
 2. 将以下行添加到 `null-buildpack/bin/compile` 文件，并落实更改。有关如何落实更改的信息，请参阅 [Git Basics - Recording Changes to the Repository ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}。
  ```
  rm -rfv $2/*
  ```
 3. 通过使用以下命令，使用修改用于删除高速缓存的空 buildpack 推送应用程序。完成此步骤后，会删除应用程序高速缓存目录中的所有内容。
  ```
  cf push appname -p app_path -b <modified_null_buildpack>
  ```
 4. 通过使用以下命令，使用想要使用的最新 buildpack 推送应用程序： 
  ```
  cf push appname -p app_path -b <latest_buildpack>
  ```
 
## 来自 PHP buildpack 的注意消息
{: #ts_phplog}

您可能会在日志中看到包含“注意”的消息。通过更改日志记录级别，可以停止记录这些消息。	

使用 PHP buildpack 将应用程序推送到 {{site.data.keyword.Bluemix_notm}} 时，可能会看到包含`注意`的消息：
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] 错误 [26-Jan-2015 14:00:59] 注意：[pool www] 当 FPM 未以 root 用户身份运行时，会忽略“user”伪指令
• 2015-01-26T15:01:00.63+0100 [App/0] 错误 [26-Jan-2015 14:00:59] 注意：[pool www] 当 FPM 未以 root 用户身份运行时，会忽略“user”伪指令
• 2015-01-26T15:01:00.63+0100 [App/0] 错误 [26-Jan-2015 14:00:59] 注意：fpm 正在运行，pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] 错误 [26-Jan-2015 14:00:59] 注意：准备就绪，可处理连接
```
在 PHP buildpack 中，error_log 参数用于定义日志记录级别。缺省情况下，`error_log` 参数的值为 **stderr notice**。以下示例显示 Cloud Foundry 所提供 PHP buildpack 的 `nginx-defaults.conf` 文件中的缺省日志记录级别配置。有关更多信息，请参阅 [cloudfoundry/php-buildpack ![外部链接图标](../icons/launch-glyph.svg " 外部链接图标")](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}。
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```
	
`注意`消息仅供参考，可能并不表示有问题。您可以通过在 buildpack 的 nginx-defaults.conf 文件中将日志记录级别从 `stderr notice` 更改为 `stderr error` 来停止记录这些消息。例如： 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
有关如何更改缺省日志记录配置的更多信息，请参阅 [error_log ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}。
	

## 无法将第三方 Python 库导入 {{site.data.keyword.Bluemix_notm}}
{: #ts_importpylib}

您可能无法将第三方 Python 库导入 {{site.data.keyword.Bluemix_notm}}。要解决该问题，请将配置文件添加到 Python 应用程序的根目录中。

当您尝试导入第三方 Python 库（如 `web.py` 库）时，`cf push` 命令会失败。
{: tsSymptoms}

Python 应用程序缺少配置信息。
{: tsCauses}

将 `requirements.txt` 文件和 `Procfile` 文件添加到 Python 应用程序的根目录中。以下信息假定您要导入 `web.py` 库：
{: tsResolve}

 1. 将 `requirements.txt` 文件添加到 Python 应用程序的根目录中。
 
 `requirements.txt` 文件指定 Python 应用程序所需的库数据包以及数据包版本。以下示例显示的是 `requirements.txt` 文件的内容，其中 `web.py==0.37` 指示要下载的 `web.py` 库版本为 0.37，而 `wsgiref==0.1.2` 指示 web.py 库所需的 Web 服务器网关接口版本为 0.1.2。 
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	 有关如何配置 `requirements.txt` 文件的更多信息，请参阅 [Requirements files](https://pip.readthedocs.org/en/1.1/requirements.html)。

 2. 将 `Procfile` 文件添加到 Python 应用程序的根目录中。`Procfile` 文件中必须包含 Python 应用程序的启动命令。在以下命令中，*yourappname* 是 Python 应用程序的名称，*PORT* 是 Python 应用程序在接收应用程序用户请求时必须使用的端口号。*$PORT* 为可选项。如果不在启动命令中指定 PORT，那么会使用应用程序内 `VCAP_APP_PORT` 环境变量下的端口号。 
	```
	web: python <yourappname>.py $PORT
	```

现在，您可以将第三方 Python 库导入 {{site.data.keyword.Bluemix_notm}}。	


## 实例详细信息页面上的操作按钮已禁用
{: #ts_actionsbutton}

“实例详细信息”页面上的“操作”按钮已禁用。
{: tsSymptoms} 

发生此问题的原因如下：
{: tsCauses}

 * 应用程序不是 Java&trade; Web 应用程序。“运行时管理实用程序”(RMU) 仅支持使用 Liberty buildpack 部署的 Web 应用程序。
 * 应用程序不是使用嵌入式 Liberty buildpack 部署的。
 * 应用程序是使用 Liberty buildpack 早期版本部署的。

如果该问题是由 Liberty buildpack 早期版本导致的，请在 {{site.data.keyword.Bluemix_notm}} 中重新部署应用程序。否则，您可以向支持团队提供以下客户机应用程序日志文件：
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
 
  
## 打开跟踪或转储窗口时需要凭证
{: #ts_username}

打开跟踪或转储窗口时需要用户名和密码。
{: tsSymptoms}

由于登录会话超时，发生此问题。
{: tsCauses}

重新输入用户名和密码。
{: tsResolve}


## 正在执行跟踪或转储操作时发生错误
{: #ts_target}

正在执行跟踪或转储操作时显示错误消息。该消息指示应用程序的目标实例未处于运行状态：	
{: tsSymptoms}

```
实例 0：已成功设置跟踪规范
实例 2：已成功设置跟踪规范
实例 1：应用程序 abcd 的目标实例 1 未处于运行中状态。
实例 3：已成功设置跟踪规范
实例 4：已成功设置跟踪规范
```

发生此问题的原因如下：
{: tsCauses} 

  * 跟踪或转储管理功能仅用于正在运行的应用程序实例。无法对已停止、正在启动或已崩溃的应用程序实例使用跟踪或转储操作。
  * 打开跟踪或转储对话框时，应用程序实例的状态正在更改。 

关闭窗口，然后重新打开该窗口。
{: tsResolve} 


## 实例具有不同的 traceSpecification 配置
{: #ts_different_config}

对于一个应用程序的不同实例，您可能会看到不同的 traceSpecification 配置。
{: tsSymptoms}

发生此行为的原因如下：
{: tsCauses}

  * 您先前更改了一个或多个实例的配置。如果更改一个实例的 traceSpecification 配置，该更改并不会应用到同一应用程序的其他实例。例如，您的应用程序使用 log4j，并且此应用程序有 2 个实例。您可以将实例 0 的日志级别从参考更改为调试，但实例 1 的日志级别仍为参考。
  
  * 应用程序向外扩展后有了新的实例。RMU 不会将现有实例的 traceSpecification 配置应用到向外扩展的新实例。新实例会使用缺省配置。例如，您的应用程序使用 log4j，并且此应用程序有 1 个实例。您可以将此实例的日志级别从信息更改为调试。进行此更改后，如果将应用程序向外扩展到 2 个实例，那么新实例的日志级别将为参考，而不是调试。

无需执行任何操作。这是正常的情况。
{: tsResolve} 


## 超出磁盘配额
{: #ts_diskquota}

您可能会在应用程序日志中看到超过磁盘配额的消息。

您在应用程序日志中看到`超过磁盘配额`错误消息。
{: tsSymptoms}

此问题由以下其中一个原因导致：
{: tsCauses} 

  * 转储文件是使用运行中的应用程序实例生成的，并且这些文件用完了分配的磁盘配额。缺省情况下，一个应用程序实例的磁盘配额是 1 GB。您可以通过单击**仪表板>应用程序>应用程序运行时**来检查磁盘使用情况。以下示例显示某个应用程序的两个实例的运行时信息，包括磁盘使用情况：
    ```
    实例  状态	  CPU	 内存使用情况  磁盘使用情况

	    0		 运行中	1.0%	 344.8MB/512MB	236.8MB/1GB
	    2		 运行中	2.3%	 361.2MB/512MB	235.7MB/1GB
    ```
  * 磁盘配额受当前组织配额限制。

使用以下其中一种方法：
{: tsResolve} 

  * 下载转储文件后将其删除。
  * 通过将以下条目包含在部署清单中，使用更大的磁盘配额重新部署应用程序：
    ```
	disk_quota：2048
	```
	
