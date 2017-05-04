---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# FIPS 方式
{: #fips_mode}

Nodejs buildpack V3.2-20160315-1257 及更高版本支持 [FIPS ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards)。  
{: shortdesc}

要使用已启用 FIPS 的节点引擎，请将环境变量 FIPS_MODE 设置为 true。
例如：

```
$ cf set-env myapp FIPS_MODE true
```
{: codeblock}

您有必要了解：当 FIPS_MODE 为 true 时，某些节点模块可能无法工作。例如，**使用 [MD5 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://en.wikipedia.org/wiki/MD5) 的节点模块将失败**，例如 [Express ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://expressjs.com/)。对于 Expess，在 Expess 应用程序中将 [etag ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://expressjs.com/en/api.html) 设置为 false 可能会帮助解决此问题。例如，您可以在代码中执行以下操作：

```
app.set('etag', false);
```
{: codeblock}
有关更多信息，请参阅此 [stackoverflow 帖子 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js)。

**注**：*无法*同时支持[应用程序管理](/docs/manageapps/app_mng.html)和 FIPS_MODE。如果设置了 BLUEMIX_APP_MGMT_ENABLE 环境变量，并且 FIPS_MODE 环境变量设置为 true，那么应用程序将无法编译打包。

可用于检查 FIPS_MODE 状态的方法很多：
<ul>
<li> 您可以检查应用程序的日志中是否有类似于以下内容的消息：    

  <pre>
  Installing FIPS-enabled IBM SDK for Node.js (4.4.3) from cache
  </pre>
  {: codeblock}

此消息指示正在运行已启用 FIPS 的 node.js 引擎，但 FIPS 未必正在运行
</li>

<li> 您可以检查 **process.versions.openssl** 的值。例如：

  <pre>
console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

如果 SSL 版本包含“fips”，那么正在使用的 SSL 版本支持 FIPS。  
</li>

<li> 对于 node.js V6 及更高版本，您可以使用类似如下代码检查 crypto.fips 返回的值：

  <pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

如果返回值为 1，表示正在使用 FIPS。请注意，对于 node.js V6 之前的版本，crypto.fips 将返回*undefined*。
</li>
</ul>

## Nodejs V4
{: #nodejs_v4_fips}

下表说明了使用 FIPS 的 node.js V4 的行为：

|                 | 结果        |
| :-------------- | :------------ |
|FIPS_MODE=true   |success (1)    |
|FIPS_MODE !=true |success (2)    |

* success (1)
  * FIPS 正在使用中。
  * 该日志中将包含消息 *Installing FIPS-enabled IBM SDK for Node.js*。
  * process.versions.openssl 返回的值将包含“fips”。
* success (2)
  * FIPS *未在*使用中。
  * 该日志中将*不会*包含消息 *Installing FIPS-enabled IBM SDK for Node.js*。
  * process.versions.openssl 返回的值将*不*包含“fips”。

## Nodejs V6
{: #nodejs_v6_fips}

要在 Node.js V6 中以 FIPS 方式运行，除了设置 **FIPS_MODE=true** 以外，您还必须在启动命令中包含 **--enable-fips**，如以下示例所示：
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

下表说明了使用 FIPS 的 node.js V6 的行为：

|                 |--enable-fips  |NO --enable-fips |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |success (1)    |success (2)      |
|FIPS_MODE !=true |failure (3)    |success (4)      |

* success (1)
  * FIPS 正在使用中。
  * 该日志中将包含消息 *Installing FIPS-enabled IBM SDK for Node.js*。
  * process.versions.openssl 返回的值将包含“fips”
  * crypto.fips 将返回 1，指示 FIPS 正在使用中
* success (2)
  * FIPS *未在*使用中。
  * 该日志中将包含消息 *Installing FIPS-enabled IBM SDK for Node.js*。
  * process.versions.openssl 返回的值将包含“fips”
  * crypto.fips 将返回 0，指示 FIPS *未在*使用中
* failure (3)
  * FIPS *未在*使用中。
  * 该日志中将*不会*包含消息 *Installing FIPS-enabled IBM SDK for Node.js*。
  * 编译打包将失败，并显示消息“ERR node: bad option: --enable-fips”
* success (4)
  * FIPS *未在*使用中。
  * 该日志中将*不会*包含消息 *Installing FIPS-enabled IBM SDK for Node.js*。
  * process.versions.openssl 返回的值将*不*包含“fips”
  * crypto.fips 将返回 0，指示 FIPS *未在*使用中
