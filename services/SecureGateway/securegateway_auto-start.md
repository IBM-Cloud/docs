---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-25"

---
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configuring Auto-start for the Client

## Linux
{: #linux}

If you have chosen to use you system's auto-start facility, use one of the methods below to start the client.  The configuration file that will be used by the client can be found at:

```
/etc/ibm/sgenvironment.conf
```
{: screen}

<b>Note:</b> Auto-start functionality is not available for Red Hat Linux 6.

This file includes the following important variables to set:

| Environment Variable | Description       |
| ------------- | ----------- |
| RESTART_CLIENT | Stop and Restart the client during install or upgrade (Yes or No) |
| GATEWAY_ID | Your gateway ID as created on the Secure Gateway for Bluemix UI |
| SECTOKEN | Security Token for this Gateway ID, if you choose to enforce security when creating it |
| ACL_FILE | Access Control List File you want to use to restrict on-premises access to resources |
| LOGLEVEL | The log level you want to set for your service (default is INFO) |
| USE_UI   | Set this to 'N' if you don't want to launch the client UI |
| UI_PORT  | The port on which you want to launch client UI on (default is 9003) |
| LANGUAGE | The language you want to have client logs in (default is en) |

<b>Note:</b> This file is only read if you are using your system's auto-start facility.  If you are running the client manually this file is ignored.

### Upstart
{: #upstart}

### Starting the client
{: #upstart-start}

If you using the upstart capability so that the Secure Gateway client runs automatically at system startup you have to check its configuration first (/etc/ibm/sgenvironment.conf).  Once you have configured the upstart service you can use the following command to start it:

```
sudo initctl start securegateway_client
```
{: pre}

To restart the service:

```
sudo initctl restart securegateway_client
```
{: pre}

### Stopping the client
{: #upstart-stop}

To stop the service, run the following command:

```
sudo initctl stop securegateway_client
```
{: pre}

### SystemD
{: #systemd}


### Starting the client
{: #systemd-start}

If you are using the systemD capability so that the Secure Gateway client runs automatically at system startup you may have to check its configuration first (/etc/ibm/sgenvironment.conf).  Once you have configured the upstart service you can use the following command to start it:

```
systemctl start securegateway_client
```
{: pre}

To restart the service:

```
systemctl restart securegateway_client
```
{: pre}

For status on the service:

```
systemctl status securegateway_client
```
{: pre}

### Stopping the client
{: #systemd-stop}

To stop the service, run the following command:

```
systemctl stop securegateway_client
```
{: pre}

### SystemV
{: #systemv}

System V is not setup during installation like the other auto-start facilities. Scripts are available in the installation directory /opt/ibm/securegateway/client/upstart, they are:

```
secgw.sh
securegateway_clientd
```
{: screen}

<b>Note:</b> This section will affect users of SuSE/SLES 11.

Optional: If you are running SuSE version 11 that uses systemV auto-start, scripts are provided that can be used to configure this process. Follow the below procedure:

```
cd /opt/ibm/securegateway/client/upstart/systemV
cp secgw.sh /usr/local/bin
chmod +x /usr/local/bin/secgw.sh
cp securegateway_clientd /usr/local/bin
chmod +x /usr/local/bin/securegateway_clientd
cd /etc/init.d
ln -s /usr/local/bin/securegateway_clientd
insserv securegateway_clientd
vi /etc/ibm/sgenvironment.conf
```
{: codeblock}

Once these steps have been executed, the YasT and systemV commands can be used to start/stop the daemon.

Return to [Getting Started - Adding a Client](./securegateway_client.html).

## Windows
{: #windows}

To alter the state of the windows service, open a command window with administrator privileges.

```
cd "<Installation_directory>\ibm\securegateway\client"
```
{: pre}

If the service is already running, the user can use the below command to stop it

```
windowsService.cmd uninstall
```
{: pre}

To start the service, use the following command

```
windowsService.cmd install
```
{: pre}

<b>Note:</b> The service will run based on the configurations stored in:

```
%Installation_directory%/ibm/securegateway/client/securegw_service.config
```
{: pre}

The application logs for windows service will be stored at:

```
%Installation_directory%/ibm/securegateway/client/logs/securegw_win_service.log
```
{:pre}

 The logs are rolled into a new file on a daily basis.

Return to [Getting Started - Adding a Client](./securegateway_client.html).
