---

copyright:
  years: 2016, 2017
lastupdated: "2017-06-22"

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

# Planning the installation
<!-- for example, Uploading your data -->
{: #cam_planning_installation}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Before you start the installation, it is important to understand the installation flow. The installation is a three step process wherein you install Kubernetes, install Cloud Automation Manager on top of Kubernetes Cluster, and finally configure LDAP and import the starter packs.
{:shortdesc}

1. [Install Kubernetes](/docs/services/CloudAutomationManager/cam_install_k8.html)
2. [Install Cloud Automation Manager on Kubernetes cluster](cam_install_cam.html)
3. [Configure LDAP and import the starter packs](cam_post_install.html)

**Note:** Upgrade, backup, and restore procedures are not applicable in this beta release.
 
 ## Choosing the deployment topology
This beta version is tested on two topologies:
* Single node having both the capabilties of master and worker 

  It is not recommended for production environment or for heavy load. You can use this only for proof of concept, demos, and so on. 
* Multi-node Kubernetes cluster topology having one master and minimum one worker node 

  For improved performance, use one master and two worker nodes. 

## Checking the hardware prerequisites
{: #cam_hw_prereq}
You must have the following hardware prerequisites for master node: 
 - 8 GB RAM. 
  
   If it is a single node topology, use 16 GB RAM. 
 - 4 cores of CPU
 - Minimum 80 GB disk space   
 
   If it is a single node topology, use 250 GB. 

You must have the following hardware prerequisites for worker node: 
- 8 GB RAM 
  
  For both single node topology and single worker node in a cluster, use 16 GB RAM
- 4 cores of CPU
- Minimum 150 GB disk space
  
  For both single node topology and single worker node in a cluster, use 250 GB. 

## Checking the software prerequisites

Prerequisites for Kubernetes installation:
* Operating system: Ubuntu 16.04.x LTS.

  If you are bringing your own Kubernets, then ensure its version is V1.6.4-00 with Flannel.

<strong>Note:</strong> The Cloud Automation Manager does not provide support for Kubernetes. 

Prerequisites for Cloud Automation Manager installation:
* Kubernetes must be installed before Cloud Automation Manager
* `nfs-common` package must be installed on all nodes.

## Checking the network prerequisites
{: #cam_network_prereq}

* Internet connectivity must be available during Kubernetes deployment. 

## Checking authentication and security prerequisites
{: #cam_security_prereq}

**Prerequisites for Kubernetes:**

* You must have root access for all master and worker nodes for Kubernetes deployment.

**Prerequisites for Cloud Automation Manager:**

* You must have LDAP to authenticate to Cloud Automation Manager. 
* You must have sudo access for Cloud Automation Manager deployment.
* Firewall is disabled for all master and worker nodes. This Cloud Automation Manager beta release might not work properly if firewall is enabled.
* You can configure Cloud Automation Manager with only one LDAP directory at any point in time.
* You can configure Cloud Automation Manager with only one tenant. The tenant is defined during the onboarding process. For more information about the onboarding process, see [Configuring Cloud Automation Manager](cam_post_install.html#cam_post_install). 
* Role-based access control is not implemented in this release of Cloud Automation Manager. All users have the same access privileges. 


## Checking the storage prerequisites
* Two shared Network File System (NFS)

  25 GB for logs and 15 GB for database with read and write access. 
  
  In the `/etc/exports file`, set the NFS shares to `no_root_squash` so that even non-root users are able to access the NFS shared directories.
  An example of a `etc/exports` file: 
  ```
  /export *(rw,fsid=0,insecure,no_subtree_check,async)
  /export/CAM_logs *(rw,nohide,insecure,no_subtree_check,async,no_root_squash)
  /export/CAM_db *(rw,nohide,insecure,no_subtree_check,async,no_root_squash)
  ```
  <strong>Note:</strong> Work with your storage administrator or system admin to configure your NFS before you proceed with deployment.
  
  NFS must be encrypted if you need logs and database security, however, no encryption is provided by Cloud Automation Manager. 
  Ensure that you have your own NFS storage. If you place NFS outside the kubernetes cluster, then the data remains safe even in the event of any Kubernets cluster issues.
