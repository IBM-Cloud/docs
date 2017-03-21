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

*版本：*1.0.0

IBM Containers CLI 是一種 {{site.data.keyword.Bluemix_notm}} CLI 外掛程式，可管理 Bluemix 上的容器及容器群組。
{: shortdesc}

**附註：***必要條件* 列出使用指令之前需要哪些動作。沒有必要動作的指令會列為**無**。否則，必要條件可能包括下列一個以上的動作：
<dl>
<dt>端點</dt>
<dd>必須透過 <code>bluemix api</code> 設定 API 端點後，才能使用此指令。</dd>
<dt>登入</dt>
<dd>需要使用 <code>bluemix login</code> 指令進行登入後，才能使用此指令。如果是使用聯合 ID 登入，請使用 '--sso' 選項以一次性密碼進行鑑別。</dd>
<dt>目標</dt>
<dd>必須使用 <code>bluemix target</code> 指令來設定組織及空間後，才能使用此指令。</dd>
<dt>Docker</dt>
<dd>需要有 Docker CLI (docker)，才能在 IBM Containers CLI 外掛程式中執行指令。</dd>
</dl>

<table summary="您可以用來在 Bluemix 上管理容器的 bluemix 指令。">
 <caption>表格 1. 用來在 Bluemix 上管理容器的指令</caption>
 <thead>
 <th colspan="5">用來在 Bluemix 上管理容器的指令</th>
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
  <td>[bluemix ic info
](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_info)</td>
  <td>[bluemix ic init](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_init)</td>
  <td>[bluemix ic images
](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_images)</td>
  <td>[bluemix ic inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_inspect)</td>
 </tr>
 <tr>
 <td>[bluemix ic ip-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_bind)</td>
 <td>[bluemix ic ip-release](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-request
](/docs/cli/reference/bluemix_cli/index.html#ip_request)</td>
 <td>[bluemix ic ip-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_unbind)</td>
 <td>[bluemix ic ips](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ips)</td>
 </tr>
 <tr>
 <td>[bluemix ic kill](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_kill)</td>
 <td>[bluemix ic logs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_logs)</td>
 <td>[bluemix ic namespace-get
](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_get)</td>
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
 <td>[bluemix ic volume-fs
](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs)</td>
 <td>[bluemix ic volume-fs-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_create)</td>
 <td>[bluemix ic volume-fs-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_remove)</td>
 <td>[bluemix ic volume-fs-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors
](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_flavors)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_remove)</td>
 <td>[bluemix ic volumes
](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic wait](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic wait-status](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait_status)</td>
 <td>[bluemix ic version
](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_version)</td>
 </tr>
  </tbody>
 </table>


## bluemix ic attach
{: #bluemix_ic_attach}

控制執行中容器，或檢視其輸出。使用 `CTRL+C` 以結束並停止容器。此指令會呼叫 Docker CLI。如需相關資訊，請參閱 Docker 說明中的 [attach ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} 指令。

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>--no-stdin（選用）</dt>
   <dd>不要包含標準輸入。</dd>
   <dt>--sig-proxy（選用）</dt>
   <dd>將所有接收到的信號 Proxy 到處理程序。預設值為 <i>true</i>。</dd>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
    </dl>

<strong>範例</strong>：

下列範例顯示連接至容器 `my_container` 的要求：

```
bluemix ic attach my_container
```



## bluemix ic build
{: #bluemix_ic_build}

呼叫 IBM Containers 建置服務，以在本端或專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中建置 Docker 映像檔。此指令會呼叫 Docker CLI。如需相關資訊，請參閱 Docker 說明中的 [build ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/build/){: new_window} 指令。

```
bluemix ic build -t TAG|--tag TAG [--no-cache] [-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：
   <dl>
   <dt>-t <i>TAG</i>|--tag <i>TAG</i>（必要）</dt>
   <dd>要套用至所建立映像檔的儲存庫名稱。</dd>
   <dt>--no-cache（選用）</dt>
   <dd>建置映像檔時不要使用快取。預設值為 <i>false</i>。</dd>
   <dt>--pull（選用）</dt>
   <dd>嘗試從登錄中取回基礎映像檔，即使已快取也一樣。</dd>
   <dt>-q|--quiet（選用）</dt>
   <dd>抑制容器所產生的詳細輸出。預設值為 <i>false</i>。</dd>
   <dt><i>DOCKERFILE_LOCATION</i>（必要）</dt>
   <dd>本端主機上 Dockerfile 及環境定義的路徑。</dd>
    </dl>

<strong>範例</strong>：

下列範例顯示建置名稱為 *myimage* 之映像檔的要求。Dockerfile 及其他要在建置中使用的構件，位於執行指令的同一目錄中。因為登錄及名稱空間隨附於映像檔名稱，所以映像檔會建置在您組織的專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中。

```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


## bluemix ic cp
{: #bluemix_ic_cp}
在容器與本端檔案系統之間複製檔案或資料夾。此指令會呼叫 Docker CLI。如需相關資訊，請參閱 Docker 說明中的 [cp ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} 指令。


## bluemix ic cpi
{: #bluemix_ic_cpi}

存取「Docker 中心」映像檔或本端登錄中的映像檔，並將映像檔複製到您的專用 {{site.data.keyword.Bluemix_notm}} 儲存庫。

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：
   <dl>
   <dt><i>SOURCE_IMAGE</i>（必要）</dt>
   <dd>來源儲存庫及映像檔名稱。</dd>
   <dt><i>DESTINATION_IMAGE</i>（必要）</dt>
   <dd>專用 {{site.data.keyword.Bluemix_notm}} 儲存庫 URL（包含名稱空間及目的地映像檔名稱）。映像檔的標記是選用性的。</dd>
   </dl>

<strong>範例</strong>：

將映像檔從來源儲存庫複製到專用儲存庫，並新增映像檔的標記：

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

將 `sinatra` 映像檔從 `training` 儲存庫複製到專用儲存庫 `registry.ng.bluemix.net/mynamespace`，並將映像檔命名為 `mysinatra`。請新增映像檔 `mysinatra` 的標記 `v1`。

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}

在容器內執行指令。如需相關資訊，請參閱 Docker 說明中的 [exec ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} 指令。

```
bluemix ic exec [-d|--detach] [-it] [-u USER|--user USER] CONTAINER [CMD]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>-d|--detach（選用）</dt>
   <dd>在背景中執行指定的指令。</dd>
   <dt>-it（選用）</dt>
   <dd>互動模式。請持續顯示標準輸入。鍵入 <i>exit</i> 以結束。</dd>
   <dt>-u <i>USER</i>|--user <i>USER</i>（選用）</dt>
   <dd>使用者名稱。</dd>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   <dt><i>CMD</i>（選用）</dt>
   <dd>要在一或數個指定容器內執行的指令。</dd>
   </dl>

<strong>範例</strong>：

以互動模式，執行 `my_container` 容器內的 `bash` 指令：

```
bluemix ic exec -it my_container bash
```

執行 `my_container` 容器內的 `date` 指令：

```
bluemix ic exec my_container date
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

建立可擴充容器群組。

```
bluemix ic group-create [--publish,-p PORT] --name GROUP_NAME [--memory,-m MEMORY_SIZE] [-n,--hostname HOSTNAME] [-d,--domain DOMAIN] [--env,-e ENV_KEY=ENV_VAL] [--env-file ENVIRO

NMENT_VARIABLE_FILE] [-P false|true] [--volume] [--min MIN_INSTANCE_COUNT] [--max MAX_INSTANCE_COUNT] [--desired DESIRED_INSTANCE_COUNT] [--anti false|true] [--auto false|true] IMAGE_NAME [CMD [CMD ...]]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：
   <dl>
    <dt><i>IMAGE_NAME</i>（必要）</dt>
   <dd>要包含在容器群組中之每個容器實例的映像檔。您可以在映像檔之後列出指令，但不能在映像檔之後放置任何選項。請在指定映像檔之前併入所有選項。<br><br>如果您使用組織專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中的映像檔，請以下列格式指定映像檔：<i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>。<br><br>如果您使用 IBM Containers 所提供的映像檔，請不要併入您組織的名稱空間。請以下列格式指定映像檔：<i>registry.ng.bluemix.net/IMAGE</i>。</dd>
   <dt>--name <i>GROUP_NAME</i>（必要）</dt>
   <dd>將名稱指派給群組。<i>-n</i> 已淘汰。<br>
   <strong>提示：</strong>容器名稱必須以字母開頭。名稱可以包含大寫字母、小寫字母、數字、句點 .、底線 _ 或連字號 -。</dd>
   <dt>-m <i>MEMORY_SIZE</i>|--memory <i>MEMORY_SIZE</i>（選用）</dt>
   <dd>將記憶體限制指派給群組 (MB)。從 CLI 建立容器群組時，每一個容器實例的預設值都是 <i>64</i> MB。從 {{site.data.keyword.Bluemix_notm}}「儀表板」建立容器群組時，每一個容器實例的預設值都是 <i>256</i> MB。接受值是 <i>64</i>、<i>256</i>、<i>512</i>、<i>1024</i> 及 <i>2048</i>。指派記憶體限制之後，即無法變更其值。</dd>
   <dt>-n <i>HOSTNAME</i>|--hostname <i>HOSTNAME</i>（選用）</dt>
   <dd>主機名稱，例如 <i>mycontainerhost</i>。主機與網域會結合，以構成完整公用路徑 URL，例如 <i>http://mycontainerhost.mybluemix.net</i>。在使用 <i>bluemix ic group-inspect</i> 指令檢閱容器群組的詳細資料時，主機與網域會一起列出，作為路徑。</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i>（選用）</dt>
   <dd>通常網域為 <i>.mybluemix.net</i>。主機與網域會結合，以構成完整公用路徑 URL，例如 <i>http://mycontainerhost.mybluemix.net</i>。在使用 <i>bluemix ic group-inspect</i> 指令檢閱容器群組的詳細資料時，主機與網域會一起列出，作為路徑。</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>|--env <i>ENV_KEY=ENV_VAL</i>（選用）</dt>
   <dd>設定環境變數。個別列出多個索引鍵。如果包含引號，請用它們括住環境變數名稱及值。例如：`-e "key1=value1" -e "key2=value2" -e "key3=value3"`。下表顯示一些您可以指定的常用環境變數：</dd>
    </dl>


|  環境變數                              |     說明                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | 將服務連結至容器。請使用 `CCS_BIND_APP` 環境變數，將應用程式連結至容器。應用程式會連結至目標服務，並作為橋接器，以容許 {{site.data.keyword.Bluemix_notm}} 將您橋接應用程式的 `VCAP_SERVICES` 資訊帶入執行中容器實例。如需建立橋接應用程式的相關資訊，請參閱[將服務連結至容器](../../../containers/container_integrations_binding.html){: new_window}。 |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | 若要將 Bluemix 服務直接連結至容器，而不使用橋接應用程式，請使用 CCS_BIND_SRV。此連結容許 Bluemix 將 VCAP_SERVICES 資訊注入執行中容器實例。若要列出多個 Bluemix 服務，請將它們併入為相同環境變數的一部分。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 新增要在容器中監視的日誌檔。包括含有日誌檔路徑的 `LOG_LOCATIONS` 環境變數。 |
{: caption="表 2. 常用環境變數" caption-side="top"}

 <dl>
   <dt>--env-file <i>ENVIRONMENT_VARIABLE_FILE</i>（選用）</dt>
   <dd> 從檔案匯入環境變數，其中 ENVFILE 是本端目錄上檔案的路徑。檔案中的每一行都代表一個 key=value 配對。</dd>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro]（選用）</dt>
   <dd>以 <i>VolumeId:ContainerPath[:ro]</i> 格式指定詳細資料，將磁區連接至容器。
   <ul>
   <li><i>VOLUME</i>：磁區 ID 或名稱。</li>
   <li><i>CONTAINER_PATH</i>：容器中磁區的絕對路徑。</li>
   <li>ro：選用。指定 <i>ro</i> 會使磁區變成唯讀，而不是預設的讀寫。</li></ul>
   </dd>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i>（選用）</dt>
   <dd>公開 HTTP 資料流量的埠。群組中的容器必須接聽 HTTP 埠。無法提出 HTTPS 要求。若為容器群組，您無法包含多個埠。<br><br>在您指定埠時，即將應用程式設為可供「{{site.data.keyword.Bluemix_notm}} 負載平衡器」或相同 {{site.data.keyword.Bluemix_notm}} 空間中嘗試連接主機的容器使用。然後，{{site.data.keyword.Bluemix_notm}} 負載平衡器或容器可以使用此埠來連接相同 {{site.data.keyword.Bluemix_notm}} 空間中的主機和應用程式。如果在 Dockerfile 中針對您要使用的映像檔指定了埠，請包含該埠。<br>
   <strong>提示</strong>：<ul>
   <li>對於 IBM 認證的 Liberty Server 映像檔或此映像檔的已修改版本，請輸入埠 9080。</li>
   <li>對於 IBM 認證的 Node.js 映像檔或此映像檔的已修改版本，請輸入埠 8000。</li>
   </ul>
   </dd>
   <dt>-P（選用）</dt>
   <dd>發佈所有埠</dd>
   <dt>--min <i>MIN_INSTANCE_COUNT</i>（選用）</dt>
   <dd>實例數下限。預設值為 1。如果設定實例數下限，則在建立容器群組之後，無法變更此值。</dd>
   <dt>--max <i>MAX_INSTANCE_COUNT</i>（選用）</dt>
   <dd>實例數上限。預設值為 2。如果設定實例數上限，則在建立容器群組之後，無法變更此值。</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i>（選用）</dt>
   <dd>您需要的實例數。預設值為 2。</dd>
   <dt>--auto（選用）</dt>
   <dd>建立容器群組並啟用自動回復後，IBM Containers 會對所指派的埠提出 HTTP 要求，以檢查每個實例的性能。<br>
如果您未在兩個後續 90 秒間隔內收到來自容器實例的回應，則會移除實例，並將其取代為新的實例。如果容器回應，則不需要採取任何動作。此處理程序會不斷地重複。在 30 分鐘時間範圍期間，如果本身為群組成員的不同容器總數等於或超出觀察到的群組大小上限的 3 倍，則會永久停用容器群組的自動回復。若要重新啟用自動回復，您必須重建容器群組。</dd>
  <dt>--anti（選用）</dt>
  <dd> 使用互斥，讓容器群組更高度可用。--anti 選項會強制將群組中的每個容器實例放在不同的實體運算節點上，這樣可減少群組中所有容器因硬體故障而損毀的機會。您可能無法搭配使用此選項與較大的群組大小，因為每一個 Bluemix 地區及組織可用來進行部署的運算節點集有限。如果您的部署失敗，請減少群組中的容器實例數，或移除 --anti 選項。</dd>
   <dt><i>CMD</i>（選用）</dt>
   <dd>傳遞給容器群組執行的指令及引數。這個指令必須是長時間執行的指令。請不要使用不會執行很久的短期指令（例如，<i>/bin/date</i>），因為短期指令可能會導致容器損毀。<br> <strong>附註：</strong> <ul>
   <li>指令及其引數必須在 <i>bluemix ic run</i> 指令行的結尾。</li>
   <li>如果指令引數包含連字號 -（如前一個範例指令中的 <i>-c</i>），則指令前面必須有兩個連字號 --。</li>
   </ul></dd>
   </dl>


<strong>範例</strong>：

使用 IBM Containers 所提供的 `registry.ng.bluemix.net/ibmnode` 映像檔來建立容器群組 `my_container_group`，然後在該容器群組上執行 `ping localhost` 長時間執行指令：

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

使用 IBM Containers 所提供的 `registry.ng.bluemix.net/ibmnode` 映像檔來建立容器群組 `my_container_group`，然後在該容器群組上執行 `tail -f /dev/null` 長時間執行指令：

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

使用 `registry.ng.bluemix.net/ibmliberty` 映像檔，以建立已啟用自動回復的可擴充群組 `mygroup`。埠是 `9080`、主機名稱是 `mycontainerhost`，而網域名稱是 `mybluemix.net`。
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty
```


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

檢視在建立容器群組時針對它所指定的詳細資訊，例如環境變數、埠或記憶體。

```
bluemix ic group-inspect CONTAINER_GROUP
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER_GROUP</i>（必要）</dt>
   <dd>容器群組 ID 或名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示檢查容器群組 `my_group` 的要求：

```
bluemix ic group-inspect my_group
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

列出所指定容器群組的實例。

```
bluemix ic group-instances CONTAINER_GROUP
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER_GROUP</i>（必要）</dt>
   <dd>容器群組 ID 或名稱。</dd>
   </dl>

<strong>範例</strong>：

列出容器群組 `my_group` 的所有實例：

```
bluemix ic group-instances my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

從空間移除容器群組。

```
bluemix ic group-remove [-f|--force] GROUP_NAME [GROUP_NAME2 [...]]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt>-f|--force（選用）</dt>
   <dd>強制移除執行中或失敗的容器。</dd>
   <dt><i>GROUP_NAME</i>（必要）</dt>
   <dd>容器群組 ID 或名稱。</dd>
   </dl>


<strong>範例</strong>：

下列範例顯示移除容器群組的要求，其中 `my_group` 是容器群組的名稱。

```
bluemix ic group-remove my_group
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

更新容器群組。


```
bluemix ic group-update [--anti] [--desired DESIRED_INSTANCE_COUNT] [-e ENV_KEY=ENV_VAL] GROUP_NAME
```

**提示：**若要更新容器群組的主機名稱或網域，請使用 `bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP`。

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：
 <dl>
   <dt>--anti（選用）</dt>
   <dd>使用互斥，讓容器群組更高度可用。--anti 選項會強制將群組中的每個容器實例放在不同的實體運算節點上，這樣可減少群組中所有容器因硬體故障而損毀的機會。您可能無法搭配使用此選項與較大的群組大小，因為每一個 Bluemix 地區及組織可用來進行部署的運算節點集有限。如果您的部署失敗，請減少群組中的容器實例數，或移除 --anti 選項。</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i>（選用）</dt>
   <dd>您需要的實例數。預設值為 <i>2</i>。</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>（選用）</dt>
   <dd>設定環境變數。個別列出多個索引鍵。如果包含引號，請用它們括住環境變數名稱及值。例如：`-e "key1=value1" -e "key2=value2" -e "key3=value3"`。</dd>
   <dt><i>GROUP_NAME</i>（必要）</dt>
   <dd>容器群組 ID 或名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示更新容器群組 `my_group` 的要求：

```
bluemix ic group-update --desired 5 my_group
```


## bluemix ic groups
{: #bluemix_ic_groups}

列出組織的專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中的容器群組。

```
bluemix ic groups [-q]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：
	<dl>
	<dt>-q（選用）</dt>
   	<dd>僅顯示群組 ID</dd>
	</dl>


## bluemix ic images
{: #bluemix_ic_images}

檢視組織專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中所有可用映像檔的清單。如需相關資訊，請參閱 Docker 說明中的 [images ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/images){: new_window} 指令。此清單包括映像檔 ID、建立日期及映像檔名稱。

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>-a|--all（選用）</dt>
   <dd>包括組織儲存庫中每個映像檔的所有映像檔層，而不只是最新層。</dd>
   <dt>-f（選用）</dt>
   <dd>依提供的條件來過濾映像檔清單。</dd>
   <dt>--no-trunc（選用）</dt>
   <dd>不要截斷輸出。</dd>
   <dt>-q|--quiet（選用）</dt>
   <dd>只顯示數值 ID。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示接收組織可用映像檔清單的要求：

```
bluemix ic images
```


## bluemix ic info
{: #bluemix_ic_info}

檢視一組資訊，說明容器雲端服務實例的狀態。這項資訊包括容器限制、容器用量、執行中的容器、記憶體限制、記憶體用量、浮動 IP 位址限制、浮動 IP 位址用量、CCS 主機 URL、登錄主機 URL 及除錯模式狀態。

```
bluemix ic info
```

<strong>必要條件</strong>：端點、登入、目標


## bluemix ic init
{: #bluemix_ic_init}

起始設定本端機器上的 containers 環境，以使用 IBM Containers 服務的完整功能。

```
bluemix ic init
```

<strong>必要條件</strong>：端點、登入、目標

**附註：**起始設定之前，請確定 PATH 環境變數中已安裝並配置 Docker CLI (Docker)。若要切換至其他地區，請使用 `bluemix region-set` 指令。

<strong>範例</strong>：

切換至 `us-south` 地區：

```
bluemix region-set us-south
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

檢視容器的相關資訊。如需相關資訊，請參閱 Docker 說明中的 [inspect ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} 指令。

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>IMAGE</i>（必要）</dt>
   <dd>指定映像檔名稱或 ID，以檢視特定映像檔的詳細資訊。</dd>
   <dt>images（必要）</dt>
   <dd>檢視儲存庫中所有映像檔的詳細資訊。</dd>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>指定容器名稱或 ID，以檢視特定容器的詳細資訊。</dd>
   </dl>

**提示：**一次只能指定 *IMAGE*、*images* 或 *CONTAINER* 其中一項。

<strong>範例</strong>：

下列範例顯示檢查名為 `proxy` 之容器的要求：

```
bluemix ic inspect proxy
```


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

將可用的浮動 IP 位址連結至容器。

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>IP_ADDRESS</i>（必要）</dt>
   <dd>要連結的 IP 位址。</dd>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>要連結的容器 ID 或名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示將 IP 位址 `192.123.12.12` 連結至容器 `proxy` 的要求：

```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

釋放容器雲端服務實例中的浮動 IP 位址。

```
bluemix ic ip-release IP_ADDRESS [IP_ADDRESS2 [...]]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>IP_ADDRESS</i>（必要）</dt>
   <dd>要釋放的 IP 位址。</dd>
   </dl>


## bluemix ic ip-request
{: #ip_request}
要求新的浮動 IP 位址。

```
bluemix ic ip-request [-q]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt>-q（選用）</dt>
   <dd>只列出 IP 位址，而不含連結至那些 IP 位址之容器的 ID。</dd>
   </dl>


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

取消浮動 IP 位址與其容器的連結。

公用 IP 位址是 IBM Containers 中的有限資源。因此，大約每週會從免費試用版使用者定期收回已配置給空間但未連結至容器的公用 IP 位址。不過，絕不會從隨收隨付制或訂閱客戶收回已解除連結的公用 IP 位址。

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>IP_ADDRESS</i>（必要）</dt>
   <dd>要取消連結的 IP 位址。</dd>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>要取消連結的容器 ID 或名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示取消 IP 位址 `192.123.12.12` 與容器 `proxy` 的連結的要求：

```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic ips
{: #bluemix_ic_ips}

列出已登入使用者的可用浮動 IP 位址。這份清單包括 IP 位址以及 IP 位址所鏈結的容器 ID。如果 IP 位址未使用，則不會顯示容器 ID。

```
bluemix ic ips [-q]
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt>-q（選用）</dt>
   <dd>只列出 IP 位址，而不含連結至那些 IP 位址之容器的 ID。</dd>
   </dl>


<strong>範例</strong>：

下列範例顯示接收組織的所有 IP 位址清單的要求。
```
bluemix ic ips -q
```


## bluemix ic kill
{: #bluemix_ic_kill}

停止容器中的執行中處理程序，而不停止容器。如需相關資訊，請參閱 Docker 說明中的 [kill ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} 指令。

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i>（選用）</dt>
   <dd>將指令傳送給正在容器中執行的處理程序。</dd>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器 ID 或名稱。</dd>
   </dl>


<strong>範例</strong>：

下列範例顯示結束 (kill) 名為 `proxy` 之容器中處理程序的要求：

```
bluemix ic kill proxy
```


## bluemix ic logs
{: #bluemix_ic_logs}

顯示執行中容器的輸出或錯誤日誌。如需相關資訊，請參閱 Docker 說明中的 [logs ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} 指令。
```
bluemix ic logs [OPTIONS] CONTAINER
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

檢視所登入組織之專用 {{site.data.keyword.Bluemix_notm}} 映像檔儲存庫的名稱。

```
bluemix ic namespace-get
```

<strong>必要條件</strong>：端點、登入、目標


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

設定所登入組織之專用 {{site.data.keyword.Bluemix_notm}} 映像檔儲存庫的名稱。

*限制*：您不能在儲存庫名稱空間名稱中使用連字號 `-`。

```
bluemix ic namespace-set NAME
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>NAME</i>（必要）</dt>
   <dd>一次性函數，可設定組織的儲存庫名稱空間（如果尚未設定的話）。在您設定名稱空間之後，請先透過 `bluemix ic init` 指令重新起始設定 IBM Containers，然後再繼續進行。</dd>
   </dl>


## bluemix ic pause
{: #pause}

暫停執行中容器內的所有處理程序。如需相關資訊，請參閱 Docker 說明中的 [pause ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} 指令。若要停止容器，請參閱 [bluemix ic unpause](#unpause) 指令。

```
bluemix ic pause CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：
   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   </dl>

<strong>回應</strong>：

- 已順利暫停容器。

- 容器雲端服務的指令失敗

 `{message}`

 其中 `{message}` 是相關的錯誤。

- 指令失敗 - 無法連接至容器雲端服務

<strong>範例</strong>：

下列範例顯示暫停名為 `proxy` 之容器的要求：

```
bluemix ic pause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

列出容器的埠對映或特定對映。此指令會覆蓋 `docker port` 指令。如需相關資訊，請參閱 Docker 說明中的 [port ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/port/){: new_window} 指令。


## bluemix ic ps
{: #bluemix_ic_ps}
檢視已登入使用者之名稱空間中的執行中容器清單。此指令預設只會顯示執行中容器。如需相關資訊，請參閱 Docker 說明中的 [ps ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} 指令。

```
bluemix ic ps [-a|--all] [--filter env=SEARCH_CRITERIA] [-s|--size] [-l NUM|--limit NUM] [-q|--quiet]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>-a|--all（選用）</dt>
   <dd>顯示所有容器（包括執行中及已停止）。</dd>
   <dt>--filter env=<i>SEARCH_CRITERIA</i>（選用）</dt>
   <dd>搜尋具有特定環境變數值的容器。您可以依照檢查容器時 CLI 回應之 Env 區段中所列出的任何環境變數索引鍵或值來過濾容器。請將 SEARCH_CRITERIA 取代為您所尋找的索引鍵或值。您的搜尋準則不需要完全相符。</dd>
   <dt>-s|--size（選用）</dt>
   <dd>列出容器的大小。</dd>
   <dt>-l <i>NUM</i>|--limit <i>NUM</i>（選用）</dt>
   <dd>列出最近建立的容器，其中 <i>NUM</i> 是您要傳回的最新建立容器數目。<br><br> 例如，如果您已依序建立容器 <i>node1</i> 到 <i>node5</i>，則 <i>bluemix ic ps --limit 2</i> 指令會傳回 node4 和 node5，因為它們是最後建立的兩個容器。</dd>
   <dt>-q|--quiet（選用）</dt>
   <dd>只顯示容器 ID。</dd>
   </dl>


<strong>範例</strong>：

下列範例顯示查看所有執行中及已停止容器的要求：

```
bluemix ic ps -a
```


## bluemix ic rename
{: #bluemix_ic_rename}
重新命名容器。如需相關資訊，請參閱 Docker 說明中的 [rename ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} 指令。

```
bluemix ic rename OLD_NAME NEW_NAME
```
<strong>必要條件</strong>：端點、登入、目標、Docker<strong>指令選項</strong>：

<dl>
   <dt><i>OLD_NAME</i>（必要）</dt>
   <dd>容器的舊名稱。</dd>
   <dt><i>NEW_NAME</i>（必要）</dt>
   <dd>容器的新名稱。</dd>
   </dl>


## bluemix ic reprovision
{: #bluemix_ic_reprovision}

在您已登入的 Bluemix 空間中，重建 IBM Containers 服務。會維護空間的原始配額。

<strong>重要事項</strong>：當您執行此指令時，此空間中您的單一容器及群組都不會移轉至重新佈建的空間，而且將會在移轉處理程序期間予以移除。

```
bluemix ic reprovision [--force|-f] [ENVIRONMENT_NAME]
```
<strong>指令選項</strong>：<dl>
   <dt>--force|-f（選用）</dt>
   <dd>強制在 Bluemix 空間中重建 IBM Containers 服務。</dd>
   <dt><i>AVAILABILITY_ZONE</i>（選用）</dt>
   <dd>在其中部署容器的 IBM Containers 可用性區域的名稱。如果未指定任何可用性區域，則會使用針對地區所設定的預設可用性區域。</dd>
   </dl>


## bluemix ic restart
{: #bluemix_ic_restart}

重新啟動容器。如需相關資訊，請參閱 Docker 說明中的 [restart ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} 指令。

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i>（選用）</dt>
   <dd>重新啟動容器之前要等待的秒數。</dd>
   </dl>


<strong>回應</strong>：

- 已順利重新啟動容器。

- 容器雲端服務的指令失敗

 `{message}`

 其中 `{message}` 是相關的錯誤。

- 指令失敗 - 無法連接至容器雲端服務

<strong>範例</strong>：

下列範例顯示重新啟動名為 `proxy` 之容器的要求：

```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

移除容器。如需相關資訊，請參閱 Docker 說明中的 [rm ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} 指令。

```
bluemix ic rm [-f|--force] CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>-f|--force（選用）</dt>
   <dd>強制移除執行中或失敗的容器。</dd>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   </dl>

<strong>回應</strong>：

- 已順利移除容器。

- 容器雲端服務的指令失敗

 `{message}`

 其中 `{message}` 是相關的錯誤。

- 指令失敗 - 無法連接至容器雲端服務。

<strong>範例</strong>：

下列範例顯示移除名為 `proxy` 之容器的要求：

```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

移除已登入使用者之名稱空間中的映像檔。如需相關資訊，請參閱 Docker 說明中的 [rmi ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} 指令。

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>-R <i>REGISTRY</i>|--registry <i>REGISTRY</i>（選用）</dt>
   <dd>變更登錄主機。預設值為使用您在 <i>bluemix ic init</i> 指令中指定的登錄。</dd>
   <dt><i>IMAGE</i>（必要）</dt>
   <dd>您要移除之映像檔的名稱。如果映像檔名稱中未指定標籤，則預設會刪除標記為 <i>latest</i> 的映像檔。</dd>
   </dl>

<strong>回應</strong>：

- 已移除：`{IMAGE}`

 其中 `{IMAGE}` 是已移除之映像檔的名稱。

- 錯誤！未指定任何登錄主機。

- 映像檔移除失敗 - 無法連接至容器雲端登錄

- 容器雲端服務的指令失敗

 `{message}`

 其中 `{message}` 是相關的錯誤。

<strong>範例</strong>：

下列範例顯示移除映像檔 `mynamespace/myimage:latest` 的要求：

```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic route-map
{: #bluemix_ic_route_map}

建立用來存取容器群組之網際網路資料流量的路徑。您可以使用此指令，建立新路徑或更新現有路徑。

```
bluemix ic route-map [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i>（選用）</dt>
   <dd>路徑的主機名稱。主機名稱是完整公用路徑 URL 的第一個部分（例如 URL <i>mycontainerhost.mybluemix.net</i> 中的 <i>mycontainerhost</i>）。</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i>（選用）</dt>
   <dd>路徑的網域名稱，即完整公用路徑 URL 的第二個部分。在大部分情況下，網域為 <i>mybluemix.net</i>。您也可以使用此參數來指定專用網域。</dd>
   <dt><i>CONTAINER_GROUP</i>（必要）</dt>
   <dd>容器群組 ID 或名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示對映稱為 `GROUP1` 之群組的路徑的要求，其中 `my_host` 是主機名稱，而 `mybluemix.net` 是網域。
```
bluemix ic route-map -n my_host -d mybluemix.net GROUP1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

建立用來存取容器群組之網際網路資料流量的路徑。您可以使用此指令，建立新路徑或更新現有路徑。

```
bluemix ic route-unmap [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i>（選用）</dt>
   <dd>路徑的主機名稱。</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i>（選用）</dt>
   <dd>路徑的網域名稱。</dd>
   <dt><i>CONTAINER_GROUP</i>（必要）</dt>
   <dd>容器群組 ID 或名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示取消對映名稱為 `GROUP1` 之群組的路徑的要求，其中 `my_host` 是主機名稱，而 `organization.com` 是網域。
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


## bluemix ic run
{: #bluemix_ic_run}

在容器雲端服務中，從映像檔名稱啟動新的容器。如需相關資訊，請參閱 Docker 說明中的 [run ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/run/){: new_window} 指令。


```
bluemix ic run [-p PORT|--publish PORT] [-P] [-m MEMORY|--memory MEMORY] [-e ENV|--env ENV] [--volume VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS] [-it] IMAGE [CMD [CMD ...]]
```
**附註：**請確定已安裝 Cloud Foundry 指令工具，而且您有 Cloud Foundry 記號。使用 `bluemix login` 和 `bluemix ic init` 成功登入時，會產生必要的記號及憑證。

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i>（選用）</dt>
   <dd>公開 HTTP 資料流量的埠。包括 Dockerfile 中針對您要使用之映像檔所指定的任何埠。您可以利用多個 <i>-p</i> 選項來包含多個埠。如果公用 IP 位址可供使用，則公開一個埠會自動將公用 IP 位址連結至容器。<br><br>如果空間中具有您要連結至容器的現有 IP 位址，您可以指定 IP 位址，而不用稍後再連結它。必須以下列格式指定 IP 位址：&lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt; <br><br>如需要求空間之 IP 位址的相關資訊，請參閱 <a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a> 指令。<br><br>在您指定埠時，即將應用程式設為可供「{{site.data.keyword.Bluemix_notm}} 負載平衡器」或相同 {{site.data.keyword.Bluemix_notm}} 空間中嘗試連接主機的容器使用。如果在 Dockerfile 中針對您要使用的映像檔指定了埠，請包含該埠。<br><br><strong>提示：</strong><ul><li>對於 IBM 認證的 Liberty Server 映像檔或此映像檔的已修改版本，請輸入埠 9080。</li><li>對於 IBM 認證的 Node.js 映像檔或此映像檔的已修改版本，請輸入埠 8000。</li></ul></dd>
   <dt>-P（選用）</dt>
   <dd>自動公開映像檔的 Dockerfile 中針對 HTTP 資料流量所指定的埠。</dd>
   <dt>-m <i>MEMORY</i>|--memory <i>MEMORY</i>（選用）</dt>
   <dd>將記憶體限制指派給群組 (MB)。從 CLI 建立容器群組時，每個容器實例的預設值都是 64 MB。從「{{site.data.keyword.Bluemix_notm}} 儀表板」建立容器群組時，每個實例的預設值都是 256 MB。接受值為 64、256、512、1024 和 2048。指派記憶體限制之後，即無法變更其值。</dd>
   <dt>-e <i>ENV</i>|--env <i>ENV</i>（選用）</dt>
   <dd>設定環境變數，其中 <i>ENV</i> 是 key=value 配對。個別列出多個索引鍵。如果您併入引號，請用它們括住環境變數名稱及值。例如：-e "key1=value1" -e "key2=value2" -e "key3=value3"。下表顯示一些您可以指定的常用環境變數：</dd>
   </dl>


|      環境變數                          |   說明                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | 將服務連結至容器。請使用 `CCS_BIND_APP` 環境變數，將應用程式連結至容器。應用程式會連結至目標服務，並作為橋接器，以容許 {{site.data.keyword.Bluemix_notm}} 將您橋接應用程式的 `VCAP_SERVICES` 資訊帶入執行中容器實例。如需建立橋接應用程式的相關資訊，請參閱[將服務連結至容器](../../../containers/container_integrations_binding.html){: new_window}。 |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | 若要將 Bluemix 服務直接連結至容器，而不使用橋接應用程式，請使用 CCS_BIND_SRV。此連結容許 Bluemix 將 VCAP_SERVICES 資訊注入執行中容器實例。若要列出多個 Bluemix 服務，請將它們併入為相同環境變數的一部分。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | 新增要在容器中監視的日誌檔。包括含有日誌檔路徑的 `LOG_LOCATIONS` 環境變數。 |
{: caption="表 3. 常用環境變數" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro]（選用）</dt>
   <dd>以 <i>VolumeId:ContainerPath[:ro]</i> 格式指定詳細資料，將磁區連接至容器。
   <ul>
   <li><i>VOLUME</i>：磁區 ID 或名稱。</li>
   <li><i>CONTAINER_PATH</i>：容器中磁區的絕對路徑。</li>
   <li>ro：選用。指定 <i>ro</i> 會使磁區變成唯讀，而不是預設的讀寫。</li></ul>
   </dd>
   <dt>-n <i>NAME</i>|--name <i>NAME</i>（必要）</dt>
   <dd>將名稱指派給容器。<br> <strong>提示：</strong>容器名稱必須以字母開頭。名稱可以包含大寫字母、小寫字母、數字、句點 .、底線 _ 或連字號 -。</dd>
   <dt>--link <i>NAME</i>:<i>ALIAS</i>（選用）</dt>
   <dd>每當您想要讓某個容器與另一個執行中的容器進行通訊時，可以使用主機名稱的別名來予以定址。</dd>
   <dt>-it（選用）</dt>
   <dd>以互動模式執行容器。建立容器之後，請持續顯示標準輸入。鍵入 <i>exit</i> 以結束。</dd>
   <dt><i>IMAGE</i>（必要）</dt>
   <dd>要併入容器中的映像檔。您可以在映像檔之後列出指令，但不能在映像檔之後放置任何選項。請在指定映像檔之前併入所有選項。請在指定映像檔之前併入所有選項。<br><br>如果您使用組織專用 {{site.data.keyword.Bluemix_notm}} 儲存庫中的映像檔，請以下列格式指定映像檔：<i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>。<br><br>如果您使用 IBM Containers 所提供的映像檔，請以下列格式指定映像檔：<i>registry.ng.bluemix.net/IMAGE</i>。</dd>
   <dt><i>CMD</i>（選用）</dt>
   <dd>傳遞給容器群組執行的指令及引數。這個指令必須是長時間執行的指令。請不要使用不會執行很久的短期指令（例如，<i>/bin/date</i>），因為短期指令可能會導致容器損毀。</dd>
   </dl>


<strong>範例</strong>：

在以 `registry.ng.bluemix.net/ibmnode` 映像檔為建置基礎的 `my_container` 容器上，執行 `sh -c "while true; do date; sleep 20; done"` 長時間執行指令。

```
bluemix ic run --name my_container registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


使用 `my_namespace/nginx` 映像檔，來建立並啟動具有 `1024` MB 記憶體限制的容器 `proxy`，其中 `my_namespace` 是與已登入使用者相關聯的名稱空間。

```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

使用 `my_namespace/blog` 映像檔來建立並啟動容器，並將認證傳遞為環境變數。`my_namespace` 是與已登入使用者相關聯的名稱空間。

```
bluemix ic run -n my_container -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/my_namespace/blog
```

使用 `my_namespace/blog` 映像檔，以在容器中新增磁區，其中 `my_namespace` 是與已登入使用者相關聯的名稱空間。

```
bluemix ic run -n my_container -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/my_namespace/blog
```


## bluemix ic service-bind
{: #bluemix_ic_service-bind}

將服務新增至執行中的容器群組。此指令僅適用於容器群組。單一容器必須在執行 bluemix ic run 指令時連結服務。

```
bluemix ic service-bind GROUP_NAME SERVICE_INSTANCE 
```
<strong>指令選項</strong>：<dl>
   <dt><i>GROUP_NAME</i>（必要）</dt>
   <dd>群組 ID 或名稱。</dd>
   <dt><i>SERVICE_INSTANCE</i>（必要）</dt>
   <dd>要新增至容器群組的服務實例名稱。</dd>
   </dl>


## bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

從執行中的容器群組移除服務。此指令僅適用於容器群組。單一容器必須移除容器，並在沒有服務的情況下建立新的容器。

```
bluemix ic service-unbind GROUP_NAME SERVICE_INSTANCE 
```
<strong>指令選項</strong>：<dl>
   <dt><i>GROUP_NAME</i>（必要）</dt>
   <dd>群組 ID 或名稱。</dd>
   <dt><i>SERVICE_INSTANCE</i>（必要）</dt>
   <dd>要新增至容器群組的服務實例名稱。</dd>
   </dl>


## bluemix ic start
{: #ic_start}
啟動已停止的容器。如需相關資訊，請參閱 Docker 說明中的 [start ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/start/){: new_window} 指令。若要停止容器，請參閱 [bluemix ic stop](#ic_stop) 指令。

```
bluemix ic start CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   </dl>


<strong>回應</strong>：

- 已順利啟動容器。

- 容器雲端服務的指令失敗

 `{message}`

 其中 `{message}` 是相關的錯誤。

- 指令失敗 - 無法連接至容器雲端服務

<strong>範例</strong>：

下列範例顯示啟動名為 `proxy` 之容器的要求。

```
bluemix ic start proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

對於一個以上的容器，檢視即時用量統計資料。使用 `CTRL+C` 以結束。如需相關資訊，請參閱 Docker 說明中的 [stats ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} 指令。

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   <dt>--no-stream（選用）</dt>
   <dd>只顯示最新結果，而不包含它之前的任何資訊。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示最新容器統計資料的要求：

```
bluemix ic stats --no-stream my_container
```


## bluemix ic stop
{: #ic_stop}
停止執行中的容器。如需相關資訊，請參閱 Docker 說明中的 [stop ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} 指令。若要啟動容器，請參閱 [bluemix ic start](#ic_start) 指令。

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i>（選用）</dt>
   <dd>結束 (kill) 容器之前要等待的秒數。</dd>
   </dl>

<strong>回應</strong>：

- 已順利停止容器。

- 容器雲端服務的指令失敗

 `{message}`

 其中 `{message}` 是相關的錯誤。

- 指令失敗 - 無法連接至容器雲端服務

<strong>範例</strong>：

下列範例顯示停止名為 `proxy` 之容器的要求。

```
bluemix ic stop proxy
```


## bluemix ic top
{: #bluemix_ic_top}

顯示正在容器中執行的處理程序。如需相關資訊，請參閱 Docker 說明中的 [top ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/top/){: new_window} 指令。

```
bluemix ic top CONTAINER [CONTAINER]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示要在稱為 `my_container` 之容器中顯示處理程序的要求。

```
bluemix ic top my_container
```


## bluemix ic unpause
{: #unpause}

取消暫停執行中容器內的所有處理程序。如需相關資訊，請參閱 Docker 說明中的 [unpause ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} 指令。若要暫停容器，請參閱 [bluemix ic pause](#pause) 指令。

```
bluemix ic unpause CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   </dl>

<strong>回應</strong>：

- 已順利取消暫停容器。

- 容器雲端服務的指令失敗

 `{message}`

 其中 `{message}` 是相關的錯誤。

- 指令失敗 - 無法連接至容器雲端服務

<strong>範例</strong>：

下列範例顯示取消暫停名為 `proxy` 之容器的要求：

```
bluemix ic unpause proxy
```


## bluemix ic unprovision
{: #bluemix_ic_unprovision}

從您已登入的 Bluemix 空間刪除 IBM Containers 服務。

<strong>注意</strong>：當您執行此指令時，會遺失您的所有單一容器及容器群組。您的空間仍可在 Bluemix 中使用。若要重新開始使用 IBM Containers，您必須執行 `bluemix ic reprovision` 來重新佈建 IBM Containers 服務。

```
bluemix ic reprovision [--force|-f] 
```
<strong>指令選項</strong>：<dl>
   <dt>--force|-f（選用）</dt>
   <dd>強制從 Bluemix 空間刪除 IBM Containers 服務。</dd>
 </dl>


## bluemix ic version
{: #bluemix_ic_version}

顯示 Docker 的版本及 IBM Containers API。

```
bluemix ic version
```

<strong>必要條件</strong>：Docker

若要查看 IBM Containers 的版本，請執行 `bluemix ic info`。如需相關資訊，請參閱 Docker 說明中的 [version ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/version/){: new_window} 指令。


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

建立磁區。

```
bluemix ic volume-create VOLUME_NAME FS_NAME
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>FS_NAME</i>（選用）</dt>
   <dd>檔案共用名稱。如果沒有檔案共用可供使用，或未指定檔案共用，則會在空間的預設檔案共用上建置磁區。</dd>
   <dt><i>VOLUME_NAME</i>（必要）</dt>
   <dd>磁區名稱。名稱可以包含小寫字母、數字、底線 _ 及連字號 -。</dd>
   </dl>


<strong>範例</strong>：

下列範例顯示建立磁區的要求。

```
bluemix ic volume-create volume_name fileshare_name
```


## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

列出檔案共用。

```
bluemix ic volume-fs
```


## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

建立檔案共用。

```
bluemix ic volume-fs-create FILE_SHARE_NAME
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>FILE_SHARE_NAME</i>（必要）</dt>
   <dd>檔案共用名稱。名稱可以包含小寫字母、數字、底線 _ 及連字號 -。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示建立檔案共用的要求。
```
bluemix ic volume-fs-create my_file_share
```


## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

列出所有檔案共用特性。

```
bluemix ic volume-fs-flavors
```

<strong>必要條件</strong>：端點、登入、目標


## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

檢查檔案共用。

```
bluemix ic volume-fs-inspect FILE_SHARE_NAME
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

  <dl>
  <dt><i>FILE_SHARE_NAME</i>（必要）</dt>
   <dd>檔案共用名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例是檢查檔案共用的要求，其中 `my_file_share` 是檔案共用的名稱。
```
bluemix ic volume-fs-inspect my_file_share
```


## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

移除檔案共用。

```
bluemix ic volume-fs-remove FILE_SHARE_NAME
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>FILE_SHARE_NAME</i>（必要）</dt>
   <dd>檔案共用名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示移除檔案共用的要求，其中 `my_file_share` 是檔案共用的名稱。
```
bluemix ic volume-fs-remove my_file_share
```


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

檢查磁區。

```
bluemix ic volume-inspect VOLUME_NAME
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>VOLUME_NAME</i>（必要）</dt>
   <dd>磁區名稱。</dd>
   </dl>

<strong>範例</strong>：

下列範例是檢查磁區的要求，其中 `volume_name` 是磁區的名稱。

```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

移除磁區。

```
bluemix ic volume-remove VOLUME_NAME
```

<strong>必要條件</strong>：端點、登入、目標

<strong>指令選項</strong>：

   <dl>
   <dt><i>VOLUME_NAME</i>（必要）</dt>
   <dd>磁區名稱。</dd>
    </dl>

<strong>範例</strong>：

下列範例顯示移除磁區的要求，其中 `volume_name` 是磁區的名稱。

```
bluemix ic volume-remove volume_name
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

列出磁區。

```
bluemix ic volumes
```

<strong>必要條件</strong>：端點、登入、目標


## bluemix ic wait
{: #bluemix_ic_wait}

結束容器，並顯示結束碼作為確認。如需相關資訊，請參閱 Docker 說明中的 [wait ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} 指令。

```
bluemix ic wait CONTAINER [CONTAINER]
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示結束稱為 `my_container` 之容器的要求：

```
bluemix ic wait my_container
```


## bluemix ic wait-status
{: #bluemix_ic_wait_status}

等待單一容器或容器群組達到非暫時性狀態。在此等待時間，您的指令行不會返回，因此您無法輸入指令。只要容器達到非暫時性狀態，就會顯示 OK 訊息。若為單一容器，非暫時性狀態包括 Running、Shutdown、Crashed、Paused 或 Suspended。若為容器群組，非暫時性狀態包括 CREATE_COMPLETE、UPDATE_COMPLETE 或 FAILED

```
bluemix ic wait-status CONTAINER
```

<strong>必要條件</strong>：端點、登入、目標、Docker

<strong>指令選項</strong>：

   <dl>
   <dt><i>CONTAINER</i>（必要）</dt>
   <dd>容器名稱或 ID。</dd>
   </dl>

<strong>範例</strong>：

下列範例顯示結束稱為 `my_container` 之容器的要求：

```
bluemix ic wait my_container
```
