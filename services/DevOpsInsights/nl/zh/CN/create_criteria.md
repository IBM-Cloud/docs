---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 定义策略
{: #policies}

策略用于控制 Continuous Delivery Pipeline 中的检测点。如果您的代码不符合或超出在特定检测点执行的策略，那么会暂停部署以防止发布有风险的更改。
{:shortdesc}

您可在 {{site.data.keyword.DRA_short}} 中定义策略。这将在包含 {{site.data.keyword.DRA_short}} 的 {{site.data.keyword.Bluemix_notm}} 组织中创建策略。相同组织中的任何应用程序都可以使用该策略。 

要定义策略，请执行以下操作：

1. 在左侧导航中，单击**设置**。

2. 单击**策略**。

3. 单击**创建策略**，然后输入新策略的名称和描述。

4. 单击**下一步**。

4. 至少添加一个规则到策略：
  1. 单击**向策略添加规则**。
  2. 选择规则类型。
  3. 输入规则的详细信息和条件。
  4. 单击**保存**。

5. 当您完成添加规则到策略时，单击**完成**。

## 创建规则
{: #criteria}

规则定义了策略用于判断成功或失败的条件。您可创建“单元测试和测试覆盖”策略，其中包含单元测试规则（需要 80% 的单元测试成功）和测试覆盖规则（需要 100% 代码覆盖）。如果在管道中添加了引用此规则的检测点，那么该检测点可阻止不能同时满足这两个规则的任何构建继续进行。 

您可以通过将测试标记为“重要”，从而要求测试在任何情况下都必须成功。要创建规则，请选择策略，然后单击**向策略添加规则**。 

### 创建功能验证测试规则
{: #criteria_fvt}

1. 键入描述并选择格式。

2. 指定必须通过并声明成功的测试用例百分比。

3. 定义重要的任何测试用例。

4. 要监视测试用例回归，请选中**监视测试用例回归**复选框。

5. 单击**保存**。


### 创建单元测试规则
{: #criteria_ut}

1. 键入描述并选择格式。

2. 指定必须通过并声明成功的测试用例百分比。

3. 定义重要的任何测试用例。

4. 要监视测试用例回归，请选中**监视测试用例回归**复选框。

5. 单击**保存**。


### 创建代码覆盖规则
{: #criteria_codecoverage}

1. 键入描述并选择格式。

2. 指定需要声明成功的代码覆盖百分比。

3. 要监视代码覆盖回归，请选中**监视测试用例回归**复选框。

4. 单击**保存**。

### 创建静态安全扫描规则
{: #criteria_static}

1. 输入描述。

2. 指定规则允许的高严重性、中等严重性和低严重性问题的最大数量。 

3. 单击**保存**。

### 创建动态安全扫描规则
{: #criteria_dynamic}

1. 输入描述。

2. 指定规则允许的高严重性、中等严重性和低严重性问题的最大数量。 

3. 单击**保存**。

## 测试结果格式和工具

{{site.data.keyword.DRA_short}} 支持以下类型的度量和格式：

* 功能验证测试（Mocha、xUnit）
* 单元测试（Mocha、xUnit、Karma/Mocha）
* 代码覆盖（作为 JSON 摘要报告格式的 Istanbul、Blanket.js）

{{site.data.keyword.DRA_short}} 还支持 Selenium 和 Jasmine 测试。这些测试必须包含在官方支持的工具中，如 xUnit 和 Mocha。要了解有关同时使用 {{site.data.keyword.deliverypipeline}}、{{site.data.keyword.DRA_short}} 和 Selenium 的更多信息，请参阅[在 Delivery Pipeline 上从命令行运行 Selenium 测试](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/)。

对于具有测试用例的项，您可以指定重要测试用例，即不管可接受的百分比而必须通过的测试。重要测试用例名称必须匹配测试用例的 `full title` 属性。    
* 对于 Karma/Mocha 测试，`describe()` 和 `it()` 描述字符串通过空格链接在一起。
* 对于 xUnit 测试，程序包名、类名和函数名通过空格链接在一起。在以下示例中对此进行了说明：
  ```
  <testsuites package="test">
    <testsuite package="otc-api" name="PUT Service Instances - Test Setup" tests="2" failures="0" errors="0">
      <testcase name="#1 Authorization passed for mock user: idsb3t1@us.ibm.com"/>
      <testcase name="#2 Authorization passed for mock user: idsb3t4@us.ibm.com"/>
    </testsuite>
  </testsuite>
  ```
  该示例生成以下测试用例名称：
  ```
  test otc-api PUT Service Instances - Test Setup #1 Authorization passed for mock user: idsb3t1@us.ibm.com
  test otc-api PUT Service Instances - Test Setup #2 Authorization passed for mock user: idsb3t1@us.ibm.com
  ```

您可以通过向管道添加 Sauce Labs 工具集成，将 Sauce Labs 与 {{site.data.keyword.DRA_short}} 一起使用。然后，将 `SAUCE_USERNAME` 和 `SAUCE_ACCESS_KEY` 环境变量作为凭证引入 Selenium 测试。

您可以在运行之后，在日志中查看所有测试的完整标题。  

**注：**
* {{site.data.keyword.DRA_short}} 不支持在完整标题中包含连字符的重要测试。    
* 如果您更改组织名称，那么您必须重新创建与之前名称相关联的策略。您将丢失对名称更改之前所生成的任何决策报告的访问权。

## 查看决策报告    
{: #DI_decision_reports}

在管道运行后，{{site.data.keyword.DRA_short}} 会开始从管道收集并分析测试结果，以建立基线。它会收集每个后续运行所产生的数据并与之前的结果进行比较。决策检测点使用此数据来确定何时停止部署。 

要查看管道中某个检测点的决策报告，请完成以下步骤：

   1. 在包含要检查的检测点的阶段上，单击**查看日志和历史记录**。

   2. 在包含检测点的作业中，单击检测点的名称。

   3. 在日志视图中，找到“`在此处查看 {{site.data.keyword.DRA_short}} 报告`”消息并单击链接以打开报告。
