---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# コンセンサス・テスト 2: 1 つのビザンチン・ノード
{: #pbft_test2}

最終更新日: 2016 年 8 月 4 日
{: .last-updated}

コンセンサス・テスト 2 は、4 つのうち 1 つのノードがビザンチンであり、1 つのノードが任意かつ並列でオフラインにされているというネットワーク・シナリオで PBFT コンセンサス・プロトコルをテストします。
{:shortdesc}

PBFT プロトコルでは、(N-1)/3 以下のピアがビザンチン (任意かつ並列) でオフラインになっても、N 個のピアを持つブロックチェーン・ネットワークが機能し続けることを保証します。Bluemix ブロックチェーン環境には 4 つのピアがあるため、1 つのピアが異常終了しても、ネットワークはコンセンサスを実行し、台帳にトランザクションを追加し続けます。PBFT 式を当てはめると、(4-1)/3 = 1 = ビザンチン・ノードの数になるため、ブロックチェーン・ネットワークのトランザクション処理は続行します。

以下の手順に従って、PBFT を 1 つのビザンチン・ノードを持つ 4 ノードのネットワークでテストします。
1.	ネットワーク・ユーザー ID とパスワードでログインします。  
    a.  ***VP0 URL***/registrar への POST を実行します。  
    b.  Payload: {“enrollId”: “***test\_user1***”, enrollSecret”: “***test\_user1\_enrollSecret***”} を実行します。
    c.  ピアがペイロードを返します。
2.  ネットワークが稼働中であることを確認します。  
    a.  各ピアのブロックチェーンの高さを照会し、ピアごとに URL を指定します。  
    b.  GET ***VP0 URL***/chain を実行します。  
    c.  コマンドからペイロードが返されます。
      ```
      {
      "currentBlockHash":
      "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
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
      "message":
      "YOUR_CHAINCODE_ID_RETURNED_HERE"
      },
      "id": 1
      }
      ```  
    d. 要求はネットワーク上の 4 つのピアすべてに送信されます。ピアは PBFT コンセンサス・プロトコルを実行し、この要求の実行に同意し、それぞれの台帳に結果を保管します。  
    e.  すべてのトランザクションは非同期であることに注意してください。戻りペイロードには、今後のチェーンコード呼び出しで使用されるチェーンコード・ハッシュが含まれます。
  
    f.  デプロイメントの完了は、プロセッサーの速度やネットワーク待ち時間といった要因に依存しています。
  
4.  テスト目的で、インターフェースの停止ボタンを使用して手動で停止し、ビザンチン・ノード VP2 をシミュレートします。(**注**: VP2 が「停止」されたことがインターフェースに反映されるまで 30 ～ 60 秒かかる場合があります。
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
    d.  要求は 4 つのピアすべてに再び送信されます。ピアは PBFT コンセンサス・プロトコルを実行し、この要求の実行に同意し、それぞれの台帳に結果を保管します。
6.  この要求も非同期です。しばらくしたら、チェーンコードで "a" 変数の値を照会して、呼び出し操作が完了したことを確認します。  
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
      "message": "999"
      },
      "id": 3
      }
      ```
7.  予想どおり、チェーンコードが最初にデプロイされたときよりも "a" の値が 1 だけ小さくなっています。
8.  追加の呼び出し操作と照会操作を引き続き実行することができます。このプロセスは、前の手順と同じです。

(コンセンサス・テスト 2 の終わり)
