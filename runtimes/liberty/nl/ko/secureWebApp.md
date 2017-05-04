---

copyright:
  years: 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 보안 Java 웹 애플리케이션 작성
{: #secure_java_web_app}

심각한 보안 취약성이 나타나지 않도록 하려면 모든 웹 애플리케이션을 보안을 고려하여 디자인하고 코딩해야 합니다.
{: shortdesc}

{{site.data.keyword.Bluemix}}는 안전한 Liberty Java 코드를 작성하고 대부분의 XSS(Cross-site scripting) 문제를 방지할 수 있도록 보안 스타터 애플리케이션을 제공합니다. 이 [보안 스타터 애플리케이션](https://github.com/IBM-Bluemix/java-secure-app)을 다운로드하고, 빌드하고, 로컬 및 {{site.data.keyword.Bluemix_notm}}에 배치할 수 있습니다.

## 보안 웹 앱 작성 이유
{: #why}

보안 취약성은 다양한 보안 공격에 의해 악용될 수 있습니다. 공격으로 인해 신임 정보를 도둑맞고 데이터 및 기능이 유실되며 서비스가 중단되고 비즈니스의 평판과 매출에 손상을 입을 수 있습니다. XSS(Cross-site scripting)는 대부분의 웹 애플리케이션에서 방지해야 하는 일반적인 보안 취약성 중 하나입니다.

웹 애플리케이션 개발을 시작하기 전에 XSS 공격 및 개선 기술 이론을 학습하는 대신 이 [보안 스타터 애플리케이션](https://github.com/IBM-Bluemix/java-secure-app)을 사용할 수 있습니다. 보안 스타터 애플리케이션에는 XSS 방지 기술을 배우고 적용하면서 개발을 시작할 수 있도록 XSS를 방지하는 중요한 보안 코딩 사례의 코딩 예제가 포함되어 있습니다.

## 보안 샘플 앱 사용 방법
{: #how}

[보안 스타터 애플리케이션](https://github.com/IBM-Bluemix/java-secure-app)을 새 Liberty 애플리케이션 개발을 위한 시작점으로 사용할 수 있습니다. 앱에서 XSS 대책 코드를 학습한 다음 애플리케이션 API의 오퍼레이션에 적용하십시오. 보안 스타터 애플리케이션의 대책을 사용하면 XSS 공격을 줄이거나 방지하여 서버와 브라우저에서 애플리케이션이 손상되지 않도록 악의적인 사용자 입력을 막을 수 있습니다.

먼저 이 보안 스타터 애플리케이션을 다운로드한 다음 [getting-started-java](https://github.com/IBM-Bluemix/get-started-java) 샘플 애플리케이션에서 수행하는 방식과 동일하게 Bluemix 또는 로컬에 이 애플리케이션을 빌드하고 배치하십시오. [Bluemix에서 Liberty 시작하기](getting-started.html)로 이동하여 Bluemix에 애플리케이션을 빌드하고 배치하는 방법을 자세히 보십시오. 시작하기 위해 이러한 단계를 사용하여 앱을 복제하고 빌드하고 실행할 수 있습니다.

```
git clone https://github.com/IBM-Bluemix/java-secure-app
cd java-secure-app
mvn install liberty:run-server
```
http://localhost:9080/GetStartedSecureJava/에서 앱 보기

## 자세한 정보
{: more}
보안 스타터 애플리케이션에는 **BadServlet.java**가 있습니다. 이 애플리케이션은 개발자가 주의하지 않는 경우에 작성할 수 있는 안전하지 않은 코드의 예를 보여줍니다.

보안 스타터 애플리케이션에는 **GoodServlet.java**도 있으며, 여기에는 입력 유효성 검증, 출력 인코딩, 보안 HTTP 헤더 설정 및 컨텐츠 보안 정책과 같은 보안 코딩에 대한 많은 우수 사례가 포함되어 있습니다. 이러한 사례는 XSS에 대한 중요한 대책입니다. 해당 사례를 적용하면 일부 인젝션과 디렉토리 조회와 같은 다른 취약성을 줄일 수 있습니다.

[XSS Prevention Cheat Sheet ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.owasp.org/index.php/XSS){: new_window}에서 XSS 및 해당 대책을 자세히 보십시오.
