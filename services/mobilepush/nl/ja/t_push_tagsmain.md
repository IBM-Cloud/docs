---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# タグ・ベースの通知 
{: #push-ios-main-tags}
最終更新日: 2017 年 1 月 16 日
{: .last-updated}

タグ・ベースの通知メッセージは、特定のタグにサブスクライブしているすべてのデバイスをターゲットとします。タグを定義して、タグを使用したメッセージの送受信を行うことが可能です。
 

まず、アプリケーションのタグを作成し、タグ・サブスクリプションをセットアップしてから、タグ・ベースの通知を開始する必要があります。[REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile.{DomainName}/imfpush/){: new_window}を使用してタグ・ベースの通知を送信するには、メッセージ・リソースに投稿する際に「tagNames」を指定するようにしてください。 
