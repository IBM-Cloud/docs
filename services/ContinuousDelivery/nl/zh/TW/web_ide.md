---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-31"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# 使用 Eclipse Orion IDE 編輯程式碼
{: #web_ide}

Eclipse Orion {{site.data.keyword.webide}} 是一種您可以針對 Web 進行開發的瀏覽器型開發環境。有了內容輔助、程式碼完成及錯誤檢查的協助，您就可以使用 JavaScript、HTML 及 CSS 進行開發。{{site.data.keyword.webide}} 幾乎可以搭配任何語言一起使用，並且提供大部分檔案類型的語法強調顯示。來源控制是內建的，而且您可以在本端部署程式碼來測試及除錯應用程式。
{:shortdesc}

最好的一點是，{{site.data.keyword.webide}} 採用 Web 技術。您不必進行任何安裝、維護和擴充。您可以在具有網際網路連線的任何位置進行開發。

## 設定編輯器
{: #editorsetup}

{{site.data.keyword.webide}} 可進行自訂，以選擇色系、技術工具，以及符合開發需求的設定。若要檢視及修改設定，請從左邊的功能表中，按一下**設定**圖示 <img class="inline" src="images/webide_settings_icon_light_small.png"  alt="「設定」圖示">。

如果您經常需要在編輯時變更特定設定，則可以從**本端編輯器設定**圖示 <img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="「本端編輯器設定」圖示"> 快速存取這些設定。 

![本端編輯器設定](images/webide_local_editor_settings_light.png)

預設一律會顯示編輯器樣式及字型大小的設定。若要在功能表中包括其他編輯器設定，請遵循下列步驟：

1. 按一下**本端編輯器設定**圖示 <img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="「本端編輯器設定」圖示">。

2. 按一下**編輯器設定**。

3. 若要從**本端編輯器設定**功能表中包括或排除設定，請按一下每一個設定旁的星星。

![「編輯器設定」切換](images/webide_editor_settings_toggle_light.png)


## 編輯程式碼
{: #editcode}

{{site.data.keyword.webide}} 有兩個主要區段。第一個區段是檔案導覽器，會以樹狀結構顯示專案檔。您可以從檔案導覽器中建立、重新命名、刪除及管理檔案和資料夾。

**提示：**若要將檔案上傳至檔案導覽器，請將它們從您的電腦拖曳至檔案導覽器。

第二個區段是編輯器窗格。編輯器提供數個程式碼特性（包括內容輔助及語法驗證）。

![Web IDE](images/webide_light.png)

### 使用多個檔案
1. 若要同時使用兩個檔案，請按一下**變更分割編輯器模式**圖示 <img class="inline" src="images/webide_split_editor_icon_light_small.png"  alt="「分割編輯器」圖示">。
2. 從開啟的功能表中，選取視圖。

 在您選取視圖之後，如果已在編輯器中開啟檔案，則兩個編輯器視圖都會顯示該檔案。

 若要開啟或變更在其中一個編輯器視圖中顯示的檔案，請執行下列動作：
 1. 將游標移至您要變更的編輯器視圖。
 2. 在檔案導覽器中，按一下檔案。

### 鍵盤快速鍵
只能透過鍵盤快速鍵存取 {{site.data.keyword.webide}} 中的大部分指令。

若要查看編輯器中的鍵盤快速鍵清單，請按 Alt+Shift+?。如果您是使用 Mac OS，請按 Ctrl+Shift+?。

## 管理原始碼
{: #sourcecontrol}

{{site.data.keyword.webide}} 是與原始碼管理工具整合。若要使用 Git 儲存庫，請按一下 **Git 儲存庫**圖示 <img class="inline" src="images/webide_git_icon_light_small.png"  alt="「Git 儲存庫」圖示">。 

 **提示**：如果您要搭配使用 {{site.data.keyword.webide}} 與開放式工具鏈，則工作區會預先移入 GitHub、{{site.data.keyword.ghe_short}} 或「Git 儲存庫及問題追蹤」儲存庫。會強調顯示與現行工具鏈相關聯的儲存庫。


## 從工作區部署應用程式
{: #deploy}

1. 若要部署應用程式，請從執行列中選取或建立啟動配置。
1. 按一下部署圖示 <img class="inline" src="images/webide_deploy_button_light_small.png"  alt="部署圖示">。使用您工作區的現行內容以及啟動配置中所定義的環境，即可部署您應用程式的實例。 
2. 部署應用程式之後，即可使用執行列來停止、重新啟動或除錯應用程式、檢視日誌，以及執行其他作業。
![執行列](images/webide_runbar_light.png)    

<!-- 3/6/2016: bl commands don't work with V2/CD 
## Editing outside of the {{site.data.keyword.webide}}
{: #editlocal}

To use an editor besides the {{site.data.keyword.webide}}, set up {{site.data.keyword.Bluemix_live}} so that you can work directly with your project files in any tool. {{site.data.keyword.Bluemix_live_notm}} is a command-line application that synchronizes the changes in your local file system with your cloud workspace in {{site.data.keyword.jazzhub}}. 

### Before you begin 

Download and install the [{{site.data.keyword.Bluemix_live_notm}} command-line interface![External link icon](../../icons/launch-glyph.svg "External link icon")](http://livesyncdownload.ng.bluemix.net){: new_window}.

### Synchronizing your local environment with {{site.data.keyword.Bluemix_notm}}
{: #edit_local_download}

1. Open a command-line window.
2. Sign in to {{site.data.keyword.Bluemix_notm}}:

	```
	bl login
	```
	{: pre}

3. When you are prompted, enter your IBMid and password.
4. View a list of your {{site.data.keyword.Bluemix_notm}} projects: 

	```
	bl projects
	```
	{: pre}

4. Synchronize your local environment with your project on {{site.data.keyword.Bluemix_notm}}:

	```
	bl sync projectName
	```
	{: pre}

where `projectName` is your {{site.data.keyword.Bluemix_notm}} app's name.

When you are finished editing, enter `q` to end synchronization.

### Enabling the Desktop Sync feature to edit code locally

The Desktop Sync feature is like Live Edit mode for the command line. You need the Desktop Sync feature to debug on the command line.
1. In another command-line window, enable the Desktop Sync feature:

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. Use the launch configuration that you created in the {{site.data.keyword.webide}}. After you select the launch configuration, the Desktop Sync feature is enabled in your local environment. In the command-line window that you just opened, you can view the app's URL, the debug URL, the manage URL, and view the {{site.data.keyword.Bluemix_live_notm}} state.

3. Refresh the browser and verify that you can see the changes that you saved to static files in the local workspace. 

### Disabling the Desktop Sync feature

1. In the second command-line window, enter `bl stop`.
2. In the first command-line window, enter `q`.

--> 
