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

使用 Eclipse Orion {{site.data.keyword.webide}} 时，无需 Git 终端：您可以在 Web IDE 中运行许多常用 Git 命令。

不管您在哪里编写代码，都可以使用本快速参考来执行常用任务。

## 创建本地分支
{: #create_branch}

### Eclipse Orion Web IDE
1. 单击**引用**列表。

1. 单击**新建分支**。

2. 输入分支名称，然后单击**提交**。

### Git 终端
1. 输入 `git branch <branchname>`，然后按 Enter 键。

## 使用本地分支
{: #start_working_on_branch}

### Eclipse Orion Web IDE
1. 单击**引用**列表，并展开**本地**。

2. 单击要修改的分支旁边的“检出”图标 <img  class="inline" src="./images/checkout.png" alt="“检出”图标">。

1. 确保所选分支显示在**引用**列表中。

### Git 终端
1. 要查看本地分支，请输入 `git branch -l`，然后按 Enter 键。

2. 输入 `git checkout <branchname>`，然后按 Enter 键。


## 更新本地分支以包含来自远程分支的更改
{: #update_branch}

### Eclipse Orion Web IDE
1. 单击**同步**。

1. 如果遇到冲突，请[解决冲突](#resolve_a_rebase_conflict)。

### Git 终端
1. 输入 `git pull`，然后按 Enter 键。

## 删除本地分支
{: #delete_branch}

### Eclipse Orion Web IDE
1. 确保要删除的分支未检出。如果该分支已检出，请[检出其他分支](#start_working_on_branch)。

1. 单击**引用**列表，并展开**本地**。

2. 单击要除去的本地分支旁边的**删除** <img class="inline"  src="./images/delete.png" alt="“删除”图标">。

### Git 终端
1. 输入 `git branch -d <branchname>`，然后按 Enter 键。

##强制将本地更改推送到远程分支
{: #force_push}

使用活动本地分支的内容覆盖所引用远程分支的内容。

**重要信息**：强制将本地分支推送到远程分支时，可能会丢失远程分支上的提交。

### Eclipse Orion Web IDE

1. 在“工作目录更改”部分的“出局”部分中，单击**推送**旁边的箭头。
2. 单击**强制推送分支**。
3. 确认警告。

### Git 终端

1. 输入 `git push <origin> <remote branch> -f`，然后按 Enter 键。

## 废弃活动本地分支中未编译打包的更改
{: #discard_changes}

### Eclipse Orion Web IDE
1. 在“工作目录更改”部分中，针对包含您要废弃的更改的每个已修改文件，选中对应的复选框。
2. 单击“检出”图标 <img class="inline"  src="./images/discard.png" alt="检出所选文件并废弃所有更改">。

### Git 终端
1. 输入 `git checkout -- path/to/file/filename` 以废弃对文件的更改。

## 提交文件并推送到远程分支
{: #commit}

### Eclipse Orion Web IDE
1. 在“工作目录更改”部分中，针对要提交的每个文件，选中对应的复选框。

3. 在**输入提交消息**字段中，输入描述更改的消息。


  **提示**：请提供详细的提交消息。您的消息应该提供足够的详细信息，以供用户了解为什么更改是必要的，但不要包含更多额外信息。可以在团队的问题跟踪程序中包含项的链接以提供帮助。提交消息的第一行包含的字符数应该少于 50 个。请先添加一个空行，再添加其他文本。

4. 单击**提交**。

5. 单击**推送**。

### Git 终端
1. 输入 `git status`，然后按 Enter 键。

2. 复查要提交的更改。如果列出了所有文件以待提交，请继续。要提交未编译打包的文件，请先对这些文件执行编译打包。

3. 输入 `git commit`，然后按 Enter 键。

4. 输入提交摘要，添加一个空行，然后添加提交描述。

  **提示**：提交摘要应该少于 50 个字符。提交描述应该提供足够的详细信息，以供用户了解为什么更改是必要的，但不要包含更多额外信息。可以在团队的问题跟踪程序中包含项的链接以提供帮助。

5. 保存提交消息。

  **注**：要保存提交消息并关闭 VIM（这可能是您的缺省文本编辑器），请按 Esc 键，输入 `:wq`，然后按 Enter 键。

4. 输入 `git push`，然后按 Enter 键。

## 查看提交历史记录
{: #view_commit_history}

### Eclipse Orion Web IDE
1. 在“活动分支”部分中，展开**历史记录**以查看该分支的提交历史记录。

  提交历史记录还可以作为可视的连通图查看。

1. 单击**图形表示法切换**图标 <img  class="inline" src="./images/graphicalhistoryicon.png" alt="“图形历史记录”图标">。

  一旦切换后，就会将活动分支的提交历史记录以及任何入局或出局更改绘制为连通图。该可视表示法显示所有提交以及提交到的分支。

  <img class="screen-shot" src="./images/visualhistoryexample.png" alt="可视提交历史记录">

### Git 终端
1. 输入 `git log`，然后按 Enter 键。

2. 浏览提交者的提交。
 * 要查看更多条目，请按 Page Down 键。
 * 要查看先前条目，请按 Page Up 键。

3. 要停止查看条目，请按 Q 键。

## 比较提交引入的更改
{: #compare_changes}

### Eclipse Orion Web IDE
1. 查看提交历史记录，并找到提交。有关更多信息，请参阅[查看提交历史记录](#view_commit_history)。

2. 通过单击提交来查看该提交的详细信息。

3. 单击文件旁边的 **>**，然后复查该文件的更改。


  **注**：如果提交引入了对行的更改，那么原始行将为渐变粉，新行将为渐变绿。与此类似，通过提交所添加的行将为渐变绿，通过提交所除去的行将为渐变粉。

### Git 终端
1. 输入 `git log -p`，然后按 Enter 键。

  **注**：要仅查看特定数量的提交，请输入 `git log -p -<number_of_commits_to_view>`。

2. 浏览提交。
 * 要查看更多条目，请按 Page Down 键。
 * 要查看先前条目，请按 Page Up 键。

3. 复查更改。

  **注**：如果提交引入了对行的更改，那么原始行将为红色文本，并以减号 (-) 开头。新行将为绿色文本，并以加号 (+) 开头。与此类似，通过提交所添加的行将为绿色文本，并以 + 开头。通过提交所除去的行将为红色文本，并以 - 开头。

1. 要停止查看条目，请按 Q 键。

## 修改上次的提交
{: #modify_last_commit}

  **注**：对已推送到远程存储库的上次提交进行修改时，将重写提交历史记录。这可能会导致提交失败以及对您项目中的其他贡献者造成其他问题。在修改已推送到远程存储库的提交之前，请务必明白自己要执行的操作会带来什么后果。

### Eclipse Orion Web IDE
1. 针对要添加到提交的项，选中对应的复选框。

1. 选中**修订先前的提交**复选框。

2. 如果需要，请输入新的提交消息。

3. 单击**提交**。

### Git 终端
1. 检查您的状态。根据需要，对文件执行编译打包或取消编译打包操作。

2. 输入 `git commit --amend`，然后按 Enter 键。

3. 在文本编辑器中，接受或修改提交消息。

  **注**：要保存提交消息并关闭 VIM（这可能是您的缺省文本编辑器），请按 Esc 键，输入 `:wq`，然后按 Enter 键。

## 标记提交
{: #tag_commit}

### Eclipse Orion Web IDE
1. 查看提交历史记录，并找到提交。有关更多信息，请参阅[查看提交历史记录](#view_commit_history)。

2. 通过单击提交来查看该提交的详细信息。

2. 在“提交”窗格中，单击**为提交创建标记** <img class="inline"  src="./images/tag.png" alt="为提交创建标记">。

3. 在“名称”字段中，输入标记的文本。单击**提交**。

### Git 终端
1. 查看提交历史记录，并获取要标记的提交的标识。有关更多信息，请参阅[查看提交历史记录](#view_commit_history)。

2. 输入 `git tag -a <tag_text> <commit_id>`，然后按 Enter 键。

## 更改提交者名称和电子邮件地址
{: #change_the_committer_name_and_email_address}

### Eclipse Orion Web IDE
1. 单击“配置”图标 <img class="inline" src="./images/configurations.png" alt="“配置”图标">。

3. 通过更新 user.email 和 user.name 值来更改用户电子邮件地址和姓名。单击**提交**以保存每个更改。

### Git 终端
要针对单个存储库更新您的姓名和电子邮件地址，请执行以下操作：

1. 输入 `git config user.email "<your@email.com>"`，然后按 Enter 键。

2. 输入 `git config user.name "<Your Name>"`，然后按 Enter 键。

要针对所有存储库更新您的姓名和电子邮件地址，请执行以下操作：

1. 输入 `git config --global user.email "<your@email.com>"`，然后按 Enter 键。

2. 输入 `git config --global user.name "<Your Name>"`，然后按 Enter 键。

##还原提交
{: #revert}

还原提交已引入活动分支的更改。

### Eclipse Orion Web IDE

1. 在“历史记录”下，选择提交。

2. 单击页面右侧提交摘要上方的“还原”图标 <img class="inline" src="./images/revert.png" alt="“还原”图标">。

### Git 终端

1. 输入 `git revert <commit ID>`，然后按 Enter 键。

## 合并更改
{: #merge_changes}

需要将源分支中的更改传递到目标分支时，必须首先进行合并。通常，源分支是在其中进行更改的分支，目标分支是主分支。

### Eclipse Orion Web IDE
1. 确定要合并的分支。

2. 检出目标分支。有关更多信息，请参阅[使用本地分支](#start_working_on_branch)。

 <img class="screen-shot" src="./images/destinationbranch.png" alt="检出目标分支">

1. 单击**引用**列表，展开**本地**，然后单击源分支的名称。源分支中的更改会显示在“入局”部分中。

  <img class="screen-shot" src="./images/sourcebranch.png" alt="“入局”部分中显示的源分支中的更改">

1. 在“入局”部分中，单击**合并**图标 <img  class="inline" src="./images/mergeicon.png" alt="“入局”部分中的“合并”图标">

1. 在**引用**列表中，单击刚才将更改合并到其中的分支旁边的“检出”图标。

1. 如果要传递更改，请单击**推送**。否则，此时可以创建测试部署，以确保一切按预期运行。

### Git 终端
1. 确定要合并的分支。

2. 检出目标分支。 有关更多信息，请参阅[使用本地分支](#start_working_on_branch)。

3. 输入 `git merge <source_name>`，然后按 Enter 键。


## 解决合并冲突
{: #resolve_a_merge_conflict}

### Eclipse Orion Web IDE
1. 在“更改的文件”窗格中，查看包含冲突的文件的列表。

2. 在 Web IDE 中，打开包含冲突的每个文件。

3. 解决每个冲突更改。

  **注**：请删除不想保留的所有文本。各冲突的格式如下：

		<<<<<<< HEAD
		Text in checked out branch.
		=======
		Text in merged branch.
		>>>>>>> commit_ID_from_merged_branch
4. 对于每个冲突文件，选中对应的复选框。输入合并提交消息，然后单击**提交**。

### Git 终端
1. 对于包含冲突的文件，查看 Git 消息以获取相应的名称。

2. 在文本编辑器中，打开包含冲突的文件。

3. 解决每个冲突更改，然后保存文件。

  **注**：请删除不想保留的所有文本。各冲突的格式如下：

		<<<<<<< HEAD
		Text in checked out branch.
		=======
		Text in merged branch.
		>>>>>>> merged_branch
4. 对修改过的每个文件编译打包，然后提交合并。

## 为分支重定基底
{: #rebase_branches}

### Eclipse Orion Web IDE
1. 确定要重定基底的分支。您要将源分支的内容重定为目标分支的基底。

2. 检出目标分支。有关更多信息，请参阅[使用本地分支](#start_working_on_branch)。

1. 单击**引用**列表。

1. 单击源分支的名称。

1. 在“入局”部分中，单击“重定基底”图标 <img  class="inline" src="./images/rebase.png" alt="“重定基底”图标">。

5. 如果遇到冲突，请[解决冲突](#resolve_a_rebase_conflict)。

6. 重复上一步所需次数，以完成重定基底操作。

1. 单击**引用**列表，展开**源**，然后单击源分支的名称。

1. 单击**推送**。

### Git 终端
1. 通过输入 `git checkout <destination_branchname>` 并按 Enter 键，检出要更新的分支。

2. 输入 `git rebase <source_branchname>`，然后按 Enter 键。

3. 如果遇到冲突，请[解决冲突](#resolve_a_rebase_conflict)。

5. 重复上一步所需次数，以完成重定基底操作。

  **注**：要停止重定基底操作，请输入 `git rebase --abort`，然后按 Enter 键。

## 解决重定基底冲突
{: #resolve_a_rebase_conflict}

### Eclipse Orion Web IDE
1. 在“工作目录更改”部分中，查看冲突文件的列表。

2. 在 Web IDE 中，打开包含冲突的每个文件。

3. 解决每个冲突更改。

  **注**：请删除不想保留的所有文本。各冲突的格式如下：

		<<<<<<< HEAD
		Text in checked out branch.
		=======
		Text in merged branch.
		>>>>>>> commit_ID_from_merged_branch
4. 在“重定基底”窗格中，针对每个已更正的文件，选中对应的复选框，然后单击**继续**。

### Git 终端
1. 对于包含冲突的文件，查看 Git 消息以获取相应的名称。

2. 在文本编辑器中，打开包含冲突的文件。

3. 解决每个冲突更改，然后保存文件。

  **注**：请删除不想保留的所有文本。各冲突的格式如下：

		<<<<<<< HEAD
		Text in checked out branch.
		=======
		Text in merged branch.
		>>>>>>> merged_branch
4. 对修改过的每个文件编译打包。

5. 通过输入 `git rebase --continue` 并按 Enter 键，恢复重定基底操作。
