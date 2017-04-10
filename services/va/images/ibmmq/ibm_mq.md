---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-07"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# IBM MQ Bluemix Container Image
{: #ibm_mq}

The ibm-mq image is supplied for {{site.data.keyword.containershort}}. It includes {{site.data.keyword.IBM}} MQ Advanced for Developers (non-warranted). 

{:shortdesc}


## How it works
{: #ibm_mq_how}

{{site.data.keyword.IBM_notm}} MQ Advanced for Developers contains everything you need to start developing your own messaging solutions and {{site.data.keyword.IBM_notm}} MQ applications. 

To develop messaging solutions and {{site.data.keyword.IBM_notm}} MQ applications in {{site.data.keyword.Bluemix_notm}}, you can deploy the ibm-mq Docker image in the {{site.data.keyword.containershort}}. Then, you can create and run queue managers, and use the web UI or a terminal to configure them to meet your messaging solution or application requirements.

**Note:** You can use the ibm-mq image for development and unit test only. You can also use the image to explore the product, learn from tutorials, and evaluate the contribution that {{site.data.keyword.IBM_notm}} MQ can make to your organization.

## What is included
{: #ibm_mq_what}

This ibm-mq image contains the software package for {{site.data.keyword.IBM_notm}} MQ Advanced for Developers Version 9.0.x, which is a full-function version of the product that you can use for development and unit test. You can download this version at no charge and you are free to use it within the terms of the license.

{{site.data.keyword.IBM_notm}} MQ Advanced for Developers is available on Windows 64-bit operating systems and Linux on x86-64 operating systems. All product prerequisites are included in the download package. For more information, see [IBM MQ Downloads ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](http://www-03.ibm.com/software/products/lv/ibm-mq-advanced-for-developers){: new_window}

For information about the features that are included in {{site.data.keyword.IBM_notm}} MQ Advanced for Developers, see [IBM MQ ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSFKSJ_9.0.0/com.ibm.mq.helphome.v90.doc/WelcomePagev9r0.htm){: new_window}



## Usage Restrictions
{: #ibm_mq_usage}

The following table shows the restrictions that apply to the free usage of the ibm-mq image in {{site.data.keyword.Bluemix_notm}}:

| Environment	| Free Usage Restrictions |
|-------------|-------------------------|
| Development	| Unlimited free usage of the ibm-mq image to create single containers for development. |
| Test | Unlimited free usage of the ibm-mq image to create single containers for unit testing. Check the [License information](getstarted.html#ibm_mq_license ) for more information about what testing is permitted. |
| Production | The {{site.data.keyword.IBM_notm}} MQ Advanced for Developer license does not allow it’s use for production. |

**Note:** The pricing for the ibm-mq image is independent of the pricing for the containers that you use in {{site.data.keyword.Bluemix_notm}}.


## License information
{: #ibm_mq_license}

Information about licenses:

*	The Dockerfiles and associated scripts are licensed under the [Apache License 2.0 ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](http://www.apache.org/licenses/LICENSE-2.0.html){: new_window}.
* [License information for {{site.data.keyword.IBM_notm}} MQ Advanced for Developers ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](http://www-03.ibm.com/software/sla/sladb.nsf/displaylis/973FA648A5DE42948525806E004CC757?OpenDocument){: new_window}.

**Note:** The license does not allow further distribution. The terms for {{site.data.keyword.IBM_notm}} MQ in the image restrict usage for development and unit testing.


## Getting Started
{: #ibm_mq_get_started}

Complete the following steps to run and manage {{site.data.keyword.IBM_notm}} MQ in a container that runs on {{site.data.keyword.Bluemix_notm}}:

1. [Provision a container that is based on the ibm-mq image](ibm_mq.html#ibm_mq_provision)

    **Note:** The container is tied to the running state of the Queue Manager inside it. If you stop the Queue Manager using the console or command line, the container will stop shortly after. 

2. Manage {{site.data.keyword.IBM_notm}} MQ resources that are running in a container. You can do it graphically from the IBM MQ web console or programmatically by using commands from a terminal. 

    1. Choose any of the following options to manage {{site.data.keyword.IBM_notm}} MQ resources in the container:
    
        *	Launch the {{site.data.keyword.IBM_notm}} MQ web console and manage {{site.data.keyword.IBM_notm}} MQ graphically. For more information, see [Launch the IBM MQ web console](ibm_mq.html#ibm_mq_webui).
        *	From a terminal, use the Docker CLI. For more information, see [Setting up a terminal to use the Docker CLI](ibm_mq.html#ibm_mq_docker_commands).
        * From a terminal, use the IBM Bluemix Container Service CLI. For more information, see [Setting up a terminal to use the IBM Bluemix Container Service CLI](ibm_mq.html#ibm_mq_containers_cli)
        
    2. Configure the {{site.data.keyword.IBM_notm}} MQ Queue Manager that runs in the container. 

        * To manage the Queue Manager through the command line, use the *runmqsc* program. Run the following command: `runmqsc QM_Name` where *QM_Name* is the name of your Queue Manager. For more information, see [Managing your container through the command line](ibm_mq.html#ibm_mq_access).
    
        * To manage the Queue Manager grahically, use the web UI.
        
    3. Follow instructions on the [IBM MQ Knowledge Center ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/en/SSFKSJ_9.0.0/com.ibm.mq.helphome.v90.doc/WelcomePagev9r0.htm){: new_window} to create Message Queues on your Queue Manager and put or get messages to them.
    
        For example, run in `runmqsc` the following command to create a new Local Queue: `DEFINE QLOCAL('MY.Q')`, where *MY.Q* is the name of the Local Queue from terminal. You can view the queue in the web console, or you can display the queue and its properties by running in 'runmqsc` the following command: `DISPLAY QLOCAL('MY.Q')`.
    
3. [Optional] Monitor {{site.data.keyword.IBM_notm}} MQ logs inside the container. For more information, see [Managing your container through the command line](ibm_mq.html#ibm_mq_access).

For more information about the IBM MQ Getting started introduction, see [IBM MQ Version 9.0.x Welcome page ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](http://www.ibm.com/support/knowledgecenter/en/SSFKSJ_9.0.0/com.ibm.mq.helphome.v90.doc/WelcomePagev9r0.htm){: new_window}

For more information on the image and how to build your own image locally in Docker, see [the MQ Docker GitHub page ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-messaging/mq-docker){: new_window}
    
For the latest blogs and information on IBM MQ, see [The MQ Developer works blog ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/developerworks/community/blogs/messaging){: new_window}


### Provisioning a container that is based on the ibm-mq image
{: #ibm_mq_provision}

Complete the following steps to provision a Docker container in {{site.data.keyword.Bluemix_notm}} that is based on the ibm-mq image that is provided by {{site.data.keyword.IBM_notm}}:

1.	Log in to {{site.data.keyword.Bluemix_notm}}. Log in with your {{site.data.keyword.Bluemix_notm}} ID.
2.	From the catalog, select **Containers** and choose the *ibm-mq* image.
3.	Select **Single** to create a single instance container, which can be used for development and testing purposes.
4.	Enter the name of the container; for example, mq.
5.	Select the size of the container.
6.	In the Public IP address field, select **Request and Bind Public IP**.
7.	In the Public Ports field, specify **1414/tcp, 9443/tcp**.
8.	Expand the Advanced options, click **Add a new environment variable**, and enter the following environment variables: LICENSE, and MQ_QMGR_NAME.

    * Set the value of **LICENSE** to **accept** to agree to the IBM MQ Advanced for Developers license terms. 
    
        If you wish to view the license before accepting it, you can set LICENSE to “view” and the license will be printed in the container logs. 
    
        If English is not your first language, you can view the license file in a different language by setting another environment variable called **LANG** to one of the following values: *zh_TW* for Chinese_TW, *zh* for Chinese, *cs* for Czech, *en* for English, *fr* for French, *de* for German, *el* for Greek, *id* for Indonesian, *it* for Italian, *ja* for Japanese, *ko* for Korean, *lt* for Lithuanian, *pl* for Polish, *pt* for Portuguese, *ru* for Russian, *sl* for Slovenian, *es* for Spanish, or *tr* for Turkish.

    * Set the value of **MQ_QMGR_NAME** with the value *MYMQ* where *MYMQ* is your chosen Queue Manager name.
 
        **Note:** If you do not specify values for the environment variables LICENSE and MQ_QMGR_NAME, the container is created but does not start. 
    
    * [Optional] By default, the {{site.data.keyword.IBM_notm}} MQ Web Console is started in the container. To change the default behavior, set the **MQ_DISABLE_WEB_CONSOLE** environment variable value to *true*.
    
        **Note:** To use the web console, do not set the *MQ_DISABLE_WEB_CONSOLE* environment variable.

    * [Optional] To see the MQ logs through the {{site.data.keyword.Bluemix_notm}} UI, set the environment variable **LOG_LOCATIONS** to the value `/var/mqm/qmgr/QM_Name/errors/AMQERR01.LOG` where *QM_Name* is the value you set for the environment variable *MQ_QMGR_NAME*.
    
    *	[Optional] By default, the {{site.data.keyword.IBM_notm}} MQ Developer default objects are created. To change the default behavior, set the **MQ_DEV** environment variable to *false*, and modify the default installation values for IBM MQ with your custom values. For more information, see [Modify the default installation values](ibm_mq.html#ibm_mq_dev_default)
 
9. [Optional] In the Advanced options section, assign a volume. Use {{site.data.keyword.Bluemix_notm}} volumes for storing {{site.data.keyword.IBM_notm}} MQ data and configuration persistently over container migrations. {{site.data.keyword.IBM_notm}} MQ data that is not stored in a volume will be lost if a container is terminated.

    The ibm-mq image can be used with {{site.data.keyword.Bluemix_notm}} volumes, however volumes must be mounted to **/mnt/mqm** to be detected and utilized by {{site.data.keyword.IBM_notm}} MQ.

    By default, any containers created without a volume will lose any IBM MQ data when the container is stopped. If you want to prevent this, you must use persistent messaging and {{site.data.keyword.Bluemix_notm}} Volumes.

    1. Click **Create a volume**, enter a volume name, and select a file share.
    2. Click **Assign an existing volume**, and select the volume you created. Enter **/mnt/mqm** in the path box. Ensure the **Read-only** box is not checked.

    **Note:** When mounting a volume for use as the IBM MQ data directory, you must mount it to the location */mnt/mqm*. By mounting it to */mnt/mqm* the ibm-mq script will detect the volume and configure the IBM MQ filesystem to use it.
     
10.	Click **Create** and then wait for the container to start running.

    After the container is created, the container dashboard opens. Check the status of the container is set to **Running**. 

    To check the logs of you container, click **Monitoring and Logs** and select the **Logging** tab. The logs are displayed. For advanced analysis of you logs, click **Advanced view** to display your logs in Kibana.

You have created and started a queue manager. You can now connect an MQ application with the following connection details:

| Connection Property | Value |
|-------|-------|
| IP address  | Container’s public IP address |
| Port | 1414 |
| Channel | DEV.APP.SVRCONN |


### Managing your container through the command line
{: #ibm_mq_access}

After the container that runs {{site.data.keyword.IBM_notm}} MQ is deployed in {{site.data.keyword.Bluemix_notm}}, you can access your container and   the status of the container and validate the {{site.data.keyword.IBM_notm}} MQ installation.

Complete the following steps to verify the setup and configuration of {{site.data.keyword.IBM_notm}} MQ in the container:

1.	Set up the IBM Containers CLI. For more information, see [the Bluemix CLI page](https://plugins.ng.bluemix.net/ui/home.html) and follow the instructions to install the latest Cloud Foundry Container service plugin.

2.	From a terminal, log in to your {{site.data.keyword.Bluemix_notm}} organization and space where the container is running with your {{site.data.keyword.Bluemix_notm}} ID. Run the following commands:

    1. `bx login`
    2. `bx ic init`
    
3.	Check the status of the container. Run the following command: `bx ic ps`

4.	Attach a Bash session to your container:

    `bx ic exec -it container_name /bin/bash`
    
    where container_name is the name of the container
    
5.	Run commands to manage you MQ setup, for example:

| Command | Action |
|---------|---------|
| dspmqver | Verify the IBM MQ version and build information. |
| dspmq | Check the status of the Queue Manager that is running in the container. | 
| runmqsc | Manage MQ resources. |

To monitor MQ logs, choose one of the following options:

* If your terminal is configured to run {{site.data.keyword.containershort}} CLI commands, run the following command: `bx ic exec container_id tail -f /var/mqm/qmgr/QM_ Name/errors/AMQERR01.LOG` where *container_id* is the name of your container and *QM_ Name* is the name of your Queue Manager.
    
* If your terminal is configured to run Docker CLI commands, run the following command: `docker exec container_id tail -f /var/mqm/qmgr/QM_Name/errors/AMQERR01.LOG` where *container_id* is the name of your container and *QM_Name* is the name of your Queue Manager.
    
    

### Launching the IBM MQ web console
{: #ibm_mq_webui}

Complete the following steps to launch the {{site.data.keyword.IBM_notm}} MQ web console:

1.	In the {{site.data.keyword.Bluemix_notm}} dashboard, select your container, and check the status of the container is set to *Running*.
2.	Verify that your container has the public port 9443 configured.
3.	Check the container details to find the Public IP or request and bind one if not already done.
4.	From a web browser, launch the following URL: `https://DockerContainerPublicIP:9443/ibmmq/console/` where DockerContainerPublicIP is the public IP of your container.

    A security warning opens because the TLS certificate that the web server uses when hosting the MQ console is generated and self-signed. Click **add exception** and confirm.

    **Note:** In a production environment, use your own certificate which is recognized and trusted by your browser. This certificate should be issued by a certificate authority. 
    
    The browser opens the web user interface.
    
5. Log in to the {{site.data.keyword.IBM_notm}} MQ console with the credentials:

    1.	User: admin
    2.	Password: passw0rd
    
You are now ready to administer IBM MQ.

### Setting up a terminal to use the IBM Bluemix Container Service CLI
{: #ibm_mq_containers_cli}

Use the {{site.data.keyword.containershort}} CLI to run {{site.data.keyword.IBM_notm}} MQ administration commands directly in a container.

Complete the following steps to set up a terminal to run bx ic commands to manage IBM MQ:

1.	Set up the {{site.data.keyword.containershort}} CLI. For more information, see [the Bluemix CLI page](https://plugins.ng.bluemix.net/ui/home.html) and follow the instructions to install the latest Cloud Foundry Container service plugin.

2.	From a terminal, log in to {{site.data.keyword.Bluemix_notm}}. Run the following commands:

    1. `bx login`
    2. `bx ic init`
    
3.	Attach a Bash session to your container:

    `bx ic exec -it container_name /bin/bash`
    
    where container_name is the name of the container
    


### Setting up a terminal to use the Docker CLI
{: #ibm_mq_docker_commands}

Use the Docker CLI to run {{site.data.keyword.IBM_notm}} MQ administration commands directly in a container.

Complete the following steps to set up a terminal to run Docker commands to manage IBM MQ:

1.	Set up the {{site.data.keyword.containershort}} CLI. For more information, see [the Bluemix CLI page](https://plugins.ng.bluemix.net/ui/home.html) and follow the instructions to install the latest Cloud Foundry Container service plugin.

2.	From a terminal, log in to {{site.data.keyword.Bluemix_notm}}. Run the following commands:

    1. `bx login`
    2. `bx ic init`
    3. Copy the values that are provided for the following environment variables: DOCKER_HOST, DOCKER_CERT_PATH, and DOCKER_TLS_VERIFY.
    4. Override the local Docker environment by setting the following variables to connect to {{site.data.keyword.containershort}}:
        
        `export DOCKER_HOST=<your_host_value>`
        
        `export DOCKER_CERT_PATH=<your_cert_path_value>`
        
        `export DOCKER_TLS_VERIFY=1`

3.	Attach a Bash session to your container:

    `bx ic exec -it container_name /bin/bash`
    
    where container_name is the name of the container
    
**Note:** Only some Docker commands are supported by this option.




### Modify the default installation values
{: #ibm_mq_dev_default}

When the queue manager is created, it will be created with the {{site.data.keyword.IBM_notm}} MQ Developer defaults. These default objects are designed to help you get started quickly developing applications or even trying out {{site.data.keyword.IBM_notm}} MQ. 

The Queue Manager will be created with the following default objects:

* A MQ Administrator user **admin** with a password of *passw0rd*.
*	A MQ Application user **app** with no password.
*	A listener **DEV.LISTENER.TCP** configured to bind to port 1414/TCP.
*	A channel **DEV.APP.SVRCONN** configured to handle MQ client application connections.
*	A channel **DEV.ADMIN.SVRCONN** configured to handle MQ admin connections.
*	3 Queues **DEV.QUEUE.1**, **DEV.QUEUE.2**, **DEV.QUEUE.3** where you can place messages.
*	A Dead Letter Queue **DEV.DEAD.LETTER.QUEUE** where undeliverable messages will be placed.
*	A base topic **DEV.BASE.TOPIC** with the topic string of */dev*.
*	A Channel Authentication record to block all client connections unless they are connecting through the channel **DEV.APP.SVRCONN** or **DEV.ADMIN.SVRCONN**.
*	A Channel Authentication record to block all admin users connecting except through the **DEV.ADMIN.SVRCONN** channel.
*	A Channel Authentication record to only allow the user admin to connect to the **DEV.ADMIN.SVRCONN** channel.
*	Connection authentication set to require admin applications to pass valid credentials when connecting and to adopt that user ID for authority checks.

With these default objects, you could connect a client application that can put and get messages to a queue, or subscribe and publish to the topic.

If you wish to customize the developer defaults that are created, you can add the following environment variables when you create your container from the ibm-mq image.

| Environment variable | Purpose | Default |
|----------------------|---------|---------|
| MQ_ADMIN_PASSWORD | Set this variable to change the password of the created MQ administrator from the default to your own choice. The password must be at least 8 characters long. The username for the admin user is fixed as admin. | passw0rd |
| MQ_APP_PASSWORD | Set this variable to set the password for the application user. The username for the application user is fixed as app. If you set this environment variable, then you must supply the userid and password when you connect MQ clients. <br> The password must be at least 8 characters long. |  |
| MQ_TLS_KEYSTORE | Set this environment variable to the location of a PKCS#12 keystore that contains the certificate you want the MQ Web Console and IBM MQ Queue Manager to use for TLS operations. <br> When this environment variable is set, the developer channels created will be enabled for TLS using the CipherSpec ‘TLS_RSA_WITH_AES_256_GCM_SHA384’. <br> **Note:** You need to make the key store file available inside your {{site.data.keyword.Bluemix_notm}} container. To do this, you can mount a volume containing your keystore when you create the container. |  |
| MQ_TLS_PASSPHRASE | Set this environment variable to set the password for the keystore specified in the environment variable MQ_TLS_KEYSTORE. |  |
| MQ_DEV | Set this environment variable to control whether the {{site.data.keyword.IBM_notm}} MQ Developer default objects are created. | true |
| MQ_DISABLE_WEB_CONSOLE | Set this environment variable to disable the configuration and starting of the web console if you wish to conserve CPU/RAM usage of your container. |  |



