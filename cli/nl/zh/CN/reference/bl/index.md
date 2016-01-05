# bl 命令

*上次更新时间：*2015 年 11 月 13 日

如果您要构建 Node.js 应用程序，那么可以使用 Bluemix™ Live Sync 快速更新 Bluemix 上运行的应用程序实例，并像在桌面上进行操作一样进行开发，而无需重新部署。进行更改后，即可立即在运行中的 Bluemix 应用程序中看到该更改。Bluemix Live Sync 命令行界面称为 *bl*。

您可使用 **bl** 命令行界面命令完成以下任务：

* 启动和停止 Bluemix 上运行的应用程序。
* 从桌面创建新的基于云的项目
* 将更改从桌面同步到基于云的项目工作空间以及 Bluemix 上运行的应用程序。
* 请参阅可用于同步的项目列表。
* 请参阅正在运行的应用程序状态。

有关下载和使用 bl 命令的更多信息，请参阅 [Bluemix Live Sync](https://www.ng.bluemix.net/docs/manageapps/bluemixlive.html#bluemixlive)。

## bl 命令

Bluemix Live Sync 命令行 **bl** 的语法如下：

``` bl command [arguments][options] [--help]```

### 命令
<dl>
<dt>login, l</dt>
<dd>登录到 Bluemix。</dd>
<dt>logout, lo</dt>
<dd>注销用户。</dd>
<dt>sync, s</dt>
<dd>启动桌面和服务器之间的同步过程。</dd>
<dt>create, c</dt>
<dd>创建专用项目，将其链接到此目录中的 Git 存储库，然后将内容部署到 Bluemix。</dd>
<dt>projects, p</dt>
<dd>列出可用于同步的所有项目。</dd>
<dt>start, st</dt>
<dd>在 Bluemix 中启动应用程序实例。</dd>
<dt>stop, sp</dt>
<dd>在 Bluemix 中停止应用程序实例。</dd>
<dt>status, ss</dt>
<dd>列出 Bluemix 中正在运行的应用程序实例的状态。</dd>
</dl>

### 自变量
<dl>
<dd>命令的自变量。</dd>
</dl>

### 选项
<dl>
<dd>命令的选项。</dd>
</dl>

### 全局选项
<dl>
<dt>--help</dt>
<dd>显示指定命令的帮助页面</dd>
<dt>--verbose</dt>
<dd>启用详细日志记录。</dd>
</dl>

**注：**如果有任何自变量或选项包含空格，请将值用双引号括住。
