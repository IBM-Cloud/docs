---

copyright:
  years: 2016
lastupdated: "2016-08-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# コンセンサス・テスト 3: 2 つのビザンチン・ノード
{: #pbft_test2}


コンセンサス・テスト 3 は、4 つのうち 2 つのノードがビザンチンであり、2 つのノードが任意かつ並列でオフラインにされているというネットワーク・シナリオで PBFT コンセンサス・プロトコルをテストします。
{:shortdesc}

PBFT プロトコルでは、(N-1)/3 以下のピアがビザンチン (任意かつ並列) でオフラインになっても、N 個のピアを持つブロックチェーン・ネットワークが機能し続けることを保証します。Bluemix ブロックチェーン・ネットワークには 4 つのピアがあるため、2 つのピアが異常終了した場合、ネットワークがトランザクションを実行したり、一部を台帳に追加したりすることはありません。PBFT 式を当てはめると、(4-1)/3 = 1 < ビザンチン・ノードの数 (2) になるため、トランザクション処理は停止します。

以下の手順に従って、PBFT を 2 つのビザンチン・ノードを持つ 4 ノードのネットワークでテストします。
1.  ネットワーク・ユーザー ID とパスワードでログインします。  
    a.  ***VP0 URL***/registrar への POST を実行します。  
    b.  Payload {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”} を実行します。  
    c.  ピアがペイロードを返します。
2.  ネットワークが稼働中であることを確認します。  
    a.  各ピアのブロックチェーンの高さを照会し、ピアごとに URL を指定します。  
    b.  GET ***VP0 URL***/chain を実行します。  
    c.  コマンドからペイロードが返されます。
      ```
      {
      "currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
      "height": 1
      }
      ```
    d.  これがブロックチェーンに対する最初の操作であれば、チェーンの高さは 1 になります。チェーンに存在するブロックはジェネシス・ブロックのみであるためです。チェーンの高さは、トランザクションが台帳に追加されるにつれて増えていきます。
3.  チェーンコードをデプロイします。  
    a.  ***VP0 URL***/chaincode への POST を実行します。  
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
      "message": "YOUR_CHAINCODE_ID"
      },
      "id": 1
      }
      ```
    d.  要求はネットワーク上の 4 つのピアすべてに送信されます。ピアは PBFT コンセンサス・プロトコルを実行し、この要求の実行に同意し、それぞれの台帳に結果を追加します。  
    e.  すべてのトランザクションは非同期であることに注意してください。戻りペイロードには、トランザクション ID のみが含まれています。これは、結果を照会するために後で使用できます。
4.  テスト目的のために、ビザンチン (任意かつ並列) で、インターフェースの停止ボタンを使用して停止することによって、ノード VP2 と VP3 をオフラインにする操作をシミュレートします。(**注**: VP2 と VP3 が「停止」されたことがインターフェースに反映されるまで 30 ～ 60 秒かかる場合があります。)
5.  チェーンコードで呼び出し操作を実行します。  
    a.  この例では、chaincode_example02 は 1 ユニットを a から b に移動します。  
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
    d.  ネットワークが f=(N-1)/3 PBFT テストに失敗するので、呼び出し操作は入力として承認されますが実行されず、共有台帳には何も追加されません。
6.  "a" 変数の値を照会して、呼び出し操作が実行されていないことを確認します。  
    a.  次のようにペイロードを使って ***VP0 URL***/chaincode に POST を実行します。

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
      "message": "1000"
      },
      "id": 3
      }
      ```
    c.  "a" の値は変更されないことに注意してください。
  (コンセンサス・テスト 3 の終わり)
