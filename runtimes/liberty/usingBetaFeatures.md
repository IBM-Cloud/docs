---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Using the beta features
{: #using_beta_features}

*Last Updated: 23 May 2016*

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
<td>cloudant-1.0</td>
<td>httpWhiteboard-1.0</td>
<td>logstashCollector-1.1</td>
</tr>

<tr>
<td>osgiBundle-1.0</td>
<td>passwordUtilities-1.0</td>
<td></td>
<td></td>
<td></td>
</tr>

</table>

In order to use the Liberty beta features in Bluemix you will need to do either:

1. [Deploy a server directory or a packaged server](optionsForPushing.html) with one or more beta features enabled in the server.xml file as in the example that follows:
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>passwordUtilities-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  Set the IBM_LIBERTY_BETA environment variable to **true**. This variable directs the Liberty buildpack to install and enable the beta features for your application.  See the following examples:
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
{: #codeblock}

# rellinks
## general
* [Liberty runtime](index.html)
* [Liberty Profile Overview](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
