---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Configuring the CLI to use Swift and Cloud Foundry commands

To interact with the {{site.data.keyword.objectstorageshort}} service by using Swift or Cloud Foundry commands, you must install the prerequisite software.
{: shortdesc}


## Installing the Swift client {: #install-swift-client}

If you haven't already, install the following prerequisite software.
* Python 2.7 or later
* setuptools package
* pip package
* Cloud Foundry CLI


To install the Python Swift client, run the following command:
```
pip install python-swiftclient
```
{: pre}

To install the Python Keystone client, run the following command:
```
pip install python-keystoneclient
```
{: pre}

For more information about the prerequisites, see <a href="http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software" target="_blank">the OpenStack documentation. <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>



## Setting up the client {: #setup-swift-client}

To configure the Swift client, you must `export` your authentication information. You can [generate credentials](/docs/services/ObjectStorage/os_credentials.html) through the CLI by using Cloud Foundry or cURL commands or through the {{site.data.keyword.Bluemix_notm}} UI. The client takes the information from the environment variables in the following table.

<table>
<caption> Table 1. Environment variables and descriptions </caption>
  <tr>
    <th> Environment variable </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> <code> OS_USER_ID </code> </td>
    <td> Your {{site.data.keyword.objectstorageshort}} user ID. </td>
  </tr>
  <tr>
    <td> <code> OS_PASSWORD </code> </td>
    <td> The password for your {{site.data.keyword.objectstorageshort}} instance. </td>
  </tr>
  <tr>
    <td> <code> OS_PROJECT_ID </code> </td>
    <td> Your project ID. </td>
  </tr>
  <tr>
    <td> <code> OS_REGION_NAME </code> </td>
    <td> The region in which your objects are stored. {{site.data.keyword.objectstorageshort}} is available in the Dallas and London regions. </td>
  </tr>
  <tr>
    <td> <code> OS_AUTH_URL </code> </td>
    <td> The endpoint URL. Be sure that <code>/v3</code> is added to the end of the URL. </td>
  </tr>
</table>



To export your authentication information, input your credentials and run the following command:
```
export OS_USER_ID=
export OS_PASSWORD=
export OS_PROJECT_ID=
export OS_AUTH_URL=
export OS_REGION_NAME=
export OS_IDENTITY_API_VERSION=
export OS_AUTH_VERSION=

swift auth
```
{: codeblock}


Example:
```
export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
export OS_PASSWORD=*******
export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
export OS_AUTH_URL=https://identity.open.softlayer.com/v3
export OS_REGION_NAME=dallas
export OS_IDENTITY_API_VERSION=3
export OS_AUTH_VERSION=3

swift auth
```
{: screen}
