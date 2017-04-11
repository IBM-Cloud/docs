---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.geospatialshort_Geospatial}} のトラブルシューティング 
{: #ts_geospatial}


{{site.data.keyword.Bluemix_short}} での
{{site.data.keyword.geospatialshort_Geospatial}} の使用に関するいくつかの一般的な疑問に対する回答を得ましょう。
{:shortdesc}

##アプリケーションを停止してもサービスが地域のモニターを続けている
{: #stop-monitoring}


アプリケーションを停止することで自動的に {{site.data.keyword.geospatialshort_Geospatial}} が停止することはありません。
{:shortdesc}


{{site.data.keyword.geospatialshort_Geospatial}} を使
用するアプリケーションを停止しても、サービス管理ダッシュボードでは、アプリケーションで指定した地域をサービスがモニターし続けていることが認識されます。
{: tsSymptoms}


アプリケーションを停止しても、{{site.data.keyword.geospatialshort_Geospatial}} サービス・インスタンスは実行し続けます。このサービスは、アプリケーション
が実行中かどうかに関わらず、サービスを停止するまでは地域のモニターを続けます。
{: tsCauses}


サービス管理ダッシュボードから {{site.data.keyword.geospatialshort_Geospatial}} を停止します。または、REST API を使用してサービスを停止するようにアプリケーションを変更し、その変更を {{site.data.keyword.Bluemix_short}} にプッシュします。
{: tsResolve}

##アプリケーション内に指定しなかった地域をサービスがモニターしている
{: #unspecified-region}



複数のアプリケーションを同じサービス・インスタンスにバインドした場合、別のアプリケーションがこれらの地域を追加した可能性があります。
{:shortdesc}



サービス管理ダッシュボードで {{site.data.keyword.geospatialshort_Geospatial}} インスタンスを表示すると、アプリケーションの 1 つで指定した以上の地域がモニターされていることが分かります。
{: tsSymptoms}

{{site.data.keyword.geospatialshort_Geospatial}} の単一インスタンスが、それにバインドされたすべてのアプリケーションの地域をモニターします。これが意味するのは、サービス管理ダッシュボードでは、すべてのアプリケーションによって指定された地域の情報が表示されるということです。
{: tsCauses}

{{site.data.keyword.geospatialshort_Geospatial}} が特定の地域のモニターを停止するようにするには、次のようにします。

1. サービスの停止。
2. アプリケーションを変更して地域を削除します。
3. アプリケーションを {{site.data.keyword.Bluemix_short}} にプッシュして戻します。
{: tsResolve}


##サービス管理ダッシュボードからのトラブルシューティング
{: #dashboard}

アプリケーションのトラブルシューティングを行う際、サービス・インスタンスの状況を確認するためにサービス管理ダッシュボードに移動すると便利です。サービスで処理中のデータがない場合、サービスを停止してから再始動することによって問題を修正できることがあります。
{:shortdesc}

{{site.data.keyword.geospatialshort_Geospatial}} サービス・インスタンスの状況はアプリケーションの状況とは別になっていて、いくつかのアプリケーションが同じサービス・インスタンスにバインドされることが可能です。 

サービス管理ダッシュボードに表示されるのは、
{{site.data.keyword.geospatialshort_Geospatial}} の状況についての情報であり、バインドされたアプリケーションの状況についてではありません。サービス・インスタンスの状況とアプリケーションの状況が別になっていることは、
アプリケーションを停止しても {{site.data.keyword.geospatialshort_Geospatial}} サービス・インスタンスは実行し続けることを意味します。サービスは、アプリケーションが実行中かどうかに関わらず、地域を削除するまでは、選択した地域のモニターを続けます。
