---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Bluemix 中支援的 Liberty 特性
{: #liberty_features}

Liberty for Java 即時運行環境包括「Liberty 設定檔」功能的子集。「Liberty 設定檔」提供的部分功能無法在 Liberty for Java 即時運行環境中使用，因為它們不適用於雲端環境。

下列是 Bluemix 特有的功能：
* appState-1.0
* cloudAutowiring-1.0 
* logAnalysis-1.0

下表顯示 Bluemix 中支援的 Liberty 特性

<table>

<tr>
<th align="left">特性</th>
<th align="left">特性</th>
<th align="left">特性</th>
<th align="left">特性</th>
</tr>

<tr>
<td>apiDiscovery-1.0</td>
<td>appSecurity-1.0</td>
<td>appSecurity-2.0</td>
<td>appState-1.0</td>
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
<td>mdb-3.1</td>
</tr>

<tr>
<td>mdb-3.2 </td>
<td>mediaServerControl-1.0</td>
<td>mongodb-2.0 </td>
<td>monitor-1.0 </td>
</tr>

<tr>
<td>oauth-2.0 </td>
<td>openid-2.0 </td>
<td>openidConnectClient-1.0 </td>
<td>openidConnectServer-1.0 </td>
</tr>

<tr>
<td>osgiAppIntegration-1.0</td>
<td>osgiConsole-1.0 </td>
<td>osgi.jpa-1.0 </td>
<td>passwordUtilities-1.0</td>
</tr>

<tr>
<td>restConnector-1.0 </td>
<td>requestTiming-1.0</td>
<td>rtcomm-1.0</td>
<td>rtcommGateway-1.0</td>
</tr>

<tr>
<td>samlWeb-2.0</td>
<td>scim-1.0</td>
<td>servlet-3.0</td>
<td>servlet-3.1</td>
</tr>

<tr>
<td>sessionDatabase-1.0 </td>
<td>sipServlet-1.1</td>
<td>spnego-1.0</td>
<td>ssl-1.0 </td>
</tr>

<tr>
<td>timedOperations-1.0 </td>
<td>wab-1.0 </td>
<td>wasJmsClient-1.1 </td>
<td>wasJmsClient-2.0</td>
</tr>

<tr>
<td>wasJmsSecurity-1.0 </td>
<td>wasJmsServer-1.0 </td>
<td>webCache-1.0 </td>
<td>webProfile-6.0 </td>
</tr>

<tr>
<td>webProfile-7.0</td>
<td>websocket-1.0</td>
<td>websocket-1.1</td>
<td>wmqJmsClient-1.1 </td>
</tr>

<tr>
<td>wmqJmsClient-2.0</td>
<td>wsSecurity-1.1</td>
<td>wsSecuritySaml-1.1</td>
<td></td>
</tr>
</table>

當部署 WAR 或 EAR 檔案時，依預設會啟用可用功能的子集。如需詳細資料，請參閱[獨立式應用程式](optionsForPushing.html#stand_alone_apps)。

Liberty for Java 運行環境也會讓部分 Liberty 測試版功能可供使用。那些功能未列示在表格中，但可在[使用測試版功能](/docs/runtimes/liberty/usingBetaFeatures.html)中找到。

請記住，伺服器無法載入不相容的功能，因此務必將它配置為僅啟用相容的功能。請參閱
    <a href="http://www-01.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos.html">支援的 Java EE 6 及 7 功能組合</a>。
若要查看 Liberty 中可用功能的完整清單，以及 Java EE 版本及其他資訊，請參閱 IBM Knowledge Center 中的 [Liberty 功能](https://www.ibm.com/support/knowledgecenter/SSCKBL_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html)。

使用遠端 EJB 的應用程式可以部署至 Bluemix，不過，由於 Bluemix 環境中的埠限制，無法使用 CORBA/IIOP 通訊協定來遠端存取這些遠端 EJB。

# 相關鏈結
{: #rellinks}
## 一般
{: #general}
* [Liberty 運行環境](index.html)
* [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
