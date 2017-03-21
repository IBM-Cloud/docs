---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 GitHub 包
{: #openwhisk_catalog_github}

通过 `/whisk.system/github` 包，可以方便地使用 [GitHub API](https://developer.github.com/)。

此包中包含以下订阅源：

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/github` | 包 | username、repository 和 accessToken | 与 GitHub API 进行交互 |
| `/whisk.system/github/webhook` | 订阅源 | events、username、repository 和 accessToken | 对 GitHub 活动触发触发器事件 |

建议使用 `username`、`repository` 和 `accessToken` 值创建包绑定。通过绑定，就无需在每次使用包中的订阅源时指定这些值。

## 使用 GitHub 活动触发触发器事件

`/whisk.system/github/webhook` 订阅源将服务配置为当指定的 GitHub 存储库中发生活动时触发触发器。参数如下所示：

- `username`：GitHub 存储库的用户名。
- `repository`：GitHub 存储库。
- `accessToken`：您的 GitHub 个人访问令牌。[创建令牌](https://github.com/settings/tokens)时，请确保选择 repo:status 和 public_repo 作用域。此外，请确保还没有为存储库定义任何 Webhook。
- `events`：相关的 [GitHub 事件类型](https://developer.github.com/v3/activity/events/types/)。

下面是创建触发器的示例，此触发器将在每次 GitHub 存储库中发生新落实时触发。

1. 生成 GitHub [个人访问令牌](https://github.com/settings/tokens)。
  
  下一步中将使用此访问令牌。
  
2. 使用访问令牌创建为您的 GitHub 存储库配置的包绑定。
  
  ```
  wsk package bind /whisk.system/github myGit \
    --param username myGitUser \
    --param repository myGitRepo \
    --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}
  
3. 使用 `myGit/webhook` 订阅源为 GitHub `push` 事件类型创建触发器。
  
  ```
wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}
  
  使用 `git push` 对 Github 存储库作出的承诺将导致触发器由 Webhook 触发。如果存在与触发器匹配的规则，那么将会调用相关联的操作。
该操作会接收 GitHub Webhook 有效内容作为输入参数。每一个 GitHub Webhook 事件都具有相似的 JSON 模式，但是却是事件类型所确定的唯一有效内容对象。
有关更多有效内容的内容信息，请参阅 [GitHub 事件和有效内容](https://developer.github.com/v3/activity/events/types/) API 文档。
  
