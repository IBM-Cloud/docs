---



copyright:

  years: 2015, 2017

lastupdated: "2017-01-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# IBM Containers CLI
{: #containercli}

*バージョン:* 1.0.0

IBM Containers CLI は、Bluemix でコンテナーおよびコンテナー・グループを管理するための {{site.data.keyword.Bluemix_notm}} CLI プラグインです。
{: shortdesc}

**注:** *前提条件*には、コマンドを使用する前に必要なアクションがリストされています。前提条件となるアクションのないコマンドでは、**なし**とリストされています。それ以外の場合、前提条件には以下のアクションのうちの 1 つ以上が含まれます。
<dl>
<dt>エンドポイント</dt>
<dd>このコマンドを使用する前に、<code>bluemix api</code> を介して API エンドポイントを設定する必要があります。</dd>
<dt>ログイン</dt>
<dd>このコマンドを使用する前に、<code>bluemix login</code> コマンドを使用してログインする必要があります。フェデレーテッド ID でログインする場合は、「--sso」オプションを使用し、ワンタイム・パスコードを使って認証します。</dd>
<dt>ターゲット</dt>
<dd>このコマンドを使用する前に、<code>bluemix target</code> コマンドを使用して組織およびスペースを設定する必要があります。</dd>
<dt>Docker</dt>
<dd>IBM Containers CLI プラグインでコマンドを実行するには、Docker CLI (docker) が必要です。</dd>
</dl>

<table summary="Bluemix 上のコンテナーの管理に使用することができる bluemix コマンド。">
 <caption>表 1. Bluemix 上のコンテナーを管理するためのコマンド</caption>
 <thead>
 <th colspan="5">Bluemix 上のコンテナーを管理するためのコマンド</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix ic attach](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_build)</td>
 <td>[bluemix ic cp](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cp)</td>
 <td>[bluemix ic cpi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cpi)</td>
 <td>[bluemix ic exec](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_exec)</td>
 </tr>
 <tr>
 <td>[bluemix ic group-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_create)</td>
 <td>[bluemix ic group-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_instances)</td>
 <td>[bluemix ic group-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic group-update](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_update)</td>
 </tr>
 <tr>
  <td>[bluemix ic groups](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_groups)</td>
  <td>[bluemix ic info](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_info)</td>
  <td>[bluemix ic init](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_init)</td>
  <td>[bluemix ic images](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_images)</td>
  <td>[bluemix ic inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_inspect)</td>
 </tr>
 <tr>
 <td>[bluemix ic ip-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_bind)</td>
 <td>[bluemix ic ip-release](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-request](/docs/cli/reference/bluemix_cli/index.html#ip_request)</td>
 <td>[bluemix ic ip-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_unbind)</td>
 <td>[bluemix ic ips](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ips)</td>
 </tr>
 <tr>
 <td>[bluemix ic kill](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_kill)</td>
 <td>[bluemix ic logs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_logs)</td>
 <td>[bluemix ic namespace-get](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](/docs/cli/reference/bluemix_cli/index.html#pause)</td>
 </tr>
 <tr>
 <td>[bluemix ic port](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_port)</td>
 <td>[bluemix ic ps](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic rename](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rename)</td>
 <td>[bluemix ic reprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_reprovision)</td>
 <td>[bluemix ic restart](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_restart)</td>
 </tr>
 <tr>
 <td>[bluemix ic rm](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rm)</td>
 <td>[bluemix ic rmi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rmi)</td>
 <td>[bluemix ic route-map](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic run](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_run)</td>
 </tr>
 <tr>
 <td>[bluemix ic service-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_bind)</td>
 <td>[bluemix ic service-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_unbind)</td>
 <td>[bluemix ic start](/docs/cli/reference/bluemix_cli/index.html#ic_start)</td>
 <td>[bluemix ic stats](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_stats)</td>
 <td>[bluemix ic stop](/docs/cli/reference/bluemix_cli/index.html#ic_stop)</td>
 </tr>
 <tr>
 <td>[bluemix ic top](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_top)</td>
 <td>[bluemix ic unpause](/docs/cli/reference/bluemix_cli/index.html#unpause)</td>
 <td>[bluemix ic unprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_unprovision)</td>
 <td>[bluemix ic volume-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_inspect)</td>
 <td>[bluemix ic volume-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_create)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-fs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs)</td>
 <td>[bluemix ic volume-fs-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_create)</td>
 <td>[bluemix ic volume-fs-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_remove)</td>
 <td>[bluemix ic volume-fs-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_flavors)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_remove)</td>
 <td>[bluemix ic volumes](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic wait](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic wait-status](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait_status)</td>
 <td>[bluemix ic version](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_version)</td>
 </tr>
  </tbody>
 </table>


## bluemix ic attach
{: #bluemix_ic_attach}

実行中のコンテナーを制御するか、その出力を表示します。終了してコンテナーを停止するには `CTRL+C` を使用します。このコマンドは Docker CLI を呼び出します。詳細については、Docker ヘルプで [attach ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} コマンドを参照してください。

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>--no-stdin (オプション)</dt>
   <dd>標準入力を含めません。</dd>
   <dt>--sig-proxy (オプション)</dt>
   <dd>受信したすべてのシグナルをプロセスに伝達します。デフォルト値は <i>true</i> です。</dd>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
    </dl>

<strong>例</strong>:

次の例は、コンテナー `my_container` にアタッチする要求です。

```
bluemix ic attach my_container
```



## bluemix ic build
{: #bluemix_ic_build}

IBM Containers ビルド・サービスを呼び出して、Docker イメージをローカルにビルドするか、またはプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内にビルドします。このコマンドは Docker CLI を呼び出します。詳細については、Docker ヘルプで [build ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/build/){: new_window} コマンドを参照してください。

```
bluemix ic build -t TAG|--tag TAG [--no-cache] [-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>-t <i>TAG</i>|--tag <i>TAG</i> (必須)</dt>
   <dd>作成されたイメージに適用するリポジトリー名。</dd>
   <dt>--no-cache (オプション)</dt>
   <dd>イメージをビルドするときにキャッシュを使用しません。デフォルトは、<i>false</i> です。</dd>
   <dt>--pull (オプション)</dt>
   <dd>レジストリーからベース・イメージを (それがキャッシュさ
れている場合でも) プルしようとします。</dd>
   <dt>-q|--quiet (オプション)</dt>
   <dd>コンテナーが生成する詳細出力を抑止します。デフォルトは、<i>false</i> です。</dd>
   <dt><i>DOCKERFILE_LOCATION</i> (必須)</dt>
   <dd>ローカル・ホスト上の Dockerfile およびコンテキストのパス。</dd>
    </dl>

<strong>例</strong>:

次の例は、
*myimage* という名前のイメージをビルドする要求です。
ビルドで使用される Dockerfile および他の成果物は、コマンドが実行されるディレクトリーと同じディレクトリー内にあります。レジストリーおよび名前空間がイメージ名と共に含まれているため、イメージは組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内にビルドされます。

```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage
```


## bluemix ic cp
{: #bluemix_ic_cp}
コンテナーとローカル・ファイル・システムの間でファイルまたはフォルダーをコピーします。このコマンドは Docker CLI を呼び出します。詳細については、Docker ヘルプで [cp ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} コマンドを参照してください。


## bluemix ic cpi
{: #bluemix_ic_cpi}

Docker Hub イメージ、またはローカル・レジストリーからのイメージにアクセスし、そのイメージをプライベート {{site.data.keyword.Bluemix_notm}} リポジトリーにコピーします。

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:
   <dl>
   <dt><i>SOURCE_IMAGE</i> (必須)</dt>
   <dd>ソース・リポジトリーおよびイメージの名前。</dd>
   <dt><i>DESTINATION_IMAGE</i> (必須)</dt>
   <dd>プライベート {{site.data.keyword.Bluemix_notm}} リポジトリー URL (名前空間と宛先イメージ名を含む)。イメージのタグはオプションです。</dd>
   </dl>

<strong>例</strong>:

ソース・リポジトリーからプライベート・リポジトリーにイメージをコピーし、そのイメージのタグを追加します。

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

`sinatra` イメージを `training` リポジトリーからプライベート・リポジトリー `registry.ng.bluemix.net/mynamespace` にコピーし、そのイメージの名前を `mysinatra` にします。イメージ `mysinatra` 用にタグ `v1` を追加します。

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}

コンテナー内でコマンドを実行します。詳細については、Docker ヘルプで [exec ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} コマンドを参照してください。

```
bluemix ic exec [-d|--detach] [-it] [-u USER|--user USER] CONTAINER [CMD]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-d|--detach (オプション)</dt>
   <dd>バックグラウンドで指定されたコマンドを実行します。</dd>
   <dt>-it (オプション)</dt>
   <dd>対話モード。標準入力が表示されている状態を維持します。終了するには <i>exit</i> と入力します。</dd>
   <dt>-u <i>USER</i>|--user <i>USER</i> (オプシ
ョン)</dt>
   <dd>ユーザー名。</dd>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   <dt><i>CMD</i> (必須)</dt>
   <dd>指定されたコンテナー内で実行するコマンド。</dd>
   </dl>

<strong>例</strong>:

`bash` コマンドを `my_container` コンテナー内で対話モードで実行します。

```
bluemix ic exec -it my_container bash
```

`date` コマンドを `my_container` コンテナー内で実行します。

```
bluemix ic exec my_container date
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

スケーラブル・コンテナー・グループを作成します。

```
bluemix ic group-create [--publish,-p PORT] --name GROUP_NAME [--memory,-m MEMORY_SIZE] [-n,--hostname HOSTNAME] [-d,--domain DOMAIN] [--env,-e ENV_KEY=ENV_VAL] [--env-file ENVIRO

NMENT_VARIABLE_FILE] [-P false|true] [--volume] [--min MIN_INSTANCE_COUNT] [--max MAX_INSTANCE_COUNT] [--desired DESIRED_INSTANCE_COUNT] [--anti false|true] [--auto false|true] IMAGE_NAME [CMD [CMD ...]]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:
   <dl>
    <dt><i>IMAGE_NAME</i> (必須)</dt>
   <dd>コンテナー・グループ内の各コンテナー・インスタンスに含まれるイ
メージ。イメージの後にコマンドをリストできますが、イメージの後にオプションを置かないでください。イメージを指定する前に、すべてのオプションを含めてください。<br><br>組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内のイメージを使用する場合、形式 <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i> でイメージを指定します。<br><br>IBM Containers によって提供されるイメージを使用する場合、組織の名前空間を含めないでください。形式 <i>registry.ng.bluemix.net/IMAGE</i> でイメージを指定してください。</dd>
   <dt>--name <i>GROUP_NAME</i> (required)</dt>
   <dd>グループに名前を割り当てます。<i>-n</i> は推奨されません。<br>
   <strong>ヒント:</strong> コンテナー名の先頭は文字でなければなりません。名前には、大文字、小文字、数字、ピリオド (.)、下線 (_)、およびハイフン (-) を使用できます。</dd>
   <dt>-m <i>MEMORY_SIZE</i>|--memory <i>MEMORY_SIZE</i> (オプション)</dt>
   <dd>グループにメモリー制限を MB 単位で割り当てます。CLI からコンテナー・グループを作成する場合、各コンテナー・インスタンスのデフォルト値は <i>64</i> MB です。{{site.data.keyword.Bluemix_notm}} ダッシュボードからコンテナー・グループを作成する場合、各コンテナー・インスタンスのデフォルト値は <i>256</i> MB です。受け入れられる値は、<i>64</i>、<i>256</i>、<i>512</i>、<i>1024</i>、および <i>2048</i> です。メモリー限度が割り当てられた後、その値を変更することはできません。</dd>
   <dt>-n <i>HOSTNAME</i>|--hostname <i>HOSTNAME</i> (オプション)</dt>
   <dd>ホスト名 (<i>mycontainerhost</i> など)。ホストとドメインが結合して、完全なパブリック経路 URL (例えば
<i>http://mycontainerhost.mybluemix.net</i>) を形成します。<i>bluemix ic group-inspect</i> コマンドを使用してコンテナーの詳細をレビューすると、ホストとドメインが経路として一緒にリストされます。</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (オプション)</dt>
   <dd>通常は、このドメインは <i>.mybluemix.net</i> です。ホストとドメインが結合して、完全なパブリック経路 URL (例えば <i>http://mycontainerhost.mybluemix.net</i>) を形成します。<i>bluemix ic group-inspect</i> コマンドを使用してコンテナーの詳細をレビューすると、ホストとドメインが経路として一緒にリストされます。</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>|--env <i>ENV_KEY=ENV_VAL</i> (オプション)</dt>
   <dd>環境変数を設定します。複数のキーは別々にリストしてください。引用符を含める場合、環境変数名と値の両方を囲むように指定します。
例えば、`-e "key1=value1" -e "key2=value2" -e
"key3=value3"` のようにします。指定可能な環境変数のうち、一般的に使用されるものを次の表に示します。</dd>
    </dl>


|  環境変数                              |     説明                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | コンテナーにサービスをバインドします。`CCS_BIND_APP` 環境変数を使用して、アプリをコンテナーにバインドします。このアプリはターゲット・サービスにバインドされ、ブリッジとして機能します。これにより、{{site.data.keyword.Bluemix_notm}} は、ブリッジ・アプリの `VCAP_SERVICES` 情報を、実行中のコンテナー・インスタンスに注入することができます。ブリッジ・アプリの作成について詳しくは、[コンテナーへのサービスのバインド](../../../containers/container_integrations_binding.html){: new_window}を参照してください。 |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | ブリッジ・アプリを使用せずに Bluemix サービスをコンテナーに直接バインドするには、CCS_BIND_SRV を使用します。このバインディングにより、Bluemix は、実行中のコンテナー・インスタンスに VCAP_SERVICES 情報を注入できます。複数の Bluemix サービスをリストするには、同じ環境変数の一部としてそれらのサービスを組み込みます。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | コンテナー内でモニターされるログ・ファイルを追加します。`LOG_LOCATIONS` 環境変数をログ・ファイルへのパスと共に組み込んでください。 |
{: caption="Table 2. Commonly used environment variables" caption-side="top"}

 <dl>
   <dt>--env-file <i>ENVIRONMENT_VARIABLE_FILE</i> (オプション)</dt>
   <dd> ファイルから環境変数をインポートします。ここで、ENVFILE はローカル・ディレクトリー上のファイルのパスです。ファイル内の各行が、1 つの key=value ペアを表します。</dd>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (オプション)</dt>
   <dd><i>VolumeId:ContainerPath[:ro]</i> 形式で詳細を指定して、コンテナーにボリュームを接続します。<ul>
   <li><i>VOLUME</i>: ボリュームの ID または名前。</li>
   <li><i>CONTAINER_PATH</i>: コンテナー内でのボリュームへの絶対パス。</li>
   <li>ro (オプション):<i>ro</i> を指定すると、ボリュームはデフォルトの読み取り/書き込みではなく読み取り専用になります。</li></ul>
   </dd>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (オプション)</dt>
   <dd>HTTP トラフィックのポートを公開します。グループ内のコンテナーは、この HTTP ポートを listen する必要があります。HTTPS 要求を行うことはできません。コンテナー・グループに対して複数のポートを含めることはできません。<br><br>ポートを指定したら、同じ {{site.data.keyword.Bluemix_notm}} スペース内でホストにアクセスしようとする {{site.data.keyword.Bluemix_notm}} Load Balancer またはコンテナーがアプリを使用できるように設定します。これにより、{{site.data.keyword.Bluemix_notm}} Load Balancer またはコンテナーは、そのポートを使用して、同じ {{site.data.keyword.Bluemix_notm}} スペース内のホストおよびアプリにアクセスできるようになります。使用するイメージの Dockerfile 内にポートが指定されている場合、そのポートを含めてください。<br>
   <strong>ヒント</strong>: <ul>
   <li>IBM 認定 Liberty Server イメージ、またはこのイメージの変更版の場合、ポート 9080 を入力します。</li>
   <li>IBM 認定 Node.js イメージ、またはこのイメージの変更版の場合、ポート 8000 を入力します。</li>
   </ul>
   </dd>
   <dt>-P (オプション)</dt>
   <dd>すべてのポートを公開します。</dd>
   <dt>--min <i>MIN_INSTANCE_COUNT</i> (オプション)</dt>
   <dd>インスタンスの最小数。デフォルトは 1 です。インスタンスの最小数を設定した
場合、その値をコンテナー・グループ作成後に変更することはできません。</dd>
   <dt>--max <i>MAX_INSTANCE_COUNT</i> (オプション)</dt>
   <dd>インスタンスの最大数。デフォルトは 2 です。インスタンスの最大数を設定した
場合、その値をコンテナー・グループ作成後に変更することはできません。</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (オプション)</dt>
   <dd>必要なインスタンス数。デフォルトは 2 です。</dd>
   <dt>--auto (オプション)</dt>
   <dd>コンテナー・グループが作成され、自動リカバリーが有効にされてい
る場合、IBM Containers は、割り当てられたポートへの HTTP 要求を使用して各インスタンスの正常性を検査します。<br>
その後 2 回の 90 秒間隔のうちにコンテナー・インスタンスから応答を受け取らなければ、そのインスタンスは削除され、新しいインスタンスに置き換えられます。コンテナーが応答すればアクションは行われません。このプロセスは連続して繰り返されます。30 分の時間枠の間に、グループ・メンバーとなった異なるコンテナーの総数が、最大グループ・サイズの 3 倍以上になった場合、そのコンテナー・グループに対する自動リカバリーは永続的に無効になります。自動リカバリーを再度有効にするには、コンテナー・グループを再作成する必要があります。</dd>
  <dt>--anti (オプション)</dt>
  <dd> アンチアフィニティーを使用して、コンテナー・グループの高可用性を高めます。--anti オプションを指定すると、グループ内の各コンテナー・インスタンスが、強制的に別個の物理計算ノードに配置されます。これにより、ハードウェア障害でグループ内の全コンテナーがクラッシュする可能性が低下します。各 Bluemix 地域および組織でデプロイメントに使用可能な計算ノードのセットは限られているため、グループ・サイズが大きい場合、このオプションを使用できないことがあります。デプロイメントが成功しない場合は、グループ内のコンテナー・インスタンスの数を減らすか、--anti オプションを削除してください。</dd>
   <dt><i>CMD</i> (必須)</dt>
   <dd>コンテナー・グループに渡されて実行されるコマンドと引数。このコマンドは長時間実行コマンドでなければなりません。実行時間があまり長くない一時的なコマンド (例えば、<i>/bin/date</i> など) は、コンテナーがクラッシュする原因となる可能性があるため、使用しないでください。<br> 
<strong>注:</strong> <ul>
   <li>コマンドおよびその引数は、<i>bluemix ic run</i> コマンド・ラインの末尾に指定する必要があります。</li>
   <li>コマンド引数にハイフン (-) が含まれる場合 (前のコマンド例の
<i>-c</i> のような場合)、コマンドの前にはハイフンを 2 つ (--) 付ける
必要があります。</li>
   </ul></dd>
   </dl>


<strong>例</strong>:

IBM Containers によって提供される `registry.ng.bluemix.net/ibmnode` イメージを使用してコンテナー・グループ `my_container_group` を作成し、そのコンテナー・グループで長時間実行コマンド `ping localhost` を実行します。

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

IBM Containers によって提供される `registry.ng.bluemix.net/ibmnode` イメージを使用してコンテナー・グループ `my_container_group` を作成し、そのコンテナー・グループで長時間実行コマンド `tail -f /dev/null` を実行します。

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

`registry.ng.bluemix.net/ibmliberty` イメージを使用して、スケーラブル・グループ `mygroup` を自動リカバリーを有効にして作成します。ポートは `9080`、ホスト名は `mycontainerhost`、ドメイン名は `mybluemix.net` です。
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty
```


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

コンテナー・グループの作成時に指定された詳細情報 (環境変数、ポート、メモリーなど) を表示します。

```
bluemix ic group-inspect CONTAINER_GROUP
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (必須)</dt>
   <dd>コンテナー・グループ ID または名前。</dd>
   </dl>

<strong>例</strong>:

次の例は、コンテナー・グループ `my_group` を検査する要求を示しています。

```
bluemix ic group-inspect my_group
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

指定されたコンテナー・グループのインスタンスをリストします。

```
bluemix ic group-instances CONTAINER_GROUP
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (必須)</dt>
   <dd>コンテナー・グループ ID または名前。</dd>
   </dl>

<strong>例</strong>:

コンテナー・グループ `my_group` のすべてのインスタンスをリストします。

```
bluemix ic group-instances my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

スペースからコンテナー・グループを削除します。

```
bluemix ic group-remove [-f|--force] GROUP_NAME [GROUP_NAME2 [...]]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-f|--force (オプション)</dt>
   <dd>実行中のコンテナーまたは障害が起こったコンテナーを強制的に削除
します。</dd>
   <dt><i>GROUP_NAME</i> (必須)</dt>
   <dd>コンテナー・グループ ID または名前。</dd>
   </dl>


<strong>例</strong>:

次の例は、コンテナー・グループを削除する要求です。ここで、`my_group` はコンテナー・グループの名前です。

```
bluemix ic group-remove my_group
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

コンテナー・グループを更新します。


```
bluemix ic group-update [--anti] [--desired DESIRED_INSTANCE_COUNT] [-e ENV_KEY=ENV_VAL] GROUP_NAME
```

**ヒント:** コンテナー・グループのホスト名またはドメインを更新するには、`bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP` を使用します。

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:
 <dl>
   <dt>--anti (オプション)</dt>
   <dd>アンチアフィニティーを使用して、コンテナー・グループの高可用性を高めます。--anti オプションを指定すると、グループ内の各コンテナー・インスタンスが、強制的に別個の物理計算ノードに配置されます。これにより、ハードウェア障害でグループ内の全コンテナーがクラッシュする可能性が低下します。各 Bluemix 地域および組織でデプロイメントに使用可能な計算ノードのセットは限られているため、グループ・サイズが大きい場合、このオプションを使用できないことがあります。デプロイメントが成功しない場合は、グループ内のコンテナー・インスタンスの数を減らすか、--anti オプションを削除してください。</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (オプション)</dt>
   <dd>必要なインスタンス数。デフォルトは <i>2</i> です。</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>(オプション)</dt>
   <dd>環境変数を設定します。複数のキーは別々にリストしてください。引用符を含める場合、環境変数名と値の両方を囲むように指定します。
例えば、`-e "key1=value1" -e "key2=value2" -e
"key3=value3"` のようにします。</dd>
   <dt><i>GROUP_NAME</i> (必須)</dt>
   <dd>コンテナー・グループ ID または名前。</dd>
   </dl>

<strong>例</strong>:

次の例は、コンテナー・グループ `my_group` を更新する要求です。

```
bluemix ic group-update --desired 5 my_group
```


## bluemix ic groups
{: #bluemix_ic_groups}

組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内のコンテナー・グループをリストします。

```
bluemix ic groups [-q]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:
	<dl>
	<dt>-q (オプション)</dt>
   	<dd>グループ ID のみを表示します。</dd>
	</dl>


## bluemix ic images
{: #bluemix_ic_images}

組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内の使用可能なすべてのイメージのリストを表示します。詳細については、Docker ヘルプで [images ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/images){: new_window} コマンドを参照してください。リストには、イメージ ID、作成日、およびイメージ名が含まれます。

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-a|--all (オプション)</dt>
   <dd>組織のリポジトリー内の各イメージについて、最新のイメージ層のみ
ではなく、すべてのイメージ層を含めます。</dd>
   <dt>-f (オプション)</dt>
   <dd>指定した条件でイメージのリストをフィルターに掛けます。</dd>
   <dt>--no-trunc (オプション)</dt>
   <dd>出力を切り捨てません。</dd>
   <dt>-q|--quiet (オプション)</dt>
   <dd>数字の ID のみを表示します。</dd>
   </dl>

<strong>例</strong>:

次の例は、組織の使用可能なイメージのリストを受け取る要求です。

```
bluemix ic images
```


## bluemix ic info
{: #bluemix_ic_info}

コンテナー・クラウド・サービス・インスタンスの状態を説明する情報を表示します。この情報に含まれるのは、コンテナーの限度、コンテナーの使用状況、実行中のコンテナー、メモリーの限度、メモリーの使用状況、浮動 IP アドレスの限度、浮動 IP アドレスの使用状況、CCS ホスト URL、レジストリー・ホスト URL、およびデバッグ・モード状況です。

```
bluemix ic info
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット


## bluemix ic init
{: #bluemix_ic_init}

IBM Containers サービスの全機能を使用できるようにローカル・マシン上のコンテナー環境を初期化します。

```
bluemix ic init
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

**注:** 初期化を行う前に、Docker CLI (docker) がインストールされ、PATH 環境変数内に構成されていることを確認してください。別の地域に切り替えるには、`bluemix region-set` コマンドを使用します。

<strong>例</strong>:

`us-south` 地域に切り替えます。

```
bluemix region-set us-south
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

コンテナーに関する情報を表示します。詳細については、Docker ヘルプで [inspect ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} コマンドを参照してください。

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>IMAGE</i> (必須)</dt>
   <dd>イメージの名前または ID を指定することによって、特定のイメージ
についての詳細情報を表示します。</dd>
   <dt>images (必須)</dt>
   <dd>リポジトリー内のすべてのイメージについての詳細情報を表示します。</dd>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID を指定することによって、特定のコンテ
ナーについての詳細情報を表示します。</dd>
   </dl>

**ヒント:** 一度に指定できるのは、
*IMAGE*、*images*、または
*CONTAINER* のいずれか 1 つのみです。

<strong>例</strong>:

次の例は、`proxy` という名前のコンテナーを検査する要求です。

```
bluemix ic inspect proxy
```


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

使用可能な浮動 IP アドレスをコンテナーにバインドします。

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (必須)</dt>
   <dd>バインドする IP アドレス。</dd>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>バインドするコンテナーの ID または名前。</dd>
   </dl>

<strong>例</strong>:

次の例は、IP アドレス `192.123.12.12` をコンテナー `proxy` にバインドする要求です。

```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

コンテナー・クラウド・サービス・インスタンスから浮動 IP アドレスを解放します。

```
bluemix ic ip-release IP_ADDRESS [IP_ADDRESS2 [...]]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (必須)</dt>
   <dd>リリースする IP アドレス。</dd>
   </dl>


## bluemix ic ip-request
{: #ip_request}
新しい浮動 IP アドレスを要求します。

```
bluemix ic ip-request [-q]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-q (オプション)</dt>
   <dd>IP アドレスのみをリストします。それらの IP アドレスにバインドされたコンテナーの ID はリストしません。</dd>
   </dl>


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

浮動 IP アドレスをそのコンテナーからアンバインドします。

パブリック IP アドレスは、IBM Containers の制限付きリソースです。したがって、スペースに割り当てられていてコンテナーにバインドされていないパブリック IP アドレスは、およそ週 1 回の頻度で無料試用ユーザーから定期的に再要求されます。アンバインドされたパブリック IP アドレスは、従量制課金カスタマーまたはサブスクリプション・カスタマーから再要求されることはありません。

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (必須)</dt>
   <dd>アンバインドする IP アドレス。</dd>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>アンバインドするコンテナーの ID または名前。</dd>
   </dl>

<strong>例</strong>:

次の例は、IP アドレス `192.123.12.12` をコンテナー `proxy` からアンバインドする要求です。

```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic ips
{: #bluemix_ic_ips}

ログインしているユーザーが使用可能な浮動 IP アドレスをリストします。このリストには、IP アドレスと、IP アドレスがリンクされている先のコンテナー ID が含まれます。IP アドレスが未使用の場合、コンテナー ID は示されません。

```
bluemix ic ips [-q]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-q (オプション)</dt>
   <dd>IP アドレスのみをリストします。それらの IP アドレスにバインドされたコンテナーの ID はリストしません。</dd>
   </dl>


<strong>例</strong>:

次の例は、組織のすべての IP アドレスのリストを受け取る要求を示しています。
```
bluemix ic ips -q
```


## bluemix ic kill
{: #bluemix_ic_kill}

コンテナーを停止せずにコンテナー内の実行中のプロセスを停止します。詳細については、Docker ヘルプで [kill ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} コマンドを参照してください。

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i> (オプション)</dt>
   <dd>コンテナー内の実行中のプロセスにコマンドを送信します。</dd>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの ID または名前。</dd>
   </dl>


<strong>例</strong>:

次の例は、`proxy` という名前のコンテナー内のプロセスを停止する要求です。

```
bluemix ic kill proxy
```


## bluemix ic logs
{: #bluemix_ic_logs}

実行中のコンテナーの出力ログまたはエラー・ログを表示します。詳細については、Docker ヘルプで [logs ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} コマンドを参照してください。
```
bluemix ic logs [OPTIONS] CONTAINER
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

ログイン先の組織のプライベート {{site.data.keyword.Bluemix_notm}} イメージ・リポジトリーの名前を表示します。

```
bluemix ic namespace-get
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

ログイン先の組織のプライベート {{site.data.keyword.Bluemix_notm}} イメージ・リポジトリーの名前を設定します。

*制限*: リポジトリー名前空間の名前にハイフン (`-`) を使用することはできません。

```
bluemix ic namespace-set NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>NAME</i> (必須)</dt>
   <dd>組織のリポジトリー名前空間を (まだ設定されていない場合に) 設定
する 1 回限りの機能です。名前空間を設定した後、続行する前に、`bluemix ic init` コマンドを使用して IBM Containers を再初期化してください。</dd>
   </dl>


## bluemix ic pause
{: #pause}

実行中のコンテナー内のすべてのプロセスを休止します。詳細については、Docker ヘルプで [pause ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} コマンドを参照してください。コンテナーを停止する場合は、[bluemix ic unpause](#unpause) コマンドを参照してください。

```
bluemix ic pause CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:
   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   </dl>

<strong>応答</strong>:

- コンテナーは正常に休止されました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`

 ここで、`{message}` は関連するエラーです。


- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

<strong>例</strong>:

次の例は、`proxy` という名前のコンテナーを休止する要求です。

```
bluemix ic pause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

コンテナーのポート・マッピングまたは特定のマッピングをリストします。このコマンドは `docker port` コマンドをラップします。詳細については、Docker ヘルプで [port ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/port/){: new_window} コマンドを参照してください。


## bluemix ic ps
{: #bluemix_ic_ps}
ログインしているユーザーの名前空間で実行中のコンテナーのリストを表示します。デフォルトでは、このコマンドは実行中のコンテナーのみを表示します。詳細については、Docker ヘルプで [ps ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} コマンドを参照してください。

```
bluemix ic ps [-a|--all] [--filter env=SEARCH_CRITERIA] [-s|--size] [-l NUM|--limit NUM] [-q|--quiet]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-a|--all (オプション)</dt>
   <dd>実行中のコンテナーも停止状態のコンテナーも、どちらもすべて表示します。</dd>
   <dt>--filter env=<i>SEARCH_CRITERIA</i> (オプション)</dt>
   <dd>特定の環境変数値を持つコンテナーを検索します。コンテナーの検査時に CLI 応答の「Env」セクションにリストされている任意の環境変数キーまたは値によって、コンテナーをフィルターに掛けることができます。SEARCH_CRITERIA は、検索するキーまたは値に置き換えてください。検索基準は、完全一致突き合わせである必要はありません。</dd>
   <dt>-s|--size (オプション)</dt>
   <dd>コンテナーのサイズをリストします。</dd>
   <dt>-l <i>NUM</i>|--limit <i>NUM</i> (オプション)</dt>
   <dd>最近作成されたコンテナーをリストします。ここで <i>NUM</i> は、
最近作成されたコンテナーのうちのいくつのコンテナーを返したいかを指定する数です。
<br><br> 例えば、<i>node1</i> から <i>node5</i> までのコンテ
ナーを順次作成した場合、コマンド <i>bluemix ic ps --limit 2</i> は、
作成されたコンテナーのうちの最新の 2 つである node4 と node5 を返します。</dd>
   <dt>-q|--quiet (オプション)</dt>
   <dd>コンテナー ID のみを表示します。</dd>
   </dl>


<strong>例</strong>:

次の例は、実行中と停止状態のすべてのコンテナーを表示する要求です。

```
bluemix ic ps -a
```


## bluemix ic rename
{: #bluemix_ic_rename}
コンテナーの名前を変更します。詳細については、Docker ヘルプで [rename ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} コマンドを参照してください。

```
bluemix ic rename OLD_NAME NEW_NAME
```
<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker<strong>コマンド・オプション</strong>:

<dl>
   <dt><i>OLD_NAME</i> (必須)</dt>
   <dd>コンテナーの古い名前。</dd>
   <dt><i>NEW_NAME</i> (必須)</dt>
   <dd>コンテナーの新しい名前。</dd>
   </dl>


## bluemix ic reprovision
{: #bluemix_ic_reprovision}

ログインしている Bluemix スペースで IBM Containers サービスを再作成します。スペースの元の割り当て量は維持されます。

<strong>重要</strong>: このコマンドを実行した場合、このスペース内の単一コンテナーおよびグループはどれも、再プロビジョンされたスペースにマイグレーションされず、マイグレーション・プロセス中に削除されます。

```
bluemix ic reprovision [--force|-f] [ENVIRONMENT_NAME]
```
<strong>コマンド・オプション</strong>:<dl>
   <dt>--force|-f (オプション)</dt>
   <dd>Bluemix スペースで IBM Containers サービスを強制的に再作成します。</dd>
   <dt><i>AVAILABILITY_ZONE</i> (必須)</dt>
   <dd>コンテナーがデプロイされた IBM Containers アベイラビリティー・ゾーンの名前。アベイラビリティー・ゾーンが指定されない場合は、地域に設定されたデフォルト・アベイラビリティー・ゾーンが使用されます。</dd>
   </dl>


## bluemix ic restart
{: #bluemix_ic_restart}

コンテナーを再始動します。詳細については、Docker ヘルプで [restart ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} コマンドを参照してください。

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (オプション)</dt>
   <dd>コンテナーが再始動されるまでに待機する秒数。</dd>
   </dl>


<strong>応答</strong>:

- コンテナーは正常に再始動されました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`

 ここで、`{message}` は関連するエラーです。


- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

<strong>例</strong>:

次の例は、`proxy` という名前のコンテナーを再始動する要求です。

```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

コンテナーを削除します。詳細については、Docker ヘルプで [rm ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} コマンドを参照してください。

```
bluemix ic rm [-f|--force] CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-f|--force (オプション)</dt>
   <dd>実行中のコンテナーまたは障害が起こったコンテナーを強制的に削除
します。</dd>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   </dl>

<strong>応答</strong>:

- コンテナーは正常に削除されました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`

 ここで、`{message}` は関連するエラーです。


- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

<strong>例</strong>:

次の例は、`proxy` という名前のコンテナーを削除する要求です。

```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

ログインしているユーザーの名前空間からイメージを削除します。詳細については、Docker ヘルプで [rmi ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} コマンドを参照してください。

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-R <i>REGISTRY</i>|--registry <i>REGISTRY</i> (オプション)</dt>
   <dd>レジストリー・ホストを変更します。
デフォルトでは、<i>bluemix ic init</i> コマンドに指定したレジストリーが使用されます。</dd>
   <dt><i>IMAGE</i> (必須)</dt>
   <dd>削除するイメージの名前。イメージ名にタグが指定されていない場合、
<i>latest</i> とタグ付けされたイメージはデフォルトで削除されます。
</dd>
   </dl>

<strong>応答</strong>:

- 削除されました: `{IMAGE}`

 ここで、`{IMAGE}` は削除されたイメージの名前です。

- エラー! レジストリー・ホストが指定されていません。

- イメージ削除は失敗しました - コンテナー・クラウド・レジストリーに接続できませんでした。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`

 ここで、`{message}` は関連するエラーです。


<strong>例</strong>:

次の例は、イメージ `mynamespace/myimage:latest` を削除する要求です。

```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic route-map
{: #bluemix_ic_route_map}

コンテナー・グループへのアクセスに使用するインターネット・トラフィックの経路を設定します。このコマンドを使用して、新規経路を設定するか、既存の経路を更新できます。

```
bluemix ic route-map [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (オプション)</dt>
   <dd>経路のホスト名。ホスト名は、完全なパブリック経路 URL の最初の部分です。例えば、URL <i>mycontainerhost.mybluemix.net</i> 中の <i>mycontainerhost</i> です。</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (オプション)</dt>
   <dd>完全なパブリック経路 URL の 2 番目の部分である、経路のドメイン名。
ほとんどの場合、ドメインは <i>mybluemix.net</i> です。このパラメーターを使用してプライベート・ドメインを指定することもできます。</dd>
   <dt><i>CONTAINER_GROUP</i> (必須)</dt>
   <dd>コンテナー・グループ ID または名前。</dd>
   </dl>

<strong>例</strong>:

次の例は、`GROUP1` と呼ばれるグループの経路をマップする要求です。ここで、`my_host` はホスト名で、`mybluemix.net` はドメインです。
```
bluemix ic route-map -n my_host -d mybluemix.net GROUP1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

コンテナー・グループへのアクセスに使用するインターネット・トラフィックの経路を設定します。このコマンドを使用して、新規経路を設定するか、既存の経路を更新できます。

```
bluemix ic route-unmap [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (オプション)</dt>
   <dd>経路のホスト名。</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (オプション)</dt>
   <dd>経路のドメイン名。</dd>
   <dt><i>CONTAINER_GROUP</i> (必須)</dt>
   <dd>コンテナー・グループ ID または名前。</dd>
   </dl>

<strong>例</strong>:

次の例は、`GROUP1` と呼ばれるグループ
の経路をマップ解除する要求です。ここで、`my_host` は
ホスト名、`organization.com` はドメインです。
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


## bluemix ic run
{: #bluemix_ic_run}

イメージ名を使用して、コンテナー・クラウド・サービスで新しいコンテナーを開始します。
詳細については、Docker ヘルプで [run ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/run/){: new_window} コマンドを参照してください。


```
bluemix ic run [-p PORT|--publish PORT] [-P] [-m MEMORY|--memory MEMORY] [-e ENV|--env ENV] [--volume VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS] [-it] IMAGE [CMD [CMD ...]]
```
**注:** Cloud Foundry コマンド・ツールがインストー
ルされていること、および Cloud Foundry トークンがあることを確認してください。
`bluemix login` および `bluemix ic
init` を使用した正常なログインによって、必要なトークンおよび
証明書が生成されます。
<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (オプション)</dt>
   <dd>HTTP トラフィックのポートを公開します。使用するイメージの Dockerfile 内に指定されているポートがあれば、それらのポートを含めます。複数の <i>-p</i> オプションを使用して、複数のポートを含めることができます。ポートを公開すると、パブリック IP アドレスが使用可能な場合、パブリック IP アドレスがコンテナーに自動的にバインドされます。<br><br>コンテナーにバインドしたい IP アドレスがスペース内に既に存在する場合、後でバインドするのでなく、その IP アドレスを指定できます。IP アドレスは、&lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt; <br> 形式で指定する必要があります。<br>スペース用の IP アドレスの要求について詳しくは、<a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a> コマンドを参照してください。<br><br>ポートを指定したら、同じ {{site.data.keyword.Bluemix_notm}} スペース内でホストにアクセスしようとする {{site.data.keyword.Bluemix_notm}} Load Balancer またはコンテナーがアプリを使用できるように設定します。使用するイメージの Dockerfile 内にポートが指定されている場合、そのポートを含めてください。<br><br>
<strong>ヒント:</strong><ul><li>IBM 認定 Liberty Server イメージ、またはこのイメージの変更版の場合、ポート 9080 を入力します。</li><li>IBM 認定 Node.js イメージ、またはこのイメージの変更版の場合、ポート 8000 を入力します。</li></ul></dd>
   <dt>-P (オプション)</dt>
   <dd>イメージの Dockerfile 内に指定されたポートを HTTP トラフィック
用に自動的に公開します。</dd>
   <dt>-m <i>MEMORY</i>|--memory <i>MEMORY</i> (オプ
ション)</dt>
   <dd>グループにメモリー制限を MB 単位で割り当てます。CLI からコンテナー・グループを作成す
る場合、各コンテナー・インスタンスのデフォルト値は 64 MB です。
{{site.data.keyword.Bluemix_notm}} ダッシュボードからコンテナ
ー・グループを作成する場合、各インスタンスのデフォルト値は 256 MB で
す。受け入れられる値は 64、256、512、1024、および 2048 です。メモリー限度が割り当てられた後、その値を変更することはできません。</dd>
   <dt>-e <i>ENV</i>|--env <i>ENV</i> (オプション)</dt>
   <dd>環境変数を設定します。ここで、<i>ENV</i> は key=value ぺアです。
複数のキーは別々にリストしてください。引用符を含める場合、環境変数名と値の両方を囲むように指定します。例えば、-e
"key1=value1" -e "key2=value2" -e "key3=value3"のようにします。指定可能な環境変数のうち、一般的に使用されるものを次の表に示します。</dd>
   </dl>


|      環境変数                          |   説明                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | コンテナーにサービスをバインドします。`CCS_BIND_APP` 環境変数を使用して、アプリをコンテナーにバインドします。このアプリはターゲット・サービスにバインドされ、ブリッジとして機能します。これにより、{{site.data.keyword.Bluemix_notm}} は、ブリッジ・アプリの `VCAP_SERVICES` 情報を、実行中のコンテナー・インスタンスに注入することができます。ブリッジ・アプリの作成について詳しくは、[コンテナーへのサービスのバインド](../../../containers/container_integrations_binding.html){: new_window}を参照してください。 |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | ブリッジ・アプリを使用せずに Bluemix サービスをコンテナーに直接バインドするには、CCS_BIND_SRV を使用します。このバインディングにより、Bluemix は、実行中のコンテナー・インスタンスに VCAP_SERVICES 情報を注入できます。複数の Bluemix サービスをリストするには、同じ環境変数の一部としてそれらのサービスを組み込みます。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | コンテナー内でモニターされるログ・ファイルを追加します。`LOG_LOCATIONS` 環境変数をログ・ファイルへのパスと共に組み込んでください。 |
{: caption="Table 3. Commonly used environment variables" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (オプション)</dt>
   <dd><i>VolumeId:ContainerPath[:ro]</i> 形式で詳細を指定して、コンテナーにボリュームを接続します。<ul>
   <li><i>VOLUME</i>: ボリュームの ID または名前。</li>
   <li><i>CONTAINER_PATH</i>: コンテナー内でのボリュームへの絶対パス。</li>
   <li>ro (オプション):<i>ro</i> を指定すると、ボリュームはデフォルトの読み取り/書き込みではなく読み取り専用になります。</li></ul>
   </dd>
   <dt>-n <i>NAME</i>|--name <i>NAME</i> (必須)</dt>
   <dd>コンテナーに名前を割り当てます。<br> <strong>ヒント:</strong> コンテナー名の先頭は文字でなければなりません。名前には、大文字、小文字、数字、ピリオド (.)、下線 (_)、およびハイフン (-) を使用できます。</dd>
   <dt>--link <i>NAME</i>:<i>ALIAS</i> (オプション)</dt>
   <dd>あるコンテナーが実行中の別のコンテナーと通信するようにしたい場合は、ホスト名の別名を使用してそのコンテナーを指定できます。</dd>
   <dt>-it (オプション)</dt>
   <dd>コンテナーを対話モードで実行します。コンテナーが作成された後、標準入力が表示されている状態を維持します。終了するには <i>exit</i> と入力します。</dd>
   <dt><i>IMAGE</i> (必須)</dt>
   <dd>コンテナーに含まれるイメージ。イメージの後にコマンドをリストできますが、イメージの後にオプションを置かないでください。イメージを指定する前に、すべてのオプションを含めてください。イメージを指定する前に、すべてのオプションを含めてください。<br><br>組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内のイメージを使用する場合、形式 <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i> でイメージを指定します。<br><br>
IBM Containers によって提供されるイメージを使用する場合は、形式
<i>registry.ng.bluemix.net/IMAGE</i> でイメージを指定します。</dd>
   <dt><i>CMD</i> (必須)</dt>
   <dd>コンテナー・グループに渡されて実行されるコマンドと引数。このコマンドは長時間実行コマンドでなければなりません。実行時間があまり長くない一時的なコマンド (例えば、<i>/bin/date</i> など) は、コンテナーがクラッシュする原因となる可能性があるため、使用しないでください。</dd>
   </dl>


<strong>例</strong>:

`registry.ng.bluemix.net/ibmnode` イメージに基づいて作成された `my_container` コンテナーで、長時間実行コマンド `sh -c "while true; do date; sleep 20; done"` を実行します。

```
bluemix ic run --name my_container registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


`my_namespace/nginx` イメージを使用して、メモリー限度が `1024` MB のコンテナー `proxy` を作成し、開始します。ここで、`my_namespace` は、ログイン・ユーザーと関連付けられた名前空間です。

```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

`my_namespace/blog` イメージを使用してコンテナーを作成して開始し、資格情報を環境変数として渡します。`my_namespace` は、ログイン・ユーザーと関連付けられた名前空間です。

```
bluemix ic run -n my_container -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/my_namespace/blog
```

`my_namespace/blog` イメージを使用してボリュームをコンテナーに追加します。ここで、`my_namespace` は、ログイン・ユーザーに関連付けられた名前空間です。

```
bluemix ic run -n my_container -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/my_namespace/blog
```


## bluemix ic service-bind
{: #bluemix_ic_service-bind}

実行中のコンテナー・グループにサービスを追加します。このコマンドは、コンテナー・グループにのみ使用可能です。単一コンテナーは、bluemix ic run コマンドの中でサービスをバインドする必要があります。

```
bluemix ic service-bind GROUP_NAME SERVICE_INSTANCE 
```
<strong>コマンド・オプション</strong>:<dl>
   <dt><i>GROUP_NAME</i> (必須)</dt>
   <dd>グループ ID または名前。</dd>
   <dt><i>SERVICE_INSTANCE</i> (必須)</dt>
   <dd>コンテナー・グループに追加するサービス・インスタンスの名前。</dd>
   </dl>


## bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

実行中のコンテナー・グループからサービスを削除します。このコマンドは、コンテナー・グループにのみ使用可能です。単一コンテナーは、コンテナーを削除し、サービスが含まれない新しいコンテナーを作成する必要があります。

```
bluemix ic service-unbind GROUP_NAME SERVICE_INSTANCE 
```
<strong>コマンド・オプション</strong>:<dl>
   <dt><i>GROUP_NAME</i> (必須)</dt>
   <dd>グループ ID または名前。</dd>
   <dt><i>SERVICE_INSTANCE</i> (必須)</dt>
   <dd>コンテナー・グループに追加するサービス・インスタンスの名前。</dd>
   </dl>


## bluemix ic start
{: #ic_start}
停止しているコンテナーを開始します。詳細については、Docker ヘルプで [start ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/start/){: new_window} コマンドを参照してください。コンテナーを停止する場合は、[bluemix ic stop](#ic_stop) コマンドを参照してください。

```
bluemix ic start CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   </dl>


<strong>応答</strong>:

- コンテナーは正常に開始しました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`

 ここで、`{message}` は関連するエラーです。


- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

<strong>例</strong>:

次の例は、`proxy` という名前のコンテナーを開始する要求です。

```
bluemix ic start proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

1 つ以上のコンテナーについて、使用状況統計をライブで表示します。終了するには `CTRL+C` を使用します。詳細については、Docker ヘルプで [stats ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} コマンドを参照してください。

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   <dt>--no-stream (オプション)</dt>
   <dd>最新の結果のみを表示し、それ以前の情報を含めません。</dd>
   </dl>

<strong>例</strong>:

次の例は、1 つのコンテナーについての最新の統計情報を表示する要求です。

```
bluemix ic stats --no-stream my_container
```


## bluemix ic stop
{: #ic_stop}
実行中のコンテナーを停止します。詳細については、Docker ヘルプで [stop ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} コマンドを参照してください。コンテナーを開始する場合は、[bluemix ic start](#ic_start) コマンドを参照してください。

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (オプション)</dt>
   <dd>コンテナーを強制終了するまでの待機秒数。</dd>
   </dl>

<strong>応答</strong>:

- コンテナーは正常に停止されました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`

 ここで、`{message}` は関連するエラーです。


- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

<strong>例</strong>:

次の例は、`proxy` という名前のコンテナーを停止する要求です。

```
bluemix ic stop proxy
```


## bluemix ic top
{: #bluemix_ic_top}

コンテナーで実行されているプロセスを表示します。詳細については、Docker ヘルプで [top ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/top/){: new_window} コマンドを参照してください。

```
bluemix ic top CONTAINER [CONTAINER]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   </dl>

<strong>例</strong>:

次の例は、`my_container` という名前のコンテナー内のプロセスを表示する要求です。

```
bluemix ic top my_container
```


## bluemix ic unpause
{: #unpause}

実行中のコンテナー内のすべてのプロセスを休止解除します。詳細については、Docker ヘルプで [unpause ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} コマンドを参照してください。コンテナーを休止する場合は、[bluemix ic pause](#pause) コマンドを参照してください。

```
bluemix ic unpause CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   </dl>

<strong>応答</strong>:

- コンテナーは正常に休止解除されました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`

 ここで、`{message}` は関連するエラーです。


- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

<strong>例</strong>:

次の例は、`proxy` という名前のコンテナーを休止解除する要求です。

```
bluemix ic unpause proxy
```


## bluemix ic unprovision
{: #bluemix_ic_unprovision}

ログインしている Bluemix スペースから IBM Containers サービスを削除します。

<strong>注意</strong>: このコマンドを実行すると、単一コンテナーとコンテナー・グループがすべて失われます。Bluemix では、まだスペースを使用可能です。IBM Containers の使用を再び開始するには、`bluemix ic reprovision` を実行して IBM Containers サービスを再度プロビジョンする必要があります。

```
bluemix ic reprovision [--force|-f] 
```
<strong>コマンド・オプション</strong>:<dl>
   <dt>--force|-f (オプション)</dt>
   <dd>Bluemix スペースから Bluemix を強制的に削除します。</dd>
 </dl>


## bluemix ic version
{: #bluemix_ic_version}

Docker および IBM Containers API のバージョンを表示します。

```
bluemix ic version
```

<strong>前提条件</strong>:  Docker

IBM Containers のバージョンを表示するには、`bluemix ic info` を実行します。詳細については、Docker ヘルプで [version ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/version/){: new_window} コマンドを参照してください。


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

ボリュームを作成します。

```
bluemix ic volume-create VOLUME_NAME FS_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>FS_NAME</i> (オプション)</dt>
   <dd>ファイル共有名ファイル共有が使用可能でないか指定されていない場合、ボリュームは、スペースのデフォルトのファイル共有上に作成されます。</dd>
   <dt><i>VOLUME_NAME</i> (必須)</dt>
   <dd>ボリューム名。名前には、小文字、数字、下線 (_)、およびハイフン
(-) を 使用できます。</dd>
   </dl>


<strong>例</strong>:

次の例は、ボリュームを作成する要求です。

```
bluemix ic volume-create volume_name fileshare_name
```


## bluemix ic volume-fs

{: #bluemix_ic_volume_fs}

ファイル共有をリストします。

```
bluemix ic volume-fs
```


## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

ファイル共有を作成します。

```
bluemix ic volume-fs-create FILE_SHARE_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (必須)</dt>
   <dd>ファイル共有名名前には、小文字、数字、下線 (_)、およびハイフン
(-) を 使用できます。</dd>
   </dl>

<strong>例</strong>:

以下の例では、ファイル共有を作成する要求を示します。
```
bluemix ic volume-fs-create my_file_share
```


## bluemix ic volume-fs-flavors

{: #bluemix_ic_volume_fs_flavors}

すべてのファイル共有のフレーバーをリストします。

```
bluemix ic volume-fs-flavors
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット


## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

ファイル共有を検査します。

```
bluemix ic volume-fs-inspect FILE_SHARE_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

  <dl>
  <dt><i>FILE_SHARE_NAME</i> (必須)</dt>
   <dd>ファイル共有名</dd>
   </dl>

<strong>例</strong>:

次の例は、ファイル共有を検査する要求です。ここで、`my_file_share` は、ファイル共有の名前です。
```
bluemix ic volume-fs-inspect my_file_share
```


## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

ファイル共有を削除します。

```
bluemix ic volume-fs-remove FILE_SHARE_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (必須)</dt>
   <dd>ファイル共有名</dd>
   </dl>

<strong>例</strong>:

次の例では、ファイル共有を削除する要求を示します。ここで、`my_file_share` は、ファイル共有の名前です。
```
bluemix ic volume-fs-remove my_file_share
```


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

ボリュームを検査します。


```
bluemix ic volume-inspect VOLUME_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (必須)</dt>
   <dd>ボリューム名。</dd>
   </dl>

<strong>例</strong>:

次の例は、ボリュームを検査する要求です。ここで、`volume_name` はボリュームの名前です。

```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

ボリュームを削除します。

```
bluemix ic volume-remove VOLUME_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (必須)</dt>
   <dd>ボリューム名。</dd>
    </dl>

<strong>例</strong>:

次の例は、ボリュームを削除する要求です。ここで、`volume_name` はボリュームの名前です。

```
bluemix ic volume-remove volume_name
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

ボリュームをリストします。

```
bluemix ic volumes
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット


## bluemix ic wait
{: #bluemix_ic_wait}

コンテナーを終了し、確認のために終了コードを表示します。詳細については、Docker ヘルプで [wait ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} コマンドを参照してください。

```
bluemix ic wait CONTAINER [CONTAINER]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   </dl>

<strong>例</strong>:

次の例は、`my_container` という名前のコンテナーを終了する要求です。

```
bluemix ic wait my_container
```


## bluemix ic wait-status
{: #bluemix_ic_wait_status}

単一コンテナーまたはコンテナー・グループが非過渡的な状態になるまで待機します。この待機時間中は、コマンド・ラインが戻らないため、コマンドを入力できません。コンテナーが非過渡的な状態になると、すぐに OK メッセージが表示されます。単一コンテナーの場合、非過渡的な状態には Running、Shutdown、Crashed、Paused、Suspended があります。コンテナー・グループの場合、非過渡的な状態には CREATE_COMPLETE、UPDATE_COMPLETE、FAILED があります。

```
bluemix ic wait-status CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   </dl>

<strong>例</strong>:

次の例は、`my_container` という名前のコンテナーを終了する要求です。

```
bluemix ic wait my_container
```
