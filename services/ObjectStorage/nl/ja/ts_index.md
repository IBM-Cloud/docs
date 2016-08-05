{:new_window: target="_blank"}

# {{site.data.keyword.objectstorageshort}} のトラブルシューティング
{: #troubleshooting}

*最終更新日: 2016 年 6 月 24 日*
{: .last-updated}

## Liberty プロファイルで openstack4J を使用したときに認識されないトークン・コンテンツ・パックが戻される
{: #unrecognized_token}

### 症状

Liberty プロファイルで openstack4j を使用したときに、以下のスタック・トレースが出力される場合があります。

    アプリケーション・クラス 'org.openstack4j.connectors.okhttp.HttpResponseImpl.readEntity:124' によって例外がスローされました
    org.openstack4j.api.exceptions.ClientResponseException: Unrecognized token 'contentpack': was expecting ('true', 'false' or 'null') at [Source: contentpack ; line: 1, column: 12]
    at org.openstack4j.connectors.okhttp.HttpResponseImpl.readEntity(HttpResponseImpl.java:124)
    at org.openstack4j.core.transport.HttpEntityHandler.handle(HttpEntityHandler.java:56)
    at org.openstack4j.connectors.okhttp.HttpResponseImpl.getEntity(HttpResponseImpl.java:68)
    at org.openstack4j.openstack.internal.BaseOpenStackService$Invocation.execute(BaseOpenStackService.java:169)
    at org.openstack4j.openstack.internal.BaseOpenStackService$Invocation.execute(BaseOpenStackService.java:163)
    at org.openstack4j.openstack.storage.object.internal.ObjectStorageContainerServiceImpl.list(ObjectStorageContainerServiceImpl.java:41)
    at com.mimotic.SecureMessageApp.HelloResource.getInformation(HelloResource.java:47)
    at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
    at sun.reflect.NativeMethodAccessorImpl.invoke(Unknown Source)
    at sun.reflect.DelegatingMethodAccessorImpl.invoke(Unknown Source)
    at java.lang.reflect.Method.invoke(Unknown Source)

### 解決方法

この問題は、Liberty プロファイルで提供される同じパッケージが openstack4j ライブラリーにいくつか含まれる場合のクラス・ロードの問題に起因します。例えば、OpenStack4j は JERSEY を使用し、これが Wink ライブラリーと競合する場合があります。

この問題を解決するには、以下の手順に従ってください。

1. 逆順序のクラス・ロード (parentLast) を使用します。
2. 使用可能なフィーチャーから jaxrs を除外します。
