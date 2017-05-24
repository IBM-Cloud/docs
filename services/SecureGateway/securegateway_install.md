---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-25"

---
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Installing the Client

## Docker
{: #docker}

Docker is a third-party platform that provides a container approach to installing applications quickly and easily with little or no configuration necessary. The {{site.data.keyword.SecureGateway}} service provides a Docker image to be used after the Docker utility is installed on your workstation.  To install Docker see the Docker install web site and follow the instructions for your system.

### Installing and Updating the Client
{: #docker-install}

Installing and updating the {{site.data.keyword.SecureGateway}} Client Docker image both use the same command:

```
docker pull ibmcom/secure-gateway-client
```
{: pre}

### Starting an interactive client session
{: #docker-run}

To run the Docker container for IBM {{site.data.keyword.SecureGateway}}, issue the following command:

```
docker run -it ibmcom/secure-gateway-client <gateway ID> -t <security token>
```
{: pre}

Normally it takes two parameters, your {{site.data.keyword.SecureGateway}} gateway ID and the gateway's security token, both of which are available via the {{site.data.keyword.SecureGateway}} Dashboard.

### Supported Docker Commands
{: #docker-commands}

The {{site.data.keyword.SecureGateway}} Client only supports the `pull` and `run` commands for manipulating the container.

Return to [Getting Started - Adding a Client](./securegateway_client.html).

## Mac OS X
{: #mac}

### Requirements for running on Mac OS X
{: #mac-requirements}

The following pre-requisites are required prior to running the client on Mac OS X.
 1. Install Xcode development tools, it is required by some of the node modules on this platform.

### Mac OS X Installation Procedure
{: #mac-install}

You may require administrative privileges to perform this installation, depending on your system's security setup.

 1. Mount the DMG image that was downloaded from the {{site.data.keyword.SecureGateway}} UI, normally by 'double-clicking' it.
 2. A new 'finder' window should appear.  This window should contain an Applications "shortcut" icon, drag and drop the application onto the shortcut.  If not, 'double-click' the mounted volume and drag and drop the application icon to the Applications icon in the Finder sidebar.

### Starting an interactive client session
{: #mac-run}

To start the client, run the `secgw.command` file located in the default installation location: `/Applications/ibm/`.

Return to [Getting Started - Adding a Client](./securegateway_client.html).

## Linux
{: #linux}

The installation includes the {{site.data.keyword.SecureGatewayfull}} client as well as a secure version of IBM's nodejs package.  Both are installed under the /opt/ibm directory on the system.  The installer will create or update the following:

| Directory | Filename | Description          |
| ------------- | ------------- | ----------- |
| /etc/ibm | sgenvironment.conf | configuration file for upstart |
| /etc/ibm | passwd | creates user: secgwadmin:x:501:501::/home/secgwadmin:/bin/bash |
| /etc/ibm | group | creates group: secgwadmin:x:501: |
| /etc/init | securegateway_client.conf | upstart file |
| /opt/ibm | node-v&lt;version&gt;-linux-x64 | IBM's Node JS installation |
| /opt/ibm | securegateway | {{site.data.keyword.SecureGateway}} client installation |
| /usr/local/bin | node | symlink created for IBM's node executable |
| /usr/local/bin | npm | symlink created for IBM's npm executable |
| /var/log/securegateway | client_console.log | log file created when running client as an auto-start process |

You will require root or administrative privileges to perform this installation.

### Ubuntu/PowerPC Installation
{: #debian-install}

 1. Install the {{site.data.keyword.SecureGateway}} client. For example, if you are using a Debian package, issue the following command.

    ```
    sudo dpkg -i <secure-gateway-debian-package>
    ```
    {: pre}

 2. When the client installer starts, you are prompted for the following information.

    <b>Auto-start process Yes/No</b>
        If this is an upgrade or reinstall, you must choose whether you want the existing client to be stopped while
        the installation process is running. Choose Y/y to stop the existing client. Otherwise, the client package
        is upgraded without restarting the client, which means that you can wait for an appropriate Software Update
        window to perform a restart. If you choose N/n, the installation continues and you must restart the client
        manually.

    <b>Gateway ID</b>
        Set the gateway ID for the client. The gateway ID is defined when you create a {{site.data.keyword.SecureGateway}} service. If the
        client fails to connect, you can change your selection by editing the .conf file.

    <b>Security token</b>
        If the gateway ID is enabled to check for a security token, you must provide it now. If the gateway ID does
        not require a security token, leave this blank.

    <b>Logging level</b>
        The default setting is INFO. Other valid values are TRACE, DEBUG, and ERROR.

    <b>Access Control List</b>
        Enter the absolute path of the file name containing the access control list on what has access to your
        on-premises resources. For more information, see the README.md file in /opt/ibm/securegateway or Access control list.

    <b>Client UI</b>
        Choose if you want to use client UI. If yes, user can change the port for the UI. Default value is 9003.

    <b>Note:</b> You do not have to answer any of the prompts, all will take the defined default or be left blank in the sgenvironment.conf file. This allows the installation process to run without user interaction.

    <b>Note:</b> The sgenvironment.conf is read every time that you start or restart the client using the system's upstart process. You can edit the /etc/ibm/sgenvironment.conf file at any time to make changes to your configuration and restart the client to pick up those changes.

    <b>Note:</b> The language of the {{site.data.keyword.SecureGateway}} client service logs can be changed by changing the `LANGUAGE` parameter in the /etc/ibm/sgenvironment.conf file. The service logs will change to selected language after service restart.

 3. If you restarted the client, to make sure that the client is running properly, issue the following command:

    ```
    cat /var/log/securegateway/client_console.log
    ```
    {: pre}

 4. If you want to edit the configuration file, to make sure that the configuration file is updated correctly, issue the following command:

    ```
    sudo vi /etc/ibm/sgenvironment.conf
    ```
    {: pre}

 5. To check the status of your client installation, issue the following command:

    ```
    sudo dpkg --status ibm-securegateway-client
    ```
    {: pre}

An example of the output is returned:

```
Package: ibm-securegateway-client
Status: install ok installed
Priority: extra
Section: IBM/net
Maintainer: cloudoe-dev@webconf.ibm.com
Architecture: amd64
Source: ibm-securegateway+securegateway-client
Version: 1.7.0
Description: IBM Secure Gateway Client for Bluemix
IBM Secure Gateway client package for Bluemix, supports secure connections to on-premises connections.
Homepage: https://ng.bluemix.net/
License: http://www.ibm.com/software/sla/sladb.nsf/lilookup/986C7686F22D4D3585257E13004EA6CB?OpenDocument
```
{: screen}

### RedHat/SuSE Installation
{: #rpm-install}

1. Install the {{site.data.keyword.SecureGateway}} client. For example, if you are using an RPM package, issue the following command:

   ```
   rpm -ivhf <secure-gateway-rpm-package>
   ```
   {: pre}

   <b>Note:</b> On Red Hat Version 7 and above you will have to use the '--force' option as well.

   The client installer starts and installs the client, it will create a sgenvironment.conf file in /etc/ibm.

2. Optional: If you want to use the system's upstart process you must edit this file and provide the following for the client to start correctly. See [Using Upstart](#using-systemv) for more information on editing this configuration file.

3. If you started the client using upstart, check the log file to make sure it is running correctly.

   ```
   cat /var/log/securegateway/client_console.log
   ```
   {: pre}

4. To check the status of your client installation, issue the following command:

   ```
   rpm -q ibm-securegateway-client
   ```
   {: pre}

### Starting an interactive client session
{: #linux-run}

To start the client, run the following commands:

```
cd /opt/ibm/securegateway/client
node lib/secgwclient.js <gateway ID> -t <security token>
```
{: codeblock}

Normally it takes two parameters, a {{site.data.keyword.SecureGateway}} gateway ID and the gateway's security token, both of which are available via the {{site.data.keyword.SecureGateway}} Dashboard.

Return to [Getting Started - Adding a Client](./securegateway_client.html).

## Windows
{: #windows}

### Installing the Client
{: #windows-install}

You may require administrative privileges to perform this installation, depending on your system's security setup.

 1. Copy the EXE installer file to your system.  An MD5 sum is also provided which you can use to check the integrity of the installation package.

 2. Install it by either double clicking on it and answering the prompts, or running the executable from the command prompt.

 3. The user will be prompted to choose the installation directory of their choice. The default location is the Program Files (x86) directory.

 4. The user will be prompted to select the language in which they want to launch the Command Line Interface. If not language is selected, it will be defaulted to English.

 5. The user will be prompted to install the client as a windows service. If the user chooses to do so, the client will run in background as a windows service with the configurations user provide in the subsequent dialog. The status of service can be checked in the service page of Control Panel. The service name is "IBM Bluemix Secure Gateway Service".

 6. The installer identifies if there is an existing installation on the machine. If it is detected, the user is asked if they want to use the existing configurations, else the user has the option to enter new configurations. Details like gateway ids, security tokens, acl files and log level for each gateway can be provided here. If the user has chosen to run the client as a windows service the client will launch with the configurations provided. If the user has not chosen to launch the client as a windows service, the configurations will be stored for further use. In either case, the configurations are stored in %Installation_directory%/ibm/securegateway/client/securegw_service.config.

 7. Starting version 1.5.0, the client comes with a fully functional client UI. You can configure it from the installer itself. The user can provide the password and the port number (default is 9003) from which the client UI will be launched.

 If the user chooses to launch the client with connection to multiple gateways, please take care while providing the configuration values. The gateway ids needs to be separated by spaces. The security tokens, acl files and log levels should to be delimited by --. If you don't want to provide any of these three values for a particular gateway, please use 'none'.

 <b>Note:</b>Please ensure that there are no residual white spaces.

 <b>Note:</b>Please note that the acl files should be placed in %Installation_directory%/ibm/securegateway/client directory or relative to that path.

### Starting an interactive client session
{: #windows-run}

To start the client, open a command prompt with administrative privileges and run the following commands:

```
cd "<Installation_directory>\ibm\securegateway\client"
secgw.cmd
```
{: codeblock}

Alternatively, navigate to `<Installation_directory>\ibm\securegateway\client` and double-click `secgw.cmd`.

<b>Note:</b>You can choose to use the configurations stored in `<Installation_directory>\ibm\securegateway\client\securegw_service.config` file or provide the details interactively.

Return to [Getting Started - Adding a Client](./securegateway_client.html).

## DataPower
{: #datapower}

DataPower has an embedded version of the {{site.data.keyword.SecureGateway}} Client.  Depending on the DataPower version, you may have a different version of the {{site.data.keyword.SecureGateway}} Client.  Be aware of any applicable [DataPower Client Limitations](./securegateway_interaction.html#limits-datapower).

DataPower Version | {{site.data.keyword.SecureGateway}} Client Version
-- | --
Pre-7.5.1.0 | Client v1.2.1
7.5.1.0 - Pre-7.6.0.0 | Client v1.4.2
7.6.0.0+ | Client v1.6.1

### Starting a client session
{: #datapower-run}

1. Log into the DataPower web GUI
2. Navigate to Objects -> Cloud -> Secure Gateway Client or search for Secure Gateway Client
3. Click `Add` to configure a new client connection
4. Provide a Name, the Gateway ID, and the Security Token (if applicable) and then apply the changes.

Return to [Getting Started - Adding a Client](./securegateway_client.html).
