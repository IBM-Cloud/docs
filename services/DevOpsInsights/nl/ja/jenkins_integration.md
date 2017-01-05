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

# {{site.data.keyword.DRA_short}} と Jenkins との統合
{: #toolchain_configure_jenkins}

{{site.data.keyword.DRA_full}} がモニターするためのポリシーを定義し終えたら、次のステップとして、{{site.data.keyword.DRA_short}} をツールチェーンに追加してから、継続的デリバリーのパイプラインを構成します。
{:shortdesc}

<!--##Configuring a Jenkins project-->

{{site.data.keyword.DRA_short}} を 1 つの Jenkins プロジェクトに統合するか、複数の関連した Jenkins プロジェクトにまたがって統合することができます。この統合により、品質ゲートを設定したり、{{site.data.keyword.DRA_short}} ダッシュボード上でビルド品質データを受け取ったりできるようになります。

##前提条件    
{: #DI_jenkins_prereqs}

* ローカルの Jenkins プロジェクトか、Jenkins プロジェクトを実行しているサーバーに対するアクセス権がなければなりません。

##{{site.data.keyword.DRA_short}} プラグインのインストール
{: #DI_jenkins_install}

{{site.data.keyword.DRA_short}} プラグインを Jenkins プロジェクト内にインストールするには、以下のステップに従ってください。

  1. プラグインの GitHub リポジトリーから [IBM DevOps Insight プラグインのインストール・ファイル (.hpi) をダウンロード](https://github.ibm.com/oneibmcloud/DRA-Jenkins/blob/hpi-release/target/dra.hpi)します。
  2. Jenkins のインストール済み環境で、**「Jenkins の管理 (Manage Jenkins)」**をクリックし、**「プラグインの管理 (Manage Plugins)」**を選択して、**「詳細」**タブをクリックします。
  3. **「ファイルの選択」**をクリックし、DevOps Insight プラグインのインストール・ファイルを選択します。
  4. **「アップロード」**をクリックします。
  5. Jenkins を再始動して、プラグインがインストールされたことを確認します。

##{{site.data.keyword.DRA_short}} と Jenkins との統合    
{: #DI_jenkins_integrate}

プラグインをインストールし終えたら、{{site.data.keyword.DRA_short}} を Jenkins インストール済み環境に統合する前に、[コントロール・センター](https://control-center.stage1.ng.bluemix.net/)に進んで 1 つ以上のポリシーを作成してください。

既存のジョブ内で {{site.data.keyword.DRA_short}} を使用する場合は、そのジョブごとに以下のようにします。

1. **「ビルド情報を {{site.data.keyword.DRA_short}} に公開」**、**「デプロイメント情報を {{site.data.keyword.DRA_short}} に公開」**、または**「テスト結果を {{site.data.keyword.DRA_short}} に公開」**をタイプとして指定して、ビルド後アクションを追加します。この特定のタイプは、ジョブのタイプ (ビルド、デプロイ、またはテスト) と一致している必要があります。必須フィールドに入力します。
  * 「資格情報」フィールドで、ご使用の Bluemix の ID とパスワードを選択します。Jenkins で保存されていない場合は、**「追加」**ボタンをクリックして追加し、保存します。
  * 「ビルド・ジョブ名 (Build Job Name)」フィールドで、ビルド・ジョブの名前を Jenkins での名前と正確に一致するように指定します。ビルドをテスト・ジョブと共に行う場合は、このフィールドは空のままにします。ビルド・ジョブを Jenkins 以外で行う場合は、**「Jenkins 以外でビルドを実行する (Builds are being done outside of Jenkins)」**にチェック・マークを付け、ビルド番号とビルド URL を指定します。
  * 「結果ファイルの場所 (Result File Location)」フィールドの場合、結果ファイルの場所を指定します。テストで結果ファイルを生成しない場合は、このフィールドを空のままにします。プラグインは、現在のテスト・ジョブの状況に基づいてデフォルトの結果ファイルをアップロードします。
3. *オプション*: テスト・ジョブ内の DRA ポリシー・ゲートでダウンストリームのデプロイ・ジョブを制御する場合は、タイプとして**「DevOps リスク分析ゲート」**を指定して別のビルド後アクションを追加し、必須フィールドに入力します。テスト・ジョブが関連付けられているポリシーに準拠しない場合、このゲートによりダウンストリームのジョブの実行が阻止されます。
4. **「適用」**をクリックしてから、**「保存」**をクリックします。

プロジェクト・ページから**「今すぐビルド (Build Now)」**をクリックして、プロジェクトを実行できます。

ビルドの実行後に、[コントロール・センター](https://control-center.stage1.ng.bluemix.net/)に進んで、ダッシュボードでビルドの状況を確認します。ポリシー・ゲートを構成した場合は、現在のビルドの「状況」ページに {{site.data.keyword.DRA_short}} の結果も表示されます。
