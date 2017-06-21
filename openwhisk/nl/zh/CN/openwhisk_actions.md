---

copyright:
  years: 2016, 2017
  lastupdated: "2017-04-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 创建并调用 {{site.data.keyword.openwhisk_short}} 操作
{: #openwhisk_actions}


操作是在 {{site.data.keyword.openwhisk}} 平台上运行的无状态代码片段。操作可以编写为 JavaScript、Swift 或 Python 函数，也可编写为 Java 方法或封装在 Docker 容器中的定制可执行程序。例如，操作可用于检测映像中的构面、响应数据库更改、聚集一组 API 调用或发布推文。
{:shortdesc}
操作可以显式调用，也可以作为对事件的响应来运行。对于其中任一情况，每次运行操作都会生成由唯一激活标识进行标识的激活记录。操作的输入和操作的结果是键/值对的字典，其中键为字符串，值为有效的 JSON 值。操作可以由对其他操作或对定义的操作序列的调用组成。

了解如何在首选开发环境中创建、调用和调试操作：
* [JavaScript](#openwhisk_create_action_js)
* [Swift](#openwhisk_actions_swift)
* [Python](#openwhisk_actions_python)
* [Java](#openwhisk_actions_java)
* [Docker](#openwhisk_actions_docker)

此外，请了解：

* [监视操作输出](#openwhisk_actions_polling)
* [列出操作](#openwhisk_listing_actions)
* [删除操作](#openwhisk_delete_action)
* [访问操作体中的操作元数据](#openwhisk_action_metadata)


## 创建并调用 JavaScript 操作
{: #openwhisk_create_action_js}

以下各部分指导您使用 JavaScript 中的操作。您从创建和调用简单的操作开始。然后，继续向操作添加参数，并使用这些参数来调用该操作。接下来，设置缺省参数并对它们进行调用。然后，创建异步操作并最终使用操作序列。


### 创建并调用简单 JavaScript 操作
{: #openwhisk_single_action_js}

查看以下步骤和示例以创建第一个 JavaScript 操作。

1. 创建具有以下内容的 JavaScript 文件。对于此示例，文件名为“hello.js”。

  ```javascript
  function main() {
      return {payload: 'Hello world'};
  }
  ```
  {: codeblock}

  JavaScript 文件可能包含其他函数。但是，根据约定，名为 `main` 的函数必须存在，才能为操作提供入口点。



2. 通过以下 JavaScript 函数创建操作。对于此示例，操作名为“hello”。

  ```
  wsk action create hello hello.js
  ```
  {: pre}
  ```
  ok: created action hello
  ```

3. 列出已创建的操作：

  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  hello       private
  ```

  您可以看到刚才创建的 `hello` 操作。

4. 创建操作后，可以使用“invoke”命令在 OpenWhisk 的云中运行该操作。可以通过在命令中指定标记以使用*阻塞*调用（即，请求/响应样式）或*非阻塞*调用来调用操作。阻塞调用请求将*等待*激活结果可用。等待时间段为 60 秒或为操作的已配置[时间限制](./openwhisk_reference.html#openwhisk_syslimits)（两者取较短的时间）。如果激活结果在等待时间段内可用，那么会返回激活结果。否则，激活会继续在系统中处理，并返回激活标识，以便可以稍后检查结果，这与非阻塞请求一样（请参阅[此处](#openwhisk_actions_polling)，以获取有关监视激活的提示）。

  此示例使用的是阻塞参数 `--blocking`：

  ```
  wsk action invoke --blocking hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
    ```
  ```json
  {
    "result": {
          "payload": "Hello world"
      },
      "status": "success",
      "success": true
  }
  ```

  此命令输出两条重要的信息：
  * 激活标识 (`44794bd6aab74415b4e42a308d880e5b`)
  * 如果激活结果在预期的等待时间段内可用，那么输出调用结果

  在本例中，结果为 JavaScript 函数返回的字符串 `Hello world`。激活标识可以用于在未来检索调用的日志或结果。  

5. 如果不是立即需要操作结果，可以省略 `--blocking` 标记以进行非阻塞调用。可以在以后使用激活标识来获取结果。请参阅以下示例：

  ```
  wsk action invoke hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 6bf1f670ee614a7eb5af3c9fde813043
  ```

  ```
  wsk activation result 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: pre}
  ```json
  {
      "payload": "Hello world"
  }
  ```

6. 如果忘记了记录激活标识，那么可以获取激活列表，其中激活按从最新到最旧的顺序列出。运行以下命令来获取激活列表：

  ```
  wsk activation list
  ```
  {: pre}
  ```
  activations
  44794bd6aab74415b4e42a308d880e5b         hello
  6bf1f670ee614a7eb5af3c9fde813043         hello
  ```

### 向操作传递参数

调用操作时，可以将参数传递给操作。

1. 在操作中使用参数。例如，使用以下内容来更新“hello.js”文件：

  ```javascript
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

  输入参数会作为 JSON 对象参数传递给 `main` 函数。请注意此示例中的 `name` 和 `place` 参数是如何从 `params` 对象检索到的。

2. 将 `name` 和 `place` 参数值传递给 `hello` 操作时，更新并调用该操作。请参阅以下示例：

  ```
  wsk action update hello hello.js
  ```
  {: pre}

3.  参数可以在命令行上显式提供，也可以通过提供包含所需参数的文件来提供。

  要直接通过命令行来传递参数，请向 `--param` 标志提供键/值对：
  ```
  wsk action invoke --blocking --result hello --param name Bernie --param place Vermont
  ```
  {: pre}

  为了使用包含参数内容的文件，请创建 JSON 格式的包含参数的文件。然后，必须将文件名传递到 `param-file` 标志：

  名为 parameters.json 的示例参数文件：
  ```json
  {
      "name": "Bernie",
      "place": "Vermont"
  }
  ```
  {: codeblock}

  ```
  wsk action invoke --blocking --result hello --param-file parameters.json
  ```
  {: pre}

  ```json
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```

  使用 `--result` 选项时请注意：此选项暗含 CLI 等待激活完成并随后仅显示激活结果的阻塞性调用。为了方便起见，使用此选项时可不带 `--blocking`，系统会自动推断出阻塞性。

### 设置缺省参数
{: #openwhisk_binding_actions}

操作可以通过多个指定参数进行调用。重新调用上面示例中的 `hello` 操作需要两个参数：*name*（人员的姓名）和 *place*（人员所在位置）。

您可以绑定特定参数，而不用每次将所有参数传递给操作。以下示例绑定 *place* 参数，以便操作的缺省位置为“Vermont”：

1. 更新该操作，方法是使用 `--param` 选项来绑定参数值，或者将包含参数的文件传递到 `--param-file`。

  要在命令行上显式指定缺省参数，请向 `param` 标志提供键/值对：

  ```
  wsk action update hello --param place Vermont
  ```
  {: pre}

  从文件传递参数需要创建包含所需内容的 JSON 格式的文件。然后，必须将文件名传递到 `-param-file` 标志：

  名为 parameters.json 的示例参数文件：
  ```json
  {
      "place": "Vermont"
  }
  ```
  {: codeblock}

  ```
  wsk action update hello --param-file parameters.json
  ```
  {: pre}

2. 调用操作，但这次只传递 `name` 参数。

  ```
  wsk action invoke --blocking --result hello --param name Bernie
  ```
  {: pre}
  ```json
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```

  请注意，调用操作时，无需指定 place 参数。绑定的参数仍可以通过在调用时指定该参数值来进行覆盖。



3. 调用操作，并同时传递 `name` 和 `place` 值。后者将覆盖绑定到操作的值。

  使用 `--param` 标志：

  ```
  wsk action invoke --blocking --result hello --param name Bernie --param place "Washington, DC"
  ```
  {: pre}

  使用 `--param-file` 标志：

  文件 parameters.json：
  ```json
  {
    "name": "Bernie",
    "place": "Vermont"
  }
  ```
  {: codeblock}
  ```
  wsk action invoke --blocking --result hello --param-file parameters.json
  ```
  {: pre}
  
  ```json
  {  
      "payload": "Hello, Bernie from Washington, DC"
  }
  ```

### 创建异步操作
{: #openwhisk_asynchrony_js}

`main` 函数返回后，异步运行的 JavaScript 函数可能需要返回激活结果。通过在操作中返回 Promise，可实现此目的。

1. 将以下内容保存在名为 `asyncAction.js` 的文件中。

  ```javascript
  function main(args) {
       return new Promise(function(resolve, reject) {
         setTimeout(function() {
          resolve({ done: true });
         }, 2000);
      })
   }
  ```
  {: codeblock}

  请注意，`main` 函数会返回 Promise，其指示激活尚未完成，但是预期在未来完成。

  在本例中，`setTimeout()` JavaScript 函数会等待 2 秒再调用回调函数。这代表异步代码，并进入 Promise 的回调函数。

  Promise 的回调函数采用两个自变量 resolve 和 reject，这两个自变量都是函数。`resolve()` 的调用会履行 Promise 并指示激活已正常完成。

  `reject()` 的调用可用于拒绝 Promise 并指示激活异常完成。

2. 运行以下命令来创建并调用操作：

  ```
  wsk action create asyncAction asyncAction.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result asyncAction
  ```
  {: pre}
  ```json
  {
      "done": true
  }
  ```

  请注意，您执行的是对异步操作的阻塞调用。



3. 访存激活日志以查看完成激活所用的时间：

  ```
  wsk activation list --limit 1 asyncAction
  ```
  {: pre}
  ```
  activations
  b066ca51e68c4d3382df2d8033265db0             asyncAction
  ```


  ```
  wsk activation get b066ca51e68c4d3382df2d8033265db0
  ```
  {: pre}
 ```json
  {
      "start": 1455881628103,
      "end":   1455881648126
  }
  ```

  通过比较激活记录中的 `start` 和 `end` 时间戳记，可以看出完成此激活所用时间略微超过 2 秒。




### 使用操作来调用外部 API
{: #openwhisk_apicall_action}

到目前为止，示例都是自包含 JavaScript 函数。您还可以创建调用外部 API 的操作。

以下示例调用 Yahoo Weather 服务来获取特定位置的当前天气状况。

1. 将以下内容保存在名为 `weather.js` 的文件中。


  ```javascript
  var request = require('request');

  function main(params) {
     var location = params.location || 'Vermont';
        var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';
    
        return new Promise(function(resolve, reject) {
            request.get(url, function(error, response, body) {
            if (error) {
                    reject(error);    
                }
                else {
                    var condition = JSON.parse(body).query.results.channel.item.condition;
                    var text = condition.text;
                    var temperature = condition.temp;
                    var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
                    resolve({msg: output});
                }
            });
      });
  }
  ```
  {: codeblock}

  请注意，示例中的操作使用 JavaScript `request` 库向 Yahoo Weather API 发起 HTTP 请求，然后从 JSON 结果中抽取字段。[参考](./openwhisk_reference.html#openwhisk_ref_javascript_environments)详细描述了可以在操作中使用的 Node.js 包。

  此示例还显示了需要异步操作。此操作返回 Promise，指示函数返回时此操作的结果尚不可用。相反，结果会在 HTTP 调用完成后在 `request` 回调中提供，并且会作为自变量传递给 `resolve()` 函数。

2. 运行以下命令来创建并调用操作：

  ```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location "Brooklyn, NY"
  ```
  {: pre}
  ```json
  {
      "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
  }
  ```

### 将操作包装为 Node.js 模块
{: #openwhisk_js_packaged_action}

作为在单个 JavaScript 源文件中编写所有操作码的替代方法，可以将操作编写为 `npm` 包。例如，假设一个目录包含以下文件：

首先是 `package.json`：

```json
{
  "name": "my-action",
  "main": "index.js",
  "dependencies" : {
    "left-pad" : "1.1.3"
  }
}
```
{: codeblock}

接着是 `index.js`：

```javascript
function myAction(args) {
    const leftPad = require("left-pad")
    const lines = args.lines || [];
    return { padded: lines.map(l => leftPad(l, 30, ".")) }
}

exports.main = myAction;
```
{: codeblock}

请注意，操作将通过 `exports.main` 公开；操作处理程序本身可以具有任何名称，只要名称符合接受对象和返回对象（或对象的 `Promise`）的通常特征符即可。根据 Node.js 约定，您必须将此文件命名为 `index.js`，或者将您偏好的文件名指定为 package.json 中的 `main` 属性。

要通过此包创建 OpenWhisk 操作，请执行以下操作：

1. 首先在本地安装所有依赖关系

  ```
  npm install
  ```
  {: pre}

2. 创建包含所有文件（包括所有依赖关系）的 `.zip` 归档：

  ```
  zip -r action.zip *
  ```
  {: pre}

    > 请注意：使用 Windows 资源管理器操作来创建 zip 文件将导致结构不正确。OpenWhisk zip 操作必须在 zip 的根目录中具有 `package.json`，而 Windows 资源管理器会将其放入嵌套文件夹内。最安全的选项是如上所示，在命令行上使用 `zip` 命令。


3. 创建操作：

  ```
  wsk action create packageAction --kind nodejs:6 action.zip
  ```
  {: pre}

  请注意，使用 CLI 工具从 `.zip` 归档创建操作时，必须为 `--kind` 标志显式提供值。

4. 可以像调用其他任何操作一样来调用此操作：

  ```
  wsk action invoke --blocking --result packageAction --param lines "[\"and now\", \"for something completely\", \"different\" ]"
  ```
  {: pre}
  ```json
  {
      "padded": [
          ".......................and now",
          "......for something completely",
          ".....................different"
      ]
  }
  ```


最后，请注意，虽然大部分 `npm` 包会在执行 `npm install` 时安装 JavaScript 源代码，但还有些 npm 包会安装并编译二进制工件。目前，归档文件上传不支持二进制依赖关系，而只支持 JavaScript 依赖关系。如果归档包含二进制依赖关系，那么操作调用可能会失败。

## 创建操作序列
{: #openwhisk_create_action_sequence}

可以创建用于将一序列操作链接在一起的操作。

在名为 `/whisk.system/utils` 的包中提供了多个实用程序操作，可用于创建第一个序列。您可以在[包](./openwhisk_packages.html)部分中了解有关包的更多信息。

1. 显示 `/whisk.system/utils` 包中的操作。

  ```
  wsk package get --summary /whisk.system/utils
  ```
  {: pre}
  ```
  package /whisk.system/utils：构建用于设置数据格式和组合数据的块
   action /whisk.system/utils/head：抽取数组的前缀
   action /whisk.system/utils/split：将字符串拆分成数组
   action /whisk.system/utils/sort：对数组排序
   action /whisk.system/utils/echo：返回输入
   action /whisk.system/utils/date：当前日期和时间
   action /whisk.system/utils/cat：将输入连接成一个字符串
  ```


  您将使用此示例中的 `split` 和 `sort` 操作。

2. 创建操作序列，使一个操作的结果作为自变量传递给下一个操作。

  ```
  wsk action create sequenceAction --sequence /whisk.system/utils/split,/whisk.system/utils/sort
  ```
  {: pre}

  此操作序列会将一些文本行转换为数组，然后对这些行排序。

3. 调用操作：

  ```
  wsk action invoke --blocking --result sequenceAction --param payload "Over-ripe sushi,\nThe Master\nIs full of regret."
  ```
  {: pre}
  ```json
  {
      "length": 3,
      "lines": [
          "Is full of regret.",
          "Over-ripe sushi,",
          "The Master"
      ]
  }
  ```


  在结果中，您会看到这些行已排序。

**注**：在序列中的操作之间传递的参数为显式参数，但缺省参数除外。因此，传递到操作序列的参数只可用于序列中的第一个操作。序列中第一个操作的结果成为序列中第二个操作的输入 JSON 对象（依此类推）。此对象不包含初始传递到序列的任何参数，除非第一个操作在其结果中显式包含这些参数。操作的输入参数会与操作的缺省参数合并，并且操作的输入参数优先于并覆盖任何匹配的缺省参数。有关使用多个指定参数来调用操作序列的更多信息，请参阅[设置缺省参数](./openwhisk_actions.html#openwhisk_binding_actions)。

## 创建 Python 操作
{: #openwhisk_actions_python}

创建 Python 操作的过程与创建 JavaScript 操作的过程类似。以下各部分将指导您创建并调用单个 Python 操作，然后向该操作添加参数。

### 创建并调用 Python 操作
{: #openwhisk_actions_python_invoke}

操作其实就是顶级 Python 函数。例如，创建名为 `hello.py` 的文件并包含以下源代码：

```python
def main(args):
    name = args.get("name", "stranger")
    greeting = "Hello " + name + "!"
    print(greeting)
        return {"greeting": greeting}
```
{: codeblock}

Python 操作始终会使用一个字典并生成一个字典。缺省情况下，操作的入口方法为 `main`，但与其他任何操作类型一样，在使用 `wsk` CLI 通过 `--main` 创建该操作时可显式指定入口方法。

可以通过此函数创建名为 `helloPython` 的 OpenWhisk 操作，如下所示：

```
wsk action create helloPython hello.py
```
{: pre}
CLI 会根据源文件扩展名自动推断操作类型。对于 `.py` 源文件，操作会使用 Python 2.7 运行时运行。还可以通过显式指定参数 `--kind python:3`，创建使用 Python 3.6 运行的操作。请参阅 Python [参考](./openwhisk_reference.html#openwhisk_ref_python_environments)，以获取有关 Python 2.7 与 3.6 比较情况的更多信息。
Python 操作的操作调用与 JavaScript 操作的操作调用相同：

```
wsk action invoke --blocking --result helloPython --param name World
```
{: pre}

```json
  {
      "greeting": "Hello World!"
  }
```

### 将 Python 操作打包成 zip 文件
{: #openwhisk_actions_python_zip}

您可以将 Python 操作和从属模块打包成 zip 文件。包含入口点（例如，`main`）的源文件的文件名必须为 `__main__.py`。例如，要创建具有名为 `helper.py` 的帮助程序模块的操作，请先创建包含源文件的归档：

```bash
zip -r helloPython.zip __main__.py helper.py
```
{: pre}

然后，创建操作：



```bash
wsk action create helloPython --kind python:3 helloPython.zip
```
{: pre}

### 使用虚拟环境将 Python 操作打包成 zip 文件
{: #openwhisk_actions_python_virtualenv}

另一种打包 Python 依赖项的方法是使用虚拟环境 (`virtualenv`)。这允许您链接其他包，例如可能通过 [`pip`](https://packaging.python.org/installing/) 安装的包。
要确保与 OpenWhisk 容器的兼容性，virtualenv 内部的包安装必须在目标环境中完成。
所以，应该使用 Docker 映像 `openwhisk/python2action` 或 `openwhisk/python3action` 来为操作创建 virtualenv 目录。

与基本 zip 文件支持一样，包含主入口点的源文件的名称必须为 `__main__.py`。此外，virtualenv 目录必须命名为 `virtualenv`。下面是安装依赖项、将其打包在 virtualenv 中并创建兼容 OpenWhisk 操作的示例场景。



1. 假设 `requirements.txt` 文件中包含要安装的 `pip` 模块和版本，请运行以下命令以安装依赖项，并使用兼容 Docker 映像创建 virtualenv：
 ```bash
 docker run --rm -v "$PWD:/tmp" openwhisk/python3action sh \
   -c "cd tmp; virtualenv virtualenv; source virtualenv/bin/activate; pip install -r requirements.txt;"
 ```
 {: pre}

2. 归档 virtualenv 目录及其他任何 Python 文件：
 ```bash
 zip -r helloPython.zip virtualenv __main__.py
 ```
 {: pre}

3. 创建操作：
  ```bash
  wsk action create helloPython --kind python:3 helloPython.zip
  ```
  {: pre}

虽然上面显示的步骤是针对 Python 3.6 的，但也同样适用于 Python 2.7。


## 创建 Swift 操作

创建 Swift 操作的过程与创建 JavaScript 操作的过程类似。以下各部分将指导您创建并调用单个 Swift 操作，然后向该操作添加参数。

您还可以使用在线 [Swift Sandbox](https://swiftlang.ng.bluemix.net) 来测试 Swift 代码，而不必在您的计算机上安装 Xcode。

### 创建并调用操作

操作仅仅是顶级 Swift 函数。例如，创建名为 `hello.swift` 的文件并包含以下内容：

```swift
func main(args: [String:Any]) -> [String:Any] {
    if let name = args["name"] as? String {
          return [ "greeting" : "Hello \(name)!" ]
    } else {
return [ "greeting" : "Hello stranger!" ]
    }
}
```
{: codeblock}

Swift 操作始终会使用一个字典并生成一个字典。

可以通过此函数创建名为 `helloSwift` 的 {{site.data.keyword.openwhisk_short}} 操作，如下所示：

```
wsk action create helloSwift hello.swift
```
{: pre}

使用命令行和 `.swift` 源文件时，无需指定您要创建 Swift 操作（与 JavaScript 操作相反）；该工具会根据文件扩展名来进行确定。

Swift 操作的操作调用与 JavaScript 操作的操作调用相同：



```
wsk action invoke --blocking --result helloSwift --param name World
```
{: pre}

```json
  {
    "greeting": "Hello World!"
  }
```

**注意：**Swift 操作在 Linux 环境中运行。Swift on Linux 仍在开发中；{{site.data.keyword.openwhisk_short}} 通常会使用最新可用发行版，但此版本不一定稳定。此外，用于 {{site.data.keyword.openwhisk_short}} 的 Swift 版本可能与 Mac OS 上 Xcode 的稳定发行版中的 Swift 版本不一致。

### 将操作包装为 Swift 可执行文件
{: #openwhisk_actions_swift_zip}

使用 Swift 源文件创建 OpenWhisk Swift 操作后，必须先将该文件编译成二进制文件，才能运行该操作。一旦这样做后，对该操作的后续调用会快得多，直到清除保留该操作的容器为止。此延迟称为冷启动延迟。

要避免冷启动延迟，可以将 Swift 文件编译为二进制文件，然后将其以 zip 文件格式上传到 OpenWhisk。在需要 OpenWhisk 脚手架时，创建二进制文件最简单的方法是在与其将运行的环境相同的环境中进行构建。下面是具体步骤：



- 运行交互式 Swift 操作容器。
```
docker run --rm -it -v "$(pwd):/owexec" openwhisk/swift3action bash
```
{: pre}

    这会将您置于 Docker 容器内的 Bash shell 中。在其中执行以下命令：



- 为了方便起见，请安装 zip，以用于打包二进制文件
  ```
  apt-get install -y zip
  ```
  {: pre}
- 复制源代码并准备对其进行构建
  
  ```
  cp /owexec/hello.swift /swift3Action/spm-build/main.swift
  ```
  {: pre}
  ```
  cat /swift3Action/epilogue.swift >> /swift3Action/spm-build/main.swift
  ```
  {: pre}
  ```
  echo '_run_main(mainFunction:main)' >> /swift3Action/spm-build/main.swift
  ```
  {: pre}
- zBuild 和链接
  
  ```
  /swift3Action/spm-build/swiftbuildandlink.sh
  ```
  {: pre}
- 创建 zip 归档
  
  ```
  cd /swift3Action/spm-build
  ```
  {: pre}
  ```
  zip /owexec/hello.zip .build/release/Action
  ```
- 退出 Docker 容器
  ```
  exit
  ```
  {: pre}
这已在 hello.swift 所在的目录中创建 hello.zip。
-使用名为 helloSwifty 的操作将其上传到 OpenWhisk：
  ```
  wsk action update helloSwiftly hello.zip --kind swift:3
  ```
  {: pre}
- 要检查其运行速度提高了多少，请运行
   
  ```
  wsk action invoke helloSwiftly --blocking
  ``` 
  {: pre}

操作运行所用的时间会填写在“duration”属性中，并会与运行 hello 操作中编译步骤所用的时间进行比较。

## 创建 Java 操作
{: #openwhisk_actions_java}

创建 Java 操作的过程与创建 JavaScript 和 Swift 操作的过程类似。以下各部分将指导您创建并调用单个 Java 操作，然后向该操作添加参数。

为了编译、测试和归档 Java 文件，您必须在本地安装 [JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html)。

### 创建并调用操作
{: #openwhisk_actions_java_invoke}

Java 操作是包含名为 `main` 的方法的 Java 程序，该方法的特征符与以下内容完全一样：
```java
public static com.google.gson.JsonObject main(com.google.gson.JsonObject);
```
{: codeblock}

例如，创建名为 `Hello.java` 的 Java 文件并包含以下内容：

```java
import com.google.gson.JsonObject;
public class Hello {
    public static JsonObject main(JsonObject args) {
        String name = "stranger";
        if (args.has("name"))
            name = args.getAsJsonPrimitive("name").getAsString();
        JsonObject response = new JsonObject();
        response.addProperty("greeting", "Hello " + name + "!");
        return response;
    }
}
```
{: codeblock}

然后，将 `Hello.java` 编译成 JAR 文件 `hello.jar`，如下所示：
```
javac Hello.java
```
{: pre}
```
jar cvf hello.jar Hello.class
```
{: pre}

**注：**编译 Java 文件时，[google-gson](https://github.com/google/gson) 必须存在于 Java CLASSPATH 中。

可以按如下所示从此 JAR 文件创建名为 `helloJava` 的 OpenWhisk 操作：

```
wsk action create helloJava hello.jar --main Hello
```

使用命令行和 `.jar` 源文件时，无需指定您要创建 Java 操作；该工具会根据文件扩展名来进行确定。

您需要使用 `--main` 来指定主类的名称。符合要求的主类是实现了如上所述静态 `main` 方法的主类。如果该类不在缺省包中，请使用 Java 标准类名，例如 `--main com.example.MyMain`。

Java 操作的操作调用与 Swift 和 JavaScript 操作的操作调用相同：



```
wsk action invoke --blocking --result helloJava --param name World
```
{: pre}

```json
  {
    "greeting": "Hello World!"
  }
```

## 创建 Docker 操作

通过 {{site.data.keyword.openwhisk_short}} Docker 操作，可以使用任何语言编写操作。

您的代码会编译为可执行二进制文件，并嵌入到 Docker 映像中。二进制程序通过采用来自 `stdin` 的输入并通过 `stdout` 进行回复，从而与系统进行交互。

作为先决条件，您必须拥有 Docker Hub 帐户。要设置免费 Docker 标识和帐户，请转至 [Docker Hub](https://hub.docker.com)。

对于后续指示信息，假定 Docker 用户标识为 `janesmith`，密码为 `janes_password`。假定已设置 CLI，必须执行三个步骤来设置定制二进制文件以供 {{site.data.keyword.openwhisk_short}} 使用。在此之后，上传的 Docker 映像即可用作操作。



1. 下载 Docker 框架。可以使用 CLI 进行下载，如下所示：

  

  ```
  wsk sdk install docker
  ```
  {: pre}
  ```
  现在，Docker 框架已安装在当前目录中。
  ```

  ```
  ls dockerSkeleton/
  ```
  {: pre}
  ```
  Dockerfile      README.md       buildAndPush.sh example.c
  ```

  框架是一种 Docker 容器模板，可以在其中以定制二进制文件的形式插入代码。 

2. 在 Docker 框架中设置定制二进制文件。该框架已经包含可以使用的 C 程序。

  ```
  cat dockerSkeleton/example.c
  ```
  {: pre}
  ```c
  #include <stdio.h>
  int main(int argc, char *argv[]) {
            printf("This is an example log message from an arbitrary C program!\n");
      printf("{ \"msg\": \"Hello from arbitrary C program!\", \"args\": %s }",
             (argc == 1) ? "undefined" : argv[1]);
  }
  ```
  {: codeblock}

  可以根据需要修改此文件，或者向 Docker 映像添加其他代码和依赖关系。对于后者，可能需要根据需要对 `Dockerfile` 进行调整，才能构建可执行文件。二进制文件必须位于容器内的 `/action/exec` 中。

  可执行文件会从命令行接收单个自变量。该自变量是字符串序列化的 JSON 对象，表示操作的自变量。程序可能会记录到 `stdout` 或 `stderr`。根据约定，输出的最后一行*必须*是字符串化的 JSON 对象，用于表示操作结果。

3. 使用提供的脚本来构建 Docker 映像并进行上传。必须首先运行 `docker login` 以进行认证，然后使用所选映像名称来运行脚本。

  ```
  docker login -u janesmith -p janes_password
  ```
  {: pre}
  ```
  cd dockerSkeleton
  ```
  {: pre}
  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}

  请注意，在 Docker 映像构建过程中，会对 example.c 文件中的部分内容进行编译，所以无需在您的计算机上对 C 程序进行编译。事实上，除非要在兼容主机上编译二进制文件，否则其不会在容器内部运行，因为格式不匹配。

  现在，Docker 容器可用作 {{site.data.keyword.openwhisk_short}} 操作。

  ```
  wsk action create --docker example janesmith/blackboxdemo
  ```
  {: pre}

  请注意，创建操作时使用 `--docker`。目前，假定所有 Docker 映像都在 Docker Hub 上进行托管。该操作可能会作为其他任何 {{site.data.keyword.openwhisk_short}} 操作进行调用。

  ```
  wsk action invoke --blocking --result example --param payload Rey
  ```
  {: pre}
  ```json
  {
    "args": {
          "payload": "Rey"
      },
      "msg": "Hello from arbitrary C program!"
  }
  ```

  要更新 Docker 操作，请运行 buildAndPush.sh 以将最新的映像上传到 Docker Hub。这将允许系统在下次运行操作的代码时，拉取新的 Docker 映像。如果没有运行中的容器，那么任何新调用都将使用新的 Docker 映像。但是，如果有使用前版 Docker 映像的运行中容器，那么除非运行 `wsk action update`，否则任何新调用都将继续使用该映像。这将指示系统对于任何新调用，都应该执行 docekr pull 来获取新的 Docker 映像。

  

  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}

  ```
  wsk action update --docker example janesmith/blackboxdemo
  ```
  {: pre}

  您可以在[参考](./openwhisk_reference.html#openwhisk_ref_docker)部分中找到有关创建 Docker 操作的更多信息。

## 监视操作输出
{: #openwhisk_actions_polling}

{{site.data.keyword.openwhisk_short}} 操作可能会由其他用户调用，以响应各种事件或作为操作序列的组成部分。在此类情况下，监视调用会非常有用。

可以使用 {{site.data.keyword.openwhisk_short}} CLI 在调用操作时监视其输出。

1. 在 shell 中发出以下命令：
  ```
  wsk activation poll
  ```
  {: pre}

  此命令将启动轮询循环，以持续检查从激活生成的日志。

2. 切换到其他窗口，并调用操作：

  ```
  wsk action invoke /whisk.system/samples/helloWorld --param payload Bob
  ```
  {: pre}
  ```
  ok: invoked /whisk.system/samples/helloWorld with id 7331f9b9e2044d85afd219b12c0f1491
  ```

3. 观察轮询窗口中的激活日志：

  ```
  Activation: helloWorld (7331f9b9e2044d85afd219b12c0f1491)
    2016-02-11T16:46:56.842065025Z stdout: hello bob!
  ```

    与此类似，每当运行轮询实用程序时，都会实时看到 OpenWhisk 中代表您运行的任何操作的日志。





## 列出操作
{: #openwhisk_listing_actions}

您可以使用以下命令列出已创建的所有操作：

```
wsk action list
```
{: pre}

随着您编写更多操作，此列表会变长，因此将相关操作分组成[包](./openwhisk_packages.html)会很有用。要过滤操作列表以只列出特定包中的操作，可以使用以下命令：

 

```
wsk action list [PACKAGE NAME]
```
{: pre}


## 删除操作
{: #openwhisk_delete_action}

可以通过删除不想使用的操作来进行清理。

1. 运行以下命令来删除操作：
  ```
  wsk action delete hello
  ```
  {: pre}
  ```
  ok: deleted hello
  ```

2. 验证该操作是否不再出现在操作列表中。
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  ```
  {: pre}

## 访问操作体中的操作元数据
{: #openwhisk_action_metadata}

操作环境包含多个特定于运行中操作的属性。这些属性允许操作以编程方式通过 REST API 来使用 OpenWhisk 资产，或者允许设置在操作即将耗尽其分配的时间预算时发出内部警报。使用 OpenWhisk Docker 框架时，这些属性可通过所有受支持运行时的系统环境进行访问：Node.js、Python、Swift、Java 和 Docker 操作。

* `__OW_API_HOST`：运行此操作的 OpenWhisk 部署的 API 主机
* `__OW_API_KEY`：调用此操作的主体的 API 密钥，此密钥可能是受限制的 API 密钥
* `__OW_NAMESPACE`：*激活*的名称空间（这可能与操作的名称空间不同）
* `__OW_ACTION_NAME`：运行中操作的标准名称
* `__OW_ACTIVATION_ID`：此运行中操作实例的激活标识
* `__OW_DEADLINE`：此操作将耗尽整个持续时间配额时的近似时间（以戳记毫秒为度量单位）
