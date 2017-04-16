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

# パイプラインからのビルドとデプロイ
{: #deliverypipeline_build_deploy}
最終更新日: 2016 年 8 月 29 日
{: .last-updated}

IBM&reg; Bluemix&reg;
{{site.data.keyword.deliverypipeline}} サービスにより、反復可
能な継続的統合と継続的デリバリーのプロセスを実装することができ
ます。
{:shortdesc}

以下のタスクを実行して、パイプラインを作成および構成します。

## ステージの追加
{: #deliverypipeline_add_stage}

1. 「パイプライン: すべてのステージ」ページで、
**「ステージの追加」**をクリックします。「ステージ構成」ページが開きます。
2. ステージを構成します。
  1. **「入力」**タブで、ステージの
入力データを選択します。
  2. **「ジョブ」**タブで、少なくと
も 1 つのジョブを追加および構成します。最初のステージには、通常少なくとも 1 つのビルド
・ジョブがあります。
3. **「保存」**をクリックします。

## ジョブのステージへの追加
{: #deliverypipeline_add_job}

1. ステージで**「ステージ構成」**アイコンをクリックし、**「ステージの構成」**をクリックします。
2. **「ジョブ」**タブをクリックします。
3. **「ジョブの追加」**をクリック
します。追加するジョブのタイプを選択します。
4. ジョブを構成します。
5. **「保存」**をクリックします。

![ジョブのステージへの追加](./images/AddJob.png)

## ステージの実行
{: #deliverypipeline_run_stage}

「パイプライン: すべてのステージ」ページで、
**「ステージを実行」**アイコンをクリ
ックして、ステージを手動で実行する
ことができます。

![ステージで「ステージの実行」アイコンをクリック](./images/RunStage.png)

次の 2 つの方法のいずれかで、ビルド履歴ページからオンデマンド
でビルドとデプロイメントを依頼することもできます。

* 構成済みステージの下にあるボックスにビルドをドラッグします。
* ビルドの隣にある**「送信先」**アイコンをクリックしてから、デプロイ先となるスペース
を選択します。
![このビルド・アイコンを使用してス
テージを実行します](./images/deploy_to.png)

実行中のステージをキャンセルするには、ステージで
**「ログおよび履歴の表示」**をクリックします。ジ
ョブのリストで、実行中のジョブの番号をクリックし、次に
**「キャンセル」**をクリックします。個別にジョブを取り消す
には、そのジョブをクリックして**「キャンセル」
** をクリックするか、そのステージのジョブの隣にある**「停止」** アイコンをクリックします。


## アプリのデプロイ
{: #deliverypipeline_deploy}

適切に構成されたデプロイ・ジョブは、ジョブが実行されるたびにタ
ーゲットにアプリをデプロイします。デプロイ・ジョブを手動で実行するには、ジョブが配置さ
れているステージの **「ステージの実行」
**アイコンをクリックします。

###入力データの改訂
ステージを手動で実行する場合、または前のステージが完了したため
にステージが実行される場合、実行中のステージはその入力データの改訂を選択し
ます。通常、入力データの改訂はビルド番号です。
入力データの改訂を選択するには、ステージは次のプロセスに従います。

1. 特定の改訂が選択されている場合は、それを使用します。
2. 特定の改訂が指定されていない場合は、同じ入力データを使用す
るステージが検出されるまで、前のステージを検索します。
その入力データが最後に正常に実行された改訂を検索して使用します。

3. 特定の改訂が指定されていない場合で、指定されたソースを入力
データとして使用しているステージが他にない場合は、その入力データの最新の
改訂を使用します。

**ヒント:**以前のビルドをデプロイすることが
できます。ビルドを含むステージで、**「ログおよび履歴の表示」**をクリックします。開いたページ上で、実行
番号をクリックして展開し、ビルド・ジョブをクリックします。**「送信先」**をクリックして、ターゲットを選択します。

###アプリへのサービスの追加
サービスをアプリに追加して、そのサービスを
Bluemix ダッシュボードまたは Cloud Foundry コマンド・ライン・インタ
ーフェース (CLI) から管理することができます。DevOps サービス・パイプライン・ジョブのスク
リプトで Cloud Foundry CLI コマンドを実行することもできます。例えば、デプロイ・ジョブのス
クリプトでサービスをアプリに追加することができます。
サービスの追加について詳しくは、
[
アプリケーションへのサービスの追加](https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service)を参照してください。

## ログの表示
{: #deliverypipeline_view_logs}

ジョブのログを表示して、「ステージ履歴」ページ
で実行中のステージを表示することができます。

ジョブのログを表示するには、ジョブをクリックします。または、ステージ上で
**「ログおよび履歴の表示」**をクリックします。

デプロイされたアプリケーションのランタイム・ログを表示するには
、**「ランライム・ログの表示」**
をクリックします。

![該当ログを開く
ためにクリックできるステージ・タイトルのエリア](./images/view_logs_and_history.png)

ジョブ・ログに加え、単体テストの結果、生成される成果物、および
ビルド・ジョブのコード変更を表示することができます。

「ステージ履歴」ページからステージを実行、取り
消し、または構成することもできます。ページの上部で、**「実行」
**をクリックしてステージを実行、または**「構成」**をクリックしてステージを構成することができます。ステージを実行中
に、実行番号をクリックしてから「キャンセル」をクリックすると、ス
テージを取り消すことができます。

![「ステージ履
歴」ページでステージ実行番号をクリックして選択](./images/click_stage_run_number.png)

<!--
[1]: https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest
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
[23]: https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service
[24]: ../deploy_var
[25]: ./images/click_stage_run_number.png
[26]: ./images/diagram.jpg

-->
