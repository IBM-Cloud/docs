---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# タグ・ベースの通知 
{: #push-ios-main-tags}
最終更新日: 2016 年 12 月 06 日
{: .last-updated}

タグ・ベースの通知メッセージは、特定のタグにサブスクライブしているすべてのデバイスをターゲットとします。タグを定義して、タグを使用したメッセージの送受信を行うことが可能です。
 

まず、アプリケーションのタグを作成し、タグ・サブスクリプションをセットアップしてから、タグ・ベースの通知を開始する必要があります。[REST API](https://mobile.{DomainName}/imfpush/) を使用してタグ・ベースの通知を送信する場合には、メッセージ・リソースにポストする際に「tagNames」が指定されていることを確認してください。 
