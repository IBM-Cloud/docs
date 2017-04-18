---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Kibana ダッシュボードのエクスポートと共有
<!-- for example, Uploading your data -->
{: #exporting_sharing_kibana_dash}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

ダッシュボード・スキーマを JSON ファイルとしてエクスポートするか、ログ・データのカスタマイズ済み Kibana ダッシュボードの URL を共有します。
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Kibana を使用して、ダッシュボードを JSON ファイルとしてエクスポートするか、ダッシュボードの URL を共有することで、他のステークホルダーと共同作業することができます。

Kibana ダッシュボードを JSON ファイルとしてエクスポートするには、以下のタスクを行います。

1. **「Save」**アイコン ![「Save」アイコン](images/logging_save.jpg) をクリックし、**「Advanced」** **>** **「Export schema」**をクリックします。

    ![ダッシュボードを JSON ファイルとしてエクスポート](images/logging_export_json.jpg)

2. JSON ファイルに分かりやすい名前を選択し、**「Save」**をクリックします。この JSON ファイルを持つユーザーは誰でも、Kibana ダッシュボードでこのファイルを開くことができます。 

Kibana ダッシュボードの URL を作成して共有するには、以下のタスクを行います。

1. Kibana ダッシュボードで、**「Folder」**アイコン ![「Folder」アイコン](images/logging_folder.jpg) をクリックして、最近のダッシュボードをすべてリストするメニューを表示します。このメニューには、名前で保存したダッシュボードのほかに、名前を付けていないダッシュボードが *ALCH_TENANT_ID_application_id* の形式でリストされます。 

    ![ダッシュボードのリスト](images/logging_list_of_dashboards.jpg)

2. 共有するダッシュボードの **「Share」**アイコン ![「Share」アイコン](images/logging_create_url.jpg) をクリックします。共有可能な URL が作成され、表示されます。 

    ![共有可能な URL のペイン](images/logging_shareable_link_popup.jpg)

    この URL をコピーして、他のユーザーとダッシュボードを共有します。**「Close」**をクリックして、ダッシュボードに戻ります。
