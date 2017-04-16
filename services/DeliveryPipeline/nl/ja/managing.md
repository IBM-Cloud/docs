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
最終更新日: 2016 年 8 月 30 日
{: .last-updated}

IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} 統合を管理、構
成、および拡張できます。
{:shortdesc}

以下のタスクを完了して、パイプラインを管理、構成、および拡張します。

## アクセスの制御
{: #deliverypipeline_access}

ステージの実行またはパイプラインの変更が可能な作業者
を制限することができます。そのためには、「パイプライン設定」ページに移動します。「パイプライン: すべてのステージ」ページで**「ステージ
構成」**アイコンをクリックして移動
します。

![「パイプライン設定
ギア」アイコン](./images/pipeline_settings.png)

## 環境プロパティーおよびリソース
{: #deliverypipeline_envprop}

{{site.data.keyword.deliverypipeline}}
サービスと相互作用するには、環境プロパティーと事前にインストールされた
リソースを使用することができます。例えば、環境プロパティーと事前インストールされたリソー
スをジョブ・スクリプトまたはテスト・コマンドに取り込むことができます。詳しくは、
[{{site.data.keyword.deliverypipeline}} サービスの
環境プロパティーとリソース (Environment properties and resources for
the {{site.data.keyword.deliverypipeline}} service)](./deploy_var.html) を参照してください。

固有の環境プロパティーを**「環境プロパティー」** タブからステージへ追加することができます。
環境プロパティーはステージの各ジョブで使用可能です。

「環境プロパティー」タブから次の 4 つのタイプのプロパテ
ィーを追加することができます。
* **文字**: 単一行の値を持つプロパティー・キー 。
* **テキスト・エリア**: 複数行の値を持つプロパティー・キー。
* **セキュア (Secure)**: 単一行の値を持つプロパティー・キー。値はアスタリスクで表示されます。
* **プロパティー**: プロジェクトのリポジトリーにあるファイル。
このファイルには、複数のプロパティーを含めることができます。各プロパティーは固有の行になければなり
ません。キーと値のペアを分離するには、等号 (=) を使用します。

## パイプラインの機能の拡張
{: #deliverypipeline_extend}

サポートされるサービスを使用するようにジョブを構成することで、
Build & Deploy パイプラインの機能を拡張することができます。
例えば、テスト・ジョブは静的コード・スキャンを実行することができ、ビ
ルド・ジョブはストリングをグローバル化することができます。

パイプラインの機能の拡張について詳しくは、
[{{site.data.keyword.deliverypipeline}}
サービスの拡張](./deliverypipeline_extension.html)を参照してください。

<!-- [1]: https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest
[2]: https://www.ng.bluemix.net/docs/#services/DeliveryPipeline/index.html#getstartwithCD
[3]: http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push
[4]: https://console.ng.bluemix.net/?ace_base=true/#/pricing/cloudOEPaneId=pricing
[5]: ./images/open_logs.png
[6]: #manifests
[7]: ./images/runbar-annotated-dark.png
[8]: ./images/input_tab_only_execute.png
[9]: ./images/deploy_to.png
[10]: ./images/view_logs_and_history.png
[11]: ./images/play_button.png
[12]: ./images/basicAnimate.gif
[13]: ./images/AddStage.png
[14]: ./images/AddJob.png
[15]: ./images/jobs.png
[16]: ./images/RunStage.png
[17]: https://www.ng.bluemix.net/docs/starters/container_pipeline.html#container_pipeline
[18]: ../../../tutorials/basicbuild
[19]: #add_stage
[20]: #add_job
[21]: ../deploy_ext
[22]: ./images/pipeline_settings_icon.png
[23]: ./images/pipeline_settings.png
[24]: https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service
[25]: ../deploy_var
[26]: ./images/click_stage_run_number.png
[27]: ./images/diagram.jpg -->
