---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用 New Relic
{: #new_relic}

*上次更新时间：2016 年 3 月 23 日*

New Relic 是第三方服务，其提供应用程序的监视度量值。有关 New Relic 服务提供哪些内容的更多信息，请参阅 [New Relic](http://newrelic.com/java)。

根据此 [Java 代理程序手动安装文档](https://docs.newrelic.com/docs/agents/java-agent/installation/java-agent-manual-installation)，要使用 New Relic 服务监视的 Java 应用程序通常需要使用 New Relic 代理程序和帐户许可证密钥进行绑定并配置。在 IBM Bluemix 环境中，可以通过在 IBM Bluemix 中创建服务实例来获取 New Relic 许可协议和帐户。然后，可以将 Java 应用程序绑定到 New Relic 服务实例；对于已准备好受 New Relic 服务监视的应用程序，Liberty buildpack 会自动进行配置。具体而言，该 buildpack 会：

* 为应用程序提供 New Relic 代理程序。
* 从 VCAP_APPLICATION 和 VCAP_SERVICES 应用程序环境变量获取应用程序名称和许可证密钥。
* 配置 New Relic 代理程序所需的属性和配置模板。

请参阅 Liberty buildpack 为应用程序生成的样本配置：

```
    -javaagent:/home/vcap/app/.new_relic_agent/new_relic_agent-3.12.0.jar
    -Dnewrelic.home=/home/vcap/app/.new_relic_agent
    -Dnewrelic.config.license_key=123456
    -Dnewrelic.config.app_name=myapp
    -Dnewrelic.config.log_file_path=../../../../../logs
```
{: #codeblock}

## 添加 New Relic 服务
{: #add_new_relic}

对于 IBM Bluemix 中要使用 New Relic 监视的现有 Java 应用程序，请执行以下步骤。
1. 在 IBM Bluemix 中创建 New Relic 服务实例。```
    $ cf create-service newrelic standard mynewrelic```
{: #codeblock}

2. 使用 New Relic 服务将应用程序部署到 IBM Bluemix。请参阅以下样本应用程序清单：```
        ---
        applications:
        - name: myapp
         memory: 1G
         instances: 1
         host: myapp
         domain: mybluemix.net
         path: myapp.war
         services:
          - mynewrelic```
{: #codeblock}

3. 直接从应用程序的 IBM Bluemix 仪表板访问应用程序的 New Relic 仪表板。

### 添加用户提供的 New Relic 服务
{: #add_user_provided_new_relic}

如果现有 New Relic 帐户和许可证密钥，那么可以使用“用户提供的服务”将现有 New Relic 服务绑定到应用程序。

1. 使用现有许可证密钥来创建用户提供的服务实例。例如，如果现有许可证密钥为 1234567，那么可以使用 CF CLI 来执行“create-user-provided-service”命令，并在提示时提供许可证密钥 1234567，如下所示：```
    $ cf create-user-provided-service mynewrelic -p "licenseKey"
    licenseKey> 1234567
```
{: #codeblock}

2. 使用用户提供的 New Relic 服务实例将应用程序部署到 IBM Bluemix。下面是使用用户提供的 New Relic 服务实例的样本应用程序清单：```
        ---
        applications:
        - name: myapp
         memory: 1G
         instances: 1
         host: myapp
         domain: mybluemix.net
         path: myapp.war
         services:
          - mynewrelic```
{: #codeblock}

3. 访问 New Relic 仪表板来查看应用程序度量值。

New Relic 服务的自动配置与其他服务的自动配置不同，因为该服务是容器管理服务，是通过 buildpack 的框架提供的。由于此服务是通过框架提供的，因此其自动配置与其他服务的自动配置不同，不同之处有以下三个方面：
* 选择退出不是一个选项。
* 服务集成依赖于 New Relic 代理程序，而它是一种 Java 代理程序。因此，这种代理程序是通过 Java 选项进行配置的，与 server.xml 文件中的云变量完全不同。
* 配置依赖于 VCAP_SERVICES 和 VCAP_APPLICATION。

# 相关链接
## 常规
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
