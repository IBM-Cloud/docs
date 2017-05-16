---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Managing resources in your environments
{: #managing}

{{site.data.keyword.bplong}} simplifies the management of your environments. You can modify your deployed resources and repeatedly redeploy changes on-demand.

{:shortdesc}

Changes to your environment can be deployed with a lightweight process. When you want to change what resources are allocated, you code changes to your configuration in declarative syntax, meaning you state only your wanted outcome. With {{site.data.keyword.bpshort}}, you can preview your changes before deployment.


## Updating resources with the GUI
{: #gui}

If you prefer a graphical view to manage the resources in your environments, you can use the {{site.data.keyword.bpshort}} dashboard.
{:shortdesc}

After you publish code changes to your configuration in GitHub, or modify variables in the GUI, complete the following steps to deploy updates to your environment:

1. In the **{{site.data.keyword.bpshort}}** dashboard, select **Environments**.

2. Click the row of the specific environment that you want to update.

3. Click **Plan** and inspect your plan log for errors. The environment is locked until you or other collaborators in your {{site.data.keyword.Bluemix_notm}} account apply the plan or cancel it. 

4. Click **Apply** to deploy updates. 


## Updating resources with the CLI
{: #cli}

You can programmatically update resources in your environments with the {{site.data.keyword.bpshort}} CLI.
{:shortdesc}

After you publish code changes to your configuration in GitHub, complete the following steps to deploy updates to your environment:

1. Run the `plan` command. The {{site.data.keyword.bpshort}} CLI pulls the updated environment configuration from GitHub and outputs a preview how your resources differ against your current deployment.

  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}

2. View the plan output in the activity log.

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

3. Deploy your plan by running the `apply` command. 

  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}


## Updating resources with the API
{: #api}

You can programmatically manage resources in your environments with the {{site.data.keyword.bpshort}} API. 
{:shortdesc}

After you publish code changes to your configuration in GitHub, complete the following steps to deploy updates to your environment:

1. Run the `POST v1/environments/<environment_ID>/plan` call. The {{site.data.keyword.bpshort}} API pulls the updated environment configuration from GitHub and compares it with the Terraform state file to show how your resources differ against your current deployment.

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

  Example response:
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

2. View the plan output in the activity log.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. Deploy your plan by running the `PUT /v1/environments/<environment_ID>/apply` call. 

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
  ```
  {: codeblock}


## Auditing changes to your environments
{: #auditing}

Configurations can be audited in the version history of your source control repository. To monitor deployments to your environment, or view logs of previous deployments, {{site.data.keyword.bpshort}} offers the following options to view audit logs.

### From the {{site.data.keyword.bpshort}} dashboard
{: #auditing-gui}

1. Select the row of the environment to access the environment details page.

2. Monitor the **Recent Activities** section. You can also view historical logs of previous plans and deployments.

### With the {{site.data.keyword.bpshort}} CLI
{: #auditing-cli}

1. Retrieve your environment ID.

  ```
  bx schematics environment list
  ```
  {: codeblock}

2. Retrieve the activity IDs for your environment. Activity IDs are assigned to plan, apply, destroy, and delete actions. The following command lists all of the activities that ran against your environment.

  ```
  bx schematics activity list --id ENVIRONMENT_ID
  ```
  {: codeblock}

3. Retrieve data about a specific activity, such as who made changes to an environment and when.

  ```
  bx schematics activity show --id ACTIVITY_ID
  ```
  {: codeblock}

4. Optional: To view a detailed log, such as plan or apply output, run the `log` command. 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

### With the {{site.data.keyword.bpshort}} API
{: #auditing-api}

1. Retrieve your environment ID.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
  
  The response body contains all environments in your {{site.data.keyword.Bluemix_notm}} account. Locate the `id` value of the specific environment that you want to audit.

2. Retrieve the activity IDs for the actions run against your environment.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. Get a specific activity for an environment. 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID> \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

4. Inspect a detailed log of the Terraform output.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
