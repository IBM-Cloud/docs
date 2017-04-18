---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.streaminganalyticsshort}} troubleshooting
{: #ts_StreamingAnalytics}

You can find the answers to common questions about how to use {{site.data.keyword.streaminganalyticsshort}} on {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

## When I launch the service, I am prompted for credentials to log into the console
{: #log_in_console}

When you launch {{site.data.keyword.streaminganalyticsshort}}, you are prompted for credentials to log into the service console.
{:shortdesc}

You launch a {{site.data.keyword.streaminganalyticsshort}} service you had previously created and instead of directly accessing the service console, you see a login page where you are prompted for credentials.
{: tsSymptoms}

The service infrastructure has been updated and your browser cache is preventing the service from picking up the update.
{: tsCauses}

Clear your browser cache to make sure you get the latest version of the service console.
{: tsResolve}

## My application is unhealthy
{: #app_unhealthy}

You can't run your application correctly and the health status is `unhealthy`.
{:shortdesc}

You submit an application to the service instance, the application starts but fails immediately, and the health status is `unhealthy`. The following error appears in the log file: `/lib64/libc.so.6: version GLIBC_2.14 not found`.
{: tsSymptoms}

You did not compile the application using a RHEL 6.5 operating system or an equivalent CentOS version.
{: tsCauses}

You must re-compile your application in a Red Hat Enterprise Linux (RHEL) 6.5 operating system or an equivalent CentOS version, using Intel processors. Submit your application to the service instance again.
{: tsResolve}
