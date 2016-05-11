---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用 JConsole 监视 Bluemix 中的 Liberty
{: #jconsole}

*上次更新时间：2016 年 3 月 23 日*

## 使用 JConsole 监视 Bluemix 中的 Liberty 的步骤如下：
{: #steps_to_monitor}

1. 在包含相应 server.xml 的服务器软件包内推送应用程序。
2. 在命令行上使用相应系统属性来启动 JConsole 应用程序。
3. 向 JConsole 提供正确的远程进程 URL、用户名和密码。

### 推送服务器软件包
{: #push_server_package}

推送包含应用程序的服务器软件包，并将其限制为推送到单个实例。server.xml 文件必须包含 ``monitor-1.0`` 和 ``restConnector-1.0` 功能。此外，还必须包含 basicRegistry 元素和 administrator-role 元素。```xml
       <featureManager>
           <feature>jsp-2.2</feature>
           <feature>monitor-1.0</feature>
           <feature>restConnector-1.0</feature>
       </featureManager>

       <basicRegistry>
           <user name="jconuser" password="jconpassw0rd"/>
       </basicRegistry>

       <administrator-role>
           <user>jconuser</user>
       </administrator-role>
```
{: #codeblock}

   * 注：密码应该使用 Liberty 提供的 securityUtility 工具进行编码。

### 启动 JConsole 应用程序
{: #start_jconsole_app}

JConsole 包含在 Java 安装中。要启动 JConsole 应用程序，请转至 &lt;java-home&gt;/bin，并运行以下命令：
```
    $ jconsole -J-Djava.class.path=<java-home>/lib/jconsole.jar;<liberty-home>/wlp/clients/restConnector.jar```
{: #codeblock}

您可能需要传递其他参数来配置 Java trustStore。以下参数应适用于大部分情况：
```
    -J-Djavax.net.ssl.trustStore=<java-home>/jre/lib/security/cacerts -J-Djavax.net.ssl.trustStorePassword=changeit -J-Djavax.net.ssl.trustStoreType=jks
```
{: #codeblock}

### 完成连接
{: #start_jconsole_app}
  * 在“远程进程”字段中填写以下 URL：
    * service:jmx:rest://&lt;appName&gt;.mybluemix.net:443/IBMJMXConnectorREST.
  *  另外，使用 server.xml 文件中管理员角色的用户和密码填写“用户名”和“密码”字段。
  * 单击“连接”。

连接成功后，JConsole 会启动监视。

如果连接失败，可生成日志以帮助诊断问题。首先，尝试通过向 jconsole 命令添加** -J-Djava.util.logging.config.file=c:/tmp/logging.properties** 来收集客户机端跟踪。下面是样本日志记录属性文件：```
    handlers= java.util.logging.FileHandler
    .level=INFO java.util.logging.FileHandler.pattern = /tmp/jmxtrace.log
    java.util.logging.FileHandler.limit = 50000
    java.util.logging.FileHandler.count = 1
    java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
    javax.management.level=FINEST
    javax.management.remote.level=FINER
    com.ibm.level=FINEST```
{: #codeblock}

您还可以将 <b>&dash;J&dash;Djavax.net.debug=ssl</b> 添加到 jconsole 命令。这会在单独的 JConsole 输出窗口中生成 SSL 诊断跟踪。最后，可以通过将以下内容添加到 server.xml 文件，在服务器端启用跟踪：```
    <logging traceSpecification="com.ibm.ws.jmx.*=all"/>
```
{: codeblock}

# 相关链接
## 常规
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
