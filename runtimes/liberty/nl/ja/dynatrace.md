---

copyright:
  years: 2016
lastupdated: "2016-06-10"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dynatrace の使用
{: #using_dynatrace}

Dynatrace は、アプリケーションのモニタリングを提供するサード・パーティー・サービスです。

Dynatrace サービスで提供される内容について詳しくは、[『Dynatrace Application Monitoring』](http://www.dynatrace.com/en/products/application-monitoring.html)を参照してください。

Liberty アプリケーションが Dynatrace を使用するように構成されている場合、デフォルトの動作では、Liberty ランタイムは Dynatrace サイトから Dynatrace エージェント jar ファイルを取得し、その Dynatrace エージェントをアプリケーションで実行します。このデフォルトの動作では、Dynatrace を使用するために必要な最小構成は、Dynatrace コレクターを指すユーザー提供のサービスを作成することです。

## Dynatrace コレクターを指すユーザー提供のサービスの作成

まず、Dynatrace コレクターをセットアップする必要があります。次に、Dynatrace エージェントが Dynatrace コレクターと接続するための情報を渡す、ユーザー提供のサービスを作成する必要があります。Dynatrace コンポーネントの関係について詳しくは、[『Dynatrace Architecture』](https://community.dynatrace.com/community/display/DOCDT63/Architecture)を参照してください。

<ol>
<li>Dynatrace コレクターをセットアップします。<ul>
  <li>Dynatrace コレクターのダウンロード手順およびセットアップ手順については、[Dynatrace コミュニティー Web サイト](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace)を参照してください。</li>
  <li>コレクターは、Bluemix 内のアプリケーションで実行されている Dynatrace エージェントにアクセス可能なロケーションでセットアップする必要があります。
  </li>
  </ul>
</li>
<li>実行中の Dynatrace コレクターを指すユーザー提供サービスを作成します。<b>注</b> ユーザー提供のサービスの名前には <b>dynatrace</b> が含まれている必要があります。例えば、次のコマンドを使用します。<pre>
  $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
  </pre>
  {: codeblock}

この例では、my-dynatrace-collector はサービスに付けられた名前、DynatraceCollectorIPaddress は構成済み Dynatrace コレクターの IP アドレス、profile はこのモニター対象アプリケーションに関連付けられたオプションの Dynatrace プロファイル名です。デフォルト・プロファイル値は Monitoring です。オプション・パラメーターは次の例のように指定できます。


  <pre>
  $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                                        "options" : {"dynatrace-parameter-1": "value",
                                                     "dynatrace-parameter-2": "value"}}'
  </pre>
  {: codeblock}

使用可能なオプションについて詳しくは、Dynatrace コミュニティー Web サイトの[『Agent Configuration』の『Agent Setting』セクション](https://community.dynatrace.com/community/display/DOCDT62/Agent+Configuration)を参照してください。例えば、exclude オプションを使用すると、Dynatrace のモニター対象からクラスを除外できます。ユーザー提供サービスの構成について詳しくは、[『DynaTrace Agent Framework』](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md)を参照してください。

</li>
<li>アプリケーションを Bluemix にプッシュ後、作成したユーザー提供サービスをアプリケーションにバインドします。例えば、次のコマンドを使用します。<pre>
  $ cf bs myApp my-dynatrace-collector
  </pre>  
  {: codeblock}

**注**: サービスのバインド後にアプリケーションを再ステージングする必要があります。

</li>
</ol>

## オプション構成
{: #optional_configuration}

ユーザー自身が Dynatrace エージェント jar ファイルを取得し、ホストすることも可能です。その場合は、以下の追加の構成ステップが必要です。
1. Liberty ビルドパックでダウンロードできるように、Dynatrace エージェント jar ファイルを獲得し、ホストします。
2. Dynatrace エージェントをダウンロードできるように、Liberty アプリケーションを構成します。

### Dynatrace エージェントのホスティング
{: #hosting_dynatrace_agent}
Dynatrace エージェントは Web サーバー上でホストされる必要があり、Liberty ビルドパックはそのサーバーからエージェント jar をダウンロード可能でなければなりません。サーバーは、エージェント jar に関する詳細を指定する index.yml ファイルを使用して構成する必要があります。Dynatrace エージェントをセットアップするには、以下の手順に従ってください。
  1. Dynatrace エージェント jar をダウンロードします。Dynatrace エージェント jar のダウンロード手順については、Dynatrace コミュニティー Web サイトの[『Dynatrace Server Platform Installers』](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace)を参照してください。Bluemix 上で実行するための適切なエージェント jar ファイルは、**dynatrace-agent-unix.jar** バージョン **6.+** です。
  2. Liberty ビルドパックによるダウンロードが可能なロケーションでエージェント jar ファイルをホストします。このファイルは、使用可能ないずれかのサーバー機能を使用して Bluemix 自体の上でホストするか、パブリックに使用可能なロケーションでホストすることができます。
     * ホストするロケーションには必ず index.yml ファイルを配置します。index.yml ファイルには、後にコロンの付いたエージェント jar のバージョン ID とそのエージェント jar のロケーションの完全な URL からなる項目が含まれていなければなりません。例えば、次のように指定します。
```
      ---
      6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
```  
{: codeblock}
     * **dynatrace-agent-6.3.0-unix.jar** ファイルは、index.yml ファイルで指定されたロケーションで使用可能でなければなりません。jar ファイルと index.yml の両方のロケーションを同じディレクトリーにすることができます。

### Liberty アプリケーションの構成
{: #configuring_liberty_app}

モニター対象の Liberty アプリケーションは、以前にセットアップしたエージェント jar をホストするサーバーを検出するように構成する必要があります。**JBP_CONFIG_DYNATRACEAPPMONAGENT** 環境変数を使用してアプリケーションを構成できます。**JBP_CONFIG_DYNATRACEAPPMONAGENT** 環境変数は、Dynatrace エージェントのダウンロード元となるビルドパックを指示します。この環境変数を設定するには、以下の手順に従ってください。
<ol>
   <li> 値が *"repository_root: URL_of_server_hosting_index.yml"* になるように変数 **JBP_CONFIG_DYNATRACEAPPMONAGENT** を設定します。例えば、アプリケーションのプッシュ後に次のコマンドを発行します。
  
  <pre>   
    $ cf se myApp JBP_CONFIG_DYNATRACEAPPMONAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
  </pre>
  {: codeblock}

  この例では、*my-dynatrace-agent-host.mybluemix.net* は、以前に構成したサーバーでホストされる index.yml ファイルの URL です。
  </li>
  <li> 環境変数の設定後、アプリケーションを再ステージングします。Liberty アプリケーションの staging_task.log には、エージェント・ホスティング・サーバーからの Dynatrace エージェントの正常なダウンロードを示すメッセージが出されます。例えば、次のように指定します。
<pre>
    Downloading dynatrace-agent-6.3.0-unix.jar 6.3.0 from https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)
  </pre>
  {: codeblock}

</li>
<li>staging_task.log を見るには、次のコマンドを実行します。
<pre>
    $ cf files myAppName logs/staging_task.log
  </pre>  
  {: codeblock}

</li>
</ol>

# 関連リンク
{: #rellinks}
## 一般
{: #general}
* [Liberty ランタイム](index.html)
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
