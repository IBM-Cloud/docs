---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#System Access
{: #system_access}
These topics include various ways to access and setup access to your systems.
{: shortdesc}

## Service Dashboard
{: #service_dashboard}

After you create your service instance, you will be taken to the service dashboard. You can always get back to the service dashboard by clicking the service icon from your organization dashboard.
From the service dashboard you can access:

*  A link to this documentation
*  A link to download the required OpenVPN configuration files.
*  The ability to start and stop the virtual machine. The VM is initially started.
*  The Hostname.
*  The admin user and admin password.
*  A private SSH key.
*  The WebSphere® admin user and admin password.
*  The Admin Center and Admin Console URLS.


## Setting up openVPN for WebSphere Application Server for Bluemix instances
{: #setup_openvpn}

OpenVPN is required for access to any WebSphere Application Server on Bluemix virtual machine. You must have it installed and it must be running with administrator privileges.  

### Use the following instructions to set up openVPN in Windows:

1. From the [openVPN Windows download](http://swupdate.openvpn.org/community/releases/) link, download
  * [openvpn-install-2.3.4-I001-x86_64.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-x86_64.exe){: new_window} for 64-bit, or
  * [openvpn-install-2.3.4-I001-i686.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-i686.exe){: new_window} for 32-bit.
2. Ensure you [Run as a Windows Administrator](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} and install openVPN.
3. Download he VPN configuration files from the OpenVPN download link of the WebSphere Application Server for Bluemix instance in the service dashboard. Extract all four files in the compressed file to the **{OpenVPN home}\config** directory.   For example:

  <pre>  
    C:\Program Files\OpenVPN\Config
  </pre>
  {: codeblock}
  
4. Start the openVPN client program "OpenVPN GUI". Ensure that you select [Run as a Windows Administrator](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} to start the program. If you do not, you might not be able to connect.

### Use the following instructions to set up openVPN in Linux:
1. To install openVPN follow these [instructions](https://openvpn.net/index.php/access-server/docs/admin-guides/182-how-to-connect-to-access-server-with-linux-clients.html){: new_window}.
  * If you need to manually download and install the RPM Package Manager, go to [openVPN unix/linux download](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){: new_window}. You might need assistance from your Linux administrator.
3. Download the VPN configuration files from the OpenVPN download link of the WebSphere Application Server for Bluemix instance in the service dashboard. Extract the files into the directory from which you plan to start the openVPN client. You need all four files in the same directory.
3. Start the openVPN client program.  Open a terminal window and go to the directory that contains the config files. Run the following command as root:
  
  <pre>
      $ openvpn --config vt-wasaas-wasaas.ovpn
  </pre>
  {: codeblock}  

### Use the following instructions to setup openVPN in Mac:
1. One method is to install [Tunnelblick](https://tunnelblick.net/){: new_window}, an open source software product.
2. Extract the VPN configuration files from the WebSphere service. Tunnelblick prompts for your admin password for Mac and adds the config to the set of VPNs you can use to connect.
3. Connect to the VPN network and then you can access your virtual machine. After your first access, Tunnelblick caches the configuration and you can connect from [Tunnelblick](https://tunnelblick.net/){: new_window}. You can put an icon on the top menu bar for easy access.


## Using SSH to access WebSphere Application Server for Bluemix VMs
{: #using_ssh}

These instructions assume that you are using OpenSSH as your client. OpenSSH is normally available on Linux or in Cygwin running on Windows. It also can be installed to run from a Windows command prompt.

To verify installation of OpenSSH, enter the command:
  ```
      $ ssh -V
  ```
  {: codeblock}

Your response should be similar to:
  ```
      OpenSSH_6.6p1, OpenSSL 1.0.1g 7 Apr 2014
  ```
  {: codeblock}

Use the following instructions to set up SSH access to your WebSphere Application Server for Bluemix VMs

1. Review the warning message that appears the first time you connect, "The authenticity of host x.x.x.x cannot be established." This is normal. When prompted, select yes. The public key is now installed on your VM for the user virtuser.
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
* The traditional WebSphere Application Server commands can be issued from */opt/IBM/WebSphere/AppServer/bin*.
* The traditional WebSphere Application Server profile location for the server is  */opt/IBM/WebSphere/Profiles/DefaultAppSrv01/servers/server1*.

## Using the Admin Center and Admin Console links
{: #console_links}

When you click on the link to the Admin Center or the Admin Console, you might receive an *Untrusted Connection* warning. The exact message text varies by browser, as do the exact steps to bypass or eliminate the warning.

Since you are using links provided by {{site.data.keyword.IBM}}, you can safely ignore the warning and connect. If your browser offers to store a security exception, doing so is the easiest way to prevent the warning in the future.

Another option is to export the incoming signer certificate and then import it into your browser as a trusted root certificate. This option would require you to make an entry in your *hosts* file that maps the VM's IP address to the certificate issuer's common name. This name is in the following format: wl<pureapplication.ibmcloud.com. If you now use the host name instead of the IP address in the URL, you should connect cleanly. You then have to access the Admin Center or Admin Console using that host name instead of the IP address in the URL.

Lastly, customers often install their own root certificates for applications they make external. For more information, refer to the [WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/tsec_securecomm.html?cp=SSEQTP_8.5.5%2F1-11-2-6&lang=en){: new_window} or [Liberty Core](http://www.ibm.com/support/knowledgecenter/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_comm.html?lang=en){: new_window} Knowledge Center.

## Firewall Ports
{: #firewall_ports}

You might find it necessary to open ports on the firewall to allow access to applications and databases.
  * On each WebSphere Application Server for Bluemix node, you find a script openFirewallPorts.sh in the WAS_HOME/virtual/bin directory.
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

**Note**: Both the sport and dport of the port opened is opened in the INPUT and OUTPUT sections of the firewall. You must run this script as root by using sudo. You can also modify iptables directly.
