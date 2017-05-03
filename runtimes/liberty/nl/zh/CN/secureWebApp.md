---

copyright:
  years: 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 编写安全 Java Web 应用程序
{: #secure_java_web_app}

在针对所有 Web 应用程序进行设计和代码编写时，都必须牢记安全性，以避免引入严重的安全漏洞。
{: shortdesc}

{{site.data.keyword.Bluemix}} 提供了一种安全的入门模板应用程序，可帮助您编写更安全的 Liberty Java 代码，同时避免大部分跨站点脚本编制 (XSS) 问题。可下载此[安全入门模板应用程序](https://github.com/IBM-Bluemix/java-secure-app)，进行构建并在本地以及在 {{site.data.keyword.Bluemix_notm}} 上进行部署。

## 为什么要编写安全 Web 应用程序
{: #why}

安全漏洞可能会被各种安全攻击所利用。攻击可能会窃取凭证，导致数据丢失和功能失灵，干扰服务，并损害公司声誉和收入。跨站点脚本编制 (XSS) 是在大多数 Web 应用程序中存在而必须避免的一种常见安全漏洞。

您可以使用此[安全入门模板应用程序](https://github.com/IBM-Bluemix/java-secure-app)，而不用在开始 Web 应用程序开发之前学习 XSS 攻击理论和补救方法。安全入门模板应用程序包含关键安全代码编写实践的代码编写示例，这些实践可防范 XSS，这样您就可以在学习并应用 XSS 防范方法的同时着手进行开发。

## 如何使用安全样本应用程序
{: #how}

可以使用[安全入门模板应用程序](https://github.com/IBM-Bluemix/java-secure-app)来着手开发新 Liberty 应用程序。首先了解应用程序中的 XSS 防范措施代码，然后将其应用于应用程序 API 的操作。安全入门模板应用程序中的防范措施通过缓解或阻止 XSS 攻击，从而帮助阻止恶意用户输入在服务器和浏览器上对您的应用程序造成损害。

首先，下载此安全入门模板应用程序，然后进行构建，并在 Bluemix 上或本地进行部署，方法与使用 [getting-started-java](https://github.com/IBM-Bluemix/get-started-java) 样本应用程序一样。转至 [Liberty on Bluemix 入门](getting-started.html)可了解有关在 Bluemix 上构建和部署应用程序的更多信息。首先，可以使用这些步骤来克隆、构建和运行应用程序。

```
git clone https://github.com/IBM-Bluemix/java-secure-app
cd java-secure-app
mvn install liberty:run-server
```
查看应用程序：http://localhost:9080/GetStartedSecureJava/

## 更多信息
{: more}
安全入门模板应用程序包含 **BadServlet.java**。此应用程序显示了开发者可能会由于疏忽而编写的不安全代码的示例。

安全入门模板应用程序还包含 **GoodServlet.java**，其中包含若干良好的安全代码编写实践，例如输入验证、输出编码、安全 HTTP 头设置和内容安全策略。这些实践是针对 XSS 的关键防范措施。应用这些实践还能缓解其他漏洞，例如一些注入和目录遍历。

请参阅 [XSS 防范备忘单 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.owasp.org/index.php/XSS){: new_window}，以了解有关 XSS 及其防范措施的更多信息。
