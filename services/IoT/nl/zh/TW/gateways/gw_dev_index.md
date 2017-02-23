---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 在 {{site.data.keyword.iot_short_notm}} 上開發閘道
{: #gw_dev_index}

如果您的裝置無法直接連接至網際網路，您可以建置閘道裝置來擷取資料，並將資料傳送至 {{site.data.keyword.iot_full}} 組織中的應用程式。
我們有提供用戶端程式庫、範例及資訊，可協助您將裝置閘道連接至您的 {{site.data.keyword.iot_short_notm}} 組織及應用程式。
{:shortdesc}

## 連線通訊協定
閘道是使用 MQTT 傳訊通訊協定來連接至 {{site.data.keyword.iot_short_notm}}。不支援使用 HTTP 傳訊將閘道連接至 {{site.data.keyword.iot_short_notm}}。只有裝置可以使用 HTTP 傳訊來連接。

## 用戶端檔案庫
用來開發可連接至 {{site.data.keyword.iot_short_notm}} 之閘道的用戶端程式庫提供下列語言：

|用戶端程式庫 |程式庫和進一步說明文件的鏈結
|:---|:---
|C++| https://github.com/ibm-watson-iot/iot-cpp
|C#| https://github.com/ibm-watson-iot/iot-csharp
|嵌入式 C| https://github.com/ibm-watson-iot/iot-embeddedc
|Java™|https://github.com/ibm-watson-iot/iot-java
|mBed C++|https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/
|Node.js|https://github.com/ibm-watson-iot/iot-nodejs
|Node-RED|https://github.com/ibm-watson-iot/iot-nodered
|Python|https://github.com/ibm-watson-iot/iot-python

如需可用之用戶端程式庫的相關資訊和鏈結，另請參閱[適用於 {{site.data.keyword.iot_short_notm}} 開發的用戶端程式庫](../iot_platform_client_lib.html)。
