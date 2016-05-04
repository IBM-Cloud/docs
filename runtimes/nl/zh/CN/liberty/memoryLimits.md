---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 内存限制和 Liberty buildpack
{: #memory_limits}

*上次更新时间：2016 年 3 月 23 日*

使用 Liberty buildpack 部署应用程序时，必须指定内存限制。

**避免故障**

* 内存限制为 256 MB 时，使用 Liberty buildpack 部署的“Hello World”servlet 可能无法正确部署并运行。如果部署了此 servlet，那么其运行时占用的内存会接近 256M 的限制。即使对于简单应用程序，也请考虑至少为“内存限制”指定 512M。

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

# 相关链接
## 常规
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
