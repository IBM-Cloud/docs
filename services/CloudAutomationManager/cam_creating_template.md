---

copyright:
  years: 2016, 2017
lastupdated: "2017-06-19"

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
{:screen:.screen}
{:codeblock:.codeblock}

<!-- Additional task topic: OPTIONAL
This is the template for additional task topics that are needed beyond the basic tasks in the getting started index.md.  As needed, other task topics can be included, with titles such as "Configuring x", "Administering y", "Managing z", etc. This topic is a peer of the getting started index.md in the <servicename>.ditamap. This topic can have one level of children and they also can be referenced in <servicename>.ditamap -->

# Creating a template
<!-- for example, Uploading your data -->
{: #cam_creating_template}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Create your own template to deploy a customized instance to your environment.
{:shortdesc}

To create a template, follow these steps:

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. In the left-side navigation bar, click **Library > Templates**. The template library is displayed.
2. Click **Create Template**.
3. Enter a template name, a template description, and select the cloud provider type associated to the template.
4. Click **Create**.
5. In the **Template Metadata** tab, you can enter template details as a long description or a list of features.
6. In the **Template Source** tab, enter the template code or import it from a file or from a URL by clicking **Import Source File**. The template must be in HCL or JSON format.
7. In the **Parameters** tab, enter the template parameters. or import them from the template source or from a file by clicking **Import Parameters**.
8. Click **Save**.
9. If you want to deploy your template, click **Deploy Template** in the overflow menu in the upper-right side of the  template library. For more information about deploying a template, see [Deploying a template](/docs/services/CloudAutomationManager/cam_deploying_local.html).
