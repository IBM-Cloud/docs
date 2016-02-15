{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}

# SendGrid 문제점 해결
{: #ts_sendgrid}

*마지막 업데이트 날짜: 2015년 12월 9일*

다음은 {{site.data.keyword.Bluemix}}에서 SendGrid 사용 관련 질문에 대한 답변입니다.
{:shortdesc}


## SendGrid를 사용하여 이메일을 보낼 수 없음
{: #ts_sendgrid_email}

SendGrid 서비스를 사용하여 이메일을 보낼 수 없다면 서비스 인스턴스당 허용되는 이메일 한계에 도달한 것일 수 있습니다.
{:shortdesc}


허용되는 최대 이메일 수만큼 이메일을 보낸 후에는 SendGrid 서비스를 사용하여 추가로 이메일을 보낼 수 없습니다.
{: tsSymptoms}


SendGrid 서비스를 사용하여 이메일을 보낼 경우 매달 서비스 인스턴스당 25,000개의 이메일을 보내도록 제한됩니다. 이 한계에 도달하면 SendGrid에서 이메일 전송을 중지하므로 이 서비스 사용에 대한 추가 비용이 발생하지는 않습니다.
{: tsCauses}

허용되는 나머지 이메일 수를 확인하려면 {{site.data.keyword.Bluemix_notm}} 대시보드에서 SendGrid 서비스 인스턴스를 클릭한 다음 **SENDGRID 대시보드 열기**를 클릭하십시오. **나머지 크레딧** 필드에서 숫자를 확인할 수 있습니다. 


매달 서비스 인스턴스당
제공되는 이메일 한계인 25,000개에 도달한 후 이메일을 추가로 보내려는 경우
다른 서비스 인스턴스를 추가할 수 있습니다. SendGrid에 대한 자세한 정보는 [SendGrid 시작하기](https://sendgrid.com/docs/index.html){: new_window}를 참조하십시오.    
{: tsResolve}

