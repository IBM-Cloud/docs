---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 定义策略
{: #criteria}

有了 {{site.data.keyword.DRA_short}}，为您应用程序定义策略变得非常轻松。要开始使用，请执行下列步骤：
{:shortdesc}

1. 在侧面的菜单上，单击**策略**。

2. 单击**创建策略 (+)**，然后输入新策略的名称和描述。

3. 单击**下一步**。

4. 至少添加一个规则到策略：
  1. 单击**创建规则 (+)**。
  2. 选择规则类型。
  3. 输入规则的详细信息和条件。
  4. 单击**保存**。

5. 当您完成添加规则到策略时，单击**完成**。

此时将在添加 {{site.data.keyword.DRA_short}} 的 {{site.data.keyword.Bluemix_notm}} 组织中创建策略。相同组织中的任何应用程序都可以使用该策略。

{{site.data.keyword.DRA_short}} 支持以下类型的度量和格式：

* 功能验证测试（Mocha、JUnit）
* 单元测试（Mocha、JUnit、Karma/Mocha）
* 代码覆盖（作为 JSON 摘要报告格式的 Istanbul、Blanket.js）

{{site.data.keyword.DRA_short}} 还支持 Selenium 和 Jasmine 测试。这些测试必须包含在正式支持的工具中，如 JUnit、xUnit 和 Mocha。要了解有关同时使用 {{site.data.keyword.deliverypipeline}}、{{site.data.keyword.DRA_short}} 和 Selenium 的更多信息，请参阅[在 Delivery Pipeline 上从命令行运行 Selenium 测试](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/)。

对于具有测试用例的项，您可以指定重要测试用例，即不管可接受的百分比而必须通过的测试。重要测试用例名称必须匹配测试用例的 `full title` 属性。    
* 对于 Karma/Mocha 测试，`describe()` 和 `it()` 描述字符串与空格链接在一起
* 对于 JUnit 测试，程序包名、类名和函数名与空格链接在一起    

您可以通过向管道添加 Sauce Labs 集成，使用 Sauce Labs 与 {{site.data.keyword.DRA_short}}。然后，将 `SAUCE_USERNAME` 和 `SAUCE_ACCESS_KEY` 环境变量作为凭证引入 Selenium 测试。

您可以在运行之后，在日志中查看所有测试的完整标题。  

注意：
* {{site.data.keyword.DRA_short}} 不支持在完整标题中包含连字符的重要测试。    
* 如果您更改组织名称，那么您必须重新创建与之前名称相关联的策略。您将丢失对名称更改之前所生成的决策报告的访问权。

## 创建功能验证测试规则
{: #criteria_fvt}

1. 键入描述并选择格式。

2. 指定必须通过声明成功的测试用例百分比。

3. 定义重要的任何测试用例。

4. 要监视测试用例回归，请选中**监视测试用例回归**复选框。

5. 单击**保存**。


## 创建单元测试规则
{: #criteria_ut}

1. 键入描述并选择格式。

2. 指定必须通过声明成功的测试用例百分比。

3. 定义重要的任何测试用例。

4. 要监视测试用例回归，请选中**监视测试用例回归**复选框。

5. 单击**保存**。


## 创建代码覆盖规则
{: #criteria_codecoverage}

1. 键入描述并选择格式。

2. 指定需要声明成功的代码覆盖百分比。

3. 要监视代码覆盖回归，请选中**监视测试用例回归**复选框。

4. 单击**保存**。
