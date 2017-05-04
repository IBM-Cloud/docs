---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-07"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Recursos do Liberty suportados no Bluemix
{: #liberty_features}

O tempo de execução instantâneo do Liberty for Java inclui um subconjunto dos
recursos do perfil Liberty.  Alguns recursos que o perfil Liberty fornece não estão
disponíveis no tempo de execução instantâneo do Liberty for Java porque não são
aplicáveis no ambiente de nuvem.

Os recursos a seguir incluídos são específicos do Bluemix:
* appstate-2.0
* cloudAutowiring-1.0
* logAnalysis-1.0

A tabela a seguir mostra os recursos do Liberty suportados no Bluemix

<table>

<tr>
<th align="left">Recurso</th>
<th align="left">Recurso</th>
<th align="left">Recurso</th>
<th align="left">Recurso</th>
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

Um subconjunto dos recursos disponíveis é ativado por padrão ao implementar
arquivos WAR ou EAR.  Consulte
[Apps independentes](optionsForPushing.html#stand_alone_apps) para obter
detalhes.

O tempo de execução do Liberty for Java também torna alguns recursos beta do Liberty
disponíveis. Esses recursos não são listados na tabela, mas podem ser localizados em
[Usando
os recursos beta](/docs/runtimes/liberty/usingBetaFeatures.html).

Lembre-se de que um servidor não pode carregar recursos incompatíveis; por isso,
certifique-se de que ele esteja configurado para permitir somente recursos compatíveis. Consulte
    <a href="http://www-01.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_prog_model_supported_combos.html">Combinações
de recursos Java EE 6 e 7 suportados</a>.

Para ver uma lista completa dos recursos disponíveis no Liberty com as versões do
Java EE e outras informações, consulte
[Recursos
do Liberty](https://www.ibm.com/support/knowledgecenter/SSCKBL_8.5.5/com.ibm.websphere.wlp.doc/ae/rwlp_feat.html) no IBM Knowledge Center.

Os aplicativos que usam EJBs remotos podem ser implementados no Bluemix,
no entanto, os EJBs remotos não são acessíveis remotamente com o protocolo
CORBA/IIOP devido a restrições de porta no ambiente do Bluemix.

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
