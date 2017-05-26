---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Eclipse Orion Web IDE での開発
{: #web_ide}

Eclipse Orion {{site.data.keyword.webide}} は、Web 開発を行うことのできるブラウザ・ベスの開発環境です。コンテンツ・アシスト、コド補完、エラ・チェックによる支援を利用して JavaScript、HTML、CSS での開発を行うことができます。{{site.data.keyword.webide}} は、ほとんどすべての言語に対応しており、大部分のファイル・タイプに対して構文の強調表示を提供します。ソス管理が組み込まれており、コドをロカルにデプロイしてアプリのテストとデバッグを行うことができます。
{:shortdesc}

何よりも良い点は、{{site.data.keyword.webide}} が Web ベスであるという点です。インストルが必要なものは何もなく、保守や拡大縮小が必要なものも何もありません。インタネット接続さえあれば、どこでも開発を行うことができます。

## IDE のセットアップ
{: #editorsetup}

{{site.data.keyword.webide}} はカスタマイズ可能であり、開発ニズに合わせて、カラ・スキム、テクニカル・ツル、および設定を選択することができます。これらの設定を表示したり変更したりするには、左側のメニュから**「設定」**アイコン<img class="inline" src="images/webide_settings_icon_light_small.png"  alt="設定アイコン">をクリックします。


編集中にしばしば設定を変更する必要がある場合は、**「ロカル・エディタ設定」**アイコン <img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="「ロカル・エディタ設定」アイコン">から簡単に設定にアクセスできます。 

![ロカル・エディタ設定](images/webide_local_editor_settings_light.png)

デフォルトでは、エディタ・スタイルとフォント・サイズの設定が常に表示されます。他のエディタ設定をメニュに含めるには、以下の手順を実行します。

1. **「ロカル・エディタ設定」**アイコン<img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="「ロカル・エディタ設定」アイコン">をクリックします。

2. **「エディタ設定」**をクリックします。

3. **「ロカル・エディタ設定」**メニュから設定を組み込んだり除外したりするには、各設定の横の星印をクリックします。

![「エディタ設定」トグル](images/webide_editor_settings_toggle_light.png)


## コドの編集
{: #editcode}

{{site.data.keyword.webide}} には、2 つの主要セクションがあります。1 つ目のセクションはファイル・ナビゲタであり、プロジェクト・ファイルがツリ構造で表示されます。ファイル・ナビゲタから、ファイルとフォルダの作成、名前変更、削除、管理を行うことができます。

**ヒント:** ファイルをファイル・ナビゲタにアップロドするには、対象のファイルをコンピュタからファイル・ナビゲタにドラッグします。

2 つ目のセクションはエディタ・ペインです。このエディタは、コンテンツ・アシストや構文検査など、いくつかのコディング機能を備えています。

![Web IDE](images/webide_light.png)

### 複数のファイルの処理
1. 2 つのファイルを同時に操作するには、**「分割エディタ・モドを変更します」**アイコン<img class="inline" src="images/webide_split_editor_icon_light_small.png"  alt="「分割エディタ」アイコン">をクリックします。
2. 開いたメニュから、1 つのビュを選択します。

 ビュを選択した後、既にエディタで開かれていたファイルがある場合、そのファイルは両方のエディタ・ビュに表示されます。

 一方のエディタ・ビュに表示されているファイルをオプンまたは変更するには、次のようにします。
 1. 変更するエディタ・ビュにカソルを移動します。
 2. ファイル・ナビゲタで、いずれかのファイルをクリックします。

### キボド・ショトカット
{{site.data.keyword.webide}} の大部分のコマンドは、キボド・ショトカットでのみアクセス可能です。

エディタのキボド・ショトカットのリストを表示するには、Alt+Shift+? を押します。Mac OS を使用している場合は、Ctrl+Shift+? を押します。

## ソス・コドの管理
{: #sourcecontrol}

{{site.data.keyword.webide}} は、ソス・コド管理ツルと統合されています。Git リポジトリに関する作業を行うには、**「Git リポジトリ」**アイコン<img class="inline" src="images/webide_git_icon_light_small.png"  alt="「Git リポジトリ」アイコン">をクリックします。 

 **ヒント**: {{site.data.keyword.webide}} をオプン・ツルチェンと共に使用している場合、ワクスペスには GitHub、{{site.data.keyword.ghe_short}}、または Git Repos and Issue Tracking のリポジトリが事前に取り込まれます。現行のツルチェンと関連付けられているリポジトリは強調表示されます。


## ワクスペスからのアプリのデプロイ
{: #deploy}

1. アプリをデプロイするには、実行バから、起動構成を選択または作成します。
1. 「デプロイ」アイコン<img class="inline" src="images/webide_deploy_button_light_small.png"  alt="「デプロイ」アイコン">をクリックします。ワクスペスの現在の内容と、起動構成に定義された環境を使用して、アプリのインスタンスがデプロイされます。 
2. アプリがデプロイされた後、実行バを使用して、アプリの停止、再始動、デバッグ、ログの表示などを行うことができます。![実行バ](images/webide_runbar_light.png)    

<!-- 3/6/2016: bl commands don't work with V2/CD 
## Editing outside of the {{site.data.keyword.webide}}
{: #editlocal}

To use an editor besides the {{site.data.keyword.webide}}, set up {{site.data.keyword.Bluemix_live}} so that you can work directly with your project files in any tool. {{site.data.keyword.Bluemix_live_notm}} is a command-line application that synchronizes the changes in your local file system with your cloud workspace in {{site.data.keyword.jazzhub}}. 

### Before you begin 

Download and install the [{{site.data.keyword.Bluemix_live_notm}} command-line interface![External link icon](../../icons/launch-glyph.svg "External link icon")](http://livesyncdownload.ng.bluemix.net){: new_window}.

### Synchronizing your local environment with {{site.data.keyword.Bluemix_notm}}
{: #edit_local_download}

1. Open a command-line window.
2. Sign in to {{site.data.keyword.Bluemix_notm}}:

	```
	bl login
	```
	{: pre}

3. When you are prompted, enter your IBMid and password.
4. View a list of your {{site.data.keyword.Bluemix_notm}} projects: 

	```
	bl projects
	```
	{: pre}

4. Synchronize your local environment with your project on {{site.data.keyword.Bluemix_notm}}:

	```
	bl sync projectName
	```
	{: pre}

where `projectName` is your {{site.data.keyword.Bluemix_notm}} app's name.

When you are finished editing, enter `q` to end synchronization.

### Enabling the Desktop Sync feature to edit code locally

The Desktop Sync feature is like Live Edit mode for the command line. You need the Desktop Sync feature to debug on the command line.
1. In another command-line window, enable the Desktop Sync feature:

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. Use the launch configuration that you created in the {{site.data.keyword.webide}}. After you select the launch configuration, the Desktop Sync feature is enabled in your local environment. In the command-line window that you just opened, you can view the app's URL, the debug URL, the manage URL, and view the {{site.data.keyword.Bluemix_live_notm}} state.

3. Refresh the browser and verify that you can see the changes that you saved to static files in the local workspace. 

### Disabling the Desktop Sync feature

1. In the second command-line window, enter `bl stop`.
2. In the first command-line window, enter `q`.

--> 
