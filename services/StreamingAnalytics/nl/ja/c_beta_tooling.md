---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#開発ツールおよび環境
{: #c_beta_tooling}


{{site.data.keyword.streaminganalyticsshort}} 用のアプリケーションの開発に使用されるツールおよび環境には、以下の考慮事項が適用されます。
{:shortdesc}


* {{site.data.keyword.streaminganalyticsshort}} には、クラウド内の {{site.data.keyword.streamsshort}} 開発環境およびクラウド内の Streams Studio は含まれません。ローカル側にインストールされた {{site.data.keyword.streamsshort}} 環境でアプリケーションを開発し、それらをアプリケーション・バンドルとしてサブミットしてください。開発環境がない場合は、{{site.data.keyword.streamsshort}} Quick Start Edition を無料で [{{site.data.keyword.streamsshort}} 製品ページ](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)からダウンロードできます。
* 互換性を確保するために、アプリケーション・バンドルは Red Hat Enterprise Linux 6.5 環境、または同等の CentOS バージョンでコンパイルしてください。
* {{site.data.keyword.streamsshort}} 開発環境で、環境変数 `JAVA_HOME` を $STREAMS_INSTALL/java に設定してください。
