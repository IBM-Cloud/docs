---

copyright:
  years: 2015, 2016
lastupdated: "2016-12-21"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#{{site.data.keyword.jazzhub_short}} サンプル・プロジェクトにおけるテキスト・ベースのパイプラインの共有 {: #share-pipeline}

「{{site.data.keyword.Bluemix_notm}} にデプロイ」ボタンで {{site.data.keyword.Bluemix_notm}} にデプロイされたサンプル・プロジェクトに対して、{{site.data.keyword.jazzhub_short}} パイプライン構成を YAML ファイルとして定義できます。テキストとして定義されたパイプラインは共有することができ、それによりプロジェクトをフォークする人は独自のパイプラインを構成する必要がなくなります。この機能は現在開発中で、YAML フォーマットと実装は随時変更される可能性があります。現在この機能は、{{site.data.keyword.Bluemix_notm}} をターゲットとする Git リポジトリーおよび GitHub リポジトリーを持つプロジェクトでのみ使用可能です。
{: shortdesc} 

サンプル・プロジェクトのルート・ディレクトリー内に、`pipeline.yml` ファイルを含む `.bluemix` という名前のフォルダーが存在する必要があります。

「{{site.data.keyword.Bluemix_notm}} にデプロイ」ボタンを使用してプロジェクトが複製されると、{{site.data.keyword.jazzhub_short}} は `pipeline.yml` ファイルに基づいたパイプラインを作成します。 

例: 
``` 
<sample root>
	.bluemix
		pipeline.yml
	<other sample content>
```
{: codeblock} 

YAML ファイル・フォーマットはパイプラインの仕様を含む単一の YAML 文書です。以下のサンプル {{site.data.keyword.jazzhub_short}} パイプラインは、Ant を使用して Java アプリを 1 つのステージでビルドします。その後、別のステージで、パイプラインがそのアプリを {{site.data.keyword.Bluemix_notm}} にデプロイします。 

``` 
---
stages:
- name: Build Stage
  inputs:
  - type: git
    branch: master
  triggers:
  - type: commit
  properties:
  - name: APP_VERSION
    value: '1.0'
    type: text
  jobs:
  - name: Build
    type: builder
    artifact_dir: output
    build_type: ant
    script: |-
      #!/bin/bash
      ant
    enable_tests: true
    test_file_pattern: tests/TEST-*.xml
- name: Deploy Stage
  inputs:
  - type: job
    stage: Build Stage
    job: Build
  triggers:
  - type: stage
  jobs:
  - name: Deploy to dev
    type: deployer
    target:
      url: https://api.ng.bluemix.net
      organization: uateam@ca.ibm.com
      space: dev
      application: JavaSampleUnitTest
    script: |
      cf push "${CF_APP}"
      # View logs
      #cf logs "${CF_APP}" --recent
```
{: codeblock} 

##YAML ファイルの構文 {: #yaml-syntax}

どのようなパイプラインも、以下の構文を使用してテキストで表現することができます。

パイプライン:

```
---
stages:
<sequence of stages>
```
{: codeblock} 

ステージ: 
```
---
name: <name>
[inputs: 
	<sequence of inputs>] 
[triggers:   
	<sequence of triggers>] 
[properties:   
	<sequence of properties>] 
[jobs:   
	<sequence of jobs>]
```
{: codeblock} 

入力:
```
type: 'git' | 'job'
[branch: <branch name>] ;only for Git inputs
stage: <stage name>		  ;only for job inputs
job: <job name>			   	;only for job inputs
```
{: codeblock} 

トリガー:
```
type: 'commit' | 'stage'
[enabled: 'true | 'false'] ;true is assumed if not specified
```
{: codeblock} 	
	
プロパティー:
```
name: <property name>
value: <property value>
[type: 'text' | 'secure' | 'text_area' | 'file'] ;text is assumed if not specified
```
{: codeblock} 

ジョブ:
```
[name: <job name>]
type: 'builder' | 'deployer' | 'tester'
fail_stage: 'true' | 'false'
[extension_id: <extension id>] ;extension jobs only
[working_dir: <working dir path>] ;builder and tester only
[artifact_dir: artifact path>] ;builder only
[build_type: <build type>] ;builder only
[script: <script>] ;not for extension jobs
[enable_tests: 'true' | 'false'] ;builder and tester only
[test_file_pattern: <pattern>] ;builder and tester only
[target: <target>] ;deployer and extension jobs only
*[<extension property name>: <value>] ;extension jobs only
```
{: codeblock} 

ターゲット:
```
url: <target url>
organization: <org name>
space: <space name>
[application: <application name>]
```
{: codeblock} 

##拡張ジョブおよび拡張定義 {: #extension-jobs} 

拡張定義は拡張ジョブで使用可能な一連のプロパティーを定義します。`extension_id ` プロパティーが指定されると、ジョブは拡張ジョブとして扱われます。拡張に使用可能なプロパティーを把握するには、その資料を参照してください。 

##YAML ファイルを使用したパイプラインとの対話 {: #pipeline-yaml} 

**環境変数および解決** 
<!-- Formating for this? -->

パイプラインが `pipeline.yml` ファイルから作成される前に、「{{site.data.keyword.Bluemix_notm}} にデプロイ」機能は、ファイル内のすべての環境変数を {{site.data.keyword.Bluemix_notm}} インターフェースで指定した情報 (例えば、組織) に置き換えます。YAML 値が置換されるのは、その値が 1 つの環境変数のみで構成される場合のみです。 

```
{
  "project_id": "_ljkahfliasdlk",
  "env": {
     "CF_ORGANIZATION" : "user@se.ibm.com"
  },
  "config": {
    "format" : "yaml",
    "content" : "
      ...
        target:
          url: http://api.ng.bluemix.net
          organization: ${CF_ORGANIZATION}
        script: \"echo ${CF_ORGANIZATION}\"
      ...
    "
  }
}
```
{: codeblock} 

このサンプル内で、ターゲット組織はターゲット URL に対して解決され、パイプライン構成内に残る値は組織 GUID です。デプロイメント・スクリプト内のオカレンスは置換されません。

ターゲット URL は環境変数または実際の値として指定する必要があり、組織とスペースの GUID または名前を指定する必要があります。1 つの値を指定するともう 1 つの値も置換されます。

変数 | 説明
---------------- | ---------------- 
CF_TARGET_URL |	Bluemix ターゲット URL
CF_ORGANIZATION	| 組織名
CF_ORGANIZATION_ID	| 組織 GUID
CF_SPACE |	スペース名
CF_SPACE_ID |	スペース GUID
CF_APP	| アプリ名

{: caption="Table 1. Environment variables" caption-side="top"}

**パイプラインからの YAML ファイルの生成** 

パイプラインから YAML ファイルを生成することができます。 

以下の形式の URL を使用して、既存のパイプラインからファイルを生成します。

```
<DevOps Services domain>/pipeline/user/project/yaml
```
{: codeblock} 

accept ヘッダーはこの呼び出しでは必要ありません。この呼び出しはブラウザーから使用できます。 

**注:** 安全上の理由により、secure-stage 環境プロパティー値は生成されたパイプライン YAML ファイルから省略されます。 
