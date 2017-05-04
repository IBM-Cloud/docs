---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-07"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Bluemix 中支持的 Liberty 功能
{: #liberty_features}

Liberty for Java 即时运行时包含 Liberty 概要文件功能的子集。Liberty 概要文件提供的某些功能在 Liberty for Java 即时运行时中不可用，因为这些功能在云环境中不适用。

其中包含特定于 Bluemix 的以下功能：
* appstate-2.0
* cloudAutowiring-1.0 
* logAnalysis-1.0

下表显示了 Bluemix 中支持的 Liberty 功能

<table>

<tr>
<th align="left">功能</th>
<th align="left">功能</th>
<th align="left">功能</th>
<th align="left">功能</th>
</tr>

<tr>
<td>apiDiscovery-1.0</td>
<td>appSecurity-1.0</td>
<td>appSecurity-2.0</td>
<td>appstate-2.0</td>
</tr>

<tr>
<td>batch-1.0</td>
<td>batchManagement-1.0</td>
<td>beanValidation-1.0 </td>
<td>beanValidation-1.1</td>
</tr>

<tr>
<td>bells-1.0</td>
<td>blueprint-1.0</td>
<td>cdi-1.0</td>
<td>cdi-1.2</td>
</tr>

<tr>
<td>cloudAutowiring-1.0 </td>
<td>cloudant-1.0</td>
<td>concurrent-1.0</td>
<td>couchdb-1.0</td>
</tr>

<tr>
<td>distributedMap-1.0 </td>
<td>ejb-3.2*</td>
<td>ejbHome-3.2</td>
<td>ejbLite-3.1</td>
</tr>

<tr>
<td>ejbLite-3.2</td>
<td>ejbPersistentTimer-3.2</td>
<td>ejbRemote-3.2*</td>
<td>el-3.0</td>
</tr>

<tr>
<td>eventLogging-1.0</td>
<td>federatedRegistry-1.0</td>
<td>j2eeManagement-1.1</td>
<td>jacc-1.5</td>
</tr>

<tr>
<td>jaspic-1.1</td>
<td>javaee-7.0</td>
<td>javaMail-1.5</td>
<td>jaxb-2.2</td>
</tr>

<tr>
<td>jaxrs-1.1</td>
<td>jaxrs-2.0</td>
<td>jaxrsClient-2.0</td>
<td>jaxws-2.2 </td>
</tr>

<tr>
<td>jca-1.6 </td>
<td>jca-1.7</td>
<td>jcaInboundSecurity-1.0</td>
<td>jdbc-4.0</td>
</tr>

<tr>
<td>jdbc-4.1</td>
<td>jms-1.1</td>
<td>jms-2.0</td>
<td>jmsMdb-3.1 </td>
</tr>

<tr>
<td>jmsMdb-3.2</td>
<td>jndi-1.0</td>
<td>jpa-2.0</td>
<td>jpa-2.1</td>
</tr>

<tr>
<td>jsf-2.0</td>
<td>jsf-2.2</td>
<td>json-1.0 </td>
<td>jsonp-1.0</td>
</tr>

<tr>
<td>jsp-2.2</td>
<td>jsp-2.3</td>
<td>ldapRegistry-3.0 </td>
<td>localConnector-1.0 </td>
</tr>

<tr>
<td>logAnalysis-1.0</td>
<td>logstashCollector-1.0</td>
<td>managedBeans-1.0</td>
<td>microProfile-1.0</td>
</tr>

<tr>
<td>mdb-3.1</td>
<td>mdb-3.2 </td>
<td>mediaServerControl-1.0</td>
<td>mongodb-2.0 </td>
</tr>

<tr>
<td>monitor-1.0 </td>
<td>oauth-2.0 </td>
<td>openid-2.0 </td>
<td>openidConnectClient-1.0 </td>
</tr>

<tr>
<td>openidConnectServer-1.0 </td>
<td>osgiAppIntegration-1.0</td>
<td>osgiConsole-1.0 </td>
<td>osgi.jpa-1.0 </td>
</tr>

<tr>
<td>passwordUtilities-1.0</td>
<td>restConnector-1.0 </td>
<td>requestTiming-1.0</td>
<td>rtcomm-1.0</td>
</tr>

<tr>
<td>rtcommGateway-1.0</td>
<td>samlWeb-2.0</td>
<td>scim-1.0</td>
<td>servlet-3.0</td>
</tr>

<tr>
<td>servlet-3.1</td>
<td>sessionDatabase-1.0 </td>
<td>sipServlet-1.1</td>
<td>spnego-1.0</td>
</tr>

<tr>
<td>ssl-1.0 </td>
<td>timedOperations-1.0 </td>
<td>wab-1.0 </td>
<td>wasJmsClient-1.1 </td>
</tr>

<tr>
<td>wasJmsClient-2.0</td>
<td>wasJmsSecurity-1.0 </td>
<td>wasJmsServer-1.0 </td>
<td>webCache-1.0 </td>
</tr>

<tr>
<td>webProfile-6.0 </td>
<td>webProfile-7.0</td>
<td>websocket-1.0</td>
<td>websocket-1.1</td>
</tr>

<tr>
<td>wmqJmsClient-1.1 </td>
<td>wmqJmsClient-2.0</td>
<td>wsSecurity-1.1</td>
<td>wsSecuritySaml-1.1</td>
</tr>
</table>

缺省情况下，部署 WAR 或 EAR 文件时，将启用可用的功能子集。请参阅[独立应用程序](optionsForPushing.html#stand_alone_apps)，以获取详细信息。

Liberty for Java 运行时还提供了某些 Liberty Beta 功能。这些功能未在表中列出，但可在[使用 Beta 功能](/docs/runtimes/liberty/usingBetaFeatures.html)中找到。

请记住，服务器无法装入不兼容的功能，因此请确保将其配置为仅启用兼容的功能。请参阅
    <a href="http://www-01.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos.html">Supported Java EE 6 and 7 feature combinations</a>。

要查看 Liberty 中可用的完整功能列表以及 Java EE 版本和其他信息，请参阅
IBM Knowledge Center 中的 [Liberty Features](https://www.ibm.com/support/knowledgecenter/SSCKBL_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html)。

可以将使用远程 EJB 的应用程序部署到 Bluemix；但是，由于 Bluemix 环境中的端口限制，因此不能通过 CORBA/IIOP 协议来远程访问远程 EJB。

# 相关链接
{: #rellinks notoc}
## 常规
{: #general notoc}
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
