{:new_window: target="_blank"}


# {{site.data.keyword.blockstorageshort}} 製品情報
{: #about-block-storage}

最終更新日: 2016 年 8 月 1 日
{: .last-updated}

## ボリューム 
{: #using-volumes-concept}

IBM {{site.data.keyword.blockstorageshort}} を使用して、ボリュームを作成し、仮想サーバーに接続できます。デフォルトでは、IBM {{site.data.keyword.virtualmachinesshort}} は永続ストレージを持たず、再始動するときにデフォルト・イメージに戻ります。{{site.data.keyword.blockstorageshort}} は仮想サーバーに永続ストレージを提供します。ブロック・ストレージ・ボリュームに格納されたデータは、お使いの仮想サーバーのライフサイクルが過ぎても存続します。{{site.data.keyword.blockstorageshort}} では、OpenStack Cinder を使用してボリュームのライフサイクルを管理します。

{{site.data.keyword.blockstorageshort}} ボリュームは、{{site.data.keyword.blockstorageshort}} サービス・インスタンスを使用して作成します。以下の方法で、ボリュームを仮想サーバーに接続できます。
  

* 提供する特定のデバイスを指定します。 
* システムが自動的に使用可能なデバイス名を選択することを指定します。 

仮想サーバーは入出力操作を、{{site.data.keyword.blockstorageshort}} サービスとは無関係に、指定されたデバイスに対して直接実行します。

## スナップショット 
{: #using-snapshots-concept}

ボリュームのスナップショットをブロック・レベルで作成することもできます。ボリュームが接続されている間、スナップショットは作成できません。したがって、作成されたスナップショットはクラッシュ対応になります。 

次に行うこと

ボリュームを作成します。詳しくは、[ボリュームの作成](../BlockStorage/blockstorage_creatingvolume.html)を参照してください。
