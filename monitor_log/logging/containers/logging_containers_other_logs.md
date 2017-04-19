---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Collecting non-default log data from a container
{: #logging_containers_collect_data}

To capture data from non-default log locations inside a container, set the environment variable **LOG_LOCATIONS** when you create a container. 
{:shortdesc}

* Add the **LOG_LOCATIONS** environment variable with a path to the log file when you create the container. 
* You can add multiple log files by separating them with commas. 

## Collecting non-default log data through the Bluemix console
{: #logging_containers_collect_data_ui}

Complete the following steps to collect non-default data through the console:

1. From the catalog, select **Containers** and choose an image. 

    The list of images that are displayed include images that are provided by {{site.data.keyword.IBM}} and images that are stored in your private {{site.data.keyword.Bluemix_notm}} registry. 

2. Define your container. Choose the type, enter a name for the container, select its size, and define other attributes such as IP address details and ports. For more information, see [Create and deploy a single container through the {{site.data.keyword.Bluemix_notm}} UI](/docs/containers/container_single_ui.html#gui). 

3. Expand the **Advanced Options** section and select **Add a new environment variable**.

4. Add the **LOG_LOCATIONS** variable and set its value to the log that you want to analyze.

    For example, when you add a container that is based on the latest Liberty image, to analyze the log file *dpkg.log*, set the environment value to the following value:
    
    <table>
      <caption>Table 1. Log locations sample value</caption>
      <tbody>
        <tr>
          <th align="center">Variable name</th>
          <th align="center">Value</th>
        </tr>
        <tr>
          <td align="left">LOG_LOCATIONS</td>
          <td align="left">/var/log/dpkg.log</td>
        </tr>
      </tbody>
    </table>

4. Click **Create**.

The container dashboard opens. Check the status of the container is *Running*, then check the logs in the **Monitoring and logs** tab.


## Collecting non-default log data through the CLI
{: #logging_containers_collect_data_cli}

Complete the following steps to collect non-default log data through the CLI:

1. Set up a terminal to use the {{site.data.keyword.containershort}} CLI. For more information, see [Setting up the IBM Bluemix Container Service CLI](/docs/containers/container_cli_cfic_install.html).

2. Log in to the Cloud Foundry CLI by using the following command: `cf login`. Enter your {{site.data.keyword.Bluemix_notm}} ID, password, organization, and space as you are prompted. 

    By default, you are logged in to the US South region or the last region you logged in to. 
    
    You can include the **–a** option to log in to a specific region in {{site.data.keyword.Bluemix_notm}}. For example, the following table lists the commands per region:

    <table>
      <caption>Table 2. Commands per region</caption>
      <tbody>
        <tr>
          <th align="center">Region</th>
          <th align="center">Command</th>
        </tr>
        <tr>
          <td align="left">US South</td>
          <td align="left"> cf login -a api.ng.bluemix.net</td>
        </tr>
        <tr>
          <td align="left">United Kingdom</td>
          <td align="left">cf login -a api.eu-gb.bluemix.net</td>
        </tr>
	 <tr>
          <td align="left">Frankfurt</td>
          <td align="left">cf login -a api.eu-de.bluemix.net</td>
        </tr>
       </tbody>
    </table>
    

3. Log in to the {{site.data.keyword.containershort}} by using the following command: `cf ic login`

4. Create a single container from an image. Include the LOG_LOCATIONS environment variable to include non-default log locations.  

    To add a custom location so that you can view that log information in Kibana, add the **LOG_LOCATIONS** environment variable when you create the container. Enter the following command:
    
    `docker run -p portNumber -e "LOG_LOCATIONS=log1,log2" --name containerName registry.domain_name/imageName:imageTag`
    
    where
    
     <table>
      <caption>Table 3. Command options</caption>
      <tbody>
        <tr>
          <th align="center">Option</th>
          <th align="center">Description</th>
        </tr>
        <tr>
          <td align="left">-p</td>
          <td align="left"> If you want to make your app accessible from the Internet, you need to expose a public port. Include any ports that are specified in the Dockerfile for the image you are using. <br> You can choose between UDP and TCP to indicate the IP protocol that you want to use. If you do not specify a protocol, your port is automatically exposed for TCP traffic. <br> When you expose a public port, you create a Public Network Security Group for your container that allows you to send and receive public data on the exposed port only. All other public ports are closed and cannot be used to access your app from the internet. <br> You can include multiple ports with multiple -p options. </td>
        </tr>
        <tr>
          <td align="left">-e</td>
          <td align="left">Set an environment variable. <br> You can list multiple keys separately. Include quotation marks around both the environment variable name and the value. <br> To add a log file to be monitored in the container, include the LOG_LOCATIONS environment variable with a path to the log file.</td>
        </tr>
        <tr>
          <td align="left">--name</td>
          <td align="left">Defines the name of the container.</td>
        </tr>
	<tr>
          <td align="left">registry.domain_name</td>
          <td align="left">Registry in the public region. For example, for US South region, the default domain name is: `ng.bluemix.net` and for the United Kingdom, the default domain name is: `eu-gb.bluemix.net` </td>
        </tr>
        <tr>
          <td align="left">imageName</td>
          <td align="left">Name of the image that you want to add.</td>
        </tr>
	<tr>
          <td align="left">imageTag</td>
          <td align="left">Tag of the image that you want to add.</td>
        </tr>
      </tbody>
    </table>
    
    For example, to create a container based on the latest Liberty image and include the log file `/var/log/dpkg.log`, use the following command: 
    
    `docker run -p 9080 -e "LOG_LOCATIONS=/var/log/dpkg.log" --name MyContainer registry.ng.bluemix.net/ibmliberty:latest`
    
    The dpkg.log file is a standard Ubuntu log file that is commonly generated during the creation of a container, but is not pushed automatically to Kibana.

To check the status of the container, run the command `docker ps`. When the status is *Running*, check the logs in the {{site.data.keyword.Bluemix_notm}} console, through the command line, or through Kibana.



