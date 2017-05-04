---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Liberty for Java 故障诊断
{: #ts}


以下是对在 {{site.data.keyword.Bluemix_notm}} 上使用 Liberty for Java 的常见故障诊断问题的回答。
{:shortdesc}

## 应用程序无法开始接受连接
{: #health_check_timeout}


Liberty 应用程序无法启动，发生“无法开始接受连接”错误。例如，日志中的错误可能看起来如下所示：
{: tsSymptoms}

```
   2016-11-14T14:44:58.45+0000 [API/0]      OUT App instance exited with guid 21ac63eb-9595-428a-94c7-b0b02aaf77cc payload: {"cc_partition"=>"default", "droplet"=>"21ac63eb-9595-428a-94c7-b0b02aaf77cc", "version"=>"b2772438-92de-4d47-b680-ea772ac2288a", "instance"=>"f4799c8c89214bbd8067883c3ffe23e0", "index"=>0, "reason"=>"CRASHED", "exit_status"=>255, "exit_description"=>"failed to accept connections within health check timeout", "crash_timestamp"=>1479134698} 2016-11-14T14:45:07.50+0000 [DEA/4]      ERR Instance (index 0) failed to start accepting connections
```
{: #codeblock}

Bluemix 在应用程序上执行运行状况检查，以查看其是否已成功启动。运行状况检查会测试应用程序是否在分配给应用程序的端口上进行侦听。此检查的缺省超时是 60 秒，一些应用程序可能超过 60 秒才能启动。
应用程序可能需要更长时间才能启动的原因有多种。例如，绑定服务（如 [Monitoring and Analytics](/docs/services/monana/index.html#gettingstartedtemplate) 或 [New Relic](/docs/runtimes/liberty/newRelic.html)）或者[启用调试器](/docs/manageapps/app_mng.html#debug)将增加启动时间。应用程序还可能会执行初始化步骤，这可能需要较长时间才能完成。
{: tsCauses}

首先，检查日志以查看是否存在任何明显的错误可能导致 Liberty 应用程序失败。如果找不到明显错误，请尝试以下内容：
{: tsResolve}

### **增加运行状况检查超时。**

* 当使用“cf push”命令部署应用程序时，使用“-t”选项指定较长的应用程序启动超时。例如：

        $ cf push myApp -t 180
        {: #codeblock}

* 在 manifest.yml 文件中也可以指定运行状况检查超时。例如：

        ---
           ...
           timeout: 180
        {: #codeblock}

### **禁用 appstate 功能。**

appstate 功能与 Bluemix 运行状况检查进程集成在一起，可确保 Liberty 应用程序经过完全初始化后，才能接收 HTTP 请求。一旦应用程序完全初始化后，appstate 功能即不再起作用。此功能的副作用是一些应用程序可能花费较长时间才能启动。要禁用 appstate 功能，可在应用程序上设置以下环境属性，并重新编译打包该应用程序：

```
   $ cf set-env myApp JBP_CONFIG_LIBERTY “app_state: false”
```
{: #codeblock}

### **考虑重构应用程序。**

如果您的应用程序花费较长时间进行初始化，您可能必须重构应用程序以执行延迟和/或异步初始化。

### **使用“no-route”选项进行部署。**

1. 使用“--no-route”选项部署应用程序。这将禁用端口运行状况检查。例如：

        $ cf push myApp –no-route
        {: #codeblock}

2. 初始化应用程序之后，将路径映射到应用程序。例如：

        $ cf map-route myApp mybluemix.net
        {: #codeblock}

## IBM 网关发生 SSL 错误
{: #ssl_handshake_failure}


日志中可以看到以下错误，应用程序可能无法启动：
{: tsSymptoms}

```
    2016-11-03T12:32:44.82-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error
    2016-11-03T12:32:44.83-0200 [App/0]      ERR [ERROR   ] CWPKI0022E: SSL HANDSHAKE FAILURE:  A signer with SubjectDN CN=*.gateway.prd.na.ca.ibmserviceengage.com, O=International Business Machines Corp., L=Armonk, ST=New York, C=US was sent from the target host.  The signer might need to be added to local trust store /home/vcap/app/wlp/usr/servers/defaultServer/resources/security/key.jks, located in SSL configuration alias defaultSSLConfig.  The extended error message from the SSL handshake exception is: PKIX path building failed: java.security.cert.CertPathBuilderException: PKIXCertPathBuilderImpl could not build a valid CertPath.; internal cause is:
    2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: The certificate issued by CN=DigiCert Global Root CA, OU=www.digicert.com, O=DigiCert Inc, C=US is not trusted; internal cause is:
    2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error
```
{: codeblock}

在 Monitoring & Analytics 服务绑定到 Liberty 应用程序之后，如果 Liberty 应用程序已部署为服务器目录或打包服务器，而该服务器包含配置 Liberty ssl-1.0 功能的 server.xml，那么可能会产生此错误。将 Monitoring & Analytics 服务绑定到 Liberty 应用程序导致运行时通过安全连接来连接到服务。该安全连接是使用缺省 SSL 设置建立的。由于在 Liberty 的 server.xml 中已指定缺省 SSL 设置，因此所配置的信任库可能不会信任 Monitoring & Analytics 服务所使用的证书。
{: tsCauses}

使用以下其中一个选项来修改配置以使用 JVM 的信任库。确保在进行更改之后，重新编译打包应用程序。
{: tsResolve}

### 更新 Liberty 的 server.xml

更新 server.xml 以使用 JVM 的 cacerts 文件作为信任库。将以下内容添加到 server.xml：

        <ssl id="defaultSSLConfig" trustStoreRef="defaultTrustStore"/>
        <keyStore id="defaultTrustStoretore" location="${java.home}/lib/security/cacerts"/>
        {: codeblock}

### 更新配置的信任库

修改所配置的信任库，以信任 DigitCert ROOT CA。
  1. 从 https://www.digicert.com/CACerts/DigiCertGlobalRootCA.crt 下载 DigiCert 根 CA。
  2. 假设 resources/security/key.jks 用作信任库，请使用 Java 的 keytool 实用程序将 CA 导入到密钥：

            $ keytool -importcert --storepass <keyStorePassword> -keystore &lt;path&gt;/resources/security/key.jks -file DigiCertGlobalRootCA.crt
            {: codeblock}
