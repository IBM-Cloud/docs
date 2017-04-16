---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Funzioni Liberty supportate in Bluemix
{: #liberty_features}

Il runtime istantaneo Liberty for Java include una sottoserie di funzioni Liberty Profile.  Alcune funzioni che fornisce Liberty Profile non sono disponibili nel runtime istantaneo Liberty for Java perché non sono applicabili nell'ambiente cloud.

Le seguenti funzioni incluse sono specifiche per Bluemix:
* appState-1.0
* cloudAutowiring-1.0
* logAnalysis-1.0

La seguente tabella mostra le funzioni Liberty supportate in Bluemix

<table>

<tr>
<th align="left">Funzione</th>
<th align="left">Funzione</th>
<th align="left">Funzione</th>
<th align="left">Funzione</th>
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

Una sottoserie di funzioni disponibili vengono abilitate per impostazione predefinita quando si distribuiscono file WAR o EAR.  Consulta [Applicazioni autonome](optionsForPushing.html#stand_alone_apps) per i dettagli.

Il runtime Liberty for Java rende inoltre disponibili alcune funzioni beta di Liberty. Queste funzioni non sono elencate nella tabella ma possono essere trovate all'indirizzo [Utilizzo delle funzioni beta](/docs/runtimes/liberty/usingBetaFeatures.html).

Tieni presente che un server non può caricare funzioni non compatibili, assicurati che sia configurato per abilitare solo le funzioni che sono compatibili. Consulta
    <a href="http://www-01.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos.html">Supported Java EE 6 and 7 feature combinations</a>.

Per visualizzare un elenco completo delle funzioni disponibili in Liberty con le versioni Java EE e altre informazioni consulta
[Liberty Features](https://www.ibm.com/support/knowledgecenter/SSCKBL_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html)
nel IBM Knowledge Center.

Le applicazioni che utilizzano EJB remoti possono essere distribuite a Bluemix
tuttavia, gli EJB remoti non sono accessibili in remoto con il protocollo CORBA/IIOP
a causa di limitazioni delle porte nell'ambiente Bluemix.

# rellinks
{: #rellinks}
## general
{: #general}
* [Runtime Liberty](index.html)
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
