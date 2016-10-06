{:new_window: target="_blank"} 

# {{site.data.keyword.blockstorageshort}} (Beta) 概説

最終更新日: 2016 年 9 月 7 日
{: .last-updated}

{{site.data.keyword.blockstoragefull}} では、永続ストレージを必要とするトランザクション集約型のワークロードやランタイムのために、ブロック・レベルのストレージにアクセスできます。{{site.data.keyword.blockstorageshort}} サービスを使用して、ボリューム・ライフサイクルの管理、IBM Virtual Servers へのボリュームの接続、およびブロック・ストレージ・ボリュームのスナップショットの作成を行うことができます。

始める前に、以下の情報を確認します。

* スペースに、{{site.data.keyword.blockstorageshort}} サービスのインスタンスが作成されていることを確認します。新規サービス・インスタンスの追加方法について詳しくは、[新規サービス・インスタンスの要求](../../services/reqnsi.html#req_instance)を参照してください。
* {{site.data.keyword.blockstorageshort}} サービスは、アンバインドされたコンテキストでのみサポートされます。 
* IBM {{site.data.keyword.virtualmachinesshort}} が作成済みで、ブロック・ストレージ・ボリュームに接続されている必要があります。IBM {{site.data.keyword.virtualmachinesshort}} でブロック・ストレージ・ボリュームを使用することについては、[ブロック・ストレージ・ボリュームと IBM Virtual Servers](../../virtualmachines/vm_create.html#storage_BS)を参照してください。 

{{site.data.keyword.blockstorageshort}} については、以下のステップから始めます。

1. ボリュームを作成します。
   
   a. Bluemix UI で、**「コンソール」 > 「ストレージ」**を選択します。

   b. 以前にプロビジョンしたブロック・ストレージ・インスタンスを選択します。

   c. 「管理」ページで、**「ボリュームの作成 (Create Volume)」**をクリックして、「ボリュームの作成 (Create Volume)」ダイアログを開始します。

   d.	名前を指定します。 
   
      **注:** この名前は表示目的でのみ使用されます。
   
   e. 必要なボリュームのサイズを指定します。 
   
      **注:** 小数は使用できません。サイズの上限は、組織に割り当てられている割り当て量によって決まります。
   
   f.	オプションで、ボリュームの詳細説明を入力します。
   
   g.	**「作成」**をクリックして情報を送信し、ダイアログを閉じます。

  ボリュームの作成には、しばらく時間がかかる可能性があります。

2. ボリュームを仮想サーバーに接続します。

   a. Bluemix UI で、**「コンソール」 > 「ストレージ」**を選択します。

   b. 以前にプロビジョンしたブロック・ストレージ・インスタンスを選択します。

   c. 使用可能なボリュームのリストからボリュームを選択します。
   
   d.	「アクション」ドロップダウン・メニューから、**「接続 (Attach)」**をクリックします。
   
   e.	「接続 (Attach)」ダイアログで、ドロップダウン・リストから仮想サーバーのインスタンスを選択します。 
   
   f.	オプションで、そのボリュームの接続に使用するデバイスを指定します。 
   
      **注:** デバイスを指定しない場合は、仮想サーバーで使用可能なデバイスのうち最初のものがシステムによって自動的に選択されます。
   
   g.	**「接続 (Attach)」**をクリックして情報を送信し、ダイアログを閉じます。
   
   このボリュームは、仮想サーバーのインスタンスに関する情報と併せて、接続済みボリュームの表にリストされます。
これで、仮想サーバーがデバイスを使ってデータを永続的に保持できるようになりました。 
 
次に行うこと

ボリュームが接続された後、そのボリュームを使用するように仮想サーバーを構成する必要があります。詳しくは、[ボリュームの準備](../BlockStorage/blockstorage_preparingvolume.html)を参照してください。

# 関連リンク
{: #rellinks}

## チュートリアルおよびサンプル
{:id="samples"}

* [How to Use IBM Block Storage for Bluemix with IBM Virtual Servers](https://developer.ibm.com/bluemix/2016/02/24/use-block-storage-for-bluemix-with-virtual-servers/){: new_window}
* [Getting Started with IBM Block Storage for Bluemix](https://developer.ibm.com/bluemix/2016/02/15/getting-started-with-block-storage/){: new_window}
* [IBM Block Storage for Bluemix Demo](https://www.youtube.com/watch?v=3gCIHYKU1rE&list=PLzpeuWUENMK2d3L5qCITo2GQEt-7r0oqm&index=45){: new_window}

## API リファレンス
{: #api}
* [OpenStack Block Storage (Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

