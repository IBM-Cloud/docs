---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 配置选项
{: #configuration_options}
{: shortdesc}

有各种选项可用于配置 sdk-for-nodejs buildpack。

## NPM 脚本
{: #npm_scripts}
NPM 提供了脚本编制功能，允许您运行脚本，其中包括分别适用于 node_modules 安装前后的 **preinstall** 和 **postinstall** 脚本。有关完整详细信息，请参阅 [npm-scripts ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.npmjs.com/misc/scripts)。

## 高速缓存行为
{: #cache_behavior}
{{site.data.keyword.Bluemix}} 为每个节点应用程序保留一个高速缓存目录，并且将在构建之间持久存储该目录。高速缓存会存储解析的依赖项，这样每次部署应用程序时就不需要再下载和安装这些依赖项。例如，假设 myapp 依赖于 **express**。那么第一次部署 myapp 时会下载 **express** 模块。在后续部署 myapp 时，会使用高速缓存的 **express** 实例。缺省行为是对 NPM 安装的所有 node_modules 以及 bower 安装的 bower_components 进行高速缓存。

使用 NODE_MODULES_CACHE 变量来确定 Node buildpack 是使用还是忽略先前构建的高速缓存。缺省值为 true。要禁用高速缓存，请将 NODE_MODULES_CACHE 设置为 false，例如，通过 cf 命令行：

```
$ cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

请注意，不会高速缓存应用程序中包含的 node_modules。

可使用顶层 **package.json** 中的 **cacheDirectories** 数组，以精确控制将哪些模块高速缓存。当 **cacheDirectories** 元素显示在 **package.json** 中时，仅高速缓存位于 **cacheDirectories** 数组中的那些模块。在以下示例中，仅高速缓存 node_modules 和 bower_components。

```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}
