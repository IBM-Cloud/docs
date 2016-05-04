---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 定制 JRE
{: #customizing_jre}

*上次更新时间：2016 年 3 月 23 日*

应用程序在 Liberty buildpack 提供和配置的 Java 运行时环境 (JRE) 中运行。通过 Liberty buildpack，还可以配置 JRE 版本或类型，定制 JVM 选项或覆盖 JRE 功能。

## IBM JRE

缺省情况下，应用程序配置为使用 IBM JRE 的轻量级版本运行。此轻量级 JRE 已精简为只提供必要的核心功能，使用的磁盘和内存占用量都大幅减少。有关轻量级 JRE 内容的更多信息，请参阅 [Liberty for Java 运行时](http://download.boulder.ibm.com/ibmdl/pub/software/dw/jdk/docs/bluemix/libertyforjava_jre.doc.html)。

缺省情况下，将使用 IBM JRE V8。使用 JBP_CONFIG_IBMJDK 环境变量可指定 IBM JRE 的替代版本。例如，要使用最新版本的 IBM JRE 7.1，请设置以下环境变量：
```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "version: 1.7.+"
```
{: #codeblock}

version 属性可以设置为版本范围。支持两种版本范围：1.7.+ 和 1.8.+。为了获得最佳结果，请使用 Java 8。

## OpenJDK
{: #openjdk}

（可选）应用程序可以配置为以 OpenJDK 作为 JRE 来运行。要启用应用程序以使用 OpenJDK 运行，请将 JVM 环境变量设置为“openjdk”。例如，使用 cf 命令行工具运行以下命令：
```
    $ cf set-env myapp JVM 'openjdk'
```
{: #codeblock}

如果启用，缺省情况下，将使用 OpenJDK V8。使用 JBP_CONFIG_OPENJDK 环境变量可指定 OpenJDK 的替代版本。例如，要使用最新版本的 OpenJDK 7，请设置以下环境变量：
```
    $ cf set-env myapp JBP_CONFIG_OPENJDK "version: 1.7.+"
```
{: #codeblock}

version 属性可以设置为版本范围（例如，1.7.+）或[可用 OpenJDK 版本列表](https://download.run.pivotal.io/openjdk/lucid/x86_64/index.yml)上列出的任何特定版本。为了获得最佳结果，请使用 Java 8。

## 配置 JRE 选项
{: #configuring_jre}

### JVM 缺省配置
{: #jvm_default_config}

Liberty buildpack 在配置缺省 JVM 选项时会考虑以下内容：

* 应用程序的内存限制。所应用的 JVM 堆设置的计算依据是：
  * 应用程序的内存限制，如[内存限制和Liberty buildpack](memoryLimits.html#memory_limits) 中所述
  * JRE 类型（因为 JVM 的堆相关选项随 JRE 支持的选项不同而不同）。

* [Bluemix 中支持的 Liberty 功能](libertyFeatures.html#libertyfeatures)。
  * Bluemix 中不支持两阶段落实全局数据库事务，因此已通过设置 -Dcom.ibm.tx.jta.disable2PC=true 禁用该功能。

* Bluemix 环境。

    配置 JVM 选项的目的是优化 Bluemix 环境并协助诊断与内存相关的错误状况。
  * 通过在应用程序内存耗尽时禁用 JVM 转储选项和终止进程来配置应用程序的快速故障恢复。
  * 虚拟化调整（仅限 IBM JRE）。
  * 将发生故障时应用程序的可用内存资源相关信息路由到 Loggregator。
  * 如果应用程序已配置为启用 JVM 内存转储，那么会禁用 Java 进程终止功能，并会将 JVM 内存转储路由到通用应用程序“dumps”目录。然后，可以从 Bluemix 仪表板或 CF CLI 来查看这些转储。

下面是缺省 JVM 配置的示例，它是由 buildpack 为具有 512M 内存限制的已部署应用程序生成的：
```
    -Xtune:virtualized
    -Xmx384M
    -Xdump:none
    -Xdump:heap:defaults:file=../../../../../dumps/heapdump.%Y%m%d.%H%M%S.%pid.%seq.phd
    -Xdump:java:defaults:file=../../../../../dumps/javacore.%Y%m%d.%H%M%S.%pid.%seq.txt
    -Xdump:snap:defaults:file=../../../../../dumps/Snap.%Y%m%d.%H%M%S.%pid.%seq.trc
    -Xdump:tool:events=systhrow,filter=java/lang/OutOfMemoryError,request=serial+exclusive,exec=../../../../.buildpack-diagnostics/killjava.sh
    -Dcom.ibm.tx.jta.disable2PC=true
```
{: #codeblock}

### 定制 JVM 配置
{: #customizing_jvm}

应用程序可以使用为该应用程序配置的 JRE 所定义的规范来定制 JVM 选项。请直接参考 JRE 文档中有关如何指定选项及其用法的指导，因为选项随 JRE 不同而不同。

<table>
<tr>
<th align="left">JRE</th>
<th align="left">命令行选项格式</th>
<th align="left">参考信息</th>
</tr>

<tr>
<td>IBM JRE</td>
<td>包含运行时选项（前缀为 -X），任何 Java 系统属性（前缀为 -D），不建议随意使用 -XX（这些选项可能会更改）</td>
<td>[V8 命令行选项](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.lnx.80.doc/diag/appendixes/cmdline/cmdline.html)，[V7 命令行选项](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/diag/appendixes/cmdline/cmdline.html)
</td>
</tr>

<tr>
<td> OpenJDK</td>
<td>基于 HotSpot 运行时，其中包含 -X（表示非标准）、-XX（表示开发者选项）符号表示法，以及用于启用或禁用该选项的布尔标志</td>
<td>[HotSpot 运行时概述](http://openjdk.java.net/groups/hotspot/docs/RuntimeOverview.html)</td>
</tr>
</table>

需要定制 JVM 选项的应用程序可以将该选项设置为 Bluemix 中的环境变量 IBM_JAVA_OPTIONS、JAVA_OPTS 或 JVM_ARGS 其中某一个的值。有关如何设置应用程序的环境变量的信息，请参阅“环境变量”部分。打包服务器或服务器目录还可以包含含有命令行选项的 jvm.options 文件，而不设置环境变量。

将 JVM 选项应用到 JRE 时，会先应用 Liberty buildpack 的缺省选项，然后应用定制选项。以特定顺序附加定制选项，即表中列出的顺序。选项的优先顺序是由应用 Java 选项的顺序所定义的。最后应用的选项的优先顺序高于之前应用的选项。

注：某些选项只有在代理程序触发选项后才会生效。

<table>
<tr>
<th align="left">应用的顺序</th>
<th align="left">应用程序 JVM 选项设置</th>
<th align="left">描述</th>
<th align="left">支持的应用程序类型</th>
<th align="left">更新已部署应用程序的 JVM 选项</th>
<th align="left">适用于 OpenJDK JRE</th>
</tr>

<tr>
<td>1</td>
<td>IBM_JAVA_OPTIONS</td>
<td>IBM JRE 支持的环境变量</td>
<td>所有</td>
<td>重新启动或重新编译打包应用程序</td>
<td>否</td>
</tr>

<tr>
<td>2</td>
<td>JAVA_OPTS</td>
<td>通过 Liberty buildpack Java 选项框架使用的环境变量</td>
<td>所有</td>
<td>重新编译打包应用程序</td>
<td>是</td>
</tr>

<tr>
<td>3</td>
<td>jvm.options</td>
<td>Liberty 运行时打包服务器或服务器目录支持的 JVM 配置文件</td>
<td>服务器软件包</td>
<td>重新编译打包应用程序</td>
<td>是</td>
</tr>

<tr>
<td>4</td>
<td>JVM_ARGS</td>
<td>Liberty 运行时支持的环境变量</td>
<td>所有</td>
<td>重新启动或重新编译打包应用程序</td>
<td>是</td>
</tr>
</table>

### 确定运行中应用程序的已应用 JVM 选项
{: #determining_applied_jvm_options}

除了使用 JVM_ARGS 环境变量指定的应用程序定义选项之外，生成的选项还会以下列形式持久存储在运行时环境中：作为命令行选项（独立 Java 应用程序）或位于 jvm.options 文件中（非独立 Java 应用程序）。针对应用程序应用的 JVM 选项可以从 Bluemix 仪表板或 CF CLI 进行查看。

独立 Java 应用程序的 JVM 选项会持久存储为命令行选项。可在 staging_info.yml 文件中查看这些选项。
```
    $ cf files myapp staging_info.yml
```
{: #codeblock}

用于 WAR、EAR、服务器目录和打包服务器部署的 JVM 选项会持久存储在 jvm.options 文件中。

要查看 jvm.options 文件中的 WAR、EAR 和服务器目录，请运行以下命令：
```
    $ cf files myapp app/wlp/usr/servers/defaultServer/jvm.options
```
{: #codeblock}

要查看 jvm.options 文件中的打包服务器，请将 &lt;serverName> 替换为您服务器的名称，并运行以下命令：
```
    $ cf files myapp app/wlp/usr/servers/<serverName>jvm.options
```
{: #codeblock}

#### 用法示例
{: #example_usage}

使用定制 JVM 选项部署应用程序以启用 IBM JRE JVM 详细垃圾回收日志记录：
* 应用程序的 manifest.yml 文件中包含的 JVM 选项：
```
    env:
      JAVA_OPTS: "-verbose:gc -Xverbosegclog:./verbosegc.log,10,1000"
```
{: #codeblock}

* 查看所生成的 JVM 详细垃圾回收日志记录：
```
    $ cf files myapp app/wlp/usr/servers/defaultServer/verbosegc.log.001
```
{: #codeblock}    

* 更新已部署应用程序的 IBM JRE JVM 选项以在发生 OutOfMemory（内存不足）状况时触发 heap、snap 和 javacore：

使用 JVM 选项设置应用程序的环境变量，然后重新启动应用程序：
```
    $ cf set-env myapp JVM_ARGS '-Xdump:heap+java+snap:events=systhrow,filter=java/lang/OutOfMemoryError'
    $ cf restart myapp
```
{: #codeblock}

* 查看触发内存不足状况时所生成的 JVM 转储：
```
    $ cf files myapp dumps

    Getting files for app myapp in org myemail@email.com / space dev as myemail@email.com...
    OK

    Snap.20141106.100252.81.0003.trc           307.3K
    heapdump.20141106.100252.81.0001.phd       3.9M
    javacore.20141106.100252.81.0002.txt     870.5K
```
{: #codeblock}

### 覆盖 JRE
{: #overlaying_jre}

有一些情况需要将多个文件与 JRE 捆绑以公开它们的功能。应用程序开发者可以提供 JRE 文件以供定制。

可以在归档根目录的 resources 文件夹中使用应用程序 WAR、EAR 或 JAR 打包要覆盖的文件。对于服务器（压缩文件或服务器目录），可以使用 server.xml 文件在服务器目录的 resources 文件夹中打包那些文件。

* WAR file
  * WEB-INF
  * resources
    * other files
    * .java-overlay


* EAR file
  * META-INF
  * resources
    * other files
    * .java-overlay


* JAR file
  * META-INF
  * resources
    * other files
    * .java-overlay


* server_name DIR
  * apps
  * dropins
  * server.xml
  * resources
    * other files
    * .java-overlay

.java-overlay 目录包含特定的文件，这些文件的文件层次结构与要覆盖的 Java JRE 的文件层次结构（以 .java/jre 开头）相同。

例如，如果要使用 AES 256 位加密，那么需要覆盖以下 Java 策略文件：
```
    .java\jre\lib\security\US_export_policy.jar
    .java\jre\lib\security\local_policy.jar
```
{: #codeblock}

下载相应的不受限制的策略文件，并将其添加到应用程序，如下所示：
```
    resources\.java-overlay\.java\jre\lib\security\US_export_policy.jar
    resources\.java-overlay\.java\jre\lib\security\local_policy.jar
```
{: #codeblock}

推送应用程序时，这些 jar 会覆盖 Java 运行时中的缺省策略 jar。此过程会启用 AES 256 位加密。

# 相关链接
## 常规
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
