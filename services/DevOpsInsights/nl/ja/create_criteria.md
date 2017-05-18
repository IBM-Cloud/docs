---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# ポリシーの定義
{: #policies}

ポリシーは、継続的デリバリー・パイプラインの中のゲートを制御します。
特定のゲートにおいて制定されているポリシーをコードが満たしていない、または超えていない場合、リスクのある変更版がリリースされることがないよう、デプロイメントが制止されます。
{:shortdesc}

ポリシーは {{site.data.keyword.DRA_short}} で定義します。
ポリシーは、{{site.data.keyword.DRA_short}} が含まれている {{site.data.keyword.Bluemix_notm}} 組織 (org) 内に作成されます。
同じ org 内のすべてアプリケーションが、そのポリシーを使用できます。
 

ポリシーを定義するには、次のようにします。


1. 左側のナビゲーションから、**「設定」**をクリックします。


2. **「ポリシー」**をクリックします。


3. **「ポリシーの作成 (Create Policy)」**をクリックしてから、新しいポリシーの名前と説明を入力します。


4. **「次へ」**をクリックします。

4. 以下のようにして、1 つ以上のルールをポリシーに追加します。
  1. **「ルールをポリシーに追加する (Add Rule to Policy)」**をクリックします。
  2. ルールのタイプを選択します。
  3. ルールの詳細情報と条件を入力します。
  4. **「保存」**をクリックします。

5. ルールをポリシーに追加し終えたら、**「完了」**をクリックします。

## ルールの作成
{: #criteria}

ルールは、ポリシーで成功か失敗かを判断するために使用する基準を定義します。
例えば、80% の単体テスト成功を求める単体テスト・ルールと、100% コード・カバレッジを求めるテスト・カバレッジ・ルールを含む「単体テストとテスト・カバレッジ」ポリシーを作成するとします。
パイプラインの中にこのルールを参照するゲートを追加すると、これらのルールの両方を満たさないビルドは、このゲートより先には進めなくなります。 

テストに重大のマークを付けることにより、どんな場合であろうと成功を必須とすることができます。
ルールを作成するには、ポリシーを選択して**「ルールをポリシーに追加する (Add Rule to Policy)」**をクリックします。
 

### functional-verification-test ルールの作成
{: #criteria_fvt}

1. 説明を入力して形式を選択します。

2. 成功と宣言するのに必要なテスト・ケースの合格パーセンテージを指定します。

3. クリティカルなテスト・ケースを定義します。

4. テスト・ケースの回帰をモニターするには、**「テスト・ケースの回帰のモニター (Monitor for test case regression)」**チェック・ボックスにチェック・マークを付けます。


5. **「保存」**をクリックします。


### unit-test ルールの作成
{: #criteria_ut}

1. 説明を入力して形式を選択します。

2. 成功と宣言するのに必要なテスト・ケースの合格パーセンテージを指定します。

3. クリティカルなテスト・ケースを定義します。

4. テスト・ケースの回帰をモニターするには、**「テスト・ケースの回帰のモニター (Monitor for test case regression)」**チェック・ボックスにチェック・マークを付けます。


5. **「保存」**をクリックします。


### code-coverage ルールの作成
{: #criteria_codecoverage}

1. 説明を入力して形式を選択します。

2. 成功と宣言するのに必要なコード・カバレッジのパーセンテージを指定します。

3. コード・カバレッジの回帰をモニターするには、**「テスト・ケースの回帰のモニター (Monitor for test case regression)」**チェック・ボックスにチェック・マークを付けます。


4. **「保存」**をクリックします。

### static-security-scan ルールの作成
{: #criteria_static}

1. 説明を入力します。


2. ルールによって許容される高、中、低の重大度の問題の最大数を指定します。
 

3. **「保存」**をクリックします。

### dynamic-security-scan ルールの作成
{: #criteria_dynamic}

1. 説明を入力します。


2. ルールによって許容される高、中、低の重大度の問題の最大数を指定します。
 

3. **「保存」**をクリックします。

## テスト結果の形式とツール

{{site.data.keyword.DRA_short}} は以下のタイプのメトリックと形式をサポートしています。

* 機能検証テスト (Mocha、xUnit)
* 単体テスト (Mocha、xUnit、Karma/Mocha)
* コード・カバレッジ (Blanket.js、JSON 要約報告書の形式の Istanbul)

{{site.data.keyword.DRA_short}} は Selenium テストと Jasmine テストもサポートしています。これらのテストは、xUnit や Mocha などの公式にサポートされているツールに組み込まなければなりません。
{{site.data.keyword.deliverypipeline}}、{{site.data.keyword.DRA_short}}、Selenium を一緒に使用することについては、[Running Selenium tests from the command line on a delivery pipeline](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/) を参照してください。


テスト・ケースがある項目の場合、クリティカル・テスト・ケースを指定できます。これは、許容パーセンテージにかかわらずパスしなければならないテストのことです。クリティカル・テスト・ケースの名前は、テスト・ケースの `full title` 属性と一致していなければなりません。
    
* Karma/Mocha テストの場合、`describe()` 説明ストリングと `it()` 説明ストリングがスペースで連結されます。

* xUnit テストの場合、パッケージ名、クラス名、関数名がスペースで連結されます。
この例を以下に示します。

  ```
  <testsuites package="test">
    <testsuite package="otc-api" name="PUT Service Instances - Test Setup" tests="2" failures="0" errors="0">
      <testcase name="#1 Authorization passed for mock user: idsb3t1@us.ibm.com"/>
      <testcase name="#2 Authorization passed for mock user: idsb3t4@us.ibm.com"/>
    </testsuite>
  </testsuite>
  ```
この例では、以下のテスト・ケース名が生成されます。
```
  test otc-api PUT Service Instances - Test Setup #1 Authorization passed for mock user: idsb3t1@us.ibm.com
  test otc-api PUT Service Instances - Test Setup #2 Authorization passed for mock user: idsb3t1@us.ibm.com
  ```

Sauce Labs ツール統合をパイプラインに追加すると、Sauce Labs を {{site.data.keyword.DRA_short}} で使用できます。
それから、`SAUCE_USERNAME` 環境変数と `SAUCE_ACCESS_KEY` 環境変数を資格情報として Selenium テストに取り込みます。

実行後に、ログ内にすべてのテストのフル・タイトルが表示されます。
  

**注:**
* {{site.data.keyword.DRA_short}} は、フル・タイトルにハイフンが含まれるクリティカル・テストをサポートしていません。    
* 組織名を変更する場合は、前の組織名と関連付けられていたポリシーを再作成しなければなりません。名前の変更前に生成された決定レポートにはアクセスできなくなります。


## 決定レポートの表示    
{: #DI_decision_reports}

パイプラインが実行された後、{{site.data.keyword.DRA_short}} はそのパイプラインでのテスト結果の収集と分析を開始して、基準を確立します。その後の実行のたびに、そのデータが収集され、前の結果と比較されます。決定ゲートでは、このデータを利用して、デプロイメントを停止する時を決定します。 

パイプラインからのゲートの決定レポートを表示するには、以下の手順を実行します。

   1. 確認するゲートを含むステージで、**「ログおよび履歴の表示 (View logs and history)」**をクリックします。

   2. そのゲートを含むジョブから、そのゲートの名前をクリックします。


   3. ログ・ビューで「`ここから {{site.data.keyword.DRA_short}} レポートを確認します (Check {{site.data.keyword.DRA_short}} report here)`」というメッセージを見つけ、リンクをクリックしてレポートを開きます。

