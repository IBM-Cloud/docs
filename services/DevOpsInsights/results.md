---

copyright:
  years: 2016, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Viewing results

## Deployment Risk evaluations

After a pipeline runs, {{site.data.keyword.DRA_short}} starts to collect and analyze the test results from it to establish a baseline. Data from every subsequent run is collected and compared against previous results. Decision gates use this data to determine when to stop a deployment. 

You can see your deployment and gate evaluation data from the Deployment Risk dashboard. To open the dashboard, open {{site.data.keyword.DRA_short}} and from the side menu, click **Deployment Risk**.

If you are using a {{site.data.keyword.contdelivery_short}} pipeline, you can view individual gate execution reports from the pipeline itself. To view the decision report for a gate from the pipeline:

1. On the stage that contains the gate to check, click **View logs and history**.

2. From the job that contains the gate, click the gate's name.

3. In the log view, find the `Check {{site.data.keyword.DRA_short}} report here` message and click the link to open the report.

## Developer Insights and Team Dynamics reports

You can view dashboards about your team and code after an initial data mining period. In the service navigation menu, click **Developer Insights** or **Team Dynamics** and then select a data category to view this information.
