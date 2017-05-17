---



copyright:

  years: 2015, 2017
lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} CLI 入門
{: #getting-started}

{{site.data.keyword.Bluemix_notm}} CLI は、コマンド・ライン・インターフェースを使用してアプリケーション、コンテナー、インフラストラクチャー、およびその他のサービスと対話するための一元化された手法を提供します。 

**制約事項:** {{site.data.keyword.Bluemix_notm}} CLI は Cygwin ではサポートされないため、Cygwin コマンド・ライン・ウィンドウでは {{site.data.keyword.Bluemix_notm}} CLI を使用しないでください。

**注:** CLI および {{site.data.keyword.Bluemix_notm}} が稼働しているホストとの間に HTTP プロキシー・サーバーがあるネットワークを使用している場合、HTTP_PROXY 環境変数にプロキシー・サーバーのホスト名または IP アドレスを指定する必要があります。

**注:** {{site.data.keyword.Bluemix_notm}} CLI ツールでは、Cloud Foundry コマンド・ライン・インターフェースはインストール済み環境にバンドルされていました。ただし、独自の cf cli インストール済み環境がある場合、{{site.data.keyword.Bluemix_notm}} CLI コマンド `bx xxx` と Cloud Foundry CLI コマンド `cf xxx` を併用することは許可されていません。cf cli を使用して Cloud Foundry リソースを管理する場合は、代わりに `bluemix cf` を使用してください。バックエンドでは、バンドルされた Cloud Foundry CLI のコマンドは、{{site.data.keyword.Bluemix_notm}} CLI との共有コンテキストで実行されます。さらに、`bluemix cf api/login/logout/target` は許可されていません。代わりに `bluemix api/login/logout/target` を使用してください。

## {{site.data.keyword.Bluemix_notm}} CLI のインストール
{: #install_bluemix_cli}


Mac OS および Windows の場合は、[{{site.data.keyword.Bluemix_notm}} CLI パッケージ](/docs/cli/index.html#downloads)をダウンロードし、インストーラーを実行してください。

Linux の場合は、以下のステップを実行してください。

  1. パッケージをダウンロードし、解凍します。例えば次のようにします。

  ```
  ~$ tar -xvf Bluemix_CLI.tar.gz
  Bluemix_CLI/
  Bluemix_CLI/update_global_config
  Bluemix_CLI/install_bluemix_cli
  Bluemix_CLI/bx/
  Bluemix_CLI/bx/bash_autocomplete
  Bluemix_CLI/bx/zsh_autocomplete
  Bluemix_CLI/bin/
  Bluemix_CLI/bin/bluemix
  ~$
  ```

  2. `Bluemix_CLI` ディレクトリーに移動し、root 権限で `./install_bluemix_cli` コマンドを実行します。このコマンドを root ユーザーで実行するか、または、`sudo` コマンドを使用して root 権限を取得してください。例えば次のようにします。

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

これで、{{site.data.keyword.Bluemix_notm}} CLI の使用を開始することも、追加プラグインをインストールすることもできます。

## プラグインのインストール
{: #install_plug-in}

{{site.data.keyword.Bluemix_notm}} CLI では、組み込みコマンド以外のコマンドを統合するために、プラグイン拡張フレームワークがサポートされています。


ローカルまたはリモート・サーバーで、リポジトリーからプラグインをインストールすることができます。{{site.data.keyword.Bluemix_notm}} には、{{site.data.keyword.Bluemix_notm}} CLI プラグインおよび Cloud Foundry CLI プラグインをホストする以下のリポジトリーがあります。

   * {{site.data.keyword.Bluemix_notm}} CLI プラグインをホストする [{{site.data.keyword.Bluemix_notm}} CLI プラグイン・リポジトリー ](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)

リポジトリーからインストールするには、以下のステップを実行します。

  1. リポジトリー内でプラグインを見つけます。{{site.data.keyword.Bluemix_notm}} CLI をインストールした後、デフォルトでオフィシャル・リポジトリー `Bluemix` が追加されます。`bluemix plugin repo-plugins` コマンドを使用して、`Bluemix` リポジトリー内のプラグインをリストできます。例えば次のようにします。

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. `bluemix plugin install` コマンドを使用して、`Bluemix` リポジトリーからプラグインをインストールします。例えば次のようにします。

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```


ローカル環境からプラグインをインストールするには、以下のステップを実行します。

  1. プラグインをダウンロードします。例えば次のようにします。

  ```
  ~$ wget http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2--2016-02-18 14:02:12-- http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2
  Resolving public.dhe.ibm.com... 9.17.248.112
  Connection to public.dhe.ibm.com|9.17.248.112|:80... connected.
  HTTP request sent, awaiting response... 200 OK
  Length: 9857792 (9.4M) [text/plain]
  Saving to: 'auto-scaling-darwin-amd64-0.2.2'

  auto-scaling-darwin-0.2.2 100%[===================>] 9.40M 518KB/s in 22s

  2016-02-18 14:02:34 (443 KB/s) - `auto-scaling-darwin-amd64-0.2.2' saved [9857792/9857792]
  ```

  2. UNIX 系システムの場合、`chmod` コマンドを使用することによって、ダウンロードされたファイルを実行可能にする必要があります。例えば次のようにします。

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. `bluemix plugin install` コマンドを使用してプラグインをインストールします。例えば次のようにします。

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

リモート・サーバーからインストールするには、以下のステップを実行します。

  1. `bluemix plugin install` コマンドを使用することによって、リモート URL から直接プラグインをインストールします。例えば次のようにします。

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```


これで、{{site.data.keyword.Bluemix_notm}} コマンド・ラインを使用する準備ができました。コマンドと説明のリストを確認するには、`bluemix help` を実行します。 
