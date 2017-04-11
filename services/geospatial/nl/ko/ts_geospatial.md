---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.geospatialshort_Geospatial}} 문제점 해결 
{: #ts_geospatial}


{{site.data.keyword.Bluemix_short}}의 {{site.data.keyword.geospatialshort_Geospatial}} 사용과 관련된 몇 가지 일반적인 질문에 대한 답변입니다.
{:shortdesc}

##내 앱을 중지해도 서비스가 계속 지역을 모니터링함
{: #stop-monitoring}


앱을 중지해도 {{site.data.keyword.geospatialshort_Geospatial}}가 자동으로 중지되지 않습니다.
{:shortdesc}


{{site.data.keyword.geospatialshort_Geospatial}}를 사용하는 애플리케이션을 중지했지만 서비스 관리 대시보드에 서비스가 앱에서 지정한 지역을 계속 모니터링하고 있다고 표시됩니다.
{: tsSymptoms}


애플리케이션을 중지하는 경우 {{site.data.keyword.geospatialshort_Geospatial}} 서비스 인스턴스가 계속 실행됩니다. 앱 실행 여부에 관계없이 서비스를 중지할 때까지 서비스가 지역을 계속 모니터합니다.
{: tsCauses}


서비스 관리 대시보드에서 {{site.data.keyword.geospatialshort_Geospatial}}를 중지하십시오. 또는 REST API를 사용하여 서비스를 중지하도록 앱을 수정한 다음 변경사항을 {{site.data.keyword.Bluemix_short}}에 다시 푸시할 수 있습니다.
{: tsResolve}

##서비스가 내 앱에서 지정하지 않은 지역을 모니터링함
{: #unspecified-region}



동일한 서비스 인스턴스에 바인딩된 애플리케이션이 둘 이상인 경우 다른 애플리케이션이 이러한 지역을 추가했을 수 있습니다.
{:shortdesc}



서비스 관리 대시보드에서 {{site.data.keyword.geospatialshort_Geospatial}} 인스턴스를 보는 경우 하나의 앱에서 지정한 것보다 더 많은 지역이 모니터링되고 있는 것을 확인할 수 있습니다.
{: tsSymptoms}

{{site.data.keyword.geospatialshort_Geospatial}}의 단일 인스턴스는 자신에게 바인딩된 모든 앱의 지역을 모니터합니다. 즉, 서비스 관리 대시보드를 볼 때 모든 앱에서 지정된 지역에 대한 정보가 표시됩니다.
{: tsCauses}

{{site.data.keyword.geospatialshort_Geospatial}}가 특정 지역을 모니터링하는 것을 중지하려면 다음을 수행하십시오. 

1. 서비스를 중지합니다. 
2. 해당 지역을 제거하도록 앱을 수정합니다. 
3. 앱을 {{site.data.keyword.Bluemix_short}}에 다시 푸시합니다.
{: tsResolve}


##서비스 관리 대시보드에서 문제점 해결
{: #dashboard}

애플리케이션의 문제점을 해결할 때 서비스 관리 대시보드로 이동하여 서비스 인스턴스의 상태를 확인할 수 있습니다. 데이터를 처리하지 않는 경우 서비스를 중지 후 다시 시작하여 문제점을 해결할 수도 있습니다.
{:shortdesc}

{{site.data.keyword.geospatialshort_Geospatial}} 서비스 인스턴스의 상태는 애플리케이션의 상태와 구분되며 여러 애플리케이션을 동일한 서비스 인스턴스에 바인딩할 수 있습니다.  

서비스 관리 대시보드는 자신에게 바인딩된 애플리케이션이 아니라 {{site.data.keyword.geospatialshort_Geospatial}}의 상태에 대한 정보를 제공합니다. 서비스 인스턴스와 애플리케이션이 각각 별도의 상태를 가진다는 것은 애플리케이션을 중지할 경우에도 {{site.data.keyword.geospatialshort_Geospatial}} 서비스 인스턴스가 계속 실행됨을 의미합니다. 앱 실행 여부에 관계없이 서비스를 제거할 때까지 서비스가 선택된 지역을 계속 모니터합니다. 
