---

copyright:
  years: 2015, 2016
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#System Access
{: #system_access}


Methods of creating and managing a service instance are discussed in this section, along with various ways to access and setup access to your systems.
{: shortdesc}


## REST API Usage in WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}
{: #restapi_usage}

Instances in WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} are created, provisioned, managed, and deleted in one of the following ways:

* From the {{site.data.keyword.Bluemix_notm}} Catalog and Service Dashboard in the {{site.data.keyword.Bluemix_notm}} UI.
* From the creation of an application or script that uses RESTful APIs.

Through use of Swagger 2.0 compliant REST APIs, clients have access to the same function as provided through the portal and dashboard. For more information about supported REST APIs and resources, see the WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} [REST API Documentation](https://wasaas-broker.ng.bluemix.net/wasaas-broker/api#/){: new_window}. For sample code that demonstrates usage of the REST APIs, download the Git hosted WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} [REST API Samples](https://github.com/IBM-Bluemix/WebSphere-for-Bluemix-API-Usage){: new_window}.

**Note:** After you create a service instance, depending on the Tee-Shirt size that is created, your service might not be immediately ready for use. It is recommended that you query the **Status** field of the JSON returned to determine the current state of the service instance.

**Note:** The **apiEndpoint** URL referenced in the [REST API Samples](https://github.com/IBM-Bluemix/WebSphere-for-Bluemix-API-Usage){: new_window} points to the US South Region. If you are using other regions, ensure that your application references the appropriate **apiEndpoint**.

*Table 1. API Endpoint URLs for Rest API Implementation*

| **Region name** | **Geographic location** | **Region prefix** | **API Endpoint URL** |       
|:-------------:|:----------:|:--------------:|:-------------:|
| US South | Dallas, TX, US | ng | https://wasaas-broker.ng.bluemix.net/wasaas-broker/api  |
| United Kingdom | London, England | eu-gb | https://wasaas-broker.eu-gb.bluemix.net/wasaas-broker/api  |
| Sydney | Sydney, Australia | au-syd | https://wasaas-broker.au-syd.bluemix.net/wasaas-broker/api  |
| Frankfurt | Frankfurt, Germany | eu-de | https://wasaas-broker.eu-de.bluemix.net/wasaas-broker/api  |



## Service Dashboard
{: #service_dashboard}

After you create your service instance, you will be taken to the service dashboard. You can always get back to the service dashboard by clicking the service icon from your organization dashboard.
From the service dashboard you can access:

* A link to this documentation
* A link to download the required OpenVPN configuration files
* The ability to start and stop the virtual machine. The VM is initially started
* The host name
* The admin user and admin password
* A private SSH key
* The WebSphere® admin user and admin password
* The Admin Center and Admin Console URLS

**Note**: Due to a specific amount of compute, memory, and I/O resources, clients are charged for accumulated VMs in the STOPPED state at a reduced rate of 5%. Clients are managed to a fixed number of STOPPED instances with no more than 10 IP addresses or 64 GB of memory.


## Setting up openVPN for WebSphere Application Server in Bluemix instances
{: #setup_openvpn}

OpenVPN is required for access to any WebSphere Application Server in Bluemix virtual machine. It must be installed and running with administrator privileges.

### Use the following instructions to set up openVPN in Windows:

1. From the [openVPN Windows download](http://swupdate.openvpn.org/community/releases/) link, download
  * [openvpn-install-2.3.4-I001-x86_64.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-x86_64.exe){: new_window} for 64-bit, or
  * [openvpn-install-2.3.4-I001-i686.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-i686.exe){: new_window} for 32-bit.
2. Ensure you [Run as a Windows Administrator](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} and openVPN is installed.
3. Download the VPN configuration files from the OpenVPN download link of the WebSphere Application Server in Bluemix instance in the service dashboard. Extract all four files in the compressed file to the **{OpenVPN home}\config** directory. For example:

  <pre>  
    C:\Program Files\OpenVPN\Config
  </pre>
  {: codeblock}

4. Start the openVPN client program "OpenVPN GUI". Ensure that you select [Run as a Windows Administrator](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} to start the program. If you do not, you might not be able to connect.

### Use the following instructions to set up openVPN in Linux:
1. To install openVPN, follow the [instructions](https://openvpn.net/index.php/access-server/docs/admin-guides/182-how-to-connect-to-access-server-with-linux-clients.html){: new_window}.
  * If you need to manually download and install the RPM Package Manager, go to [openVPN unix/linux download](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){: new_window}. You might need assistance from your Linux administrator.
3. Download the VPN configuration files from the OpenVPN download link of the WebSphere Application Server in Bluemix instance in the service dashboard. Extract the files into the directory from which you plan to start the openVPN client. You need all four files in the same directory.
3. Start the openVPN client program. Open a terminal window and go to the directory that contains the config files. Run the following command as root:

  <pre>
      $ openvpn --config vt-wasaas-wasaas.ovpn
  </pre>
  {: codeblock}  

### Use the following instructions to configure openVPN in Mac:
1. One method is to install [Tunnelblick](https://tunnelblick.net/){: new_window}, an open source software product.
2. Extract the VPN configuration files from the WebSphere service. Tunnelblick prompts for your admin password for Mac and adds the config to the set of VPNs you can use to connect.
3. Connect to the VPN network and then you can access your virtual machine. After your first access, Tunnelblick caches the configuration and you can connect from [Tunnelblick](https://tunnelblick.net/){: new_window}. You can put an icon on the top menu bar for easy access.


## Using SSH to access WebSphere Application Server in Bluemix VMs
{: #using_ssh}

These instructions assume that you are using OpenSSH as your client. OpenSSH is normally available on Linux or in Cygwin running on Windows. It also can be installed to run from a Windows command prompt.

To verify installation of OpenSSH, enter the command:
  ```
      $ ssh -V
  ```
  {: codeblock}

The following message is an example of the response:
  ```
      OpenSSH_6.6p1, OpenSSL 1.0.1g 7 Apr 2014
  ```
  {: codeblock}

Use the following instructions to set up SSH access to your WebSphere Application Server in Bluemix VMs

1. Review the warning message that appears the first time you connect, "The authenticity of host x.x.x.x cannot be established." This message is normal. When prompted, select yes. The public key is now installed on your VM for the user virtuser.
2. Log in to virtuser by using the private key. For best results, use the private key authentication method.
3. Copy the contents of the private key into a file.
4. Run the command:

  <pre>
    $ ssh virtuser@169.53.246.xxx -i /path/privateKeyFileName
  </pre>
  {: codeblock}

5. Gain full sysadmin authority by switching virtuser to root by using the command:

  <pre>
    $ sudo su root
  </pre>
  {: codeblock}

6. If you experience problems when you access the system with the private ssh key, use the root password that is provided. Log in as root by running the command that follows and provide the password.

 <pre>
    $ ssh root@169.53.246.x
  </pre>
  {: codeblock}

7. Whether you access the system with the private ssh key or the root password, immediately change the root password.
8. To simplify your SSH commands, create a file that is named "config" in the %HOME%/.ssh directory. For example:

  <pre>
   Host VM1
      Hostname 169.53.246.xxx
      User virtuser
      IdentityFile /path/privateKeyFileName
  </pre>
  {: codeblock}

9. Run "ssh VM1" to be connected as virtuser.

## System paths
{: #system_paths}

* The Liberty Profile commands can be issued from */opt/IBM/WebSphere/Liberty/bin*.
* The Liberty Profile server profile location is */opt/IBM/WebSphere/Profiles/Liberty/servers/server1*.
* The Traditional WebSphere Application Server commands can be issued from */opt/IBM/WebSphere/AppServer/bin*.
* The Traditional WebSphere Application Server profile location for the server is */opt/IBM/WebSphere/Profiles/DefaultAppSrv01/servers/server1*.

## Using the Admin Center and Admin Console links
{: #console_links}

When you click the link to the Admin Center or the Admin Console, you might receive an *Untrusted Connection* warning. The exact message text varies by browser, as do the exact steps to bypass or eliminate the warning.

Since you are using links that are provided by {{site.data.keyword.IBM}}, you can safely ignore the warning and connect. If your browser offers to store a security exception, doing so is the easiest way to prevent the warning in the future.

Another option is to export the incoming signer certificate and then import it into your browser as a trusted root certificate. This option would require you to make an entry in your *hosts* file that maps the VM's IP address to the certificate issuer's common name. This name is in the following format: wl<pureapplication.ibmcloud.com. If you now use the host name instead of the IP address in the URL, you can connect cleanly. You then must access the Admin Center or Admin Console by using that host name instead of the IP address in the URL.

Lastly, customers often install their own root certificates for applications they make external. For more information, refer to the [WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/tsec_securecomm.html?cp=SSEQTP_8.5.5%2F1-11-2-6&lang=en){: new_window} or [Liberty Core](http://www.ibm.com/support/knowledgecenter/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_comm.html?lang=en){: new_window} IBM Knowledge Center.

## Firewall Ports
{: #firewall_ports}

You might find it necessary to open ports on the firewall to allow access to applications and databases.
  * On each WebSphere Application Server in Bluemix node, you find a script openFirewallPorts.sh in the WAS_HOME/virtual/bin directory.
  * On each Liberty collective host, you find a script openFirewallPorts.sh in the WAS_HOME/virtual/bin directory.

Usage:
  ```
      $ openFirewallPorts.sh -ports <PORT>:<PROTOCOL>,... -persist true|false
  ```
  {: codeblock}

* PORT is a port number
* PROTOCOL is either TCP or UDP
* -persist is either true or false

To specify multiple ports, separate them with a comma ","

**Note**: The sport and dport of the port that is opened is open in the INPUT and OUTPUT sections of the firewall. You must run this script as root by using sudo. You can also modify iptables directly.

## Configuring the web server
{: #configure_webserver}

When you provision a cell or a collective, you receive a preconfigured environment. Specifically, for a Traditional Network Deployment cell, you receive the following environment:

* A Deployment Manager that is collocated with the IBM HTTP Server for development and testing purposes.

* A custom node federated to the Deployment Manager.

* The Deployment Manager, the IHS Server, and the Node Agent all initially provisioned to the STARTED state.

If you require the web server to handle all user requests, then you might need to generate and propagate the plug-in after you deploy your application.

**Avoid trouble:** Before you generate and propagate the plug-in, ensure that the following prerequisite tasks are complete:

* In your local Windows, Linux or MAC environment, ensure that [openVPN](systemAccess.html#setup_openvpn) is configured, started and you are connected to the appropriate region.

* From the WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Service Dashboard, click **Open the admin console** and login with wsadmin and the Admin Password that is provided in the Service Dashboard.

* From the Admin Console, create an application server (for example, ***server1***), because the Deployment Manager is federated with an empty custom node.

* Start the server that you created.

* During application installation, ensure that the modules of your application are mapped to the server you just started and to the web server (for example, ***webserver1***).

The following high-level steps assume that the prerequisite tasks are complete:

1. From the Admin Console, generate the plug-in from the Environment option:
   1. Choose Environment > Update global web server plug-in configuration
   2. Click **OK** or **Overwrite to generate a new plug-in configuration file**
2. From the Deployment Manager, copy the plug-in to the web server configuration:

  ```
   cp /opt/IBM/WebSphere/Profiles/DefaultDmgr01/config/cells/plugin-cfg.xml /opt/IBM/WebSphere/Plugins/config/webserver1/plugin-cfg.xml
  ```
  {: codeblock}
3. Edit **httpd.conf** in **IHS_HOME/conf** (for example, */opt/IBM/WebSphere/HTTPServer/conf*) and ensure that the following two lines exist:

    ```
    LoadModule was_ap22_module /opt/IBM/WebSphere/Plugins/bin/64bits/mod_was_ap22_http.so
    WebSpherePluginConfig /opt/IBM/WebSphere/Plugins/config/webserver1/plugin-cfg.xml
    ```
    {: codeblock}  
4. Open the ports with these two commands:

  ```
   export serverPorts=2810:TCP,2810:UDP,8880:TCP,8880:UDP,9101:TCP,9101:UDP,9061:TCP,9061:UDP,9080:TCP,9080:UDP,9354:TCP,9354:UDP,9044:TCP,9044:UDP,9443:TCP,9443:UDP,5060:TCP,5060:UDP,5061:TCP,5061:UDP,11005:TCP,11005:UDP,11007:TCP,11007:UDP,9633:TCP,9633:UDP,7276:TCP,7276:UDP,7286:TCP,7286:UDP,5558:TCP,5558:UDP,5578:TCP,5578:UDP

   sudo /opt/IBM/WebSphere/AppServer/virtual/bin/openFirewallPorts.sh -ports $serverPorts -persist true
  ```
    {: codeblock}
5. Stop and start the web server with the following two commands:
    ```
    sudo /opt/IBM/WebSphere/HTTPServer/bin/apachectl -k stop
    sudo /opt/IBM/WebSphere/HTTPServer/bin/apachectl -k start
    ```
    {: codeblock}
8. Access your application through the plug-in:
  ```
   http://169.53.246.xxx/contextRoot/
  ```
  {: codeblock}

**NOTE:** The steps that are provided represent one path of many when you're attempting to configure a web server. If further assistance is needed, see the [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/search/configure%20web%20server?scope=SSAW57_9.0.0){: new_window}.

**NOTE:** If you cannot access your application, you are likely facing a port access issue on your firewall. Therefore, you might need to restart any of the following servers: the application server, the node agent, the web server, and the deployment manager. Additionally, it is possible that you might need to access the WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Service Dashboard and restart each virtual machine.
