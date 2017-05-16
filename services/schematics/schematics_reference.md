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

# {{site.data.keyword.bpshort}} CLI plug-in for the {{site.data.keyword.Bluemix_notm}} CLI
{: #cli}

Refer to the {{site.data.keyword.bpshort}} commands for the {{site.data.keyword.Bluemix}} CLI to manage your environments and perform other operations within {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Before you use the CLI commands:

* Log in to {{site.data.keyword.Bluemix_notm}} with `bx login [--sso]` to authenticate your session. Users with a federated ID need to use the `--sso` flag to generate a one-time passcode.

To view a list of commands, you can run `bx schematics help`.

<table id="manage_environments" summary="Manage your environments with the bx schematics environment commands.">
<caption>Table 1. Available commands to manage your environment. The commands follow the <code>bx schematics environment</code> syntax.
</caption>
 <thead>
 <th colspan="5">Managing your environment</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx schematics environment create](#environment-create)</td>
 <td>[bx schematics environment delete](#environment-delete)</td>
 <td>[bx schematics environment list](#environment-list)</td>
 <td>[bx schematics environment show](#environment-show)</td>
 <td>[bx schematics environment update](#environment-update)</td>
 </tr>
</tbody></table>
 
 <table id="update_resources" summary="Update the resources provisioned by your environment with the bx schematics action commands.">
 <caption>Table 2. Available commands to update resources in your environment. The commands follow the <code>bx schematics action</code> syntax.
 </caption>
  <thead>
  <th colspan="5">Updating your resources</th>
  </thead>
  <tbody>
  <td>[bx schematics action apply](#action-apply)</td>
  <td>[bx schematics action destroy](#action-destroy)</td>
  <td>[bx schematics action plan](#action-plan)</td>
  </tr></tbody></table>
  
  <table id="audit_environment" summary="Auditing activities that ran against your environment with the bx schematics activity commands.">
  <caption>Table 3. Available commands to audit the activities you ran against your environment. The commands follow the <code>bx schematics activity</code> syntax.
  </caption>
   <thead>
   <th colspan="5">Auditing your environment</th>
   </thead>
   <tbody>
   <td>[bx schematics activity list](#activity-list)</td>
   <td>[bx schematics activity log](#activity-log)</td>
   <td>[bx schematics activity planfile](#activity-planfile)</td>
   <td>[bx schematics activity show](#activity-show)</td>
   </tr></tbody></table>

## bx schematics environment create
{: #environment-create notoc}

Create an environment in {{site.data.keyword.Bluemix_notm}} from your configuration.

```
bx schematics environment create --file FILE_NAME [--json]
```
{: codeblock}

### Parameters

<dl>
<dt>--file FILE_NAME</dt>
<dd>The JSON file that is used to pass details about your environment.
<p>
<p>Example JSON with all available values:
<pre>{
    "description": "(Optional) Description of the environment",
    "frozen": false,
    "name": "Name of the environment",
    "sourceurl": "The GitHub URL that points to the Terraform configuration",
    "tags": ["(Optional) metadata_tag_1", "(Optional) metadata_tag_2"],
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
}</pre></dd>
<dt>--json</dt>
<dd>Print the output in JSON format.</dd>
</dl>

## bx schematics environment delete
{: #environment-delete notoc}

Remove your environment configuration from {{site.data.keyword.Bluemix_notm}}. This command is only recommended for environments without running resources. If you delete an environment with running resources, you need to manage each resource in the individual service dashboards.

```
bx schematics environment delete --id ENVIRONMENT_ID [--force]
```
{: codeblock}

### Parameters

<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>The unique identifier of the environment. You can retrieve this value by running <code>bx schematics environment list</code>.</dd>
<dt>--force</dt>
<dd>Force advancement of the command without a yes/no  confirmation.</dd>
</dl>

## bx schematics environment list
{: #environment-list notoc}

Retrieve a list of all existing environments in your {{site.data.keyword.Bluemix_notm}} account.

```
bx schematics environment list [--count VALUE] [--offset VALUE] [--json] 
```
{: codeblock}

### Parameters
<dl>
<dt>--count VALUE</dt>
<dd>The number of environments to limit in your return.</dd>
<dt>--offset VALUE</dt>
<dd>The offset in the list of environments.</dd>
<dt>--json</dt>
<dd>Print the output in JSON format.</dd>
</dl>

## bx schematics environment show
{: #environment-show notoc}

Retrieve details about an existing environment.

```
bx schematics environment show --id ENVIRONMENT_ID [--json]
```
{: codeblock}

### Parameters
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>The unique identifier of the environment. You can retrieve this value by running <code>bx schematics environment list</code>.</dd>
<dt>--json</dt>
<dd>Print the output in JSON format.</dd>
</dl>
  
## bx schematics environment update
{: #environment-update notoc}

Update the details about an existing environment, such as environment name or GitHub URL. To update the number of resources that are allocated in the environment, see [bx schematics action plan](#action-plan).

```
bx schematics environment update --id ENVIRONMENT_ID --file FILE_NAME [--json]
```
{: codeblock}

### Parameters
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>The unique identifier of the environment. You can retrieve this value by running <code>bx schematics environment list</code>.</dd>
<dt>--file FILE_NAME</dt>
<dd>The JSON file that is used to pass details about your environment. See [bx schematics environment create](#environment-create) for an example JSON snippet with allowed values.</dd>
<dt>--json</dt>
<dd>Print the output in JSON format.</dd>
</dl>

## bx schematics action apply
{: #action-apply notoc}

Deploy your environment configuration. The `apply` command scans and executes the configurations that are stored in your GitHub repository.

```
bx schematics action apply --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### Parameters
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>The unique identifier of the environment. You can retrieve this value by running <code>bx schematics environment list</code>.</dd>
<dt>--force</dt>
<dd>Force advancement of the command without a yes/no  confirmation.</dd>
<dt>--json</dt>
<dd>Print the apply output in JSON format.</dd>
</dl>

## bx schematics action destroy
{: #action-destroy notoc}

Destroy your environment and resources. The `destroy` command tears down your environment, including running resources. This action is typically used for only temporary environments, such as a QA environment, with the intention of standing the environment for a limited period. It is not recommended that you destroy production environments. The `destroy` action cannot be reversed and should be used with caution.

```
bx schematics action destroy --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### Parameters
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>The unique identifier of the environment. You can retrieve this value by running <code>bx schematics environment list</code>.</dd>
<dt>--force</dt>
<dd>Force advancement of the command without a yes/no  confirmation.</dd>
<dt>--json</dt>
<dd>Print the destroy output in JSON format.</dd>
</dl>
</dl>

## bx schematics action plan
{: #action-plan notoc}

Compare your environment configuration against the deployed configuration. The `plan` command scans the  configuration in your GitHub repository and runs a diff against the state file that is associated with your deployed environment. The plan output shows what resources would be added or removed if you deployed your environment configuration with the `apply` command. 

```
bx schematics action plan --id ENVIRONMENT_ID [--file FILE_NAME] [--json]
```
{: codeblock}

### Parameters
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>The unique identifier of the environment. You can retrieve this value by running <code>bx schematics environment list</code>.</dd>
<dt>--file FILE_NAME</dt>
<dd>The optional JSON file that is used to pass parameters for the plan action. You can pass the parameter <code>sourcesha</code> to reference a specific Git branch for the environment's Terraform configuration. The Git branch must be specified as a head reference such as <code>refs/heads/BRANCH_NAME</code>. If no parameter is specified, the default value is the head of the master branch, that is <code>refs/heads/master</code>.
<p>
<p>Example JSON snippet with value:
<pre>{
  "sourcesha": "refs/heads/BRANCH_NAME"
}</pre></dd>
<dt>--json</dt>
<dd>Print the plan output in JSON format.</dd>
</dl>

## bx schematics activity list
{: #activity-list notoc}

List the data from Terraform activities that ran against an environment.

```
bx schematics activity list --id ENVIRONMENT_ID [--count VALUE] [--offset VALUE] [--json]
```
{: codeblock}

### Parameters
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>The unique identifier of the environment. You can retrieve this value by running <code>bx schematics environment list</code>.</dd>
<dt>--count VALUE</dt>
<dd>The number of activities to return.</dd>
<dt>--offset VALUE</dt>
<dd>The offset in the list.</dd>
<dt>--json</dt>
<dd>Print the plan output in JSON format.</dd>
</dl>

## bx schematics activity log
{: #activity-log notoc}

View detailed activity logs for actions that are run against an environment.

```
bx schematics activity log --id ACTIVITY_ID
```
{: codeblock}

### Parameters
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>The flag to return details about a specific activity. You can retrieve a list of activity IDs per environment with the <code>bx schematics activity list --id ENVIRONMENT_ID</code> command.</dd>
</dl>

## bx schematics activity planfile
{: #activity-planfile notoc}

View plan files for an environment.

```
bx schematics activity planfile --id ACTIVITY_ID
```
{: codeblock}

### Parameters
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>The flag to return details about a specific activity. You can retrieve a list of activity IDs per environment with the <code>bx schematics activity list --id ENVIRONMENT_ID</code> command.</dd>
</dl>

## bx schematics activity show
{: #activity-show notoc}

Retrieve details about a specific activity that ran against an environment.

```
bx schematics activity show --id ACTIVITY_ID [--json]
```
{: codeblock}

### Parameters
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>The flag to return details about a specific activity. You can retrieve a list of activity IDs per environment with the <code>bx schematics activity list --id ENVIRONMENT_ID</code> command.</dd>
<dt>--json</dt>
<dd>Print the plan output in JSON format.</dd>
</dl>
