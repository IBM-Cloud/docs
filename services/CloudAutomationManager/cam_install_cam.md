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

# Installing Cloud Automation Manager 
<!-- for example, Uploading your data -->
{: #cam_install_cam}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Install Cloud Automation manager on the top of Kubernetes cluster for multi-node topology. For a single node topology, install Cloud Automation Manager on the same node where you have installed Kubernetes.
{:shortdesc}

Prerequisites to install Cloud Automation Manager:

- Kubernetes cluster must be running and available. For more information, see [Planning the installation](cam_planning.html) and [Installing Kubernetes](cam_install_k8.html).
- You must have sudo access on the master node.

Run the following steps to install Cloud Automation Manager:

1. Run the following steps to configure a NFS share for Cloud Automation Manager storage:  
    1. Log in to Kubernetes master. 
    2. In the extracted tarball file location, open the `lib/setenv` file in edit mode. 
    3. Provide values for the following NFS-specific environment variables:	
        * `nfs_server` - The IP address or the host name of the server where NFS is installed.
        * `nfs_share_logs` - The shared folder in NFS where the logs can be written.
        * `nfs_share_db` - The folder in NFS where the shared database can be stored. 
        * `mount_point` - The default value is `log/microservice`. You can change it according to your requirements.
    4. Verify whether the NFS mount is successful. 
    5. Create a file in the `/mnt/CAM_logs` directory to verify that the directory has write access.

2. In the master node, go to `IBM_CAM_1.1.0.0` folder and run the following command to install Cloud Automation Manager:
    ```
    bash CAM-install.sh
    ```	
    For multi-node topology, run `bash CAM-install.sh` script on all nodes. 
	
3. After the installation is successful, run either of the following commands to check the status of PODs: 
    ```
    kubectl get pods -n <namespace>
    ```
    The output lists POD records with their status and details. 
    
    or 
    ```
    watch kubectl get pods -n <namespace>
    ```
    As and when a POD status changes, the `watch` command refreshes the list automatically. 
    
    **Note:** POD creation takes some time to pull the images depending on the network connectivity. For more infomration on Kubernets POD, see [Pod Overview](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/){:new_window:}.
 
4. Configure LDAP and onboarding tenant and import starter packs. For the procedure, see [Configuring Cloud Automation Manager](/docs/services/CloudAutomationManager/cam_post_install.html).

5. To access the Cloud Automation Manager, enter the following URL in your browser:
    ```
    https://<CAM_master_node_IP_address>:30000/
    ```

