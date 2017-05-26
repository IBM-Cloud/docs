---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 创建策略和规则
{: #policies_and_rules}

策略是规则集，用于控制 Delivery Pipeline 中的检测点。如果您的代码不符合或超出在特定检测点执行的策略，那么会暂停部署以防止发布有风险的更改。

您可在 {{site.data.keyword.DRA_short}} 中定义策略。这将在包含 {{site.data.keyword.DRA_short}} 的 {{site.data.keyword.Bluemix_notm}} 组织中创建策略。相同组织中的任何应用程序都可以使用该策略。 

## 创建策略
{: #create_policies}

要创建策略，请执行以下操作：

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
{: #creating_rules}

规则定义了策略用于判断成功或失败的条件。您可创建“单元测试和测试覆盖”策略，其中包含单元测试规则（需要 80% 的单元测试成功）和测试覆盖规则（需要 100% 代码覆盖）。如果在管道中添加了引用此规则的检测点，那么该检测点可阻止不能同时满足这两个规则的任何构建继续进行。 

您可以通过将测试标记为“重要”，从而要求测试在任何情况下都必须成功。要创建规则，请选择策略，然后单击**向策略添加规则**。 

### 创建功能验证测试规则
{: #criteria_fvt}

1. 键入描述并选择格式。

2. 指定必须通过声明成功的测试用例百分比。

3. 定义重要的任何测试用例。

4. 要监视测试用例回归，请选中**监视测试用例回归**复选框。

5. 单击**保存**。


### 创建单元测试规则
{: #criteria_ut}

1. 键入描述并选择格式。

2. 指定必须通过声明成功的测试用例百分比。

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

可以将 {{site.data.keyword.DRA_short}} 与 IBM Application Security on Cloud 相集成，以运行静态代码和动态应用程序扫描。有关 Application Security on Cloud 的更多信息，请参阅[正式文档](/docs/services/ApplicationSecurityonCloud/index.html)。

1. 输入描述。

2. 指定规则允许的高严重性、中等严重性和低严重性问题的最大数量。 

3. 单击**保存**。

### 创建动态安全扫描规则
{: #criteria_dynamic}

可以将 {{site.data.keyword.DRA_short}} 与 {{site.data.keyword.appseccloudfull}} 相集成以运行动态应用程序扫描。有关 Application Security on Cloud 的更多信息，请参阅[正式文档](/docs/services/ApplicationSecurityonCloud/index.html)。

1. 输入描述。

2. 指定规则允许的高严重性、中等严重性和低严重性问题的最大数量。 

3. 单击**保存**。
