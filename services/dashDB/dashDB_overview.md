---

copyright:
  years: 2014, 2017
lastupdated: "2017-05-16"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#About dashDB
{: #dashDB_overview}

There are two different database solutions provided by {{site.data.keyword.IBM}} {{site.data.keyword.dashdbshort}}: a data warehousing and analytics solution ({{site.data.keyword.dashdbshort_notm}} for Analytics plans), and an online transaction processing solution ({{site.data.keyword.dashdbshort_notm}} for Transactions plans).
{: shortdesc}

##dashDB managed service
{: #managed_service}

The fully managed service of {{site.data.keyword.dashdbshort_notm}} handles all of the software upgrades, operating system updates, and hardware maintenance. The service includes 24x7 health monitoring of the database and infrastructure. In the event of a hardware or software failure, the service is automatically restarted.
{: shortdesc}

For more information about the managed service aspects of {{site.data.keyword.dashdbshort_notm}}, see: [{{site.data.keyword.dashdbshort_notm}} managed service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/managed_service.html).

##Plans and configurations
{: #plans_cfgs}

You can choose a {{site.data.keyword.dashdbshort_notm}} plan that is configured and optimized for the work that you need to do:
{: shortdesc}

   * An entry plan to try things out
   * Small, medium, and large plans for production
   * MPP configurations for parallel processing
   * Plans configured for High Availability or for Oracle compatibility
   * And more ...

View available plans in the {{site.data.keyword.Bluemix}} catalog:
   * Plans configured for data warehouse and analytic (OLAP) workloads: [{{site.data.keyword.dashdbshort_notm}} for Analytics](https://console.ng.bluemix.net/catalog/services/dashdb-for-analytics){:new_window}
   * Plans configured for high-speed, transactional processing (OLTP): [{{site.data.keyword.dashdbshort_notm}} for Transactions](https://console.ng.bluemix.net/catalog/services/dashdb-for-transactions-sql-database){:new_window}

If you don't see a configuration in the catalog that you need, [contact {{site.data.keyword.IBM_notm}} sales ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/connect/ibm/us/en/?lnk=fcw){:new_window} to discuss other options.

##dashDB for Analytics
{: #dashDB_an}

In the {{site.data.keyword.dashdbshort_notm}} for Analytics data warehouse plans, use the {{site.data.keyword.dashdbshort_notm}} data warehouse to store relational data, including special types such as geospatial data. Analyze your own data, or data loaded from other cloud services, by using our built-in analytics or by connecting your own apps. You can leverage the high-performance, in-memory database technology with columnar tables for analytic workloads. The {{site.data.keyword.dashdbshort_notm}} web console handles common data management tasks, such as loading data, and analytics tasks like running queries and R scripts.
{: shortdesc}

You can also connect external applications and tools to {{site.data.keyword.dashdbshort_notm}} and use them to further manage or analyze your data. For example:
   * Connect {{site.data.keyword.IBM_notm}} InfoSphere® Data Architect to design and deploy your database schema.
   * Connect Esri ArcGIS to perform geospatial analytics and map publishing with your data.
   * Connect an {{site.data.keyword.IBM_notm}} Cognos® server to run Cognos reports against your data.
   * Connect SQL-based tools such as Tableau, Microstrategy, or Microsoft Excel to manipulate or analyze your data.
   * Connect your {{site.data.keyword.Bluemix_short}} applications that need an analytics database.
   * Connect Aginity Workbench to migrate Netezza® data models and data to {{site.data.keyword.dashdbshort_notm}}.

##Provisioning of dashDB for Analytics
{: #whse_provision}

The {{site.data.keyword.IBM_notm}} {{site.data.keyword.dashdbshort_notm}} for Analytics data warehouse can be provisioned on {{site.data.keyword.BluSoftlayer_full}} and for AWS.
{: shortdesc}

If you want to have the {{site.data.keyword.dashdbshort_notm}} for Analytics data warehouse provisioned for AWS, select the **{{site.data.keyword.IBM_notm}} {{site.data.keyword.dashdbshort_notm}} for Analytics MPP Small for AWS** plan.

##dashDB for Transactions
{: #dashDB_tr}

In the {{site.data.keyword.dashdbshort_notm}} for Transactions plans, use the {{site.data.keyword.dashdbshort_notm}} relational database for online transaction processing. You can connect new or existing applications, and you can begin processing transactions and storing your data. With DB2® and Oracle compatibility, you can connect small or large applications and benefit from a managed enterprise-class database system. You can leverage the {{site.data.keyword.dashdbshort_notm}} for Transactions web console to manage users, load data, and get connection information.
{: shortdesc}

<!-- ##dashDB web console overview
{: #console_overview}

You can manage your {{site.data.keyword.dashdbshort_notm}} database, analyze your data, and monitor sensitive data with the {{site.data.keyword.dashdbshort_notm}} web console accessible from {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Open the web console by clicking the service tile on your application overview page, and then click **Open**.

Single sign-on authentication connects you directly to the web console. You can access connection information from the web console, and the **Downloads** page includes links to client drivers for accessing {{site.data.keyword.dashdbshort_notm}} from remote applications. You can also access sample data and reports.

###Sensitive data reporting

The {{site.data.keyword.dashdbshort_notm}} web console includes a sensitive data reporting feature that detects and monitors sensitive objects in the {{site.data.keyword.dashdbshort_notm}} data warehouse, such as credit card numbers and US Social Security numbers.

To run and view reports that identify columns that contain sensitive data and provide information about connections and activities that access the sensitive data, select **Monitor &gt; Sensitive Data** in the web console. -->


<!-- ##IBM Analytics Services
{: #analytics_services}

For more information about {{site.data.keyword.IBM_notm}} analytics services and finding your local services representative, see: [{{site.data.keyword.IBM_notm}} Analytics Services ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/software/data/services/).
{: shortdesc} -->









