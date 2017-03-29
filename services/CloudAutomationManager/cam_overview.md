---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-22"

---
<!-- Copyright info and last updated date at top of file: REQUIRED
    The copyright and lastupdated info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be --- surrounded by 3 dashes ---
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    The value "lastupdated" must be followed by a machine date in quotes in the following format: "YYYY-MM-DD"
    The value for "years" must be indented 2 spaces under "copyright", followed by "lastupdated" which should start on its own non-indented line.

-->

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

<!-- About service_name_short topic: OPTIONAL
This is a template for an optional overview section if needed for your service. -->

# About Cloud Automation Manager
<!-- Insert your short service name into topic title above -->
{: #about_cam}
<!-- Provide an appropriate ID above -->


<!-- The short description section should include a sentence introducing the concepts. For example: -->
<!-- With the Cloud Automation Manager service, you can accelerate application delivery by automating application provisioning with cloud resource templates and blueprints.-->
IBM Cloud Automation Manager is a cloud management solution for deploying cloud infrastructure in multiple clouds with an optimized user experience. 
{:shortdesc}

<!-- <p>Cloud resource templates capture application infrastructure, cloud resources, Bluemix services, and their relationships, in a declarative text format that can be placed under version control.</p>

<p>Blueprints are cloud resource templates with additional software configuration controls that enable automated configuration of highly individualized, fit-for-purpose application environments with no programming required.</p>-->

<p>The Cloud Automation Manager service uses open source Terraform to manage and deliver cloud infrastructure as code. Cloud infrastructure delivered as code is reusable, able to be placed under version control, shared across distributed teams, and it can be used to easily replicate environments. The Cloud Automation Manager content library comes pre-populated with sample templates to help you get started quickly. Use the sample templates as is or customize them as needed.</p>

<p>With the Cloud Automation Manager service, you can provision cloud infrastructure and accelerate application delivery into IBM Cloud, Amazon EC2, and VMware vSphere cloud environments with a single user experience.</p>

<p>You can spend more time building applications and less time building environments when cloud infrastructure is delivered with automation. You are able to get started fast with pre-built infrastructure from the Cloud Automation Manager library.</p>

<p>The Cloud Automation Manager service supports the Bluemix resources that are supported by SoftLayer. For information about the SoftLayer resources, see <a href="https://github.com/softlayer/terraform-provider-softlayer/tree/master/docs/resources" target="_blank">https://github.com/softlayer/terraform-provider-softlayer/tree/master/docs/resources</a>. The only difference between the Bluemix resources and the SoftLayer resources is the actual name of the resource type, where `softlayer` is replaced by `bluemix_infrastructure`. For example the `softlayer_ssh_key` resource in SoftLayer is the `bluemix_infrastructure_ssh_key` resource in Bluemix. </p>

<!-- ## Concept title
{: #cam_concept} -->

<!-- If your service doc doesn't have a troubleshooting topic or section, you can add the following to your About: -->


<!--Add a heading and content for how to get help. (Support not available for experimental.) Use this template for experimental services:  -->
<!-- ## Getting help and support for Cloud Automation Manager
{: #gettinghelp}

If you have problems or questions when using Cloud Automation Manager, you can get help by searching for information or by asking questions through a forum. You can also open a support ticket.

* If you have technical questions about developing or deploying an app with Cloud Automation Manager, post your question on [Stack Overflow](http://stackoverflow.com/search?q=cloud-automation-manager+ibm-bluemix){:new_window} and tag your question with "ibm-bluemix" and "cloud-automation-manager".

* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers](https://developer.ibm.com/answers/?smartspace=bluemix){:new_window} forum. Include the  "cloud-automation-manager" and "bluemix" tags.

See [Getting help](https://www.{DomainName}/docs/support/index.html#getting-help) for more details about using the forums.

For information about opening an IBM support ticket, or about support levels and ticket severities, see [Contacting support](https://www.{DomainName}/docs/support/index.html#contacting-support). -->
