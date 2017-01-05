---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.DRA_short}} (試験用) の概説
{: #gettingstarted}

{{site.data.keyword.DRA_full}} は、ビルドやデプロイメントに対するリスクを識別するのに使用します。
{:shortdesc}

{{site.data.keyword.DRA_short}} は、単体テスト、機能テスト、コード・カバレッジのツールからの結果を集約して分析することによって、デプロイメント・プロセス内に指定されたゲートで、ユーザーのコードが事前定義済みのポリシーを満たしているかどうかを判別します。コードがポリシーを満たしていないか、ポリシーを超えていない場合、リスクのある変更版がリリースされないように、デプロイメントが停止されます。{{site.data.keyword.DRA_short}} は、継続的デリバリー環境のセーフティー・ネット、品質規格を実装して時間の経過とともに向上させるための方法、およびプロジェクトの正常性を把握するのに役立つデータ可視化ツールとして使用できます。

{{site.data.keyword.DRA_short}} は試験的オファリングで、開発と試験のみの目的で現状のまま提供されています。{{site.data.keyword.DRA_short}} を使用するには、{{site.data.keyword.deliverypipeline}} を使用するツールチェーンに追加します。

{: #catalog}
{{site.data.keyword.DRA_short}} の UI にアクセスするには、既存のツールチェーンから以下のステップに従ってください。

1. **「ツールの追加 (Add a Tool)」**ボタンをクリックします。

2. **「{{site.data.keyword.DRA_short}}」** をクリックします。

3. **「統合の作成 (Create Integration)」**をクリックします。

4. **{{site.data.keyword.DRA_short}}** タイルをクリックします。

5. 以下の残りのタスクを行ってセットアップを完了します。

	1. [{{site.data.keyword.deliverypipeline}} 統合を構成](./pipeline_integration.html)します。
	2. パイプラインを実行し、[{{site.data.keyword.deliverypipeline}} ダッシュボードを確認](./pipeline_decision_reports.html)します。
	3. {{site.data.keyword.DRA_short}} が管理するための[ポリシーを定義](./create_criteria.html)します。
	4. 再度パイプラインを実行して、プロジェクトがポリシーに合格するか確認します。


# 関連リンク
{: #rellinks}

## チュートリアルとサンプル
{: #samples}

* [Using analytics to advise on the likelihood of successful deployments](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){:new_window}

## 関連リンク
{: #general}

* [ツールチェーンの概要](https://new-console.ng.bluemix.net/docs/toolchains/toolchains_overview.html){:new_window}
* [Delivery Pipeline の概要](https://new-console.ng.bluemix.net/docs/services/DeliveryPipeline/index.html){:new_window}
* [IBM Bluemix 料金シート](https://new-console.ng.bluemix.net/pricing/){:new_window}
* [IBM Bluemix prerequisites](https://developer.ibm.com/bluemix/support/?cm_mc_uid=96503159749414585876298&cm_mc_sid_50200000=1462802909#prereqs){:new_window}
