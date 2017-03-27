---



copyright:

  years: 2015，2017

lastupdated: "2016-03-02"



---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:download: .download}

# Git を使用したコーディングの開始

{{site.data.keyword.Bluemix}} に自動的にデプロイする、ホストされた Git リポジトリーを作成することができます。次に、その Git リポジトリーに変更をプッシュすることにより、アプリで実行されるコードを変更することができます。
{:shortdesc}

1. 開始するには、アプリの「概要」ページで、**「Git リポジトリーおよびパイプラインの追加」**をクリックするか、{{site.data.keyword.Bluemix_notm}} Classic Experience で**「Git の追加」**をクリックします。
2. オープンしたウィンドウで、**「リポジトリーにスターター・アプリ・パッケージを取り込み、Build & Deploy パイプラインを使用可能にします」**チェック・ボックスが選択されていることを確認します。Git リポジトリーが作成されました。スターター・コードが使用可能な場合、リポジトリーにロードされます。さらに、{{site.data.keyword.jazzhub}} で実行されている Delivery Pipeline サービスによってアプリケーションもデプロイされます。
3. アプリを更新するには、コマンド・ラインまたは Web IDE を使用します。
**コマンド・ラインを使用する場合は、次のようにします。**
   a. アプリの「概要」ページの Git URL から Git リポジトリーを複製します。
   b. お好きなエディターでコードを更新します。
   c. Git コマンド・ライン・インターフェースから変更をプッシュします。

   **Web IDE を使用する場合は、次のようにします。**
   a. アプリの「概要」ページで、**「コードの編集」**をクリックします。Web IDE でプロジェクトが開きます。
   b. 必要に応じて変更を行い、次に、組み込み Git サポートを使用してプッシュします。

更新されたアプリが {{site.data.keyword.Bluemix_notm}} に再デプロイされます。

ステップごとの詳しい手順の説明については、[Set up Git integration and auto-deploy in DevOps Services ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://hub.jazz.net/tutorials/jazzeditor/#git_integration_and_autodeployment){: new_window} を参照してください。

## Git を追加しましたか。{{site.data.keyword.Bluemix_notm}} Live Sync を試してください

Node.js アプリをビルドする場合、{{site.data.keyword.Bluemix_notm}} Live Sync を使用すれば、{{site.data.keyword.Bluemix_notm}} 上のアプリ・インスタンスを素早く更新でき、デスクトップ上で行う場合と同じように開発することができます。

{{site.data.keyword.Bluemix_notm}} Live Sync について詳しくは、『[{{site.data.keyword.Bluemix_notm}} Live Sync](/docs/develop/bluemixlive.html)』を参照してください。コマンドについて詳しくは、[{{site.data.keyword.Bluemix_notm}} Live Sync CLI の資料](/docs/cli/reference/bl/index.html)を参照してください。{{site.data.keyword.Bluemix_notm}} Live Sync を Web IDE とともに使用するには、『[Live Edit](/docs/develop/bluemixlive.html)』を参照してください。

始める前に、{{site.data.keyword.Bluemix_notm}} Live Sync bl コマンド・ラインをダウンロードし、インストールします。

**重要:** bl コマンド・ライン・ツールは、Windows 7 と 8、および Mac OS X バージョン 10.9 以降でのみ使用可能です。

<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="(新しいタブまたはウィンドウで開きます)"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="「Windows bl コマンド・ラインのダウンロード」ボタン" /> </a>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="(新しいタブまたはウィンドウで開きます)"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="「Mac bl コマンド・ラインのダウンロード」ボタン" /> </a>
</p>

1. コマンド・ラインで、以下のコマンドを入力してログインします。
```
bl login
```
プロンプトが出されたら、{{site.data.keyword.ibmid}} とパスワードを入力します。

2. 以下のコマンドを入力して、{{site.data.keyword.Bluemix_notm}} Live Sync で同期できるプロジェクトのリストを表示します。

```
bl projects
```
ご使用のアプリケーションに一致するプロジェクト名をリスト内で見つけます。プロジェクト名のフォーマットは、
*your alias* | *your application name* です。
3. 以下のコマンドを入力し、ローカル環境を {{site.data.keyword.Bluemix_notm}} 上のプロジェクトと同期させます。プロジェクトの所有者なら、projectName に your-application-name を指定すれば済みます。
<!--- this command needs italicized parameters projectName localDirectory and yellow on 'local' -->
```
bl sync projectName -d localDirectory --verbose
```
このコマンドは、「q」を入力するまで継続して実行されます (そして同期化が続行されます)。--verbose オプションにより、ロギング情報と状況情報が表示されます。引数に空白を含むものがある場合は、名前を引用符で囲む必要があります。
4. 別のコマンド・ライン・ウィンドウのローカル・ディレクトリーで以下のコマンドを入力し、アプリケーションを Live Edit モードで {{site.data.keyword.Bluemix_notm}} にデプロイします。

```
bl start
```

ローカル・ディレクトリーにあるファイルを変更すると、その変更内容は、{{site.data.keyword.Bluemix_notm}} で稼動しているアプリケーションとプロジェクト・クラウド・ワークスペースの両方に自動的に伝搬します。
Node アプリケーションの再始動が必要な場合は、以下のコマンドを使用できます。

```
bl start --restart 
```
