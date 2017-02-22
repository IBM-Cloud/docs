---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Offline mode for Liberty
{: #offline_mode}

When a Liberty application is pushed to {{site.data.keyword.Bluemix}} the Liberty buildpack can access sites external to Bluemix
to acquire artifacts required by the application.  The following are the external sites that the Liberty buildpack can access.  In [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) and
[Bluemix Local](/docs/local/index.html#local) environments these sites may need to be *whitelisted*.

* https://download.run.pivotal.io, and https://java-buildpack.cloudfoundry.org are used to access components for:
  * [AppDynamics agent](https://www.appdynamics.com/)
  * [MariaDB JDBC driver](https://mariadb.com/)
  * [New Relic agent](newRelic.html)
  * [OpenJDK](customizingJRE.html#OpenJDK)
  * [PostgreSQL JDBC driver](https://www.postgresql.org)
* https://dl.zeroturnaround.com/jrebel/ is used to access components for [JRebel](https://zeroturnaround.com/software/jrebel/).
* https://download.ruxit.com/agent/paas/cloudfoundry/java is used to access components for [Dynatrace Ruxit agent](dynatrace.html).
* http://downloads.dynatracesaas.com/cloudfoundry/buildpack/java/  is used to access the [Dynatrace agent](dynatrace.html).

## Working with a proxy
{: #working_with_proxy}

In some environments such as [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) and
[Bluemix Local](/docs/local/index.html#local) a proxy can be configured. See
[Working with a proxy](/docs/manageapps/workingWithProxy.html) for more details.

# rellinks
{: #rellinks}
## general
{: #general}
* [Liberty runtime](index.html)
* [Liberty Profile Overview](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
