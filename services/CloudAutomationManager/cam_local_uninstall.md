---

copyright:
  years: 2016, 2017
lastupdated: "2017-06-23"

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

# Uninstalling Cloud Automation Manager
<!-- for example, Uploading your data -->
{: #cam_local_uninstall}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

If required, you can uninstall IBM Cloud Automation Manager by using the steps described in this section.  
{:shortdesc}

1. As a sudo user, run the `CAM-delete.sh` command to delete the entire deployment from all master and worker nodes.

    **Note:** The command deletes replication controller, Services, Pods, persistent volume, persistent volume clam, and namespace.
    
2. Optionally, go to NFS server and manually remove the persistant MongoDB data and logs. The `CAM-delete.sh` command does not remove them as they may be needed for any future analysis. 

