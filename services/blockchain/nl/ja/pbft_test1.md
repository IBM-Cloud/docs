---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# コンセンサス・テスト 1: ビザンチン・ノードなし
{: #pbft_test1}
最終更新日: 2016 年 8 月 4 日
{: .last-updated}

コンセンサス・テスト 1 は、4 つのノードがどれもビザンチンではなく、どのノードも任意かつ並列でオフラインにされていないというブロックチェーン・ネットワーク・シナリオで PBFT コンセンサス・プロトコルをテストします。
{:shortdesc}

Developer Network または High Security Business Network を起動した後、以下の手順に従ってビザンチン・ノードなしで PBFT をテストします。

(**注**: コード・スニペットとコード命令では、さまざまなシンボル値が使用されています。**VPO URL**、**"test_user1"**、**"test_user1_enrollSecret"**、**YOUR_CHAINCODE_ID** は単なるプレースホルダーです。ネットワーク・コンソールの**「API」**タブから、**「サービス資格情報」**と**「VP URL」**のリテラル値にアクセスします。チェーンコードをネットワークにデプロイすると、**YOUR_CHAINCODE_ID** の値が**「ネットワーク」**タブに表示されます。さらに、JSON 応答ペイロードのハッシュ値は、以下の例とは異なります。)

1.	ネットワーク・ユーザー ID とパスワードでログインします。  
    a.  ***VP0 URL***/registrar への POST を実行します。  
    b.	Payload {“enrollId”: “test_user1”, enrollSecret”: “test_user1_enrollSecret”} を実行します。  
    c.	ピアがペイロードを返します。
2.	ネットワークが稼働中であることを確認します。  
    a.	各ピアのブロックチェーンの高さを照会し、ピアごとに URL を指定します。  
    b.  GET ***VP0 URL***/chain を実行します。  
    c.  ピアがペイロードを返します。
   ```
   {
     "currentBlockHash":
     "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
     "height": 1
   }
   ```
    d.	これがブロックチェーンに対する最初の操作であれば、チェーンの高さは 1 になります。チェーンに存在するブロックはジェネシス・ブロックのみであるためです。チェーンの高さは、トランザクションが台帳に追加されるにつれて増えていきます。
3.	チェーンコードをデプロイします。  
    a.	***VP0 URL***/chaincode への POST を実行します。  
    b.  ペイロードを使用して次のようにします。  
       ```
       {
       "jsonrpc": "2.0",
       "method": "deploy",
       "params": {
       "type": 1,
       "chaincodeID":{
       "path":"github.com/hyperledger/fabric/examples/chaincode/go/chaincode_example02"
       },
       "ctorMsg": {
       "function":"init",
       "args": ["a", "1000", "b", "2000"]
       },
       "secureContext": "***test\_user1***"
       },
       "id": 1
       }
       ```
     c.  ピアがペイロードを返します。  
       ```
       {
       "jsonrpc": "2.0",
       "result": {
       "status": "OK",
       "message":
       "52b0d803fc395b5e34d8d4a7cd69fb6aa00099b8fabed83504ac1c5d61a425aca5b3ad3bf96643ea4fdaac132c417c37b00f88fa800de7ece387d008a76d3586"
       },
       "id": 1
       }
       ```
    d. 要求はネットワーク上の 4 つのピアすべてに送信されます。ピアは PBFT コンセンサス・プロトコルを実行し、この要求の実行に同意し、それぞれの台帳に結果を保管します。  
    e.	すべてのトランザクションは非同期であることに注意してください。戻りペイロードには、今後のチェーンコード呼び出しで使用されるチェーンコード・ハッシュが含まれます。
4.  しばらくしてから、デプロイ要求が完了したことを確認します。  
    a.  各ピアのブロックチェーンの高さを照会し、ピアごとに順番に URL を指定します。  
    b.  GET ***VP0 URL***/chain を実行します。  
    c.  コマンドからペイロードが返されます。
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 2
      }
      ```
    d.  デプロイ操作の完了は、プロセッサーの速度やネットワーク待ち時間といった要因に依存しています。
5.  チェーンコードがデプロイされたので、チェーンコードで操作を以下のように呼び出すことができます。  
    a.  chaincode_example02 を使用して、1 ユニットを a から b に移動します。  
    b.  次のようにペイロードを使って ***VP0 URL***/chaincode に POST を実行します。

      ```
      {
      "jsonrpc": "2.0",
      "method": "invoke",
      "params": {
      "type": 1,
      "chaincodeID":{
      "name":"YOUR_CHAINCODE_ID"
      },
      "ctorMsg": {
      "function":"invoke",
      "args": ["a", "b", "1"]
      }
      “secureContext”: “***test\_user1***”
      },
      "id": 2
      }
      ```
    c.  ピアがペイロードを返します。
```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message": "5a4540e5-902b-422d-a6ab-e70ab36a2e6d"
      },
      "id": 2
      }
      ```  
    d.  要求は 4 つのピアすべてに再び送信されます。ピアは PBFT コンセンサス・プロトコルを実行し、この要求の実行に同意し、それぞれの台帳に結果を保管します。
6.  直前の要求は非同期です。しばらくしたら、"a" 変数の値をチェーンコードから照会して、呼び出し操作が完了したことを確認します。  
    a.  次のようにペイロードを使って ***VP0 URL***/chaincode に POST します。
      ```
      {
      "jsonrpc": "2.0",
      "method": "query",
      "params": {
      "type": 1,
      "chaincodeID":{
      "name":"YOUR_CHAINCODE_ID"
      },
      "ctorMsg": {
      "function":"query",
      "args": ["a"]
      }
      “secureContext”: “***test\_user1***”
      },
      "id": 3
      }
      ```   
    b.  ピアがペイロードを返します。
```
      {
      "jsonrpc": "2.0",
      "result": {
      "status": "OK",
      "message": "999"
      },
      "id": 3
      }
      ```
    c.  予想どおり、チェーンコードが最初にデプロイされたときよりも "a" の値が 1 だけ小さくなっています。"a" に割り当てられた元の値は 1,000 であり、"b" に割り当てられた元の値は 2,000 でした。手順 5 でトリガーされた呼び出し要求によって、1 つのユニットが "a" から "b" に転送されます。
7.  呼び出し操作と照会操作を引き続き実行することができます。このプロセスは、前の手順と同じです。

  (コンセンサス・テスト 1 の終わり)
