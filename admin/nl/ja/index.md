{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

#{{site.data.keyword.Bluemix_notm}} の管理
{: #administer}
*最終更新日: 2015 年 11 月 18 日*

**「アカウントおよびサポート」** &gt; **「組織の管理」**をクリックして、組織、スペース、および割り当てられたユーザーを管理します。{{site.data.keyword.Bluemix_notm}} Local ユーザーまたは {{site.data.keyword.Bluemix_notm}} Dedicated ユーザーの場合、ローカル・インスタンスおよび専用インスタンスの管理に関する詳細について、[{{site.data.keyword.Bluemix_notm}} Local および {{site.data.keyword.Bluemix_notm}} Dedicated の管理](index.html#mng)を参照してください。
{:shortdesc}

##アカウントの管理
{: #mngacct}

{{site.data.keyword.Bluemix}} では、ユーザー・インターフェースのダッシュボードから、ユーザーのアクセス権限を含め、組織およびスペースをすべて管理できます。また、使用量と請求をモニターすることもできます。{:shortdesc}

###組織およびスペース
{: #orgsandspaces}

組織管理者またはアカウント所有者は、「組織の管理」ページを使用して、ユーザーのアクセス権限など、組織またはスペースの設定を表示および管理することができます。「組織の管理」ページを開くには、メニューで*「アカウントおよびサポート」* &gt; **「組織の管理」**と進みます。

####組織

組織は以下の項目によって定義されます。


<dl>
<dt>users</dt>
<dd>組織とスペースの基本的なアクセス権限を付与された役割です。
組織内のスペースに対するその他のアクセス権を付与されるためには、
ユーザーは組織に割り当てられる必要があります。詳しくは、『[ユーザーと役割 (Users
and roles)](index.html#userroles)』を参照してください。</dd>
<dt>ドメイン</dt>
<dd>組織に割り振られるインターネットへの経路を提供します。
経路にはサブドメインとドメインがあります。サブドメインは通常アプリケーション名です。
ドメインは、システム・ドメインであるか、または、アプリケーション用に登録したカスタム・ドメインである場合があります。<br/>
<p>**注**: カスタム・ドメインを追加する場合、そのカスタム・ドメインが {{site.data.keyword.Bluemix_notm}} システム・ドメインを指すように解決されるよう、DNS サーバーを構成する必要があります。この方法では、{{site.data.keyword.Bluemix_notm}}
はカスタム・ドメインの要求を受け取ると、ご使用のアプリケーションに適切に経路指定することができます。
</p></dd>
<dt>割り当て量</dt>
<dd>組織による使用に割り振ることが可能なサービス数およびメモリー容量を含む、組織のリソース限度を示します。割り当て量は、組織の作成時に割り当てられます。組織のスペースにおけるアプリケーションまたはサービスはすべて、
割り当て量の使用に寄与します。従量課金 (PAYG) プランまたはサブスクリプション・プランの場合、組織変更による必要に応じて、Cloud Foundry のアプリケーションおよびコンテナーの割り当て量を調整できます。</dd>
</dl>

{{site.data.keyword.Bluemix_notm}} では、
組織を使用してユーザー間のコラボレーションを可能にし、以下の方法で
プロジェクト・リソースの論理的なグループ化を容易にすることができます。

<ul>
<li>スペース、アプリケーション、サービス、ドメイン、経路、およびユーザーのセットを一緒にして
組織内でグループ化できます。</li>
<li>スペースおよび組織へのアクセス権限を、ユーザー・ベースで管理することができます。</li>
</ul>

組織を作成する際は、
組織名は {{site.data.keyword.Bluemix_notm}} で固有にする必要があります。
組織を作成したユーザーには、自動的に*組織管理者*権限が割り当てられ、組織名の編集、組織の削除、組織内のスペースの作成が可能になります。

組織を削除すると、組織内のすべてのスペース、アプリケーション、およびサービスが削除されます。


{{site.data.keyword.Bluemix_notm}}
は、組織内および組織のスペース内にユーザーを割り当てることで、プロジェクト間のコラボレーションを
可能にします。**「ユーザー」**タブを使用して、組織のユーザーを表示および管理できます。
**「ユーザー」**タブの**「新規ユーザーの招待」**リンクをクリックすることによって、組織にユーザーを招待することもできます。以下の権限を組織内のユーザーに割り当てることができます。


<ul>
<li>組織ユーザー</li>
<li>組織管理者</li>
<li>組織請求管理者</li>
<li>組織監査員</li>
</ul>

####スペース

組織内でスペースを使用して、
アプリケーション、サービス、およびユーザーのセットをグループ化することができます。


ユーザーを組織に追加した後、そのユーザーに組織内のスペースへのアクセス権を付与することができます。
組織と同様に、スペースにもユーザーに割り当てることができるアクセス権のセットがあります。


<ul>
<li>スペース管理者</li>
<li>スペース開発者</li>
<li>スペース監査員</li>
</ul>

**注**: ユーザーには、スペース内で少なくとも 1 つのアクセス権が割り当てられていなければなりません。

スペースの**「ドメイン」**タブは、
スペースに割り当てられたドメインの読み取り専用リストです。
システム・ドメインはスペースで常に使用可能で、カスタム・ドメインもまたスペースに割り振ることができます。
スペースで作成されたアプリケーションは、
リストされたスペース用のドメインのいずれかを使用することができます。

###ユーザーと役割
{: #userroles}

アカウント所有者は、組織およびスペースですべての操作を実行します。


####ユーザーのタイプ

ユーザーはアカウントのメンバーまたはコラボレーターになることができます。

<dl>
<dt>メンバー</dt>
<dd>ユーザーが自分で {{site.data.keyword.Bluemix_notm}} アカウントを作成した場合、またはアカウントへの招待を受けて、{{site.data.keyword.Bluemix_notm}} での最初の体験としてその招待から登録した場合、そのユーザーはそのアカウントのメンバーです。</dd>
<dt>コラボレーター</dt>
<dd>ユーザーが以前に別のアカウントで {{site.data.keyword.Bluemix_notm}} を使用したことがあり、その後このアカウントに招待されてそれを受け入れた場合、そのユーザーは {{site.data.keyword.Bluemix_notm}} アカウントのコラボレーターです。</dd>
</dl>

####ユーザー役割

ユーザーは、以下のアクセス権を割り当てられ、組織またはスペースにおいてさまざまなユーザー役割を担うことができます。

<dl>
<dt>組織管理者</dt>
<dd>組織管理者は以下のアクセス権限を所有します。<ul>
<li>組織内のスペースの作成、削除。</li>
<li>そのユーザーが組織のメンバーまたはアカウント所有者でもある場合、組織にユーザーを招待します。</li>
<li>既に組織内に存在する既存ユーザーを管理します。</li>
<li>組織のドメインの管理。</li>
</ul>
<p>**注**: ユーザー・タイプがコラボレーターであり、以前に別のアカウントで {{site.data.keyword.Bluemix_notm}} を使用したことがあるユーザーは、組織管理者役割が割り当てられていても、組織にユーザーを招待することはできません。ユーザーを招待するには、ユーザー・タイプがメンバーでなければなりません。この問題に対処する方法については、『<a href="../troubleshoot/accessing.html#tr_adduser">ユーザーを組織に追加できない</a>』を参照してください。</p>
</dd>
<dt>請求管理者</dt>
<dd>請求管理者は、組織のランタイム情報およびサービス使用量情報を表示するアクセス権限を所有します。</dd>
<dt>組織監査員</dt>
<dd>組織監査員は、スペースのアプリケーションおよびサービス・コンテンツを表示するアクセス権限を所有します。</dd>
<dt>スペース管理者</dt>
<dd>スペース管理者は以下のアクセス権限を所有します。<ul>
<li>ユーザーをスペースに追加して、ユーザーを管理します。</li>
<li>スペースに対してフィーチャーを使用可能にします。</li>
</ul>
</dd>
<dt>スペース開発者</dt>
<dd>スペース開発者は以下のアクセス権限を所有します。<ul>
<li>スペース内でアプリケーションおよびサービスを作成、削除、および管理します。
</li>
<li>スペース内でログへのアクセス権限を所有します。</li>
</ul>
</dd>
<dt>スペース監査員</dt>
<dd>スペース監査員は、アプリケーションおよびサービス、設定、レポート、ログの各情報など、
スペースに関するすべての情報に対して読み取り専用アクセス権限を所有します。</dd>
</dl>

###組織の管理
{: #orgmng}

組織管理者またはアカウント所有者は、自身の組織を管理することができます。管理タスクには、組織の作成、組織の名前変更、スペースの作成、スペースへのユーザーの招待、既存の組織の削除が含まれます。

<ul>
<li>組織の作成<p>支払アカウントを保有するユーザーのみが組織を作成することができます。支払アカウントを保有している場合は、以下の手順を実行して組織を作成できます。</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} ダッシュボードに移動し、右上にあるアイコンをクリックし、**「組織の管理」**を選択します。</li>
<li>**「組織の作成」**をクリックし、プロンプトに従って組織を作成します。</li>
</ol>
</li>
<li>組織の名前変更<p>組織を名前変更するには、以下の手順を実行します。</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} ダッシュボードに移動し、右上にあるアイコンをクリックし、**「組織の管理」**を選択します。</li>
<li>名前変更する組織を選択します。</li>
<li>**「組織」**フィールドに新しい名前を入力し、**「保存」**をクリックします。</li>
</ol>
</li>
<li>メンバーのリスト<p>組織またはスペースのメンバーをリストするには、以下の手順を実行します。
</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} ダッシュボードに移動し、右上にあるアイコンをクリックし、**「組織の管理」**を選択します。**「ユーザー」**タブで組織のメンバーとメンバーの役割を確認できます。
</li>
<li>組織内のスペース名をクリックして、このスペースのメンバーとメンバーの役割を確認します。
</li>
</ol>
</li>
<li>スペースの作成<p>組織内にスペースを作成できます。例えば、開発環境として *dev* スペース、テスト環境として *test* スペース、実稼働環境として *production* スペースを作成できます。その後、アプリをスペースに関連付けることができます。スペースを作成するには、以下の手順を実行します。</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} ダッシュボードに移動し、右上にあるアイコンをクリックし、**「組織の管理」**を選択します。</li>
<li>組織名の下にある**「スペースの作成」**をクリックし、プロンプトに従ってスペースを作成します。</li>
</ol>
</li>
<li>スペースへのユーザーの招待<p>ユーザーをコラボレーターとして組織に招待することができます。また、組織のユーザーを個別のスペースに追加することもできます。ユーザーは、自身が追加されたスペースにのみアクセスできます。ユーザーをスペースに追加するには、以下の手順を実行します。</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} ダッシュボードに移動し、右上にあるアイコンをクリックし、**「組織の管理」**を選択します。その後、組織内の**「ユーザーの追加」**をクリックして、プロンプトに従ってユーザーを組織に追加します。</li>
<li>ユーザーをスペースに追加します。左側のナビゲーション・ペインでスペースを選択し、**「ユーザーの追加」**をクリックして、プロンプトに従ってユーザーをスペースに追加します。</li>
</ol>
</li>
<li>既存の組織の削除<p>組織を削除するには、{{site.data.keyword.Bluemix_notm}} の登録および ID サポートに連絡します。</p>
<p>**注**: 削除操作は元に戻せません。組織を削除すると、その組織に関連付けられたすべてのアプリケーションとサービスが失われます。</p>
</li>
</ul>

## {{site.data.keyword.Bluemix_notm}} Local および {{site.data.keyword.Bluemix_notm}} Dedicated の管理
{: #mng}

{{site.data.keyword.Bluemix}} Local または Dedicated 環境でのリソースの管理、使用量のモニター、ユーザー許可の管理、およびセキュリティー・レポート、ログ、状況、アップグレード通知の表示には、管理コンソールを使用します。
{:shortdesc}

### 管理コンソールへのアクセス
{: #oc_access}

URL 

`https://opsconsole.&lt;subdomain&gt;.bluemix.net/` を入力して、管理コンソールにアクセスできます。

<dl>
<dt><strong>&lt;subdomain&gt;</strong></dt>
<dd>この値は、ローカル・インスタンスまたは専用インスタンスの名前です。{{site.data.keyword.Bluemix}} インスタンスのサブドメイン名はオンボード時に割り当てられています。</dd>
</dl>

### システム情報の表示
{: #oc_system}

管理コンソールを使用してシステム情報をモニターします。

システム情報を表示するには、**「管理」&gt;「システム情報 (SYSTEM INFORMATION)」** をクリックします。

保留中の更新、全般的なシステム情報、および LDAP 構成の詳細に関する様々なセクションを展開して表示することができます。

* 「更新 (Updates)」セクションでは、お客様の側でのアクションが求められる保留中の更新をすべて表示できます。スケジュールに入っている更新をカレンダー・リンクを使用してカレンダー・アプリにインポートすれば、更新のトラッキングも簡単にできます。

<ol>
<li>特定の更新に対してアクションを起こすには、以下のステップを実行します。
<ol type="a">
<li><strong>「<em>Number</em> 件の更新が保留中 (Number updates pending)」</strong>をクリックして、保留中の更新をすべて表示します。</li>
<li>アクションを起こすべき更新を選択するか、または更新の詳細 (更新期間、予定日、中断状況など) を表示します。</li>
<li><strong>「利用不能日の設定 (SET UNAVAILABLE DATES)」</strong>をクリックして、更新期間の内、更新の適用には不適当な特定の日を設定します。利用不能日を設定すると、IBM はお客様の選択内容に基づいて更新を承認し、スケジュールに入れます。更新が承認されてスケジュールに入ると、通知が届きます。</li>
<li>利用不能日がなければ、<strong>承認 (APPROVE)</strong>をクリックして更新を承認します。承認すると、スケジュールに入っている更新期間中に更新が適用されます。IBM からは、更新のデプロイメントの開始時と終了時に通知が送信されます。</li>
</ol>
</li>
<li>スケジュールに入っている更新を自分が選んだカレンダー・アプリにインポートするには、以下のステップを実行します。
<ol type="a">
<li>カレンダー・アプリを開きます。</li>
<li>「システム情報 (System Information)」ページにリストされている**「カレンダー URL (Calendar URL)」**をご使用のアプリに貼り付けて、更新カレンダーをインポートします。または、「カレンダー URL (Calendar URL)」をクリックしてカレンダー・ファイルをダウンロードし、次に、`.ics` ファイルを使用してカレンダー・ファイルをカレンダー・アプリにインポートします。</li>
<li>資格情報を入力します。</li>
<li>スケジュールに入っている更新を表示します。</li>
</ol>
</li>
</ol>

* 「一般情報 (General Information)」セクションでは、以下の情報を表示できます。
    * {{site.data.keyword.Bluemix_notm}} ビルドに関する基本情報。
    * バージョン、URL、地域、および CLI 資料へのリンクが含まれた API 情報。
    * システムおよびサービスに関する共有ドメイン情報。
    * アプリケーション、ユーザー、および組織の総数に関する統計。
* 「LDAP 構成の詳細 (LDAP Configuration Details)」セクションでは、LDAP サーバーを選択し、ユーザーとグループのマッピング情報を表示できます。{{site.data.keyword.IBM}} WebID を使用している場合、その ID は、「LDAP 構成の詳細 (LDAP Configuration Details)」セクションに示されます。

### 使用量情報の表示
{: #oc_resource}

管理コンソールを使用して、リソースやネットワークの使用量をモニターします。

リソース情報を表示するには、**「管理」&gt;「使用量」**をクリックします。

「リソース・モニタリング (Resource Monitoring)」セクションでは、以下の情報を表示できます。

* リソース使用率情報 (何 GB のメモリー、何 GB のディスク・スペースが使用されているか、など)。すべてのドロップレット実行エージェント (DEA) での平均 CPU 使用量を表示することができます。**「CPU」**タイルをクリックすることで、各 DEA の CPU 使用量を表示できます。使用量が最も大きい DEA が先頭にリストされます。各 DEA は、ジョブと IP アドレスによって識別されます。CPU 使用量は、システム・プロセスで使用された CPU 量、ユーザー・プロセスで使用された CPU 量、および待機プロセスで使用された CPU 量の 3 つのカテゴリーに分かれています。
* 入力帯域幅および出力帯域幅のネットワーク使用率情報 (過去 1 日、1 週間、または 1 カ月)。
表示されるデータは、パブリック・ネットワークとプライベート・ネットワークの両方の入出力トラフィックの合計に基づいています。
* {{site.data.keyword.Bluemix_notm}} の平均応答時間 (過去 10 分、1 時間、および 1 日)。
* {{site.data.keyword.Bluemix_notm}} の 1 秒あたりの平均トランザクション数 (過去 10 分、1 時間、および 1 日)。

### レポートの表示
{: #oc_report}

ご使用の {{site.data.keyword.Bluemix_notm}} インスタンスに関して、セキュリティー・レポートやログ (DataPower&trade;、ファイアウォール、およびログイン監査など) を表示できます。

レポートやログを表示するには、**「管理」&gt;「レポートおよびログ (REPORTS AND LOGS)」**をクリックします。

以下のオプションから選択します。

* フィールドから開始日および終了日を選択して、表示するレポートとログをフィルタリングできます。

* 左ナビゲーション・ペインから各種レポートを展開および表示できます。
* レポートおよびログのコレクション内で検索できます。検索は、レポート名に加え、レポートおよびログ内に含まれているテキスト・コンテンツにも適用されます。**「管理イベント (Administration Events)」**、**「DataPower レポート (DataPower Reports)」**、**「ファイアウォール (Firewall)」**、および**「ログイン監査 (Login Audit)」**によって検索をフィルターに掛けることもできます。
* レポートまたはログを表示した場合、レポートの右上にある ![ダウンロード](images/icon_download.png) アイコンをクリックすると、対象をダウンロードできます。

### 状況の表示
{: #oc_status}

管理コンソールを通して、ご使用の {{site.data.keyword.Bluemix_notm}} インスタンスに関する状況をモニターできます。通知を調べずに済むように、通知の RSS フィードをサブスクライブすることもできます。

ご使用の {{site.data.keyword.Bluemix_notm}} インスタンスの状況を表示するには、以下のステップを実行します。

1. 管理コンソールの右上隅にある**「プロファイル設定」**アイコンをクリックします。

2. 次に、**「状況」**をクリックします。

「システム状況」ページが表示されます。左ペインに、各地域のランタイムとサービスおよびご使用の {{site.data.keyword.Bluemix_notm}} インスタンスの状況が表示されます。右ペインに通知が表示されます。

3. RSS フィード用にブラウザーを構成している場合、通知の RSS フィードをサブスクライブできます。
通知リストの左上にある**「更新情報 (UPDATES)」**の右側に ![RSS](images/icon_RSS.png) アイコンがあることを確認し、次のいずれかのアクションを選択します。

* ![RSS](images/icon_RSS.png) アイコンを、ご使用の RSS リーダーにドラッグします。
* RSS アイコンを右クリックし、**「リンク・アドレスのコピー (Copy link address)」**を選択し、URL を RSS リーダーに貼り付けます。


4. 表示する通知をフィルターに掛けます。通知リストの右上にある**「フィルター」**をクリックします。次に、通知に含まれていると思われる単語 (例えば、「保守」) を入力して、通知のリストを検索して絞り込むことができます。あるいは、**「タイプ」**、**「地域」**、**「カテゴリー」**、**「開始日」**、または**「終了日」**によって表示する通知をクリックして選択できます。

### カタログの管理
{: #oc_catalog}

{{site.data.keyword.Bluemix_notm}} カタログで、どの {{site.data.keyword.Bluemix_notm}} サービスおよびスターターをユーザーに表示するかを管理することができます。

管理コンソールを使用してカタログを管理するには、**「管理」&gt;「カタログ管理 (CATALOG MANAGEMENT)」**をクリックします。

サービスまたはスターターのタイルを選択して、サービスまたはスターターのプランの表示可能性を編集します。表示可能性を編集するには、以下のオプションから選択します。
* 非表示のサービスまたはスターターを表示して、「カタログ」でユーザーに表示されるようにするには、**「すべてのプランを有効化 (ENABLE ALL PLANS)」**を選択します。
* {{site.data.keyword.Bluemix_notm}} カタログで、サービスやスターターをユーザーに対して非表示にするには、**「すべてのプランを無効化 (DISABLE ALL PLANS)」**を選択します。
* 個別プランの表示可能性を制御するには、プラン名を選択してから、ドロップダウン・メニューを使用して**「すべての組織に対して有効化 (Enable for all organizations)」**、 **「すべての組織に対して無効化 (Disable for all organizations)」**、または**「特定の組織に対してプランを有効化 (Enable plan for specific organizations)」**を選択します。

### 組織の管理
{: #oc_organizations}

組織の作成と削除、組織へのマネージャーの追加、および割り当て量の使用量のモニターを行うことで、組織を管理できます。

管理コンソールを使用して組織を管理するには、**「管理」&gt;「組織管理 (ORGANIZATION ADMINISTRATION)」**をクリックします。

さまざまなセクションを展開および表示できます。組織の割り当て量プランを確認および管理することもできます。

* 新規組織を作成し、マネージャーを追加するには、<strong>「組織の作成」</strong>をクリックします。組織の名前を入力し、次に、マネージャーとして追加する個人の名前または E メールを入力します。複数の名前を入力および選択することで、複数のマネージャーを追加できます。<strong>「組織の作成」</strong>をクリックし、変更を保存して組織を作成します。
* 「割り当て量のモニター (Quota Monitoring)」セクションでは、セクションを展開して、以下の情報を表示できます。
    * 環境メモリー使用量。このセクションでは、完全なシステム環境のメモリー使用量が詳細に示されます。
グラフで、使用中システム・メモリー、合計システム・メモリー、使用済みの割り当て量、および割り振られている合計割り当て量を含む情報が示されます。以下の用語リストで、グラフに表示されるメモリー使用量のタイプを定義します。
	<dl>
	<dt><strong>使用中システム・メモリー (Used system memory)</strong></dt>
	<dd>環境で使用されている物理メモリー。</dd>
	<dt><strong>合計システム・メモリー (Total system memory)</strong></dt>
	<dd>環境で使用可能な合計物理メモリー。</dd>
	<dt><strong>デプロイ済み割り当て量 (Quota deployed)</strong></dt>
	<dd>すべての組織でデプロイされているすべてのアプリ用に割り振られているメモリーの合計。デプロイ済み割り当て量の合計は、環境の物理的な合計システム・メモリーを超過する可能性があります。例えば、合計システム・メモリーが 16 GB で、合計 5 個の異なる組織にそれぞれ 4 GB のメモリーを割り振った場合、合計割り当て量は、すべての組織についてお客様に割り振られている合計システム・メモリーを超過しています。ただし、多くの場合、各組織に個別に割り振られている合計割り当て量を各組織が使用していないことが考えられます。また、すべての組織が、それぞれに割り振られている合計メモリー割り当て量を同時に使用しないことが考えられます。</dd>
	<dt><strong>合計割り当て量 (Total quota)</strong></dt>
	<dd>すべての組織に割り振られている合計メモリー。</dd>
	</dl>
	* 組織のメモリー使用量。このセクションでは、組織レベルでのメモリー使用量の詳細が示されます。合計割り当て量、および各組織にデプロイされている割り当て量を表示できます。グラフで、組織別の最も大きいメモリー使用量をリストした情報が示されます。デフォルトでは、使用メモリー量が最大の組織がリストの先頭になります。**「最大メモリー使用量 (Highest Memory Usage)」**および**「過剰メモリー割り振り (Excess Memory Allocation)」**を基準としてソートできます。
	<dl>
	<dt><strong>最大メモリー使用量 (Highest Memory Usage)</strong></dt>
	<dd>このオプションは、最大メモリー量を使用している組織を特定するために使用します。使用メモリー量が最も多い組織を特定するため、最大メモリー使用量を基準としてソートします。リストは、デプロイ済み割り当て量によってソートされます。</dd>
	<dt><strong>過剰メモリー割り振り (Excess Memory Allocation)</strong></dt>
	<dd>このオプションは、必要より大きい割り当て量プランが設定されている組織を識別する場合に使用します。
	過剰メモリー使用量を基準としてソートすることで、当該組織に割り振られている割り当て量に対して使用メモリー量が最小の組織を識別します。</dd>
	</dl>
* 組織の割り当て量プランを変更するには、「組織メモリー使用量 (Organization memory usage)」セクションで、編集する組織のグラフ内のバーをクリックするか、「組織リスト (Organization List)」セクションで組織の名前を選択します。「組織の編集」ページでは、割り当て量プランの変更、組織の名前の変更、およびマネージャーの追加/削除を行うことができます。組織の現行使用量では不十分な割り当てプランを選択した場合、メッセージを受け取ります。「組織の編集」ページで行った変更を保存するには、**「保存」**をクリックします。
* 「組織リスト (Organization List)」セクションでは、 {{site.data.keyword.Bluemix_notm}} 環境内のすべての組織を表示できます。
	* 組織を削除するには、「アクション」列の![削除](images/icon_trash.png)をクリックします。
	* 組織の割り当て量プランを表示および編集するには、リスト内の組織の名前をクリックします。
	* 組織の名前の編集およびマネージャーの追加/削除を行うには、リスト内の組織の名前をクリックします。

### ユーザーおよび許可の管理
{: #oc_useradmin}
LDAP を使用し、自社のユーザー・レジストリーからご使用の {{site.data.keyword.Bluemix_notm}} インスタンスにユーザーを追加できます。ユーザーは、個別またはグループで追加できます。また、ユーザー許可を表示できます。`admin` 許可が割り当てられている場合、他のユーザーの許可を設定および管理することもできます。

管理コンソールを使用してユーザーを管理するには、**「管理」&gt;「ユーザー管理 (USER ADMINISTRATION)」**をクリックします。

「ユーザー管理 (User Administration)」ページに、ローカル・インスタンスまたは専用インスタンスのユーザーが全員表示されます。
各ユーザーの許可が表示されます。許可は、None、`Admin`、`Catalog`、`Login`、`Reports`、および `Users` のいずれかになります。許可を有効にするか、または目的の許可について `view` 権限または `write` 権限をユーザーに与えることができます。許可および権限はアイコンで示されます。アイコンの各タイプと説明については、『[許可](#permissions)』を参照してください。

以下のオプションから選択します。
* ユーザーを検索します。上部にある**「検索」**フィールドを使用して、表内のユーザーを検索できます。
* ユーザーを追加します。`admin` 許可、または `write` 権限がある `users` 許可を持っている場合、ユーザーを追加することができます。ユーザーまたはユーザーのグループを追加するには、**「単一ユーザーの追加 (ADD SINGLE USER)」**または**「ユーザー・グループの追加 (ADD USER GROUP)」**をクリックします。**「検索」**フィールドに、検索対象のユーザー名またはグループ名を入力し、**「組織 (Org)」**リストからユーザーまたはユーザー・グループの追加先となる組織を選択します。追加するユーザーまたはグループが見つかったら、ユーザー名をクリックしてから、**「単一ユーザーの追加 (ADD USER)」**または**「複数ユーザーの追加 (ADD USERS)」**をクリックして追加します。50 人を超えるユーザーのグループは、バックグラウンド・バッチ・ジョブを介して追加されます。追加操作が成功すると、ユーザーまたはグループが表に追加され、表示および検索できるようになります。追加されたユーザーには、許可は割り当てられていません。
* 許可および組織を編集します。`admin` 許可を持っている場合、他のユーザーの許可および組織を編集することができます。許可を編集するには、ユーザーを特定し、ユーザー名をクリックします。許可を有効または無効にするには、開いたウィンドウに含まれている、以下のオプションから選択します。
	* 許可を有効にするには、リストから**「オン (On)」**を選択します。
	* リストから**「読み取り (Read)」**を選択して、ユーザーにその許可について `view` (read-only) 権限を持たせるか、**「書き込み (Write)」**を選択して、その許可について `write` (edit、add、remove) 権限を持たせます。
	* 許可を無効にするには、**「オフ (Off)」**を選択します。組織を編集するには、以下のオプションから選択します。
	* 検索フィールドを使用して組織を特定し、クリックしてオプションから選択し、**「追加」**をクリックして、ユーザーを組織に追加します。
	* ![削除。負符号で示されている](images/icon_remove.png) アイコンをクリックして、組織からユーザーを削除します。終了したら、**「保存」**をクリックします。
* ユーザーを削除します。`admin` 許可、または `write` 権限がある `users` 許可を持っている場合、ユーザーを削除することができます。ユーザーを削除するには、そのユーザーを検索し、![「削除」](images/icon_trash.png)アイコンをクリックし、次に**「削除」**をクリックします。

#### 許可
{: #permissions}

ユーザーには、以下の許可を割り当てることができます。

| **ユーザー許可** | **説明** |
|-----------------|-------------------|
| admin | `admin` 許可を備えているユーザーは、他のユーザーの許可を編集できます。 |
| catalog | `catalog` 許可を持つユーザーには、ローカル・インスタンスまたは専用インスタンスで利用できるサービスを `view` または `write` (modify) する権限を割り当てることができます。 |
| login | `login` 許可を備えているユーザーは、管理コンソールにログインできます。この許可がない場合、ユーザーはログインできません。 |
| reports | `reports` 許可を持つユーザーには、セキュリティー・レポートを `view` または `write` (modify) する権限を割り当てることができます。 |
| users | `users` 許可を持つユーザーには、ユーザー・リストを `view` する権限、またはユーザーを `write` (add または remove) する権限を割り当てることができます。この許可では、他のユーザーの許可を設定することはできません。|

*表 1. 許可*

許可を有効にするか、または目的の許可について `view` 権限または `write` 権限をユーザーに与えることができます。許可および権限は次のアイコンで示されます。

* ![有効。チェック・マークで示されている](images/icon_enabled.png) アイコン (許可の横) は、その許可が有効になっていることを示しています。
* ![表示。目で示されている](images/icon_read.png) アイコンは、そのユーザーに、その許可について `view` (read-only) 権限があることを示しています。

* ![書き込み。鉛筆で示されている](images/icon_write.png) アイコンは、そのユーザーに、その許可について `write` (edit、add、remove) 権限があることを示しています。


### Admin REST API を使用したユーザーの管理
{: #usingadminapi}

`Admin` REST API を使用して、{{site.data.keyword.Bluemix_notm}} インスタンスのユーザーの追加と削除を行うことができます。`Admin` REST API のエンドポイントおよび JSON のリソースは、コマンド・ラインからの基本操作を可能にするために実験に基づいて提供されています。この情報の例に含まれているエンドポイントと URL は、急な通知で変更または廃止される可能性があります。

以下のツールは、この後の例を使用するための前提条件です。他のツールを使用するという選択肢もあります。

* cURL。REST API 要求をコマンドとして入力するために必要です。cURL は、HTTP 要求をサーバーに送信し、コマンド・ライン・インターフェースを介してサーバー応答を受信するための、無料ユーティリティーです。cURL は、[cURL Download サイト](http://curl.haxx.se/download.html){: new_window}からダウンロードできます。
* Python。Python の pretty-print JSON ツールを使用するために必要です。このオプション・ツールは、JSON テキストを入力として取り、読みやすい出力を提供します。Python は、[Python Downloads サイト](https://www.python.org/downloads){: new_window}からダウンロードできます。

#### 管理コンソールへのログイン

`Admin` API 要求を実行する前に、管理コンソールにログインする必要があります。`admin` 許可、または `write` 権限のある `users` 許可を持っている場合、ユーザーを追加または削除することができます。他のユーザーの許可を編集するには、`admin` 許可を持っている必要があります。

管理コンソールにログインするには、`https://<your_host>.ibm.com/login` エンドポイントで基本アクセス認証を使用できます。サーバーは、セッションで Cookie を返します。その Cookie を、管理コンソールのすべての操作に使用します。

**注:** 数時間使用されない場合、そのセッションは無効になります。

管理コンソールにログインするには、次のコマンドを実行します。

`curl --user <user_id>:<password> -c ./cookies.txt --header "Accept: application/json" https://<your_host>.ibm.com/login | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">--user <em>user_id</em>:<em>password</em></dt>
<dd class="pd">ユーザー ID とパスワードを受け入れ、Basic 許可ヘッダーを送信します。</dd>


<dt class="pt dlterm">-c <em>filename</em></dt>
<dd class="pd">指定されたユーザー ID とパスワードを、指定されたファイルに Cookie として保管します。</dd>


<dt class="pt dlterm">--header</dt>
<dd class="pd">Accept ヘッダーを送信します。</dd>

</dl>

このコマンドの出力例を以下に示します。
```
{
    "message": "Logged in",
    "name": {
        "familyName": "*last_name*",
        "givenName": "*first_name*"
    }
}
```
{: screen}

#### 組織のリスト表示
{: #listingorg}

ユーザーを追加する場合は、組織を指定する必要があります。`Admin` REST API を使用して、すべての組織をリストすることができます。組織をリストするには、`read` 権限のある `users` 許可を持っている必要があります。組織をすべてリストするには、以下のコマンドを実行します。

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd"><samp class="ph codeph">-c</samp> オプションを使用してあらかじめファイルに保管されていたユーザー ID とパスワードを、Cookie として HTTP サーバーに渡します。</dd>

</dl>

各組織について、結果には次の情報が含まれます。
* `"guid"`、組織の GUID
* `"name"`、組織の名前

このコマンドの出力例を以下に示します。
```
{
     "resources": [
         {
             "guid": "05af098d-d476-4fb0-8b87-a84350e72af3",
             "name": "org-1"
         },
         {
             "guid": "5129a5a8-37c2-4ee4-a9b2-bebae3531db5",
             "name": "org-2"
         },

		 		 ....

		 ],
		 "total_results": 284
}
```
{: screen}

#### ユーザーのリスト表示
{: #listingusr}

`Admin` REST API を使用して、登録済みのユーザーをリストすることで、目的のユーザーが既に {{site.data.keyword.Bluemix_notm}} 環境に追加されているかどうかを確認できます。
登録済みのユーザーをリストするには、`read` 権限のある `users` 許可を持っている必要があります。ユーザーを全員リストするには、以下のコマンドを実行します。

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd"><samp class="ph codeph">-c</samp> オプションを使用してあらかじめファイルに保管されていたユーザー ID とパスワードを、Cookie として HTTP サーバーに渡します。</dd>
</dl>

登録されている各ユーザーについて、結果には次の情報が含まれます。
* `"first_name"` (名) と `"last_name"` (姓)
* `"user_id"`、ユーザー ID と E メール・アドレス
* `"guid"`、組織の GUID。
* `"permissions"`、管理コンソールのユーザーに割り当てられる。

このコマンドの出力例を以下に示します。


```
{
    "next_url": "/codi/v1/users?results_per_page=100&amp;page=2",
    "prev_url": "",
    "resources": [
        {
            "active": true,
            "created_at": "2015-04-08T17:38:51.788Z",
            "created_by": "",
            "first_name": "some first name",
            "guid": "5d5268cf-39c0-48d3-96ae-7afe928e5dd7",
            "last_name": "some last name",
            "permissions": [
                {
                    "display": "ops.admin"
},
                {
                    "display": "ops.catalog.write"
},
                {
                    "display": "ops.reports.write"
},
                {
                    "display": "ops.catalog.read"
},
                {
                    "display": "ops.users.write"
},
                {
                    "display": "ops.reports.read"
},
                {
                    "display": "ops.login"
},
                {
                    "display": "ops.users.read"
                }
            ],
            "user_id": "someid@us.ibm.com"
        },
		 		 ...


     }
    ],
    "total_pages": 395,
    "total_results": 39421
}

```
{: screen}

#### ユーザーの追加

`Admin` REST API を使用して、{{site.data.keyword.Bluemix_notm}} インスタンスにユーザーを追加できます。ユーザーを追加するには、`write` 権限のある `users` 許可を持っている必要があります。

追加するユーザーは 1 人だけでもかまわないし、ユーザーのリストを追加することもできます。ユーザーを 1 つの組織にのみ追加することもできるし、複数の組織に追加することもできます。-->ユーザーを追加するには、以下の情報を指定する必要があります。

* ユーザーのファーストネーム (名) とラストネーム (姓)。「[ユーザーのリスト表示](index.html#listingusr)」にある、`"first_name"` と `"last_name"` を指定します。
* E メール・アドレスとユーザー ID。E メール・アドレスとユーザー ID についてはどちらも、「[ユーザーのリスト表示](index.html#listingusr)」にある `"user_id"` を指定します。
* `"guid"`。「[組織のリスト表示](index.html#listingorg)」にある組織の GUID を指定します。

情報は、JSON ファイルで提供します。

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd"><samp class="ph codeph">-c</samp> オプションを使用してあらかじめファイルに保管されていたユーザー ID とパスワードを、Cookie として HTTP サーバーに渡します。</dd>
</dl>

<ol>
<li>適切な JSON 形式で情報を含む JSON ファイルを作成します。<p>例えば、以下の内容を含む、`user.json` という名前のファイルを作成します。
</p>
<code>
{
    "members": [
        {
            "emails": [
"some_user_id@domain.com"
],
            "first_name": "Some_first_name",
            "last_name": "Some_last_name",
            "user_id": "some_user_id@domain.com"
        }
    ],
    "organization_roles": [
        {
            "id": "7a891f9c-e4e7-46c7-8b4e-dffaa7eb3bcd"
        }
    ]
}
</code><br/><br/>
</li>
<li>以下のコマンドを実行して、JSON ファイルのコンテンツをユーザーのエンドポイントに投稿します:<br/><br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<your_host>.ibm.com/codi/v1/users
</code>
</li>
</ol>

<dl class="parml">

<dt class="pt dlterm">-v </dt>
<dd class="pd">詳細出力を指定します。</dd>


<dt class="pt dlterm">-X POST</dt>
<dd class="pd">デフォルトの GET 要求をオーバーライドして、POST 要求を指定します。</dd>


<dt class="pt dlterm">-H "Content-Type: application/json"</dt>
<dd class="pd">content-type ヘッダーを指定します。この場合、JSON です。</dd>


<dt class="pt dlterm">-d *data*</dt>
<dd class="pd">POST 要求で HTTP サーバーに送信するデータ (この場合、ファイル `user.json`) を指定します。</dd>

</dl>



このコマンドの出力例を以下に示します。


```
* Connected to localhost (127.0.0.1) port 3000 (#0)
 
 > POST /codi/v1/users HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 > Content-Type: application/json
 > Content-Length: 333
 >
 * upload completely sent off: 333 out of 333 bytes
 &lt; HTTP/1.1 201 Created
 &lt; x-powered-by: Express
 &lt; vary: X-HTTP-Method-Override
 &lt; content-type: application/json
 &lt; date: Wed, 22 Apr 2015 19:32:54 GMT
 &lt; connection: close
 &lt; transfer-encoding: chunked
 &lt; X-Time_Check: Proxy Time: 5612 msec
 ```
{: screen}

#### ユーザーの削除

`Admin` REST API を使用して、{{site.data.keyword.Bluemix_notm}} インスタンスからユーザーを削除できます。ユーザーを削除するには、`write` 権限のある `users` 許可を持っている必要があります。

ユーザーを削除するには、そのユーザーのユーザー ID を指定する必要があります。次のコマンドを実行します。

`curl -v -b ./cookies.txt -X DELETE https://<your_host>.ibm.com/codi/v1/users?user_id=<some_user_id@domain.com>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-X DELETE</dt>
<dd class="pd">DELETE 要求を指定します。</dd>
</dl>

このコマンドの出力例を以下に示します。


```
 * connect to ::1 port 3000 failed: Connection refused
 *   Trying 127.0.0.1...
 * Connected to localhost (127.0.0.1) port 3000 (#0)
 &gt; DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 &gt; User-Agent: curl/7.37.1
 &gt; Host: localhost:3000
 &gt; Accept: */*
 &gt; Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 &gt; 
 &lt; HTTP/1.1 201 Created
 &lt; x-powered-by: Express
 &lt; content-type: application/json
 &lt; date: Wed, 22 Apr 2015 21:01:09 GMT
 &lt; connection: close
 &lt; transfer-encoding: chunked
 &lt; X-Time_Check: Proxy Time: 1922 msec
 &lt; 
 ```
{: screen}

### CF CLI を使用したユーザーの管理
{: #usingadmincli}

Cloud Foundry コマンド・ライン・インターフェースと {{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインを使用することで、{{site.data.keyword.Bluemix_notm}} 環境のユーザーを管理できます。例えば、LDAP レジストリーからユーザーを追加できます。

最初に、CF コマンド・ライン・インターフェースをインストールします。{{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインを使用する場合、CF バージョン 6.11.2 以降が必要です。[Cloud Foundry コマンド・ライン・インターフェースのダウンロード](https://github.com/cloudfoundry/cli/releases){: new_window}

**制限:** Cloud Foundry コマンド・ライン・インターフェースは、Cygwin ではサポートされていません。Cloud Foundry コマンド・ライン・インターフェースは Cygwin コマンド・ライン・ウィンドウ以外のコマンド・ライン・ウィンドウで使用してください。

#### {{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインの追加

CF コマンド・ライン・インターフェースをインストール後、{{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインを追加できます。

以下のステップを実行して、リポジトリーを追加し、プラグインをインストールします。


<ol>
<li>{{site.data.keyword.Bluemix_notm}} 管理プラグイン・リポジトリーを追加するには、以下のコマンドを実行します:<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://opsconsole.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">ご使用の {{site.data.keyword.Bluemix_notm}} インスタンス用 URL のサブドメインです。</dd>
</dl>
</li>
<li>{{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインをインストールするには、以下のコマンドを実行します:<br/><br/> <code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

#### {{site.data.keyword.Bluemix_notm}} 管理
CLI プラグインの使用

{{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインを使用すると、ユーザーの追加と削除、組織へのユーザーの割り当てと割り当て解除、といった管理タスクを実行できます。コマンドのリストを表示するには、次のコマンドを実行します。


`cf plugins`
{: codeblock}

追加でコマンドのヘルプを表示するには、`--help` オプションを使用します。

#### {{site.data.keyword.Bluemix_notm}} への接続とログイン

管理 CLI プラグインを使用してユーザーを管理する場合、まず接続とログインを行います (まだ行っていない場合)。

<ol>
<li>{{site.data.keyword.Bluemix_notm}}> API エンドポイントに接続するには、以下のコマンドを実行します:<br/><br/> <code>
cf api https://api.&lt;subdomain&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">ご使用の {{site.data.keyword.Bluemix_notm}} インスタンス用 URL のサブドメインです。</dd>
</dl>
<p>正しい URL は、管理コンソールの「リソースおよび情報 (Resources and Information)」ページで確認できます。URL は**「API URL」**フィールドの「API 情報」セクションに表示されます。</p>
</li>
<li>以下のコマンドを使用して {{site.data.keyword.Bluemix_notm}} にログインします:<br/><br/>
<code>
cf login
</code>
</li>
</ol>

#### ユーザーの追加

LDAP レジストリーから {{site.data.keyword.Bluemix_notm}} 環境にユーザーを追加できます。次のコマンドを入力します。


`cf bluemix-admin-add-user <user_name> <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">LDAP レジストリー内のユーザーの名前。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">ユーザーの追加先となる {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
</dl>

**ヒント:** **bluemix-admin-add-user** という長いコマンド名の別名として **baau** を使用することもできます。

#### ユーザーの削除

次のコマンドを入力して、{{site.data.keyword.Bluemix_notm}} 環境からユーザーを削除できます。

`cf bluemix-admin-remove-user <user_name>`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 内のユーザーの名前。</dd>

</dl>

**ヒント:** **bluemix-admin-remove-user** という長いコマンド名の別名として **baru** を使用することもできます。

#### 組織の追加および削除

組織を追加および削除できます。

* 組織を追加するには、以下のコマンドを入力します。

`cf Bluemix-admin-create-organization <organization> <manager>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">追加先となる {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">組織のマネージャーのユーザー名。</dd>
</dl>

**ヒント:** **bluemix-admin-create-organization** という長いコマンド名の別名として **baco** を使用することもできます。

* 組織を削除するには、以下のコマンドを入力します。

`cf Bluemix-admin-delete-organization <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">削除する {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
</dl>

**ヒント:** **bluemix-admin-create-organization** という長いコマンド名の別名として **bado** を使用することもできます。

#### 組織へのユーザーの割り当て

{{site.data.keyword.Bluemix_notm}} 環境内のユーザーを特定の組織に割り当てることができます。次のコマンドを入力します。


`cf bluemix-admin-set-org <user_name> <organization> [<role>]`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 内のユーザーの名前。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">ユーザーの割り当て先となる {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} ユーザーの役割とそれぞれの説明については、[役割](#roles)を参照してください。
</dd>
</dl>

**ヒント:** **bluemix-admin-set-org** という長いコマンド名の別名として **baso** を使用することもできます。

#### 組織からのユーザーの割り当て解除

{{site.data.keyword.Bluemix_notm}} 環境内のユーザーについて、特定の組織への割り当てを解除することができます。次のコマンドを入力します。


`cf bluemix-admin-unset-org <user_name> <organization> [<role>]`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 内のユーザーの名前。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">ユーザーの割り当て先となる {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} ユーザーの役割とそれぞれの説明については、[役割](#roles)を参照してください。
</dd>
</dl>

**ヒント:** **bluemix-admin-unset-org** という長いコマンド名の別名として **bauo** を使用することもできます。

#### 役割

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">組織管理者。組織管理者には、次のアクションを行う権限があります。<ul>
<li>組織内のスペースの作成、削除。</li>
<li>組織へのユーザーの招待とユーザーの管理。</li>
<li>組織のドメインの管理。</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">請求管理者。請求管理者は、組織におけるランタイムおよびサービスの使用率情報を表示できます。
</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">組織監査員。組織監査員は、スペース内のアプリケーションとサービスの内容を表示できます。
</dd>
</dl>

#### 組織の割り当て量の設定

特定の組織の使用量の割り当て量を設定できます。

`cf bluemix-admin-set-quota <organization> <plan>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">割り当て量を設定する {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
<dt class="pt dlterm">&lt;plan&gt;</dt>
<dd class="pd">組織の割り当て量プラン。</dd>
</dl>

**ヒント:** **bluemix-admin-set-quota** という長いコマンド名の別名として **basq** を使用することもできます。

#### レポートの追加、削除、および取得

セキュリティー・レポートを追加、削除、および取得できます。
* レポートを追加するには、以下のコマンドを入力します。

`cf bluemix-admin-add-report <category> <date> <PDF|TXT|LOG> <RTF>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">レポートのカテゴリー。名前にスペースが含まれている場合は、引用符を使用して名前を囲んでください。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd"><samp class="ph codeph">YYYYMMDD</samp> という形式のレポート日付。</dd>
<dt class="pt dlterm">&lt;PDF|TXT|LOG&gt;</dt>
<dd class="pd">アップロードするレポート PDF、テキスト・ファイル、またはログ・ファイルのパス。</dd>
<dt class="pt dlterm">&lt;RTF&gt;</dt>
<dd class="pd">PDF の RTF (リッチ・テキスト・フォーマット) バージョンを含めるためのオプション。このオプションが適用されるのは、レポート PDF のパスを含めた場合のみです。RTF バージョンは、索引付けおよび検索に使用されます。</dd>
</dl>

**ヒント:** **bluemix-admin-add-report** という長いコマンド名の別名として **baar** を使用することもできます。

* レポートを削除するには、以下のコマンドを入力します。

`cf bluemix-admin-delete-report <category> <date> <name>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">レポートのカテゴリー。名前にスペースが含まれている場合は、引用符を使用して名前を囲んでください。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd"><samp class="ph codeph">YYYYMMDD</samp> という形式のレポート日付。</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">レポートの名前。</dd>
</dl>

**ヒント:** **bluemix-admin-delete-report** という長いコマンド名の別名として **badr** を使用することもできます。

* レポートを取得するには、以下のコマンドを入力します。

`cf bluemix-admin-retrieve-report <category> <date> <name>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">レポートのカテゴリー。名前にスペースが含まれている場合は、引用符を使用して名前を囲んでください。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd"><samp class="ph codeph">YYYYMMDD</samp> という形式のレポート日付。</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">レポートの名前。</dd>
</dl>

**ヒント:** **bluemix-admin-retrieve-report** という長いコマンド名の別名として **barr** を使用することもできます。

#### すべての組織のサービスの有効化および無効化

すべての組織に対して、{{site.data.keyword.Bluemix_notm}} カタログでのサービスの表示を有効化または無効化できます。

* すべての組織に対して {{site.data.keyword.Bluemix_notm}} カタログでのサービスの表示を有効化するには、以下のコマンドを入力します。

`cf bluemix-admin-enable-service-plan <plan_identifier>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">有効化するサービスの名前または GUID。非固有のサービス名を入力すると、サービス・プランを選択するように求められます。</dd>
</dl>

**ヒント:** **bluemix-admin-enable-service-plan** という長いコマンド名の別名として **baesp** を使用することもできます。

* すべての組織に対して {{site.data.keyword.Bluemix_notm}} カタログでのサービスの表示を無効化するには、以下のコマンドを入力します。

`cf bluemix-admin-disable-service-plan <plan_identifier>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">無効化するサービスの名前または GUID。非固有のサービス名を入力すると、サービス・プランを選択するように求められます。</dd>
</dl>

**ヒント:** **bluemix-admin-disable-service-plan** という長いコマンド名の別名として **badsp** を使用することもできます。

#### 組織に対するサービスの表示可能性の追加、削除、および編集

{{site.data.keyword.Bluemix_notm}} カタログで特定のサービスを表示できる組織のリストで、組織を追加または削除できます。特定の組織が {{site.data.keyword.Bluemix_notm}} カタログで表示できるサービスのリストを編集および置換することもできます。

* 組織が {{site.data.keyword.Bluemix_notm}} カタログで特定のサービスを表示できるようにするには、以下のコマンドを入力します。

`cf bluemix-admin-add-service-plan-visibility <plan_identifier> <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">表示可能性を追加するサービスの名前または GUID。非固有のサービス名を入力すると、サービス・プランを選択するように求められます。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">サービスの表示可能性リストに追加する {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
</dl>

**ヒント:** **bluemix-admin-add-service-plan-visibility** という長いコマンド名の別名として **baaspv** を使用することもできます。

* 組織に対して {{site.data.keyword.Bluemix_notm}} カタログでのサービスの表示可能性を削除するには、以下のコマンドを入力します。

`cf bluemix-admin-remove-service-plan-visibility <plan_identifier> <organization>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">表示可能性を削除するサービスの名前または GUID。非固有のサービス名を入力すると、サービス・プランを選択するように求められます。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">サービスの表示可能性リストから削除する {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
</dl>

**ヒント:** **bluemix-admin-remove-service-plan-visibility** という長いコマンド名の別名として **barspv** を使用することもできます。

* 単一または複数の組織に対して既存のすべての表示されるサービスを置換するには、以下のコマンドを使用します。

`cf bluemix-admin-edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>`
{: codeblock}

**注:** このコマンドにより、指定した組織で表示される既存のサービスが、コマンドで指定したサービスに置換されます。

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">表示されるようにするサービスの名前または GUID。非固有のサービス名を入力すると、サービス・プランを選択するように求められます。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">表示可能性を追加する {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。コマンドに追加の組織名または GUID を入力することで、複数の組織に対してサービスの表示可能性を有効化できます。</dd>
</dl>

**ヒント:** **bluemix-admin-edit-service-plan-visibility** という長いコマンド名の別名として **baespv** を使用することもできます。
