---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}

#  Bluemix インフラストラクチャー・レイヤー

*最終更新日: 2016 年 3 月 15 日*

{{site.data.keyword.Bluemix_notm}} は、オペレーティング・システムおよびインフラストラクチャーのレイヤーを管理する必要がなくなるように、それらを要約するか非表示にします。ただし、オペレーティング・システムやアプリのミドルウェアについて詳細に知る必要がある状況が発生する場合もあります。
{:shortdesc}

## Bluemix インフラストラクチャー・レイヤーの表示
{:viewinfra}

cf stacks コマンドを実行して、アプリがデプロイされる先の使用可能なスタック (つまり、ルート・ファイル・システム) を表示することができます。また、*-s* オプションと *stack_name* を指定して cf push コマンドを使用する場合もスタックを指定できます。ここで、stack_name は、`lucid64` や `cflinuxfs2` などのルート・ファイル・システムです。
```
cf push appName -s stack_name
```
`cf buildpacks` コマンドを使用して、WebSphere Liberty profile や SDK for Node.js など、アプリを実行するランタイムとして使用可能なミドルウェア・コンポーネントを表示できます。また、次のコマンドを使用して、アプリのランタイム環境を指定できます。
```
cf push appName -b buildpackname
```
