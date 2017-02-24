---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Viewing dashboards and reports
{: #DRA_toolchain_reports}

{{site.data.keyword.DRA_short}} provides you with a wealth of actionable information about your projects.
{:shortdesc}

## {{site.data.keyword.DRA_short}} dashboards    
{: #DI_toolchain_dashboards}

{{site.data.keyword.DRA_short}} provides dashboards that display information about performance across your Bluemix organization. To see them, after you open {{site.data.keyword.DRA_short}}, click **Build Verification** or **Deploy Verification**.

The dashboards are automatically populated with the most recent information from your pipelines' {{site.data.keyword.DRA_short}} test jobs. Click the elements within the dashboards for more information about them.

### Key performance indicators in builds    
{: #DI_key_performance_indicators}

The **Build Verification** page contains three graphs that contain information about the health of the selected development branch:

<table>
<thead>
<tr>
<th>Graph</th>
<th>Description</th>
</tr>
</thead>

<tbody>
<tr>
<td>Latest Builds</td>
<td>The number of recent builds that completed compared to the total number of recent builds.</td>
</tr>
<tr>
<td>Tests</td>
<td>The number of tests that passed compared to the total number of tests.</td>
</tr>
<tr>
<td>Code Coverage</td>
<td>The percentages of your code's statements and functions that are called by your tests.</td>
</tr>
</tbody></table>

## Viewing decision reports    
{: #DI_decision_reports}

After a pipeline runs, {{site.data.keyword.DRA_short}} starts to collect and analyze the test results from it to establish a baseline. Data from every subsequent run is collected and compared against previous results. Decision gates use this data to determine when to stop a deployment. 

To view the decision report for a gate from the pipeline, complete these steps:

   1. On the stage that contains the gate to check, click **View logs and history**.

   2. From the jobs window of the stage, click the gate's name.

   3. In the log view, locate the message 'Check {{site.data.keyword.DRA_short}} report here` and click the provided link to open the report.
