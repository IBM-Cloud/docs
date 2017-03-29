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
{:screen:.screen}
{:codeblock:.codeblock}

<!-- Additional task topic: OPTIONAL
This is the template for additional task topics that are needed beyond the basic tasks in the getting started index.md.  As needed, other task topics can be included, with titles such as "Configuring x", "Administering y", "Managing z", etc. This topic is a peer of the getting started index.md in the <servicename>.ditamap. This topic can have one level of children and they also can be referenced in <servicename>.ditamap -->

# Configuring a vSphere connection
<!-- for example, Uploading your data -->
{: #cam_creating_vsphere_connection}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

In order for Cloud Automation Manager to access your vSphere environment, you must provide the IP address or host name of the vCenter server and the user credentials to access it. 
{:shortdesc}

Because of current product limitations, note that:
- The IP address of the vCenter server must be a public IP address and not the internal IP address behind your VPN.
- When you create a template to be deployed to a vSphere cloud provider, ensure to specify the following parameter in the `provider` section:
 ```
 provider "vsphere" {
   allow_unverified_ssl = true
 }
 ```

For more information about vSphere, see the [VMware vSphere 6.5 Documentation Center](https://pubs.vmware.com/vsphere-65/index.jsp){:new_window}.

