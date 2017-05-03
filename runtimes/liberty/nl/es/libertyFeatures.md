---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-07"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Características de Liberty que reciben soporte en Bluemix
{: #liberty_features}

El tiempo de ejecución instantáneo de Liberty for Java incluye un subconjunto de características de Liberty Profile.  Algunas características que proporciona Liberty Profile no están disponibles en el tiempo de ejecución instantáneo de Liberty for Java porque no son aplicables en el entorno de nube.

Se incluyen las siguientes características que son específicas para Bluemix:
* appstate-2.0
* cloudAutowiring-1.0
* logAnalysis-1.0

La tabla siguiente muestra las funciones de Liberty soportadas en Bluemix

<table>

<tr>
<th align="left">Característica</th>
<th align="left">Característica</th>
<th align="left">Característica</th>
<th align="left">Característica</th>
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
<td>microProfile-1.0</td>
</tr>

<tr>
<td>mdb-3.1</td>
<td>mdb-3.2</td>
<td>mediaServerControl-1.0</td>
<td>mongodb-2.0</td>
</tr>

<tr>
<td>monitor-1.0</td>
<td>oauth-2.0</td>
<td>openid-2.0</td>
<td>openidConnectClient-1.0</td>
</tr>

<tr>
<td>openidConnectServer-1.0</td>
<td>osgiAppIntegration-1.0</td>
<td>osgiConsole-1.0</td>
<td>osgi.jpa-1.0</td>
</tr>

<tr>
<td>passwordUtilities-1.0</td>
<td>restConnector-1.0</td>
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
<td>sessionDatabase-1.0</td>
<td>sipServlet-1.1</td>
<td>spnego-1.0</td>
</tr>

<tr>
<td>ssl-1.0</td>
<td>timedOperations-1.0</td>
<td>wab-1.0</td>
<td>wasJmsClient-1.1</td>
</tr>

<tr>
<td>wasJmsClient-2.0</td>
<td>wasJmsSecurity-1.0</td>
<td>wasJmsServer-1.0</td>
<td>webCache-1.0</td>
</tr>

<tr>
<td>webProfile-6.0</td>
<td>webProfile-7.0</td>
<td>websocket-1.0</td>
<td>websocket-1.1</td>
</tr>

<tr>
<td>wmqJmsClient-1.1</td>
<td>wmqJmsClient-2.0</td>
<td>wsSecurity-1.1</td>
<td>wsSecuritySaml-1.1</td>
</tr>
</table>

Un subconjunto de características disponibles está habilitado de forma predeterminada al desplegar archivos WAR o EAR.  Consulte [Apps autónomas](optionsForPushing.html#stand_alone_apps) para obtener más detalles.

El tiempo de ejecución de Liberty for Java también hace que algunas características beta de Liberty estén disponibles. Estas características no se listan en la tabla pero pueden encontrase en [Utilización de las características beta](/docs/runtimes/liberty/usingBetaFeatures.html).

Tenga en cuenta que un servidor no puede cargar características incompatibles, por lo que debe asegurarse de que se configura para habilitar únicamente características que son compatibles. Consulte
    <a href="http://www-01.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos.html">Combinaciones de características de Java EE 6 y 7 soportadas</a>.

Para ver una lista completa de las características disponibles en Liberty junto con las versiones de Java EE y otra información, consulte
[Características de Liberty](https://www.ibm.com/support/knowledgecenter/SSCKBL_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html) en IBM Knowledge Center.

Las aplicaciones que utilizan los EJB remotos se pueden desplegar en Bluemix;
no obstante, los EJB remotos no están accesibles con el protocolo CORBA/IIOP
debido a restricciones de puerto en el entorno de Bluemix.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
