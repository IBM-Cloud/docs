# bl コマンド

*最終更新日:* 2015 年 11 月 13 日

Node.js アプリケーションを作成する場合、Bluemix™ Live Sync を使用して、Bluemix で実行中のアプリケーション・インスタンスを即時に更新して、デスクトップの場合と同じように再デプロイせずに開発することができます。変更を行うと、実行中の Bluemix アプリケーションでその変更を即時に確認できます。Bluemix Live Sync コマンド・ライン・インターフェースは *bl* と呼ばれます。

**bl** コマンド・ライン・インターフェース・コマンドを使用して、次のタスクを完了できます。

* Bluemix で実行中のアプリケーションの開始と停止。
* デスクトップからのクラウド・ベースのプロジェクトの新規作成。
* デスクトップの変更を、クラウド・ベースのプロジェクト・ワークスペースおよび Bluemix で実行中のアプリケーションに同期。
* 同期に使用可能なプロジェクトのリストの表示。
* 実行中のアプリケーションの状況の表示。

bl コマンドのダウンロードと使用について詳しくは、[Bluemix Live Sync](https://www.ng.bluemix.net/docs/manageapps/bluemixlive.html#bluemixlive) を参照してください。

## bl コマンド

Bluemix Live Sync コマンド・ライン **bl** の構文は次のとおりです。

``` bl command [arguments][options] [--help]```

### command
<dl>
<dt>login、l</dt>
<dd>Bluemix にログインします。</dd>
<dt>logout、lo</dt>
<dd>ユーザーをログアウトします。</dd>
<dt>sync、s</dt>
<dd>デスクトップとサーバー間の同期処理を開始します。</dd>
<dt>create、c</dt>
<dd>プライベート・プロジェクトを作成し、それをこのディレクトリー内の Git リポジトリーにリンクし、コンテンツを Bluemix にデプロイします。</dd>
<dt>projects、p</dt>
<dd>同期に使用可能なすべてのプロジェクトをリストします。</dd>
<dt>start、st</dt>
<dd>Bluemix のアプリケーション・インスタンスを開始します。</dd>
<dt>stop、sp</dt>
<dd>Bluemix のアプリケーション・インスタンスを停止します。</dd>
<dt>status、ss</dt>
<dd>Bluemix の実行中アプリケーション・インスタンスの状況をリストします。</dd>
</dl>

### arguments
<dl>
<dd>コマンドの引数。</dd>
</dl>

### options
<dl>
<dd>コマンドのオプション。</dd>
</dl>

### グローバル・オプション
<dl>
<dt>--help</dt>
<dd>指定されたコマンドのヘルプ・ページを表示します。</dd>
<dt>--verbose</dt>
<dd>詳細ロギングを有効にします。</dd>
</dl>

**注:** 引数またはオプションにスペースが含まれる場合、値を二重引用符で囲んでください。
