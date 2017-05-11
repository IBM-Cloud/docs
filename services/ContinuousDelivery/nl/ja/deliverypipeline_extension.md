---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-16"

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

# {{site.data.keyword.deliverypipeline}} の拡張
{: #deliverypipeline_extending}

サポートされるサービスを使用するようにジョブを構成することで、{{site.data.keyword.deliverypipeline}} の機能を拡張できます。例えば、テスト・ジョブで静的コード・スキャンを実行し、ビルド・ジョブで文字列をグローバル化できます。{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->

次のタスクは、選択されたツールを Delivery Pipeline と統合する方法を説明します。

## パイプラインを使用した静的コード・スキャンの実行

{: #deliverypipeline_scan}

コードをデプロイする前にコードのセキュリティー問題を検索したい場合、IBM® Static Analyzer for Bluemix™ をパイプラインの一部として使用すると、Java™ アプリの静的 `.war`、`.ear`、`.jar`、または `.class` ビルド・バイナリー・ファイルに対して自動化チェックを実行できます。

Static Analyzer サービスを使用するパイプラインは、通常以下のステージを含みます。

+ ソース・ファイルをビルドするためのビルド・ステージ
+ 以下のジョブを含む処理ステージ
  + Static Analyzer サービスを実行するためのビルド・ジョブ
  + コンテナー・ビルドを実行するビルド・ジョブ
+ コンテナーをデプロイするためのデプロイ・ステージ


### 静的コード・スキャンの作成

開始する前に、[サービスのご利用条件を確認します![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/software/sla/sladb.nsf/sla/bm-6814-01){: new_window}。

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. 処理ステージを作成します。

  a. **「ステージの追加」**をクリックします。

  b. ステージに`「処理」`などの名前を付けます。

  c. 入力タイプに**「ビルド成果物」**を選択します。

  d. ステージとジョブの値を確認し、必要であれば値を更新します。

2. この処理ステージに、コード・スキャンを実行するためのビルド・ジョブを追加します。

  a. **「ジョブ」**タブで、**「ジョブの追加 (ADD JOB)」**をクリックします。

  b. ジョブ・タイプに**「テスト」**を選択します。

  c. テスター・タイプに**「IBM Security Static Analyzer」**を選択します。

  d. 組織とスペースの値を確認し、必要であれば値を更新します。

  e. 必要に応じて**「サービスとスペースの自動セットアップ」**チェック・ボックスを選択またはクリアします。

    * サービス用の Bluemix のスペースと、サービスをコンテナーにバインドするアプリを、パイプラインで確認する場合は、このチェック・ボックスを選択します。サービスやバインドされたアプリが存在しない場合、パイプラインによって、このサービスの無料プランがご使用のスペースに追加されます。作成されたバインド済みアプリには、`pipeline_bridge_app` という名前が付けられます。その後、パイプラインは、pipeline_bridge_app からの資格情報を使用して、バインド済みサービスにアクセスします。

    * サービスとバインド済みアプリを Bluemix のスペースで構成してある場合、または[これらの要件を手動で構成する](/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline){: new_window}場合は、このチェック・ボックスをクリアします。

  f. **「分析の完了を待機する時間」**フィールドで、0 から 59 分の値を入力します。デフォルト値は 5 分です。ジョブ終了時、Static Analyzer ダッシュボードの URL がコンソール・ログに記録されます。

     Static Analyzer のスキャンが指定した時間までに終了しない場合は、ジョブは失敗します。しかし、スキャンの分析は実行を続行し、Static Analyzer ダッシュボードで表示することができます。Static Analyzer スキャンの完了後に、ジョブを再実行した場合、スキャン要求は再実行依頼されず、パイプライン・ジョブは完了できます。また、正常に終了したスキャン結果でパイプラインをブロックされないように構成することもできます。手順については、次のステップを参照してください。

  g. このジョブが失敗またはタイムアウトになる場合の対応に応じて、**「このジョブが失敗したらこのステージの実行を停止する (Stop running this stage if this job fails)」**チェック・ボックスを選択またはクリアします。脆弱性が高い場合、ジョブは失敗する可能性があります。

    * このチェック・ボックスを選択した状態でジョブが失敗した場合、このステージ内の後続のジョブと後続のステージは実行されません。

    * このチェック・ボックスをクリアした状態でジョブが失敗した場合、ステージは後続のジョブとステージをブロックせずに続行します。例えば、処理すべき多くの問題がレポートに含まれていることが分かっている場合、スキャンには長時間かかる可能性があるため、続行するようにステージを構成するという選択肢もありえます。こうしたシナリオでは、単にスキャンに時間がかかりすぎるという理由だけで残りのジョブとステージの実行を停止するのは避けたいと考えられます。

  h. **「保存」**をクリックします。

3. ジョブが終了したら、**「ログおよび履歴の表示」**をクリックして結果を表示します。分析が成功またはタイムアウトになった場合、スキャン結果に URL が表示されます。スキャン状況が処理中になっている場合は、スキャンが完了して全結果が表示されるまで待ちます。

4. 分析が終了する前に再度処理ステージの実行が必要な場合は、実行可能です。しかし、次のような状況では、新しい分析は再実行依頼されず、前回の結果が使用されます。
  * 新しい分析を始めたときに処理ステージが実行中だった場合
  * ビルドのスキャンがすでに実行依頼されている場合
  * 新しいソース・ビルドがまだ実行されていない場合

5. 新しい分析を始動するには、次のいずれかの手順を実行します。
  * 処理ステージに入力するビルド・ステージを実行してから、処理ステージを再度実行します。
  * スキャン結果の URL を開き、**「ごみ箱」**アイコンをクリックします。その後、処理ステージを再度実行します。

コンソール出力例:

**成功したスキャン**
![成功したスキャンの例](images/analyzer_success.png)

**保留中のスキャン**
![保留中のスキャンの例](images/analyzer_pending.png)

Static Analyzer サービスの使用について詳しくは、[Static Analyzer サービスの資料](/docs/services/ApplicationSecurityonCloud/index.html){: new_window}を参照してください。

<!--

## Globalizing strings by using the pipeline
{: #deliverypipeline_globalize}

You can translate strings automatically into other languages when you use the IBM Globalization Pipeline service with your pipeline. IBM Globalization Pipeline uses machine translation to translate your source files as part of the pipeline's build and deployment process.

You can also update the machine-translated strings within the globalization project. A translator or native speaker of the language can then review the machine-translated strings to ensure that they are of a high quality.

To see an example of a typical pipeline that uses the Globalization Pipeline service, watch this video:

<iframe width="640" height="360" src="https://www.youtube.com/embed/UToj7FIomCg?feature=player_embedded" frameborder="0" allowfullscreen></iframe>

### Creating a globalization stage and job
Before you begin:

1. All English-translatable strings should be included in one or more `filename_en.properties` or `filename_en.json` files that all use the same name. For example: `messages_en.properties`.

2. If your messages are in `.json` files, remove the depth from the structure by removing any subkeys. To remove the subkeys, change instances of `{key: {subkey: value, subkey:value}}` to `{key:value, key:value}`.

To create the globalization stage and job:

1. Create a globalization stage.

  a. Click **ADD STAGE**.

  b. Name the stage; for example, `Globalization`.

  c. For the input type, select **SCM repository**.

2. In the globalization stage, add a job to translate the source files.

  a. On the **JOBS** tab, click **ADD JOB**.

  b. For the job type, select **Build**.

  c. For the builder type, select **IBM Globalization Pipeline**.

  d. For the organization and space, verify the values and update them if needed.

  e. In the **Source file name** field, type the name and extension of the `.properties` or `.json` input file. If you have files in different subdirectories, but they all have the same name, you need to type the file name once only. For example, if you have a `messages_en.properties` file in three directories, type `messages_en.properties` for the source file name, and all files with that name will be translated.

  f. Determine whether to select the **Set up service and space for me** check box.

    * If you want the pipeline to check your Bluemix space for the service and an app that binds the service to the container, select this check box. If the service or bound app does not exist, the pipeline adds the free plan of the service to your space for you. The bound app that is created is named `pipeline_bridge_app`. Then, the pipeline uses the credentials from pipeline_bridge_app to access the bound services.

    * If you configured the service and bound app in your Bluemix space already or if you want to [configure these requirements manually](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline), leave this check box cleared.

  g. For the Globalization bundle prefix, enter a prefix for the bundle name, which is structured in this format: `<globalization_bundle_prefix>.path.to.source.file`. The pipeline job creates this Globalization bundle for you in the Globalization Pipeline service.

    **Tip:** Use the DevOps Services project name in the prefix so that the project can be identified easily in the Globalization Pipeline service.

  h. Click **SAVE**.

3. Create another stage to package your app. For the input of the job in this stage, use the IBM Globalization Pipeline job from the previous stage. Do not use the source as the input. The Globalization Pipeline job augments the source files with the machine-translated strings.

4. To ensure that the machine-translated content is included in the packaged app, create another stage to package the app in. For the input to that stage, include the Globalization Pipeline job.

The machine translated files are placed in the same directory as the source `.properties` or `.json` file. To view the files, click **Job > Artifacts**.

After the stage is completed, you can review the translated files from the console output. You can also direct translators to the files so that they can review the machine-translation output and provide revisions to improve quality. The revisions are stored in a Cloudant™ database and take precedence over any future machine translations of the same strings.

For more information about using the Globalization Pipeline service from the Bluemix Dashboard, [see the Globalization Pipeline service documentation](https://www.ng.bluemix.net/docs/services/GlobalizationPipeline/index.html).

-->

## パイプラインでのビルドの Slack 通知の作成
{: #deliverypipeline_slack}

IBM Container Service、IBM Security Static Analyzer、IBM Globalization のビルド結果に関する通知を Delivery Pipeline から Slack チャネルに送信できます。

始める前に、以下のように Slack WebHook URL を作成するかコピーします。

1. チームの Slack Integration ページを開きます。`https://_project_name_.slack.com/services`
2. 統合のリストで、**「着信 WebHook (Incoming WebHooks)」**を見つけて**「追加 (Add)」**をクリックします。
3. チャネルを選択し、**「着信 WebHook 統合の追加 (Add Incoming WebHooks Integration)」**をクリックします。
4. **WebHook URL** を追加するか、既存のものをコピーします。

詳しくは、[Slack の Incoming WebHook 資料![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://api.slack.com/incoming-webhooks){: new_window}を参照してください。

Slack 通知を作成するには、次のようにします。

1. パイプラインで、ステージの構成を開きます。
2. **「環境プロパティー」**タブで、**「プロパティーの追加」**をクリックします。
3. **「文字プロパティー」**を選択します。
4. 環境プロパティーの名前と値を入力します。操作を繰り返して、複数の環境プロパティーを作成します。

  *表 1. Slack 通知を構成する環境プロパティー*

  <table>
  <tr>
  <th>名前</th>
  <th>値</th>
  <th>説明</th>
  <tr/>
  <tr>
    <td><code>SLACK_WEBHOOK_PATH</code></td>
    <td>URL</td>
    <td>必須。Slack プロジェクトの設定に保存される WebHook URL です。</td>
  </tr>
  <tr>
    <td><code>SLACK_COLOR</code></td>
    <td>以下のいずれかの値を入力できます。
      <ul><li><code>good</code></li>
      <li><code>warning</code></li>
      <li><code>danger</code></li>
      <li>#439FEO などカラーの 16 進数</li></ul></td>
    <td>オプション。Slack のメッセージの横に表示される境界線の色。デフォルトの色は、良いメッセージは緑、悪いメッセージは赤、情報メッセージは灰色です。</td>
  </tr>
  <tr>
    <td><code>NOTIFY_FILTER</code></td>
    <td>メッセージ・タイプのサブセットのみを受け取るには、以下のいずれかの値を入力します。
      <ul>
      <li><code>good</code>: 不明メッセージ、良いメッセージ、情報メッセージのみを取得します。悪いメッセージは送信されません。</li>
      <li><code>bad</code>: すべてのメッセージを取得します。</li>
      <li><code>info</code>: 情報メッセージのみを取得します。良いメッセージ、悪いメッセージ、不明メッセージは送信されません。</li>
      <li><code>unknown</code>: すべてのメッセージを取得します。</li></ul>
      例: <code>NOTIFY_FILTER = bad</code> と設定した場合、Slack チャネルでエラー通知のみが表示されます。</td>
    <td>オプション。通知を送信するメッセージのタイプを決定します。デフォルトでは、良いメッセージと悪いメッセージが送信されますが、情報メッセージは送信されません。
      <ul><li><code>good</code>: 成功したビルドの結果。</li>
      <li><code>bad</code>: 失敗したビルドの結果。</li>
      <li><code>info</code>: ビルド・プロセスに関する情報メッセージ。</li>
      <li><code>unknown</code>: 不明メッセージには、タイプは割り当てられません。</li></ul></td>
   </table>

5. **「保存」**をクリックします。

6. 上記ステップを繰り返し、IBM Container Service、IBM Security Analyzer、IBM Globalization ジョブが含まれる他のステージについて Slack 通知を送信するようにします。

Slack で表示されるビルド通知には、プロジェクトへのリンクが含まれます。場合によっては、プロジェクトのダッシュボードへのリンクが含まれることもあります。Slack ユーザーがこれらのリンクを開くには、そのユーザーが Bluemix に登録されていて、かつパイプラインが構成されているプロジェクトのメンバーでなければなりません。

## パイプラインでのビルドの HipChat 通知の作成
{: #deliverypipeline_hipchat}

IBM Container Service、IBM Security Static Analyzer、IBM Globalization のビルド結果に関する通知を Delivery Pipeline から HipChat ルームに送信できます。

始める前に、以下のように HipChat トークンを作成するか既存のものをコピーします。

1. チームの HipChat アカウント・ページに移動します。`https://_project_name_.hipchat.com/account/api`
2. 新しいトークンを作成するか、既存のトークンを使用します。

HipChat 通知を作成するには、次のようにします。

1. パイプラインで、ステージの構成を開きます。
2. **「環境プロパティー」**タブで、**「プロパティーの追加」**をクリックします。
3. **「文字プロパティー」**を選択します。
4. 環境プロパティーの名前と値を入力します。操作を繰り返して、複数の環境プロパティーを作成します。

  *表 2. HipChat 通知を構成する環境プロパティー*

  <table>
  <tr>
  <th>名前</th>
  <th>値</th>
  <th>説明</th>
  </tr>
  <tr>
    <td><code>HIP_CHAT_TOKEN</code></td>
    <td>英数字ストリング</td>
    <td>必須。上の『始める前に』で、HipChat トークンの作成または既存トークンのコピーの手順を参照してください。</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_ROOM_NAME</code></td>
    <td>ルームの名前</td>
    <td>必須。</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_COLOR</code></td>
    <td>以下のいずれかの値を入力します。
      <ul><li><code>yellow</code></li>
      <li><code>red</code></li>
      <li><code>green</code></li>
      <li><code>purple</code></li>
      <li><code>gray</code></li>
      <li><code>random</code></li></ul>
    </td>
    <td>オプション: HipChat 通知の背景色と枠のカラーを指定します。<code>HIP_CHAT_COLOR</code> を設定する場合、このスクリプトを呼び出すときに色を指定する必要はありません。
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_COLOR</code></td>
    <td>以下のいずれかの値を入力します。
      <ul><li><code>good</code></li>
      <li><code>danger</code></li>
      <li><code>info</code></li></ul>
    この変数は、HipChat 通知と Clack 通知の両方のカラーに適用されます。<code>NOTIFICATION_COLOR</code> を指定する場合、<code>HIP_CHAT_COLOR</code> も <code>SLACK_COLOR</code> も指定する必要はありません。</td>
    <td>オプション: HipChat 通知と Slack 通知の両方の背景色と枠のカラーを指定します。<code>NOTIFICATION_COLOR</code> を設定する場合、このスクリプトを呼び出すときに色を指定する必要はありません。
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_LEVEL</code></td>
    <td>以下のいずれかの値を入力します。
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul></td>
    <td>オプション: 通知レベルを指定します。何が通知をトリガーするのかについて詳しくは、<code>NOTIFICATION_FILTER</code> を参照してください。</td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_FILTER</code></td>
    <td>以下のいずれかの値を入力します。
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul>
    <td>オプション: 通知フィルター・レベルを指定します。以下のパラメーターが一致するときに通知が送信されます。
      <ul><li><code>NOTIFICATION_FILTER = good</code> および <code>NOTIFICATION_LEVEL = bad</code>、<code>good</code>、または <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = info</code> および <code>NOTIFICATION_LEVEL = bad</code>、<code>good</code>、<code>info</code>、または <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = bad</code> および <code>NOTIFICATION_LEVEL = bad</code> または <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = unknown</code> および <code>NOTIFICATION_LEVEL = bad</code>、<code>good</code>、または <code>unknown</code></li></ul></td>
    </tr>
  </table>

5. **「保存」**をクリックします。

6. 上記ステップを繰り返し、IBM Container Service、IBM Security Static Analyzer、IBM Globalization ジョブが含まれる他のステージについて HipChat 通知を送信するようにします。

## パイプラインでデプロイメントのダウン時間をゼロにする Active Deploy の使用
{: #deliverypipeline_activedeploy}

Delivery Pipeline で IBM® Active Deploy サービスを使用して、アプリまたはコンテナー・グループの継続デプロイメントを自動化できます。概要について詳しくは、[Active Deploy の資料](/docs/services/ActiveDeploy/updatingapps.html#adpipeline){: new_window}を参照してください。

## パイプラインでのコンテナー・イメージのビルドとデプロイ
{: #deliverypipeline_containers}

IBM Continuous Delivery Pipeline for Bluemix を使用して、Bluemix へのアプリのビルドとコンテナーのデプロイメントを自動化できます。Delivery Pipeline サービスは以下をサポートします。
  - Docker イメージのビルド
  - Bluemix へのコンテナーのイメージのデプロイ

概要について詳しくは、[Delivery Pipeline とコンテナーの概要](/docs/containers/container_pipeline_ov.html#container_pipeline_ov){: new_window}を参照してください。
