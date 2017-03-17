---

copyright:
  years: 2012, 2017
  
lastupdated: "2017-01-25"  

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# {{site.data.keyword.mqa}} のトラブルシューティング 
{: #tsmqa}
ここでは、{{site.data.keyword.mqa}} の使用に関するよくある質問と回答をいくつか紹介します。
{:shortdesc}

## JavaScript ハイブリッドのビルドが失敗する
{: #ts_js_build_fail}

IBM MobileFirst Platform Foundation コンポーネント用の JavaScript&tm; ハイブリッド SDK がアプリケーション内に存在し、必要なコードが追加されていても、JavaScript ハイブリッド {{site.data.keyword.mqa}} アプリケーションのビルドが失敗します。


{{site.data.keyword.mqa}} アプリケーションのビルドの実行を試みると、ビルドは失敗します。
{: tsSymptoms notoc} 


1. Android および iOS のプラットフォーム固有のハイブリッド SDK コンポーネントはプロジェクトにインストールされていません。
2. Android および iOS のプラットフォーム固有のハイブリッド SDK コンポーネント (インストール済み) が、JavaScript SDK コンポーネント (インストール済み) と互換性がありません。
3. ネイティブの Android SDK か、ネイティブの iOS SDK か、またはその両方がインストール済みですが、Android および iOS のプラットフォーム固有のハイブリッド SDK コンポーネントはインストールされていません。
{: tsCauses notoc} 
 

この問題を解決するには、以下のステップを実行することをお勧めします。
{: tsResolve notoc}
  1.  必須であるすべての Android および iOS のプラットフォーム固有のハイブリッド SDK
コンポーネントと、ご使用のアプリがサポートするプラットフォームのそれぞれに必要なネイティブの Android SDK またはネイティブの iOS SDK が、インストール済みであることを確認してください。 
  2. Android および iOS のプラットフォーム固有のハイブリッド SDK コンポーネントのメジャー・バージョン番号が、JavaScript コンポーネントのメジャー・バージョン番号と同じかそれ以上 (次のメジャー・バージョンまで) であることを確認してください。次の表に例を示します。
  
| JavaScript コンポーネントのバージョン | プラットフォーム固有のコンポーネントのバージョン | 互換性はあるか? |
|---------: |------------: |------------: |
| 1.2.3 | 1.2.3 | はい |
| 1.2.3 | 1.2.1 | いいえ |
| 1.2.3 | 1.3.2 | はい |
| 1.2.3 | 2.0.0 | いいえ |

  3. Android および iOS のプラットフォーム固有のハイブリッド SDK コンポーネントがインストール済みであることを確認してください。ご使用のアプリがネイティブの Android SDK およびネイティブの iOS SDK のプラットフォーム上で実行されている場合はそれらの SDK が必要ですし、ハイブリッド・アプリケーションに各プラットフォーム用の Android および iOS のプラットフォーム固有のハイブリッド SDK コンポーネントがインストールされている必要もあります。

  
## 評判分析を開けず、テスト・アプリも配布できない
{: #ts_sent_fail}

評判分析を開けず、テスト・アプリも分散できません。

ご使用のブラウザーがポップアップ・ウィンドウをブロックしているため、評判分析を開けず、テスト・アプリを配布することもできません。
{: tsSymptoms notoc} 

Mobile Quality Assurance は、ポップアップ・ウィンドウと Cookie を使用して Mobile Quality Assurance サーバーと通信します。
{: tsCauses notoc}


Mobile Quality Assurance と Mobile Quality Assurance サーバー間の通信を確立するには、ポップアップ・ウィンドウと Cookie を許可するようにブラウザーの設定を構成する必要がある場合があります。例えば、ユーザー・インターフェースで「評判スコア (Sentiment Score)」などのオプションをクリックしたときに、Mobile Quality Assurance がサーバーと通信できない可能性があります。評判分析は、ポップアップ・ウィンドウと Cookie がブロックされていると表示できません。ブラウザーの設定の構成方法について詳しくは、ご使用のブラウザーの資料を参照してください。
{: tsResolve notoc}


## 有効期限が切れたアプリケーションを実行できない
{: #ts_app_expired}

Mobile Quality Assurance アプリケーションを実行できません。

Mobile Quality Assurance アプリケーションを実行しようとすると、メッセージ「アプリケーションは失効しているため、現時点では実行できません (Your application has expired and cannot be run at this time)」が表示されます。
{: tsSymptoms notoc} 

アプリケーションには、Mobile Quality Assurance の「ビルド (Builds)」ページで使用不可のマークが付けられています。
{: tsCauses notoc}


Mobile Quality Assurance の「ビルド (Builds)」ページで、使用不可のマークが付けられているアプリケーションがないことを確認します。通常、アプリケーションは、ビルドの特定のバージョンを使用しないようそのアプリケーション自体からテスターに通知するために、使用不可とマークが付けられています。Mobile Quality Assurance の「ビルド (Builds)」ページの設定について詳しくは、IBM Knowledge Center の「Managing builds」を参照してください。
{: tsResolve notoc}

