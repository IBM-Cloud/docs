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


# コンセンサス・テスト 4: ビザンチン・ノードの再始動
{: #pbft_test1}


コンセンサス・テスト 4 は、4 つのうち 1 つのノードがビザンチンになった後にオンラインになり、1 つのノードが任意かつ並列でオフラインにされているというネットワーク・シナリオで PBFT コンセンサス・プロトコルをテストします。


ブロックチェーン・ネットワークを再結合した以前のビザンチン・ピアは、台帳のコピーが他のピアのコピーより遅れていることを検出します。遅れているピアは。欠落しているブロックを現在の台帳のピアからコピーすることによって、その台帳を自動的に更新します。このプロセスは、状態の転送と呼ばれます。
{:shortdesc}

このテスト・ケースでは大量の呼び出し操作が必要になることに注意してください。ピアは、内部の*チェックポイント*・メッセージを送信することによって、現在の台帳の状態を互いに通知します。遅れているピアは、これらのメッセージを確認することによって、遅れていることを判別します。

1 つのビザンチン・ノードを再始動した後に PBFT をテストするには、以下の手順に従います。
1. ネットワーク・ユーザー ID とパスワードでログインします。  
   a. ***VP0 URL***/registrar への POST を実行します。  
   b. Payload {“enrollId”: “**test\_user1**”, enrollSecret”: “**test\_user1\_enrollSecret**”} を実行します。  
    c.	ピアがペイロードを返します。
2. ネットワークが稼働中であることを確認します。  
    a.	各ピアのブロックチェーンの高さを照会し、ピアごとに URL を指定します。  
   b. **GET ***VP0 URL***/chain** を実行します。  
    c.	コマンドがペイロードを返します。  
```json
{
"currentBlockHash": "RrndKwuojRMjOz/rdD7rJD/NUupiuBuCtQwnZG7Vdi/XXcTd2MDyAMsFAZ1ntZL2/IIcSUeatIZAKS6ss7fEvg==",
"height": 1
}
```
    d.	これがブロックチェーンに対する最初の操作であれば、チェーンの高さは 1 になります。チェーンに存在するブロックはジェネシス・ブロックのみであるためです。チェーンの高さは、トランザクションを台帳に追加するにつれて増えていきます。
3. チェーンコードをデプロイします。  
    a.	***VP0 URL***/chaincode への POST を実行します。  
   b. ペイロードを使用して次のようにします。  
```json
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
   c. ピアがペイロードを返します。
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "YOUR_CHAINCODE_ID"
},
"id": 1
}
```
    d. 要求はネットワーク上の 4 つのピアすべてに送信されます。ピアは PBFT コンセンサス・プロトコルを実行し、この要求の実行に同意し、それぞれの台帳に結果を保管します。  
   e. すべてのトランザクションは非同期です。戻りペイロードには、今後のチェーンコード呼び出しで使用されるチェーンコード・ハッシュが含まれます。
f. デプロイ操作の完了は、プロセッサーの速度やネットワーク待ち時間といった要因に依存しています。  
4. テスト目的のために、ビザンチン (任意かつ並列) で、インターフェースの停止ボタンを使用してノードを停止することによって、ピア VP2 をオフラインにする操作をシミュレートします。
5. チェーンコードで呼び出し操作を実行します。  
   a. この例では、chaincode_example02 は 1 ユニットを a から b に移動します。  
   b. 次のようにペイロードを使って ***VP0 URL***/chaincode への POST を実行します。
```json
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
   c. ピアがペイロードを返します。
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "5a4540e5-902b-422d-a6ab-e70ab36a2e6d"
},
"id": 2
}
```
    d. 要求は再びネットワーク上の 4 つのピアすべてに送信されます。ピアは PBFT コンセンサス・プロトコルを実行し、この要求の実行に同意し、それぞれの台帳に結果を追加します。  
6. この要求も非同期です。しばらくしてから、呼び出し操作が完了したことを確認します。  
   a. 次のようにペイロードを使って ***VP0 URL***/chaincode への POST を実行します。
```json
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
"args":["a"]
}
“secureContext”: “***test\_user1***”
},
"id": 3
}
```
   b. ピアがペイロードを返します。
```json
{
"jsonrpc": "2.0",
"result": {
"status": "OK",
"message": "999"
},
"id": 3
}
```
   c. 予想どおり、"a" の値は 1 以下になります。
7. インターフェースの開始ボタンを使用して、手動で再始動することによって、ピア **VP2** がオンラインに戻ることをシミュレートします。
8. 呼び出し操作を VP0 に送信します。
9. 4 つすべてのピアでチェーンコードの値 "a" を照会します。すべてのピアで "a" に対して同じ値が返されます。(**注**: 再始動されたピア (**VP2**) が `stateTransfer` 関数を正常に実行するまでにかかる時間は、さまざまなパラメーターで異なります。コンセンサスに達するためには、PBFT では 2f + 1 個のピアだけが必要であることに注意してください。**VP2** は現状のコンセンサスでは不要であるため、「キャッチアップ」のために大量の呼び出しが必要になる場合があります。このコンセンサス実装について詳しくは、Linux Foundation の Hyperledger Project の hyperledger/fabric「[プロトコルの規格](https://github.com/hyperledger/fabric/blob/v0.6/docs/protocol-spec.md#5-byzantine-consensus-1)」を参照してください。)

(コンセンサス・テスト 4 の終わり)
