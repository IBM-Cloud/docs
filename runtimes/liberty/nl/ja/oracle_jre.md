---

copyright:
  years: 2016
lastupdated: "2016-06-21"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Oracle JRE の使用
{: #using_oraacle_jre}

必要に応じて、Oracle JRE を使用して Bluemix 上で Liberty アプリケーションを実行できます。実行するには、以下の条件を満たす必要があります。
* ビルドパックによるダウンロードが可能なロケーションで JRE をホストする。
* ホスト JRE のロケーションが指定されている index.yml ファイルをホストする。
* その JRE を使用するようにアプリケーションを構成する。

## JRE および index.yml のホスティング
{: #hosting_jre}

Oracle JRE ファイルは Web サーバー上でホストされる必要があり、Liberty ビルドパックはそのサーバーから Oracle JRE ファイルをダウンロード可能でなければなりません。このファイルは、使用可能ないずれかのサーバー機能を使用して Bluemix 自体の上でホストするか、パブリックに使用可能なロケーションでホストすることができます。サーバーは、JRE ファイルに関する詳細を指定した index.yml ファイルを使用して構成する必要があります。JRE と index.yml をホストするには、以下の手順を実行します。
  1. Oracle JRE を取得します。JRE は、UNIX 64 ビット OS で使用するバージョンが必要であり、tar.gz ファイルでなければなりません。
  2. Liberty ビルドパックによるダウンロードが可能なロケーションで JRE ファイルをホストします。 
  3. ホストするロケーションには必ず index.yml ファイルを配置します。index.yml ファイルには、後にコロンの付いた Oracle JRE のバージョン ID とその JRE ファイルのロケーションの完全な URL からなる項目が含まれていなければなりません。index.yml のフォーマットは、次のとおりです。
```
   ---
   jre_version: https://hostingLocation/jreName.tar.gz
```
{: codeblock}

    * 例えば、次のように指定します。
    ```
       ---
       1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```

## アプリケーションの構成
{: #configure_app}

Liberty アプリケーションでは、2 つの環境変数を設定する必要があります。*JBP_CONFIG_OPENJDK* は index.yml ファイルのロケーションを指定するように設定し、*JVM* 環境変数は *openjdk* に設定して代替 JRE を使用するようにビルドパックを構成する必要があります。

JBP_CONFIG_OPENJDK 変数の場合、値は次のようになります。
```
   'repository_root: "https://locationToIndexYml"'
```
{: codeblock}

これを設定するには、次のようなコマンドを発行します。
```
   $ cf se myApp JBP_CONFIG_OPENJDK 'repository_root: https://myHostingApp.ng.bluemix.net'
```
{: codeblock}

*repository_root* URL には「index.yml」は含まれませんが、そのロケーションの直前までを指しています。

JVM 環境変数を設定するには、次のようなコマンドを発行します。
```
   $ cf se myApp JVM 'openjdk'
```
{: codeblock}

**注**: 環境変数の設定後にアプリケーションを再ステージングする必要があります。

## 確認
{: #confirmation}

予期された JRE が使用されていることを確認するには、staging_task.log に次のようなメッセージがあるか調べます。
```
   -----> Downloading OpenJdk 1.8.0_91 from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}

# 関連リンク
{: #rellinks}
## 一般
{: #general}
* [Liberty ランタイム](index.html)
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
