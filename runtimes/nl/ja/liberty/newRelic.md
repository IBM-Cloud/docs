---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# New Relic の使用
{: #new_relic}

*最終更新日時: 2016 年 3 月 23 日*

New Relic は、アプリケーションのモニタリング・メトリックを提供するサード・パーティーのサービスです。New Relic サービスが提供する内容について詳しくは、[New
Relic](http://newrelic.com/java)を参照してください。

この [Java agent manual installation documentation](https://docs.newrelic.com/docs/agents/java-agent/installation/java-agent-manual-installation) によると、New Relic サービスを使用してモニターされる Java アプリケーションは、通常 New Relic エージェントとアカウントのライセンス・キーを使用してバンドルおよび構成する必要があります。IBM Bluemix 環境では、New Relic の使用許諾契約書とアカウントは、IBM Bluemix 内にサービス・インスタンスを作成することにより取得できます。その後 Java アプリケーションを New Relic サービス・インスタンスにバインドすると、Liberty ビルドパックがアプリケーションを自動構成して、New Relic サービスでモニターする準備を行います。具体的にはビルドパックは次のことを行います。

* アプリケーションに New Relic エージェントを提供する。
* VCAP_APPLICATION および VCAP_SERVICES アプリケーション環境変数からアプリケーション名とライセンス・キーを取得する。
* New Relic エージェントで要求されるプロパティーと構成テンプレートを構成する。

Liberty ビルドパックがアプリケーション用に生成したサンプル構成は以下のようになります。

```
    -javaagent:/home/vcap/app/.new_relic_agent/new_relic_agent-3.12.0.jar
    -Dnewrelic.home=/home/vcap/app/.new_relic_agent
    -Dnewrelic.config.license_key=123456
    -Dnewrelic.config.app_name=myapp
    -Dnewrelic.config.log_file_path=../../../../../logs
```
{: #codeblock}

## New Relic サービスの追加
{: #add_new_relic}

IBM Bluemix 内で既存の Java アプリケーションを New Relic でモニターするには、以下のステップに従ってください。
1. IBM Bluemix に New Relic サービス・インスタンスを作成します。```
    $ cf create-service newrelic standard mynewrelic```
{: #codeblock}

2. New Relic サービスを使用してアプリケーションを IBM Bluemix にデプロイします。以下のサンプル・アプリケーション・マニフェストを参照してください。```
        ---
        applications:

        - name: myapp
         memory: 1G
         instances: 1
         host: myapp
         domain: mybluemix.net
         path: myapp.war
         services:
          - mynewrelic```
{: #codeblock}

3. アプリケーションの IBM Bluemix ダッシュボードからアプリケーションの New Relic ダッシュボードに直接アクセスします。

### ユーザー提供の New Relic サービスの追加
{: #add_user_provided_new_relic}

既存の New Relic アカウントとライセンス・キーがある場合は、「ユーザー提供のサービス」を使用して既存の New Relic サービスをアプリケーションにバインドできます。

1. 既存のライセンス・キーを使用してユーザー提供のサービス・インスタンスを作成します。例えば、既存のライセンス・キーが 1234567 の場合、「create-user-provided-service」に CF CLI を使用して、以下のプロンプトでライセンス・キー 1234567 を入力できます。
```
    $ cf create-user-provided-service mynewrelic -p "licenseKey"
    licenseKey> 1234567
```
{: #codeblock}

2. ユーザー提供の New Relic サービス・インスタンスを使用してアプリケーションを IBM Bluemix にデプロイします。ユーザー提供の New Relic サービス・インスタンスを使用するサンプル・アプリケーション・マニフェストは以下のようになります。```
        ---
        applications:

        - name: myapp
         memory: 1G
         instances: 1
         host: myapp
         domain: mybluemix.net
         path: myapp.war
         services:
          - mynewrelic```
{: #codeblock}

3. New Relic ダッシュボードにアクセスしてアプリケーション・メトリックを表示します。

New Relic サービスの自動構成は、ビルドバックのフレームワークを通じて使用可能にされるコンテナー管理サービスであるため、他のサービスの自動構成と異なります。フレームワークを通じて使用可能にされるため、このサービスの自動構成は以下の 3 点で他のサービスと異なっています。
* オプトアウトはオプションではありません。
* サービス統合は Java エージェントである New Relic エージェントに依存します。したがって、server.xml ファイルのクラウド変数とは対照的に、これは Java オプションから構成されます。
* 構成は VCAP_SERVICES および VCAP_APPLICATION の両方に依存します。

# 関連リンク
## 一般
* [Liberty ランタイム](index.html)
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
