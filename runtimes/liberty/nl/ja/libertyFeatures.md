---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Bluemix でサポートされる Liberty フィーチャー
{: #liberty_features}

Liberty for Java インスタント・ランタイムには、Liberty プロファイル・フィーチャーのサブセットが含まれています。Liberty プロファイルが提供するフィーチャーの中には、クラウド環境で適用されないために Liberty for Java インスタント・ランタイムでは使用できないものがあります。

Bluemix に固有の以下のフィーチャーが含まれています。
* appState-1.0
* cloudAutowiring-1.0 
* logAnalysis-1.0

下表に、Bluemix でサポートされる Liberty フィーチャーを示します。

<table>

<tr>
<th align="left">フィーチャー</th>
<th align="left">フィーチャー</th>
<th align="left">フィーチャー</th>
<th align="left">フィーチャー</th>
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

使用可能なフィーチャーのサブセットは、WAR ファイルまたは EAR ファイルのデプロイ時にデフォルトで有効にされます。詳細については、[『スタンドアロン・アプリケーション』](optionsForPushing.html#stand_alone_apps)を参照してください。

Liberty for Java ランタイムは、一部の Liberty ベータ・フィーチャーも使用可能にします。これらのフィーチャーは表にはリストされていませんが、[『ベータ・フィーチャーの使用』](/docs/runtimes/liberty/usingBetaFeatures.html)に記載されています。

サーバーは互換性のないフィーチャーをロードできないことに注意してください。そのため、互換性のあるフィーチャーのみを有効にするようにサーバーを構成してください。
    <a href="http://www-01.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos.html">『Supported Java EE 6 and 7 feature combinations』</a>を参照してください。

Liberty で使用可能なフィーチャー、Java EE バージョン、およびその他の情報の完全なリストを確認するには、IBM Knowledge Center の[『Liberty フィーチャー』](https://www.ibm.com/support/knowledgecenter/SSCKBL_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html)を参照してください。

リモート EJB を使用するアプリケーションを Bluemix にデプロイできますが、Bluemix 環境でのポートに関する制限のため、リモート EJB に CORBA/IIOP プロトコルでリモートにアクセスすることはできません。

# 関連リンク
{: #rellinks}
## 一般
{: #general}
* [Liberty ランタイム](index.html)
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
