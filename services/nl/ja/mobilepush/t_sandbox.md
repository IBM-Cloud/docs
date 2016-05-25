---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# サンドボックス・モードおよび実動モード

{: #push-sandboxandproduction-modes}

プッシュ通知は、サンドボックスまたは実動のいずれかのモードで使用できます。サンドボックスは、サーバー・アプリケーション・プッシュ・サービスとのプッシュ API の統合を開発およびテストするための自己完結型のテスト環境です。最初に、Push ダッシュボードを使用して、サンドボックス・モードと実動モードを構成します。[Push REST API](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window} を使用して、プッシュ・サービスの動作モードをサンドボックスと実動の間で切り替えます。デフォルトでは、サンドボックス・モードが有効になっています。ただし、モードの切り替え時に、タグ、デバイス、およびサブスクリプションは共有されません。


アプリケーションをライブ環境にデプロイする準備ができたら、Push REST API を使用して「実動」モードを選択します。REST API については、REST API を参照してください。

プッシュ・サービスの動作モードをサンドボックスから実動に切り替えるには、以下のようにします。

1. PUT ApplicationID Settings REST API 呼び出しを使用します。
2. JSON 本体で、[GET ApplicationID Settings REST](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window} API 呼び出しを使用して、モードが切り替えられたことを確認します。予想される応答は、"mode": "PRODUCTION です。
 
 ```
 { 
 "mode": "PRODUCTION"
 }
 ```
1. 環境モードの切り替え後、クライアント・コードを再度実行して、「実動」モードでデバイスを登録します。

REST API については、REST API を参照してください。
