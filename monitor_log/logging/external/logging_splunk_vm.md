---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Example: Streaming Cloud Foundry application logs to Splunk
{: #splunk}

In this example, a developer named Jane creates a virtual server by using IBM Virtual Servers Beta and the Ubuntu image.  Jane tries to stream Cloud Foundry app logs from {{site.data.keyword.Bluemix_notm}} to Splunk.
{:shortdesc}

  1. To begin, Jane sets up Splunk.

     a. Jane downloads Splunk Light from the [Download Splunk Light site ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window}, and then installs it by using the following command. The software is installed on */opt/splunk*.

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. Jane installs and patches the RFC5424 syslog technology add-on to integrate with {{site.data.keyword.Bluemix_notm}}. For more information about the instructions for installing the add-on, see the [Cloud Foundry guideline ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}.

	    Jane installs the add-on by using the following commands:

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        Then, Jane patches the add-on by replacing */opt/splunk/etc/apps/rfc5424/default/transforms.conf* with a new *transforms.conf* file that consists of the following text:

	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     c. After Splunk is set up, Jane must open some ports on the Ubuntu machine to accept the incoming syslog drain (port 5140) and Splunk web UI (port 8000) because {{site.data.keyword.Bluemix_notm}} virtual server has the firewall set up by default.

	    **Note:** The iptable confiration is done here for Jane's evaluation purpose and is temporary. To configure the firewall setting in Bluemix virtual server in production, see the [Network Security Groups ![External link icon](../icons/launch-glyph.svg "External link icon")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} documentation for details.

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   Then, Jane runs Splunk by using the following command:

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Jane configures the Splunk settings to accept the syslog drain from {{site.data.keyword.Bluemix_notm}}. She must create a data input for the syslog drain.

     a. From the Splunk web interface, Jane clicks **Data > Data inputs**. A list of input types that Splunk supports is displayed.

     b. She selects **TCP**, because the syslog drain uses the TCP protocol.

     c. In the **TCP** pane, she enters **5140** in the **Port** field, leaves the remaining fields blank, and then clicks **Next**.

     d. From the **Source Type** list, she selects **Uncategorized > rfc5424_syslog**.

     e. For the **Method** type, she selects **IP**.

     f. In the **Index** field, Jane clicks **Create a new index**. She names the new index "bluemix", and then clicks **Save**.

     g. Finally, in the **Review** window, Jane confirms that the setting is correct and then clicks **Submit** to enable this data input.

  3. In {{site.data.keyword.Bluemix_notm}}, Jane creates a syslog drain service and binds the service to an app.

     a. Jane creates a syslog drain service by using the following command from the cf cli:

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **Note:** *dummyhost* is not the real name. It is used to hide the actual host name.

     b. Jane binds the syslog drain service to an app in her space, and then restages the app.

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


Jane tries out her app, and then she types the following query string in the Splunk web interface:

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jane sees a stream of logs in her Splunk web interface. Though the Splunk that Jane installs is Splunk Light, she can still retain 500MB logs a day.

