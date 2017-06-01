---

copyright:
  years: 2017
lastupdated: "2017-05-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.bpfull_notm}} (Beta)
{: #gettingstarted}

{{site.data.keyword.bplong}} is an automation tool that you can use to define and deploy your cloud infrastructure as a single unit, and reuse those cloud resource definitions across any number of environments.
{:shortdesc}

{{site.data.keyword.bpshort}} uses Terraform, by HashiCorp, to codify infrastructure. Components of your infrastructure are broken down into individual resources, which can be anything from physical hardware to user accounts. By abstracting high-level and low-level resources, you can treat your infrastructure like you treat your software, as code. 

When you work with {{site.data.keyword.bpshort}}, you write configurations for your environment in declarative syntax. You state how you want to your environment to look, such as having 10 {{site.data.keyword.virtualmachinesshort}} in production. The service compares your configuration to what Terraform previously created and adds or removes resources as necessary.

{{site.data.keyword.bpshort}} is a collaborative DevOps tool that provides a single source of truth for infrastructure. You can store environment configurations in source control, giving your team the ability to conduct code reviews, version their infrastructure, track the changes through commit history, and revert changes more easily.

{{site.data.keyword.bpshort}} is automatically available to all users in your {{site.data.keyword.Bluemix_notm}} account.


## Creating a configuration
{: #configuration}

When you create a configuration, you are codifying the cloud resources that make up your environment.
{:shortdesc}


If you want to try out a sample configuration with {{site.data.keyword.bpshort}}, complete the following steps. In the sample, you can provision an SSH key to use in {{site.data.keyword.BluSoftlayer_notm}}. 

**Note:** The sample configuration requires a {{site.data.keyword.BluSoftlayer_notm}} account. See the [linking your {{site.data.keyword.Bluemix_notm}} and SoftLayer accounts doc](../../pricing/linking_accounts.html#unifyingaccounts) if you have an existing account, or you can [sign up for an account](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).

1. Generate an SSH key pair locally.
  ```
  ssh-keygen -t rsa
  ```
  {:codeblock}

2. Fork the sample configuration in <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key" target="_blank">GitHub <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>. 

  The following examples show different types of blocks that are in the sample configuration. You can see the full configuration in the `main.tf` file of the GitHub repository.
  
  * The provider block sets up the {{site.data.keyword.IBM_notm}} Cloud provider and login credentials.

    ```
    provider "ibmcloud" {
      bluemix_api_key = "${var.bxapikey}"
      softlayer_username = "${var.slusername}"
      softlayer_api_key = "${var.slapikey}"
      softlayer_account_number = "${var.slaccountnum}"
    }
    ```
    {:screen}
  
  * The resource block defines a component of your infrastructure, which in this sample is an SSH key.
  
    ```
    resource "ibmcloud_infra_ssh_key" "ssh_key" {
      label = "${var.key_label}"
      notes = "${var.key_note}"
      public_key = "${var.public_key}"
    }
    ```
    {:screen}
  
  * The variable block defines your variables, which you can enter in the {{site.data.keyword.bpshort}} GUI for this sample.
  
    ```
    variable bxapikey {
      description = "Your Bluemix API key."
    }
    ```
    {:screen}
  
  * The output block defines what is displayed in the Terraform output after the configuration is used to create your environment and the resource (SSH key) is created.
  
    ```
    output "ssh_key_id" {
      value = "${ibmcloud_infra_ssh_key.ssh_key.id}"
    }
    ```
    {:screen}
  
You can now create an environment from your configuration. 

{:codeblock}

## Creating an environment
{: #environment}

When you create an environment, you point the service to your configuration so that the service can extract your latest code changes. 
{:shortdesc}

Using the sample configuration, complete the following steps to create an environment.

1. In the menu, select **Services** and then **{{site.data.keyword.bpshort}}**. You are taken to the {{site.data.keyword.bpshort}} dashboard.

2. In the left navigation menu, select **Environments** and click **Create Environment** to describe properties about your configuration. Creating an environment defines how {{site.data.keyword.bpshort}} provisions and updates cloud resources, but does not create resources yet.

3. Enter details about your environment. The sample configuration requires the values that are listed in the following table.

  <table summary="The values that are required so that you can use the sample configuration as the source of your environment.">
  <caption>Table 1. The values that are required so that you can use the sample configuration as the source of your environment.
  </caption>
  <thead>
  <th colspan="1">Setting</th>
  <th colspan="1">Description</th>
  </thead>
  <tbody>
  <tr>
  <td>Source control URL</td>
  <td>Enter the GitHub URL where you forked the sample configuration.</td>
  </tr>
  <tr>
  <td>Name</td>
  <td>Enter a unique name to assign to your environment.</td>
  </tr>
  <td>Terraform version</td>
  <td>Enter the version of Terraform to ensure that a compatible version of Terraform is run against your environment. For the sample configuration, use version <code>0.9.3</code>.</td>
  </tr>
  <tr>
  <td>Variables</td>
  <td>You can define variables in the service or override the environment variables that are in your <code>.tf</code> files. You can mask sensitive variables when you click the lock icon. Masking variables prevents other users from seeing the hidden values in the environment details page. 
  <p>
  <p>Add the following variables and values to work with the sample configuration:
  <ul>
  <li><code>bxapikey</code> - Enter your {{site.data.keyword.Bluemix_notm}} API key. If you do not have an existing API key, you can generate the value by running <code>bluemix iam api-key-create NAME</code>.
  <li><code>slusername</code> - Enter your {{site.data.keyword.BluSoftlayer_notm}} user name.
  <li><code>slapikey</code> - Enter your {{site.data.keyword.BluSoftlayer_notm}} API key. You can retrieve the value from the [{{site.data.keyword.slportal}}](https://control.bluemix.net), in the <strong>API Access Information</strong> section.
  <li><code>slaccountnum</code> - Enter your {{site.data.keyword.BluSoftlayer_notm}} account number. This value is only required if you have multiple accounts that are associated with your ID.
  <li><code>datacenter</code> - Enter the data center that you want to deploy the SSH key resource to. See the <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key/blob/master/README.md" target="_blank">readme file <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> for a full list of available values.</li>
  <li><code>public_key</code> - Enter the public SSH key. To copy the public key to your clipboard, you can run the <code>pbcopy < ~/.ssh/id_rsa.pub</code> command.
  <li><code>key_label</code> - Identify the key with a unique name.
  <li><code>key_note</code> - Optional: Add descriptive text about the SSH key.</ul>
  </td>
  </tr></tbody></table>

4. When you have finished filling out the environment's details, click **Create**. The newly created environment is displayed. 
5. To see a preview of what resources are provisioned or removed when you deploy your environment, click **Plan**. 
6. View the plan log to inspect the output for any errors. 
7. When you are ready to deploy your environment, click **Apply**. You can monitor the apply log to see whether the key deployed successfully. A successful deployment shows the following line towards the end of the output:

  ```
  Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
  ```
  {: screen}

  You can also view the SSH key in the [{{site.data.keyword.slportal}}](https://control.bluemix.net/devices/sshkeys).
8. Optional: To remove the SSH key and remove the environment from {{site.data.keyword.Bluemix_notm}}, select **Destroy resources** from the actions menu.

### What's next
{: #next}

* To find out more about programmatically deploying your environments, [check out the CLI or API](schematics_deploying.html).
* To create your own configurations from scratch, check out the <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">{{site.data.keyword.IBM_notm}} Cloud resources <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>. {{site.data.keyword.IBM_notm}} Cloud resources are available as a Terraform plug-in provider.
