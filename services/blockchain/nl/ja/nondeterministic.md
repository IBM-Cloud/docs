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

# 非決定論的チェーンコード
{: #ndcc}


IBM Blockchain ネットワークは決定論的なチェーンコードのみをサポートします。非決定論的なチェーンコードの使用はサポートされておらず、どのブロックチェーン・ネットワークでも重大エラーが発生します。{:shortdesc}

**非決定論的チェーンコード**とは、時間が経過しても、ノード間のブロックチェーン台帳で同じ値が付加**されない**あらゆるチェーンコードです。これとは対照的に、**決定論的チェーンコード**では、時間が経過しても、ノード間のブロックチェーン台帳で常に同じ値が付加されます。

### 決定論的チェーンコードの例
常に 1 つずつ変数の値が増分される **invoke** トランザクションは決定論的です。すべてのノードで結果は常に同じであり、差異はないためです。このトランザクションが固定値 5 に対して実行されると、付加される値はすべてのノードで常に 6 になります。決定論的なチェーンコードのネットワークの結果については、ブロックチェーン内で不一致はありません。各ノードの台帳のコピーは常に、値が (同期後に) 前の呼び出しよりも 1 大きくなっていることを示します。

### 非決定論的チェーンコードの例
ブロックチェーン変数の値を一日の始まり (00:00) からの経過秒数で増分する **invoke** トランザクションは非決定論的です。時間の経過とともにノード間で値が変化するためです。例えば、このトランザクションが固定値 5 に対して実行されるたびに、付加される値はノード間で異なります (まれに例外があります)。これは、00:00 からの経過秒数が必然的に変化するためです。この非決定論的チェーンコードのネットワーク結果は、相違のあるブロックチェーンです。すべてのノードで、5 に 00:00 からの経過秒数を加えた値が同じになることはありません。

### ランダム性
チェーンコードは、時間が経過しても、ノード間で付加される値にランダム性がないことが求められます。何らかのランダム性が存在すると、ノード間でブロックチェーンが異なってしまい、これはネットワークで解決される必要があります。ランダム性を回避するには、並列チェーンコードが呼び出しチェーンコードからの入力値に影響を及ぼさないようにする必要があります。例えば、並列照会によってノード間の呼び出し値に差異が生じる可能性があるため、**query** トランザクションを **invoke** トランザクションと並行して実行しないでください。

### グローバル変数の使用
グローバル変数またはインスタンス変数を使用して、台帳から取得した値を保管したり、台帳に値を設定したりすると、非決定論的になる可能性があります。チェーン・コードは、チェーン・コード・コンテナーの再始動において状態を維持しないグローバル変数またはインスタンス変数に依存すべきではありません。以下の例ではグローバル変数を使用しています。`stub.PutState` 関数によって台帳に書き込まれる `key` の値は、グローバル変数から派生しています。

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### 1 つのマップ・タイプに対する反復
1 つのマップ・タイプに対する反復は、非決定論的になる可能性があります。これは、Go プログラミング言語において順序が決定論的ではないためです。以下に、`columnTypes` というマップに対する反復の例を示します。

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
