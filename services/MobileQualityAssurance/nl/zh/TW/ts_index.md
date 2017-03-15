---

copyright:
  years: 2012, 2017
  
lastupdated: "2017-01-25"  

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# 对 {{site.data.keyword.mqa}} 进行故障诊断 
{: #tsmqa}
下面是使用 {{site.data.keyword.mqa}} 时遇到的几个常见问题的解决方法。
{:shortdesc}

## JavaScript 混合构建失败
{: #ts_js_build_fail}

即使用于 IBM MobileFirst Platform Foundation 的 JavaScript&tm; 混合 SDK 组件在应用程序中且已添加所需代码，JavaScript 混合 {{site.data.keyword.mqa}} 应用程序构建还是失败。


当您尝试运行 {{site.data.keyword.mqa}} 应用程序构建时，构建会失败。
{: tsSymptoms notoc} 


1. Android 和 iOS 平台特定的混合 SDK 组件未在项目中安装。
2. 安装的 Android 和 iOS 平台特定的混合 SDK 组件与安装的 JavaScript SDK 组件不兼容。
3. 已安装本机 Android SDK 和/或本机 iOS SDK，但未安装 Android 和 iOS 平台特定的混合 SDK 组件。
{: tsCauses notoc} 
 

解决此问题的一些建议包括以下步骤：
{: tsResolve notoc}
  1.  确保已安装全部所需的 Android 和 iOS 平台特定的混合 SDK 组件，以及用于应用程序所支持平台的每个所需的本机 Android SDK 或本机 iOS SDK。 
  2. 确保 Android 和 iOS 平台特定的混合 SDK 组件的主版本号与 JavaScript 组件的相同或比它更高，但应低于下一个主版本号。下表包含示例：
  
| JavaScript 组件版本 | 平台特定的组件版本 | 是否兼容？ |
|---------: |------------: |------------: |
| 1.2.3 | 1.2.3 | 是 |
| 1.2.3 | 1.2.1 | 否 |
| 1.2.3 | 1.3.2 | 是 |
| 1.2.3 | 2.0.0 | 否 |

  3. 确保已安装 Android 和 iOS 平台特定的混合 SDK 组件。如果应用程序在那些平台上运行，就需要本机 Android SDK 和本机 iOS SDK，而且混合应用程序还必须为每个平台安装 Android 和 iOS 平台特定的混合 SDK 组件。

  
## 无法打开观点分析或分发测试应用程序
{: #ts_sent_fail}

无法打开观点分析或分发测试应用程序。

无法打开观点分析或分发测试应用程序，因为浏览器阻止了弹出窗口。
{: tsSymptoms notoc} 

Mobile Quality Assurance 使用弹出窗口和 cookie 与 Mobile Quality Assurance 服务器进行通信。
{: tsCauses notoc}


要在 Mobile Quality Assurance 与 Mobile Quality Assurance 服务器之间建立通信，可能需要配置浏览器设置，以允许弹出窗口和 cookie。例如，当您单击用户界面上的某个选项（例如“观点分数”）时，系统可能会阻止 Mobile Quality Assurance 与服务器进行通信。如果阻止了弹出窗口和 cookie，那么无法显示观点分析。有关如何配置浏览器设置的更多信息，请参阅具体浏览器的文档。
{: tsResolve notoc}


## 无法运行到期的应用程序
{: #ts_app_expired}

无法运行 Mobile Quality Assurance 应用程序。

当您尝试运行 Mobile Quality Assurance 应用程序时，看到以下消息：您的应用程序已到期，目前无法运行。
{: tsSymptoms notoc} 

您的应用程序在 Mobile Quality Assurance“构建”页面中标记为已禁用。
{: tsCauses notoc}


检查 Mobile Quality Assurance“构建”页面，以确保没有应用程序标记为已禁用。通常，应用程序标记为已禁用是告知测试人员（通过应用程序自身）不要使用特定版本的构建。有关 Mobile Quality Assurance“构建”页面中的设置的更多信息，请参阅 IBM Knowledge Center 中的“管理构建”。
{: tsResolve notoc}

