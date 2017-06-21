---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.streaminganalyticsshort}} 疑難排解
{: #ts_StreamingAnalytics}

您可以找到如何在 {{site.data.keyword.Bluemix_short}} 上使用 {{site.data.keyword.streaminganalyticsshort}} 之常見問題的答案。
{:shortdesc}

##啟動這項服務時，系統提示我輸入認證以登入主控台
{: #log_in_console}

啟動 {{site.data.keyword.streaminganalyticsshort}} 時，系統會提示您輸入認證以登入服務主控台。
{:shortdesc}

您可以啟動先前建立的 {{site.data.keyword.streaminganalyticsshort}} 服務，而且會看到提示您輸入認證的登入頁面，而不是直接存取服務主控台。
{: tsSymptoms}

已更新服務基礎架構，而且瀏覽器快取會讓服務無法取得更新。
{: tsCauses}

請清除瀏覽器快取，以確保取得服務主控台的最新版本。
{: tsResolve}

##我的應用程式不健全
{: #app_unhealthy}

您無法正確地執行應用程式，且性能狀態為 `unhealthy`。
{:shortdesc}

您將應用程式提交至服務實例，應用程式啟動但立即失敗了，性能狀態為 `unhealthy`。下列錯誤出現在日誌檔中：`/lib64/libc.so.6: version GLIBC_2.14 not found`。
{: tsSymptoms}

您未使用 RHEL 6.5 作業系統或相等的 CentOS 版本編譯應用程式。
{: tsCauses}

您必須在 Red Hat Enterprise Linux (RHEL) 6.5 作業系統或相等的 CentOS 版本中，重新編譯應用程式，並且使用 Intel 處理器。將應用程式重新提交至服務實例。
{: tsResolve}
