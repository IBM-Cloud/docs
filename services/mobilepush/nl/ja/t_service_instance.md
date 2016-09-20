---

copyright:
 years: 2015, 2016

---

# プッシュ・サービス・インスタンスの作成
{: #create-push-instance}

{{site.data.keyword.IBM}} {{site.data.keyword.mobilepushshort}} の使用を開始するには、最初に {{site.data.keyword.Bluemix}} アプリケーション (例えば、Node.js アプリ) を作成します。次に、プッシュ・サービス {{site.data.keyword.mobilepushfull}} のインスタンスを作成し、この Bluemix アプリケーションにバインドする必要があります。これはまた、Bluemix カタログの「ボイラープレート」セクションに移動して、「MobileFirst Services Starter」をクリックすることでも行えます。

**注**: 環境を管理するために複数の組織を構成した場合は、モバイル・アプリ用のランタイムおよびサービスを作成する組織を選択します。


1. Bluemix アプリケーションがない場合は、1 つ (例えば、Node.js アプリ) を作成する必要があります。
Bluemix アプリケーションを作成するには「Bluemix ダッシュボード (Bluemix Dashboard)」に移動し、**「アプリの作成」**をクリックします。
	
	**注**: アプリケーションがある場合は、ステップ 7 に進み、サービスを追加します。![サービス・インスタンスの作成](images/create_service_instance1.jpg "サービス・インスタンスの作成")

1. **「アプリ・テンプレートの選択」**で、**「WEB」**をクリックします。

3. **「開始点の選択」**エリアで、**「SDK for Node.js」**を選択して、**「続行」**をクリックします。![開始点](images/create_service_nodejs2.jpg) 

4. **「スペース」**プルダウン・メニューで、組織スペースを選択します。


	![
Select organization space](images/create_a_service3.jpg)
1. **「名前」**にアプリの名前を入力し、「ホスト」にホストの名前を入力します。


1. **「選択済みプラン」**プルダウン・メニューから、プランを選択し、**「作成」**ボタンをクリックします。アプリケーションのステージングを待ちます。

1. **「概要」**リンクをクリックします。![サービスの追加](images/create_service_add4.jpg)
1. **「サービスの追加」**をクリックします。「カタログ」画面が表示されます。

1. **「IBM Push Notifications」**を選択します。**「スペース」**プルダウン・メニューから組織を選択します。

	![組織スペースのプルダウン・メニュー](images/create_service_org.jpg)
1. **「サービス名」**に、Push Notification Service の名前を入力します。

1. **「選択済みプラン」**で、プランを選択し、**「作成」**ボタンをクリックします。

1. **「はい」**をクリックして、アプリケーションを再ステージングします。
                                

	![IBM Push Notification Service](images/create_service_notification5.jpg)

1. **「Push Notifications」**をクリックして、「Push Notification」ダッシュボードを表示します。
