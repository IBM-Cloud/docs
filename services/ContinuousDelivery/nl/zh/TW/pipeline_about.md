---

copyright:
  years: 2016, 2017
lastupdated: "2017-4-4"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 關於 Delivery Pipeline
{: #deliverypipeline_about}

IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} 服務（也稱為管線）會自動持續部署 Bluemix 專案。在管線中，階段的序列會擷取輸入並執行工作（例如建置、測試及部署）。
{:shortdesc}

下列各節說明管線的概念性詳細資料。

## 階段
{: #deliverypipeline_stages}

建置、部署及測試程式碼時，階段會組織輸入及工作。階段可接受來自來源控制儲存庫（SCM 儲存庫）的輸入，或來自其他階段中之建置工作（建置構件）的輸入。當您建立第一個階段時，會在**輸入**標籤上自動設定預設值。

階段的輸入會傳遞給階段所包含的工作，並且會提供每個工作一個全新的容器以便在其中執行。階段中的工作無法將構件傳遞給彼此。

您可以定義可在所有工作中使用的階段環境內容。例如，您可以定義 `TEST_URL` 內容，以傳遞用來在單一階段中部署及測試工作的單一 URL。部署工作會部署至該 URL，測試工作則會測試該 URL 上的執行中應用程式。

在階段中，每次將變更遞送給專案的 SCM 儲存庫時，依預設會自動執行建置及部署。階段及工作會依序執行；它們讓您能進行工作的流程控制。例如，您可以在部署階段之前放置測試階段。如果測試階段中的測試失敗，則不會執行部署階段。

您可能想要更嚴格地控制特定階段。如果您不想要每次在輸入發生變更時都執行階段，則可以停用此功能。在**輸入**標籤的「階段觸發程式」區段中，按一下**只在手動執行此階段時才執行工作**。

![「輸入」標籤](images/input_tab_only_execute.png)

## 工作
{: #deliverypipeline_jobs}

工作是階段內的執行單位。一個階段可以包含多個工作，並且會循序執行階段中的工作。根據預設值，如果工作失敗，則不會執行階段中的後續工作。

![階段內的建置及測試工作](images/jobs.png)

工作是在為每一個管線執行所建立之 Docker 容器內的不同工作目錄中執行。執行工作之前，會將在階段層次所定義的輸入移入其工作目錄中。例如，您可以具有包含測試工作及部署工作的階段。如果您將相依關係安裝在某個工作上，則另一個工作無法使用這些相依關係。不過，如果您在階段的輸入中提供相依關係，則這兩個工作都可以使用這些相依關係。

簡單類型的建置工作除外，當您配置工作時，可以納入含有建置、測試或部署指令的 UNIX Shell Script。因為工作是在特定容器中執行，所以某個工作的動作無法影響其他工作的執行環境，即使那些工作是相同階段的一部分也是一樣。

此外，管線工作只能以 `sudo` 身分執行下列指令：
  * `/usr/sbin/service`
  * `/usr/bin/apt-get`
  * `/usr/bin/apt-key`
  * `/usr/bin/dpkg`
  * `/usr/bin/add-apt-repository`
  * `/opt/IBM/node-v0.10.40-linux-x64/npm`
  * `/opt/IBM/node-v0.12.7-linux-x64/npm`
  * `/opt/IBM/node-v4.2.2-linux-x64/npm`
  * `/usr/bin/Xvfb`
  * `/usr/bin/pip`


執行工作之後，會捨棄為它所建立的容器。工作執行的結果可以持續保存，但其執行環境則否。

**附註**：工作最多可以執行 60 分鐘。工作超出此限制時，即會失敗。如果工作超出此限制，請將它分成多個工作。例如，如果工作執行三個作業，則可能會將它分成三個工作：一個作業一個工作。

若要瞭解如何將工作新增至階段，請參閱[將工作新增至階段](/docs/services/ContinuousDelivery/pipeline_build_deploy.html#deliverypipeline_add_job){: new_window}。

### 建置工作

建置工作會在準備部署時編譯您的專案。它們會產生可傳送至建置保存目錄的構件，不過根據預設值，會將構件放在專案的根目錄中。

從建置工作取得輸入的工作，必須參照在它們建立所在之相同結構中的建置構件。例如，如果建置工作會將建置構件保存至 `output` 目錄，則部署所編譯的專案時，部署 Script 會參照 `output` 目錄，而不是專案根目錄。您可以在**建置保存目錄**欄位中輸入目錄名稱，以指定要保存的目錄。將欄位空白，會保存根目錄。

**附註**：如果您為建置工作選取**簡單**建置器類型，則會跳過建置程序。在該情況下，不會編譯您的程式碼，而是會依現狀將它傳送至部署階段。若要建置並部署，請選取非**簡單**的建置器類型。

#### 建置 Script 的環境內容
您可以在建置工作的建置 Shell 指令內包含環境內容。這些內容讓您能存取工作執行環境的相關資訊。如需相關資訊，請參閱 [{{site.data.keyword.deliverypipeline}} 服務的環境內容及資源](/docs/services/ContinuousDelivery/pipeline_deploy_var.html)。

### 部署工作

部署工作會將您的專案當成應用程式上傳至 Bluemix，而且可以從 URL 進行存取。部署專案之後，您可以在 Bluemix 儀表板上找到所部署的應用程式。

部署工作可以部署新的應用程式，或更新現有的應用程式。即使您先使用另一種方法（例如 Cloud Foundry 指令行介面，或 Web IDE 中的執行列）來部署應用程式，還是可以使用部署工作來更新應用程式。若要更新應用程式，請在部署工作中使用該應用程式的名稱。

您可以部署至一或多個地區及服務。例如，您可以設定 {{site.data.keyword.deliverypipeline}} 使用一個以上的服務、在一個地區中測試，以及部署至多個地區進行正式作業。如需相關資訊，請參閱[地區](/docs/overview/whatisbluemix.html#ov_intro_reg){: new_window}。

#### 部署 Script 的環境內容

您可以在部署工作的部署 Script 內包含環境內容。這些內容讓您能存取工作執行環境的相關資訊。如需相關資訊，請參閱 [{{site.data.keyword.deliverypipeline}} 服務的環境內容及資源](/docs/services/ContinuousDelivery/pipeline_deploy_var.html)。

### 測試工作
如果您想要要求符合條件，請在建置及部署工作之前或之後包含測試工作。您可以視需要將測試工作自訂成簡單或複雜。例如，您可以發出 cURL 指令，並預期會有特定回應。也可以使用協力廠商測試服務（例如 Sauce Labs）來執行一組單元測試或執行功能測試。

如果您的測試產生 JUnit XML 格式的結果檔案，則會在每個測試結果頁面的**測試**標籤上顯示根據這些結果檔案的報告。如果測試失敗，則工作也會失敗。

#### 測試 Script 的環境內容

您可以在測試工作的 Script 中包含環境內容。這些內容讓您能存取工作執行環境的相關資訊。如需相關資訊，請參閱 [{{site.data.keyword.deliverypipeline}} 服務的環境內容及資源](/docs/services/ContinuousDelivery/pipeline_deploy_var.html)。

## 資訊清單檔
{: #deliverypipeline_manifest}

資訊清單檔（名為 `manifest.yml` 並儲存在專案的根目錄中）控制如何將專案部署至 Bluemix。如需建立專案資訊清單檔的相關資訊，請參閱[關於應用程式資訊清單的 Bluemix 文件](/docs/manageapps/depapps.html#appmanifest)。若要與 Bluemix 整合，您專案的根目錄中必須要有資訊清單檔。不過，您不需要根據檔案中的資訊來進行部署。

在管線中，您可以使用 `cf push` 指令引數來指定資訊清單檔的所有項目。`cf push` 指令引數有助於具有多個部署目標的專案。如果多個部署工作都嘗試使用專案資訊清單檔中所指定的路徑，則會發生衝突。

為了避免衝突，指定路徑時可以使用 `cf push`，再加上主機名稱引數 `-n` 及路徑名稱。藉由修改個別階段的部署 Script，即可避免在部署至多個目標時發生路徑衝突。

若要使用 `cf push` 指令引數，請開啟部署工作的配置設定，並修改**部署 Script** 欄位。如需相關資訊，請參閱 [Cloud Foundry Push 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push){: new_window}。

## 範例管線
{: #deliverypipeline_example}

簡單的管線可能包含三個階段：

1. 「建置」階段：在應用程式上編譯及執行建置程序。
2. 「測試」階段：部署應用程式實例，然後對其執行測試。
3. 「正式作業」階段：部署所測試應用程式的正式作業實例。

此管線顯示在下列概念性圖表中：

![管線中階段及工作的概念性圖表](images/diagram.jpg)

*三階段管線的概念性模型*

階段都採用其從儲存庫及建置工作的輸入，而且會循序並各自獨立地執行階段內的工作。在範例管線中，會循序執行階段，即使「測試」及「正式作業」階段都採用「建置」階段的輸出作為其輸入。
