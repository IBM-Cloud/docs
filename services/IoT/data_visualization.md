---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-08"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Visualizing real-time data by using boards and cards
{: #boards_and_cards}

Create boards and cards to create and share your own dashboards that visualize your device data in real time.
{:shortdesc}

By using boards and cards, you can graphically visualize data set values from one or more devices to provide a quick overview and enhance understanding of the data. Create boards and add cards that display the data as raw numbers, real-time graphs, gauges, and more. Add members to your boards to share them with other users in your organization. Arrange the cards and add explanatory text dividers to fine-tune your presentation.  

You can also expand on the default set of cards by [creating your own custom cards](custom_cards/custom-cards.html).

![Showing real-time data with cards.](images/boards_and_cards.svg "Showing real-time data with cards.")

## Default boards
{: #default_boards}
The {{site.data.keyword.iot_full}} dashboard has the following default boards:

|Board Name | Description | Cards Included
|:---|:---|:---|  
|Usage Overview  | The usage statistics for your organization. Lists device types and the data that is consumed. | <ul><li>Device types<li>Data transferred</ul>
|Rule-Centric Analytics | The rules for your organization. Additional cards list triggered alerts, associated devices, device properties, and alert information. | <ul><li>Rules I Manage<li>Rule Alerts<li>Rule Alert Info<li>Associated Devices<li>Device Info<li>Device Properties</ul>  
|Device-Centric Analytics | The devices that are connected to your organization. Additional cards show alerts for a selected device,  information for a selected device, device properties, and alert information. | <ul><li>Devices I Care About<li>Device Info<li>Rule Alerts For That Device<li>Rule Alert Info<li>Device Properties</ul>
|Risk and Security Overview (Beta) | The overall security status of your organization. System operators and security analysts can view details of compliance, connection status for devices, the causes of connection failures, and the devices that are blocked or allowed by a blacklist or whitelist.  From the Connection Compliance card, users can drill down to a detailed report about non-compliant devices and can export the report to the Excel. | <ul><li>Policy Compliance<li>Connection Security<li>Blacklist/Whitelist Compliance</ul>

You can update these boards by adding, updating, and removing cards.

To reset a default board to its original state, you can delete it. The board is then re-created with the original cards.
{: tip}

## Creating boards and cards
{: #visualizing_data}

{{site.data.keyword.iot_short_notm}} provides a built-in dashboard that you can use to display the real-time data that your device is returning. By default, the Overview page displays usage information about your {{site.data.keyword.iot_short_notm}} organization, such as data and the storage space that is consumed. To see real-time device data as it flows in, add device-specific cards to this page.

For a recipe of step-by-step instructions for how to display real-time device data, see the [Configuring Boards & Cards in the new Watson IoT Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/configuring-the-cards-in-the-new-watson-iot-dashboard/){: new_window} recipe.
{: tip}

To create a board and add a card to that board:
1. In the {{site.data.keyword.iot_short_notm}} dashboard, select **Boards**.
2. Select a board that you have editing rights for or create a new board.
3. In the board, click **Add New Card**.
3. Select a card type.  
**Tip:** If you are not sure which visualization to pick for a devices type card, select **Generic visualization**. You can change the card type later.
<dl>
<dt>Devices</dt>
<dd><table>
<thead>
<tr>
<th>Type</th>
<th>Data that is displayed</th>
</tr>
</thead>
<tbody>
<tr>
<td>Generic visualization</td>
<td>The value of one or more data sets. </br>**Tip:** To see up to three data point values in a small table, choose the large widget size. </td>
</tr>
<tr>
<td>Line chart</td>
<td>One or more data sets in a real-time scrolling chart. Use the Settings menu to set the data range and retention, the look and feel of the graphs, and more. </td>
<tr>
<td>Bar chart</td>
<td>Data set values in labeled bars. Use the Settings menu to toggle horizontal or vertical bar direction.</td>
</tr>
<tr>
<td>Donut chart</td>
<td>Two or more data sets in a circular representation.</td>
</tr>
<tr>
<td>Value</td>
<td>The raw value of one or more data sets.</td>
</tr>
<tr>
<td>Gauge</td>
<td>The value of a data set shown as a gauge. Use the Settings menu to optionally set gauge thresholds for lower, middle, and upper data ranges.  </td>
</tr>
<tr>
<td>Device properties</td>
<td>Specific properties for one or more devices.</td>
</tr>
<tr>
<td>All device properties</td>
<td>All properties for one or more devices.</td>
</tr>
<tr>
<td>Device list</td>
<td>A list to monitor multiple devices. A list can be used as a data source for other cards. </br>You can filter lists by device ID and type in the card settings. Device lists of size L or larger can also be interactively filtered by clicking the filter icon in the card. Filter entries can be added as single entries, ranges (x-y), or comma-separated.</br> By default, a list displays device ID and type. You can configure the list card settings to have the card also display other device metadata.  </td>
</tr>
<tr>
<td>Device info</td>
<td>Basic information for a single device.</td>
<tr>
<td>Device map</td>
<td>The location of devices in a device list.</td>
</tr>
</tbody>
</table>
</dd>
<dt>Analytics</dt>
<dd>
<table>
<thead>
<tr>
<th>Type</th>
<th>Data that is displayed</th>
</tr>
</thead>
<tbody>
<tr>
<td>Rules</td>
<td>A list of the rules that have alerts.</td>
</tr>
<tr>
<td>Rule alerts</td>
<td>A list of alerts for a device.</td>
</tr>
<tr>
<td>Alert info</td>
<td>Basic information for a single alert.</td>
</tr>
</tbody>
</table>
</dd>
<dt>Risk Management (Beta)</dt>
<dd>Available with [Advanced Security](reference/security/RM_security.html) organizations only.
<table>
<thead>
<tr>
<th>Type</th>
<th>Data that is displayed</th>
</tr>
</thead>
<tbody>
<tr>
<td>Policy Compliance</td>
<td>An overview of connection security and of blacklisted and whitellisted devices.</td>
</tr>
<tr>
<td>Blacklist/Whitelist Compliance</td>
<td>The number of blacklisted or whitelisted devices.</td>
</tr>
<tr>
<td>Connection Security</td>
<td>The number of devices that failed the connection security check.</td>
</tr>
</tbody>
</table>
</dd>
<dt>Usage</dt>
<dd>
<table>
<thead>
<tr>
<th>Type</th>
<th>Data that is displayed</th>
</tr>
</thead>
<tbody>
<tr>
<td>Device types</td>
<td>A pie chart that displays the number of registered devices per device type for your organization.</td>
</tr><tr>
<td>Data transfered</td>
<td>Usage statistics for transferred data for your organization.</td>
</tr>
</tbody>
</table>
</dd>
<dt>Basic</dt>
<dd>
<table>
<thead>
<tr>
<th>Type</th>
<th>Data that is displayed</th>
</tr>
</thead>
<tbody>
<tr>
<td>Separator</td>
<td>A horizontal separator to structure and group cards on the board.</td>
</tr>
</tbody>
</table>
</dd>
</dl>

4.	Select the card source data.  
Select one or more card data sources and then click **Next**.  
Data sources can be single registered devices or other cards. To use a card data source, a list or map card must exists on the board.  
5. Add one or more data sets for each of your data sources.
 - Devices
    2. Select an event that includes the data point that you want to display.
    3.	Select the property that represents the data point.
    1.	Give the data set an identifying name.
    4.	Set the type, unit, precision, and minimum and maximum values for the data point.  
    When you are done, you can click **New Data Set** to add more data sets or click **Next**.
 - Lists
    2. Select a device type or select **Any device type**.
    2. Select an event that includes the data point that you want to display.
    3.	Select the property that represents the data point.
    1.	Give the data set an identifying name.
    4.	Set the type, unit, precision, and minimum and maximum values for the data point.  
    When you are done, you can click **New Data Set** to add more data sets or click **Next**.
5.	Customize the card visualization in card preview.  
 7. Select the presentation size.  
In addition to setting the size of the card on your board, the card size setting also controls other presentation variables, such as the number of devices that are listed, the graph metadata that is displayed, and so on.   
**Tip:** Click the different size labels to see previews of the cards at different sizes.
 8. Configure any additional settings.  
If the card supports it, click **Settings** to see additional settings that you can configure, such as data ranges for gauge type cards and filtering options for device list cards.
6. Update the card information.  
 1. Provide a title and a description for the card and, optionally, select a color scheme.   
 2. Click **Submit** to create the card.
7.	Position the new card on your board by dragging it to a good location.  
