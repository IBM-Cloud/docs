---

copyright:
 years: 2015, 2016

---

# Android アプリ用の Push SDK の初期化
{: #android_initialize}

初期化コードを配置する一般的な場所は、Android アプリケーション内のメインアクティビティーの onCreate メソッド内です。

Bluemix アプリケーション・ダッシュボード内の**「モバイル・オプション」**リンクをクリックして、アプリケーション経路とアプリケーション GUID を取得します。これらの値を、経路とアプリ GUID に使用します。コード・スニペットを変更して、Bluemix アプリの appRoute パラメーターと appGUID パラメーターを使用するようにします。


##Core SDK を初期化します。

```
// Initialize the SDK for Java (Android) with IBM Bluemix AppGUID and route
BMSClient.getInstance().initialize(getApplicationContext(), "applicationRoute","applicationGUID", bluemixRegion:"Location where your app Hosted");
```


**appRoute**

Bluemix で作成したサーバー・アプリケーションに割り当てられた経路を指定します。

**AppGUID**

Bluemix で作成したアプリケーションに割り当てられた固有キーを指定します。この値では、大/小文字が区別されます。

**bluemixRegionSuffix**

アプリがホストされている場所を指定します。次の 3 つの値のいずれかを使用できます。

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

##クライアント Push SDK を初期化します。

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```
