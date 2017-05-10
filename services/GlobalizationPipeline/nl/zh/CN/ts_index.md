---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.GlobalizationPipeline_short}} 故障诊断
{: #globalizationpipelinets}


以下是有关使用 {{site.data.keyword.GlobalizationPipeline_short}} 常见问题的一些解答。
{:shortdesc}


## 应用程序的名称未正确地翻译
{: #problem1}

所生成的特定字符串的翻译不符合预期。
{:shortdesc}

翻译资源文件时，包含产品名称或其他专有名词的字符串可能未正确翻译。
{: tsSymptoms}

通常，产品名称或专有名称不会正确地翻译为其他语言，尤其是名称包含实际单词时更是如此。当翻译这些类型的单词或短语时，因这些单词在特定语言中的意思，翻译后的文本可能与英文名称具有不同的意思。
{: tsCauses}

在使用产品名称之前，请先测试产品名称的翻译，如果发现问题，请相应地修改文本或翻译。有关使用机器翻译时书写样式的提示，请参阅[机器翻译提示](./tips.html#globalizationpipeline_tips)。
{: tsResolve}



## 无法上传资源文件
{: #problem2}

我尝试上传的资源文件不被接受。
{:shortdesc}

当向新翻译束中添加资源文件或更新要翻译的现有资源文件时，接收到错误。
{: tsSymptoms}

{{site.data.keyword.GlobalizationPipeline_short}} 仅接受以下类型的资源文件：Java™ .properties、JSON 和 AMD I18N。
{: tsCauses}

请确保要上传的资源文件是以下其中一种类型。
{: tsResolve}
* Java .properties
* JSON
* AMD I18N



## 因为资源文件太大而无法上传
{: #problem3}

我尝试上传的资源文件不被接受。
{:shortdesc}

当向翻译项目添加或更新资源文件时，由于文件的一部分太大而发生错误。
{: tsSymptoms}

{{site.data.keyword.GlobalizationPipeline_short}} 仅接受满足特定大小需求的资源文件。
{: tsCauses}

请确保资源文件符合以下准则：
{: tsResolve}
* 每个键最多可为 256 个字符。
* 每个值最多可为 2048 个字符。
* 每个翻译项目最多可包含 500 个键值对。
* 资源文件不能超过 2 MB。




## 字符串中包含的变量周围的留空不一致
{: #problem5}

翻译后变量周围所使用的留空不总是相同的。
{:shortdesc}

翻译后，字符串中所含变量周围所使用的留空从一个语言到另一个语言不总是相同的。
{: tsSymptoms}

机器翻译引擎设计用来使用自然语言，可能无法始终识别或了解如何处理编程语言所使用的特定语法。因此，处理与纯文本混合在一起的语法可能会有所不同。
{: tsCauses}

{{site.data.keyword.GlobalizationPipeline_short}} 目前识别常用于代表变量的“{}”模式，将会保留其中所包含的原始内容格式。
{: tsResolve}
