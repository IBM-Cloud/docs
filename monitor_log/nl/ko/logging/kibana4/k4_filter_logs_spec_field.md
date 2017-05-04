---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 특정 필드 값에 맞게 로그 필터링
{:#k4_filter_logs_spec_field}

특정 필드 값을 포함하는 항목을 검색할 수 있습니다.
{:shortdesc}

특정 필드 값을 포함하는 항목을 검색하려면 다음 단계를 완료하십시오.

1. Kibana 검색 페이지에서 표시하는 데이터의 서브세트를 확인하십시오. 자세한 정보는 [Kibana 검색 페이지에 표시되는 데이터 식별](logging_kibana_analize_logs_interactively.html#k4_identify_data)을 참조하십시오.

2. *필드 목록*에서 필터를 정의하려는 필드를 식별하고 클릭하십시오.

    필드에 대해 최대 5개의 값이 표시됩니다. 각 값에는 두 개의 돋보기 단추가 있습니다. 
    
    값을 볼 수 없으면 [필드 목록에 나열되지 않은 값의 필터 추가](k4_add_filter_out_value.html#k4_add_filter_out_value)를 참조하십시오.

3. 필드 값이 있는 항목을 검색하는 필터를 추가하려면 해당 값에 대해 돋보기 단추 ![포함 모드의 돋보기 단추](images/k4_include_field_icon.jpg "포함 모드의 돋보기 단추")를 선택하십시오.

    ![필드 값을 포함하는 필터](images/k4_add_filter_for_field.jpg "필드 값을 포함하는 필터")

    필드 값을 포함하지 않는 항목을 검색하는 필터를 추가하려면 해당 값에 대해 돋보기 단추 ![포함 모드의 돋보기 단추](images/k4_exclude_field_icon.jpg "포함 모드의 돋보기 단추")를 선택하십시오.

    ![필드 값을 제외하는 필터](images/k4_add_filter_to_exclude_field.jpg "필드 값을 제외하는 필터")

4. 다음 옵션 중 하나를 선택하여 Kibana의 필터에 대해 작업하십시오.

    <table>
      <tbody>
        <tr>
          <th align="center">옵션</th>
          <th align="center">설명</th>
          <th align="center">기타 정보</th>
        </tr>
        <tr>
          <td align="left">사용</td>
          <td align="left">필터를 사용하려면 이 옵션을 선택하십시오.</td>
          <td align="left">필터를 추가하면 자동으로 사용됩니다.<br> 필터를 사용하지 않으면 이 옵션을 클릭하여 사용으로 설정하십시오.</td>
        </tr>
        <tr>
          <td align="left">사용 안함</td>
          <td align="left">필터를 사용하지 않으려면 이 옵션을 선택하십시오.</td>
          <td align="left">필터를 추가한 다음 필드 값의 항목을 숨기려면 **사용 안함**을 클릭하십시오.</td>
        </tr>
        <tr>
          <td align="left">고정</td>
          <td align="left">Kibana 페이지 전체에서 필터를 유지하려면 이 옵션을 선택하십시오.</td>
          <td align="left">*검색* 페이지, *시각화* 페이지 또는 *대시보드* 페이지에 필터를 고정할 수 있습니다.</td>
        </tr>
        <tr>
          <td align="left">전환</td>
          <td align="left">필터를 전환하려면 이 옵션을 선택하십시오.</td>
          <td align="left">기본적으로 필터와 일치하는 항목이 표시됩니다. 일치하지 않는 항목을 표시하려면 필터를 전환하십시오.</td>
        </tr>
        <tr>
          <td align="left">제거</td>
          <td align="left">필터를 제거하려면 이 옵션을 선택하십시오.</td>
          <td align="left"></td>
        </tr>
      </tbody>
    </table>

 

 
 

