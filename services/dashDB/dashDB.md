---

copyright:
  years: 2014, 2017
lastupdated: "2017-06-16"

---

<!-- Attribute definitions --> 
{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:pre: .pre}

#Getting started with dashDB
{: #dashDB}

<b>Note:</b> On June 20, 2017, IBM is renaming <b>dashDB for Transactions</b> to <b>Db2 on Cloud</b>. Over the coming weeks, documents will be updated to reflect this name change.

{{site.data.keyword.IBM}} {{site.data.keyword.dashdbshort}} managed service is an SQL database provisioned for you in the cloud. You can use {{site.data.keyword.dashdbshort_notm}} just as you would use any database software, but without the overhead and expense of hardware setup or software installation and maintenance. 
{: shortdesc}

##Interfaces
{: #interfaces}

You can work with your {{site.data.keyword.dashdbshort_notm}} database in four ways:
{: shortdesc}

   * {{site.data.keyword.dashdbshort_notm}} web console
   * REST APIs
   * Connect applications or your favorite tools from your local computer
   * Use {{site.data.keyword.dashdbshort_notm}} as a data source for your Bluemix apps or services

###dashDB web console
{: #web_console}

The web console provides a graphical interface for everything that you need to use your database, including: load facilities, an SQL editor, driver downloads, and more.
{: shortdesc}

![View of {{site.data.keyword.dashdbshort_notm}} web console dashboard page](images/console_v1.jpg)
<!-- ![View of {{site.data.keyword.dashdbshort_notm}} web console dashboard page](images/console_v2.jpg) -->

Click the link to take a tour of the {{site.data.keyword.dashdbshort_notm}} web console: [General tour ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/dashdb-general-quick-tour){:new_window}.

You can access your {{site.data.keyword.dashdbshort_notm}} web console in two ways:
   * From your {{site.data.keyword.Bluemix_notm}} dashboard - You can open the web console from the Service Details page for your {{site.data.keyword.dashdbshort_notm}} service.
   * Direct URL - You can bookmark the URL of the web console for your {{site.data.keyword.dashdbshort_notm}} service.

###REST APIs
{: #apis}

With {{site.data.keyword.dashdbshort_notm}} for Analytics plans, you can perform tasks related to file management, loading data, and running R scripts by using the [{{site.data.keyword.dashdbshort_notm}} REST API ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/dashdb-api){:new_window}.
{: shortdesc}

###Connect applications or your favorite tools from your local computer
{: #connect_apps}

Configure your local environment to connect to your {{site.data.keyword.dashdbshort_notm}} database by completing the following steps:
{: shortdesc}

1. Download the [{{site.data.keyword.dashdbshort_notm}} driver package ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package.html){:new_window} from the Downloads page of the {{site.data.keyword.dashdbshort_notm}} web console.
2. [Install the driver package ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package_install.html){:new_window} on the computer where your apps or tools are running.
3. [Configure the driver files ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/en/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_driver_package_config.html){:new_window} for your {{site.data.keyword.dashdbshort_notm}} database.

###Use dashDB as a data source for your Bluemix apps or services
{: #data_src}

Apps hosted on {{site.data.keyword.Bluemix_notm}} can connect to your {{site.data.keyword.dashdbshort_notm}} database exactly the same way your local applications connect to your {{site.data.keyword.dashdbshort_notm}} database.
{: shortdesc}

When your apps use the {{site.data.keyword.Bluemix_notm}} platform, you can take advantage of the `VCAP _SERVICES` environment variable to simplify the task of specifying database details and credentials:
1. On your {{site.data.keyword.Bluemix_notm}} dashboard, in the **Connections** tab of the Service Details page for your {{site.data.keyword.dashdbshort_notm}} service, click the **Create connection** button.
2. Select the {{site.data.keyword.Bluemix_notm}} app to use with your {{site.data.keyword.dashdbshort_notm}} database as a data source, and then click the **Connect** button.
3. Update your application code to retrieve database details and credentials from the `VCAP_SERVICES` environment variable:

    **Example without `VCAP_SERVICES`**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $database    = "BLUDB";         # Get these database details from
    $hostname    = "<Host-name>";   # the Connect page of the dashDB
    $port        = 50000;           # web console.
    $user        = "<User-ID >";    #
    $password    = "<Password>";    #
    $dsn         = "DATABASE=$database;" .
                   "HOSTNAME=$hostname;" .
                   "PORT=$port;" .
                   "PROTOCOL=TCPIP;" .
                   "UID=$user;" .
                   "PWD=$password;";

    $conn_string = $driver . $dsn;

    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

    **Example with `VCAP_SERVICES`**

    ```php
    <?php
    $driver      = "DRIVER={IBM DB2 ODBC DRIVER};";

    $vcap        = json_decode( getenv( "VCAP_SERVICES" ), true );
    $dsn         = $vcap[ "dashDB" ][0][ "credentials" ][ "dsn" ];

    $conn_string = $driver . $dsn;
                                   
    $conn        = db2_connect( $conn_string, "", "" );
    ?>
    ```

##Samples
{: #samples}

Here are links to samples demonstrating how to connect to your {{site.data.keyword.dashdbshort_notm}} database from applications in different languages:
{: shortdesc}

   * [.NET ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting__net_applications.html){:new_window}
<!-- * [JAVA ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_java.html){:new_window} -->
   * [JDBC ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_jdbc_applications.html){:new_window}
<!-- * [Node.js ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_nodejs.html){:new_window} -->
   * [PHP ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_php.html){:new_window}
<!-- * [Python ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.doc/connecting/connect_connecting_python.html){:new_window} -->
   * [dashDB samples on GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/dashdb-nodejs-helloworld){:new_window}


