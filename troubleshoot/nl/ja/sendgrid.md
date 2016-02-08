{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}

# SendGrid のトラブルシューティング
{: #ts_sendgrid}

*最終更新日: 2015 年 12 月 9 日*

ここでは、{{site.data.keyword.Bluemix}} での SendGrid の使用に関する質問に対する回答を示します。
{:shortdesc}


## SendGrid を使用して E メールを 送信できない
{: #ts_sendgrid_email}

SendGrid サービスを使用して E メールを送信できない場合は、サービス・インスタンス 1 つにつき許可されている E メール数の上限に達した可能性があります。
{:shortdesc}


送信した E メール数が許可されている最大数になると、それ以後は、SendGrid サービスを使用してそれ以上に E メールを送信することができません。
{: tsSymptoms}


E メールを SendGrid サービスを使用して送信する時は、各月、サービス・インスタンス 1 つにつき、送信する E メール数は 25,000 通に制限されています。この上限に達すると、その後、SendGrid は E メールの送信を停止します。よって、このサービスを使用してもさらに料金が課されることはありません。
{: tsCauses}

許可されている残りの E メール数を調べるには、{{site.data.keyword.Bluemix_notm}} ダッシュボードから SendGrid サービス・インスタンスをクリックし、次に**「SENDGRID ダッシュボードを開く (OPEN SENDGRID DASHBOARD)」**をクリックします。
**「クレジット残高 (Credits Remaining)」**フィールドにある数字が確認できます。


各月、サービス・インスタンス 1 つあたり、 E メール 25,000 通という上限に達した後もさらに E メールを送信したい場合は、サービス・インスタンスをもう 1 つ追加することができます。
SendGrid について詳しくは、『[Getting Started with SendGrid](https://sendgrid.com/docs/index.html){: new_window}』を参照してください。    
{: tsResolve}

