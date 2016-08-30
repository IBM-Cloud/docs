---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Viewing decision reports
{: #DRA_toolchain_reports}

*Last updated: 25 August 2016*
{: .last-updated}

To run {{site.data.keyword.DRA_short}} in the pipeline, start the pipeline from the initial stage as you normally would, or if you would prefer to just test {{site.data.keyword.DRA_short}}, run a stage that contains {{site.data.keyword.DRA_short}} jobs.
{:shortdesc}

##The {{site.data.keyword.DRA_short}} dashboard

The {{site.data.keyword.DRA_short}} dashboard allows you to monitor test performance and code coverage across your Bluemix organization at a glance. To see it, after opening {{site.data.keyword.DRA_short}}, click the **Build status** tab.

The dashboard is automatically populated with the most recent test results and code coverage figures for every microservice in your organization. Click the arrow beside an environment to see the tests that it comprises.

## Viewing decisions reports

After a pipeline has been configured and run, {{site.data.keyword.DRA_short}} starts to collect and analyze the test results from it pipeline to establish a baseline. Each time a pipeline runs, data is collected and compared against previous runs. After the analysis is complete, at each gate {{site.data.keyword.DRA_short}} decides to either allow the deployment to proceed or stop the pipeline if the rules for the gate were not met.

To view the decision report for a gate, complete these steps:

   1. On the stage that contains the gate to check, click **View logs and history**.

   2. From the jobs window of the stage, click the gate's name.

    ![Deployment Risk Analytics is active](images/DRA_gate.png)

   3. In the log view, locate the message 'Check {{site.data.keyword.DRA_short}} report here` and click the provided link to open the report.

    ![Deployment Risk Analytics decision](images/DRA_report.png)
