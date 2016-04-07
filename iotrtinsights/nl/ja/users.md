---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# ユーザーの管理 {: #manage-users}

{{site.data.keyword.iotrtinsights_short}} はチームのコラボレーション用に設計されており、管理者は、{{site.data.keyword.iotrtinsights_short}} コンソールにアクセスできるユーザーを追加できます。
{: shortdesc}

役割の説明:
- オペレーター (Operator)
オペレーターは {{site.data.keyword.iotrtinsights_short}} コンソールに直接ログインして、デバイスおよびデバイス・グループのリアルタイムのデータ・フローをモニターします。オペレーターは、ルールのアクティブ化と非アクティブ化、および編集可能なダッシュボードの変更も行うことができます。  
- 管理者 (Administrator)
管理者は、オペレーターが実行できるタスクに加え、ユーザーの追加、ダッシュボードのレイアウトの管理、データ・ソースの追加、およびデバイス・タイプの管理を行うことができます。  
- 所有者
所有者役割は、Bluemix で {{site.data.keyword.iotrtinsights_short}} サービス・インスタンスをデプロイした IBM ID に割り当てられます。所有者は、管理者と同じ特権を備えています。ただし、所有者を削除することはできません。

新規ユーザーを追加するには、以下のようにします。
1. ユーザーを {{site.data.keyword.iot_short}} に追加します。  
>**重要:** 管理者役割のユーザーを追加する場合は、そのユーザーを {{site.data.keyword.iot_short}} に追加する必要もあります。  

  1. {{site.data.keyword.iotrtinsights_short}} サービスのデータ・ソースである {{site.data.keyword.iot_short}} サービスのダッシュボードにログインします。  
  2. **「アクセス (Access)」>「メンバー (Members)」**にナビゲートし、**「メンバーの追加 (Add Members)」**をクリックします。
  3. 追加するユーザーの IBM ID を入力し、**「メンバーの追加 (Add Members)」**をクリックします。
2. ユーザーを {{site.data.keyword.iotrtinsights_short}} に追加します。
  1. 管理者役割または所有者役割を備えたユーザーとして {{site.data.keyword.iotrtinsights_short}} コンソールにログインします。
  2. **「セットアップ (Set Up)」>「ユーザーの管理 (Manage Users)」**に移動します。
  3. **「新規ユーザーの追加 (Add new user)」**をクリックします。
  4. 招待するユーザーの E メール・アドレスを入力し、ユーザーの役割を選択してから、![「作成」アイコン](images/create.png "「作成」アイコン") をクリックします。Web コンソール・リンクが含まれている E メールがユーザーに送信されます。E メール・アドレスが IBM ID に既に関連付けられている場合、そのユーザーはコンソールに直接ログインしてアクセスできます。そうでない場合は、ユーザーは、コンソールにアクセスする前に、無料の IBM ID を作成するように求められます。  
>**Real-Time Insights インスタンスの選択:** 複数の Real-Time Insights インスタンスにオペレーターまたは管理者としてアクセスできるユーザーは、インスタンスを迅速に切り替えることができます。Real-Time Insights コンソールで、自分のユーザー名をクリックし、アクセスするインスタンスを選択できます。  
