---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} 功能概述
{: #feature_overview}

上次更新时间：2016 年 6 月 29 日
{: .last-updated}

{{site.data.keyword.iot_full}} 基于以下关键方面进行构建：

  1. Connect - 连接设备并开发应用程序。
  2. 信息管理 - 存储和查看设备数据，并将 {{site.data.keyword.iot_short_notm}} 与其他服务集成。
  3. 分析 - 通过使用 {{site.data.keyword.iot_short_notm}} 仪表板可视化实时设备数据。
  4. 风险管理 - 通过对用户和应用程序的访问控制来配置安全的连接和体系结构。

## Connect
{: #connect}

{{site.data.keyword.iot_short_notm}} Connect 是任何 {{site.data.keyword.iot_short_notm}} 服务的起始点。连接设备、创建应用程序、控制设备以及与第三方服务交互全部通过 {{site.data.keyword.iot_short_notm}} Connect 实现。

### 网关设备

通过使用网关，可将设备连接到 {{site.data.keyword.iot_short_notm}}，在不使用网关的情况下，设备无法连接到因特网。网关设备集成了设备功能和应用程序功能。网关可像设备一样接收命令和发送设备数据，但也可像应用程序一样将命令发送到所连接的其他设备。

可以将无法直接连接到因特网的设备连接到网关设备，这样其设备数据可发送到网关设备，接着网关设备可将这些数据发送到 {{site.data.keyword.iot_short_notm}} 服务。

### 设备管理

通过组合设备管理 API 以及设备上安装的设备管理代理程序，提供了设备管理功能。受管设备可执行设备管理操作，这些操作可通过主 {{site.data.keyword.iot_short_notm}} 仪表板触发。

通过设备管理，可重新引导、下载和安装固件更新，还可远程将设备重置为出厂设置，所有这些操作都从 {{site.data.keyword.iot_short_notm}} 用户界面执行。

### 第三方服务集成

在 {{site.data.keyword.iot_short_notm}} 中构建了第三方服务集成，包括对 The Weather Company 天气位置服务（可用于查找设备所在位置的当前天气）的支持。

---

## 信息管理
{: #information_management}

{{site.data.keyword.iot_short_notm}} 信息管理在设备所发送的数据到达 {{site.data.keyword.iot_short_notm}} 服务后对其进行控制。信息管理包括数据存储和转换。

### 设备上次事件高速缓存

通过使用 {{site.data.keyword.iot_short_notm}} 上次事件高速缓存 API，可检索设备上次所发送的事件。这在设备联机或脱机的情况下都适用，这样不管设备的物理位置或使用状态如何，您都可检索设备状态。对于最多 365 天之前发生的任何特定事件，可检索设备的上次事件数据。

### 设备事件数据存储

可以存储 {{site.data.keyword.iot_short_notm}} 服务中的设备事件数据以供将来使用。要执行深度分析以获取对该数据的洞察，数据存储是非常关键的第一步。例如，您可跟踪较长时间段内的更改，存储数据集，以用于功能强大的分析工具（包括用于 Watson API 和认知计算）。

---

## 分析
{: #analytics}

### 可视化实时设备数据

您可以通过使用仪表板卡，可视化和显示实时设备数据。仪表板卡实时监视和显示设备数据，这样您可以跟踪关键设备或设备数据。这些可视化内容显示在主 {{site.data.keyword.iot_short_notm}} 仪表板上，便于您快速访问实时设备数据的上下文和状态。

---

## 风险管理
{: #risk_management}

### 安全的连接和体系结构

{{site.data.keyword.iot_short_notm}} 的体系结构旨在防止设备冒充其他设备，以维护设备数据的完整性。设备通过使用只有您自己知道的客户机标识和认证令牌组合来连接到 {{site.data.keyword.iot_short_notm}}。注册设备或生成 API 密钥后，认证令牌将使用加密盐 (Salt) 进行加密并散列化以维护凭证的安全性。完全支持通过 TLS V1.2 进行连接。

---
