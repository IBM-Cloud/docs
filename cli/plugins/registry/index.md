---



copyright:

  years: 2017

lastupdated: "2017-05-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

The {{site.data.keyword.registrylong}} CLI is a plug-in to manage your registry and its resources for your account.
{: shortdesc}

**Prerequisites**
* Before running the registry commands, log in to {{site.data.keyword.Bluemix_short}}
 with the `bx login` command to generate a {{site.data.keyword.Bluemix_short}}
 access token and authenticate your session.

To find out about how to use the {{site.data.keyword.registrylong}} CLI, see [IBM Bluemix Container Registry overvie](https://console.ng.bluemix.net/docs/services/Registry/registry_setup.html#registry_setup).

<table summary="Manage your Containers Registry">
<caption>Table 1. Commands for managing {{site.data.keyword.registryshort}} on {{site.data.keyword.Bluemix_short}}
</caption>
 <thead>
 <th colspan="5">Commands for managing the registry</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx cr api](#bx_cr_api)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 <td>[bx cr image-inspect](#bx-cr-image-inspect)</td>
 <td>[bx cr image-list (bx cr images)](#bx-cr-image-list)</td>
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 </tr>
 <tr>
 <td>[bx cr login](#bx-cr-login)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-list (bx cr namespaces)](#bx-cr-namespace-list)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 <td>[bx cr token-add](#bx-cr-token-add)</td>
 </tr>
 <tr>
 <td>[bx cr token-get](#bx-cr-token-get)</td>
 <td>[bx cr token-list (bx cr tokens)](#bx-cr-token-list)</td>
 <td>[bx cr token-rm](#bx-cr-token-rm)</td>
 </tr>
 </tbody></table>



## bx cr api
{: #bx_cr_api}

Returns the details about the registry API endpoint that the commands are run against.

```
bx cr api
```
{: codeblock}


## bx cr info
Displays the name and the account of the registry that you are logged in to.

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
Displays details about a specific image.

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE]
```
{: codeblock}

**Parameters**


<dl>
<dt>--format FORMAT</dt>
<dd>(Optional) Format the output elements by using a Go template. 


</dd>
<dt>IMAGE</dt>
<dd>The full {{site.data.keyword.Bluemix_short}} registry path to the image that you want to inspect, which is in the format `namespace/image:tag`. If a tag is not specified in the image path, the image tagged `latest` is inspected. You can inspect multiple images by listing each private {{site.data.keyword.Bluemix_short}} registry path in the command with a space between each path.</dd>
</dl>


## bx cr image-list (bx cr images)
Displays all images in your {{site.data.keyword.Bluemix_short}} account.

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**Parameters**
<dl>
<dt>--no-trunc</dt>
<dd>(Optional) Do not truncate the image digests.</dd>
<dt>-q, --quiet</dt>
<dd>(Optional) Each image is listed in the format: `repository:tag`.</dd>
<dt>--include-ibm</dt>
<dd>(Optional) Includes IBM-provided public images in the output. Without this option, by default private images only are listed.</dd>
<dt>--format FORMAT</dt>
<dd>(Optional) Format the output elements by using a Go template. 


</dd>

</dl>


## bx cr image-rm
Deletes one or more specified images from your registry.

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**Parameters**
<dl>
<dt>IMAGE</dt>
<dd>The full {{site.data.keyword.Bluemix_short}} registry path to the image that you want to remove, in the format `namespace/image:tag`. If a tag is not specified in the image path, the image tagged `latest` is deleted by default. You can delete multiple images by listing each private {{site.data.keyword.Bluemix_short}} registry path in the command with a space between each path.</dd>
</dl>


## bx cr login
This command runs the `docker login` command against the registry. The `docker login` command is required to be able to run the `docker push` or `docker pull` commands for the registry. This command is not required to run other `bx cr` commands. If Docker is not installed, this command returns an error message.

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
Adds a namespace to your {{site.data.keyword.Bluemix_short}} account.

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**Parameters**
<dl>
<dt>NAMESPACE</dt>
<dd>The namespace you want to add. The namespace must be unique across all {{site.data.keyword.Bluemix_short}} accounts in the same region.</dd>
</dl>


## bx cr namespace-list (bx cr namespaces)
Displays all namespaces that are owned by your {{site.data.keyword.Bluemix_short}} account.

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
Removes a namespace from your {{site.data.keyword.Bluemix_short}} account. Images in this namespace are deleted when the namespace is removed.

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**Parameters**
<dl>
<dt>NAMESPACE</dt>
<dd>The namespace that you want to remove.</dd>
</dl>


## bx cr token-add
Adds a token that you can use to control access to a registry.

```
bx cr token-add [--description VALUE] [-q, --quiet] [--non-expiring] [--readwrite]
```

{: codeblock}


**Parameters**
<dl>
<dt>--description VALUE</dt>
<dd>(Optional) Specifies the value as a description for the token, which is displayed when you run `bx cr token-list`. If your token is created automatically by IBM Bluemix Container Service, the description is set to your Kubernetes Cluster name. In this case, the token is removed automatically when your cluster is removed.</dd>
<dt>-q, --quiet</dt>
<dd>(Optional) Displays the token only, without any surrounding text.</dd>
<dt>--non-expiring</dt>
<dd>(Optional) Creates a token with access that does not expire. Without this parameter set, access from a token expires after 24 hours by default.</dd>
<dt>--readwrite</dt>
<dd>(Optional) Creates a token that grants read and write access. Without this option, access is read-only by default.</dd>
</dl>


## bx cr token-get
Retrieve the specified token from the registry.

```
bx cr token-get TOKEN
```

{: codeblock}

**Parameters**
<dl>
<dt>TOKEN</dt>
<dd>(Optional) The unique identifier of the token that you want to retrieve.</dd>
</dl>


## bx cr token-list (bx cr tokens)
Displays all tokens that exist for your {{site.data.keyword.Bluemix_short}} account.

```
bx cr token-list --format FORMAT
```
{: codeblock}

**Parameters**
<dl>
<dt>--format FORMAT</dt>
<dd>(Optional) Format the output elements by using a Go template. 


</dd>
</dl>


## bx cr token-rm
Remove one or more specified tokens.

```
bx cr token-rm TOKEN [TOKEN]
```
{: codeblock}

**Parameters**
<dl>
<dt>TOKEN</dt>
<dd>(Optional) TOKEN can be either the token itself, or the unique identifier of the token, as shown in `bx cr token-list`. Multiple tokens can be specified and they must be separated by a space.</dd>
</dl>


</dd>
</dl>


