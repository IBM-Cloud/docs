---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# *필드 목록*에 나열되지 않은 값의 필터 추가
{:#k4_add_filter_out_value}

*필드 목록*에 표시되지 않은 값의 필터를 추가하려면 조회를 통해 값을 포함하는 레코드를 검색하십시오. 그런 다음 검색 페이지에서 사용 가능한 테이블 항목에서 필터를 추가하십시오.
{:shortdesc}

*필드 목록* 섹션에 표시된 목록에서 사용할 수 없는 값의 필터를 추가하려면 다음 단계를 완료하십시오.

1. Kibana 검색 페이지에서 표시하는 데이터의 서브세트를 확인하십시오. 자세한 정보는 [Kibana 검색 페이지에 표시되는 데이터 식별](logging_kibana_analize_logs_interactively.html#k4_identify_data)을 참조하십시오.

    예를 들어, 다음 그림은 *필드 목록*에 있는 CF 앱의 인스턴스 값을 보여줍니다. 
    
    ![필드 목록에 값 표시](images/k4_add_filter_f1.jpg "필드 목록에 값 표시")
    
    인스턴스 번호 *3*에 관심이 있지만, 이 번호는 사용자에게 표시되는 목록에서 사용 가능하지 않습니다.

2. 검색 페이지에서 특정 필드 값을 검색하도록 조회를 수정하십시오.

    예를 들어, 인스턴스 *3*을 검색하려면 다음과 같이 조회를 입력합니다.
   `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:"3"`
    
    ![조회 수정](images/k4_add_filter_f2.jpg "조회 수정")
    
    테이블에서 조회와 일치하는 레코드를 볼 수 있습니다. 
    
 3. 한 레코드를 펼치고 돋보기 단추 ![포함 모드의 돋보기 단추](images/k4_include_field_icon.jpg "포함 모드의 돋보기 단추")를 선택하여 필터를 추가하십시오.
 
     예를 들어, 값이 *3*인 인스턴스 ID의 필터를 추가하려면 *instance_id*별로 돋보기 단추 ![포함 모드의 돋보기 단추](images/k4_include_field_icon.jpg "포함 모드의 돋보기 단추")를 클릭하십시오.
     
     ![테이블 표시](images/k4_add_filter_f3.jpg "테이블 표시")
     
4. 필터가 추가되었는지 확인하십시오.

    예를 들어 다음 그림은 테이블에서 추가한 후 사용으로 설정된 필터를 표시합니다.
    
    ![필터 표시](images/k4_add_filter_f4.jpg "필터 표시")
    
    
