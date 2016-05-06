---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 用于推送 Liberty 应用程序的选项
{: #options_for_pushing}

*上次更新时间：2016 年 3 月 23 日*

Bluemix 中 Liberty 服务器的行为由 Liberty buildpack 进行控制。buildpack 可以为特定类的应用程序提供完整运行时环境。这些 buildpack 是在云中提供可移植性并构成开放式云体系结构的关键所在。Liberty buildpack 提供了能够运行 Java EE 7 和 OSGi 应用程序的 WebSphere Liberty 容器。
它支持 Spring 等流行框架，并包含 IBM JRE。WebSphere Liberty 支持适合云的快速应用程序开发。Liberty buildpack 支持多个部署到单个 Liberty 服务器的应用程序。作为 Liberty buildpack 集成到 Bluemix 的一部分，该 buildpack 会确保用于绑定服务的环境变量在 Liberty 服务器中显示为配置变量。

您可以使用以下方法将 Liberty 应用程序部署到 Bluemix。

* 推送独立应用程序
* 推送服务器目录
* 推送打包服务器

重要信息：使用 Liberty buildpack 部署应用程序时，请为应用程序指定至少 512M 的内存限制。有关更多信息，请参阅[内存限制和 Liberty buildpack](memoryLimits.html)。

## 独立应用程序
{: #stand_alone_apps}

独立应用程序（例如 WAR 或 EAR 文件）可部署到 Bluemix 中的 Liberty。

要部署独立应用程序，请运行带有 -p 参数（指向您的 WAR 或 EAR 文件）的 cf push 命令。
例如：

```
    $ cf push <yourappname> -p myapp.war
```
{: #codeblock}

系统会为所部署的独立应用程序提供缺省 Liberty 配置。缺省配置会启用以下 Liberty 功能：

* beanValidation-1.1
* [cdi-1.2](optionsForPushing.html#cdi12)
* ejbLite-3.2
* el-3.0
* jaxrs-2.0
* jdbc-4.1
* jndi-1.0
* jpa-2.1
* jsf-2.2
* jsonp-1.0
* jsp-2.3
* managedBeans-1.0
* servlet-3.1
* websocket-1.1
* icap:managementConnector-1.0
* appstate-1.0

这些功能与 Java EE 7 Web 概要文件功能对应。可以通过设置 JBP_CONFIG_LIBERTY 环境变量来指定其他 Liberty 功能集。例如，要仅启用 jsp-2.3 和 websocket-1.1 功能，请运行以下命令并对应用程序重新编译打包：

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: {features: [jsp-2.3, websocket-1.1]}"
```
{: #codeblock}

注：为了获得最佳结果，请使用 JBP_CONFIG_LIBERTY 环境变量来设置 Liberty 功能，或者使用定制 server.xml 文件将应用程序部署为[服务器目录](optionsForPushing.html#server_directory)或[打包服务器](optionsForPushing.html#packaged_server)。设置此环境变量将确保应用程序只使用其所需的功能，并且不受 buildpack 的缺省 Liberty 功能集更改的影响。如果需要提供功能集以外的额外 Liberty 配置，请使用[服务器目录](optionsForPushing.html#server_directory)或[打包服务器](optionsForPushing.html#packaged_server)选项来部署应用程序。

如果部署了 WAR 文件，那么可以像在内嵌 ibm-web-ext.xml 文件中所设置的那样，在上下文根下访问 Web 应用程序。如果 ibm-web-ext.xml 文件不存在，或者未指定上下文根，那么可在根上下文下访问应用程序。例如，

```
    http://<yourappname>.mybluemix.net/
```
{: #codeblock}

如果部署了 EAR 文件，那么可在根上下文下访问内嵌的 Web 应用程序，如 EAR 部署描述符中所定义。例如，

```
    http://<yourappname>.mybluemix.net/acme/
```
{: #codeblock}

完整的缺省 Liberty server.xml 配置文件如下所示：
```
    <server>
       <featureManager>
          <feature>beanValidation-1.1</feature>
          <feature>cdi-1.2</feature>
          <feature>ejbLite-3.2</feature>
          <feature>el-3.0</feature>
          <feature>jaxrs-2.0</feature>
          <feature>jdbc-4.1</feature>
          <feature>jndi-1.0</feature>
          <feature>jpa-2.1</feature>
          <feature>jsf-2.2</feature>
          <feature>jsonp-1.0</feature>
          <feature>jsp-2.3</feature>
          <feature>managedBeans-1.0</feature>
          <feature>servlet-3.1</feature>
          <feature>websocket-1.1</feature>
          <feature>icap:managementConnector-1.0</feature>
          <feature>appstate-1.0</feature>
       </featureManager>

       <application name='myapp' location='myapp.war' type='war' context-root='/'/>
       <httpEndpoint id='defaultHttpEndpoint' host='*' httpPort='${port}'/>
       <webContainer trustHostHeaderPort='true' extractHostHeaderPort='true'/>
       <include location='runtime-vars.xml'/>
       <logging logDirectory='${application.log.dir}' consoleLogLevel='INFO'/>
       <httpDispatcher enableWelcomePage='false'/>
       <applicationMonitor dropinsEnabled='false' updateTrigger='mbean'/>
       <config updateTrigger='mbean'/>
       <cdi12 enableImplicitBeanArchives='false'/>
       <appstate appName='myapp' markerPath='${home}/../.liberty.state'/>
    </server>
```
{: #codeblock}

### CDI 1.2
{: #cdi12}

由于性能原因，缺省情况下，当只部署 WAR 和 EAR 文件时，会禁用 [CDI1.2 隐式 Bean 归档扫描](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_cdi_behavior.html)。可使用 JBP_CONFIG_LIBERTY 环境变量启用隐式 Bean 归档扫描。
例如：

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: { implicit_cdi: true }"
```    
{: #codeblock}

重要信息：为了使环境变量更改生效，您必须重新编译打包应用程序：

```
    $ cf restage myapp
```
{: #codeblock}

## 服务器目录
{: #server_directory}

在某些情况下，可能需要为您的应用程序提供定制 Liberty 服务器配置。部署 WAR 或 EAR 文件时，如果缺省 server.xml 文件不包含应用程序所需的特定设置，那么可能需要此定制配置。

如果 Liberty 概要文件已安装在工作站上，且已经为应用程序创建 Liberty 服务器，那么可以将该目录的内容推送到 Bluemix。例如，如果 Liberty 服务器名称为 defaultServer，请运行以下命令：

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer
```
{: #codeblock}

如果未在工作站上安装 Liberty 概要文件，那么可以使用以下步骤为您的应用程序创建服务器目录：

1. 创建名为 defaultServer 的目录。
2. 在 defaultServer 目录中创建 apps 目录。
3. 将 WAR 或 EAR 文件复制到 defaultServer/apps 目录中。
4. 在 defaultServer 目录中，创建具有以下示例内容的 server.xml 文件。此外：
  * 务必更新应用程序元素的 location 或 type 属性，以便与您的应用程序的文件名和类型相匹配。
  * 图中的 server.xml 文件显示了最小功能集。您可能需要调整该功能集来满足您的应用程序的需要。

```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
        </featureManager>

        <httpEndpoint id='defaultHttpEndpoint' host='*' httpPort='8080' />

        <application name="myapp" context-root="/" type="war" location="myapp.war"/>
    </server>
```
{: #codeblock}

准备好服务器目录后，可以将其部署到 Bluemix。

```
    $ cf push <yourappname> -p defaultServer
```
{: #codeblock}

注：作为服务器目录的一部分部署的 Web 应用程序可在[上下文根下访问，正如在 Liberty 概要文件中确定的那样](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/twlp_dep_war.html?cp=SSAW57_8.5.5%2F1-3-11-0-5-6)。例如：

```
    http://<yourappname>.mybluemix.net/acme/
```
{: #codeblock}

## 打包服务器
{: #packaged_server}

您还可以将打包服务器文件推送到 Bluemix。打包服务器文件是使用 Liberty 服务器软件包命令创建的。除了应用程序和配置文件之外，打包服务器文件中还包含应用程序所需的共享资源和 Liberty 用户功能。

要打包 Liberty 服务器，请从 Liberty 安装目录使用 ./bin/server package 命令。指定服务器名称，并包含“––include=usr”选项。例如，如果 Liberty 服务器为 defaultServer，请运行以下命令：

```
    $ wlp/bin/server package defaultServer --include=usr
```
{: #codeblock}

此命令会在服务器目录中生成 serverName.zip 文件。然后，您可以使用 cf push 命令将该压缩文件推送到 Bluemix。例如：

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer/defaultServer.zip
```
{: #codeblock}

注：作为打包服务器的一部分部署的 Web 应用程序可在上下文根下访问，正如在 Liberty 概要文件中确定的那样。

### server.xml 文件的修改
{: #modifications_of_serverxml}

推送打包服务器或 Liberty 服务器目录时，Liberty buildpack 会检测 server.xml 文件以及您的应用程序。Liberty buildpack 会对 server.xml 文件进行以下修改。

* buildpack 确保文件中只有一个 httpEndpoint 元素。
* buildpack 确保 httpEndpoint 元素中的 httpPort 属性指向称为 ${port} 的系统变量。buildpack 还会覆盖主机属性。
* buildpack 会将 logging 元素中的 logDirectory 属性设置为指向系统日志目录。
* buildpack 确保 runtime-vars.xml 文件与 server.xml 文件以逻辑方式合并。具体而言，就是 buildpack 将行 *&lt;include location="runtime-vars.xml" /&gt;* 附加到 server.xml 文件。

### 可引用的变量
{: #referenceable_variables}

以下变量是在 runtime-vars.xml 文件中定义的，而且是从推送的 server.xml 文件中引用的。所有变量均区分大小写。

* ${port}：Liberty 服务器正在侦听的 HTTP 端口。
* ${vcap_console_port}：正在运行 vcap 控制台的端口（通常与 ${port} 相同）。
* ${vcap_app_port}：应用程序服务器正在侦听的端口（通常与 ${port} 相同）。
* ${vcap_console_ip}：vcap 控制台的 IP 地址（通常是 Liberty 服务器正在侦听的 IP 地址）。
* ${application_name}：应用程序名称，它是使用 cf push 命令中的选项定义的。
* ${application_version}：此应用程序实例的版本，采用 UUID 格式，例如 b687ea75-49f0-456e-b69d-e36e8a854caa。后续每次推送包含新代码或应用程序工件更改的应用程序时，此变量都会更改。
* ${host}：正在运行应用程序的 DEA 的 IP 地址（通常与 ${vcap_console_ip} 相同）。
* ${application_uris}：可用于访问此应用程序的端点的 JSON 样式数组，例如：myapp.mydomain.com。
* ${start}：启动应用程序的时间与日期，采用类似于 2013-08-22 10:10:18 -0400 的格式。

### 访问绑定服务的信息
{: #accessing_info_of_bound_services}

要将服务绑定到应用程序时，有关该服务的信息（例如，连接凭证）会包含在 Cloud Foundry 为应用程序设置的 [VCAP_SERVICES 环境变量](http://docs.run.pivotal.io/devguide/deploy-apps/environment-variable.html#VCAP-SERVICES)中。对于[自动配置的服务](autoConfig.html)，Liberty buildpack 会在 server.xml 文件中生成或更新服务绑定条目。服务绑定条目的内容可以使用下列其中一种格式：

* cloud.services.&lt;service-name&gt;.&lt;property&gt;，描述诸如服务的名称、类型和计划之类的信息。
* cloud.services.&lt;service-name&gt;.connection.&lt;property&gt;，描述服务的连接信息。

典型的信息集如下所示：
* name：服务名称。例如，mysql-e3abd。
* label：所创建服务的类型。例如，mysql-5.5。
* plan：服务计划，如该计划的唯一标识所示。例如，100。
* connection.name：连接的唯一标识，采用 UUID 格式。例如，d01af3a5fabeb4d45bb321fe114d652ee。
* connection.hostname：正在运行服务的服务器的主机名。例如，mysql-server.mydomain.com。
* connection.host：正在运行服务的服务器的 IP 地址。例如，9.37.193.2。
* connection.port：服务正在侦听入局连接的端口。例如，3306,3307。
* connection.user：用于向服务认证此应用程序的用户名。用户名由 Cloud Foundry 自动生成。例如：unHwANpjAG5wT。
* connection.username：connection.user 的别名。
* connection.password：用于向服务认证此应用程序的密码。密码由 Cloud Foundry 自动生成。例如：pvyCY0YzX9pu5。

对于 Liberty buildpack 未自动配置的绑定服务，应用程序需要自己管理后端资源的访问。

# 相关链接
## 常规
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
