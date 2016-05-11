---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# 資産の管理
{: #manage-assets}

{{site.data.keyword.iotrtinsights_full}} の強力な機能の一部として、デバイスを管理対象資産にマップすること、および資産にマップされるすべてのデバイスに適用されるルールを作成することができます。
{: shortdesc}

例えば、モニター対象にする単一の資産に、複数のデバイスおよび多数のセンサーを含めることができます。

>**ヒント:** 資産が更新または変更されたときに、マッピング手順を繰り返すことができます。コンテキスト・ファイルおよびマッピング・ファイル内の `action` パラメーターにより、資産やデバイスを追加および削除できます。

デバイスを資産にマップするには、以下のようにします。
1. 資産のリストを作成し、CSV ファイルとして保存します。
このファイルには、資産管理ソフトウェアからの資産データが含まれます。
サンプル・ファイル・フォーマット:
```
ASSETNUM,ASSETTYPE,AS_DESCRIPTION,AS_DESCRIPTION_LD,INSTALLDATE,AS_ITEMNUM,AS_ITEMSETID,AS_LOCATION,PRIORITY,PURCHASEPRICE,REPLACECOST,SERIALNUM,AS_SITEID,AS_STATUS,ACTION  
5001,FACILITIES,New Asset 1,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123451,MYSITE,OPERATING,+    
5002,FACILITIES2,New Asset 2,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123452,MYSITE,OPERATING,+
```
{: codeblock}

  ここで、  
  - ASSETNUM - **必須:** システムにおける資産 ID 番号。(12)
  - ASSETTYPE - 資産のタイプ。(15)
  - AS_DESCRIPTION - 資産の要旨。(100)
  - AS_DESCRIPTION_LD - 資産の完全な説明。(32,000)
  - INSTALLDATE - (yyyy-MM-dd という形式の日付) 資産がインストールされた日付。
  - AS_ITEMNUM - 資産の関連項目番号。(30)
  - AS_ITEMSETID - 資産の項目セット番号。(8)
  - AS_LOCATION - 資産の場所。(12)
  - PRIORITY - (整数) 資産の優先順位。(12)
  - PURCHASEPRICE - (10 進数) 資産の購入価格。(10.2)
  - REPLACECOST - (10 進数) 資産を置き換えるためのコスト。(10.2)
  - SERIALNUM - 資産シリアル番号。(64)
  - AS_SITEID - 資産がインストールされたサイトの ID。(8)
  - AS_STATUS - 資産の状況。(20)
  - ACTION - `+` 記号は資産が追加されたことを意味し、`-` 記号は資産が削除されたことを意味します。  
  >**ヒント:** 括弧内の数字は、ストリングの最大長を示しています。別途記載がない限り、パラメーター・フォーマットは、大/小文字混合の英数字です。
5. 資産とデバイスのマッピング・リストを作成し、CSV ファイルとして保存します。
  このファイルを使用して、資産リスト内のインポートした資産を {{site.data.keyword.iot_short}} デバイスにマップします。
  サンプル・ファイル・フォーマット:
  ```
  sourceType,sourceId,targetType,targetId,action  
  d:orgid:iot-device-type,device001,asset,5001,+  
  d:orgid:iot-device-type,device002,asset,5002,+  
  d:orgid:iot-device-type,device003,asset,5002,+  
  ```
  {: screen}   

  ここで、
    - sourceType - デバイスの以下の {{site.data.keyword.iot_short}} データで構成されます。
      - orgid - {{site.data.keyword.iot_short}} 組織 ID
      - iot-device-type - {{site.data.keyword.iot_short}} デバイス・タイプ  
    - sourceID - {{site.data.keyword.iot_short}} デバイス ID  
    - targetType - 資産マッピングを作成するために単語`「asset」`を使用
    - targetID - 作成したコンテキスト・ファイルからの資産の ASSETNUM 項目
    - action - `+` 記号は資産がマップされていることを意味し、`-` 記号は資産がマッピングから削除されたことを意味します。
2. 管理者ユーザーとして {{site.data.keyword.iotrtinsights_short}} コンソールにログインします。
2. **「デバイス」>「デバイス・グループの管理 (Manage Device Groups)」**に移動し、**「資産のインポート (Import Asset)」**をクリックします。  
3. 作成した資産ファイルを参照して選択します。
4. ![「作成」アイコン](images/create.png "「作成」アイコン") をクリックして資産リストを作成します。
3. 作成した資産とデバイスのマッピング・ファイルを参照して選択します。
4. ![「作成」アイコン](images/create.png "「作成」アイコン") をクリックして資産リストを作成します。
5. **「デバイス」>「デバイス・グループの管理 (Manage Device Groups)」**に移動し、いずれかの資産をクリックして、資産にマップされたデバイスのリストを確認します。
