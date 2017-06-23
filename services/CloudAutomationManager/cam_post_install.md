---

copyright:
  years: 2016, 2017
lastupdated: "2017-06-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Configuring Cloud Automation Manager
{: #cam_post_install}

After you install the Cloud Automation Manager, first ensure that all the containers are in a `running` state. Then, proceed with configuring LDAP and importing the starter packs. 
{:shortdesc}

## Configuring LDAP and onboarding tenant
{: #cam_ldap_configure}

You must configure LDAP to authenticate to the Cloud Automation Manager. After the configuration is complete, you can use the credentials in the LDAP directory to log in to the Cloud Automation Manager.

**Note:** You can configure only one tenant. All users have the same access privileges. Role-based access control is not implemented in this release of Cloud Automation Manager. 

Run the following steps on the master node to register the tenant and configure LDAP registry for authentication:

1. Run the following command:  
 ```
 cd IBM_CAM_1.1.0.0/scripts
 ``` 
2. Edit the `openLdap_config.env` sample file to specify the information corresponding to your LDAP server. See the following example of configuration file:  
    ```
    "LDAP_ID": "OpenLDAP",
    "LDAP_REALM": "OpenLDAPRealm",
    "LDAP_HOST": "ldap-service",
    "LDAP_PORT": "389",
    "LDAP_IGNORECASE": true,
    "LDAP_BASEDN": "dc=abc,dc=com",
    "LDAP_BINDDN": "cn=admin,dc=abc,dc=com",
    "LDAP_BINDPASSWORD": "Pwd0rd",
    "LDAP_TYPE": "Custom",
    "LDAP_USERFILTER": "(&(uid=%v)(objectClass=person))",
    "LDAP_GROUPFILTER": "(&(cn=%v)(objectClass=groupOfUniqueNames))",
    "LDAP_USERIDMAP": "*:uid",
    "LDAP_GROUPIDMAP": ":cn",
    "LDAP_GROUPMEMBERIDMAP": "groupOfUniqueNames:uniquemember"
    ```
    where:

    * `LDAP_ID` the unique ID of the LDAP directory.
    * `LDAP_REALM` is the unique name for the LDAP realm.
    * `LDAP_HOST` is the domain name or IP address of the LDAP server.
    * `LDAP_PORT` is the port number of the LDAP server. Default value: 389. 
    * `LDAP_IGNORECASE` is set to `true` to ignore the case during authentication check.
    * `LDAP_BASEDN` is the distinguished name of the search base.
    * `LDAP_BINDDN` is the user who is allowed to search the base DN. 
    * `LDAP_BINDPASSWORD` is the password of the user who is mentioned in the bind DN.
    * `LDAP_TYPE` is the type of LDAP server that you are connecting to. 
    * `LDAP_USERFILTER` is the filter clause for searching users. 
    * `LDAP_GROUPFILTER` is the filter clause for searching groups. 
    * `LDAP_USERIDMAP` is the filter to map a user name to an LDAP entry.
    * `LDAP_GROUPIDMAP` is the filter to map a group name to an LDAP entry.
    * `LDAP_GROUPMEMBERIDMAP` is the filter to map a user to a group.

3. Run the following command:  

    ```
    bash onboard_cam.sh <master_node_IP> <tenant_name> <openLdap_config_file>  
    ```

    where:  
    * `<master_node_IP>` is the Cloud Automation Manager host name or IP address.  
    * `<tenant name>` is the name of the tenant. This tenant is set as the default tenant. You cannot change the tenant configuration later. 
    * `<openLdap_config_file>` is the LDAP environment file. You can choose to set the environment variables instead of using the file. The variable names must be same as shown in the example file.

    If LDAP is successfully configured, the following message is displayed:
    ```
    Successfully onboarded the LDAP directory.
    ```

If LDAP configuration is unsuccessful, see [Troubleshooting Cloud Automation Manager](cam_local_troubleshoot.html#troubleshooting-cloud-automation-manager) for possible resolutions. 

### Updating the LDAP environment settings

After you configure LDAP and onboard the tenant, if you need to update the LDAP settings, first run the following command to clear the earlier LDAP settings:

```
bash offboard_cam.sh <master_node_IP>
```

You can then run the following onboarding command as described in [Configuring LDAP and onboarding tenant](cam_post_install.html#cam_ldap_configure):

```
bash onboard_cam.sh <master_node_IP> <tenant_name> <openLdap_config_file>
```

**Note:** The `offboard_cam.sh` script does not delete the tenant configuration. The script updates only the LDAP configuration.

## Importing starter pack templates  
{: #cam_starter_pack_configure}

You need internet connectivity to import the starter pack templates. 

If you do not have internet connectivity while you are configuring Cloud Automation Manager, you can download the starter pack templates later from [GitHub](https://github.com/IBM-CAMHub-Open/starterlibrary). For information about using the downloaded templates, see [Creating a template](cam_creating_template.html#creating-a-template) and [Deploying a template](cam_deploying_local.html#deploying-a-template).

To import the starter pack templates, run the following script on the master node:

```
./importTemplatesToCatalog.sh <master_node_IP> <user name> <user password>
```

   where:

   * `<master_node_IP>` is the Cloud Automation Manager host name or IP address.
   * `<user name>` is the Cloud Automation Manager user name.
   * `<user password>` is the user's password.

The script injects the entries in the template library. 

**Note:** The vSphere and NSXv templates are saved to your local directory. For information about using the templates, see [Creating a template](cam_creating_template.html#creating-a-template) and [Deploying a template](cam_deploying_local.html#deploying-a-template). 

For information about the available resources, see [VMware vSphere Provider and Resource Documentation](https://github.com/IBM-tfproviders/terraform-provider-vsphere/wiki/VMware-vSphere-Provider-and-Resource-Documentation) and [NSXv Terraform Provider and Resource Documentation](https://github.com/IBM-tfproviders/terraform-provider-nsxv/wiki/NSXv-Terraform-Provider-and-Resource-Documentation).

## What to do next

You can access the Cloud Automation Manager by entering the following URL in your browser:

```
https://<CAM_master_node_IP_address>:30000/
```

If you are unable to log in, see [Troubleshooting Cloud Automation Manager](cam_local_troubleshoot#cam_local_troubleshoot) for possible scenarios.

