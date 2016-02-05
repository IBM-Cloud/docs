{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}

# SendGrid 疑難排解
{: #ts_sendgrid}

*前次更新：2015 年 12 月 9 日*

以下是在 {{site.data.keyword.Bluemix}} 中使用 SendGrid 的相關問題的解答。
{:shortdesc}


## 無法使用 SendGrid 來傳送電子郵件
{: #ts_sendgrid_email}

如果您無法使用 SendGrid 服務來傳送電子郵件，可能是因為您已達到每個服務實例所容許的電子郵件數目限制。
{:shortdesc}


在您傳送的電子郵件數目達到所容許的上限之後，即無法使用 SendGrid 服務來傳送更多電子郵件。
{: tsSymptoms}


當您使用 SendGrid 服務來傳送電子郵件時，每個服務實例每月可傳送的電子郵件限制為 25,000 封。在達到此限制之後，SendGrid 即停止傳送電子郵件，而使用此服務並不會產生進一步的費用。
{: tsCauses}

若要檢查剩餘的所容許電子郵件數目，請從 {{site.data.keyword.Bluemix_notm}} 儀表板按一下 SendGrid 服務實例，然後按一下**開啟 SendGrid 儀表板**。您可以在**剩餘額度**欄位中看到該數目。


如果在達到每個服務實例每月 25,000 封電子郵件的限制之後，還想要傳送更多電子郵件，您可以新增另一個服務實例。如需 SendGrid 的相關資訊，請參閱[開始使用 SendGrid](https://sendgrid.com/docs/index.html){: new_window}。    
{: tsResolve}

