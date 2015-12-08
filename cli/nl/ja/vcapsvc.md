
{:shortdesc: .shortdesc}

# VCAP サービス

*最終更新日: 2015 年 11 月 9 日*


VCAP_SERVICES 環境変数は、{{site.data.keyword.Bluemix_notm}} でサービス・インスタンスと対話するために使用できる情報が格納された JSON オブジェクトです。{:shortdesc}


## VCAP_SERVICES 環境変数の値の取得
{:retrieving}

VCAP_SERVICES 環境変数は、{{site.data.keyword.Bluemix_notm}} でサービス・インスタンスと対話するために使用できる情報が格納された JSON オブジェクトです。この情報には、サービス・インスタンス名、資格情報、およびサービス・インスタンスへの接続 URL が含まれています。これらの値は、アプリケーションが {{site.data.keyword.Bluemix_notm}} でサービス・インスタンスにバインドされると VCAP_SERVICES 環境変数に取り込まれます。

VCAP_SERVICES 環境変数の値は、サービス・インスタンスをアプリケーションにバインドしたときにのみ使用可能です。アプリケーション環境変数は、
WebSocket コンソール・ドライバーを使用して表示できます。以下の例は、WebSocket コンソール・ドライバーを使用して、Node.js アプリケーションの環境変数を表示する方法を示しています。

最初に、コマンドを実行して Node.js アプリケーションを再プッシュします。```
cf push -c "curl -s https://raw.githubusercontent.com/dmikusa-pivotal/cf-debug-tools/master/debug-console.sh | bash" yourapp```
次に、以下の URL を入力します。```
https://yourapp.{APPDomain}/bash.sh
```
表示されるページで、ツールに接続するためのチェック・マークをクリックしてから、env コマンドを発行してアプリケーションの環境変数を表示します。cf-debug-tools の詳細については、「[Debug Tools for Cloud Foundry](https://github.com/dmikusa-pivotal/cf-debug-tools)」を参照してください。## Bluemix インフラストラクチャー・レイヤーの表示
{:viewinfra}


{{site.data.keyword.Bluemix_notm}} は、オペレーティング・システムおよびインフラストラクチャーのレイヤーを管理する必要がなくなるように、それらを要約するか非表示にします。ただし、オペレーティング・システムやアプリのミドルウェアについて詳細に知る必要がある状況が発生する場合もあります。

cf stacks コマンドを実行して、アプリがデプロイされる先の使用可能なスタック (つまり、ルート・ファイル・システム) を表示することができます。また、*-s* オプションと *stack_name* を指定して cf push コマンドを使用する場合もスタックを指定できます。ここで、stack_name は、`lucid64` や `cflinuxfs2` などのルート・ファイル・システムです。
```
cf push appName -s stack_name
```
`cf buildpacks` コマンドを使用して、WebSphere Liberty profile や SDK for Node.js など、アプリを実行するランタイムとして使用可能なミドルウェア・コンポーネントを表示できます。また、次のコマンドを使用して、アプリのランタイム環境を指定できます。
```
cf push appName -b buildpackname
```
