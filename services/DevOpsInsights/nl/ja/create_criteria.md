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

# ポリシーの定義
{: #criteria}

{{site.data.keyword.DRA_short}} を使用すると、アプリケーションのポリシーを簡単に定義できます。開始するには、以下のステップに従ってください。
{:shortdesc}

1. サイド・メニューで、**「ポリシー (Policy)」**をクリックします。

2. **「ポリシーの作成 (+) (Create Policy (+))」**をクリックしてから、新しいポリシーの名前と説明を入力します。

3. **「次へ」**をクリックします。

4. 以下のようにして、1 つ以上のルールをポリシーに追加します。
  1. **「ルールの作成 (+) (Create Rule (+))」**をクリックします。
  2. ルールのタイプを選択します。
  3. ルールの詳細情報と条件を入力します。
  4. **「保存」**をクリックします。

5. ルールをポリシーに追加し終えたら、**「完了」**をクリックします。

{{site.data.keyword.DRA_short}} の追加先の {{site.data.keyword.Bluemix_notm}} 組織内にポリシーが作成されます。同じ組織内のどのアプリケーションもこのポリシーを使用できます。

{{site.data.keyword.DRA_short}} は以下のタイプのメトリックと形式をサポートしています。

* 機能検証テスト (Mocha、JUnit)
* 単体テスト (Mocha、JUnit、Karma/Mocha)
* コード・カバレッジ (Blanket.js、JSON 要約報告書の形式の Istanbul)

{{site.data.keyword.DRA_short}} は Selenium テストと Jasmine テストもサポートしています。これらのテストは、JUnit、xUnit、 Mocha などの公式にサポートされているツールに組み込まなければなりません。{{site.data.keyword.deliverypipeline}}、{{site.data.keyword.DRA_short}}、Selenium を一緒に使用することについては、[Running Selenium tests from the command line on a delivery pipeline](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/) を参照してください。

テスト・ケースがある項目の場合、クリティカル・テスト・ケースを指定できます。これは、許容パーセンテージにかかわらずパスしなければならないテストのことです。クリティカル・テスト・ケースの名前は、以下のようなテスト・ケースの `full title` 属性と一致していなければなりません。    
* Karma/Mocha テストの場合、`describe()` 説明ストリングと `it()` 説明ストリングがスペースで連結される
* JUnit テストの場合、パッケージ名、クラス名、関数名がスペースで連結される    

Sauce Labs 統合をパイプラインに追加すると、Sauce Labs を {{site.data.keyword.DRA_short}} で使用できます。それから、`SAUCE_USERNAME` 環境変数と `SAUCE_ACCESS_KEY` 環境変数を資格情報として Selenium テストに取り込みます。

実行後に、ログ内にすべてのテストのフル・タイトルが表示されます。  

注:
* {{site.data.keyword.DRA_short}} は、フル・タイトルにハイフンが含まれるクリティカル・テストをサポートしていません。    
* 組織名を変更する場合は、前の組織名と関連付けられていたポリシーを再作成しなければなりません。名前の変更前に生成された決定報告書にはアクセスできなくなります。

## 機能検証テストのルールの作成
{: #criteria_fvt}

1. 説明を入力して形式を選択します。

2. 成功と宣言するのに必要なテスト・ケースの合格パーセンテージを指定します。

3. クリティカルなテスト・ケースを定義します。

4. テスト・ケースの回帰をモニターするには、**「テスト・ケースの回帰のモニター (Monitor for test case regression)」**チェック・ボックスを選択します。

5. **「保存」**をクリックします。


## 単体テストのルールの作成
{: #criteria_ut}

1. 説明を入力して形式を選択します。

2. 成功と宣言するのに必要なテスト・ケースの合格パーセンテージを指定します。

3. クリティカルなテスト・ケースを定義します。

4. テスト・ケースの回帰をモニターするには、**「テスト・ケースの回帰のモニター (Monitor for test case regression)」**チェック・ボックスを選択します。

5. **「保存」**をクリックします。


## コード・カバレッジのルールの作成
{: #criteria_codecoverage}

1. 説明を入力して形式を選択します。

2. 成功と宣言するのに必要なコード・カバレッジのパーセンテージを指定します。

3. コード・カバレッジの回帰をモニターするには、**「テスト・ケースの回帰のモニター (Monitor for test case regression)」**チェック・ボックスを選択します。

4. **「保存」**をクリックします。
