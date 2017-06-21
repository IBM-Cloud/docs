---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-27"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# IBM Bluemix Container Service のモニター
{: #monitoring_bmx_containers_ov}

{{site.data.keyword.Bluemix}} では、コンテナーのメトリックがコンテナー外部から自動的に収集されるので、コンテナー内部にエージェントをインストールして保守する必要がありません。
{:shortdesc}

コンテナー内エージェントでは、コンテナーが急速に作成されて破棄されるような、短期間だけ存在する軽量クラウド・インスタンスおよび自動スケーリング・グループに対して、
オーバーヘッドおよびセットアップ時間がかなり大きくなる可能性があります。このアウト・オブ・バンドのデータ収集方法によって、こういった問題点がなくなり、モニタリングの負担がユーザーにかからなくなります。

ホスト内で実行中のプロセスが、メトリックに関するエージェントレス・モニタリングを実行します。このプロセスはクローラーとも呼ばれ、デフォルトでは、すべてのコンテナーから以下のメトリックを常に収集します。

* CPU
* メモリー
* ネットワーク情報

メトリック・データは Graphite で収集され、{{site.data.keyword.Bluemix_notm}} UI と Grafana の両方に表示されます。 

Grafana は、{{site.data.keyword.Bluemix_notm}} UI から、またはブラウザーから直接、起動できます。詳しくは、『[Grafana でのメトリックの分析](../grafana/monitoring_analyzing_metrics_grafana.html#analyzing_metrics_grafana)』を参照してください。

Docker 規則およびグループ・アカウンティング情報が、モニタリング・データ収集の基本的メカニズムとして使用されます。

## メトリックの保存

収集されるのは、1 分間につき最大 1 データ・ポイントです。7 日以内に書き込まれなかったコンテナー・メトリックは削除されます。
    
## メトリックのソート

データはコンテナー ID 順に並べて表示されます。 

コマンド・ラインから `cf ic ps` コマンドを実行することで、プライベート {{site.data.keyword.Bluemix_notm}} イメージ・レジストリー内にあるコンテナーのコンテナー ID のリストを表示できます。

