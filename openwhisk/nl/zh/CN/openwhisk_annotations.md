---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# OpenWhisk 资产上的注释

OpenWhisk 操作、触发器、规则和包（统称为“资产”）可以使用`注释`进行装饰。注释附加到资产，就像用 `key` 定义名称，用 `value` 定义值的参数一样。在命令行界面 (CLI) 中通过 `--annotation`（或缩写命令 `-a`）可方便地对其进行设置。
{: shortdesc}

理由：向 OpenWhisk 添加注释是考虑在不更改底层资产模式的情况下进行试验。在编写本文档之前，我们一直有意地不定义允许使用哪些`注释`。然而，随着我们开始更偏重于将注释用于传递语义变化，最终我们需要着手将其记录下来。

目前，注释的最普遍用法是记录操作和包。您将看到 OpenWhisk 目录中有许多包带有注释，例如对其操作提供的功能的描述，在包绑定时哪些参数是必需的，哪些是调用时参数，以及参数是否为“秘密信息”（例如，密码）。我们已根据需要创造了这些注释，例如用于允许 UI 集成。

下面是针对 `echo` 操作的一组注释样本，此操作会将其输入自变量不加修改地返回（例如，`function main(args) { return args }`）。此操作可用于对输入参数进行日志记录（例如，作为某个序列或规则的一部分）。

```
wsk action create echo echo.js \
    -a description 'An action which returns its input. Useful for logging input to enable debug/replay.' \
    -a parameters  '[{ "required":false, "description": "Any JSON entity" }]' \
    -a sampleInput  '{ "msg": "Five fuzzy felines"}' \
    -a sampleOutput '{ "msg": "Five fuzzy felines"}'
```
{: pre}

我们已用于描述包的注释包括：

- `description`：对该包的精简描述
- `parameters`：一个数组，用于描述范围限定为该包的参数（下面将进一步描述）

与此类似，用于操作的注释包括： 

- `description`：对该操作的精简描述
- `parameters`：一个数组，用于描述执行该操作所需的操作
- `sampleInput`：一个示例，显示使用典型值的输入模式
- `sampleOutput`：一个示例，显示输出模式，通常用于 `sampleInput`

我们已用于描述参数的注释包括：

- `name`：该参数的名称
- `description`：对该参数的精简描述
- `doclink`：一个链接，指向该参数的进一步文档（例如，对于 OAuth 令牌很有用） 
- `required`：对于必需参数为 true，对于可选参数为 false
- `bindTime`：如果该参数应该在绑定包时指定，那么为 true
- `type`：该参数的类型，为 `password` 或 `array`（但可以有更广的用法）

*不会*对注释进行检查。所以，例如完全可以使用注释来推断两个操作组合成一个序列是否合法，但系统目前还不会这样做。

## 特定于 Web 操作的注释
{: #openwhisk_annotations_webactions}

最近，我们使用新功能扩展了核心 API。为了支持包和操作参与这些功能，我们引入了在语义上有意义的以下新注释。这些注释必须显式设置为 `true` 才能生效。如果将值从 `true` 更改为 `false`，会将连接的资产排除在新 API 之外。这些注释在系统中并无其他意义。这些注释包括：

- `final`：仅应用于操作。它会使已经定义的所有操作参数无法改变。带有此注释的操作的参数一旦通过其封装包或操作定义来定义了值，即无法通过调用时参数进行覆盖。
- `web-export`：仅应用于操作。如果出现此注释，它会使其对应操作可供 REST 调用访问，而*无需*认证。例如，我们调用这些 [*Web 操作*](openwhisk_webactions.html)是因为它们允许用户通过浏览器使用 OpenWhisk 操作。需要注意的是，Web 操作的*所有者*在系统中运行这些操作时会产生开销（即，操作的*所有者*同时拥有激活记录）。
- `require-whisk-auth`：应用于操作。如果操作执行 `web-export` 注释，并且此注释也为 `true`，那么只有经认证的主体才可访问该路径。需要注意的是，Web 操作的*所有者*在系统中运行这些操作时会产生开销（即，操作的*所有者*同时拥有激活记录）。
- `raw-http`：仅在出现 `web-export` 注释时应用于操作。如果出现该注释，HTTP 请求查询和主体参数将作为保留的属性传递到操作。

