---

copyright:
  years: 2017
lastupdated: "2017-02-28"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# {{site.data.keyword.mqa}} の開始 (非推奨)
{: #gettingstartedtemplate}

**{{site.data.keyword.mqafull}} サービスは非推奨です。** 状況と日付について詳しくは、[Retirement of Bluemix Mobile Quality Assurance blog entry ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/?p=72728){: new_window}を参照してください。
{:deprecated}

{{site.data.keyword.mqafull}} は、チームが、テスターおよびライブ・ユーザーのエクスペリエンスを取り込んで、高品質のモバイル・アプリを継続的にビルドおよび提供できるようにします。
{: shortdesc}

{{site.data.keyword.mqa}} サービスを素早く稼働させるには、以下のステップに従ってください。

1. {{site.data.keyword.mqa}} サービスのインスタンスを作成<!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->した後、{{site.data.keyword.Bluemix}} ダッシュボードの**「サービス」**セクション内のタイルをクリックして、{{site.data.keyword.mqa}} コンソールにアクセスできます。

	{{site.data.keyword.mqa}} サービスが起動します。

2. **「MQA アプリの追加 (Add MQA App)」**を選択し、アプリの名前を指定して、モバイル・アプリを {{site.data.keyword.mqa}} インスタンスに追加します。

3. {{site.data.keyword.mqa}} [Client SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/support/docview.wss?uid=swg27044490){: new_window}をダウンロードし、続いて以下のいずれかの手順を実行して、アプリの装備を完了します。

	* [Android アプリでの MQA の装備](mqa_inst_app_android.html)
	* [iOS アプリでの MQA の装備](mqa_inst_app_ios.html)
	* [Cordova アプリでの MQA の装備](mqa_inst_app_cord.html)

	単一の SDK を使用して、実動前アプリと実動アプリの両方を装備します。`MODE:` パラメーターを使用して、実動前モードには *QA* を、実動モードには *MARKET* を指定できます。内部のテスターがアプリで発生したバグと異常終了に関する詳細情報を提供できるようにするには、実動前モードを指定します。ユーザーがアプリに関する詳細情報を提供できるようにするには、実動モードを指定します。アプリが実動である場合、{{site.data.keyword.mqa}} によって、アプリ内部でのユーザー権限からのフィードバックの取得が容易になります。

4. アプリを装備した後、{{site.data.keyword.mqa}} サービス・インスタンスのインターフェースで以下のいずれかのオプションを選択して、そのアプリの詳細な品質情報を表示できます。

	<dl>
		<dt><strong>「セッション」</strong></dt>
		<dd>異常終了、バグ、フィードバック、およびセッション中のデバイスの状態に関する情報を検討します。詳しくは、IBM Knowledge Center の [Viewing session details ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ViewingSessionDetails.html){: new_window}を参照してください。</dd>
		<dt>![](/images/cap_crashicon.jpg) <strong>「異常終了」</strong></dt>
		<dd>異常終了の原因となった事象に関する情報を検討します。詳しくは、IBM Knowledge Center の [Crash reports ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_CrashReports.html){: new_window}を参照してください。</dd>
		<dt>![](/images/cap_bugicon.jpg) <strong>「バグ」</strong></dt>
		<dd>バグ・レポート、画面キャプチャー、およびデバイスの詳細情報など、ユーザーによって報告された情報を検討します。詳しくは、IBM Knowledge Center の [Bug reports ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_BugReports.html){: new_window}を参照してください。</dd>
		<dt>![](/images/cap_feedbackicon.jpg) <strong>「フィードバック」</strong></dt>
		<dd>フィードバックを誰がいつ書き込んだかを知るためにユーザー・フィードバック応答を検討します。詳しくは、IBM Knowledge Center の [User feedback ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_UserFeedback.html){: new_window}を参照してください。</dd>
		<dt><strong>「評判スコア (Sentiment score)」(構成されている場合)</strong></dt>
		<dd>アプリの品質のモニター、測定、および向上のために、時間の経過に伴うユーザー評判のスコアとバージョンを検討します。詳しくは、IBM Knowledge Center の [User sentiment ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/UserSentiment.html){: new_window}を参照してください。</dd>
		<dt><strong>「登録済みデバイス」</strong></dt>
		<dd>テスト・セッション中に使用されたデバイスのリストと、これらのデバイスに関する情報を検討します。詳しくは、IBM Knowledge Center の [Viewing device information ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ManagingDevices.html){: new_window}を参照してください。</dd>
	</dl>

	これらのメトリックには以下のデータが含まれます。

	* 異常終了、バグ、フィードバック、およびセッションに関する実動前データ
	* 異常終了、フィードバック、評判、およびセッションに関する実動データ

	![アプリの品質メトリックを表示できるインターフェースの画面キャプチャー](images/quality_metrics_saas4.gif)

	アプリに関するこの情報を表示することにより、特定の問題についてさらに調査するかどうかを判断できます。例えば、アプリの異常終了率が急上昇した場合、異常終了率をクリックすると、そのアプリの異常終了レポートに関するより詳細な情報を表示できます。

5. アプリの評判スコア全体を表示するには、以下のように評判分析を構成する必要があります。

	1. *「評判スコア (Sentiment Score)」*セクションで、選択したアプリの評判分析の構成のリンクをクリックします。

	2. 「アプリケーションの詳細 (Application Details)」 ページで、[評判分析の構成![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/tEnablingUserSentiment.html){: new_window}を行い、変更を保存します。


# 関連リンク
{: #rellinks notoc}

## チュートリアルおよびサンプル
{: #samples notoc}

* [ビデオ: Getting Started with Mobile Quality Assurance in Bluemix ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.youtube.com/watch?v=zHRfGatcKPM){: new_window}  
* [ビデオ: Sentiment Analysis in Mobile Quality Assurance ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.youtube.com/watch?v=uhkqb8BIn6k){: new_window}
* [developerWorks: Add IBM Mobile Quality Assurance to your mobile quality regimen ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/developerworks/library/mo-mqa/index.html){: new_window}
* [developerWorks: Build mobile apps that work: Five tips from an expert panel ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/developerworks/library/mo-mqa-tips/index.html){: new_window}
* [developerWorks: Build a mobile app that isn't perfect ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/developerworks/library/mo-build-imperfect-mobile-app/){: new_window}
* [developerWorks: DevOps for mobile apps challenges and best practices ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/developerworks/library/mo-bestdevops-mobileapps/index.html){: new_window}
* [サンプル: bluelist-mqa ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://hub.jazz.net/project/mobilecloud/bluelist-mqa/overview){: new_window}
