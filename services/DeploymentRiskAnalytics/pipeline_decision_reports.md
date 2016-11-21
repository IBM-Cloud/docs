---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Viewing dashboards and reports
{: #DRA_toolchain_reports}

*Last updated: 21 October 2016*
{: .last-updated}

{{site.data.keyword.DRA_short}} provides you with a wealth of actionable information about your projects.
{:shortdesc}

## {{site.data.keyword.DRA_short}} dashboards

{{site.data.keyword.DRA_short}} provides dashboards that allow you to monitor build status, environment status, and test performance  across your Bluemix organization. To see them, after opening {{site.data.keyword.DRA_short}}, click the **Build Verification**, **Test Results**, or **Environments** tabs, respectively.

The dashboards are automatically populated with the most recent information from your pipelines' {{site.data.keyword.DRA_short}} test jobs. Click on the elements within the dashboards for more information about them. 

## Viewing decisions reports

After a pipeline has been configured and run, {{site.data.keyword.DRA_short}} starts to collect and analyze the test results from it pipeline to establish a baseline. Each time a pipeline runs, data is collected and compared against previous runs. After the analysis is complete, at each gate {{site.data.keyword.DRA_short}} decides to either allow the deployment to proceed or stop the pipeline if the rules for the gate were not met.

To view the decision report for a gate from the pipeline, complete these steps:

   1. On the stage that contains the gate to check, click **View logs and history**.

   2. From the jobs window of the stage, click the gate's name.

    ![Deployment Risk Analytics is active](images/DRA_gate.png)

   3. In the log view, locate the message 'Check {{site.data.keyword.DRA_short}} report here` and click the provided link to open the report.

    ![Deployment Risk Analytics decision](images/DRA_report.png)
