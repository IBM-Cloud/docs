---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-19"

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

# Installing Cloud Automation Manager Local
<!-- for example, Uploading your data -->
{: #cam_installing_local}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Install Kubernetes and then install Cloud Automation Manager on top of Kubernetes Cluster. 

{:shortdesc}

1. [Install Kubernetes](/docs/services/CloudAutomationManager/cam_install_k8.html).
2. [Install Cloud Automation Manager on Kubernetes cluster](/docs/services/CloudAutomationManager/cam_install_cam.html).

Before you install Kubernetes and Cloud Automation Manager, consider the following points:

- Network File System is encrypted out of the box and no encryption is provided by Cloud Automation Manager. 
- Firewall must be disabled for all master and worker nodes. If you enable the firewall, Cloud Automation Manager throws an error. 
- Upgrade, update, backup, and restore are not available in this beta release.
- Kubernetes is available along with the product, but Cloud Automation Manager does not provide support for Kubernetes. There are HTTP downloads from Kubernetes site. 
- Kubernetes require access to internet during deployment. 
- You must have root access for all master and worker nodes for Kubernetes deployment.
- You must have sudo access for Cloud Automation Manager deployment. 
- You must have a minimum of one master and two worker nodes. 
- You must have either a local or corporate LDAP. 
