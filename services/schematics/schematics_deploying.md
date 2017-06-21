---

copyright:
  years: 2017
lastupdated: "2017-06-08"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Deploying resources to your environments
{: #deploying}

With {{site.data.keyword.bplong}}, you can deploy your latest code changes directly from your source code. When you deploy your environment, you are deploying the resources the are defined by your configuration files. You can then manage the provisioning, orchestrations, and lifecycle of the environment from within {{site.data.keyword.bpshort}}.
{:shortdesc}

## Deploying to your environments with the GUI
{: #gui}

If you prefer a graphical view to deploy your environment, you can use the {{site.data.keyword.bpshort}} dashboard.
{:shortdesc}


### Prerequisite
{: #gui-prereq}

* Store a Terraform configuration in source control. Configurations can be written in HashiCorp Configuration Language (HCL) or JSON syntax. See the <a href="https://www.terraform.io/docs/configuration/index.html">Terraform configuration docs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> for HCL syntax and guidelines on how to write configurations. See the <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">{{site.data.keyword.IBM_notm}} Cloud provider <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> for available resources.

After you store your configuration:

1. In the **{{site.data.keyword.bpshort}}** dashboard, select **Environments**.

2. Click **Create Environment** to add an environment, or select the row of an existing environment that you want to deploy.

3. Click **Plan** to preview what resources are provisioned when you deploy your environment. When you run plan, {{site.data.keyword.bpshort}} extracts the variables in your environment details and the latest version of your configuration from source control. The plan output displays how the configuration compares to what is deployed according to your Terraform state file. Your environment is locked from more changes until the plan is applied to your environment or canceled. 

4. View the log in the **Recent Activity** section to inspect the plan output. The plan output shows if errors exist and which resources the service is planning to create, change, or destroy.

5. When you are ready to launch your plan, click **Apply**. You can monitor the activity log to ensure that the plan is successfully applied in the latest run. 


## Deploying to your environments with the CLI
{: #cli}

You can use the {{site.data.keyword.bpshort}} plug-in for the {{site.data.keyword.Bluemix_notm}} CLI to deploy updates to your environment. 
{:shortdesc}

### Prerequisites
{: #cli-prereq}

* Store a Terraform configuration in source control.
* If you haven't already, install the {{site.data.keyword.Bluemix_notm}} CLI for your operating system from the [{{site.data.keyword.Bluemix_notm}} CLI repository](http://clis.ng.bluemix.net/ui/home.html).

After you log in to the {{site.data.keyword.Bluemix_notm}} CLI:

1. Install the {{site.data.keyword.bpshort}} CLI plug-in by running the following command.
  
  ```
  bx plugin install schematics -r Bluemix
  ```
  {: codeblock}

  The {{site.data.keyword.bpshort}} plug-in appears under `bx plugin list` if the installation is successful. 

2. Create an environment from your configuration. When you create your environment, you are pointing the service to your source control so that it can extract the latest code.

  a. Create a JSON file to pass metadata that describes your environment, including the GitHub repo where your Terraform files are stored.
  
  The following JSON sample shows all available parameters.
  
  ```
  {
    "description": "(Optional) Description of the environment",
    "frozen": false,
    "name": "Name of the environment",
    "sourceurl": "The GitHub URL that points to the Terraform configuration",
    "tags": [
      "(Optional) tag_1",
      "(Optional) tag_2"
    ],
    "terraformversion": "0.9",
    "variablestore": [
      {
        "name": "(Optional) variable_1",
        "secure": false,
        "value": "Visible value"
      },
      {
        "name": "(Optional) variable_2_secret",
        "secure": true,
        "value": "Secured value"
      }
    ]
  }
  ```
  {: codeblock}
  
  b. Run the `create` command to add the environment to {{site.data.keyword.bpshort}}.
  
  ```
  bx schematics environment create --file FILE_NAME
  ```
  {: codeblock}
  
  <table summary="Description of the create command.">
  <caption>Table 1. Description of the create command.
  </caption>
  <thead>
  <th colspan="1">Parameter</th>
  <th colspan="1">Description</th>
  </thead>
  <tbody>
  <tr>
  <td>--file FILE_NAME</td>
  <td>The JSON file that you created in the previous step to describe your environment.
  </td>
  </tbody></table>
  
  Note the `ID` value that is returned. The `ID` is a unique identifier that is assigned to your environment and is used in subsequent commands.
  
3. Run the `plan` command to preview how your environment would change. The plan command shows which resources would change and by what quantity compared to what is deployed, but the changes do not take effect until you run the `apply` command.
  
  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="Description of the plan command.">
  <caption>Table 2. Description of the plan command.
  </caption>
  <thead>
  <th colspan="1">Parameter</th>
  <th colspan="1">Description</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>The specific environment that you want to run an execution plan for. You can run <code>bx schematics list</code> if you need to retrieve the value for environment ID.
  </td>
  </tbody></table>
  
  An `activity_id` is assigned to the plan and recorded in the activity log. 

4. Retrieve the activity log to view the Terraform plan output.

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  <table summary="Description of the log command.">
  <caption>Table 3. Description of the log command.
  </caption>
  <thead>
  <th colspan="1">Parameter</th>
  <th colspan="1">Description</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ACTIVITY_ID</td>
  <td>The specific activity that you want to view the log for. You can run <code>bx schematics activity list --id ENVIRONMENT_ID</code> if you need to retrieve the value for activity ID.
  </td>
  </tbody></table>
  
5. Run the `apply` command to deploy resources to your environment.
  
  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="Description of the apply command.">
  <caption>Table 4. Description of the apply command.
  </caption>
  <thead>
  <th colspan="1">Parameter</th>
  <th colspan="1">Description</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>The specific environment that you want to deploy updates to. You can run <code>bx schematics list</code> if you need to retrieve the value for environment ID.
  </td>
  </tbody></table>
  
6. Monitor the apply output to ensure that the deployment is successful. 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  A successful deployment returns the following line towards the end of the output.
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
  
## Deploying to your environments with the API
{: #api}

You can programmatically deploy your environment with the {{site.data.keyword.bpshort}} API. 
{:shortdesc}

Calls to the <a href="https://us-south.schematics.bluemix.net/swagger-api/">{{site.data.keyword.bpshort}} API <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> point to the following base endpoint:

```
https://us-south.schematics.bluemix.net
```
{: codeblock}

### Prerequisite
{: #api-prereq}

* Store a Terraform configuration in source control.

Complete the following steps to deploy resources to your environment:

1. Generate an IAM OAuth token to use in your authentication header. The command outputs a UAA token and an IAM token.
  
  ```
  bx iam oauth-tokens
  ```
  {: codeblock}
  
  Example output:
  ```
  IAM token:  Bearer eyJraWQ...
  ```
  {: screen}
    
  The `Bearer eyJraWQ...` output is a truncated example of the IAM token. Include the full token in the header of your API calls.
  
2. Create an environment by running a `POST v1/environments` call.

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
    -d '{
    "description": "(Optional) Description of the environment",
    "frozen": false,
    "name": "Name of the environment",
    "sourceurl": "The GitHub URL that points to the Terraform configuration",
    "tags": [
      "(Optional) metadata_tag_1",
      "(Optional) metadata_tag_2"
    ],
    "terraformversion": "0.9",
    "variablestore": [{
        "name": "(Optional) variable_1",
        "secure": false,
        "value": "Visible value"
    },
    {
        "name": "(Optional) variable_2_secret",
        "secure": true,
        "value": "Secured value"
    }]
  }'
  ```
  {: codeblock}
    
  A successful response returns the following output.
  ```
  {
    "id": "Environment ID",
    "name": "Environment name",
    "description": "Description of the environment",
    "account": "{{site.data.keyword.Bluemix_notm}} account GUID",
    "owner": "The IBMid of the user who created the environment",
    "creationtime": "YYYY-MM-DDTHH:MM:SSZ",
    "status": "CREATED",
    "frozen": false,
    "sourceurl": "The GitHub URL that points to the configuration",
    "statefile": "The reference to the Terraform state file",
    "terraformversion": "0.9",
    "tags": [
      "metadata_tag_1",
      "metadata_tag_2"
    ],
    "variablestore": [
      {
        "name": "(Optional) variable_1",
        "value": "Visible value"
      }
    ]
  }
  ```
  {: screen}
    
  Note the `id` value that is returned. The `id` is a unique identifier that is assigned to your environment and is used in subsequent calls.
  
3. Run the `POST v1/environments/<environment_ID>/plan` call to preview which resources will be deployed to your environment when you apply your configuration. Plans extract the environment configurations in the master branch of your repository.
  
  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
  A successful response returns an `activityid`. The activity ID value is needed to view logs, such as plan and apply output.
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

4. Run the `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` call to view the plan output.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

5. Deploy your environment by running the `PUT v1/environments/<environment_ID>/apply/` call.
  
  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
6. Monitor the deployment by running the `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` call to view the apply output.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

  A successful deployment returns the following line towards the end of the output.
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
