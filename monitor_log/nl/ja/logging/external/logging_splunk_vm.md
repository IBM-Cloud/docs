---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 例: Cloud Foundry アプリケーション・ログの Splunk へのストリーミング
{: #splunk}

この例では、Jane という開発者が、IBM Virtual Servers Beta および Ubuntu イメージを使用して仮想サーバーを作成します。
Jane は Cloud Foundry アプリケーション・ログを
{{site.data.keyword.Bluemix_notm}} から Splunk へストリームし
ようと試みます。{:shortdesc}

  1. まず、Splunk をセットアップします。

     a. Jane は、[Splunk Light のダウンロード・サイト ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window} から
Splunk Light をダウンロードして、次のコマンドを使用してこれをインストールします。
ソフトウェアは */opt/splunk* にインストールされます。

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. RFC5424 syslog テクノロジー・アドオンをインストールして適用し、{{site.data.keyword.Bluemix_notm}} と統合します。アドオンのインストール手順について詳しくは、
[『Cloud Foundry ガイドライン』 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window} を参照してください。

	    次のコマンドを使用してアドオンをインストールします。

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        次に Jane は、
*/opt/splunk/etc/apps/rfc5424/default/transforms.conf*
を次のテキストで構成される新規の *transforms.conf* ファイルと
置き換えて、アドオンを適用します。

	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     c. Splunk のセットアップ後、Ubuntu マシン上の一
部のポートをオープンして、着信 syslog ドレーン (ポート 5140)
および Splunk Web UI (ポート 8000) を受け入れる必要があります。
{{site.data.keyword.Bluemix_notm}} 仮想サーバーのファイアウォ
ールがデフォルトでセットアップされているためです。

	    **注:** ここでは Jane の評価目的のために iptable 構成としているため、これは一時的なものです。実動における Bluemix 仮想サーバーでのファイアウォール設定を構成する方法について詳しくは、[『ネットワーク・セキュリティー・グループ』![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} 資料を参照してください。

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   次に、Jane は次のコマンドを使用して Splunk を実行します。

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Splunk 設定を構成して、
{{site.data.keyword.Bluemix_notm}} から syslog ドレーンを受け
入れます。syslog ドレーン用にデータ入力を作成する必要があります。

     a. Splunk Web インターフェースから、**「データ (Data)」>「データ入力 (Data inputs)」
**とクリックします。Splunk がサポー
トする入力タイプのリストが表示されます。

     b. syslog ドレーンが TCP プロトコルを使用するため、
**TCP** を選択します。

     c. **TCP** ペインの **「ポ
ート」**フィールドで、**「5140」**と入力
し、残りのフィールドは空白のまま残し、**「次へ」**
をクリックします。

     d. **「ソース・タイプ」**リストから、
**「未カテゴリー化 (Uncategorized)」>「rfc5424_syslog」
**を選択します。

     e. **「方式 (Method)」**タイプに
**「IP」**を選択します。

     f. **「索引 (Index)」**フィールド
で、**「新規索引の作成 (Create a new index)」
**をクリックします。新規索引に「bluemix」という名前を付け、**「保存」**をクリックします。

     g. 最後に**「レビュー (Review)」**ウィンドウで、設定が正しいことを確認し、**「送信 (Submit)」**をクリックしてこのデータ入力を有効にします。

  3. {{site.data.keyword.Bluemix_notm}}で、syslog ドレ
ーン・サービスを作成し、これをアプリにバインドします。

     a. cf cli から次のコマンドを使用して syslog ドレーン・サービスを作成します。

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **注:** *dummyhost* は実
名ではありません。実際のホスト名を非表示にするために使用されます。

     b. Jane は 自分のスペースで syslog ドレーン・サービスをアプリにバ
インドしてから、アプリを再ステージングします。

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


アプリを試行して、Splunk Web インターフェースで次の照
会ストリングを入力します。

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Splunk Web インターフェースでログのストリームを確認します。Jane がインストール
する Splunk は Splunk Light ですが、1 日に 500 MB のログを保存することが可能です。

