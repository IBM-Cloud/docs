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

# 비결정적 체인코드
{: #ndcc}


IBM Blockchain 네트워크는 결정적 체인코드만 지원합니다. 비결정적 체인코드의 사용은 지원되지 않으며, 블록체인 네트워크에서 서버 오류가 발생합니다.
{:shortdesc}

**비결정적 체인코드**는 블록체인 원장에서 시간이 지나면서 노드 간에 동일한 추가 값이 결과로 나타나지 **않는** 체인코드입니다. 이와는 대조적으로, **결정적 체인코드**는 블록체인 원장에서 시간이 지나면서 노드 간에 항상 동일한 추가 값을 생성합니다. 

### 결정적 체인코드 예제
변화 없이 모든 노드에서 결과가 항상 동일하므로, 항상 하나씩 변수 값을 증가시키는 **호출** 트랜잭션은 결정적입니다. 예를 들어, 이 트랜잭션이 5의 고정 값에 대해 실행될 때마다 추가된 값은 언제나 항상 모든 노드에서 6입니다. 결정적 체인코드의 네트워크 출력은 블록체인에서 서로 차이가 없습니다. 각 노드에서 원장의 사본은 항상 값이 이전 호출보다 1만큼 크다는 것을 표시합니다(동기화 이후). 

### 비결정적 체인코드 예제
시작일(00:00) 이후의 경과 시간(초)으로 블록체인 변수의 값을 증가시키는 **호출** 트랜잭션은 비결정적입니다. 시간이 지나면서 값이 노드 간에 변하기 때문입니다. 예를 들어, 이 트랜잭션이 고정 값 5에 대해 실행될 때마다 추가된 값은 노드 간에 분산됩니다(거의 예외가 없음). 시작일(00:00) 이후의 경과 시간(초)이 필연적으로 변하기 때문입니다. 이 비결정적 체인코드의 네트워크 출력은 분기하는 블록체인입니다. 모든 노드는 5 + 시작일(00:00) 이후의 경과 시간 값에서 일치하지 않습니다. 

### 무작위성
체인코드는 시간이 지나면서 노드 간에 추가된 값에서 무작위성을 드러내지 않아야 합니다. 무작위성은 노드 간에 분기하는 블록체인을 생성하며, 이는 다시 네트워크에 의해 해결되어야 합니다. 무작위성을 피하려면, 병렬 체인코드가 호출 체인코드의 입력 값에 영향을 줄 수 없음을 확인해야 합니다. 예를 들어, 병렬 조회가 노드 간에 호출 값에서 변화를 생성할 수 있으므로 **호출** 트랜잭션과 병렬로 **조회** 트랜잭션을 실행하지 마십시오. 

### 글로벌 변수 사용
글로벌 또는 인스턴스 변수를 사용하여 원장에서 검색된 값을 저장하거나 원장에 값을 설정하면 비결정성이 나타날 수 있습니다. 체인코드는 체인코드 컨테이너의 재시작 시 해당 상태를 유지하지 않는 글로벌 또는 인스턴스 변수에 의존해서는 안 됩니다. 다음은 글로벌 변수를 사용하는 예입니다. `stub.PutState` 함수를 통해 원장에 기록되는 `key` 값은 글로벌 변수에서 파생됩니다.

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### 맵 유형에 대해 반복
Go 프로그래밍 언어에서 순서가 결정적이지 않으므로, 맵 유형에 대해 반복하면 비결정성이 나타날 수 있습니다. 다음은 `columnTypes` 맵에 대한 반복 예입니다.

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
