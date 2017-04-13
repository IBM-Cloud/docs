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

# 非唯一性鏈碼
{: #ndcc}


IBM Blockchain 網路只支援唯一性鏈碼。在任何區塊鏈網路上都不支援使用非唯一性鏈碼，且會導致重大錯誤。{:shortdesc}

**非唯一性鏈碼** 是指跨越時間和節點，**不會**在區塊鏈分類帳上導致相同附加值的任何鏈碼。相反地，**唯一性鏈碼** 則會在區塊鏈分類帳上，跨越時間和節點，一律產生相同的附加值。

### 唯一性鏈碼範例
一律將變數值加一的 **invoke** 交易是唯一性的，因為結果在每個節點上都一律相同，不會有變化。例如，每當對固定值五執行這個交易時，附加的值在每個節點上、每次都一律是六。唯一性鏈碼的網路結果不會在區塊鏈中造成分歧；每個節點上的分類帳副本一律會指出（在同步化之後）值比前一次呼叫多一。

### 非唯一性鏈碼範例
根據當日開始 (00:00) 之後經歷的秒數來增加區塊鏈變數值的 **invoke** 交易，則是非唯一性的，因為值會隨著時間不同而在各節點之間變化。例如，每次對固定值「五」執行這個交易時，附加的值會在各節點不同（罕有例外），因為自 00:00 起經歷的秒數勢必會變化。這個非唯一性鏈碼的網路結果就是分歧的區塊鏈；所有節點無法針對「五 + 自 00:00 起經歷秒數」的值達成一致。

### 隨機性
鏈碼跨越時間和節點，對於附加的值都不能有任何隨機性。任何隨機性都會在各節點之間造成分歧的區塊鏈，然後就必須由網路來解決此現象。為了避免隨機性，您必須確保不會有任何平行鏈碼影響來自呼叫鏈碼的輸入值。例如，請勿同時執行任何 **query** 交易和 **invoke** 交易，因為平行查詢可能會在各節點之間的呼叫值產生變化。

### 使用廣域變數
使用廣域變數或實例變數來儲存從分類帳中擷取的值或在分類帳上設定值，可能會導致非唯一性。鏈碼不應該根據在重新啟動鏈碼容器時不會保留其狀態的廣域變數或實例變數。以下是使用廣域變數的範例；透過 `stub.PutState` 函數寫入分類帳的 `key` 值，是衍生自廣域變數：

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### 反覆運算對映類型
反覆運算對映類型可能導致非唯一性，因為順序在 Go 程式設計語言中不具唯一性。下列範例說明如何反覆運算名為 `columnTypes` 的對映：

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
