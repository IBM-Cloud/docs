---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtering your logs for a specific field value
{:#k4_filter_logs_spec_field}

You can search for entries that include a specific field value. 
{:shortdesc}

Complete the following steps to search for entries that include a specific field value:

1. Look at the Kibana Discover page to see what subset of your data it displays. For more information, see [Identifying the data that is displayed in your Kibana Discover page](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. In the *Field List*, identify the field for which you want to define a filter and click it.

    A maximum of 5 values is shown for the field. Each value has two magnifying glass buttons. 
    
    If you cannot see the value, see [Adding a filter for a value that is not listed in the Fields list](k4_add_filter_out_value.html#k4_add_filter_out_value).

3. To add a filter that searches for entries with a field value, choose the magnifying button ![Magnifying glass button in inclusive mode](images/k4_include_field_icon.jpg "Magnifying glass button in inclusive") for that value.

    ![Filter that includes the field value](images/k4_add_filter_for_field.jpg "Filter that includes the field value")

    To add a filter that searches for entries that do not include that field value, choose the magnifying button ![Magnifying glass button in inclusive mode](images/k4_exclude_field_icon.jpg "Magnifying glass button in inclusive") for the value.

    ![Filter that excludes the field value](images/k4_add_filter_to_exclude_field.jpg "Filter that excludes the field value")

4. Choose any of the following options to work with filters in Kibana:

    <table>
      <tbody>
        <tr>
          <th align="center">Option</th>
          <th align="center">Description</th>
          <th align="center">Other info</th>
        </tr>
        <tr>
          <td align="left">Enable</td>
          <td align="left">Select this option to enable a filter.</td>
          <td align="left">When you add a filter, it is automatically enabled. <br> If a filter is disable, click on it to enable it.</td>
        </tr>
        <tr>
          <td align="left">Disable</td>
          <td align="left">Select this option to disable a filter.</td>
          <td align="left">After you add a filter, if you want to hide entries for a field value, click **disable**.</td>
        </tr>
        <tr>
          <td align="left">Pin</td>
          <td align="left">Select this option to persist the filter across Kibana pages.</td>
          <td align="left">You can pin a filter in the *Discover* page, the *Visualize* page, or the *Dashboard* page.</td>
        </tr>
        <tr>
          <td align="left">Toggle</td>
          <td align="left">Select this option to toggle a filter.</td>
          <td align="left">By default, entries that match a filter are displayed. To display entries that do not match, toggle the filter.</td>
        </tr>
        <tr>
          <td align="left">Remove</td>
          <td align="left">Select this option to remove a filter.</td>
          <td align="left"></td>
        </tr>
      </tbody>
    </table>

 

 
 

