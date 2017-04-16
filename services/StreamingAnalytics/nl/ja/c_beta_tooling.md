---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 開発ツールおよび環境
{: #c_beta_tooling}


{{site.data.keyword.streaminganalyticsshort}} 用のアプリケーションの開発に使用されるツールおよび環境には、以下の考慮事項が適用されます。
{:shortdesc}


* {{site.data.keyword.streaminganalyticsshort}} は、クラウドに {{site.data.keyword.streamsshort}} 開発環境を組み込みません。またクラウドに Streams Studio も組み込みません。ローカル側にインストールされた {{site.data.keyword.streamsshort}} 環境でアプリケーションを開発し、それらをアプリケーション・バンドルとしてサブミットしてください。開発環境が用意されていない場合は、[{{site.data.keyword.streamsshort}} 製品ページ](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)上で {{site.data.keyword.streamsshort}} Quick Start Edition を無料でダウンロードできます。
* 互換性を確保するために、アプリケーション・バンドルは Red Hat Enterprise Linux 6.5 環境、または同等の CentOS バージョンでコンパイルしてください。
* {{site.data.keyword.streamsshort}} 開発環境で、環境変数 `JAVA_HOME` を $STREAMS_INSTALL/java に設定してください。
