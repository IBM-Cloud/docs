---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.objectstorageshort}} インスタンスのアンバインドおよびプロビジョン解除 {: #deprovisioning-object-storage}

*最終更新日: 2016 年 10 月 19 日*
{: .last-updated}


### インスタンスのアンバインド
Cloud Foundry アプリで {{site.data.keyword.objectstorageshort}} が不要になったが、保存したデータを保持したい場合は、サービスのインスタンスをアプリからアンバインドすることができます。

**注意**: {{site.data.keyword.objectstorageshort}} インスタンスを {{site.data.keyword.Bluemix_notm}} アプリケーションからアンバインドしたり、サービス・キーを削除したりすると、そのインスタンスのご使用の資格情報がすべて削除され、復元できません。

1. {{site.data.keyword.Bluemix_notm}} コンソールでアプリ詳細を開きます。
2. {{site.data.keyword.objectstorageshort}} インスタンスを選択し、**「サービスのアンバインド」**をクリックします。
3. **「削除」**をクリックします。
4. **「再ステージ」**をクリックします。



### インスタンスのプロビジョン解除

不要になった {{site.data.keyword.objectstorageshort}} のアンバインドされたインスタンスがある場合、インスタンスを削除できます。

**注意**: {{site.data.keyword.objectstorageshort}} インスタンスをプロビジョン解除すると、クラウド・プロジェクトが削除されます。プロビジョン解除されたインスタンス内のすべてのコンテナーおよびオブジェクトが削除され、復元できません。

1. {{site.data.keyword.Bluemix_notm}} コンソールでアプリ詳細を開きます。
2. {{site.data.keyword.objectstorageshort}} インスタンスを選択し、**「削除」**をクリックします。
3. **「再ステージ」**をクリックします。
