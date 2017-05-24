---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Deployment Risk について

{{site.data.keyword.DRA_short}} は、デプロイメント、特にリスクについての豊富な情報を提供します。
この情報を使用し、ポリシーやゲートを利用することにより、デリバリー・パイプラインの中で品質保護を自動化することができます。
{:shortdesc}

ツールチェーンから {{site.data.keyword.DRA_short}} を開いた後、**「Deployment Risk」**をクリックします。
そこから、ステージング環境や実稼働環境でのアプリケーションの概要を得ることができ、ドリルダウンしてコード・カバレッジ、テスト・パフォーマンス、セキュリティー・レポートを確認できます。
ダッシュボードには、パイプラインの {{site.data.keyword.DRA_short}} テストからの最新情報が自動的に取り込まれます。


Deployment Risk を使用することにより、ポリシーやゲートを通じてツールチェーンの中で品質基準を適用することができます。
ポリシーは一連のルールで構成されます。ゲートはポリシーを適用するためのものです。
例えば、ビルドが単体テストやテスト・カバレッジの基準に適合することを求める「単体テストとテスト・カバレッジ」ポリシーを作成することができます。そして、そのポリシーを参照するゲートを、継続的デリバリーのプロセスに追加します。
そのポリシーを満たさないビルドは、そのゲートで制止されます。
 

## 統合情報

Deployment Risk は、{{site.data.keyword.contdelivery_full}} の一部である {{site.data.keyword.deliverypipeline}}、および Jenkins プロジェクトと統合されています。
それらの使用手順は、概略で類似しています。
  

{{site.data.keyword.deliverypipeline}} を使用している場合は、以下の手順に従います。


1. {{site.data.keyword.DRA_short}} が管理する[ポリシーとルールを作成する](risk_policies.html)。
2. {{site.data.keyword.DRA_short}} との統合のための[パイプラインのステージを準備する](risk_cd.html)。
3. パイプラインの中に、結果を {{site.data.keyword.DRA_short}} にアップロードする[テスト・ジョブを作成または編集する](risk_cd.html)。
4. それらの結果やポリシーに基づいてプロモーション決定を下す[ゲートをパイプラインに追加する](risk_cd.html)。
5. パイプラインを実行し、[結果を表示する](results.html)。

Jenkins を使用している場合、以下の手順に従います。


1. {{site.data.keyword.DRA_short}} が管理する[ポリシーとルールを作成する](risk_policies.html)。
2. [Jenkins プラグインをインストールし、構成する](risk_jenkins.html)。
3. [プラグインの指示に従ってテスト・ジョブとゲートを作成する](risk_jenkins.html)。
テスト結果が {{site.data.keyword.DRA_short}} にアップロードされて分析され、ゲートがそれらの結果を使用してプロモーション決定を下す。

4. プロジェクトを実行し、[結果を表示する](results.html)。 

コードをどんな方法でビルドしデプロイするかに関係なく、結果は同じです。
基準を満たすビルドは Deployment Risk ゲートを通過し、基準を満たさないビルドは制止されます。
 

## 前提条件
{: #prerequisites}

Deployment Risk では、[「{{site.data.keyword.DRA_short}} の概説」](/docs/services/DevOpsInsights/index.html)の説明にはない構成が必要になります。


Deployment Risk を使用するには、以下の 2 つが必要です。


* {{site.data.keyword.deliverypipeline}} または Jenkins プロジェクトのインスタンス
* プロジェクトを評価するために使用するテスト
