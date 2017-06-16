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

{{site.data.keyword.registrylong}} CLI 是一个插件，用于为您的帐户管理您的注册表及其资源。
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

返回有关对其运行命令的注册表 API 端点的详细信息。

```
bx cr api
```
{: codeblock}


## bx cr info
显示您登录到的注册表的名称和帐户。

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
显示有关特定映像的详细信息。

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE]
```
{: codeblock}

**参数**


<dl>
<dt>--format FORMAT</dt>
<dd>（可选）使用 Go 模板设置输出元素的格式。</dd>
<dt>IMAGE</dt>
<dd>要检查的映像的完整 {{site.data.keyword.Bluemix_short}} 注册表路径，格式为 `namespace/image:tag`。如果未在映像路径中指定标记，那么会检查标记为 `latest` 的映像。可以通过在命令中列出每个专用 {{site.data.keyword.Bluemix_short}} 注册表路径（各路径之间用空格分隔）来检查多个映像。</dd>
</dl>


## bx cr image-list (bx cr images)
显示 {{site.data.keyword.Bluemix_short}} 帐户中的所有映像。

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**参数**
<dl>
<dt>--no-trunc</dt>
<dd>（可选）不截断映像摘要。</dd>
<dt>-q, --quiet</dt>
<dd>（可选）列出每个映像，格式为：`repository:tag`。</dd>
<dt>--include-ibm</dt>
<dd>（可选）在输出中包含 IBM 提供的公共映像。不使用此选项时，缺省情况下仅列出专用映像。</dd>
<dt>--format FORMAT</dt>
<dd>（可选）使用 Go 模板设置输出元素的格式。</dd>

</dl>


## bx cr image-rm
从注册表中删除指定的一个或多个映像。

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**参数**
<dl>
<dt>IMAGE</dt>
<dd>要除去的映像的完整 {{site.data.keyword.Bluemix_short}} 注册表路径，格式为 `namespace/image:tag`。如果未在映像路径中指定标记，那么缺省情况下会删除标记为 `latest` 的映像。可以通过在命令中列出每个专用 {{site.data.keyword.Bluemix_short}} 注册表路径（各路径之间用空格分隔）来删除多个映像。</dd>
</dl>


## bx cr login
此命令将对注册表运行 `docker login` 命令。必须运行 `docker login` 后，才能对注册表运行 `docker push` 或 `docker pull` 命令。无须运行此命令，即可运行其他 `bx cr` 命令。如果未安装 Docker，那么此命令会返回错误消息。

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
向 {{site.data.keyword.Bluemix_short}} 帐户添加名称空间。

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**参数**
<dl>
<dt>NAMESPACE</dt>
<dd>要添加的名称空间。名称空间在同一区域中的所有 {{site.data.keyword.Bluemix_short}} 帐户之间必须唯一。</dd>
</dl>


## bx cr namespace-list (bx cr namespaces)
显示 {{site.data.keyword.Bluemix_short}} 帐户拥有的所有名称空间。

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
从 {{site.data.keyword.Bluemix_short}} 帐户中除去名称空间。除去名称空间时，会删除此名称空间中的映像。

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**参数**
<dl>
<dt>NAMESPACE</dt>
<dd>要除去的名称空间。</dd>
</dl>


## bx cr token-add
添加可用于控制对注册表的访问权的令牌。

```
bx cr token-add [--description VALUE] [-q, --quiet] [--non-expiring] [--readwrite]
```

{: codeblock}


**参数**
<dl>
<dt>--description VALUE</dt>
<dd>（可选）指定作为令牌描述的值，在运行 `bx cr token-list` 时会显示此值。如果令牌是由 IBM Bluemix Container Service 自动创建的，那么描述会设置为 Kubernetes 集群名称。在这种情况下，除去集群时，会自动除去令牌。</dd>
<dt>-q, --quiet</dt>
<dd>（可选）仅显示令牌，不包括任何周围的文本。</dd>
<dt>--non-expiring</dt>
<dd>（可选）创建具有不到期访问权的令牌。未设置此参数时，缺省情况下令牌的访问权在 24 小时后到期。</dd>
<dt>--readwrite</dt>
<dd>（可选）创建用于授予读和写访问权的令牌。不使用此选项时，缺省情况下访问权为只读。</dd>
</dl>


## bx cr token-get
在注册表中检索指定的令牌。

```
bx cr token-get TOKEN
```

{: codeblock}

**参数**
<dl>
<dt>TOKEN</dt>
<dd>（可选）要检索的令牌的唯一标识。</dd>
</dl>


## bx cr token-list (bx cr tokens)
显示针对您的 {{site.data.keyword.Bluemix_short}} 帐户存在的所有令牌。

```
bx cr token-list --format FORMAT
```
{: codeblock}

**参数**
<dl>
<dt>--format FORMAT</dt>
<dd>（可选）使用 Go 模板设置输出元素的格式。</dd>
</dl>


## bx cr token-rm
除去指定的一个或多个令牌。

```
bx cr token-rm TOKEN [TOKEN]
```
{: codeblock}

**参数**
<dl>
<dt>TOKEN</dt>
<dd>（可选）TOKEN 可以是令牌本身，也可以是令牌的唯一标识，如 `bx cr token-list` 中所示。可以指定多个令牌，令牌之间必须用一个空格分隔。</dd>
</dl>


</dd>
</dl>


