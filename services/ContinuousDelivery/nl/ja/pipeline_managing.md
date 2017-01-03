---

copyright:
  years: 2016

---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# パイプラインの管理
{: #deliverypipeline_managing}
最終更新日: 2016 年 11 月 17 日
{: .last-updated}

IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} の統合を管理、構成、および拡張できます。
{:shortdesc}

次のタスクを実行して、パイプラインを管理、構成、および拡張します。

## 環境プロパティーとリソース
{: #deliverypipeline_envprop}

環境プロパティーとあらかじめインストールされたリソースを使用して、{{site.data.keyword.deliverypipeline}} サービスと対話できます。たとえば、ジョブ・スクリプトやテスト・コマンドを取り込むことができます。 [{{site.data.keyword.deliverypipeline}} サービスの環境プロパティーとリソース](./deploy_var.html)を参照してください。

独自の環境プロパティーを、ステージの**「環境プロパティー (ENVIRONMENT PROPERTIES)」**タブからステージに追加します。環境プロパティーは、ステージのすべてのジョブに使用可能です。

「環境プロパティー (Environment Properties)」タブから、次の 4 つのタイプのプロパティーを追加できます。
* **「テキスト」**: 単一行の値を持つプロパティー・キー。
* **「テキスト域 (Text Area)」**: 複数行の値を持つプロパティー・キー。
* **「セキュア (Secure)」**: 単一行の値を持つプロパティー・キー。値はアスタリスクとして表示されます。
* **「プロパティー (Properties)」**: プロジェクトのリポジトリーにあるファイル。このファイルには、複数のプロパティーを含めることができます。プロパティーはそれぞれ独自の行で指定されている必要があります。キー値のペアを区切るには、等号 (=) を使用します。

## パイプラインの機能を拡張する
{: #deliverypipeline_extend}

サポートされるサービスを使用するようにジョブを構成することで、パイプラインの機能を拡張できます。例えば、テスト・ジョブで静的コード・スキャンを実行し、ビルド・ジョブで文字列をグローバル化できます。

パイプライン機能の拡張の詳細については、[{{site.data.keyword.deliverypipeline}} サービスの機能の拡張](./deliverypipeline_extension.html)を参照してください。

