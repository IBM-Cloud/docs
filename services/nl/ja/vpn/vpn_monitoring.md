---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 状況とトラフィック・フローのモニタリング
{: #monitor}  
*最終更新日: 2016 年 3 月 17 日*  

モニタリング・フィーチャーを使用して、オンプレミスまたは SoftLayer サーバーの VPN ゲートウェイと {{site.data.keyword.vpn_short}} ゲートウェイの間の接続状況とトラフィック・フロー速度を表示します。
{:shortdesc}  
##サービス・ダッシュボードでのモニタリング
{: #dashboard}

**「モニタリング (Monitoring)」**タブを選択して、以下の接続統計を表示します。

* **接続状況 (Connection Status):** オンプレミスまたは SoftLayer サーバーの VPN ゲートウェイと IBM VPN ゲートウェイの間の VPN 接続の状況。値: 1=UP、-1=DOWN 
* **アウトバウンド・トラフィックの速度 (バイト/秒とパケット/秒) (Outbound Traffic Rate in bytes/second and packets/second):** IBM VPN ゲートウェイからオンプレミスまたは SoftLayer サーバーの VPN ゲートウェイへのトラフィックの速度。  
* **インバウンド・トラフィックの速度 (バイト/秒とパケット/秒) (Inbound Traffic Rate in bytes/second and packets/second):** オンプレミスまたは SoftLayer サーバーの VPN ゲートウェイから IBM VPN ゲートウェイへのトラフィックの速度。  

モニタリング統計は、最新の 48 時間のデータを使用して、グラフで表示されます。グラフは 20 分ごとに自動更新されます。ただし、モニタリング・タブから他の場所に移動した後に再び戻ることによって、いつでも最新のでデータを取り出すことができます。

**注:** グラフでは、現地時間ではなく協定世界時 (UTC) の時間が使用されます。  
##Logmet でのモニタリング
{: #logmet}

[Logmet](https://logmet.{DomainName}) を使用して、詳細な接続統計を表示します。 

1. Bluemix 資格情報と、IBM VPN サービス・インスタンスを作成した場所のスペースと組織名を使用してログインします。  
2. 右上のフォルダー・アイコン (![](images/folder.png)) を選択します。
3. ダッシュボードのリストから**「VPN サービス・モニタリング (VPN Service Monitoring)」**を選択して、グラフを表示します。グラフでは、現地時間が使用されます。  

**注:** Logmet に VPN サービス・ダッシュボードを作成するには、IBM VPN サービス・ダッシュボードで**「モニタリング (Monitoring)」**タブを少なくとも 1 回選択して、Logmet に照会を送信する必要があります。Logmet では、VPN 接続の確立から接続統計の表示までに最大 10 分間かかります。


