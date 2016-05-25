---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# 沙盤推演及正式作業模式

{: #push-sandboxandproduction-modes}

您可以透過下列其中一種模式來使用 Push Notifications：沙盤推演或正式作業。沙盤推演是一種自行包含的測試環境，可開發及測試 Push API 與伺服器應用程式 Push 服務的整合。首先，使用「Push 儀表板」配置沙盤推演及正式作業模式。您可以使用 [Push REST API](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}，在沙盤推演與正式作業之間切換推送服務的作業模式。預設會啟用沙盤推演模式。不過，當您切換模式時，在這些模式之間不會共用標籤、裝置及訂閱。


如果已準備好將應用程式部署至即時環境，請使用 Push REST API 選取「正式作業」模式。如需 REST API 的相關資訊，請參閱 REST API。

若要將推送服務的作業模式從沙盤推演切換至正式作業，請執行下列動作：

1. 使用 PUT ApplicationID Settings REST API 呼叫
2. 在 JSON 主體中，使用 [GET ApplicationID Settings REST](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window} API 呼叫來確認已切換模式。預期的回應為 "mode": "PRODUCTION"
 
 ```
 { 
 "mode": "PRODUCTION"
 }
 ```
1. 在切換環境模式之後，請重新執行用戶端程式碼，以「正式作業」模式登錄裝置。

如需 REST API 的相關資訊，請參閱 REST API。
