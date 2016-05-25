---

copyright:
  years: 2016

---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be --- surrounded by 3 dashes ---
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

<!-- Common attributes used in the template are defined as follows: -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.iot_short}} troubleshooting
{: #ts}
*Last updated: 05 May 2016*


Here are the answers to common troubleshooting questions about using {{site.data.keyword.iot_full}} on {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problem connecting to the {{site.data.keyword.iot_short}}
{: #connection_problem}

Your connection to the {{site.data.keyword.iot_short}} drops or disconnects unexpectedly.
{:shortdesc}

When you attempt to connect to the {{site.data.keyword.iot_short}}, your device or application receives an error.
{: tsSymptoms}

You might have two devices trying to connect with the same clientID and credentials.Only one unique connection is allowed per clientID. You cannot have two concurrent connections using the same ID. Applications can share the same API key, but MQTT requires that the client ID is always unique.
{: tsCauses}

You can resolve this problem by confirming that you don't have two devices trying to connect by  using the same credentials.
{: tsResolve}

## Device intermittently disconnects from {{site.data.keyword.iot_short}}
{: #disconnection_problem}

Your device connection to the {{site.data.keyword.iot_short}} intermittently drops unexpectedly.
{:shortdesc}

A device that is connected to the {{site.data.keyword.iot_short}} service is disconnected intermittently. The device reconnects, but it is unexpectedly disconnected again after a while.
{: tsSymptoms}

It might be that when you connect, you are using a value for an MQTT ping option that is too low, which makes it look like the connection timed out. For example, if the client MQTT is set incorrectly, pings are not received in a timely manner, and the connection is closed.
{: tsCauses}

You can fix this problem by confirming that you have properly set the ping and KeepAlive parameters for your connection.   
{: tsResolve}
