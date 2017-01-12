---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.objectstorageshort}} インスタンスのアンバインドおよびプロビジョン解除 {: #deprovisioning-object-storage}

{{site.data.keyword.objectstorageshort}} を Cloud Foundry アプリケーションにバインドしていて、ストレージがもう必要なくなった場合は、インスタンスをアンバインドし、プロビジョン解除することができます。
{: shortdesc}


## インスタンスのアンバインド
Cloud Foundry アプリで {{site.data.keyword.objectstorageshort}} は必要なくなったが、保存されているデータを維持したい場合は、サービスのインスタンスをアプリからアンバインドすることができます。

**注意**: {{site.data.keyword.objectstorageshort}} インスタンスを {{site.data.keyword.Bluemix_notm}} アプリケーションからアンバインドしたり、サービス・キーを削除したりすると、そのインスタンスのご使用の資格情報がすべて削除され、復元できません。{{site.data.keyword.objectstorageshort}} アカウントは、{{site.data.keyword.objectstorageshort}} インスタンスがプロビジョン解除されるまで削除されません。新しいサービス・キーを再バインドまたは作成することによって、新しいクラウド資格情報を生成できます。

1. アプリにバインドされているサービスを表示するには、Cloud Foundry アプリケーション内の「接続」タブをクリックします。
2. アンバインドするサービスを見つけて、サービス・タイルのメニュー・ボタンをクリックします。
3. **「サービスのアンバインド」**を選択します。
4. **「サービス・インスタンスの削除」**ボックスをクリアし、**「OK」**をクリックします。
5. **「再ステージ」**をクリックして、変更を有効にします。



## インスタンスのプロビジョン解除

不要になった {{site.data.keyword.objectstorageshort}} のインスタンスがある場合は、そのインスタンスを削除することができます。

**注意**: {{site.data.keyword.objectstorageshort}} インスタンスをプロビジョン解除すると、クラウド・プロジェクトおよび Swift アカウントが削除されます。プロビジョン解除されたインスタンス内のすべてのコンテナーおよびオブジェクトが削除され、復元できません。

1. アプリにバインドされているサービスを表示するには、Cloud Foundry アプリケーション内の「接続」タブをクリックします。
2. アンバインドするサービスを見つけて、サービス・タイルのメニュー・ボタンをクリックします。
3. **「サービスの削除」**を選択します。
4. **「削除」**をクリックして、確認します。
5. **「再ステージ」**をクリックして、変更を有効にします。
