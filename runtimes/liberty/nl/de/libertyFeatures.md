---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# In Bluemix unterstützte Liberty-Features
{: #liberty_features}

Die Ad-hoc-Laufzeit (Instant Runtime) von Liberty for Java umfasst eine Untergruppe von Liberty-Profilfunktionen.  Einige Features, die das Liberty-Profil anbietet, stehen in der Ad-hoc-Laufzeit (Instant Runtime) von Liberty for Java nicht zur Verfügung, weil sie nicht in der Cloudumgebung angewendet werden können.

Die folgenden Funktionen, die für Bluemix spezifisch sind, sind enthalten:
* appState-1.0
* cloudAutowiring-1.0
* logAnalysis-1.0

Die folgende Tabelle zeigt die in Bluemix unterstützten Liberty-Features.

<table>

<tr>
<th align="left">Feature</th>
<th align="left">Feature</th>
<th align="left">Feature</th>
<th align="left">Feature</th>
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
<td>beanValidation-1.1 </td>
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
<td>mdb-3.2</td>
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

Eine Untergruppe verfügbarer Funktionen wird standardmäßig aktiviert, wenn WAR- oder EAR-Dateien implementiert werden.  Details finden Sie unter dem Thema [Eigenständige Apps](optionsForPushing.html#stand_alone_apps).

Die Liberty for Java-Laufzeit stellt ferner einige Funktionen der Liberty-Betaversion zur Verfügung. Diese Funktionen werden nicht in der Tabelle aufgelistet, können jedoch unter [Beta-Features verwenden](/docs/runtimes/liberty/usingBetaFeatures.html) gefunden werden.

Bedenken Sie, dass ein Server keine inkompatiblen Funktionen laden kann. Stellen Sie daher sicher, dass er so konfiguriert ist, dass nur kompatible Funktionen aktiviert werden. Siehe auch den Abschnitt zu unterstützten Kombinationen von Funktionen von Java EE 6 und 7
    <a href="http://www-01.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos.html">Supported Java EE 6 and 7 feature combinations</a>.

Eine vollständige Liste der in Liberty verfügbaren Funktionen mit Java EE-Versionen und anderen Informationen finden Sie im Abschnitt über Liberty-Funktionen [Liberty Features](https://www.ibm.com/support/knowledgecenter/SSCKBL_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html)
im IBM Knowledge Center.

Anwendungen, die ferne EJBs verwenden, können in Bluemix bereitgestellt werden. Es kann jedoch aufgrund von Porteinschränkungen in der Bluemix-Umgebung nicht mit dem CORBA/IIOP-Protokoll auf die fernen EJBs zugegriffen werden.

# Zugehörige Links
{: #rellinks}
## Allgemein
{: #general}
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
