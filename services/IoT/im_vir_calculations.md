---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-12"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Advanced calculations for edge virtual properties
{: #im_vir_calculations}

Extend the basic virtual property calculations with premade edge analytics formulas.
{:shortdesc}

**Important:** The advanced calculations only return property datapoints if the data for the selected property comes from a device that is connected to a gateway that has an Edge Analytics Agent installed. An edge rule can use this virtual property directly. To use the property with a cloud rule, an edge rule must send the datapoint to the cloud by using the Forward to cloud action. For more information, see [Installing the edge analytics agent](gateways/dashboard.html#edge).

Example: Use the advanced virtual datapoints in a line graph card to visualize data trends with data spikes removed.  
 ![Actual datapoints vs. average datapoints.](images/vir_adv_avg_card.svg "Comparison between actual and averaged datapoints.")

## Advanced formulas
{: #advanced}

The advanced calculation options include the following formulas:

**Tip:** For some of the formulas you have the option to choose a period length or a number of datapoints to include. If you know that your data flows at a consistent frequency, a time window might be a good choice. If the data is collected sporadically or unevenly, it might be best to use number of datapoints, because the time window is difficult to predict.

<table>
<thead>
<tr>
<th>Formula</th>
<th>Description</th>
<th>Usage</th>
</tr>
</thead>
<tbody>
<tr>
<td>Average</td>
<td>Returns the average value for a property over a number of recent datapoints or over a recent period.  </br></br>
Input:
<ul>
<li>Property
 <li>Period length or number of datapoints in the form of an integer that is larger than 0.</ul></td>
 <td>The AVG formula provides an average value of datapoints across a time window that is constantly moving.  </br></br> Use the average formula with a rule to avoid triggering false alerts based on noisy data that contains isolated spikes.  </br></br>Use a line graph card to visualize data trends with data spikes removed.  
</td>
</tr>
<tr>
<td>Moving Z-score</td>
<td>Returns the difference in standard deviation units between the datapoint and the mean datapoint value over a number of recent datapoints or over a recent period.  </br></br>
Input:
<ul>
<li>Property
<li>Period length or number of datapoints in the form of an integer larger than 0.</ul></td>
<td>The Moving Z-Score of a datapoint indicates the extent of an anomaly for the datapoint value relative to its recent average. A higher absolute z-score value means that the value of the current datapoint differs more from previous average datapoint values.
</br></br>Use the Moving Z-Score formula with a rule to trigger alerts on rapid change when the datapoint values differ from the recent average rather than when the datapoint exceeds a certain value.
</br></br>Use a line graph card to visualize fluctuations in your data by plotting the frequency and magnitude in standard deviations.
</td>
</tr>
<tr>
<td>Exponential smoothing</td>
<td>Returns the average value for a property over available collected datapoints, where the older property values are weighted exponentially less than newer values. The weight is controlled by the smoothing factor, where a larger value gives more weight to recent values and less to older values.  
You can also optionally use the slope factor to adjust for any trends in the data. Exponentially smoothed values reacts quicker to changes in the data than moving average does.  </br></br>
Input:
<ul>
<li>Property
<li>Smoothing factor, as a number that is larger than 0 and smaller than 1.  
<li>Optional: Slope, as a number that is larger than 0 and smaller than 1.   </br>
 **Tip:** If you are unsure if your collected data has trends, start by using a slope of .5. Depending on your results, you might want to adjust the factor.
 </ul></td>  
 <td>Applying exponential smoothing to a datapoint results in an average value where older values are weighted less when calculating the average rather than defining a period length. Instead, you limit the weight of distant values by setting a higher smoothing factor.
</br></br>Use the exponential smoothing formula with a rule to avoid triggering false alerts based on noisy data that contains isolated spikes by using all available data instead of a subset.
</br></br>Use a line graph card to visualize data trends with data spikes removed.</td>
</tr>
<tr>
<td>Box smoothing</td>
<td>Returns the average value for a property based on a range of datapoints that are centered around the current datapoint.  
Box smoothing uses a configured number of datapoint values that come before and after the currently processed datapoint to determine its smoothed value. In its calculation, box smoothing weighs all the datapoint values equally.  </br></br>
Input:
<ul>
<li>Property
<li>Number of datapoints ahead and behind (half-width) in the form of an integer larger than 0.
</ul></td>
<td>Applying box smoothing to a datapoint returns an average value of datapoints across a time window that is constantly moving and that is centered on the datapoint of interest. </br></br>**Important:** Depending on the data frequency and the half-width value, the returned datapoints are more or less delayed. For example, if the half-width is set to `5` and the data frequency is one message every second, the returned virtual datapoints are delayed by five seconds. </br></br>Use the box smoothing formula with a rule to avoid triggering false alerts based on noisy data that contains isolated spikes. **Important:** Be aware of the datapoint delay when creating your rules. </br></br>Use a line graph card to visualize data trends with data spikes removed.
</td>
</tr>
<tr>
<td>Gaussian smoothing</td>
<td>Returns the average value for a property based on a range of datapoints that are centered around the current datapoint, where property values farther from the current datapoint are weighted exponentially less than closer values.</br></br>
Input:
<ul>
<li>Property
<li>Number of datapoints ahead and behind (half-width) in the form of an integer that is larger than 0.
</ul></td>
<td>Applying gaussian smoothing to a datapoint returns a weighted average value of datapoints across a time window that is constantly moving and that is centered on the datapoint of interest. Datapoints that are farther from the datapoint of interest are weighted less when calculating the average. </br></br>**Important:** Depending on the data frequency and the half-width value, the returned datapoints are more or less delayed. For example, if the half-width is set to `5` and the data frequency is one message every second, the returned virtual datapoints are delayed by five seconds. </br></br>Use the gaussian smoothing formula with a rule to avoid triggering false alerts based on noisy data that contains isolated spikes. **Important:** Be aware of the datapoint delay when creating your rules. </br></br>Use a line graph card to visualize data trends with data spikes removed.
</td>
</tr>
</tbody>
</table>  
