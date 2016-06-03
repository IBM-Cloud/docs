---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#更新应用程序
{: #updatingapps}

*上次更新时间：2016 年 5 月 9 日*


您可以使用 cf push 命令或 {{site.data.keyword.Bluemix}} DevOps Services 来更新 {{site.data.keyword.Bluemix_notm}} 中的应用程序。在许多情况下，即便对于内置 buildpack（例如 Node.js），也必须提供 -c 参数来指定用于启动应用程序的命令。
{:shortdesc}

##创建并使用定制域
{: #domain}

您可以在应用程序的 URL 中使用定制域，而不使用缺省 {{site.data.keyword.Bluemix_notm}} 系统域，即 mybluemix.net。

域提供了分配给 {{site.data.keyword.Bluemix_notm}} 中组织的 URL 路径。要使用定制域，必须在公共 DNS 服务器上注册定制域，在 {{site.data.keyword.Bluemix_notm}} 中配置定制域，然后将定制域映射到公共 DNS 服务器上的 {{site.data.keyword.Bluemix_notm}} 系统域。定制域映射到 {{site.data.keyword.Bluemix_notm}} 系统域后，对定制域的请求会路由到 {{site.data.keyword.Bluemix_notm}} 中的应用程序。

可以使用 {{site.data.keyword.Bluemix_notm}} 用户界面或 cf 命令行界面在 {{site.data.keyword.Bluemix_notm}} 中创建并使用定制域。

* 使用 {{site.data.keyword.Bluemix_notm}} 用户界面：

  1. 为组织创建定制域。
    
	1. 在 {{site.data.keyword.Bluemix_notm}} **仪表板**的菜单栏上，单击**管理组织**。
	
	2. 在**域**选项卡上，单击**添加域**，输入定制域名，然后单击**保存**。
    	
  2. 将包含定制域的路径添加到应用程序。
  
    1. 在 {{site.data.keyword.Bluemix_notm}} **仪表板**的菜单栏上，单击要添加路径的应用程序的磁贴。这将显示“**概述**”页面。
	
	2. 在**概述**页面上的应用程序菜单中，单击**编辑路径和应用程序访问权**。
	
	3. 单击**添加路径**，然后指定要用于应用程序的路径。
	
* 使用 cf 命令行界面：
  
  1. 通过输入以下命令，为组织创建定制域：
    
    ```
    cf create-domain <your org name> mydomain
    ```
    
    *organization_name*
  
        组织的名称。
	  
    *mydomain*
    
        要使用的定制域名。
	  
  2. 通过输入以下命令，将包含定制域的路径添加到应用程序：
    
    ```
    cf map-route myapp mydomain -n host_name
    ```
    
    *myapp*
      
    	应用程序的名称。
  	
    *mydomain*
      
    	定制域的名称。
	
    *host_name*
    
        要用于应用程序的路径中的主机名。
	
在 {{site.data.keyword.Bluemix_notm}} 中配置定制域后，必须将该定制域映射到您注册的 DNS 服务器上的 {{site.data.keyword.Bluemix_notm}} 系统域：

  1. 为 DNS 服务器上的定制域名设置“CNAME”记录。
  2. 将定制域名映射到运行应用程序的 {{site.data.keyword.Bluemix_notm}} 区域的安全端点。使用以下区域端点来提供在 {{site.data.keyword.Bluemix_notm}} 中分配给您组织的 URL 路径：
  
    * US-SOUTH：`secure.us-south.bluemix.net`
    * EU-GB：`secure.eu-gb.bluemix.net`
    * AU-SYD：`secure.au-syd.bluemix.net`
  
在浏览器或命令行界面中，输入以下 URL 来访问 myapp 应用程序：

```
http://host_name.mydomain
```

**注：**要除去孤立的路径，请使用以下命令：

```
cf delete-route domain -n hostname -f
```

*domain* 是域名，*hostname* 是应用程序的路径中的主机名。有关 **cf delete-route** 命令的更多信息，请键入 `cf delete-route -h`。

##蓝绿部署
{: #blue_green}

{{site.data.keyword.Bluemix_notm}} 支持蓝绿部署方法，以便能够持续交付并尽可能减少停机事件。

*蓝绿部署*是一种零停机部署方法，由两个几乎完全一样的生产环境构成：蓝和绿。这两个环境的不同之处在于工件，开发者有目的地更改了这些工件，并且通常是通过应用程序版本进行更改。在任何给定时间，必须至少有一个环境处于活动状态。使用蓝绿部署方法，您可以实现以下优势：

* 使软件迅速从最终测试阶段过渡到实际生产。
* 部署应用程序的新版本时，不必中断到应用程序的流量。
* 快速回滚。如果其中一个环境有问题，可以迅速切换到其他环境。

如果已经将应用程序部署到 {{site.data.keyword.Bluemix_notm}}，并且要将应用程序更新为新版本，那么可以使用以下两种方法之一来确保蓝绿部署。

###示例：使用 cf rename 命令

在此示例中，应用程序的名称为 Blue。此示例演示了如何使用 **cf rename** 命令来更新 *Blue* 的版本，而不中断到应用程序的流量。现在，在更新版本可用时，可以选择删除 *Blue* 的旧版本。

1. 将 *Blue* 应用程序推送到 {{site.data.keyword.Bluemix_notm}}。
  
  ```
  cf push Blue
  ```
  
  **结果：**该 *Blue* 应用程序正在运行，并且正在响应 URL `Blue.mybluemix.net`。
  
2. 使用 **cf rename** 命令将 *Blue* 应用程序重命名为 *Green*：
  
  ```
  cf rename Blue Green
  ```
  
  使用 **cf apps** 命令列出当前空间中的应用程序：
  
  ```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  ...
  ```
  
  **结果：**该 *Green* 应用程序正在运行，并且正在响应 URL `Blue.mybluemix.net`。

3. 进行必要的更改，并使更新的 *Blue* 版本准备就绪。将更新的 *Blue* 应用程序推送到 {{site.data.keyword.Bluemix_notm}}：
  
  ```
  cf push Blue
  ```
  
  使用 **cf apps** 命令列出当前空间中的应用程序：
  
  ```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  Blue             started           1/1         1G       1G	 Blue.mybluemix.net
  ...
  ```
  
  **结果：**
    * 应用程序的两个实例已部署：*Blue* 和 *Green*。
	* 该 *Green* 应用程序正在运行，并且正在响应 URL `Blue.mybluemix.net`。
	
4. 可选：如果想要删除应用程序的旧版本 (*Green*)，请使用 **cf delete** 命令。
  
  ```
  cf delete Green -f
  ```
  
  使用 **cf route** 命令列出空间中的路径：
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  ...
  ```
  
  **结果：**该 *Blue* 应用程序正在响应 URL `Blue.mybluemix.net`。
  
###示例：使用 cf map-route 命令

在此示例中，*Blue* 是先前部署的应用程序，*Green* 是更新的版本。此示例演示了如何使用 **cf map-route** 命令来更新 *Blue* 的版本，而不中断到应用程序的流量。现在，在更新版本可用时，可以选择删除 *Blue* 的旧版本。

1. 将 *Blue* 应用程序推送到 {{site.data.keyword.Bluemix_notm}}。
  
  ```
  cf push Blue
  ```
  
  **结果：**该 *Blue* 应用程序正在运行，并且正在响应 URL `Blue.mybluemix.net`。
  
2. 进行必要的更改，并使 *Green* 版本准备就绪。将 *Green* 应用程序推送到 {{site.data.keyword.Bluemix_notm}}：
  
  ```
  cf push Green
  ```
  
  使用 **cf route** 命令列出当前空间中的应用程序：
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  Green            mybluemix.net    Green
  ...
  ```
  
  **结果：**
  
    * 应用程序的两个实例已部署：*Blue* 和 *Green*。
	* 该 *Blue* 应用程序正在响应 URL `Blue.mybluemix.net`。*Green* 应用程序正在响应 URL `Green.mybluemix.net`。
	
3. 将 *Blue* 应用程序映射到 *Green* 应用程序，让 `Blue.mybluemix.net` 的所有流量路由到 *Blue* 应用程序和 *Green* 应用程序。
  
  ```
  cf map-route Green mybluemix.net -n Blue
  ```
  
  使用 cf routes 命令列出空间中的路径：
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue, Green
  Green            mybluemix.net    Green
  ...
  ```
  
  **结果：**

    * 现在，CF 路由器会将 Blue.mybluemix.net 的流量发送到 Blue 应用程序和 Green 应用程序。
	* CF 路由器会继续将 Green.mybluemix.net 的流量发送到 Green 应用程序。
	
4. 验证 *Green* 是否在按预期运行时，请从 *Blue* 应用程序除去 `Blue.mybluemix.net` 路径：
  
  ```
  cf unmap-route Blue mybluemix.net -n Blue
  ```
  
  使用 cf routes 命令列出空间中的路径：
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  Green            mybluemix.net    Green
  ...
  ```
  
  **结果：**CF 路由器停止将流量发送到 *Blue* 应用程序。*Green* 应用程序正在响应以下两个 URL：`Green.mybluemix.net` 和 `Blue.mybluemix.net`。
  
5. 除去 *Green* 应用程序的 `Green.mybluemix.net` 路径。
  
  ```
  cf unmap-route Green mybluemix.net -n Green
  ```
  
  **结果：**CF 路由器停止将流量发送到 *Blue* 应用程序。*Green* 应用程序正在响应 URL `Blue.mybluemix.net`。
  
6. 可选：如果想要删除应用程序的旧版本 (*Blue*)，请使用 `cf delete` 命令。
  
  ```
  cf delete Blue -f
  ```
  
  使用 cf route 命令列出空间中的路径：
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  ...
  ```
  
  **结果：**该 *Green* 应用程序正在响应 URL `Blue.mybluemix.net`。


# 相关链接
{: #rellinks}

## 相关链接
{: #general}

* [蓝绿部署](http://martinfowler.com/bliki/BlueGreenDeployment.html){:new_window}
* [IBM {{site.data.keyword.Bluemix_notm}} DevOps Services](https://hub.jazz.net/){:new_window}
