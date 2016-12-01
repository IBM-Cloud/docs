
---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Safari Web ブラウザーの資格情報の構成
{: #configure-credential-for-safari}
最終更新日: 2016 年 11 月 15 日
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}} サービスの機能が拡張され、Safari ブラウザーに通知を送信できるようになりました。 

Apple 開発者アカウントを必ず取得しておいてください。Safari ブラウザーで通知を受け取るように構成するには、Web サイト Push ID を登録し、証明書を生成する必要があります。以下の手順を使用して、開始してください。

1. Apple Developer Member センターで、**「Certificates, ID & Profiles (証明書、ID およびプロファイル)」**をクリックします。 
2. **「Identifiers (ID)」**をクリックして、**「Website Push IDs (Web サイト Push ID)」**をクリックします。
3. プラス・アイコンを選択して、新規エントリーの作成を選択します。![Push ダッシュボード](images/safari_1.jpg)

4. 「Register Website Push ID (Web サイト Push ID の登録)」パネルで、適切な Web サイト Push ID の説明と識別子 ID を入力します。これは、「web」で始まる反転ドメイン名形式にすることをお勧めします。例: web.com.example.dailyweatherreports。
5. Web サイト Push ID を登録します。
6. **「Edit (編集)」**を選択して、Web サイト Push ID を更新します。
7. 「Certificate Information (証明書情報)」の「Certificate Assistant (証明書アシスタント)」ウィンドウで、E メール ID と共通名を入力します。「Certificate Authority email address (認証局 E メール・アドレス)」はブランクのままにします。
8. **「Save to disk (ディスクに保存)」**をクリックし、**「Continue (続行)」**を選択します。
9. 必要に応じて証明書を適切なフォルダーに保存してください。

 
