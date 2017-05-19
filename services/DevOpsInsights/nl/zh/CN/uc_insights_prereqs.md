---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Delivery Insights 的先决条件
{: #prereqs}

要在 {{site.data.keyword.DRA_short}} 中查看 IBM UrbanCode Deploy 服务器中的信息，必须在可以连接到 IBM UrbanCode Deploy 服务器的系统上托管 DevOps Connect 实例。此系统可以是物理计算机，也可以是虚拟机。
{:shortdesc}

托管 DevOps Connect 的系统必须满足以下先决条件：
- 系统必须具有 Java 运行时环境 (JRE) V8 或更高版本。
- 系统 `PATH` 变量必须包含 JRE 的位置。
- 系统必须允许 DevOps Connect 创建与 IBM Bluemix 的出局连接。

要安装 DevOps Connect 以用于 Delivery Insights，请打开 DevOps Insights 服务，然后单击**设置 > Delivery Insights 设置**。
