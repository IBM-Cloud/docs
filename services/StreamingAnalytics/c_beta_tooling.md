---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Development tools and environment
{: #c_beta_tooling}


These considerations apply to the tools and environment that you use to develop your applications for {{site.data.keyword.streaminganalyticsshort}}.
{:shortdesc}


* {{site.data.keyword.streaminganalyticsshort}} doesn't include an {{site.data.keyword.streamsshort}} development environment in the cloud or Streams Studio in the cloud. Develop your applications in a locally installed {{site.data.keyword.streamsshort}} environment and submit them as application bundles. If you don’t have the development environment, you can download the {{site.data.keyword.streamsshort}} Quick Start Edition, free-of-charge on the [{{site.data.keyword.streamsshort}} product page](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products).
* Compile the application bundle in a Red Hat Enterprise Linux 6.5 environment, or an equivalent CentOS version, to ensure compatibility.
* In your {{site.data.keyword.streamsshort}} development environment, set the environment variable `JAVA_HOME` to $STREAMS_INSTALL/java.
