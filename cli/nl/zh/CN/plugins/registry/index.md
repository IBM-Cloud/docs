---



copyright:

  years: 2017

lastupdated: "2017-04-07"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

{{site.data.keyword.registrylong}} CLI 是一个插件，支持您管理整个组织中的注册表资源，例如名称空间和映像。
{: shortdesc}

**先决条件**
* 运行注册表命令之前，请先使用 `bx login` 命令登录到 {{site.data.keyword.Bluemix_short}}，以生成 {{site.data.keyword.Bluemix_short}} 访问令牌并对会话进行认证。

<table summary="管理容器注册表">
<caption>表 1. 用于在 {{site.data.keyword.Bluemix_short}} 上管理 {{site.data.keyword.registryshort}} 的命令</caption>
 <thead>
 <th colspan="5">用于管理注册表的命令</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx cr api](#bx-cr-api)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 <td>[bx cr image-inspect](#bx-cr-image-inspect)</td>
 <td>[bx cr image-list](#bx-cr-image-list)</td>
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 </tr>
 <tr>
 <td>[bx cr login](#bx-cr-login)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-list](#bx-cr-namespace-list)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 </tr></tbody></table>


## bx cr api
返回有关对其运行命令的注册表 API 端点的详细信息。

```
bx cr api
```
{: codeblock}


## bx cr info
显示您登录到的注册表的名称和组织。

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
查看有关特定映像的详细信息。

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE]
```
{: codeblock}

**参数**
<dl>
<dt>--format FORMAT</dt>
<dd>（可选）使用 Go 模板设置输出元素的格式。</dd>
<dt>IMAGE</dt>
<dd>要检查的映像的完整 {{site.data.keyword.Bluemix_short}} 注册表路径，格式为 namespace/image:tag。如果未在映像路径中指定标记，那么会检查标记为 `latest` 的映像。可以通过在命令中列出每个专用 {{site.data.keyword.Bluemix_short}} 注册表路径（各路径之间用空格分隔）来检查多个映像。</dd>
</dl>


## bx cr image-list
查看 {{site.data.keyword.Bluemix_short}} 组织中的所有映像。

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**参数**
<dl>
<dt>--no-trunc</dt>
<dd>（可选）不截断输出。</dd>
<dt>-q, --quiet</dt>
<dd>（可选）显示映像的唯一标识，格式为：“repository:tag”。</dd>
<dt>--include-ibm</dt>
<dd>（可选）在输出中包含 IBM 提供的公共映像。不使用此选项时，仅列出专用映像。</dd>
<dt>--format FORMAT</dt>
<dd>（可选）使用 Go 模板设置输出元素的格式。</dd>
</dl>


## bx cr image-rm
从注册表中删除指定的映像。

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**参数**
<dl>
<dt>IMAGE</dt>
<dd>要除去的映像的完整 {{site.data.keyword.Bluemix_short}} 注册表路径，格式为 namespace/image:tag。如果未在映像路径中指定标记，那么缺省情况下会删除标记为 `latest` 的映像。可以通过在命令中列出每个专用 {{site.data.keyword.Bluemix_short}} 注册表路径（各路径之间用空格分隔）来删除多个映像。</dd>
</dl>


## bx cr login
如果安装了 Docker，那么此命令将对注册表运行 `docker login` 命令。必须运行 `docker login` 后，才能对注册表运行 `docker push` 或 `docker pull` 命令。无须运行此命令，即可运行其他 `bx cr` 命令。如果未安装 Docker，那么此命令会返回错误消息。

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
向 Bluemix 组织添加名称空间。 

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**参数**
<dl>
<dt>NAMESPACE</dt>
<dd>要添加的名称空间。名称空间在所有 {{site.data.keyword.Bluemix_short}} 组织上必须唯一。</dd>
</dl>


## bx cr namespace-list
查看您的 {{site.data.keyword.Bluemix_short}} 组织的所有名称空间。

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
从 {{site.data.keyword.Bluemix_short}} 组织中除去名称空间。除去名称空间时，会删除此名称空间中的映像。

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**参数**
<dl>
<dt>NAMESPACE</dt>
<dd>要除去的名称空间。</dd>
</dl>
