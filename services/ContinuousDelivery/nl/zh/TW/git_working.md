---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:screen:.screen}
{:codeblock:.codeblock}

# Git Repos and Issue Tracking（測試版）
{: #git_working}

使用 IBM 所管理並以 [GitLab Community Edition ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://about.gitlab.com/){:new_window} 為建置基礎的 Git 儲存庫及問題追蹤器，來與團隊分工合作並且管理原始碼。
{: shortdesc}

Git Repos and Issue Tracking 工具整合可支援團隊使用多種方式來管理程式碼以及分工合作：
   * 透過讓程式碼更為安全的精密存取控制，來管理 Git 儲存庫
   * 透過合併要求，來檢閱程式碼並加強協同作業
   * 透過問題追蹤器，來追蹤問題與共用構想
   * 在 Wiki 系統上記載專案

**附註：**因為此工具整合是以 GitLab Community Edition 為建置基礎，並由 IBM 於 Bluemix 上進行管理，所以有一些 GitLab 選項無法使用。例如，Delivery Pipeline 提供 Bluemix 的持續整合及持續交付；因此，不支援 GitLab 中的持續整合特性。此外，無法使用管理功能，因為它們是由 IBM 所管理。

## 檔案及儲存庫大小限制
{: #git_limits}

檔案嚴格限制為 100 MB。建議的儲存庫大小限制為 1 GB。如果您的儲存庫超出 1 GB，則可能會收到含有減少儲存庫大小要求的電子郵件。

## 在本端使用 Git Repos and Issue Tracking
{: #git_authentication}

您可以在本端存取 Git Repos and Issue Tracking 中所儲存的 Git 儲存庫。如需在本端設定 Git 的指示，請參閱[在指令行上開始使用 Git ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git.ng.bluemix.net/help/gitlab-basics/start-using-git){:new_window}。

### 建立個人存取記號或 SSH 金鑰來進行鑑別  
若要從本端 Git 儲存庫完成遠端 Git 作業（例如 `clone` 或 `push`），您必須使用個人存取記號或 SSH 金鑰來向 GitLab 進行鑑別。

* 若要設定個人存取記號，請參閱[個人存取記號 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git.ng.bluemix.net/help/api/README.html#personal-access-tokens){:new_window}。
* 若要設定 SSH 金鑰，請參閱 [SSH ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git.ng.bluemix.net/help/ssh/README){:new_window} 或[如何建立 SSH 金鑰 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git.ng.bluemix.net/help/gitlab-basics/create-your-ssh-keys){:new_window}。使用 SSH 鑑別來存取儲存庫，可能需要額外配置 Proxy 及防火牆。
