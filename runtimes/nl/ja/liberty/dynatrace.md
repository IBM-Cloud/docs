---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dynatrace の使用
{: #using_dynatrace}

*最終更新日: 2016 年 4 月 8 日*

Dynatrace は、アプリケーションのモニタリングを提供するサード・パーティー・サービスです。

Dynatrace サービスで提供される内容について詳しくは、[『Dynatrace Application Monitoring』](http://www.dynatrace.com/en/products/application-monitoring.html)を参照してください。

Dynatrace サービスを Liberty アプリケーションで使用できるようにする場合は、以下の処理手順に従ってください。

1. Liberty ビルドパックでダウンロードできるように、Dynatrace エージェント jar ファイルを獲得し、ホストします。
2. Liberty アプリケーションで稼働している Dynatrace エージェントが通信できるように、Dynatrace サーバーのインスタンスをセットアップします。
3. Dynatrace エージェントをダウンロードして Dynatrace サーバーに接続できるように、Liberty アプリケーションを構成します。

## Dynatrace エージェントのホスティング
{: #hosting_dynatrace_agent}
Dynatrace エージェントは Web サーバー上でホストされる必要があり、Liberty ビルドパックはそのサーバーからエージェント jar をダウンロード可能でなければなりません。サーバーは、エージェント jar に関する詳細を指定する index.yml ファイルを使用して構成する必要があります。Dynatrace エージェントをセットアップするには、以下の手順に従ってください。
  1. Dynatrace エージェント jar をダウンロードします。Dynatrace エージェント jar のダウンロード手順については、Dynatrace コミュニティー Web サイトの[『Dynatrace Server Platform Installers』](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace)を参照してください。Bluemix で実行するための適切なエージェント jar ファイルは、**dynatrace-agent-unix.jar** バージョン **6.3.0+** です。
  2. Liberty ビルドパックによるダウンロードが可能なロケーションでエージェント jar ファイルをホストします。このファイルは、使用可能ないずれかのサーバー機能を使用して Bluemix 自体の上でホストするか、パブリックに使用可能なロケーションでホストすることができます。
     * ホストするロケーションには必ず index.yml ファイルを配置します。index.yml ファイルには、後にコロンの付いたエージェント jar のバージョン ID とそのエージェント jar のロケーションの完全な URL からなる項目が含まれていなければなりません。例えば、次のように指定します。
```
      ---
      6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
```
{: #codeblock}
     * URL 末尾の jar ファイルの名前は **dynatrace-agent-version-unix.jar** でなければなりません。バージョンは **6.3.0** または **6.3.0_nnnn** でなければなりません。nnnn はミクロ・バージョン ID です。これは、Dynatrace で使用される jar ファイル名とは異なる場合があるため、jar の名前変更が必要になることがあります。       
     * **dynatrace-agent-6.3.0-unix.jar** ファイルは、index.yml ファイルで指定されたロケーションで使用可能でなければなりません。jar ファイルと index.yml の両方のロケーションを同じディレクトリーにすることができます。

## Dynatrace コレクターのセットアップ

次に、Dynatrace エージェントにアクセス可能な Dynatrace コレクターをセットアップする必要があります。Dynatrace エージェントが Dynatrace コレクターに接続するための情報を渡すユーザー提供サービスを作成することも必要です。Dynatrace コンポーネントの関係について詳しくは、[『Dynatrace Architecture』](https://community.dynatrace.com/community/display/DOCDT63/Architecture)を参照してください。

  1. Dynatrace コレクターをセットアップします。
    * Dynatrace コレクターのダウンロード手順およびセットアップ手順については、[Dynatrace コミュニティー Web サイト](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace)を参照してください。
    * コレクターは、Bluemix 内のアプリケーションで実行されている Dynatrace エージェントにアクセス可能なロケーションでセットアップする必要があります。
  2. 実行中の Dynatrace コレクターを指すユーザー提供サービスを作成します。<b>注</b> ユーザー提供のサービスの名前には <b>dynatrace</b> が含まれている必要があります。例えば、次のコマンドを使用します。```
    $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'```
{: #codeblock}
この例では、my-dynatrace-collector はサービスに付けられた名前、DynatraceCollectorIPaddress は構成済み Dynatrace コレクターの IP アドレス、profile はこのモニター対象アプリケーションに関連付けられたオプションの Dynatrace プロファイル名です。デフォルト・プロファイル値は Monitoring です。オプション・パラメーターは次の例のように指定できます。
```
    $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                                          "options" : {
                                                       "dynatrace-parameter-1": "value",
                                                       "dynatrace-parameter-2": "value"
                                         }}'
```
{: #codeblock}
使用可能なオプションについて詳しくは、Dynatrace コミュニティー Web サイトの[『Agent Configuration』の『Agent Setting』セクション](https://community.dynatrace.com/community/display/DOCDT62/Agent+Configuration)を参照してください。例えば、exclude オプションを使用すると、Dynatrace のモニター対象からクラスを除外できます。ユーザー提供サービスの構成について詳しくは、[『DynaTrace Agent Framework』](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md)を参照してください。

  3. アプリケーションを Bluemix にプッシュ後、作成したユーザー提供サービスをアプリケーションにバインドします。例えば、次のコマンドを使用します。```
    $ cf bs myApp my-dynatrace-service```
**注**: サービスのバインド後にアプリケーションを再ステージングする必要があります。


## Liberty アプリケーションの構成
{: #configuring_liberty_app}

モニター対象の Liberty アプリケーションは、以前にセットアップしたエージェント jar をホストするサーバーを検出するように構成する必要があります。**JBP_CONFIG_DYNATRACEAGENT** 環境変数を使用してアプリケーションを構成できます。**JBP_CONFIG_DYNATRACEAGENT** 環境変数は、Dynatrace エージェントのダウンロード元となるビルドパックを指示します。この環境変数を設定するには、以下の手順に従ってください。
<ol>
   <li> 値が *"repository_root: URL_of_server_hosting_index.yml"* になるように変数 **JBP_CONFIG_DYNATRACEAGENT** を設定します。例えば、アプリケーションのプッシュ後に次のコマンドを発行します。
```
    $ cf se myApp JBP_CONFIG_DYNATRACEAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'```
{: #codeblock}
この例では、*my-dynatrace-agent-host.mybluemix.net* は、以前に構成したサーバーでホストされる index.yml ファイルの URL です。
  </li>
  <li> 環境変数の設定後、アプリケーションを再ステージングします。Liberty アプリケーションの staging_task.log には、エージェント・ホスティング・サーバーからの Dynatrace エージェントの正常なダウンロードを示すメッセージが出されます。例えば、次のように指定します。
```
    Downloading dynatrace-agent-6.3.0-unix.jar 6.3.0 from https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)```
{: #codeblock}
</li>
<li>staging_task.log を見るには、次のコマンドを実行します。
```
    $ cf files myAppName logs/staging_task.log```
{: #codeblock}
</li>
</ol>

# 関連リンク
## 一般
* [Liberty ランタイム](index.html)
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
