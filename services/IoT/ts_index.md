---

copyright:
  years: 2016
lastupdated: "2016-08-01"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} troubleshooting
{: #ts}

Here are the answers to common troubleshooting questions about using {{site.data.keyword.iot_full}} on {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problem connecting to the {{site.data.keyword.iot_short_notm}}
{: #connection_problem}

Your connection to the {{site.data.keyword.iot_short_notm}} drops or disconnects unexpectedly.
{:shortdesc}

When you attempt to connect to the {{site.data.keyword.iot_short_notm}}, your device or application receives an error.
{: tsSymptoms}

You might have two devices trying to connect with the same clientID and credentials.Only one unique connection is allowed per clientID. You cannot have two concurrent connections using the same ID. Applications can share the same API key, but MQTT requires that the client ID is always unique.
{: tsCauses}

You can resolve this problem by confirming that you don't have two devices trying to connect by  using the same credentials.
{: tsResolve}

## Device intermittently disconnects from {{site.data.keyword.iot_short_notm}}
{: #disconnection_problem}

Your device connection to the {{site.data.keyword.iot_short_notm}} intermittently drops unexpectedly.
{:shortdesc}

A device that is connected to the {{site.data.keyword.iot_short_notm}} service is disconnected intermittently. The device reconnects, but it is unexpectedly disconnected again after a while.
{: tsSymptoms}

It might be that when you connect, you are using a value for an MQTT ping option that is too low, which makes it look like the connection timed out. For example, if the client MQTT is set incorrectly, pings are not received in a timely manner, and the connection is closed.
{: tsCauses}

You can fix this problem by confirming that you have properly set the ping and KeepAlive parameters for your connection.   
{: tsResolve}


## Getting help and support for {{site.data.keyword.iot_short_notm}}
{: #gettinghelp}

If you have problems or questions when using {{site.data.keyword.iot_short_notm}}, you can get help by searching for information or by asking questions through a forum. You can also open a support ticket.

When using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.Bluemix_notm}} development teams.

* If you have technical questions about developing or deploying an app with {{site.data.keyword.iot_short_notm}}, post your question on [Stack Overflow](http://stackoverflow.com/search?q=watson-iot+ibm-bluemix){:new_window} and tag your question with "ibm-bluemix" and "watson-iot".
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/watson-iot/?smartspace=bluemix){:new_window} forum. Include the  "watson-iot" and "bluemix" tags.

See [Getting help](https://www.{DomainName}/docs/support/index.html#getting-help) for more details about using the forums.

For information about opening an IBM support ticket, or about support levels and ticket severities, see [Contacting support](https://www.{DomainName}/docs/support/index.html#contacting-support).
