---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Bluemix에서 지원되는 Liberty 기능
{: #liberty_features}

Liberty for Java 인스턴트 런타임에는 Liberty 프로파일 기능 서브세트가 포함됩니다. Liberty 프로파일에서 제공하는 일부 기능은 클라우드 환경에서 적용할 수 없기 때문에 Liberty for Java 인스턴트 런타임에서 사용할 수 없습니다. 

Bluemix에 특정한 다음 기능이 포함됩니다. 
* appState-1.0
* cloudAutowiring-1.0
* logAnalysis-1.0

다음 표는 Bluemix에서 지원되는 Liberty 기능을 표시합니다. 

<table>

<tr>
<th align="left">기능</th>
<th align="left">기능</th>
<th align="left">기능</th>
<th align="left">기능</th>
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
<td>beanValidation-1.0</td>
<td>beanValidation-1.1</td>
</tr>

<tr>
<td>bells-1.0</td>
<td>blueprint-1.0 </td>
<td>cdi-1.0</td>
<td>cdi-1.2</td>
</tr>

<tr>
<td>cloudAutowiring-1.0</td>
<td>cloudant-1.0</td>
<td>concurrent-1.0</td>
<td>couchdb-1.0</td>
</tr>

<tr>
<td>distributedMap-1.0</td>
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
<td>jaxws-2.2</td>
</tr>

<tr>
<td>jca-1.6</td>
<td>jca-1.7</td>
<td>jcaInboundSecurity-1.0</td>
<td>jdbc-4.0</td>
</tr>

<tr>
<td>jdbc-4.1</td>
<td>jms-1.1</td>
<td>jms-2.0</td>
<td>jmsMdb-3.1</td>
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
<td>json-1.0</td>
<td>jsonp-1.0</td>
</tr>

<tr>
<td>jsp-2.2</td>
<td>jsp-2.3</td>
<td>ldapRegistry-3.0</td>
<td>localConnector-1.0</td>
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
<td>mongodb-2.0</td>
<td>monitor-1.0</td>
</tr>

<tr>
<td>oauth-2.0</td>
<td>openid-2.0</td>
<td>openidConnectClient-1.0</td>
<td>openidConnectServer-1.0</td>
</tr>

<tr>
<td>osgiAppIntegration-1.0</td>
<td>osgiConsole-1.0</td>
<td>osgi.jpa-1.0</td>
<td>passwordUtilities-1.0</td>
</tr>

<tr>
<td>restConnector-1.0</td>
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
<td>sessionDatabase-1.0</td>
<td>sipServlet-1.1</td>
<td>spnego-1.0</td>
<td>ssl-1.0</td>
</tr>

<tr>
<td>timedOperations-1.0</td>
<td>wab-1.0</td>
<td>wasJmsClient-1.1</td>
<td>wasJmsClient-2.0</td>
</tr>

<tr>
<td>wasJmsSecurity-1.0</td>
<td>wasJmsServer-1.0</td>
<td>webCache-1.0</td>
<td>webProfile-6.0</td>
</tr>

<tr>
<td>webProfile-7.0</td>
<td>websocket-1.0</td>
<td>websocket-1.1</td>
<td>wmqJmsClient-1.1</td>
</tr>

<tr>
<td>wmqJmsClient-2.0</td>
<td>wsSecurity-1.1</td>
<td>wsSecuritySaml-1.1</td>
<td></td>
</tr>
</table>

WAR 또는 EAR 파일을 배치하면 사용 가능한 기능 서브세트가 기본적으로 사용됩니다. 세부사항은 [독립형 앱](optionsForPushing.html#stand_alone_apps)을 참조하십시오. 

Liberty for Java 런타임에서는 일부 Liberty 베타 기능도 사용 가능합니다. 이러한 기능은 표에는 나열되어 있지 않지만 [베타 기능 사용](/docs/runtimes/liberty/usingBetaFeatures.html)에서 찾을 수 있습니다.

서버는 호환 불가능한 기능은 로드할 수 없으므로 호환 가능한 기능만 사용하도록 구성해야 합니다. 
    <a href="http://www-01.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos.html">지원되는 Java EE 6 및 7 기능 조합</a>을 참조하십시오.

Java EE 버전 및 기타 정보와 함께 Liberty에서 사용 가능한 전체 기능 목록을 보려면 IBM Knowledge Center에서
[Liberty 기능](https://www.ibm.com/support/knowledgecenter/SSCKBL_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html)을
참조하십시오. 

원격 EJB를 사용하는 애플리케이션은 Bluemix에 배치될 수 있습니다.
그러나 원격 EJB는 Bluemix 환경의 포트 제한사항 때문에
CORBA/IIOP 프로토콜을 사용하여 원격 액세스할 수 없습니다. 

# 관련 링크
{: #rellinks}
## 일반
{: #general}
* [Liberty 런타임](index.html)
* [Liberty 프로파일 개요](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
