---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-24"

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

# Cloud Automation Manager troubleshooting
{: #ts_cam}
<!-- Provide an appropriate ID above -->


<!-- This is the template for troubleshooting topics when using just a single short topic.  -->

<!-- The short description section should include the service long name and "Bluemix" for search optimization. Example short descriptions: -->

<!-- When you have problems using <service_name> on {{site.data.keyword.Bluemix_notm}}, consider these techniques for troubleshooting and getting help.
OR -->
Some known issues with Cloud Automation Manager in {{site.data.keyword.Bluemix_notm}} are documented.

{:shortdesc}

<!-- Add a headings and paragraphs about troubleshooting for your service, or a list of known issues and workarounds. -->

## Cloud Automation Manager known issues
{: #knownissues}

- If you deploy multiple instances with the same SSH key content to the SoftLayer environment, an issue occurs when trying to delete the instances.
- The template deployment to a vSphere cloud provider fails with the following error:
 ```
 Error setting up client: Post https://192.0.2.20/sdk: x509: cannot validate certificate for 192.0.2.20 because it doesn't contain any IP SANs
 ```
 To solve the problem, specify the following parameter in the `provider` section:
 ```
 provider "vsphere" {
   allow_unverified_ssl = true
 }
 ```

<!-- ## <service_short_name> troubleshooting techniques
{: #tstechniques} -->

<!-- Add a heading and content for how to get help and support. Use this template for beta and GA services:  -->

## Getting help and support for Cloud Automation Manager
{: #gettinghelp}

If you have problems or questions when using Cloud Automation Manager, you can get help by searching for information or by asking questions through a forum. You can also open a support ticket.

When using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.Bluemix_notm}} development teams.
<!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->
* If you have technical questions about developing or deploying an app with Cloud Automation Manager, post your question on [Stack Overflow](http://stackoverflow.com/search?q=cloud-automation-manager+ibm-bluemix){:new_window} and tag your question with "ibm-bluemix" and "cloud-automation-manager".
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers](https://developer.ibm.com/answers/?smartspace=bluemix){:new_window} forum. Include the "cloud-automation-manager" and "bluemix" tags.

See [Getting help](https://www.{DomainName}/docs/support/index.html#getting-help) for more details about using the forums.

For information about opening an IBM support ticket, or about support levels and ticket severities, see [Contacting support](https://www.{DomainName}/docs/support/index.html#contacting-support).
