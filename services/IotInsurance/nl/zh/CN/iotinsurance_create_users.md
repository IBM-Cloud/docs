---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# 创建用户和保障关联
{: #gettingstartedtemplate}
上次更新时间：2016 年 9 月 15 日
{: .last-updated}

创建 {{site.data.keyword.iotinsurance_short}} 服务并部署所需的支持服务和应用程序之后，您可以通过创建授权用户和保障关联来测试服务。
{:shortdesc}

**先决条件：**开始之前，请确保满足以下先决条件：

- 已在计算机上安装 [Node.js](https://nodejs.org/en/)。  
- 支持 Node.js 的运行时环境，例如 Eclipse。
- Git 软件以及对 [API 示例的 GitHub 源代码存储库](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)的访问权。或者，您可以下载[带有源代码文件的归档](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip)。
- 准备好的源代码。要准备源代码，请完成以下步骤：
  1. 将 [GitHub 源代码存储库](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)克隆或下载到您的计算机。
  2. 通过使用命令提示符转至包含克隆的源代码文件的文件夹并运行 `npm install` 命令来安装项目的开放式源代码必备软件。

创建一个用户，用来测试仪表板和样本移动应用程序的功能。

1. 在 {{site.data.keyword.iotinsurance_short}} 系统中创建用户。
  1. 编辑 createUser.js 文件以将 **user** 变量中的值替换为非重复用户信息。
  2. 保存文件。
  3. 运行 `node createUser.js`。完成此过程需要几分钟时间。
  4. 记下用户名；在下一步骤中需要该用户名。
2. 创建用户的保障关联。
  1. 编辑 createUserShieldAssociation.js 文件以在 **username** 变量中添加先前步骤中的用户名。

  2. 保存文件。
  3. 运行 `node createUserShieldAssociation.js`。有关保障的更多信息，请参阅[组件](iotinsurance_overview.html#components})。
3. （可选）分析引擎将自动更新；但是，如果未显示正确的数据，您可以通过运行 `node updateAnalyticsEngine.js` 刷新分析引擎。
4. （可选）为用户模拟危险事件。
  1. 编辑 simulateHazard.js 文件以在 **usr** 变量中添加先前步骤中的用户名。
  2. 保存文件。
  3. 运行 `node simulateHazard.js`。
5. （可选）通过运行 `node createHistoricalData.js` 创建模拟历史数据集。


# 相关链接
{: #rellinks}

## API 参考
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API 示例](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## 相关链接
{: #general}
* [开发人员支持论坛](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [堆栈溢出支持论坛](http://stackoverflow.com/questions/tagged/ibm-bluemix)
