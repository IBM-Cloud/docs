---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-24"

---

{:shortdesc: .shortdesc}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 系统详细信息
{: #openwhisk_reference}


以下各部分提供了有关 {{site.data.keyword.openwhisk}} 系统的更多详细信息。
{: shortdesc}

## {{site.data.keyword.openwhisk_short}} 实体
{: #openwhisk_entities}

### 名称空间和包
{: #openwhisk_entities_namespaces}

{{site.data.keyword.openwhisk_short}} 操作、触发器和规则属于名称空间，并可选择属于包。

包可以包含操作和订阅源。一个包不能包含其他包，所以不允许包嵌套。此外，实体不必包含在包中。

在 Bluemix 中，组织+空间对与 {{site.data.keyword.openwhisk_short}} 名称空间相对应。例如，组织 `BobsOrg` 和空间 `dev` 将对应于 {{site.data.keyword.openwhisk_short}} 名称空间 `/BobsOrg_dev`。

如果您有权创建名称空间，那么可以创建自己的名称空间。`/whisk.system` 名称空间保留用于使用 {{site.data.keyword.openwhisk_short}} 系统分发的实体。


### 标准名称
{: #openwhisk_entities_fullyqual}

实体的标准名称为
`/namespaceName[/packageName]/entityName`。请注意，`/` 用于对名称空间、包和实体定界。此外，名称空间必须带有前缀 `/`。

为了方便起见，如果名称空间是用户的*缺省名称空间*，那么可以保留不变。

例如，假设用户的缺省名称空间为 `/myOrg`。以下是一些实体的标准名称及其别名的示例。

| 标准名称 | 别名 | 名称空间 | 包 | 名称 |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` |  | `/whisk.system` | `cloudant` | `read` |
| `/myOrg/video/transcode` | `video/transcode` | `/myOrg` | `video` | `transcode` |
| `/myOrg/filter` | `filter` | `/myOrg` |  | `filter` |

使用 {{site.data.keyword.openwhisk_short}} CLI 时，您将使用此命名方案，在其他位置也同样遵循此方案。

### 实体名称
{: #openwhisk_entities_names}

包括操作、触发器、规则、包和名称空间在内的所有实体的名称均为遵循以下格式的字符序列：

* 第一个字符必须为字母数字字符或下划线。
* 后续字符可以为字母数字、空格或以下任一字符：`_`、`@`、`.` 和 `-`。
* 最后一个字符不能为空格。

更准确地说，名称必须匹配以下正则表达式（使用 Java 元字符语法表达）：`\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`。


## 操作语义
{: #openwhisk_semantics}

以下各部分描述了有关 {{site.data.keyword.openwhisk_short}} 操作的详细信息。

### 无状态
{: #openwhisk_semantics_stateless}

操作实施应该是无状态的，即*幂等*。虽然系统不会强制执行此属性，但不保证操作保持的任何状态在各调用中均可用。

此外，一个操作可能存在多个实例化，其中每个实例化都有其自己的状态。可能会将操作调用分派给其中任一实例化。

### 调用输入和输出
{: #openwhisk_semantics_invocationio}

操作的输入和输出是键/值对的字典。键为字符串，值为有效的 JSON 值。

### 操作的调用顺序
{: #openwhisk_ordering}

操作的调用并未排序。如果用户通过命令行或 REST API 调用一个操作两次，那么第二个调用可能会先于第一个调用运行。如果操作有副作用，那么可能会以任意顺序观察到这些副作用。

此外，不保证操作以原子方式执行。两个操作可以并行运行，其副作用可能会交错。对于副作用，OpenWhisk 并不能确保任何特定的并行一致性模型。任何并行副作用都将依赖于实施。

### 操作执行保证
{: #openwhisk_atmostonce}

收到调用请求时，系统会记录该请求，并分派激活。

系统会返回激活标识（对于非阻塞调用），以确认收到了调用。请注意，如果在接收 HTTP 响应之前存在网络故障或其他引起干预的故障，那么 {{site.data.keyword.openwhisk_short}} 可以接收并处理请求。

系统尝试调用操作一次，产生以下四个结果之一：
- *success*：操作调用成功完成。
- *application error*：操作调用成功，但操作有意返回了错误值，例如由于不满足自变量上的前置条件。
- *action developer error*：操作已调用，但以异常方式完成，例如操作未检测到异常或存在语法错误。
- *whisk internal error*：系统无法调用操作。
结果会记录在激活记录的 `status` 字段中，如以下部分中所述。

成功收到的每个调用以及可能对用户记帐的每个调用最终都将具有激活记录。

请注意，对于 *操作开发者错误*，操作可能已部分运行并生成外部可视的副作用。用户应负责检查是否实际发生了此类副作用并根据需要发出重试逻辑。另请注意，某些 *whisk 内部错误*将指示操作已开始运行，但在操作注册完成之前系统发生故障。

## 激活记录
{: #openwhisk_ref_activation}

每次操作调用和触发器触发都会产生一个激活记录。

激活记录包含以下字段：

- *activationId*：激活标识。
- *start* 和 *end*：记录激活开始时间和结束时间的时间戳记。值为 [UNIX 时间格式](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15)。
- *namespace* 和 `name`：实体的名称空间和名称。
- *logs*：一组字符串，其中包含在操作激活期间由操作生成的日志。每组元素对应于操作向 `stdout` 或 `stderr` 生成的一行输出，并且包含日志输出的时间和流。结构如下：`TIMESTAMP STREAM: LOG_OUTPUT`。
- *response*：用于定义 `success`、`status` 和 `result` 键的字典：
  - *status*：激活结果，可能为以下某个值：“success”、“application error”、“action developer error”和“whisk internal error”。
  - *success*：当且仅当 status 为“`success`”时，此项为 `true`
- *result*：包含激活结果的字典。如果激活成功，那么此项包含操作返回的值。如果激活不成功，那么 `result` 会包含 `error` 键，通常还会带有失败说明。


## JavaScript 操作
{: #openwhisk_ref_javascript}

### 函数原型
{: #openwhisk_ref_javascript_fnproto}

{{site.data.keyword.openwhisk_short}} JavaScript 操作在 Node.js 运行时中运行。

用 JavaScript 编写的操作必须限制为单个文件。该文件可以包含多个函数，但根据约定，必须存在名为 `main` 的函数，并且此函数是调用操作时调用的函数。例如，下面是具有多个函数的操作的示例。

```
function main() {
    return { payload: helper() }
}

function helper() {
    return new Date();
}
```
{: codeblock}

操作输入参数会作为 JSON 对象传递到 `main` 函数。成功调用的结果也是 JSON 对象，但返回方式根据操作是同步还是异步而有所不同，如以下部分中所述。


### 同步和异步行为
{: #openwhisk_ref_javascript_synchasynch}

JavaScript 函数即便返回之后，仍在回调函数中继续执行是很常见的情况。要允许此操作，JavaScript 操作的激活可以是*同步*或*异步*的。

如果 main 函数在以下某个条件下退出，那么 JavaScript 操作的激活是**同步**的：

- main 函数在不执行 `return` 语句的情况下退出。
- main 函数通过执行 `return` 语句退出，此语句返回*除* Promise 以外的任何值。

下面是异步操作的示例。

```
// an action in which each path results in a synchronous activation
function main(params) {
  if (params.payload == 0) {
     return;
  } else if (params.payload == 1) {
     return {payload: 'Hello, World!'};
  } else if (params.payload == 2) {
    return {error: 'payload must be 0 or 1'};
  }
}
```
{: codeblock}

如果 main 函数通过返回 Promise 退出，那么 JavaScript 操作的激活是**异步**的。在此情况下，系统假定操作仍在运行，直到执行或拒绝 Promise 为止。通过实例化新 Promise 对象并向其传递回调函数开始。回调函数采用两个自变量 resolve 和 reject，这两个自变量都是函数。所有异步代码都会进入该回调函数。


以下示例显示如何通过调用 resolve 函数来履行 Promise。

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
        resolve({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

以下示例显示如何通过调用 reject 函数来拒绝 Promise。

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
        reject({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

一个操作可以在某些输入上是同步的，而在其他输入上是异步的。以下是一个示例。

```
  function main(params) {
      if (params.payload) {
         // asynchronous activation
         return new Promise(function(resolve, reject) {
                setTimeout(function() {
        resolve({ done: true });
                }, 100);
             })
      } else {
// synchronous activation
         return {done: true};
      }
  }
```
{: codeblock}

请注意，不管激活是同步还是异步的，操作的调用都可以是阻塞或非阻塞调用。

### JavaScript 全局 whisk 对象已除去

全局对象 `whisk` 已除去；请迁移 nodejs 操作以使用替代方法。对于函数 `whisk.invoke()` 和 `whisk.trigger()`，请使用已经安装的客户机库 [openwhisk](https://www.npmjs.com/package/openwhisk)。对于 `whisk.getAuthKey()`，可以从环境变量 `__OW_API_KEY` 中获取 API 密钥值。对于 `whisk.error()`，可以返回拒绝的 Promise（即 Promise.reject）。

### JavaScript 运行时环境
{: #openwhisk_ref_javascript_environments}

JavaScript 操作缺省情况下在 Node.js V6.9.1 环境中执行。如果在创建/更新操作时使用“nodejs:6”值明确指定 `--kind` 标记，那么 6.9.1 环境也将用于操作。
以下包可在 Node.js 6.9.1 环境中使用：

- apn v2.1.2
- async v2.1.4
- btoa v1.1.2
- cheerio v0.22.0
- cloudant v1.6.2
- commander v2.9.0
- consul v0.27.0
- cookie-parser v1.4.3
- cradle v0.7.1
- errorhandler v1.5.0
- glob v7.1.1
- gm v1.23.0
- lodash v4.17.2
- log4js v0.6.38
- iconv-lite v0.4.15
- marked v0.3.6
- merge v1.2.0
- moment v2.17.0
- mongodb v2.2.11
- mustache v2.3.0
- nano v6.2.0
- node-uuid v1.4.7
- nodemailer v2.6.4
- oauth2-server v2.4.1
- openwhisk v3.3.2
- pkgcloud v1.4.0
- process v0.11.9
- pug v2.0.0-beta6
- redis v2.6.3
- request v2.79.0
- request-promise v4.1.1
- rimraf v2.5.4
- semver v5.3.0
- sendgrid v4.7.1
- serve-favicon v2.3.2
- socket.io v1.6.0
- socket.io-client v1.6.0
- superagent v3.0.0
- swagger-tools v0.10.1
- tmp v0.0.31
- twilio v2.11.1
- underscore v1.8.3
- uuid v3.0.0
- validator v6.1.0
- watson-developer-cloud v2.29.0
- when v3.7.7
- winston v2.3.0
- ws v1.1.1
- xml2js v0.4.17
- xmlhttprequest v1.8.0
- yauzl v2.7.0


## Python 运行时环境
{: #openwhisk_ref_python_environments}

OpenWhisk 支持使用两种不同的运行时版本来运行 Python 操作。

### Python 3 操作

Python 3 操作是使用 Python 3.6.1 执行的。要使用此运行时，请在创建或更新操作时，指定 `wsk` CLI 参数 `--kind python:3`。
除了 Python 3.6 标准库外，以下包也可供 Python 操作使用。

- aiohttp v1.3.3
- appdirs v1.4.3
- asn1crypto v0.21.1
- async-timeout v1.2.0
- attrs v16.3.0
- beautifulsoup4 v4.5.1
- cffi v1.9.1
- chardet v2.3.0
- click v6.7
- cryptography v1.8.1
- cssselect v1.0.1
- Flask v0.12
- gevent v1.2.1
- greenlet v0.4.12
- httplib2 v0.9.2
- idna v2.5
- itsdangerous v0.24
- Jinja2 v2.9.5
- kafka-python v1.3.1
- lxml v3.6.4
- MarkupSafe v1.0
- multidict v2.1.4
- packaging v16.8
- parsel v1.1.0
- pyasn1 v0.2.3
- pyasn1-modules v0.0.8
- pycparser v2.17
- PyDispatcher v2.0.5
- pyOpenSSL v16.2.0
- pyparsing v2.2.0
- python-dateutil v2.5.3
- queuelib v1.4.2
- requests v2.11.1
- Scrapy v1.1.2
- service-identity v16.0.0
- simplejson v3.8.2
- six v1.10.0
- Twisted v16.4.0
- w3lib v1.17.0
- Werkzeug v0.12
- yarl v0.9.8
- zope.interface v4.3.3

### Python 2 操作

Python 2 操作是使用 Python 2.7.12 执行的。除非在创建或更新操作时指定 `--kind` 标志，否则这是 Python 操作的缺省运行时。要显式选择此运行时，请使用 `--kind python:2`。除了 Python 2.7 标准库外，以下包也可供 Python 2 操作使用。

- appdirs v1.4.3
- asn1crypto v0.21.1
- attrs v16.3.0
- beautifulsoup4 v4.5.1
- cffi v1.9.1
- click v6.7
- cryptography v1.8.1
- cssselect v1.0.1
- enum34 v1.1.6
- Flask v0.11.1
- gevent v1.1.2
- greenlet v0.4.12
- httplib2 v0.9.2
- idna v2.5
- ipaddress v1.0.18
- itsdangerous v0.24
- Jinja2 v2.9.5
- kafka-python v1.3.1
- lxml v3.6.4
- MarkupSafe v1.0
- packaging v16.8
- parsel v1.1.0
- pyasn1 v0.2.3
- pyasn1-modules v0.0.8
- pycparser v2.17
- PyDispatcher v2.0.5
- pyOpenSSL v16.2.0
- pyparsing v2.2.0
- python-dateutil v2.5.3
- queuelib v1.4.2
- requests v2.11.1
- Scrapy v1.1.2
- service-identity v16.0.0
- simplejson v3.8.2
- six v1.10.0
- Twisted v16.4.0
- virtualenv v15.1.0
- w3lib v1.17.0
- Werkzeug v0.12
- zope.interface v4.3.3

## Docker 操作
{: #openwhisk_ref_docker}

Docker 操作在 Docker 容器中运行用户提供的二进制文件。该二进制文件在基于 [python:2.7.12-alpine](https://hub.docker.com/r/library/python) 的 Docker 映像中运行，所以该二进制文件必须与此分发版兼容。

通过 Docker 框架，可以方便地构建兼容 OpenWhisk 的 Docker 映像。可以使用 `wsk sdk install docker` CLI 命令安装该框架。

主二进制程序必须位于容器内的 `/action/exec` 中。可执行文件通过可以反序列化为 `JSON` 对象的单个命令行自变量字符串来接收输入自变量。该文件必须通过 `stdout` 以单行序列化 `JSON` 字符串形式返回结果。

您可以通过修改 `dockerSkeleton` 中包含的 `Dockerfile` 来包含任何编译步骤或依赖关系。

## REST API
{: #openwhisk_ref_restapi}
有关 REST API 的信息位于[此处](openwhisk_rest_api.html)


## 系统限制
{: #openwhisk_syslimits}

### 操作
{{site.data.keyword.openwhisk_short}} 存在一些系统限制，包括一个操作可以使用的内存量和每分钟允许的操作调用数。

下表列出了操作的缺省限制。

| 限制 | 描述 | 可配置 | 单位 | 缺省值 |
| ----- | ----------- | ------------ | -----| ------- |
| timeout | 不允许容器运行时间超过 N 毫秒 | 每个操作 |  毫秒 | 60000 |
| memory | 不允许容器分配的内存超过 N MB | 每个操作 | MB | 256 |
| logs | 不允许容器向标准输出写入超过 N MB | 每个操作 | MB | 10 |
| concurrent | 每个名称空间中提交的正在执行或排队等待执行的激活数不得超过 N | 每个名称空间 | 个 | 1000 |
| minuteRate | 每个名称空间中每分钟提交的激活数不得超过 N | 每个用户 | 个 | 5000 |
| codeSize | 操作码的最大大小 | 无法配置，每个操作的限制 | MB | 48 |
| parameters | 可以附加的参数的最大大小 | 无法配置，每个操作/包/触发器的限制 | MB | 1 |

### 每个操作的超时（毫秒）（缺省值：60 秒）
{: #openwhisk_syslimits_timeout}
* 超时限制 N 在 [100ms..300000ms] 范围内，并且按每个操作进行设置，以毫秒为单位。
* 用户在创建操作时可以更改此限制。
* 将终止运行时间超过 N 毫秒的容器。

### 每个操作的内存 (MB)（缺省值：256MB）
{: #openwhisk_syslimits_memory}
* 内存限制 M 在 [128MB..512MB] 范围内，并且按每个操作进行设置，以 MB 为单位。
* 用户在创建操作时可以更改此限制。
* 一个容器分配的内存不能超过此限制。

### 每个操作的日志 (MB)（缺省值：10MB）
{: #openwhisk_syslimits_logs}
* 日志限制 N 在 [0MB..10MB] 范围内，并且按每个操作进行设置。
* 用户在创建或更新操作时可以更改此限制。
* 超过所设置限制的日志会被截断，且在激活的最后输出中会添加警告，指出激活超出所设置的日志限制。

### 每个操作工件 (MB)（固定值：48MB）
{: #openwhisk_syslimits_artifact}
* 操作的最大代码大小为 48MB。
* 建议 JavaScript 操作使用工具，将所有源代码（包括依赖关系）连接为单个捆绑文件。

### 每个激活有效内容大小 (MB)（固定值：1 MB）
{: #openwhisk_syslimits_activationsize}
* 最大 POST 内容大小加上用于操作调用或触发的任何加工参数等于 1 MB。

### 每个名称空间的并行调用数（缺省值：1000）
{: #openwhisk_syslimits_concur}
* 为一个名称空间正在执行或排队等待执行的激活数不能超过 1000。
* 缺省限制可以通过静态方式由 whisk 在 consul kvstore 中进行配置。
* 用户当前不能更改限制。

### 每分钟的调用数（固定值：5000）
{: #openwhisk_syslimits_invocations}
* 速率限制 N 设置为 5000，用于限制 1 分钟时段中的操作调用数。
* 用户在创建操作时不能更改此限制。
* 超过此限制的 CLI 或 API 调用将收到与 HTTP 状态码“`429：请求过多`”对应的错误代码。

### 参数的大小（固定值：1MB）
{: #openwhisk_syslimits_parameters}
* 创建或更新操作/包/触发器的参数大小限制为 1MB。
* 用户无法更改此限制。
* 尝试创建或更新具有超大参数的实体时，会遭到拒绝。

### 每个 Docker 操作打开文件数 ulimit（固定值：64:64）
{: #openwhisk_syslimits_openulimit}
* 打开文件的最大数目为 64（同时适用于硬限制和软限制）。
* docker run 命令使用自变量 `--ulimit nofile=64:64`。
* 有关打开文件数 ulimit 的更多信息，请参阅 [docker run](https://docs.docker.com/engine/reference/commandline/run) 文档。

### 每个 Docker 操作进程数 ulimit（固定值：512:512）
{: #openwhisk_syslimits_proculimit}
* 用户可用的最大进程数为 512（同时适用于硬限制和软限制）。
* docker run 命令使用自变量 `--ulimit nproc=512:512`。
* 有关最大进程数 ulimit 的更多信息，请参阅 [docker run](https://docs.docker.com/engine/reference/commandline/run) 文档。

### 触发器

触发器受每分钟触发率的影响，如下表中所述。

| 限制 | 描述 | 可配置 | 单位 | 缺省值 |
| ----- | ----------- | ------------ | -----| ------- |
| minuteRate | 每个名称空间中每分钟触发的触发器数不得超过 N | 每个用户 | 个 | 5000 |

### 每分钟的触发数（固定值：5000）
* 速率限制 N 设置为 5000，用于限制 1 分钟时段中可能触发的触发器数。
* 用户在创建触发器时不能更改此限制。
* 超过此限制的 CLI 或 API 调用将收到与 HTTP 状态码“`429：请求过多`”对应的错误代码。
