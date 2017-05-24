---

copyright:
  years: 2015, 2017

lastupdated: "2017-05-22"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Navigating to the Kibana dashboard
{: #k4_launch}

You can launch Kibana from the {{site.data.keyword.Bluemix}} UI or directly from a web browser.
{:shortdesc}

Launch Kibana from {{site.data.keyword.Bluemix_notm}} to view and analyze data in context to the resource from which you launch Kibana. For example, you can launch to your specific CF app logs in Kibana, in context to that specific App.
    
Launch Kibana from a direct browser link if you want to see aggregated log data from services within a provided {{site.data.keyword.Bluemix_notm}} space. The query that is used to filter the data that is displayed in the dashboard retrieves log entries for a space in the {{site.data.keyword.Bluemix_notm}} organization. The log information that Kibana displays includes records for  all resources that are deployed within the space of the {{site.data.keyword.Bluemix_notm}} organization that you are logged in. 

The following table lists the resources and the supported navigation method to launch Kibana:

<table>
<caption>Table 1. List of resources and supported navigation methods. </caption>
  <tr>
    <th>Resource</th>
    <th>Navigating to the Kibana dashboard from the Bluemix dashboard</th>
    <th>Navigating to the Kibana dashboard from a web browser</th>
  <tr>
  <tr>
    <td>CF app</td>
    <td>Yes</td>
    <td>Yes</td>
  <tr>  
  <tr>
    <td>Container deployed in a Kubernetes cluster</td>
    <td>No</td>
    <td>Yes</td>
  <tr>  
  <tr>
    <td>Container deployed in a {{site.data.keyword.Bluemix_notm}}-managed Cloud infrastructure</td>
    <td>Yes</td>
    <td>Yes</td>
  <tr>  
</table>

For more information about Kibana, see the [Kibana User Guide ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.
    

##  Navigating to the Kibana dashboard from the Bluemix dashboard
{: #launch_Kibana_from_bluemix}

The query that is used to filter the data that is displayed in Kibana retrieves log entries for the {{site.data.keyword.Bluemix_notm}} CF app or container from where you launch Kibana.

To see the logs of a Cloud Foundry application or Docker container in Kibana, complete the following steps:

1. Log in to {{site.data.keyword.Bluemix_notm}}, and then click the app name or container from the {{site.data.keyword.Bluemix_notm}} dashboard. 
    
2. Open the log tab in the {{site.data.keyword.Bluemix_notm}} UI.

    * For CF apps, click **Logs** in the navigation bar. 
    * For containers that are deployed in the {{site.data.keyword.Bluemix_notm}}-managed Cloud infrastructure, select **Monitoring and logs** in the navigation bar and then click the **Logging** tab. 
    
        The logs tab opens.  

3. Click **Advanced view**. The Kibana dashboard opens.

    By default, the **Discover** page loads with the default index pattern selected and a time filter set to the last 30 seconds. The search query is set to match all entries for the your CF app or Docker container.

    If the Discover page does not show any log entries, adjust the time picker. For more information, see [Setting a time filter](logging_kibana_set_time_filter.html#set_time_filter).


##  Navigating to the Kibana dashboard from a web browser
{: #launch_Kibana_from_browser}

The query that is used to filter the data that is displayed in Kibana retrieves log entries for a space in the {{site.data.keyword.Bluemix_notm}} organization. The log information that Kibana displays includes records for all resources that are deployed within the space of the {{site.data.keyword.Bluemix_notm}} organization that you are logged in.

Complete the following step to launch Kibana from a browser:

1. Open [https://logging.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logging.{DomainName}) to log in to the Kibana user interface.
    
    For example, 
      
        <table>
          <caption>Table 1. URLs to launch Kibana  </caption>
           <tr>
            <th>Region</th>
            <th>URL</th>
          </tr>
          <tr>
            <td>US South</td>
            <td>https://logging.ng.bluemix.net/ </td>
          </tr>
          <tr>
            <td>United Kingdom</td>
            <td>https://logging.eu-gb.bluemix.net/ </td>
          </tr>
        </table>

    If the Discover page does not show any log entries, adjust the time picker. For more information, see [Setting a time filter](logging_kibana_set_time_filter.html#set_time_filter).


