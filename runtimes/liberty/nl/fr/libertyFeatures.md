---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Fonctions Liberty prises en charge dans Bluemix
{: #liberty_features}

Le contexte d'exécution instantané Liberty for Java inclut un sous-ensemble de fonctions Liberty Profile.  Certaines fonctions fournies par Liberty Profile ne sont pas disponibles dans le contexte d'exécution instantané Liberty for Java, car elles ne sont pas applicables dans l'environnement de cloud.

Les fonctions incluses suivantes sont spécifiques à Bluemix :
* appState-1.0
* cloudAutowiring-1.0
* logAnalysis-1.0

Le tableau suivant présente les fonctions Liberty prises en charge dans Bluemix :

<table>

<tr>
<th align="left">Fonction</th>
<th align="left">Fonction</th>
<th align="left">Fonction</th>
<th align="left">Fonction</th>
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

Un sous-ensemble des fonctions disponibles sont activées par défaut lors du déploiement des fichiers WAR ou EAR.  Voir [Applications autonomes](optionsForPushing.html#stand_alone_apps) pour plus de détails.

Le contexte d'exécution Liberty for Java met également à disposition quelques fonctions bêta Liberty, qui ne se trouvent pas dans le tableau ci-dessus mais sont répertoriées dans la rubrique [Utilisation des fonctions bêta](/docs/runtimes/liberty/usingBetaFeatures.html).

Gardez à l'esprit qu'un serveur ne peut pas charger de fonctions incompatibles, assurez-vous donc qu'il est configuré pour n'activer que des fonctions qui sont compatibles. Voir
    <a href="http://www-01.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos.html">Combinaisons de fonctions Java EE 6 et 7 prises en charge</a>.

Pour afficher une liste complète des fonctions disponibles dans Liberty accompagnée d'informations relatives aux versions Java EE versions et d'autres détails, voir [Fonctions Liberty](https://www.ibm.com/support/knowledgecenter/SSCKBL_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html)
dans IBM Knowledge Center.

Les applications qui utilisent des EJB distants peuvent être déployées dans Bluemix. Toutefois, les EJB distants ne sont pas accessibles à distance avec le
protocole CORBA/IIOP en raison de restrictions de port dans l'environnement Bluemix.

# rellinks
{: #rellinks}
## general
{: #general}
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
