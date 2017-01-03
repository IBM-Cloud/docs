---

copyright:
  years: 2016
lastupdated: "2016-12-20"

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
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- This template is for getting started with a Bluemix service. It is a task template intended to document productive use of the service. It is not intended for discovery and conceptual information.  -->




<!-- The name of this file should remain index.md.
Please delete out content examples and coding that you are not using for your service. -->

# Getting started with Cloud Automation Manager
<!-- Insert your short service name into topic title above -->
{: #CAMgettingstarted}
<!-- Provide an appropriate ID above -->

<!-- Short description: REQUIRED
The short description section should include one to two sentences describing why a developer would want to use your service in an app. This should be conversational style. For search engine optimization, include the service long name and "Bluemix". Keep the {: shortdesc} after the first paragraph so that the framework renders it properly.

Examples: -->


Use IBM Cloud Automation Manager to create and edit templates that implement common business patterns and to deploy them in your cloud environment. After they are deployed, you can manage and access the instances from the Cloud Automation Manager service.
{:shortdesc}

<!-- If overview content is required, do not include it here. Put it in a separate "## About" section below the task section. -->

<!-- Task section: REQUIRED
The task section includes steps to integrate the service into the app.  
- With task-based, technical information, reduce the conversational style in favor of succinct and direct instructions.
- DO include the basic, most-common-use scenario steps to use the service or integrate it into the app.
- DO NOT include steps to add the service from the Bluemix catalog; we assume that the user already took steps in the UI to add the service.
- DO include code snippets in all languages that can be copied, as well as VCAP service info.  
- For additional tasks like configuring, managing, etc., add a task section (## Gerund_task_title) below the task section or "About" section if used. Use a task title such as "Configuring x", "Administering y", "Managing z". -->

<!-- You can include an optional prerequisites paragraph for any prerequisites to be met before integrating the service. For example: -->

Before you can use the Cloud Automation Manager service, you must upgrade and unify your Bluemix and SoftLayer accounts. For more information, see [Upgrading and unifying Bluemix and SoftLayer billing accounts](https://console.{DomainName}/docs/admin/softlayerlink.html){:new_window}.

Note that you can deploy templates to SoftLayer infrastructures only within the region, organization, and space to which you are logged in.

<!-- Include a sentence to briefly introduce the steps. Examples: -->

After you add the Cloud Automation Manager service from the Bluemix Experimental Services catalog, to get started with the service, create and deploy a template in your Bluemix environment. 
Complete the following steps:

<!-- Use ordered list markup for the step section. For code examples:
- use three backticks ahead of and after the example (```)
- For copyable code snippet, multi-line, include {: codeblock} following the last set of backticks. A copy button will display in framework in output.
- For copyable command, single line, include {: pre} following the last set of backticks. When displayed, it will show "$" at the beginning of the command example and a copy button, but the copy button will include just the command example.
- For non-copyable output snippet, include {: screen} following the last set of backticks.
 -->

1. Click **Templates**.
2. Click **Bring your own template** if you want to create and deploy a template from scratch or click one of the pre-built templates.
3. Read the information about the template that you selected and click **Deploy an Instance**.
3. In the Deploy Instance pane, provide the required information as the instance name and click **Next**. 
4. If you are deploying a template from scratch, enter the template code in the **Template Code Editor** or upload the template code from a file or from a URL by clicking **Upload**. The template must be in HCL or JSON format depending on what you specified in the previous Deploy Instance pane.

 If you are deploying a pre-built template, you do not need to change the template code displayed in the **Template Code Editor**.
4. Click **Next**.
5. Enter the required deployment parameters and click **Deploy**. The instance window is displayed.
6. In the instance window, you can see the instance status, the instance information, and the related resource details. You can view or donwload the instance logs and you can also access the template from which the instance was deployed.

 When the deployment is completed, for each related resource, you can access the console (if existing) and eventually perform the actions listed by clicking in the **ACTIONS** column.
 
 **Note:** To access the KVM console in the SoftLayer Customer Portal, you must follow the procedure described in [Access the KVM Console](https://knowledgelayer.softlayer.com/procedure/access-kvm-console){:new_window}.

<!-- Related links section: REQUIRED.
Related links display in the upper right of the getting started page.
Ensure that you retain the lowercase anchor IDs (eg. {: #rellinks}) as shown in this template. These are used as IDs during transform and the doc framework keys off the IDs for display.
The headings coded here are not actually used. The doc framework provides the correct headings.
Also ensure that the related links stay in position at the end of this file or the doc framework will not display them properly.
Use {:new_window} for external links to open a new window.-->
<!-- Please delete all comments within the related links section to avoid breaking the build. Thanks. -->

<!--  Related Links
{: #rellinks} -->

<!-- ## Tutorials and Samples
{: #samples}
<!-- Recommended external links to your top three devWorks articles and sample applications. 	Link text should be: <sample_name> sample or developerworks: <article_name>. To confirm the available articles for your service, go to http://www.ibm.com/developerworks/views/global/libraryview.jsp?show_abstract=falsecontentarea_by=All+Zonesproduct_by=-1topic_by=BlueMixindustry_by=-1type_by=All+Typesibm-search=Search and select your service from the product drop-down menu -->
<!-- * [link text](URL){:new_window} -->

<!-- ## SDK
{: #sdk}
<!-- Links to SDK download and SDK Developer Guide -->
<!-- * [link text](URL){:new_window} -->

<!-- ## API Reference
{: #api}
<!-- External links to the landing page of each generated doc for the APIs that are supported by your service. Use only the type of API as the link text (Java, JavaScript, REST, Objective-C) -->
<!-- * [link text](URL){:new_window} -->

<!-- ## Compatible Runtimes
{: #buildpacks}
<!-- MAY BE REMOVING THIS: Peer links to the Getting Started page of each runtime that is supported by your service. Use only the name of the runtime as the link text (Node.js, Liberty for Java, Ruby on Rails, Ruby Sinatra) -->
<!-- * [link text](URL) -->

<!-- ## Related Links
{: #general}
<!-- Include a link to your full product documentation, pricing sheet, IBM Bluemix prerequisites -->
<!-- NOTE: Remove these comments when using this template. Otherwise the comment will break the build! Thanks. -->
<!-- * [link text](URL){:new_window}
* [link text](URL)
* [link text](URL) -->
