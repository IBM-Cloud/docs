---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}

#  Bluemix 基础架构层

*上次更新时间：2016 年 3 月 15 日*

{{site.data.keyword.Bluemix_notm}} 抽象化并隐藏操作系统和基础架构层，这样您就无需对这些内容进行管理。但是，有时您可能希望了解有关应用程序的操作系统和中间件的更多信息。
{:shortdesc}

## 查看 Bluemix 基础架构层
{:viewinfra}

可以运行 cf stacks 命令来显示要将应用程序部署到其中的可用堆栈或根文件系统。还可以指定堆栈，方法是在运行 cf push 命令时使用 *-s* 选项和 *stack_name*，其中 stack_name 是根文件系统，例如 `lucid64` 或 `cflinuxfs2`：
```
cf push appName -s stack_name
```
可以使用 `cf buildpacks` 命令来显示作为运行时提供的供应用程序在其中运行的中间件组件，例如 WebSphere Liberty 概要文件和 SDK for Node.js。此外，可以使用以下命令来指定应用程序的运行时环境：
```
cf push appName -b buildpackname
```
