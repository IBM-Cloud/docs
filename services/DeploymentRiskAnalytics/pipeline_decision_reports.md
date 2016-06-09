---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Viewing Decision Reports
{: #DRA_toolchain_reports}

*Last updated: 09 June 2016*

To run {{site.data.keyword.DRA_short}} in the pipeline, start the pipeline from the initial stage as you normally would, or if you would prefer to just test {{site.data.keyword.DRA_short}}, run a stage that contains {{site.data.keyword.DRA_short}} jobs.
{:shortdesc}

After your pipeline has been configured and run, {{site.data.keyword.DRA_short}} starts to collect and analyze the test results from your pipeline to establish a baseline. Each time the pipeline runs, data is collected and compared against previous runs. After the analysis is complete, at each gate {{site.data.keyword.DRA_short}} decides to either allow the deployment to proceed or stop the pipeline if the criteria for the gate was not met.

To view the decision report for a gate, complete these steps:

   1. On the stage that contains the gate to check, click **View logs and history**.

   2. From the jobs window of the stage, click the gate's name.

    ![Deployment Risk Analytics is active](images/DRA_gate.png)

   3. In the log view, locate the message 'Check {{site.data.keyword.DRA_short}} report here` and click the provided link to open the report.

    ![Deployment Risk Analytics decision](images/DRA_report.png)
