---

copyright:
  years: 2016
lastupdated: "2016-11-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 样本应用程序和教程
{: #1stanchor}


以下样本演示了应用程序和链代码在测试 IBM Blockchain 网络上是如何工作的。要了解有关支持 IBM Blockchain 网络的 Hyperledger Fabric V0.6 代码的更多信息，请访问 Linux Foundation 的 Hyperledger 项目的 [Fabric 文档](https://github.com/hyperledger/fabric/tree/v0.6/docs)。  
{:shortdesc}

要体验运行中的链代码应用程序，可以立即部署下面的 Marbles、Commercial Paper 或 Car Lease 演示（单击“部署到 Bluemix”按钮）。或者，继续阅读以探索 Hello Chaincode 教程。

- [![部署到 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  **Marbles**
- [![部署到 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  **Commercial Paper**
- [![部署到 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  **Car Lease**  

<br>
## 学习链代码教程
{: #hellocc}
本教程指导您逐步完成使用基本构建块对基础链代码应用程序进行编码的过程。您将以渐进方式构建有效的链代码，以创建用于在网络上进行交换的通用资产。接着，您将通过网络 API 与链代码进行交互。完成本教程后，您将能回答以下问题：
- 什么是链代码？
- 如何实现链代码？
- 存在哪些依赖关系？
- 什么是主函数？
- 如果将不同的值传递到自变量？
- 如何在我的网络上安全登记用户？
- 如何编译链代码？
- 如何通过 REST API 与链代码进行交互？

### 什么是链代码？
链代码是 Go (Golang) 或 Java 代码，支持用户与区块链网络进行交互。每当在网络上“调用”交易时，都将调用链代码中的函数，以读取分类帐的值以及将值写入分类帐。  

<br>
## 设置开发环境
要开始开发链代码，请首先安装以下依赖项和建议的工具：

### Git

- [Git 下载页面](https://git-scm.com/downloads)
- [Pro Git 书籍](https://git-scm.com/book/en/v2)
- [Git Desktop（Git CLI 的替代工具）](https://desktop.github.com/)

Git 是一个运行速度快、功能强大的版本控制工具，用于链代码开发和常规软件开发。Git Bash 随 Git for Windows 一起安装，是建议使用的命令行终端。

完成 Git 安装后，请验证 Git 是否已正确安装：

```
$ git version
git version 2.9.0.windows.1
```

一旦 Git 安装后，请在 [GitHub](https://github.com/) 上为自己创建帐户。IBM Blockchain on Bluemix 服务要求链代码位于 GitHub 存储库中，才可通过 REST API 进行部署。  

## Go

Go 目前是 Bluemix 上唯一支持的用于编写链代码的语言。Go 安装包含一组非常有用的工具，可用于编写链代码。例如，`go build` 命令允许在尝试将链代码部署到网络之前，先对其进行编译。请安装 Go V1.6，这是用于开发 Hyperledger Fabric V0.6 的版本：  

- [Go 1.6 安装](https://golang.org/dl/#go1.6.3)
- [Go 安装指示信息](https://golang.org/doc/install)
- [Go 文档和教程](https://golang.org/doc/)

通过运行以下命令，验证 Go 是否已正确安装。`go version` 命令的输出会根据操作系统而变化：

```
$ go version
go version go1.6.3 windows/amd64

$ echo $GOPATH
C:\gopath
```

`GOPATH` 环境变量不必与上面的示例一样，但必须使用文件系统上的有效目录。运行 `go build` 来验证链代码是否编译时，Go 会在 `$GOPATH/src` 目录中查找列在链代码的 `import` 块中的任何非标准依赖项。[Go 安装指示信息](https://golang.org/doc/install)将指导您完成 GOPATH 环境变量设置。  

<br>
## Hyperledger Fabric

Blockchain on Bluemix 支持两个版本的 Hyperledger Fabric：V0.5 和 V0.6。如下所述，链代码版本必须与 Bluemix 网络上的 Hyperledger 版本一致。

注意：
1. 要对分类帐启用 read 和 write 函数，链代码必须从 Hyperledger Fabric 导入链代码垫片。
2. 要本地编译链代码，必须在 `GOPATH` 环境变量中指定 Hyperledger Fabric 代码位置。

要确定 Bluemix 实例运行的 Hyperledger Fabric 的版本，请单击“仪表板监视器”上的**服务状态**选项卡。向下滚动到**发行说明**部分；“`您的网络使用的是以下版本`”面板将显示运行的 **Hyperledger 落实级别**：

![Bluemix 后端版本](images/fabricversion.png "Bluemix 后端版本")
图 1. Hyperledger Fabric 版本

链代码版本必须与将链代码部署到的 Hyperledger Fabric 版本一致。例如，图 1 中显示的网络需要克隆 Hyperledger Fabric V0.6（预览）代码库。对于任一版本，Fabric 代码库都必须存储在 `$GOPATH/hyperledger/fabric` 路径中：

- [V0.5 Hyperledger Fabric](https://github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview)
- [V0.6 HHyperledger Fabric](https://gerrit.hyperledger.org/r/gitweb?p=fabric.git;a=shortlog;h=refs/heads/v0.6)

要安装 Hyperledger Fabric V0.5 代码库，请使用以下 git clone 命令：

```
# 在 GOPATH 上创建父目录
mkdir -p $GOPATH/src/github.com/hyperledger
cd $GOAPTH/src/github.com/hyperledger

# 将相应的发行版代码库克隆到 $GOPATH/src/github.com/hyperledger/fabric 中
# 请注意，V0.5 发行版是存储库的分支。下面对其进行了定义（位于 -b 自变量后）
git clone -b v0.5-developer-preview https://github.com/hyperledger-archives/fabric.git
```

要安装 Hyperledger Fabric V0.6 代码库，请使用以下 git clone 命令：

```
# V0.6 发行版作为 Gerrit 光纤网存储库内部的分支存在
git clone -b v0.6 http://gerrit.hyperledger.org/r/fabric
```

如果 Fabric 未正确安装在 `GOPATH` 中，那么构建链代码将返回类似于以下示例的错误：
```
$ go build .
chaincode_example02.go:27:2: cannot find package "github.com/hyperledger/fabric/core/chaincode/shim" in any of:
        C:\Go\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOROOT)
        C:\gopath\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOPATH)
```

### 设置开发管道

使用以下步骤设置管道，用于编写、构建和测试链代码。您将在本地计算机上编写链代码，验证其是否编译，以及将其上传到 GitHub。然后，您将使用 Fabric REST API 在 Bluemix 网络上测试链代码：

1. 针对网络版本，将[学习链代码](https://github.com/IBM-Blockchain/learn-chaincode)存储库的相应版本派生到您的 GitHub 帐户。对于 V0.5 Fabric 网络，请派生 V1.0，或者对于 V0.6 Fabric 网络，请派生 V2.0。一种选择是使用位于存储库页面右上角的**派生**按钮。派生会将整个存储库复制到本地计算机，包括所有分支；分支可通过单击页面左上角的**分支：**按钮来显示。要使用 CLI 进行派生，请将以下命令输入到 Git Bash shell 中：

2. 将派生克隆到 $GOPATH：

  ```bash
  cd $GOPATH
  mkdir -p src/github.com/<YOUR_GITHUB_ID_HERE>/
  cd src/github.com/<YOUR_GITHUB_ID_HERE>/
  git clone -b v1.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  或
  git clone -b v2.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  ```

  现在，您在本地计算机上具有派生的副本。您将通过更改或添加本地文件来编写链代码，将其推送到 GitHub 上的派生，然后使用网络同级上的 REST API 将链代码部署到区块链网络。

3. 提供了本教程中使用的两个版本的链代码：**start** 是将从其开始的框架链代码，**finished* 是可供构建的已完成链代码。首先，请确保 **start** 在本地环境中构建：

  ```bash
  cd $GOPATH/src/github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/start
  go build ./
  ```

**start** 版本的学习链代码在编译时应该不会包含任何错误或消息。如果包含任何错误或消息，请查看先前的指示信息以正确安装 Go。

5. 将更改写入本地链代码文件，然后将更新后的文件推送到 GitHub 派生：

  ```bash
  cd $GOPATH/src/github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/
  # 查看本地更改了哪些文件。您应该会看到 chaincode_start.go
  git status
  # 对本地存储库中的所有更改编译打包以进行落实
  git add --all
  # 落实所有编译打包的更改。在 -m 自变量后插入简短描述
  git commit -m "Compiled my code"
  # 将本地落实推送回 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/
  git push
  ```

#### 实现链代码接口
下一步是在 Go 代码中实现链代码垫片接口。三个主函数为 **Init**、**Invoke** 和 **Query**。这三个函数都会将函数名和字符串数组用作输入，但调用点各不相同。开发路径以用于创建通用资产以在区块链网络上进行交换的工作链代码结尾。

### 依赖项
`import` 语句列出用于构建链代码的依赖项：
1. `fmt` - 包含用于调试/日志记录的 `Println`。
2. `errors` - 标准 Go 错误格式。
3. `github.com/hyperledger/fabric/core/chaincode/shim` - 用于将 Golang 代码与网络同级连接在一起的代码。

#### Init()
首次部署链代码时，将调用 `Init` 函数。顾名思义，使用此函数可初始化链代码。在此示例中，`Init` 用于配置分类帐上单个键/值对的初始状态。

在 `chaincode_start.go` 文件中更改 `Init` 函数，使其将第一个 `args` 元素存储到键“hello_world”中：

```go
func (t *SimpleChaincode) Init(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
	if len(args) != 1 {
		return nil, errors.New("Incorrect number of arguments. Expecting 1")
	}

	err := stub.PutState("hello_world", []byte(args[0]))
	if err != nil {
		return nil, err
	}

	return nil, nil
}
```

这可使用存根函数 `stub.PutState` 来完成。此函数将部署请求中发送的第一个自变量解释为要存储在键“hello_world”下的值。如果由于传递的自变量数不正确或因为写入分类帐时有问题而发生错误，那么此函数会返回错误。否则，此函数将完全退出，不返回任何消息。  

#### Invoke()
使用 `Invoke` 函数可调用链代码函数在区块链网络上执行“真正的工作”。Invoke 函数会捕获为交易，随后这些交易分组成块，以写入分类帐。更新分类帐可通过调用链代码来实现。`Invoke` 的结构非常简单；它接收函数和自变量数组。根据调用请求中 function 参数传入的函数，`Invoke` 将调用助手函数或返回错误。

在 `chaincode_start.go` 文件中更改 `Invoke` 函数，使其调用常规 write 函数。

```go
func (t *SimpleChaincode) Invoke(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
	fmt.Println("invoke is running " + function)

	// Handle different functions
	if function == "init" {
		return t.Init(stub, "init", args)
	} else if function == "write" {
		return t.write(stub, args)
	}
	fmt.Println("invoke did not find func: " + function)

	return nil, errors.New("Received unknown function invocation")
}
```

现在，代码将查找 `write`，所以请将 write 函数添加到 `chaincode_start.go` 文件：

```go
func (t *SimpleChaincode) write(stub shim.ChaincodeStubInterface, args []string) ([]byte, error) {
	var name, value string
	var err error
	fmt.Println("running write()")

	if len(args) != 2 {
		return nil, errors.New("Incorrect number of arguments. Expecting 2. name of the variable and value to set")
	}

	name = args[0]                            //rename for fun
	value = args[1]
	err = stub.PutState(name, []byte(value))  //write the variable into the chaincode state
	if err != nil {
		return nil, err
	}
	return nil, nil
}
```

此 `write` 函数应该类似于先前的 `Init` 更改。现在，可以设置 `PutState` 的键和值，这允许您在区块链分类帐上存储任何键/值对。

#### Query()
调用 `Query` 函数可查询链代码状态，而不会向链（分类帐）添加区块。只有 deploy 和 invoke 函数可添加新区块。使用 `Query` 可读取链代码状态的键/值对的值。

在 `chaincode_start.go` 文件中更改 `Invoke` 函数，使其调用通用 read 函数：

```go
func (t *SimpleChaincode) Query(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
	fmt.Println("query is running " + function)

	// Handle different functions
	if function == "read" {                            //read a variable
		return t.read(stub, args)
	}
	fmt.Println("query did not find func: " + function)

	return nil, errors.New("Received unknown function query")
}
```

现在，代码将查找 `read`，所以请将“read”函数添加到 `chaincode_start.go` 文件：

```go
func (t *SimpleChaincode) read(stub shim.ChaincodeStubInterface, args []string) ([]byte, error) {
	var name, jsonResp string
	var err error

	if len(args) != 1 {
		return nil, errors.New("Incorrect number of arguments. Expecting name of the var to query")
	}

	name = args[0]
	valAsbytes, err := stub.GetState(name)
	if err != nil {
		jsonResp = "{\"Error\":\"Failed to get state for " + name + "\"}"
		return nil, errors.New(jsonResp)
	}

	return valAsbytes, nil
}
```

此 `read` 函数使用 `GetState`，后者是对 `PutState` 的补充。此垫片函数只采用一个字符串自变量：要检索的键的名称。接着，此函数会向 `Query` 返回字节数组形式的值，然后 Query 会将此值发送到 REST 处理程序。

#### Main()
`main` 函数在每个同级部署其链代码实例时执行。此函数会启动链代码，并向同级进行注册。“main”无需进行代码更新；chaincode_start.go 和 chaincode_finished.go 文件的顶部都包含一个 `main` 函数：

```go
func main() {
	err := shim.Start(new(SimpleChaincode))
	if err != nil {
		fmt.Printf("Error starting Simple chaincode: %s", err)
	}
}
```

### 与链代码进行交互
测试链代码的最快方法是在同级上使用 REST 接口。Bluemix 仪表板监视器上的 Swagger UI 允许您试验部署链代码，而不编写任何额外的代码。  

#### Swagger API
要使用 Swagger API，请完成以下步骤：

1. 登录到 [Bluemix](https://console.ng.bluemix.net/login)，并确保您位于**仪表板**选项卡上。
1. 检查您是否位于包含 IBM Blockchain 服务的同一 Bluemix“空间”中。空间导航位于左侧。
1. 在底部附近有**服务**面板；单击 IBM Blockchain 服务。
1. 您应该会看到“欢迎使用 IBM Blockchain...”消息；单击右侧的**启动**按钮。
1. 在“监视器”页面上，您应该会看到两张表；底部表可能为空。
	- **“网络”选项卡：**
		- **同级日志**位于顶部表中。在**同级 1** 对应的行中，单击“文件”图标以查看日志。除了此静态视图外，在该页面顶部附近的**查看日志**选项卡中还有实时**流式采集同级日志**。
		- **链代码日志**位于底部表中。每个链代码都标记有部署该链代码时返回的链代码散列。选择任一链代码行中的同级，然后单击“文件”图标以查看日志。
	- **API 选项卡**：显示“Swagger API 文档”页面。
1. 继续执行以下步骤来实现安全登记。调用 REST 接口中的 `/chaincode` 端点需要安全上下文标识。要使大部分 REST 调用能够被接受，必须传递服务凭证列表中的已注册 *enrollID*：
  - 单击 **+ 网络的登记标识**以展开 *enrollID* 值及其密钥的列表。
  - 将凭证集复制到文本文件以供将来使用。
  - 展开**注册器** API 部分。
  - 展开 `POST /registrar` 部分。
  - 使用凭证中指定 `enrollID` 和“enrollSecret”的 JSON 填充`值`字段：

  ![注册示例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/registrar.PNG "注册示例")

  *响应主体*应该看起来类似以下示例：

  ![注册示例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/register_response.PNG "注册示例响应主体")

现在，您已设置 `enrollID`，可以在以下步骤中部署、调用和查询链代码时使用此标识。
### 部署链代码
为了通过 REST 接口部署链代码，链代码必须存储在公共 GitHub 存储库中。向同级发送部署请求时，请指定链代码存储库的 URL 以及用于初始化链代码的参数。

对链代码进行**部署之前**，请验证链代码是否为本地构建的：
1. 打开命令提示符，然后浏览到包含 `chaincode_start.go` 的目录。输入以下命令：
	```
	go build ./
	```
1. 展开**链代码** API 部分。
1. 展开 `POST /chaincode` 部分。
1. 使用以下示例代码设置 `DeploySpec` 文本字段（使其他字段为空白），指定链代码存储库路径，以及先前 `/registrar` 步骤中的 `enrollID`。`"path":` 应该类似于以下内容：`"https://github.com/johndoe/learn-chaincode/finished"`。这是存储库派生的路径，加上 chaincode_finished.go 文件的路径：

	```
	{
		"jsonrpc": "2.0",
 "method": "deploy",
 "params": {
 "type": 1,
      "chaincodeID":{
      "path": "https://github.com/ibm-blockchain/learn-chaincode/finished"
			},
      "ctorMsg": {
      "function": "init",
				"args": [
					"hi there"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 1
	}
	```

  *响应主体*应该看起来类似以下示例：

  ![部署示例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/deploy_response.PNG "部署示例响应主体")

  部署的响应将包含此链代码的标识。标识为 128 个字符的字母数字散列，可用于未来的调用或查询请求。将此标识复制到文本编辑器。

#### Query
在链代码中查询 `hello_world` 键的值，此键是使用 `Init` 函数设置的：
1. 展开**链代码** API 部分。
1. 展开 `POST /chaincode` 部分。
1. 使用以下示例填充 `QuerySpec` 文本字段（使其他字段为空白），指定先前部署步骤中的链代码标识，以及先前 `/registrar` 步骤中的 `enrollID`：

	```
	{
		"jsonrpc": "2.0",
		"method": "query",
		"params": {
			"type": 1,
      "chaincodeID":{
      "name": "CHAINCODE_HASH_HERE"
			},
      "ctorMsg": {
      "function": "read",
				"args": [
					"hello_world"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 2
	}
	```
“*响应主体”应该看起来类似以下示例：

  ![查询示例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query_response.PNG "查询示例响应主体")

  `hello_world` 的值为“hi there”这是由先前 deploy 调用主体设置的。

#### 调用
通过 `invoke` 调用通用 write 函数。将 `hello_world` 的值更改为 "go away"：
1. 展开**链代码** API 部分。
1. 展开 `POST /chaincode` 部分。
1. 使用以下示例填充 `InvokeSpec` 文本字段（使其他字段为空白），指定先前部署步骤中的链代码标识，以及先前 `/registrar` 步骤中的 `enrollID`：

	```
	{
		"jsonrpc": "2.0",
		"method": "invoke",
		"params": {
			"type": 1,
      "chaincodeID":{
      "name": "CHAINCODE_HASH_HERE"
			},
      "ctorMsg": {
      "function": "write",
				"args": [
					"hello_world",
					"go away"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 3
	}
	```
“*响应主体”应该看起来类似以下示例：

  ![调用示例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/invoke_response.PNG "调用示例响应主体")

  重新运行上面的查询，您应该会获得以下响应：


  ![Query2 示例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query2_response.PNG "调用示例响应")

您刚刚完成了编写一些基本链代码的过程。  

<br>
## 演示需求
{: #requirements}

Bluemix 服务随附以下先决条件，这些先决条件对于运行 Marbles、Commercial Paper 和 Car Lease 演示应用程序是必需的。您的 Bluemix 环境克隆了 Hyperledger Fabric 来提供以下依赖项：

- Bluemix 标识 https://console.ng.bluemix.net/（必需，用于创建 IBM Blockchain 网络并为同级和认证中心提供服务凭证）
- Node.js 0.12.0+ 和 npm v2+
- Golang 环境（仅当构建自己的链代码时必需）

这些演示还需要熟练使用 Node.js 和 Express 模块。您还必须对区块链上下文中的“链代码”、“分类帐”和“同级”有概念性的了解；请参阅 [Hyperledger Fabric 词汇表](https://github.com/hyperledger/fabric/blob/v0.6/docs/glossary.md)。  

<br>
## Marbles 演示
{: #marbles}

Marbles 应用程序演示两个参与方之间的简单资产转移。该应用程序旨在测试 JavaScript SDK，指导其开发，以及帮助开发者熟悉该 SDK 和链代码。

探索 [Marbles 教程](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md)，以了解 Web 应用程序、SDK 和链代码如何一起工作。如果已经熟悉链代码和 IBM Blockchain，那么可以将该演示[手动部署](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#)到 Bluemix，或者单击“部署到 Bluemix”按钮来使用该 Web 应用程序：
  
[![部署到 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  

<br>
## Commercial Paper 演示
{: #commercialpaper}

Commercial Paper 应用程序演示可以如何使用 IBM Blockchain 来实现商业票据交易网络。Commercial Paper 演示探索获得许可的区块链网络，在该网络上，会为参与者分配角色和相应的访问级别。请访问 [Commercial Paper 自述文件](https://github.com/IBM-Blockchain/cp-web#readme)，以了解有关此演示的组件的更多信息，或将其立即部署到 Bluemix 以查看运行中的交易网络：
  
[![部署到 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  

<br>
## Car Lease 演示
{: #carlease}

Car Lease 应用程序演示车辆的生命周期，从制造开始，经过一系列的车主之手，到车辆报废结束。该演示将 Node.js 用于服务器端编程，并将 Golang 用于在 IBM Blockchain 网络上运行的链代码。该演示包含两个链代码实例：一个定义车辆交易的规则，另一个记录车辆生命周期内的所有车辆交易。这两个链代码程序都使用 JSON 对象来存储数据。请访问 [Car Lease 自述文件](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md)，以了解有关该应用程序体系结构以及与此演示关联的车辆属性的更多信息，或者将演示立即部署到 Bluemix：
  
[![部署到 Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  

<br>

<!-- comment out - moving to separate file for now jh
## Non-deterministic chaincode
{: #ndcc}

IBM Blockchain networks support deterministic chaincode only. Using non-deterministic chaincode is not supported, and will cause severe errors, on any blockchain network.

**Non-deterministic chaincode** is any chaincode that does **not** result in the same appended value, over time and across nodes, on the blockchain ledger. By contrast, **deterministic chaincode** always produces the same appended value, over time and across nodes, on the blockchain ledger.

### Deterministic chaincode example
An **invoke** transaction that always increments the value of a variable by one is deterministic, because the result is always the same, on every node, without variance. Whenever this transaction is run against a fixed value of five, for example, the appended value is always six, on every node, every time. The network outcome for deterministic chaincode is no divergence in the blockchain; the copy of the ledger on each node always indicates (after syncing) that the value is one greater than the previous invocation.

### Non-deterministic chaincode example
An **invoke** transaction that increments the value of a blockchain variable with the number of elapsed seconds since the start of the day (00:00) is non-deterministic, because over time the value will vary across nodes. Each time this transaction is run against a fixed value of five, for example, the appended value diverges across nodes (with rare exceptions), because the number of elapsed seconds since 00:00 will inevitably vary. The network outcome for this non-deterministic chaincode is divergent blockchains; all nodes will not agree on the value of five + the number of elapsed seconds since 00:00.

### Randomness
Chaincode must exhibit no randomness in the appended values, over time and across nodes. Any randomness produces divergent blockchains across nodes, which must then be resolved by the network. To avoid randomness, you must ensure that no parallel chaincode can affect the input value from invocation chaincode. For example, do not run any **query** transactions in parallel with **invoke** transactions, because parallel queries could produce variance in the invocation values across nodes.

### Using a global variable
Using a global or instance variable to store a value that was retrieved from the ledger, or to set a value on the ledger, can lead to non-determinism. Chaincode should not rely on global or instance variables that will not retain their state across restarts of a chaincode container. The following is an example that uses a global variable; the value of `key`, which is written to the ledger via the `stub.PutState` function, is derived from a global variable:

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### Iterating over a map type
Iteration over a map type can lead to non-determinism, because order is not deterministic in the Go programming language. The following is an example of iteration over the map named `columnTypes`:

```go
 func generateColumns(colTypes map[string]string, colKeys []bool) ([]*shim.ColumnDefinition, error) {
	var tableColumns []*shim.ColumnDefinition
	keyIndex := 0
	for k, _ := range colTypes {
		tableColumns = append(tableColumns, &shim.ColumnDefinition{k, shim.ColumnDefinition_STRING, colKeys[keyIndex]})

		keyIndex++
	}
	return tableColumns, nil
}
```

-->


<!-- ## Using the Node.js SDK
{: #nodesdk}

Use the [Hyperledger fabric client SDK ](https://github.com/IBM-Blockchain/ibm-blockchain-js/blob/master/README.md) library for easier interaction with an IBM Blockchain network.  The SDK, through importing packages and libraries, allows for an application developer to build Node.js applications that can invoke functionality on the blockchain network from the client side.  Member services and asset management are now pluggable components on client side applications.  See the [Enhanced Node.js SDK](etn_sdk.html) section for full documentation and application examples. -->
