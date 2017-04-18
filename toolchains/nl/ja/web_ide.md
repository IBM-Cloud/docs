---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Eclipse Orion {{site.data.keyword.webide}} によるコードの編集
{: #web_ide}

最終更新日: 2016 年 9 月 9 日
{: .last-updated}

Eclipse Orion {{site.data.keyword.webide}} は、Web 向けの開発を行うためのブラウザー・ベースの開発環境です。JavaScript、HTML、CSS での開発が可能であり、コンテンツ・アシスト、コード補完、エラー・チェックの機能を備えています。{{site.data.keyword.webide}} はほぼすべての言語に対応しており、ほとんどの[ファイル・タイプ (リンク先が新しいウィンドウで開きます)](https://hub.jazz.net/docs/overview/#dev_support){: new_window} で構文の強調表示が可能です。Git または Jazz の SCM によるソース管理機能が組み込まれており、ローカル環境にコードをデプロイしてアプリのテストやデバッグを実行できるようになっています。
{:shortdesc}

何よりも、{{site.data.keyword.webide}} は Web が基盤になっています。インストールもメンテナンスもスケーリングも不要です。インターネット接続さえあれば、どこでも開発作業を行えます。

## エディターの設定
{: #editorsetup}

{{site.data.keyword.webide}} はカスタマイズが可能なので、それぞれの開発要件に合わせてカラー・スキームやテクニカル・ツールや設定を選択できます。設定を表示して変更するには、左側のメニューから**「設定」**アイコン<img class="inline" src="./images/webide_settings_icon.png"  alt="「設定」アイコン">をクリックします。

編集中にしばしば設定を変更する必要がある場合は、エディターの右上隅にある**「ローカル・エディター設定」**アイコン <img class="inline" src="./images/webide_local_settings_icon.png"  alt="「ローカル・エディター設定」アイコン">から簡単に設定にアクセスできます。

![ローカル・エディター設定](images/webide_local_editor_settings.png)

デフォルトでは、エディターのスタイルやフォント・サイズの設定は常に表示されます。その他のエディター設定をメニューに組み込む場合は、以下の手順を実行してください。

1. **「ローカル・エディター設定」**アイコン<img class="inline" src="./images/webide_local_settings_icon.png"  alt="「ローカル・エディター設定」アイコン">をクリックします。

2. **「エディター設定」**をクリックします。

3. **「ローカル・エディター設定」**メニューで設定を組み込んだり除外したりするには、各設定の横にある円をクリックします。

![エディター設定の切り替え](images/webide_editor_settings_toggle.png)


## コードの編集
{: #editcode}

{{site.data.keyword.webide}} には 2 つの主なセクションがあります。1 番目のセクションは、左側のファイル・ナビゲーターです。そこにはプロジェクト・ファイルがツリー構造で表示されます。ファイル・ナビゲーターから、ファイルやフォルダーの作成、名前変更、削除、管理を実行できます。

**ヒント:** ファイル・ナビゲーターにファイルをアップロードするには、コンピューターからファイル・ナビゲーターにファイルをドラッグします。

2 番目のセクションは、右側のエディター・ペインです。エディターには、コンテンツ・アシストや構文検証などのコーディング機能が用意されています。

![Web IDE](images/webide.png)

### 複数のファイルの操作
1. 2 つのファイルを同時に操作するには、エディターの上部にある**「分割エディター・モードを変更します」**アイコン<img class="inline" src="./images/webide_split_editor_icon.png"  alt="「分割エディター」アイコン">をクリックします。
2. メニューが表示されたら、ビューを選択します。

 ビューを選択した時に、ファイルがすでにエディターで開かれていた場合は、両方のエディター・ビューに表示されます。

 いずれかのエディター・ビューで表示されているファイルを開いたり変更したりする場合は、以下のようにします。
 1. 変更するエディター・ビューにカーソルを移動します。
 2. ファイル・ナビゲーターでファイルをクリックします。

### キーボード・ショートカット
{{site.data.keyword.webide}} のほとんどのコマンドは、キーボード・ショートカットでのみアクセスできます。

エディターのキーボード・ショートカットのリストを参照するには、Alt+Shift+? を押してください。Mac OS を使用している場合は、Ctrl+Shift+? を押してください。

## ソース・コードの管理
{: #sourcecontrol}

{{site.data.keyword.webide}} には、ソース・コード管理ツールが統合されています。Git リポジトリーを操作するには、**「Git リポジトリー」**アイコン<img class="inline" src="./images/webide_git_icon.png"  alt="「Git リポジトリー」アイコン">をクリックします。詳しくは、[Git によるソース管理 (リンク先が新しいウィンドウで開きます)](https://hub.jazz.net/docs/git/){: new_window} を参照してください。


## ワークスペースからアプリをデプロイする方法
{: #deploy}

1. 実行バーからアプリをデプロイするには、起動構成を選択するか[作成 (リンク先が新しいウィンドウで開きます)](https://hub.jazz.net/tutorials/livesync/#launch_configuration){: new_window} します。
1. デプロイ・アイコン<img class="inline" src="./images/webide_deploy_button.png"  alt="デプロイ・アイコン">をクリックします。ワークスペースの現在のコンテンツと起動構成で定義されている環境に基づいて、アプリのインスタンスがデプロイされます。 
2. アプリがデプロイされたら、実行バーから、アプリの停止、再始動、デバッグ、ログの表示などの操作を実行できます。
![実行バー](images/webide_runbar.png)

<!-- LH: I'm commenting out the following list because I think this information is obvious from the UI. I also updated the preceding sentence to mention a few things that you can do from the run bar.

 * Stop the app: <img  class="inline" src="./images/webide_stop_button.png"  alt="The stop icon">
 * Open the deployed app: <img class="inline" src="./images/webide_open_app_url.png"  alt="The open app URL icon">
 * View the logs of the deployed app: <img class="inline" src="./images/webide_view_logs.png"  alt="The view logs icon">
 * Open the app's Dashboard: <img  class="inline" src="./images/webide_open_dashboard.png"  alt="The open dashboard icon">
 * If you are developing a Node.js app, enable Live Edit mode: <img  class="inline"  src="./images/webide_enable_live_edit.png"  alt="The enable live edit slider">
 * With Live Edit mode enabled, restart the app quickly, without redeployment: <img  class="inline" src="./images/webide_live_edit_restart.png"  alt="The Live Edit restart icon">
 * With Live Edit mode enabled, access the debugger: <img  class="inline" src="./images/webide_debug_icon.png"  alt="The debug icon"> -->

 ## {{site.data.keyword.webide}} の外部での編集
{: #editlocal}

{{site.data.keyword.webide}} 以外のエディターを使用する場合は、プロジェクト・ファイルを任意のツールで直接操作できるように {{site.data.keyword.Bluemix_live}} をセットアップする必要があります。{{site.data.keyword.Bluemix_live_notm}} は、ローカル・ファイル・システムの変更内容を {{site.data.keyword.jazzhub}} のクラウド・ワークスペースと同期するためのコマンド・ライン・アプリケーションです。 

### 始めに 

[{{site.data.keyword.Bluemix_live_notm}} コマンド・ライン・インターフェース (リンク先が新しいウィンドウで開きます)](http://livesyncdownload.ng.bluemix.net){: new_window} をダウンロードしてインストールします。

### ローカル環境と {{site.data.keyword.Bluemix_notm}} の同期
{: #edit_local_download}

1. コマンド・ライン・ウィンドウを開きます。
2. {{site.data.keyword.Bluemix_notm}} にサインインします。

	```
	bl login
	```
	{: pre}

3. IBMid とパスワードが要求されたら、それぞれを入力します。
4. {{site.data.keyword.Bluemix_notm}} プロジェクトのリストを表示します。 

	```
	bl projects
	```
	{: pre}

4. ローカル環境を {{site.data.keyword.Bluemix_notm}} のプロジェクトと同期します。

	```
	bl sync projectName
	```
	{: pre}

`projectName` は {{site.data.keyword.Bluemix_notm}} アプリの名前です。

編集が終わったら、`q` と入力して同期を終了します。

### デスクトップ同期機能を有効にしてローカル環境でコードを編集する方法

デスクトップ同期機能は、コマンド・ラインのライブ編集モードのようなものです。コマンド・ラインでデバッグを実行するには、デスクトップ同期機能が必要です。
1. 別のコマンド・ライン・ウィンドウでデスクトップ同期機能を有効にします。

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. {{site.data.keyword.webide}} で作成した起動構成を使用します。起動構成を選択すると、ローカル環境でデスクトップ同期機能が有効になります。先ほど開いたコマンド・ライン・ウィンドウで、アプリの URL、デバッグ URL、管理 URL、{{site.data.keyword.Bluemix_live_notm}} の状態を表示できます。

3. ブラウザーの表示を更新して、ローカル・ワークスペースの静的ファイルに保存した変更内容が表示されることを確認します。 

### デスクトップ同期機能を無効にする方法

1. 2 番目のコマンド・ライン・ウィンドウで `bl stop` と入力します。
2. 1 番目のコマンド・ライン・ウィンドウで `q` と入力します。
