---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Configuring external log hosts
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} keeps a limited amount of log information in memory. When information is logged, the old information is replaced by the newer information. To keep all the log information, you can save your Cloud Foundry application logs to an external log host, such as a third-party log management service or other host.
{:shortdesc}

To stream logs from your CF app and the system to an external log host, complete the following steps:

  1. Determine the logging endpoint.

	 You can send logs to a third-party log aggregator, such as Papertrail, Splunk, or Sumologic. You can also send logs to a syslog host, a syslog host that is encrypted with TLS (Transport Layer Security), or an HTTPS POST endpoint. The methods to obtain logging endpoints vary for different log hosts.

  2. Create a user-provided service instance.

	 Use the `cf create-user-provided-service` command (or `cups`, a short version of the command) to create a user-provided service instance:
	 ```
	 cf create-user-provided-service <service_name> -l <logging_endpoint>
	 ```
	 &lt;service_name&gt;

	 The name for the user-provided service instance.

	 &lt;logging_endpoint&gt;

	 The logging endpoint that {{site.data.keyword.Bluemix_notm}} sends logs to. Refer to the following table to replace *logging_endpoint* with your value:

	 <table>
	 <caption>Table 1. Logging endpoint values</caption>
     <thead>
     <tr>
     <th>Logging endpoint</th>
     <th>Command</th>
	 <th>Notes</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>syslog host</td>
     <td>`cf cups my-logs -l syslog://HOST:PORT`</td>
	 <td>For example, to enable logging to Papertrail, type `cf cups my-logs -l syslog://<papertrail-url>`. Replace `<papertrail-url>` with the URL of your logging endpoint from Papertrail.</td>
     </tr>
	 <tr>
     <td>syslog-tls host</td>
     <td>`cf cups my-logs -l syslog-tls://HOST:PORT`</td>
	 <td>The certificate must be trusted by a certificate authority. Don't use self-signed certificates.</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOST:PORT`</td>
	 <td>This endpoint must be on the public Internet and accessible by {{site.data.keyword.Bluemix_notm}}</td>
     </tr>
     </tbody>
     </table>
  3. Bind the service instance to your app.

	 Use the following command to bind the service instance to your app:

	 ```
	 cf bind-service <appname> <service_name>
	 ```
	 &lt;appname&gt;

	 The name of your app.

	 &lt;service_name&gt;

	 The name for the user-provided service instance.

  4. Restage the app.
     Type `cf restage appname` for the changes to take effect.

