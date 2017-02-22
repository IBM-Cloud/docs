---

copyright:
  years: 2016, 2017
lastupdated:  "2016-08-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 保守および更新
{: #maintupdates_mf}

{{site.data.keyword.mobilefoundation_short}} は {{site.data.keyword.mfserver_short_notm}} <!--on {{site.data.keyword.containerlong}} as a container group--> をプロビジョンします。{{site.data.keyword.mobilefoundation_short}} サーバーに対する更新は、ユーザーに通知されます。都合のよいときに {{site.data.keyword.mobilefoundation_short}} サーバーを更新することができます。
{:shortdesc}

## 保守方針
{: #maintupdate_strategy_mf}

{{site.data.keyword.mobilefoundation_short}} に対する更新があると、更新が利用可能であることがユーザーに通知されます。通知は、サービス・インスタンス・ダッシュボードに表示されます。ユーザーは、自分で決定した保守時間帯に {{site.data.keyword.mobilefoundation_short}} に更新を適用することができます。

以下のいずれかのコンポーネントが更新されたときに、{{site.data.keyword.mobilefoundation_short}} サービス更新が利用可能になります。

* {{site.data.keyword.mfserver_short_notm}}.
* 基盤となる Liberty のバージョン。
* 基盤となる Java Developer Kit のバージョン。


## 更新の適用
{: #apply_update_mf}

{{site.data.keyword.mobilefoundation_short}} に対する更新は、**「再作成」**をクリックして適用できます。

更新を適用すると、{{site.data.keyword.mfp_oc_short_notm}} に表示されるサーバーのバージョンが変更され、サーバーの更新バージョンを示します。

**注:**
* ユーザーが自分の {{site.data.keyword.mobilefoundation_short}} サービス・インスタンスに独自のフィックスや更新を適用することはできません。
* **「再作成」**をクリックした際のプランによる動作の違いについては、[「開発者」プランでのサーバーの再作成](c_using_mfs_p1.html#recreate_mobilefoundation_p1)と[「プロフェッショナル 1 アプリケーション」プランでのサーバーの再作成](c_using_mfs_p2.html#recreate_mobilefoundation_p2)を参照してください。
