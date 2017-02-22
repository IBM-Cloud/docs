---



copyright:

  years: 2017

lastupdated: "2017-02-01"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong}} CLI
{: #containerregcli}

The {{site.data.keyword.registrylong}} CLI is a plug-in that lets you manage your registry resources, such as namespaces, images, and quotas, across your org.
{: shortdesc}

**Prerequisites**
* Before running the registry commands, log in to {{site.data.keyword.Bluemix_short}}
 with `bx login` to generate a {{site.data.keyword.Bluemix_short}}
 access token and authenticate your session.

<table summary="Manage your Containers Registry">
<caption>Table 1. Commands for managing {{site.data.keyword.registryshort}} on {{site.data.keyword.Bluemix_short}}
</caption>
 <thead>
 <th colspan="5">Commands for managing the registry</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx cr login](#bx-cr-login)</td>
 <td>[bx cr api](#bx-cr-api)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 <td>[bx cr namespace-list](#bx-cr-namespace-list)</td>
 </tr>
 <tr>
 <td>[bx cr image-list](#bx-cr-image-list)</td>
 <!--<td>[bx cr image-inspect](#bx-cr-image-inspect)</td>-->
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 </tr></tbody></table>

 
## bx cr login
If Docker is installed, this command runs `Docker login` against the registry. `Docker login` is required to be able to `Docker push` or `Docker pull` to the registry. This command is not required to run other `bx cr` commands. If Docker is not installed, this command returns an error message.

```
bx cr login [--target REGISTRY]
```
{: codeblock}

## bx cr api
Returns which registry API endpoint the commands are run against.

```
bx cr api
```
{: codeblock}

## bx cr namespace-add
Add a namespace to your Bluemix org. 

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**Parameters**
<dl>
<dt>NAMESPACE</dt>
<dd>The namespace you want to add. The namespace must be unique across all orgs.</dd>
</dl>

## bx cr namespace-rm
Removes a namespace from your Bluemix org. Images in this namespace are deleted when the namespace is removed.

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**Parameters**
<dl>
<dt>NAMESPACE</dt>
<dd>The namespace you want to remove.</dd>
</dl>

## bx cr namespace-list
View all namespaces within by your {{site.data.keyword.Bluemix_short}} org. You can also run this command as `bx cr namespaces`.

```
bx cr namespace-list
```
{: codeblock}

 
## bx cr image-list
View all images in your {{site.data.keyword.Bluemix_short}} org. You can also run this command as `bx cr images`.

```
 bx cr image-list [-a, --all] [--no-trunc] [-q, --quiet] [--public] [--format FORMAT]
```
{: codeblock}

**Parameters**
<dl>
<dt>-a, --all</dt>
<dd>(Optional) Includes all of the image layers for each image in your org's registry, not just the most recent layer.</dd>
<dt>--no-trunc</dt>
<dd>(Optional) Do not truncate the output.</dd>
<dt>-q, --quiet</dt>
<dd>(Optional) Displays a unique identifier for the image in the format: `repository:tag`.</dd>
<dt>--public</dt>
<dd>(Optional) Only display public images.</dd>
<dt>--format FORMAT</dt>
<dd>(Optional) Format the output using a Go template. Strings: `Tag`, `Digest`, `Vulnerable`, `Namespace`. Integer (64 bit): `Created`, `Size`.</dd>
</dl>

<!--## bx cr image-inspect
View details about a specific image.

```
bx cr image-inspect IMAGE
```
{: codeblock}

**Parameters**
<dl>
<dt>IMAGE</dt>
<dd>The full {{site.data.keyword.Bluemix_short}} registry path to the image that you want to inspect.</dd>
<dt>--format FORMAT</dt>
<dd>(Optional) Format the output using a Go template. Strings: `Tag`, `Digest`, `Vulnerable`, `Namespace`. Integer (64 bit): `Created`, `Size`.</dd>
</dl>-->

## bx cr image-rm
Delete a specified image from your registry.

```
bx cr image-rm IMAGE
```
{: codeblock}

**Parameters**
<dl>
<dt>IMAGE</dt>
<dd>The full, private {{site.data.keyword.Bluemix_short}} registry path to the image that you want to remove. If a tag is not specified in the image path, the image tagged latest is deleted by default. You can run this command with multiple images by listing each private {{site.data.keyword.Bluemix_short}} registry path in the command with a space in between.</dd></dl>
