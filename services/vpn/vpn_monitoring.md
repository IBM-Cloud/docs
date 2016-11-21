---

copyright:

  years: 2015, 2016

lastupdated: "2016-11-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Monitoring status and traffic flow
{: #monitor}  

Use the monitoring feature to view the connection status and traffic flow between your on-premises or {{site.data.keyword.BluSoftlayer}} server VPN gateway, and the {{site.data.keyword.vpn_short}} gateway. 
{:shortdesc}  
##Monitoring on service dashboard
{: #dashboard}

Select the **Monitoring** tab to view the following connection statistics.

* **Connection Status:** Up or Down status of the VPN connection between your on-premises or {{site.data.keyword.BluSoftlayer}} server VPN gateway, and the IBM VPN gateway.  
* **Traffic Outbound (Bytes) (in last 10 minutes)** and **Traffic Outbound (Packets) (in last 10 minutes):** Traffic flow from the IBM VPN gateway to your on-premises or {{site.data.keyword.BluSoftlayer}} server VPN gateway. Each datapoint on the graph represents data that is transmitted in the 10 minutes before the datapoint time.  
* **Traffic Inbound (Bytes) (in last 10 minutes)** and **Traffic Inbound (Packets) (in last 10 minutes):** Traffic flow from your on-premises or {{site.data.keyword.BluSoftlayer}} server VPN gateway to the IBM VPN gateway. Each datapoint on the graph represents data that is transmitted in the 10 minutes before the datapoint time.  

The monitoring statistics are displayed as graphs. You can set the time window to the last hour, last 2 hours, last 24 hrs, or last 3 days. The graphs are automatically updated every 20 minutes. However, you can fetch the latest data any time by switching away from the monitoring tab and returning to it.

**Note:** The graphs show data based on the local time of the browser that is used to view the monitoring page.  

##Monitoring using the Grafana dashboard
{: #logmet}

Use [Grafana](https://logmet.{DomainName}) to view detailed connection statistics. 

1. Log in with your Bluemix credentials, and the space and org name where you have created the IBM VPN service instance.  
2. Select the folder icon (![](images/folder.png)) on the top right.
3. Select **VPN Service Monitoring** from the list of dashboards to view the graphs. The graphs use local time.  

**Note:** You must select the **Monitoring** tab on the IBM VPN service dashboard at least once to send a query to Grafana to create the VPN service dashboard in Grafana. Grafana takes up to 10 minutes after you establish the VPN connection to show the connection statistics.


