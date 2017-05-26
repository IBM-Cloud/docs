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

# Destroying resources in temporary environments
{: #destroying}

You can use {{site.data.keyword.bplong}} to destroy your resources. When you destroy your resources, you are tearing down your environment and all associated resources.  
{:shortdesc}

**Warning**: When you destroy resources, the action cannot be reversed. Destroying resources is not recommended for production environments, but might be useful for temporary environments such as testing or QA.

Before you destroy your resources, consider the following guidelines: 
* Ensure that traffic is not directed to your resources.
* Ensure that any data you might need is backed up. 


## Destroying resources with the GUI
{: #gui}

You can use the {{site.data.keyword.bpshort}} dashboard to spin up and tear down temporary environments.
{:shortdesc}

1. In the **{{site.data.keyword.bpshort}}** dashboard, select the **Environments** tab.

2. Click the row of the specific environment that you want to remove. 

3. In the options menu, select **Destroy resources** or **Delete environment**. Both the delete and destroy actions are not reversible. To determine which option to select, consider whether you have active resources.
  * Select **Destroy resources** if you want to stop and remove your active resources. It is recommended that you run a plan before destruction to confirm if the resources that are associated with the environment are okay to remove.
  * Select **Delete environment** if you want to remove the environment configuration from the {{site.data.keyword.bpshort}} service. This option is typically used if the environment is not deployed and does not have active resources. If you select this option with active resources, you can no longer use the {{site.data.keyword.bpshort}} service to track or deploy changes to your environment. The active resources need to be managed individually, from their service dashboards.
  
  Follow the on-screen prompts to confirm your choice. 


## Destroying resources with the CLI
{: #cli}

You can use the {{site.data.keyword.bpshort}} CLI to spin up and tear down temporary environments.
{:shortdesc}

1. Run the `destroy` command to tear down your environment and resources.

  ```
  bx schematics action destroy --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
2. Optional: Run the `delete` command if you want to remove your configuration from the service.

  ```
  bx schematics environment delete --id ENVIRONMENT_ID
  ```
  {: codeblock}


## Destroying resources with the API
{: #api}

You can use the {{site.data.keyword.bpshort}} API to spin up and tear down temporary environments.
{:shortdesc}

1. Run the `PUT v1/environments/<environment_ID>/destroy` call to destroy your resources.

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/destroy \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

2. Optional: Run the `DELETE v1/environments/<environment_ID>` call if you want to remove your configuration from the {{site.data.keyword.bpshort}} service.

  ```
  curl -X DELETE \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID> \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
