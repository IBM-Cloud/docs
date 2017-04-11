---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-07"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Using the beta features
{: #using_beta_features}

The Liberty beta features provide early access to new functionality and programming models that might be included in a future Liberty release. Most of the beta features can also be used in applications deployed to Bluemix.

**Important**: The beta features are for development and test purposes only and may not be used in production. For the complete terms of use please see the [beta license agreement](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html).

Liberty beta features available in Bluemix
<table>
<tr>
<th align="left">Feature</th>
<th align="left">Feature</th>
<th align="left">Feature</th>
<th align="left">Feature</th>
</tr>

<tr>
<td>bluemixLogCollector-1.1</td>
<td>httpWhiteboard-1.0</td>
<td>logstashCollector-1.1</td>
<td>osgiBundle-1.0</td>
</tr>
</table>

In order to use the Liberty beta features in Bluemix you will need to do following:

1. [Deploy a server directory or a packaged server](optionsForPushing.html) with one or more beta features enabled in the server.xml file as in the example that follows:
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>bluemixLogCollector-1.1</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  Set the **IBM_LIBERTY_BETA** environment variable to **true**. This variable directs the Liberty buildpack to install and enable the beta features for your application.  For example:
  * using the cf command line tool:
```
       $ cf set-env <yourappname> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * or, using the manifest.yml file:
```
      env:
          IBM_LIBERTY_BETA: "true"
```

3. Set the **JBP_CONFIG_LIBERTY** environment variable to **"version: +"**. This variable enables the [Liberty monthly runtime](buildpackDefaults.html#liberty_versions) which supports beta features. For example:
  * using the cf command line tool:
```
       $ cf set-env <yourappname> JBP_CONFIG_LIBERTY "version: +"
```
{: #codeblock}

  * or, using the manifest.yml file:
```
      env:
          JBP_CONFIG_LIBERTY: "version: +"
```

If you are enabling the beta features on an existing application, don't forget to re-stage your application after setting the environment variables.

{: #codeblock}

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Liberty runtime](index.html)
* [Liberty Profile Overview](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
