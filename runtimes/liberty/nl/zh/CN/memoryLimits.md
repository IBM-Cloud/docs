---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-18"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 内存限制和 Liberty buildpack
{: #memory_limits}

使用 Liberty buildpack 部署应用程序时，必须指定内存限制。

## 避免故障

内存限制为 256 MB 时，使用 Liberty buildpack 部署的“Hello World”servlet 可能无法正确部署并运行。如果部署了此 servlet，那么其运行时占用的内存会接近 256M 的限制。即使对于简单应用程序，也请考虑至少为“内存限制”指定 512M。

## 内存限制和 Liberty buildpack
{: #memory_limits_and_liberty}


使用 Liberty buildpack 部署应用程序时，会提示您输入“内存限制”。

要确定指定多大的“内存限制”，请务必了解您并不是在指定 Java 应用程序堆的大小。您要指定的是整个进程可使用的内存量。此内存量包括以下组件使用的内存：

* Warden 容器使用的内存。
* 用于将内核扩展和系统库映射到进程的内存。
* 用于 jvm 可执行文件、jvm 工作堆、jit 空间和压缩引用的内存。
* 用于类（应用程序服务器和应用程序）、线程堆栈并定向到缓冲区的内存。
* Java 应用程序堆使用的内存。

有关 JVM 内存使用量的更多信息，请查看 developerWorks 文章：[Thanks for the memory](http://www.ibm.com/developerworks/library/j-nativememory-linux/)

部署应用程序时，将监视整个进程的内存使用量。如果内存使用量超出部署该应用程序指定的内存限制，那么内核会停止进程。此操作发生时不会有警告，可能通过以下方式体现：

* 如果应用程序部署期间超出“内存限制”，您会收到发生故障的消息。您可能会看到应用程序不太稳定。还可能会看到应用程序多次尝试启动，但始终不成功。或者，可能会收到一条消息，指示应用程序部署失败。
* 如果应用程序正在运行时超出“内存限制”，那么进程会停止。Cloud Foundry 会尝试重新启动应用程序。应用程序可能会重新启动，但在一段时间内不可用。

## 指定堆内存
{: #specifying_heap_memory}

可以通过各种方式定制分配给应用程序的最大堆内存量。

*  使用 JVM_ARGS 环境变量和 -Xmx 自变量。例如，要将最大堆大小设置为 512M，请使用以下命令，然后重新编译打包应用程序。

```
    $ cf set-env myapp JVM_ARGS -Xmx512m
```
{: codeblock}

* 如果应用程序为[服务目录](optionsForPushing.html#server_directory)或[打包服务器](optionsForPushing.html#packaged_server)，那么可以在 jvm.options 文件中指定 -Xmx 自变量。

* 可以使用 JBP_CONFIG_IBMJDK 环境变量来指定堆大小比率。heap_size_ratio 是浮点值，指定可分配给堆的可用内存量。例如，要将一半可用内存分配给堆，请发出以下命令，然后重新编译打包应用程序。

```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "heap_size_ratio: 0.50"
```
{: codeblock}
