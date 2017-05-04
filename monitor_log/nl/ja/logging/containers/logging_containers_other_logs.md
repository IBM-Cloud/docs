---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# コンテナーからの非デフォルト・ログ・データの収集
{: #logging_containers_collect_data}

コンテナー内の非デフォルト・ログ・ロケーションからデータを取り込むには、コンテナーの作成時に環境変数 **LOG_LOCATIONS** を設定します。
{:shortdesc}

* コンテナーの作成時にログ・ファイルへのパスを指定した **LOG_LOCATIONS** 環境変数を追加します。 
* 複数のログ・ファイルをコンマで区切って追加できます。 

## Bluemix コンソールを使用した非デフォルト・ログ・データの収集
{: #logging_containers_collect_data_ui}

以下のステップを実行して、コンソールを使用して非デフォルト・データを収集します。

1. カタログから、**「コンテナー」**を選択し、イメージを選択します。 

    表示されるイメージのリストには、{{site.data.keyword.IBM}} で提供されているイメージ、およびプライベート {{site.data.keyword.Bluemix_notm}} レジストリー内に保管されているイメージが含まれています。 

2. コンテナーを定義します。タイプを選択し、コンテナーの名前を入力し、そのサイズを選択し、IP アドレス詳細やポートなどの他の属性を定義します。詳しくは、[{{site.data.keyword.Bluemix_notm}} UI を使用した単一コンテナーの作成およびデプロイ](/docs/containers/container_single_ui.html)に関する資料を参照してください。 

3. **「詳細オプション」**セクションを展開し、**「新規環境変数の追加」**を選択します。

4. **LOG_LOCATIONS** 変数を追加し、その値を、分析するログに設定します。

    例えば、最新の Liberty イメージに基づいたコンテナーを追加した場合、ログ・ファイル *dpkg.log* を分析するには、環境値を以下の値に設定します。
    
    <table>
      <tbody>
        <tr>
          <th align="center">変数名</th>
          <th align="center">値</th>
        </tr>
        <tr>
          <td align="left">LOG_LOCATIONS</td>
          <td align="left">/var/log/dpkg.log</td>
        </tr>
      </tbody>
    </table>

4. **「作成」**をクリックします。

コンテナー・ダッシュボードが開きます。コンテナーの状況が「*実行中*」であることを確認してから、**「モニターおよびログ (Monitoring and logs)」**タブでログを確認します。


## CLI を使用した非デフォルト・ログ・データの収集
{: #logging_containers_collect_data_cli}

以下のステップを実行して、CLI を使用して非デフォルト・ログ・データを収集します。

1. {{site.data.keyword.containershort}} CLI を使用するように端末をセットアップします。詳しくは、[IBM Bluemix Container Service CLI のセットアップ](/docs/containers/container_cli_cfic_install.html)に関する資料を参照してください。

2. コマンド `cf login` を使用して、Cloud Foundry CLI にログインします。プロンプトに応じて、{{site.data.keyword.Bluemix_notm}} ID、パスワード、組織、およびスペースを入力します。 

    デフォルトでは、米国南部地域または最後にログインした地域にログインします。 
    
    {{site.data.keyword.Bluemix_notm}} の特定の地域にログインするために、**–a** オプションを含めることができます。例えば、以下の表では、地域ごとのコマンドをリストします。

    <table>
      <tbody>
        <tr>
          <th align="center">地域</th>
          <th align="center">コマンド</th>
        </tr>
        <tr>
          <td align="left">米国南部</td>
          <td align="left"> cf login -a api.ng.bluemix.net</td>
        </tr>
        <tr>
          <td align="left">英国</td>
          <td align="left">cf login -a api.eu-gb.bluemix.net</td>
        </tr>
        <tr>
          <td align="left">シドニー</td>
          <td align="left">cf login -a api.au-syd.bluemix.net</td>
        </tr>
      </tbody>
    </table>
    

3. コマンド `cf ic login` を使用して、{{site.data.keyword.containershort}} にログインします。

4. イメージから単一コンテナーを作成します。LOG_LOCATIONS 環境変数を組み込み、非デフォルト・ログ・ロケーションを含めます。  

    そのログ情報を Kibana で表示できるようにカスタム・ロケーションを追加するために、コンテナーの作成時に **LOG_LOCATIONS** 環境変数を追加します。次のコマンドを入力します。

    
    `docker run -p portNumber -e "LOG_LOCATIONS=log1,log2" --name containerName registry.domain_name/imageName:imageTag`
    
    各部分の説明:
    
     <table>
      <tbody>
        <tr>
          <th align="center">オプション</th>
          <th align="center">説明</th>
        </tr>
        <tr>
          <td align="left">-p</td>
          <td align="left"> アプリをインターネットからアクセス可能にするには、パブリック・ポートを公開する必要があります。使用するイメージの Dockerfile 内に指定されているポートがあれば、それらのポートを含めます。<br> 使用する IP プロトコルとして UDP か TCP のいずれかを選択できます。プロトコルを指定しない場合、自動的にポートは TCP トラフィックに対して公開されます。<br> パブリック・ポートを公開するときには、公開したポートでのみパブリック・データの送受信を許可するパブリック・ネットワーク・セキュリティー・グループをコンテナー用に作成します。その他のすべてのパブリック・ポートは閉じられるため、それらのポートを使用してインターネットからアプリにアクセスすることはできません。<br> 複数の -p オプションを使用して、複数のポートを含めることができます。</td>
        </tr>
        <tr>
          <td align="left">-e</td>
          <td align="left">環境変数を設定します。<br> 複数のキーを別個にリストできます。環境変数名と値の両方を引用符で囲みます。<br> コンテナー内でモニターされるログ・ファイルを追加するには、そのログ・ファイルへのパスを指定して LOG_LOCATIONS 環境変数を設定します。</td>
        </tr>
        <tr>
          <td align="left">--name</td>
          <td align="left">コンテナーの名前を定義します。</td>
        </tr>
	<tr>
          <td align="left">registry.domain_name</td>
          <td align="left">パブリック地域内のレジストリー。例えば、米国南部地域の場合、デフォルト・ドメイン名は `ng.bluemix.net` です。英国の場合、デフォルト・ドメイン名は、`eu-gb.bluemix.net` です。</td>
        </tr>
        <tr>
          <td align="left">imageName</td>
          <td align="left">追加するイメージの名前。</td>
        </tr>
	<tr>
          <td align="left">imageTag</td>
          <td align="left">追加するイメージのタグ。</td>
        </tr>
      </tbody>
    </table>
    
    例えば、最新の Liberty イメージに基づいてコンテナーを作成し、ログ・ファイル `/var/log/dpkg.log` を含めるには、以下のコマンドを使用します。 
    
    `docker run -p 9080 -e "LOG_LOCATIONS=/var/log/dpkg.log" --name MyContainer registry.ng.bluemix.net/ibmliberty:latest`
    
    dpkg.log ファイルは、標準 Ubuntu ログ・ファイルであり、一般的にコンテナーの作成時に生成されますが、Kibana に自動的にプッシュされることはありません。

コンテナーの状況を確認するには、コマンド `docker ps` を実行します。状況が「*実行中*」の場合、{{site.data.keyword.Bluemix_notm}} コンソール、コマンド・ライン、または Kibana を使用してログを確認します。



