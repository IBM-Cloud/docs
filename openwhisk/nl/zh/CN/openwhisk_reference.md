---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 系统详细信息
{: #openwhisk_reference}
*上次更新时间：2016 年 4 月 14 日*

以下各部分提供了有关 {{site.data.keyword.openwhisk}} 系统的更多详细信息。
{: shortdesc}

## {{site.data.keyword.openwhisk_short}} 实体
{: #openwhisk_entities}

### 名称空间和包

{{site.data.keyword.openwhisk_short}} 操作、触发器和规则属于名称空间，并可选择属于包。

包可以包含操作和订阅源。一个包不能包含其他包，所以不允许包嵌套。此外，实体不必包含在包中。

在 Bluemix 中，组织+空间对与 {{site.data.keyword.openwhisk_short}} 名称空间相对应。例如，组织 `BobsOrg` 和空间 `dev` 将对应于 {{site.data.keyword.openwhisk_short}} 名称空间 `/BobsOrg_dev`。

如果您有权创建名称空间，那么可以创建自己的名称空间。`/whisk.system` 名称空间保留用于使用 {{site.data.keyword.openwhisk_short}} 系统分发的实体。


### 标准名称

实体的标准名称为 `/namespaceName[/packageName]/entityName`。请注意，`/` 用于对名称空间、包和实体定界。此外，名称空间必须带有前缀 `/`。

为了方便起见，如果名称空间是用户的 *缺省名称空间*，那么可以保留不变。

例如，假设用户的缺省名称空间为 `/myOrg`。下面是一些实体的标准名称及其别名的示例。

| 标准名称 | 别名 | 名称空间 | 包 | 名称 |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` | - | `/whisk.system` | `cloudant` | `read` |
| `/myOrg/video/transcode` | `video/transcode` | `/myOrg` | `video` | `transcode` |
| `/myOrg/filter` | `filter` | `/myOrg` | - | `filter` |

使用 {{site.data.keyword.openwhisk_short}} CLI 时，您将使用此命名方案，在其他位置也同样遵循此方案。

### 实体名称

包括操作、触发器、规则、包和名称空间在内的所有实体的名称均为遵循以下格式的字符序列：

* 第一个字符必须为字母数字字符、数字或下划线。
* 后续字符可以为字母数字、数字、空格或以下任一字符：`_`、`@`、`.` 和 `-`。
* 最后一个字符不能为空格。

更准确地说，名称必须匹配以下正则表达式（使用 Java 元字符语法表达）：`\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`。


## 操作语义
{: #openwhisk_semantics}

以下各部分描述了有关 {{site.data.keyword.openwhisk_short}} 操作的详细信息。

### 无状态

操作实施应该是无状态的，即*幂等*。虽然系统不会强制执行此属性，但不保证操作保持的任何状态在各调用中均可用。

此外，一个操作可能存在多个实例化，其中每个实例化都有其自己的状态。可能会将操作调用分派给其中任一实例化。

### 调用输入和输出

操作的输入和输出是键/值对的字典。键为字符串，值为有效的 JSON 值。

### 操作的调用顺序
{: #openwhisk_ordering}

操作的调用并未排序。如果用户通过命令行或 REST API 调用一个操作两次，那么第二个调用可能会先于第一个调用运行。如果操作有副作用，那么可能会以任意顺序观察到这些副作用。

此外，不保证操作以原子方式执行。两个操作可以并行运行，其副作用可能会交错。任何并行副作用都将依赖于实施。

### 至多一次语义
{: #openwhisk_atmostonce}

系统支持对操作执行至多一次调用。

收到调用请求时，系统会记录该请求，并分派激活。

系统会返回激活标识（对于非阻塞调用），以确认收到了调用。请注意，即便缺少此响应（可能是因为网络连接中断），也可能会收到调用。

系统尝试调用操作一次，产生以下四个结果之一：
- *success*：操作调用成功完成。
- *application error*：操作调用成功，但操作有意返回了错误值，例如由于不满足自变量上的前置条件。
- *action developer error*：操作已调用，但以异常方式完成，例如操作未捕捉到异常或存在语法错误。
- *whisk internal error*：系统无法调用操作。
结果会记录在激活记录的 `status` 字段中，如以下部分中所述。

成功收到的每个调用以及可能对用户记帐的每个调用最终都将具有激活记录。


## 激活记录
{: #openwhisk_ref_activation}

每次操作调用和触发器触发都会产生一个激活记录。

激活记录包含以下字段：

- *activationId*：激活标识。
- *start* 和 *end*：记录激活开始时间和结束时间的时间戳记。值为 [UNIX 时间格式](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15)。
- *namespace* 和 `name`：实体的名称空间和名称。
- *logs*：字符串数组，其中包含在操作激活期间由操作生成的日志。每个数组元素对应于操作向 stdout 或 stderr 生成的一行输出，并且包含日志输出的时间和流。结构如下所示：“`TIMESTAMP STREAM: LOG_OUTPUT`”。
- *response*：用于定义 `success`、`status` 和 `result` 键的字典：
  - *status*：激活结果，可能为以下某个值：“success”、“application error”、“action developer error”和“whisk internal error”。
  - *success*：当且仅当 status 为“`success`”时，此项为 `true`
- *result*：包含激活结果的字典。如果激活成功，那么此项包含操作返回的值。如果激活不成功，那么会保证 `result` 包含 `error` 键，通常还会带有失败说明。


## JavaScript 操作
{: #openwhisk_ref_javascript}

### 函数原型

{{site.data.keyword.openwhisk_short}} JavaScript 操作在 Node.js 运行时中运行，此运行时当前版本为 V0.12.9。

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

JavaScript 函数即便返回之后，仍在回调函数中继续执行是很常见的情况。要允许此操作，JavaScript 操作的激活可以是*同步*或*异步*的。

如果 main 函数在以下某个条件下退出，那么 JavaScript 操作的激活是**同步**的：

- main 函数在不执行“`return`”语句的情况下退出。
- main 函数通过执行“`return`”语句退出，此语句返回*除*“`whisk.async()`”以外的任何值。

下面是同步操作的两个示例。

```
// a synchronous action
function main() {
  return {payload: 'Hello, World!'};
}
```
{: codeblock}

```
// an action in which each path results in a synchronous activation
function main(params) {
  if (params.payload == 0) {
     return;
  } else if (params.payload == 1) {
     return whisk.done();    // indicates normal completion
  } else if (params.payload == 2) {
    return whisk.error();   // indicates abnormal completion
  }
}
```
{: codeblock}

如果 main 函数通过调用“`return whisk.async();`”退出，那么 JavaScript 操作的激活是**异步**的。在此情况下，系统假定操作仍在运行，直到操作执行以下某个语句为止：
- “`return whisk.done();`”
- “`return whisk.error();`”

下面是异步执行的操作的示例。

```
function main() {
    setTimeout(function() {
        return whisk.done({done: true});
    }, 100);
    return whisk.async();
}
```
{: codeblock}

一个操作可以在某些输入上是同步的，而在其他输入上是异步的。下面是一个示例。

```
  function main(params) {
      if (params.payload) {
         setTimeout(function() {
            return whisk.done({done: true});
         }, 100);
         return whisk.async();  // asynchronous activation
      }  else {
         return whisk.done();   // synchronous activation
      }
  }
```
{: codeblock}

- 在此情况下，`main` 函数应该返回 `whisk.async()`。激活结果可用时，应该会调用 `whisk.done()` 函数，并且结果会作为 JSON 对象传递。这称为*异步*激活。

请注意，不管激活是同步还是异步的，操作的调用都可以是阻塞或非阻塞调用。

### 其他 SDK 方法

`whisk.invoke()` 函数会调用其他操作。它会接受定义以下参数的字典作为自变量：

- *name*：要调用的操作的标准名称。
- *parameters*：表示所调用操作的输入的 JSON 对象。如果省略，缺省值为空对象。
- *apiKey*：用于调用操作的授权密钥。缺省值为 `whisk.getAuthKey()`。 
- *blocking*：操作应该以阻塞还是非阻塞方式调用。缺省值为 `false`，指示非阻塞调用。
- *next*：调用完成时要执行的可选回调函数。

`next` 的特征符为 `function(error, activation)`，其中：

- 如果调用成功，那么 `error` 为 `false`，如果调用失败，那么为表示真实性的值，通常是描述错误的字符串。
- 出错时，`activation` 可能未定义，具体取决于失败方式。
- 定义时，`activation` 是包含以下字段的字典：
  - *activationId*：激活标识。
  - *result*：如果操作是以阻塞方式调用的，操作结果为 JSON 对象，否则为 `undefined`。

`whisk.trigger()` 函数会触发触发器。它会接受带有以下参数的 JSON 对象作为自变量：

- *name*：要调用的触发器的标准名称。
- *parameters*：表示触发器的输入的 JSON 对象。如果省略，缺省值为空对象。
- *apiKey*：用于触发触发器的授权密钥。缺省值为 `whisk.getAuthKey()`。
- *next*：触发完成时要执行的可选回调。

`next` 的特征符为 `function(error, activation)`，其中：

- 如果触发成功，那么 `error` 为 `false`，如果触发失败，那么为表示真实性的值，通常是描述错误的字符串。
- 出错时，`activation` 可能未定义，具体取决于失败方式。
- 定义时，`activation` 是带有 `activationId` 字段（包含激活标识）的字典。

`whisk.getAuthKey()` 函数将返回当前运行操作所使用的授权密钥。通常，无需直接调用此函数，因为它由 `whisk.invoke()` 和 `whisk.trigger()` 函数隐式使用。

### 运行时环境
{: #openwhisk_ref_runtime_environment}

JavaScript 操作在 Node.js V0.12.9 环境中执行，带有可供操作使用的以下包：

- apn
- async
- body-parser
- btoa
- cloudant
- commander
- consul
- cookie-parser
- cradle
- errorhandler
- express
- express-session
- jade
- log4js
- merge
- moment
- mustache
- nano
- node-uuid
- oauth2-server
- process
- request
- rimraf
- semver
- serve-favicon
- socket.io
- superagent
- swagger-tools
- tmp
- watson-developer-cloud
- when
- xml2js
- xmlhttprequest
- yauzl


## Docker 操作
{: #openwhisk_ref_docker}

Docker 操作在 Docker 容器中运行用户提供的二进制文件。该二进制文件在基于 Ubuntu 14.04 LTD 的 Docker 映像中运行，所以该二进制文件必须与此分发版兼容。

操作输入“payload”参数会作为位置参数传递给二进制程序，并且在“result”参数中会返回执行该程序生成的标准输出。

通过 Docker 框架，可以方便地构建兼容 {{site.data.keyword.openwhisk_short}} 的 Docker 映像。可以使用 `wsk sdk install docker` CLI 命令安装该框架。

主二进制程序应该复制到 `dockerSkeleton/client/clientApp` 文件。任何附带文件或库都可以位于 `dockerSkeleton/client` 目录中。

您还可以通过修改 `dockerSkeleton/Dockerfile` 来包含任何编译步骤或依赖关系。例如，如果操作是 Python 脚本，那么可以安装 Python。


## 系统限制
{: #openwhisk_syslimits}

{{site.data.keyword.openwhisk_short}} 存在一些系统限制，包括一个操作使用的内存量和每小时允许的操作调用数。下表列出了缺省限制。

| 限制 | 描述 | 可配置 | 单位 | 缺省值 |
| ----- | ----------- | ------------ | -----| ------- |
| timeout | 不允许容器运行时间超过 N 毫秒 | 每个操作 |  毫秒 | 60000 |
| memory | 不允许容器分配的内存超过 N MB | 每个操作 | MB | 256 |
| concurrent | 不允许每个名称空间的并行激活数超过 N 个 | 每个名称空间 | 个 | 100 |
| minuteRate | 用户每分钟调用的操作数不能超过此值 | 每个用户 | 个 | 120 |
| hourRate | 用户每小时调用的操作数不能超过此值 | 每个用户 | 个 | 3600 |

### 每个操作的超时（毫秒）（缺省值：60 秒）
* 超时限制 N 在 [100ms..300000ms] 范围内，并且按每个操作进行设置，以毫秒为单位。
* 用户在创建操作时可以更改此限制。
* 将终止运行时间超过 N 毫秒的容器。

### 每个操作的内存 (MB)（缺省值：256MB）
* 内存限制 M 在 [128MB..512MB] 范围内，并且按每个操作进行设置，以 MB 为单位。
* 用户在创建操作时可以更改此限制。
* 一个容器分配的内存不能超过此限制。

### 每个名称空间的并行调用数（个）（缺省值：100）
* 当前为一个名称空间处理的激活数不能超过 100。
* 缺省限制可以通过静态方式由 whisk 在 consul kvstore 中进行配置。
* 用户当前不能更改限制。


### 每分钟/小时的调用数（个）（固定值：120/3600）
* 速率限制 N 设置为 120/3600，用于限制 1 分钟/小时时段中的操作调用数。
* 用户在创建操作时不能更改此限制。
* 超过此限制的 CLI 调用将收到与 TOO_MANY_REQUESTS 对应的错误代码。
