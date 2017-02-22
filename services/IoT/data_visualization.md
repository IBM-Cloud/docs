---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visualizing real-time data by using boards and cards
{: #boards_and_cards}

Create boards and cards to create and share your own dashboards that visualize your device data in real time.
{:shortdesc}

By using boards and cards, you can graphically visualize data set values from one or more devices to provide a quick overview and enhance understanding of the data. Create boards and add cards that display the data as raw numbers, real-time graphs, gauges, and more. Add members to your boards to share them with other users in your organization. Arrange the cards and add explanatory text dividers to fine-tune your presentation.  

You can also expand on the default set of IBM provided cards by [creating your own custom cards](custom_cards/custom-cards.html).

![Showing real-time data with cards.](images/boards_and_cards.svg "Showing real-time data with cards.")

## Default boards
{: #default_boards}
The {{site.data.keyword.iot_full}} dashboard has the following default boards:

|Board Name | Description |  
|:---|:---|  
|Usage overview  | Shows usage statistics for your organization. Lists device types and the data that is consumed.
|Rule-Centric Analytics | Shows the rules for your organization. Additional cards list triggered alerts, associated devices, device properties, and alert information. |  
|Device-Centric Analytics | Shows the devices that are connected to your organization. Additional cards show alerts for a selected device,  information for a selected device, device properties, and alert information. |
|Risk and Security Management | Shows cards that summarize the overall security status. System operators and security analysts can view details of compliance, connection status for devices, the causes of connection failures, and the devices that are blocked or allowed through a blacklist or whitelist.  From the Connection Compliance card, the user can drill down to a detailed report about non-compliant devices, and can export the report to the Excel. |

You can update these boards by adding, updating, and removing cards.

**Tip:** To reset a default board to its original state you can delete it. The board is then re-created with the original cards.

## Creating boards and cards
{: #visualizing_data}

{{site.data.keyword.iot_short_notm}} provides a built-in dashboard that you can use to display the real-time data that your device is returning. By default, the Overview page displays usage information about your {{site.data.keyword.iot_short_notm}} organization, such as data and the storage space that is consumed. To see real-time device data as it flows in, add device-specific cards to this page.

To add a device-specific card to a board:
1. In the {{site.data.keyword.iot_short_notm}} dashboard, select **Boards**.
2. Select a board that you have editing rights for or create a new board.
3. In the board, click **Add New Card**.
2. In the Edit Generic Visualization Card box, scroll down to the Devices section.
3. Select a visualization type.
**Tip:** Select **Generic visualization** for the basic configuration. You can change the card type later.
Click **Show more** for the full list of card types.
4.	Select one or more card data sources and then click **Next** to add one or more data sets.
 1.	Give the data set an identifying name.
 2. Select an event that includes the data point that you want to display.
 3.	Select the property that represents the data point.
 4.	Set the type, unit, precision, and minimum and maximum values for the data point.  
 When you are done you can click **New Data Set** to add more data sets or click **Next**.
5.	Select the visualization.  
Select the type and size of visualization that you want to use.  Some card types have more settings.
<dl>
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
<td>A pie chart that displays the number of devices per device type.</td>
</tr><tr>
<td>Transfered data</td>
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
<td>The value of one or more data sets. </br>**Tip:** To see up to three data point values in a small table, choose the large widget size.  </td>
</tr>
<tr>
<td>Real-time chart</td>
<td>One or more data sets in a real-time scrolling chart. Use the Settings menu to set the data range and retention, the look and feel of the graphs, and more. </td>
</tr>
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
<td>The value of a data set shown as a gauge. You can configure display thresholds for good, fair, and critical values of the data set. Use the Settings menu to optionally set gauge thresholds for lower, middle, and upper data ranges.  </td>
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
<td>Device info</td>
<td>Shows basic information for a single device.</td>
</tr>
<tr>
<td>Alert info</td>
<td>Shows basic information for a single alert.</td>
</tr>
<tr>
<td>Device list</td>
<td>A list to monitor multiple devices.</td>
</tr>
<tr>
<td>Alerts</td>
<td>A list of alerts for a device.</td>
</tr>
<tr>
<td>Rules</td>
<td>A list of the rules that have alerts.</td>
</tr>
<tr>
<td>Device properties</td>
<td>Shows specific properties for one or more devices.</td>
</tr>
<tr>
<td>All device properties</td>
<td>Show all properties for one or more devices.</td>
</tr>
<tr>
<td>Device map</td>
<td>Shows the location of multiple devices in a list.</td>
</tr>
</tbody>
</table>
</dd>
</dl>

6. Specify the data source for the card.  
Depending on the card type that you selected, the data that is displayed on a card might come from a device or from another card. Select a specific device or a device list or an alert list card for the data source and then click **Next**.
7. Devices type cards only: Add one or more data sets to display in the card.   
 1. Click **Connect data set** to add a property to display in the card.
 2. Give the data set a name.
 3. Enter or select the event to display properties for.
 4. Enter or select the property to display.
 5. Specify the type of the property and optionally set unit, precision, minimum, and maximum values for the property.  
 6. Click **Next**.
7. Select the presentation size.   
For certain card types, you can click **Settings** to configure additional visualization details. Click **Next**.
7. Provide a title and a description for the card and optionally select a color scheme and then click **Submit** to create the card.
7.	Finally, position the new card on your board by dragging it to a good location.  

Great! You can now see the real-time data of your device!

For step-by-step instructions about how to display real-time device data, see the [Configuring Boards & Cards in the new Watson IoT Dashboard ![External link icon](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/configuring-the-cards-in-the-new-watson-iot-dashboard/){: new_window} recipe.
