---

copyright:
  years: 2015, 2016
lastupdated: "2017-04-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 최신 업데이트
{: #latest_updates}

서비스에 대한 최신 업데이트 목록입니다.

## 2017년 3월 15일: 업데이트된 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* 통합된 기타 서비스 유지보수
* 수정팩 8.5.5.11 또는 9.0.0.3이 Traditional WebSphere Application Server의 새 인스턴스에서 설치되도록 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 2진 파일이 업그레이드되었습니다. 
* 다음을 포함하여 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}의 [여러 보안 취약점](https://www-01.ibm.com/support/docview.wss?uid=swg22000587){: new_window}이 해결되었습니다. 
  * 기밀성 및 가용성에는 영향이 없고 무결성에는 많은 영향을 주는 라이브러리 컴포넌트와 관련된 불특정 취약성. 
  * 원격 공격자가 민감한 정보를 얻도록 허용함으로써 알려지지 않은 공격 벡터를 사용하여 기밀성에 많은 영향을 줄 수 있는 라이브러리 컴포넌트와 관련된 불특정 취약성. 
  * 원격 공격자가 서비스 거부(DoS)를 유발하도록 허용함으로써 알려지지 않은 공격 벡터를 사용하여 가용성에 약간의 영향을 줄 수 있는 라이브러리 컴포넌트와 관련된 불특정 취약성. 
  * SSL/TLS 프로토콜의 일부로 사용된 DES/3DES 암호의 오류 때문에 발생된, 원격 공격자가 민감한 정보를 얻도록 허용할 수 있는 OpenSSL의 취약성. 
  * 사용자가 웹 UI에 임의의 JavaScript 코드를 임베드하도록 허용함으로써 잠재적으로 의도된 기능을 변경하여 보안 세션 내의 신임 정보 노출을 유발하는 취약성. 
  * 사용자가 제공한 입력의 부적절한 유효성 검증 때문에 발생한, HTTP 응답 분할 공격에 대한 Apache HTTPD의 취약성. 
  * PAC 체크섬 처리에 실패하여 발생된, 원격 인증된 공격자가 시스템에서 상향된 권한을 얻을 수 있도록 허용하는 Samba의 취약성. 
  * Kerberos 인증 사용 시에 TGT(Ticket Granting Ticket)를 기타 서비스에 전달함으로써 발생된, 원격 인증된 공격자가 시스템에서 상향된 권한을 얻을 수 있도록 허용하는 Samba의 취약성. 
  * ndr_pull_dnsp_name() 함수의 정수 랩핑 결함 때문에 발생된, 힙 기반 버퍼 오버플로우에 대한 Samba의 취약성. 


## 2017년 2월 10일: 업데이트된 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* 통합된 기타 서비스 유지보수
* 수정팩 8.5.5.11 또는 9.0.0.2가 Traditional WebSphere Application Server의 새 인스턴스에서 설치되도록 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 2진 파일이 업그레이드되었습니다. 
* 수정팩 16.0.0.4가 WebSphere Application Server Liberty(Core 및 ND 플랜)의 새 인스턴스에서 설치되도록 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 2진 파일이 업그레이드되었습니다. 
* 다음을 포함하여 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}의 [여러 보안 취약점](https://www-01.ibm.com/support/docview.wss?uid=swg21997657){: new_window}이 해결되었습니다. 
  * 신뢰할 수 없는 소스의 직렬화된 오브젝트가 실행되어 자원 이용을 유발하도록 허용함으로써 발생된, 서비스 거부(DoS)에 대한 취약성. 
  * 원격 공격자가 민감한 정보를 얻도록 허용할 수 있는 잘못된 형식의 SOAP 요청의 사용. 


## 2016년 12월 16일: 업데이트된 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* 통합된 기타 서비스 유지보수
* 다음을 포함하여 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}에 영향을 주는 IBM SDK Java Technology Edition의 [여러 보안 취약점](https://www-01.ibm.com/support/docview.wss?uid=swg21995995){: new_window}이 해결되었습니다. 
  * 기밀성, 무결성 및 가용성 모두에 많은 영향을 주는 핫스팟 컴포넌트와 관련된 Oracle Java SE 및 Java SE Embedded의 불특정 취약성. 
  * 원격 공격자가 민감한 정보를 얻도록 허용함으로써 알려지지 않은 공격 벡터를 사용하여 기밀성에 많은 영향을 줄 수 있는 네트워크 컴포넌트와 관련된 Oracle Java SE 및 Java SE Embedded의 불특정 취약성. 
  *  사용자가 웹 UI에 임의의 JavaScript 코드를 임베드하도록 허용함으로써 잠재적으로 의도된 기능을 변경하여 보안 세션 내의 신임 정보 노출을 유발하는 IBM WebSphere Application Server의 XSS(Cross-site scripting) 취약성. 


## 2016년 11월 8일: 업데이트된 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* 클라이언트가 해당 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} VM에 대해 [공인 IP](networkEnvironment.html#networkEnvironment) 주소를 요청할 수 있는 기능이 추가되었습니다. 
* 다음을 포함하여 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}에 영향을 주는 [여러 보안 취약점](http://www-01.ibm.com/support/docview.wss?uid=swg21993842){: new_window}이 해결되었습니다. 
  * 신뢰할 수 없는 소스에서 직렬화된 오브젝트로 원격 공격자가 임의 Java 코드를 실행하도록 허용할 수 있는 IBM WebSphere Application Server의 취약성
  * TS_OBJ_print_bio 기능의 out-of-bounds 읽기에 의해 발생된 서비스 거부(Dos) 취약성. 원격 공격자는 애플리케이션이 충돌하도록 특별하게 만들어진 시간소인 파일을 사용하여 이 취약성을 활용할 수 있습니다. 
  * SSL/TLS 프로토콜의 일부로 사용된 64비트 블록 암호에 Triple-DES에서 오류에 의해 발생된 민감한 정보를 원격 공격자가 얻도록 허용할 수 있는 OpenSSL의 잠재적 취약성. SSL/TLS 서버와 클라이언트 사이에서 많은 양의 암호화된 트래픽을 캡처하여 man-in-the-middle 공격을 수행할 수 있는 원격 공격자가 평문 데이터를 복구하고 민감한 정보를 얻기 위해 이 취약성을 활용할 수 있습니다. 이 취약성은 SWEET32 Birthday 공격으로 알려졌습니다.
  * OpenSSL은 서비스 거부(DoS)에 취약합니다. 반복적으로 재조정을 요청하여 원격 인증 공격자는 사용 가능한 모든 메모리 리소스를 이용하도록 지나치게 큰 OCSP 상태 요청 확장을 보낼 수 있습니다. 
  * OpenSSL은 MDC2_Update 기능에서 정수 오버플로우에 의해 발생된 서비스 거부(DoS)에 취약합니다. 알 수 없는 공격 벡터를 사용하여 원격 공격자는 out-of-bounds 쓰기를 트리거하고 애플리케이션 충돌을 유발하도록 이 취약성을 활용할 수 있습니다. 
  * 특정 오퍼레이션에 대해 상수가 아닌 시간 코드 경로 중 다음을 허용하는 DSA 구현에서 오류에 의해 발생된 민감한 정보를 원격 공격자가 얻도록 허용하는 OpenSSL의 잠재적 취약성. 공격자는 개인용 DSA 키를 복구하도록 캐시 타이밍 공격을 사용하여 이 취약성을 활용할 수 있습니다. 
  * OpenSSL은 인증서 구문 분석 시에 누락된 메시지 길이 확인에 의해 발생된 서비스 거부(DoS)에 취약합니다. 원격 인증 공격자는 out-of-bounds 읽기를 트리거하고 서비스 거부(DoS)를 유발하도록 이 취약성을 활용할 수 있습니다. 

## 2016년 9월 19일: 업데이트된 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* WebSphere Application Server Liberty(Core 및 ND 플랜)의 새 인스턴스에 수정팩 16.0.0.3이 설치되도록 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 2진 파일이 업그레이드되었습니다. 
* 다음을 포함하여 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}에 영향을 주는 [여러 보안 취약점](http://www-01.ibm.com/support/docview.wss?uid=swg21990236){: new_window}이 해결되었습니다. 
  * 원격 공격자가 피싱 공격을 수행하도록 허용할 수 있는 IBM WebSphere Application Server Liberty의 취약성
  * OpenID Connect 클라이언트에서 XSS(Cross-site scripting)를 하기 위한 IBM WebSphere Application Server Liberty의 취약성
  * 기본 오류 페이지가 존재하지 않을 때 예외의 부적절한 처리로 인해 발생된 민감한 정보를 원격 공격자가 얻도록 허용할 수 있는 IBM WebSphere Application Server Liberty의 잠재적 취약성
  * Apache Commons FileUpload 컴포넌트에서 오류에 의해 발생된 서비스 거부(DoS)에 대한 Apache Tomcat의 취약성
  * 특정 조건에서 응답의 부적절한 처리로 인해 발생된 민감한 정보를 원격 공격자가 얻도록 허용할 수 있는 IBM WebSphere Application Server 및 IBM WebSphere Application Server Liberty의 취약성
  * 기밀성 영향력이 없고, 무결성 영향력이 낮으며 사용 가능성이 없는 네트워킹 컴포넌트와 관련된 지정되지 않은 취약성

## 2016년 8월 17일: 업데이트된 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* WebSphere Application Server in Bluemix 2진 파일이 8.5.5.9에서 8.5.5.10으로 업그레이드되었습니다. 
* 다음을 포함하여 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}에 영향을 주는 [여러 보안 취약점](http://www-01.ibm.com/support/docview.wss?uid=swg21988710){: new_window}이 해결되었습니다. 
  * WebSphere Application Server 및 WebSphere Application Server 하이퍼바이저 에디션 관리 콘솔에 영향을 미치는 Apache Struts 취약점
  * SIP 서비스 사용 시 IBM WebSphere Application Server의 잠재적 서비스 거부(DoS) 취약성
  * WebSphere Application Server에서 사용된 IBM HTTP Server에 영향을 미칠 수 있는 몇몇 취약점
  * IHS(IBM HTTP Server)에 영향을 미칠 수 있는 CGI 애플리케이션과 함께 HTTP 트래픽의 경로 재지정을 허용하는 취약성. 이 취약성은 "HTTPOXY"로 알려졌습니다.
  * IBM WebSphere Application Server의 정보 공개 취약성
  * webcontainer 사용자 정의 특성 HttpSessionIdReuse가 사용으로 설정되어 있는 환경에서만 발생하는 IBM WebSphere Application Server의 잠재적 우회 보안 제한 취약성


## 2016년 6월 24일: 업데이트된 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* 새 *Traditional ND* 또는 *Traditional WebSphere* 인스턴스를 작성하는 경우 V8.5 및 V9.0 중에 선택할 수 있는 기능이 추가되었습니다. 
* WebSphere Application Server Liberty(Core 및 ND 플랜)의 새 인스턴스에 수정팩 16.0.0.2가 설치되도록 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 2진 파일이 업그레이드되었습니다. 16.0.0.2는 8.5.5.9 이후 최신 수정팩입니다. 16.0.0.2부터, 이러한 플랜을 지원하는 권한이 있는 모든 Liberty 선택 기능이 기본적으로 설치됩니다. 
* 다음을 포함하여 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}에 영향을 주는 [여러 보안 취약점](http://www-01.ibm.com/support/docview.wss?uid=swg21984977){: new_window}이 해결되었습니다. 
  * IBM WebSphere Application Server에 영향을 미치는 Apache Standard Taglibs의 XXE(XML External Entity Injection) 취약점.
  * WebSphere Application Server Liberty Profile API 검색 기능 및 Swagger 문서를 사용하는 경우 예상되는 보안보다 약한 잠재적 취약점.
  * IBM WebSphere Application Server Liberty에 대한 관리 센터의 잠재적 정보 노출 취약점.
  * IBM WebSphere Application Server의 잠재적 HTTP 응답 분할 취약점.
  * OpenSSL 프로젝트에서 2016년 5월 3일에 공개한 OpenSSL 취약점.

## 2016년 6월 13일: 업데이트된 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* WebSphere Application Server in Bluemix RESTful API를 사용하는 애플리케이션 또는 스크립트의 작성을 통해 클라이언트가 가상 머신 인스턴스를 빌드, 프로비저닝, 관리 및 삭제할 수 있는 기능이 추가되었습니다. 
* 클라이언트가 10개 이하의 IP 주소 또는 64GB 이하 메모리가 할당된, 고정된 수의 중지된 인스턴스를 보유할 수 있게 하는 기능이 추가되었습니다. 클라이언트는 이제 5%의 감소 비율로 중지된 상태의 누적 인스턴스에 대해 청구됩니다. 

## 2016년 4월 26일: 업데이트된 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* FIPS140-2 사용 시에 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}의 [잠재적 보안 취약점](http://www-01.ibm.com/support/docview.wss?uid=swg21982128){: new_window} 및 Badlock을 포함한 Samba의 여러 취약점이 해결되었습니다. 
* 통합된 기타 서비스 유지보수

## 2016년 4월 15일: 업데이트된 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 2진 파일이 8.5.5.8에서 8.5.5.9로 업그레이드되었습니다. 
* OIDC(OpenID Connect) 클라이언트를 사용하는 이용자들에게 영향을 주는 IBM {{site.data.keyword.Bluemix_notm}}에 대해 Liberty for Java에서 [XSS(Cross-site scripting)](http://www-01.ibm.com/support/docview.wss?uid=swg21981221){: new_window} 취약성을 해결했습니다. 
* 통합된 기타 서비스 유지보수

## 2016년 2월 19일: 업데이트된 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}
* 해당 환경을 더 큰 가상 머신이 있는 올바른 크기로 만들도록 메모리 중심 애플리케이션이 있는 클라이언트에 대한 옵션이 추가되었습니다. 클라이언트는 최대 32GB RAM 가상 머신의 제공된 WebSphere Application Server 컴포넌트 또는 단일 시스템의 특정 리소스 크기를 선택할 수 있습니다.
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 2진 파일이 8.5.5.7에서 8.5.5.8로 업그레이드되었습니다. 
* 일반적으로 [SLOTH](http://www-01.ibm.com/support/docview.wss?uid=swg21977244){: new_window}라고 하는 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}에 영향을 주는 IBM SDK Java Technology Edition의 여러 취약점이 해결되었습니다. 
* OAuth 제공자 출력의 이용자에 영향을 주는 [XSS(Cross-site scripting)](http://www-01.ibm.com/support/docview.wss?uid=swg21976337){: new_window} 취약성이 처리되었습니다.
* 통합된 기타 서비스 유지보수

## 2015년 12월 11일: 업데이트된 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}
* 공식 제품명이 IBM Application Server on Cloud in {{site.data.keyword.Bluemix_notm}}에서 IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}로 변경되었습니다. 
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Network Deployment 플랜에 새 기능이 추가되었습니다. 플랜은 둘 이상의 가상 머신이 있는 WebSphere Application Server Network Deployment 셀 환경으로 구성됩니다. 해당 새 기능을
사용하면 고가용성, 장애 복구 및 확장성을 위한 클러스터형 환경을 설정할 수 있습니다. 
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Liberty Core 플랜에 새 기능이 추가되었습니다. 플랜에는
Liberty 프로파일(서버)의 그룹에 대한 관리 도메인이고 둘 이상의
가상 머신으로 구성된 Liberty Collective의 사용이 포함됩니다. 
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 2진 파일이 8.5.5.6에서 8.5.5.7로 업그레이드되었습니다. 
* Java 오브젝트 직렬화 해제를 처리하기 위한 [Apache Commons Collections
취약성](https://www.us-cert.gov/ncas/current-activity/2015/11/13/Apache-Commons-Collections-Java-Library-Vulnerability){: new_window}이 처리되었습니다.
* [HTTP 응답 분할 공격](http://www-01.ibm.com/support/docview.wss?uid=swg21972254){: new_window}을 허용하는 취약성이
처리되었습니다.
* 통합된 기타 서비스 유지보수

## 2015년 10월 15일: 업데이트된 Application Server on Cloud
* 다음 2개의 새로운 플랜이 추가되었습니다.
  * [WebSphere Application Server Traditional V9 Beta](https://www-01.ibm.com/marketing/iwm/iwmdocs/web/cc/earlyprograms/websphere.shtml){: new_window}
  * WebSphere Application Server ND
* 기타 서비스 유지보수