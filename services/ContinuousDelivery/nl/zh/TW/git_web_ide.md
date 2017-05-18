---

copyright:
  years: 2017
lastupdated: "2017-5-8"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# 在 Eclipse Orion Web IDE 中使用 Git
{: #git_web_ide}

當您使用 Eclipse Orion {{site.data.keyword.webide}} 時，不需要 Git 終端機：您可以在 Web IDE 中執行多個一般 Git 指令。

不管您在哪裏編寫程式碼，都可以使用此快速參照來執行一般作業。

## 建立本端分支
{: #create_branch}

### Eclipse Orion Web IDE
1. 按一下 **Reference** 清單。

1. 按一下 **New Branch**。

2. 鍵入您的分支名稱，然後按一下 **Submit**。

### Git 終端機
1. 鍵入 `git branch <branchname>`，然後按 Enter 鍵。

## 使用本端分支
{: #start_working_on_branch}

### Eclipse Orion Web IDE
1. 按一下 **Reference** 清單，然後展開 **local**。

2. 在要修改的分支旁邊，按一下移出圖示 <img  class="inline" src="./images/checkout.png" alt="「移出」圖示">。

1. 確定您的已選取分支顯示在 **Reference** 清單中。

### Git 終端機
1. 若要檢視本端分支，請鍵入 `git branch -l`，然後按 Enter 鍵。

2. 鍵入 `git checkout <branchname>`，然後按 Enter 鍵。


## 更新本端分支以包括遠端分支的變更
{: #update_branch}

### Eclipse Orion Web IDE
1. 按一下 **Sync**。

1. 如果發生衝突，請[解決它們](#resolve_a_rebase_conflict)。

### Git 終端機
1. 鍵入 `git pull`，然後按 Enter 鍵。

## 刪除本端分支
{: #delete_branch}

### Eclipse Orion Web IDE
1. 確定未移出要刪除的分支。如果已移出該分支，請[移出另一個分支](#start_working_on_branch)。

1. 按一下 **Reference** 清單，然後展開 **local**。

2. 在要移除的本端分支旁，按一下 **Delete** <img class="inline"  src="./images/delete.png" alt="「刪除」圖示">。

### Git 終端機
1. 鍵入 `git branch -d <branchname>`，然後按 Enter 鍵。

##將本端變更強制推送至遠端分支
{: #force_push}

將所參照遠端分支的內容改寫為作用中本端分支的內容。

**重要事項：**當您將本端分支強制推送至遠端分支時，可能會遺失遠端分支上的確定。

### Eclipse Orion Web IDE

1. 在 Working Directory Changes 區段的 Outgoing 區段中，按一下 **Push** 旁的箭頭。
2. 按一下 **Force Push Branch**。
3. 確認警告。

### Git 終端機

1. 鍵入 `git push <origin> <remote branch> -f`，然後按 Enter 鍵。

## 捨棄作用中本端分支中未編譯打包的變更
{: #discard_changes}

### Eclipse Orion Web IDE
1. 在 Working Directory Changes 區段中，選取每一個含有您要捨棄之變更的已修改檔案的勾選框。
2. 按一下移出圖示 <img class="inline"  src="./images/discard.png" alt="移出選取的檔案，並捨棄所有變更">。

### Git 終端機
1. 鍵入 `git checkout -- path/to/file/filename`，以捨棄檔案的變更。

## 確定檔案並推送至遠端分支
{: #commit}

### Eclipse Orion Web IDE
1. 在 Working Directory Changes 區段中，選取每一個要確定的檔案的勾選框。

3. 在 **Enter the commit message** 欄位中，鍵入可說明您變更的訊息。

  **提示**：提供詳細確定訊息。您的訊息應該提供足夠的詳細資料，讓某人瞭解為何變更是必要的，而不需要其他資訊。您可以包括團隊問題追蹤器中項目的鏈結，進行協助。確定訊息的第一行應該包含 50 個以下的字元。在您新增其他文字之前，請新增一個空白行。

4. 按一下 **Commit**。

5. 按一下 **Push**。

### Git 終端機
1. 鍵入 `git status`，然後按 Enter 鍵。

2. 檢閱要確定的變更。如果所有檔案都列為要進行確定，請繼續。若要確定未編譯打包的檔案，請先將它們編譯打包。

3. 鍵入 `git commit`，然後按 Enter 鍵。

4. 輸入確定摘要，新增空白行，然後新增確定說明。

  **提示**：確定摘要應該少於 50 個字元。確定說明應該提供足夠的詳細資料，讓某人瞭解為何變更是必要的，而不需要其他資訊。您可以包括團隊問題追蹤器中項目的鏈結，進行協助。

5. 儲存確定訊息。

  **附註：**若要儲存確定訊息，並關閉 Vim（這可能是預設文字編輯器），請按 Esc 鍵，鍵入 `:wq`，然後按 Enter 鍵。

4. 鍵入 `git push`，然後按 Enter 鍵。

## 檢視確定歷程
{: #view_commit_history}

### Eclipse Orion Web IDE
1. 在 Active Branch 區段中，展開 **History** 以查看該分支的確定歷程。

  確定歷程也可以檢視為已連接的視覺化圖形。

1. 按一下 **graphical representation toggle** 圖示 <img  class="inline" src="./images/graphicalhistoryicon.png" alt="「圖形歷程」圖示">。

  切換之後，會將作用中分支的確定歷程以及任何送入或送出變更繪製為已連接的圖形。視覺化表示法會顯示所有確定以及它們在其上進行的分支。

  <img class="screen-shot" src="./images/visualhistoryexample.png" alt="視覺化確定歷程">

### Git 終端機
1. 鍵入 `git log`，然後按 Enter 鍵。

2. 導覽確定者的確定。
 * 若要檢視更多項目，請按 Page Down 鍵。
 * 若要檢視先前的項目，請按 Page Up 鍵。

3. 若要停止檢視項目，請按 Q 鍵。

## 比較確定所建立的變更
{: #compare_changes}

### Eclipse Orion Web IDE
1. 檢視確定歷程，並找到確定。如需相關資訊，請參閱[檢視確定歷程](#view_commit_history)。

2. 按一下確定，以檢視其詳細資料。

3. 按一下檔案旁的 **>**，然後檢閱檔案的變更。

  **附註：**如果確定已建立行的變更，則原始行會加上粉紅色陰影，而新行會加上綠色陰影。同樣地，確定所新增的行會加上綠色陰影，而確定所移除的行會加上粉紅色陰影。

### Git 終端機
1. 鍵入 `git log -p`，然後按 Enter 鍵。

  **附註：**若只要檢視特定數目的確定，請鍵入 `git log -p -<number_of_commits_to_view>`。

2. 導覽確定。
 * 若要檢視更多項目，請按 Page Down 鍵。
 * 若要檢視先前的項目，請按 Page Up 鍵。

3. 檢閱變更。

  **附註：**如果確定已建立行的變更，則原始行的文字會是紅色，且開頭為減號 (-)。新行的文字會是綠色，且開頭為加號 (+)。同樣地，確定所新增行的文字會是綠色，且開頭為 +。確定所移除行的文字會是紅色，且開頭為 -。

1. 若要停止檢視項目，請按 Q 鍵。

## 修改最後一個確定
{: #modify_last_commit}

  **附註：**如果您在將最後一個確定推送至遠端儲存庫之後對其進行修改，則會重寫確定歷程。這可能會造成確定失敗，以及專案中其他貢獻者的其他問題。請確定您知道在修改您已推送至遠端儲存庫的確定之前所進行的作業。

### Eclipse Orion Web IDE
1. 選取要新增至確定的項目的勾選框。

1. 選取 **Amend previous commit** 勾選框。

2. 必要的話，請輸入新的確定訊息。

3. 按一下 **Commit**。

### Git 終端機
1. 檢查狀態。請視需要，編譯打包或取消編譯打包檔案。

2. 鍵入 `git commit --amend`，然後按 Enter 鍵。

3. 在文字編輯器中，接受或修改確定訊息。

  **附註：**若要儲存確定訊息，並關閉 Vim（這可能是預設文字編輯器），請按 Esc 鍵，鍵入 `:wq`，然後按 Enter 鍵。

## 標記確定
{: #tag_commit}

### Eclipse Orion Web IDE
1. 檢視確定歷程，並找到確定。如需相關資訊，請參閱[檢視確定歷程](#view_commit_history)。

2. 按一下確定，以檢視其詳細資料。

2. 在確定窗格中，按一下 **Create a tag for the commit** <img class="inline"  src="./images/tag.png" alt="建立確定的標籤">。

3. 在名稱欄位中，輸入標籤文字。按一下 **Submit**。

### Git 終端機
1. 檢視確定歷程，並取得要標記的確定的 ID。如需相關資訊，請參閱[檢視確定歷程](#view_commit_history)。

2. 鍵入 `git tag -a <tag_text> <commit_id>`，然後按 Enter 鍵。

## 變更確定者名稱及電子郵件位址
{: #change_the_committer_name_and_email_address}

### Eclipse Orion Web IDE
1. 按一下配置圖示 <img class="inline" src="./images/configurations.png" alt="「配置」圖示">。

3. 更新 user.email 及 user.name 值，以變更使用者電子郵件位址及名稱。按一下 **Submit**，以儲存每一個變更。

### Git 終端機
若要更新單一儲存庫的名稱及電子郵件位址，請執行下列動作：

1. 鍵入 `git config user.email "<your@email.com>"`，然後按 Enter 鍵。

2. 鍵入 `git config user.name "<Your Name>"`，然後按 Enter 鍵。

若要更新所有儲存庫的名稱及電子郵件位址，請執行下列動作：

1. 鍵入 `git config --global user.email "<your@email.com>"`，然後按 Enter 鍵。

2. 鍵入 `git config --global user.name "<Your Name>"`，然後按 Enter 鍵。

##回復確定
{: #revert}

回復確定已建立到作用中分支的變更。

### Eclipse Orion Web IDE

1. 在 History 下，選取某個確定。

2. 在頁面右側的確定摘要上方，按一下回復圖示 <img class="inline" src="./images/revert.png" alt="「回復」圖示">。

### Git 終端機

1. 鍵入 `git revert <commit ID>`，然後按 Enter 鍵。

## 合併變更
{: #merge_changes}

當您需要將變更從來源分支遞送至目的地分支時，必須先進行合併。一般而言，來源分支是您已在其中進行變更的分支，而目的地分支是您的主要分支。

### Eclipse Orion Web IDE
1. 決定要合併的分支。

2. 移出目的地分支。如需相關資訊，請參閱[使用本端分支](#start_working_on_branch)。

 <img class="screen-shot" src="./images/destinationbranch.png" alt="移出目的地分支">

1. 按一下 **Reference** 清單，展開 **local**，然後按一下來源分支的名稱。來源分支的變更會顯示在 Incoming 區段中。

  <img class="screen-shot" src="./images/sourcebranch.png" alt="來源分支的變更會顯示在 Incoming 區段中">

1. 在 Incoming 區段中，按一下 **Merge** 圖示 <img  class="inline" src="./images/mergeicon.png" alt="Incoming 區段中的 Merge 圖示">

1. 在 **Reference** 清單中，按一下您剛剛將變更合併至其中的分支旁的移出圖示。

1. 如果您要遞送變更，請按一下 **Push**。否則，此時，您可以建立測試部署，以確定每項作業都如預期運作。

### Git 終端機
1. 決定要合併的分支。

2. 移出目的地分支。如需相關資訊，請參閱[使用本端分支](#start_working_on_branch)。

3. 鍵入 `git merge <source_name>`，然後按 Enter 鍵。


## 解決合併衝突
{: #resolve_a_merge_conflict}

### Eclipse Orion Web IDE
1. 在 Changed Files 窗格中，檢閱包含衝突的檔案清單。

2. 在 Web IDE 中，開啟每一個包含衝突的檔案。

3. 解決每一個衝突的變更。

  **附註：**刪除所有您不想保留的文字。每一個衝突的格式如下：

		<<<<<<< HEAD
		所移出分支中的文字。
		=======
		所合併分支中的文字。
		>>>>>>> commit_ID_from_merged_branch
4. 針對每一個衝突的檔案，選取此勾選框。鍵入合併確定訊息，然後按一下 **Commit**。

### Git 終端機
1. 針對包含衝突的檔案，檢閱名稱的 Git 訊息。

2. 在文字編輯器中，開啟包含衝突的檔案。

3. 解決每一個衝突的變更，然後儲存檔案。

  **附註：**刪除所有您不想保留的文字。每一個衝突的格式如下：

		<<<<<<< HEAD
		所移出分支中的文字。
		=======
		所合併分支中的文字。
		>>>>>>> merged_branch
4. 編譯打包每一個您已修改的檔案，然後確定合併。

## 重設基線分支
{: #rebase_branches}

### Eclipse Orion Web IDE
1. 決定要重設基線的分支。您會將來源分支的內容重設基線到目的地分支。

2. 移出目的地分支。如需相關資訊，請參閱[使用本端分支](#start_working_on_branch)。

1. 按一下 **Reference** 清單。

1. 按一下來源分支的名稱。

1. 在 Incoming 區段中，按一下重設基線圖示 <img  class="inline" src="./images/rebase.png" alt="「重設基線」圖示">。

5. 如果發生衝突，請[解決它們](#resolve_a_rebase_conflict)。

6. 視需要重複前一個步驟多次，以完成重設基線作業。

1. 按一下 **Reference** 清單，展開 **origin**，然後按一下來源分支的名稱。

1. 按一下 **Push**。

### Git 終端機
1. 鍵入 `git checkout <destination_branchname>` 並按 Enter 鍵，以移出要更新的分支。

2. 鍵入 `git rebase <source_branchname>`，然後按 Enter 鍵。

3. 如果發生衝突，請[解決它們](#resolve_a_rebase_conflict)。

5. 視需要重複前一個步驟多次，以完成重設基線作業。

  **附註：**若要停止重設基線作業，請鍵入 `git rebase --abort`，然後按 Enter 鍵。

## 解決重設基線衝突
{: #resolve_a_rebase_conflict}

### Eclipse Orion Web IDE
1. 在 Working Directory Changes 區段中，檢閱衝突檔案的清單。

2. 在 Web IDE 中，開啟每一個包含衝突的檔案。

3. 解決每一個衝突的變更。

  **附註：**刪除所有您不想保留的文字。每一個衝突的格式如下：

		<<<<<<< HEAD
		所移出分支中的文字。
		=======
		所合併分支中的文字。
		>>>>>>> commit_ID_from_merged_branch
4. 在重設基線窗格中，選取每一個已更正檔案的勾選框，然後按一下 **Continue**。

### Git 終端機
1. 針對包含衝突的檔案，檢閱名稱的 Git 訊息。

2. 在文字編輯器中，開啟包含衝突的檔案。

3. 解決每一個衝突的變更，然後儲存檔案。

  **附註：**刪除所有您不想保留的文字。每一個衝突的格式如下：

		<<<<<<< HEAD
		所移出分支中的文字。
		=======
		所合併分支中的文字。
		>>>>>>> merged_branch
4. 編譯打包每一個您已修改的檔案。

5. 鍵入 `git rebase --continue`，然後按 Enter 鍵，以繼續重設基線作業。
