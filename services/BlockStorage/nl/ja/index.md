{:new_window: target="_blank"} 

# {{site.data.keyword.blockstorageshort}} (Beta) 入門

最終更新日: 2016 年 7 月 29 日
{: .last-updated}

{{site.data.keyword.blockstoragefull}} では、永続ストレージを必要とするトランザクション集約型のワークロードやランタイムのために、ブロック・レベルのストレージにアクセスできます。{{site.data.keyword.blockstorageshort}} サービスを使用して、ボリューム・ライフサイクルの管理、IBM Virtual Servers へのボリュームの接続、およびブロック・ストレージ・ボリュームのスナップショットの作成を行うことができます。

始める前に、以下の情報を確認します。

* {{site.data.keyword.blockstorageshort}} サービスは、アンバインドされたコンテキストでのみサポートされます。 
* IBM {{site.data.keyword.virtualmachinesshort}} が作成済みで、ブロック・ストレージ・ボリュームに接続されている必要があります。IBM {{site.data.keyword.virtualmachinesshort}} でブロック・ストレージ・ボリュームを使用することについては、[ブロック・ストレージ・ボリュームと IBM Virtual Servers](../../virtualmachines/vm_create.html#storage_BS)を参照してください。 

{{site.data.keyword.blockstorageshort}} については、以下のステップから始めます。

1. ボリュームを作成します。
   
   a. {{site.data.keyword.blockstorageshort}} サービスを開きます。

   b. **「作成」**をクリックして、**「ボリュームの作成 (Create Volume)」**ダイアログを開始します。

   c.	必要なボリュームのサイズを指定します。小数は使用できません。サイズの上限は、組織に割り当てられている割り当て量によって決まります。
   
   d.	名前を指定します。この名前は表示目的でのみ使用されます。
   
   e.	オプションで、ボリュームの詳細説明を入力します。
   
   f.	**「作成」**をクリックして情報を送信し、ダイアログを閉じます。

  ボリュームの作成には、しばらく時間がかかる可能性があります。

2. ボリュームを仮想サーバーに接続します。

   a. {{site.data.keyword.blockstorageshort}} サービスを開きます。
   
   b. 使用可能なボリュームのリストからボリュームを選択します。
   
   c.	**「接続 (Attach)」**をクリックします。
   
   d.	「接続 (Attach)」ダイアログで、ドロップダウン・リストから仮想サーバーのインスタンスを選択します。 
   
   e.	オプションで、そのボリュームの接続に使用するデバイスを指定します。デバイスを指定しない場合は、仮想サーバーで使用可能なデバイスのうち最初のものがシステムによって自動的に選択されます。
   
   f.	**「接続 (Attach)」**をクリックして情報を送信し、ダイアログを閉じます。
   
   このボリュームは、仮想サーバーのインスタンスに関する情報と併せて、接続済みボリュームの表にリストされます。
これで、仮想サーバーがデバイスを使ってデータを永続的に保持できるようになりました。 
 
次に行うこと

ボリュームを使用できるように準備します。詳しくは、[ボリュームの準備](../BlockStorage/blockstorage_preparingvolume.html)を参照してください。

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

