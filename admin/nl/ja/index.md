{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

#{{site.data.keyword.Bluemix_notm}} の管理
{: #administer}
*最終更新日: 2016 年 1 月 20 日*

**「アカウントとサポート」**アイコン ![アカウントとサポート](../support/images/account_support.svg) をクリックし、次に**「組織の管理」**を選択して、組織、スペース、および割り当てられたユーザーを管理します。{{site.data.keyword.Bluemix_notm}} Local ユーザーまたは {{site.data.keyword.Bluemix_notm}} Dedicated ユーザーの場合、ローカル・インスタンスおよび専用インスタンスの管理に関する詳細について、[{{site.data.keyword.Bluemix_notm}} Local および {{site.data.keyword.Bluemix_notm}} Dedicated の管理](index.html#mng)を参照してください。
{:shortdesc}

##アカウントの管理
{: #mngacct}

{{site.data.keyword.Bluemix}} Public では、ユーザーのアクセス権限を含め、組織およびスペースを、すべてユーザー・インターフェースのダッシュボードから管理できます。また、使用量と請求をモニターすることもできます。{:shortdesc}

###組織およびスペース
{: #orgsandspaces}

組織管理者またはアカウント所有者は、「組織の管理」ページを使用して、ユーザーのアクセス権限など、組織またはスペースの設定を表示および管理することができます。「組織の管理」ページを開くには、**「アカウントとサポート」** アイコン ![アカウントとサポート](../support/images/account_support.svg) をクリックし、次に**「組織の管理」**を選択します。

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
<p>**注**: ユーザー・タイプがコラボレーターであり、以前に別のアカウントで {{site.data.keyword.Bluemix_notm}} を使用したことがあるユーザーは、組織管理者役割が割り当てられていても、組織にユーザーを招待することはできません。ユーザーを招待するには、ユーザー・タイプがメンバーでなければなりません。この問題に対処する方法については、『<a href="../troubleshoot/index.html#ts_adduser">ユーザーを組織に追加できない</a>』を参照してください。</p>
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

組織管理者またはアカウント所有者は、自身の組織を管理することができます。管理タスクには、組織の作成、組織の名前変更、スペースの作成、スペースへのユーザーの招待、ユーザーの役割の変更、および既存の組織の削除が含まれます。

<ul>
<li>組織の作成<p>支払アカウントを保有するユーザーのみが組織を作成することができます。支払アカウントを保有している場合は、以下の手順を実行して組織を作成できます。</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} ダッシュボードに移動し、**「アカウントとサポート」** アイコン ![アカウントとサポート](../support/images/account_support.svg) をクリックし、次に**「組織の管理」**を選択します。</li>
<li>**「組織の作成」**をクリックし、プロンプトに従って組織を作成します。</li>
</ol>
</li>
<li>組織の名前変更<p>組織を名前変更するには、以下の手順を実行します。</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} ダッシュボードに移動し、**「アカウントとサポート」**アイコン ![アカウントとサポート](images/account_support.svg) をクリックし、**「組織の管理」**を選択します。</li>
<li>名前変更する組織を選択します。</li>
<li>**「組織」**フィールドに新しい名前を入力し、**「保存」**をクリックします。</li>
</ol>
</li>
<li>メンバーのリスト<p>組織またはスペースのメンバーをリストするには、以下の手順を実行します。
</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} ダッシュボードに移動し、**「アカウントとサポート」** アイコン ![アカウントとサポート](../support/images/account_support.svg) をクリックし、次に**「組織の管理」**を選択します。**「ユーザー」**タブで組織のメンバーとメンバーの役割を確認できます。
</li>
<li>組織内のスペース名をクリックして、このスペースのメンバーとメンバーの役割を確認します。
</li>
</ol>
</li>
<li>スペースの作成<p>組織内にスペースを作成できます。例えば、開発環境として *dev* スペース、テスト環境として *test* スペース、実稼働環境として *production* スペースを作成できます。その後、アプリをスペースに関連付けることができます。スペースを作成するには、以下の手順を実行します。</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} ダッシュボードに移動し、**「アカウントとサポート」** アイコン ![アカウントとサポート](images/account_support.svg) をクリックし、次に**「組織の管理」**を選択します。</li>
<li>ユーザーの組織名の後の**「スペースの作成」**をクリックし、プロンプトに従ってスペースを作成します。</li>
</ol>
</li>
<li>スペースへのユーザーの招待<p>ユーザーをコラボレーターとして組織に招待することができます。また、組織のユーザーを個別のスペースに追加することもできます。ユーザーは、自身が追加されたスペースにのみアクセスできます。ユーザーをスペースに追加するには、以下の手順を実行します。</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} ダッシュボードに移動し、**「アカウントとサポート」** アイコン ![アカウントとサポート](../support/images/account_support.svg) をクリックし、次に**「組織の管理」**を選択します。その後、組織内の**「ユーザーの追加」**をクリックして、プロンプトに従ってユーザーを組織に追加します。</li>
<li>ユーザーをスペースに追加します。ナビゲーション・ペインでスペースを選択し、**「ユーザーの追加」**をクリックして、プロンプトに従ってユーザーをスペースに追加します。</li>
</ol>
</li>
<li>ユーザーの役割の変更
<p>ユーザーの役割を変更するには、以下の手順を実行します。</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースから**「アカウントとサポート」** アイコン ![アカウントとサポート](images/account_support.svg) をクリックし、次に**「組織の管理」**を選択します。</li>
<li>**「ユーザー」**タブで**「管理者」**、**「請求管理者」**、または**「監査員」**のチェック・ボックスを選択して、組織内のユーザーの役割を変更します。あるいは、ナビゲーション・ペインからスペースを選択し、次に**「ユーザー」**タブで**「管理者」**、**「開発者」**、または**「監査員」**のチェック・ボックスを選択して、スペース内のユーザーの役割を変更します。</li>
<li>**「保存」**をクリックします。</li>
</ol>
</li>
<li>既存の組織の削除<p>組織を削除するには、{{site.data.keyword.Bluemix_notm}} の登録および ID サポートに連絡します。</p>
<p>**注**: 削除操作は元に戻せません。組織を削除すると、その組織に関連付けられたすべてのアプリケーションとサービスが失われます。</p>
</li>
</ul>

## {{site.data.keyword.Bluemix_notm}} Local および {{site.data.keyword.Bluemix_notm}} Dedicated の管理
{: #mng}

{{site.data.keyword.Bluemix_notm}} Local または {{site.data.keyword.Bluemix_notm}} Dedicated の管理者権限がある場合は、**「管理」**ページに移動して、リソースの管理、割り当て量の使用状況のモニター、ユーザー許可の管理、アップグレード通知のスケジュール設定、セキュリティー・レポートおよびログの表示などを行います。組織の管理は、スペースを作成し、ユーザーの役割と権限を設定することによって行うことができます。『[組織の管理](index.html#orgmng)』を参照してください。
{:shortdesc}

*表 1. {{site.data.keyword.Bluemix_notm}} Local または Dedicated のインスタンスを管理するための管理用タスク*

| 選択可能な操作 | 詳細 |    
|----------------|---------|
|システム使用状況のモニター | **「管理」&gt;「使用量」**をクリックします。システム情報を表示し、CPU 使用量をモニターし、使用量の計画を立てて、ビジネスにとって最良の決定を行ってください。|
|カタログの管理 | **「管理」&gt;「カタログ管理」**をクリックします。どのサービスをユーザーに可視にするかを管理します。|
|組織の管理 | **「管理」&gt;「組織管理 (ORGANIZATION ADMINISTRATION)」**をクリックします。組織を作成し、組織の割り当て量をモニターし、ニーズに沿った決定を素早く行います。|
|スペースの作成とユーザーの役割の割り当て | **「アカウントとサポート」**アイコン ![アカウントとサポート](../support/images/account_support.svg) をクリックし、次に**「組織の管理」**を選択します。組織内にスペースを作成します。ユーザーを追加し、組織およびスペースの役割をユーザーに割り当てます。 |
|管理ユーザーの権限の管理 | **「管理」&gt;「ユーザー管理 (USER ADMINISTRATION)」**をクリックします。ユーザーの追加、ユーザーの削除、およびユーザーの権限の調整を行います。 |
|レポートおよびログのレビュー | **「管理」&gt;「レポートおよびログ (REPORTS AND LOGS)」**をクリックします。ユーザーのインスタンスのセキュリティー・レポートおよび監査ログを表示します。|
|システム情報の表示 | **「管理」&gt;「システム情報」**をクリックします。保留中の更新、インスタンスの名前とバージョン、地域、API URL、CLI URL、LDAP 構成の詳細、グループとユーザーのマッピング、統計、および共有ドメインなどのシステム情報を表示します。  |

### システム情報の表示
{: #oc_system}

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

* ナビゲーション・ペインから各種レポートを展開および表示できます。
* レポートおよびログのコレクション内で検索できます。検索は、レポート名に加え、レポートおよびログ内に含まれているテキスト・コンテンツにも適用されます。**「管理イベント (Administration Events)」**、**「DataPower レポート (DataPower Reports)」**、**「ファイアウォール (Firewall)」**、および**「ログイン監査 (Login Audit)」**によって検索をフィルターに掛けることもできます。
* レポートまたはログを表示している時、![ダウンロード](images/icon_download.svg) アイコンをクリックするとレポートをダウンロードできます。

### 状況の表示
{: #oc_status}

{{site.data.keyword.Bluemix_notm}} インスタンスの状況は、{{site.data.keyword.Bluemix_notm}} の「状況」ページを使用してモニターできます。「状況」ページは、{{site.data.keyword.Bluemix_notm}} プラットフォームや {{site.data.keyword.Bluemix_notm}} 内の主要なサービスに影響を及ぼす重要な事象に関する通知や発表を見つけるための中心的な場所です。

通知を調べずに済むように、通知の RSS フィードをサブスクライブすることができます。「状況」ページおよび RSS フィードのセットアップについて詳しくは、『[{{site.data.keyword.Bluemix_notm}} の表示](../troubleshoot/getting_customer_support.html#status)』を参照してください。

### カタログの管理
{: #oc_catalog}

{{site.data.keyword.Bluemix_notm}} カタログで、どの {{site.data.keyword.Bluemix_notm}} サービスおよびスターターをユーザーに表示するかを管理することができます。**「管理」&gt;「カタログ管理」**をクリックします。

サービスまたはスターターのタイルを選択して、サービスまたはスターターのプランの表示可能性を編集します。表示可能性を編集するには、以下のオプションから選択します。
* 非表示のサービスまたはスターターを表示して、「カタログ」でユーザーに表示されるようにするには、**「すべてのプランを有効化 (ENABLE ALL PLANS)」**を選択します。
* {{site.data.keyword.Bluemix_notm}} カタログで、サービスやスターターをユーザーに対して非表示にするには、**「すべてのプランを無効化 (DISABLE ALL PLANS)」**を選択します。
* 個別プランの表示可能性を制御するには、プラン名を選択してから、ドロップダウン・メニューを使用して**「すべての組織に対して有効化 (Enable for all organizations)」**、 **「すべての組織に対して無効化 (Disable for all organizations)」**、または**「特定の組織に対してプランを有効化 (Enable plan for specific organizations)」**を選択します。

### 組織の管理
{: #oc_organizations}

組織の作成と削除、組織へのマネージャーの追加、および割り当て量の使用量のモニターを行うことで、組織を管理できます。

**「管理」&gt;「組織管理 (ORGANIZATION ADMINISTRATION)」**をクリックします。

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
	* 組織を削除するには、「アクション」列の![削除](images/icon_trash.svg)をクリックします。
	* 組織の割り当て量プランを表示および編集するには、リスト内の組織の名前をクリックします。
	* 組織の名前の編集およびマネージャーの追加/削除を行うには、リスト内の組織の名前をクリックします。

### ユーザーおよび許可の管理
{: #oc_useradmin}

LDAP を使用し、自社のユーザー・レジストリーからご使用の {{site.data.keyword.Bluemix_notm}} インスタンスにユーザーを追加できます。ユーザーは、個別またはグループで追加できます。また、ユーザー許可を表示できます。`admin` 許可が割り当てられている場合、他のユーザーの許可を設定および管理することもできます。**「管理」&gt;「ユーザー管理 (USER ADMINISTRATION)」**をクリックします。

「ユーザー管理 (User Administration)」ページに、ローカル・インスタンスまたは専用インスタンスのユーザーが全員表示されます。
各ユーザーの許可が表示されます。許可は、None、`Admin`、`Catalog`、`Login`、`Reports`、および `Users` のいずれかになります。許可を有効にするか、または目的の許可について `view` 権限または `write` 権限をユーザーに与えることができます。許可および権限はアイコンで示されます。アイコンの各タイプと説明については、『[許可](#permissions)』を参照してください。

以下のオプションから選択します。
* ユーザーを検索します。**「検索」**フィールドを使用して、表内のユーザーを検索できます。
* ユーザーを追加します。`admin` 許可、または `write` 権限がある `users` 許可を持っている場合、ユーザーを追加することができます。ユーザーまたはユーザーのグループを追加するには、**「単一ユーザーの追加 (ADD SINGLE USER)」**または**「ユーザー・グループの追加 (ADD USER GROUP)」**をクリックします。**「検索」**フィールドに、検索対象のユーザー名またはグループ名を入力し、**「組織 (Org)」**リストからユーザーまたはユーザー・グループの追加先となる組織を選択します。追加するユーザーまたはグループが見つかったら、ユーザー名をクリックしてから、**「単一ユーザーの追加 (ADD USER)」**または**「複数ユーザーの追加 (ADD USERS)」**をクリックして追加します。50 人を超えるユーザーのグループは、バックグラウンド・バッチ・ジョブを介して追加されます。追加操作が成功すると、ユーザーまたはグループが表に追加され、表示および検索できるようになります。追加されたユーザーには、許可は割り当てられていません。
* 許可および組織を編集します。`admin` 許可を持っている場合、他のユーザーの許可および組織を編集することができます。許可を編集するには、ユーザーを特定し、ユーザー名をクリックします。許可を有効または無効にするには、開いたウィンドウに含まれている、以下のオプションから選択します。
	* 許可を有効にするには、リストから**「オン (On)」**を選択します。
	* リストから**「読み取り (Read)」**を選択して、ユーザーにその許可について `view` (read-only) 権限を持たせるか、**「書き込み (Write)」**を選択して、その許可について `write` (edit、add、remove) 権限を持たせます。
	* 許可を無効にするには、**「オフ (Off)」**を選択します。組織を編集するには、以下のオプションから選択します。
	* 検索フィールドを使用して組織を特定し、クリックしてオプションから選択し、**「追加」**をクリックして、ユーザーを組織に追加します。
	* ![削除。負符号で示されている](images/icon_remove.svg) アイコンをクリックして、組織からユーザーを削除します。終了したら、**「保存」**をクリックします。
* ユーザーを削除します。`admin` 許可、または `write` 権限がある `users` 許可を持っている場合、ユーザーを削除することができます。ユーザーを削除するには、そのユーザーを検索し、![「削除」](images/icon_trash.svg)アイコンをクリックし、次に**「削除」**をクリックします。

### 許可
{: #permissions}

ユーザーには、以下の許可を割り当てることができます。

| **ユーザー許可** | **説明** |       
|-----------------|-------------------|
| admin | `admin` 許可を備えているユーザーは、他のユーザーの許可を編集できます。 |
| catalog | `catalog` 許可を持つユーザーには、ローカル・インスタンスまたは専用インスタンスで利用できるサービスを `view` または `write` (modify) する権限を割り当てることができます。 |  
| login | `login` 権限を持つユーザーは、「管理」ページを表示できます。この権限がない場合、ユーザーは「管理」メニュー・オプションを表示できません。 |
| reports | `reports` 許可を持つユーザーには、セキュリティー・レポートを `view` または `write` (modify) する権限を割り当てることができます。 |
| users | `users` 許可を持つユーザーには、ユーザー・リストを `view` する権限、またはユーザーを `write` (add または remove) する権限を割り当てることができます。この許可では、他のユーザーの許可を設定することはできません。|

*表 2. 許可*

許可を有効にするか、または目的の許可について `view` 権限または `write` 権限をユーザーに与えることができます。許可および権限は次のアイコンで示されます。

* ![有効。チェック・マークで示されている](images/icon_enabled.svg) アイコン (許可の横) は、その許可が有効になっていることを示しています。
* ![表示。目で示されている](images/icon_read.svg) アイコンは、そのユーザーに、その許可について `view` (read-only) 権限があることを示しています。

* ![書き込み。鉛筆で示されている](images/icon_write.svg) アイコンは、そのユーザーに、その許可について `write` (edit、add、remove) 権限があることを示しています。


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
<pre>
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
</pre>
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
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < vary: X-HTTP-Method-Override
 < content-type: application/json
 < date: Wed, 22 Apr 2015 19:32:54 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 5612 msec
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
 
 > DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 >
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < content-type: application/json
 < date: Wed, 22 Apr 2015 21:01:09 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 1922 msec
 <
 ```
{: screen}

### カスタム・サービス API
{: #servicebrokerapi}

新規サービスの登録または作成、サービスの更新、およびサービスの削除に使用できる 3 つの API があります。

すべての API は、<code>https://opsconsole.&lt;subdomain&gt;.bluemix.net/</code> に対して相対的になります。

<dl>
<dt><strong>&lt;subdomain&gt;</strong></dt>
<dd>この値は、ローカル・インスタンスまたは専用インスタンスの名前です。{{site.data.keyword.Bluemix}} インスタンスのサブドメイン名はオンボード時に割り当てられています。</dd>
</dl>

### 新規サービスの登録

新規サービスを登録するには、以下の API とコード・サンプルを使用してください。

#### 経路

```
POST /codi/v1/serviceBrokers
```
{: screen}

#### 要求

*表 3. フィールド*

| **名前** | **説明** |
|-----------------|-------------------|
| name | サービス・ブローカーの名前。  |
| auth_username | サービス・ブローカーとの接続に使用されるユーザー名。 |
| auth_password | サービス・ブローカーとの接続に使用されるパスワード。 |
| broker_url | サービス・ブローカーとの接続に使用される URL。 |
| owningOrganization | サービスをホワイトリスト登録する初期組織。 |

##### 本文

```
{
  "name" : "Service broker's name",
  "auth_username" : "username",
  "auth_password" : "password",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

##### ヘッダー

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### 応答

##### 状況

```
201 Created
```
{: screen}

##### 本文

```
{
  "entity": {
    "name": "Service broker's name",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "49f3adcc-ecc2-46fa-83c1-03322f04b3b1",
    "created_at": "2015-12-07T19:51:50Z",
    "updated_at": null,
    "url": "/v2/service_brokers/49f3adcc-ecc2-46fa-83c1-03322f04b3b1"
  }
}
```
{: screen}

### サービスの更新

サービスを更新するには、以下の API とコード・サンプルを使用してください。

#### 経路

`PUT /codi/v1/serviceBrokers`
{: screen}

#### 要求

*表 4. フィールド*

| **名前** | **説明** |
|-----------------|-------------------|
| name | サービス・ブローカーの名前。 この名前は、サービスを作成するために使用した名前から変更できません。 |
| auth_username | サービス・ブローカーとの接続に使用されるユーザー名。 |
| auth_password | サービス・ブローカーとの接続に使用されるパスワード。 |
| broker_url | サービス・ブローカーとの接続に使用される URL。 |
| owningOrganization | サービスをホワイトリスト登録する初期組織。 |

##### 本文

```
{
  "name" : "Service Broker's name",
  "auth_username" : "username",
  "auth_password" : "newPassword",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

##### ヘッダー

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### 応答

##### 状況

```
201 Created
```
{: screen}

##### 本文

```
{
  "entity": {
    "name": "Service Broker's name",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "2cbdb812-d37f-443b-894a-a96de31e5c38",
    "created_at": "2015-12-07T20:11:08Z",
    "updated_at": "2015-12-07T20:11:19Z",
    "url": "/v2/service_brokers/2cbdb812-d37f-443b-894a-a96de31e5c38"
  }
}
```
{: screen}

### サービスの削除

サービスを削除するには、以下の API とコード・サンプルを使用してください。

*表 5. パラメーター*

| **名前** | **説明** |
|-----------------|-------------------|
| name | サービス・ブローカーの名前。 この名前は、サービスを作成するために使用した名前から変更できません。 |

#### 経路

```
DELETE /codi/v1/serviceBrokers?name=name of service broker
```
{: screen}

#### 要求

##### ヘッダー

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### 応答

##### 状況

```
204 No Content
```
{: screen}

### CF CLI を使用したユーザーの管理
{: #usingadmincli}

Cloud Foundry コマンド・ライン・インターフェースを {{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインと共に使用することにより、{{site.data.keyword.Bluemix_notm}} Local 環境または {{site.data.keyword.Bluemix_notm}} Dedicated 環境のユーザーを管理できます。例えば、LDAP レジストリーからユーザーを追加できます。

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

コマンドのリストを表示するには、次のコマンドを実行します。


`cf plugins`
{: codeblock}

追加でコマンドのヘルプを表示するには、`-help` オプションを使用します。

{{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインを使用した作業方法について詳しくは、『[{{site.data.keyword.Bluemix_notm}} 管理](../cli/plugins/bluemix_admin/index.html)』を参照してください。
