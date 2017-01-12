---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Eclipse Orion {{site.data.keyword.webide}} を使用したコードの編集
{: #web_ide}

最終更新日: 2016 年 10 月 26 日
{: .last-updated}

Eclipse Orion {{site.data.keyword.webide}} は、Web 開発を行うことのできるブラウザー・ベースの開発環境です。コンテンツ・アシスト、コード補完、エラー・チェックによる支援を利用して JavaScript、HTML、CSS での開発を行うことができます。{{site.data.keyword.webide}} は、ほとんどすべての言語に対応しており、大部分の[ファイル・タイプ (新しいウィンドウでリンクが開きます)](https://hub.jazz.net/docs/overview/#dev_support){: new_window} に対して構文の強調表示を提供します。ソース管理は Git または Jazz SCM を通して組み込まれ、アプリのテストとデバッグを行うためにコードをローカルにデプロイすることができます。
{:shortdesc}

何よりも良い点は、{{site.data.keyword.webide}} が Web ベースであるという点です。インストールが必要なものは何もなく、保守や拡大縮小が必要なものも何もありません。インターネット接続さえあれば、どこでも開発を行うことができます。

## エディターのセットアップ
{: #editorsetup}

{{site.data.keyword.webide}} はカスタマイズ可能であり、開発ニーズに合わせて、カラー・スキーム、テクニカル・ツール、および設定を選択することができます。これらの設定を表示したり変更したりするには、左側のメニューから**「設定」**アイコン<img class="inline" src="./images/webide_settings_icon_light.png"  alt="設定アイコン">をクリックします。


編集中に特定の設定を頻繁に変更する必要がある場合、エディターの右上隅の**「ローカル・エディター設定」**アイコン<img class="inline" src="./images/webide_local_settings_icon_light.png"  alt="「ローカル・エディター設定」アイコン">からそれらの設定に素早くアクセスできます。


![ローカル・エディター設定](images/webide_local_editor_settings_light.png)

デフォルトでは、エディター・スタイルとフォント・サイズの設定が常に表示されます。他のエディター設定をメニューに含めるには、以下の手順を実行します。

1. **「ローカル・エディター設定」**アイコン<img class="inline" src="./images/webide_local_settings_icon_light.png"  alt="「ローカル・エディター設定」アイコン">をクリックします。

2. **「エディター設定」**をクリックします。

3. **「ローカル・エディター設定」**メニューへの設定の組み込みまたはメニューからの設定の除外を行うには、設定の横にある丸印をクリックします。

![「エディター設定」トグル](images/webide_editor_settings_toggle_light.png)


## コードの編集
{: #editcode}

{{site.data.keyword.webide}} には、2 つの主要セクションがあります。1 つ目のセクションは左側にあるファイル・ナビゲーターであり、プロジェクト・ファイルがツリー構造で表示されます。ファイル・ナビゲーターから、ファイルとフォルダーの作成、名前変更、削除、管理を行うことができます。

**ヒント:** ファイルをファイル・ナビゲーターにアップロードするには、対象のファイルをコンピューターからファイル・ナビゲーターにドラッグします。

2 つ目のセクションは右側にあるエディター・ペインです。このエディターは、コンテンツ・アシストや構文検査など、いくつかのコーディング機能を備えています。

![Web IDE](images/webide_light.png)

### 複数のファイルの処理
1. 同時に 2 つのファイルに対する作業を行うには、エディターの上部にある**「分割エディター・モードの変更」**アイコン<img class="inline" src="./images/webide_split_editor_icon_light.png"  alt="「分割エディター」アイコン">をクリックします。
2. 開いたメニューから、1 つのビューを選択します。

 ビューを選択した後、既にエディターで開かれていたファイルがある場合、そのファイルは両方のエディター・ビューに表示されます。

 一方のエディター・ビューに表示されているファイルをオープンまたは変更するには、次のようにします。
 1. 変更するエディター・ビューにカーソルを移動します。
 2. ファイル・ナビゲーターで、いずれかのファイルをクリックします。

### キーボード・ショートカット
{{site.data.keyword.webide}} の大部分のコマンドは、キーボード・ショートカットでのみアクセス可能です。

エディターのキーボード・ショートカットのリストを表示するには、Alt+Shift+? を押します。Mac OS を使用している場合は、Ctrl+Shift+? を押します。

## ソース・コードの管理
{: #sourcecontrol}

{{site.data.keyword.webide}} は、ソース・コード管理ツールと統合されています。Git リポジトリーに関する作業を行うには、**「Git リポジトリー」**アイコン<img class="inline" src="./images/webide_git_icon_light.png"  alt="「Git リポジトリー」アイコン">をクリックします。詳しくは、[Git を使用したソース管理 (新しいウィンドウでリンクが開きます)](https://hub.jazz.net/docs/git/){: new_window} を参照してください。


## ワークスペースからのアプリのデプロイ
{: #deploy}

1. アプリをデプロイするには、実行バーから、起動構成を選択または[作成 (新しいウィンドウでリンクが開きます)](https://hub.jazz.net/tutorials/livesync/#launch_configuration){: new_window} します。
1. 「デプロイ」アイコン<img class="inline" src="./images/webide_deploy_button_light.png"  alt="「デプロイ」アイコン">をクリックします。ワークスペースの現在の内容と、起動構成に定義された環境を使用して、アプリのインスタンスがデプロイされます。 
2. アプリがデプロイされた後、実行バーを使用して、アプリの停止、再始動、デバッグ、ログの表示などを行うことができます。![実行バー](images/webide_runbar_light.png)

 ## {{site.data.keyword.webide}} 外部での編集
{: #editlocal}

{{site.data.keyword.webide}} の他にエディターを使用するには、任意のツールでプロジェクト・ファイルを直接処理できるように {{site.data.keyword.Bluemix_live}} をセットアップします。{{site.data.keyword.Bluemix_live_notm}} は、ローカル・ファイル・システムでの変更を {{site.data.keyword.jazzhub}} 内のクラウド・ワークスペースと同期化するコマンド・ライン・アプリケーションです。 

### 始めに 

[{{site.data.keyword.Bluemix_live_notm}} コマンド・ライン・インターフェースをダウンロードしてインストールします (新しいウィンドウでリンクが開きます)](http://livesyncdownload.ng.bluemix.net){: new_window}。

### ローカル環境と {{site.data.keyword.Bluemix_notm}} の同期化
{: #edit_local_download}

1. コマンド・ライン・ウィンドウを開きます。
2. {{site.data.keyword.Bluemix_notm}} にサインインします。

	```
	bl login
	```
	{: pre}

3. プロンプトが出されたら、IBMid とパスワードを入力します。
4. {{site.data.keyword.Bluemix_notm}} プロジェクトのリストを表示します。 

	```
	bl projects
	```
	{: pre}

4. ローカル環境を {{site.data.keyword.Bluemix_notm}} 上のプロジェクトと同期化します。

	```
	bl sync projectName
	```
	{: pre}

ここで、`projectName` は {{site.data.keyword.Bluemix_notm}} アプリの名前です。

編集が完了したら、`q` を入力して同期化を終了します。

### コードをローカルに編集するための Desktop Sync 機能の有効化

Desktop Sync フィーチャーは、コマンド・ラインの Live Edit モードに似ています。コマンド・ラインでのデバッグのためには、Desktop Sync フィーチャーが必要です。
1. 別のコマンド・ライン・ウィンドウで、Desktop Sync フィーチャーを使用可能にします。

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. {{site.data.keyword.webide}} で作成した起動構成を使用します。起動構成を選択した後、Desktop Sync フィーチャーがローカル環境で使用可能になります。開いたばかりのコマンド・ライン・ウィンドウで、アプリの URL、デバッグ URL、管理 URL を表示でき、{{site.data.keyword.Bluemix_live_notm}} の状態を表示できます。


3. ブラウザーを最新表示し、ローカル・ワークスペース内の静的ファイルに保存した変更内容が表示されることを確認します。 

### Desktop Sync 機能の無効化

1. 2 つ目のコマンド・ライン・ウィンドウで、`bl stop` と入力します。
2. 最初のコマンド・ライン・ウィンドウで、`q` と入力します。
