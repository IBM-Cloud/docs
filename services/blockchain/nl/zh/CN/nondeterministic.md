---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-01"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 非确定性链代码
{: #ndcc}


IBM Blockchain 网络只支持确定性链代码。在任何区块链网络上都不支持使用非确定性链代码，这将导致严重错误。
{:shortdesc}

**非确定性链代码**是指在区块链分类帐上随时间推移以及在不同节点上**不会**生成相同附加值的任何链代码。相反，**确定性链代码**在区块链分类帐上随时间推移以及在不同节点上始终会生成相同的附加值。

### 确定性链代码示例
始终会使变量值递增 1 的 **invoke** 交易是确定性的，因为结果在每个节点上始终都相同，没有任何差异。例如，每当对固定值 5 运行此交易时，附加值每次在每个节点上都始终为 6。确定性链代码的网络结果是在区块链中完全一样；分类帐在每个节点上的副本始终指示（在同步后）本次调用的值比上次调用大 1。

### 非确定性链代码示例
使区块链变量的值递增自日初 (00:00) 起所经过秒数的 **invoke** 交易是非确定性的，因为随时间推移不同节点上的值会有差异。例如，每次对固定值 5 运行此交易时，附加值在不同节点上各不相同（罕有例外），因为自 00:00 起经过的秒数肯定会有所不同。此非确定性链代码的网络结果是各不相同的区块链；值 5 加上自 00:00 起经过的秒数所得到的结果在所有节点上并不一致。

### 随机性
链代码的附加值随时间推移以及在不同节点上不得表现出随机性。任何随机性都会在不同节点上生成不同的区块链，随后必须由网络来解析这些区块链。为了避免随机性，必须确保没有并行链代码会影响来自调用链代码的输入值。例如，请勿将任何 **query** 交易与 **invoke** 交易并行运行，因为并行查询可能会使不同节点上的调用值产生差异。

### 使用全局变量
使用全局或实例变量来存储从分类帐检索到的值，或者在分类帐上设置值，可能会导致非确定性。链代码不应该依赖在跨链代码容器重新启动时未保留其状态的全局或实例变量。以下是使用全局变量的示例：`key` 的值，通过 `stub.PutState` 函数该值会写入分类账，且从全局变量衍生：

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### 迭代映射类型
在映射类型上进行迭代可能会导致非确定性，这是因为较旧的顺序在 Go 编程语言中是非确定性的。以下是在名为 `columnTypes` 的映射上进行迭代的示例：

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
