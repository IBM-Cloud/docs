---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 创建并调用 {{site.data.keyword.openwhisk_short}} 操作
{: #openwhisk_actions}

*上次更新时间：2016 年 3 月 22 日*

操作是在 {{site.data.keyword.openwhisk}} 平台上运行的无状态代码片段。操作可以是 JavaScript 函数、Swift 函数或封装在 Docker 容器中的定制可执行程序。例如，操作可用于检测映像中的构面、聚集一组 API 调用或发布推文。
{:shortdesc}

操作可以显式调用，也可以作为对事件的响应来运行。对于其中任一情况，运行操作都会生成由唯一激活标识进行识别的激活记录。操作的输入和操作的结果是键/值对的字典，其中键为字符串，值为有效的 JSON 值。

操作可以由对其他操作的调用组成，也可以由定义的操作序列组成。

## 创建并调用 JavaScript 操作
{: #openwhisk_create_action_js}

以下各部分指导您使用 JavaScript 中的操作。首先创建并调用简单操作，然后向操作添加参数，并使用这些参数来调用该操作，设置并调用缺省参数，创建异步操作，最后使用操作序列。


### 创建并调用简单 JavaScript 操作
{: #openwhisk_single_action_js}

查看以下步骤和示例以创建第一个 JavaScript 操作。

1. 创建具有以下内容的 JavaScript 文件。对于此示例，文件名为“hello.js”。
  
  ```
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
  {: screen}

3. 列出已创建的操作：
  
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  hello       private
  ```
  {: screen}

  您可以看到刚才创建的 `hello` 操作。

4. 创建操作后，可以使用“invoke”命令在 {{site.data.keyword.openwhisk_short}} 的云中运行该操作。可以通过在命令中指定标记以使用*阻塞*调用或*非阻塞*调用来调用操作。阻塞调用会等待操作运行至完成并返回结果。此示例使用的是阻塞参数 `-blocking`：

  ```
  wsk action invoke --blocking hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
  response:
  {
      "result": {
          "payload": "Hello world"
      },
      "status": "success",
      "success": true
  }
  ```
  {: screen}

  此命令输出两条重要的信息：
  * 激活标识 (`44794bd6aab74415b4e42a308d880e5b`)
  * 调用结果

  在本例中，结果为 JavaScript 函数返回的字符串 `Hello world`。激活标识可以用于在未来检索调用的日志或结果。  

5. 如果不是立即需要操作结果，可以省略 `--blocking` 标记以进行非阻塞调用。可以在以后使用激活标识来获取结果。请参阅以下示例：

  ```
  wsk action invoke hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: screen}

  ```
  wsk activation result 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: pre}
  ```
  {
      "payload": "Hello world"
  }
  ```
  {: screen}

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
  {: screen}

### 向操作传递参数
{: #openwhisk_adding_parameters_js}

调用操作时，可以将参数传递给操作。

1. 在操作中使用参数。例如，使用以下内容来更新“hello.js”文件：
  
  ```
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
  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Vermont'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  请注意，使用 `--param` 选项可指定参数名称和值，使用 `--result` 选项将仅显示调用结果。

### 设置缺省参数
{: #openwhisk_binding_actions}

操作可以通过多个指定参数进行调用。重新调用上面示例中的 `hello` 操作需要两个参数：*name*（人员的姓名）和 *place*（人员所在位置）。

您可以绑定特定参数，而不用每次将所有参数传递给操作。以下示例绑定 *place* 参数，以便操作的缺省位置为“Vermont”：
 
1. 使用 `--param` 选项更新操作以绑定参数值。

  ```
  wsk action update hello --param place 'Vermont'
  ```
  {: pre}

2. 调用操作，但这次只传递 `name` 参数。

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  请注意，调用操作时，无需指定 place 参数。绑定的参数仍可以通过在调用时指定该参数值来进行覆盖。

3. 调用操作，并同时传递 `name` 和 `place` 值。后者将覆盖绑定到操作的值。

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Washington, DC'
  ```
  {: pre}
  ```
  {  
      "payload": "Hello, Bernie from Washington, DC"
  }
  ```
  {: screen}

### 创建异步操作
{: #openwhisk_asynchrony_js}

`main` 函数返回后，继续在回调函数中执行的 JavaScript 函数可能需要返回激活结果。可以在您的操作中使用 `whisk.async()` 和 `whisk.done()` 函数来完成此步骤。

1. 将以下内容保存在名为 `asyncAction.js` 的文件中。

  ```
  function main() {
      setTimeout(function() {
          return whisk.done({done: true});
      }, 20000);
      return whisk.async();
  }
  ```
  {: codeblock}

  请注意，`main` 函数会立即返回，并且 `whisk.async()` 返回值指示此激活应该继续运行。

  在本例中，`setTimeout()` JavaScript 函数会等待 20 秒再调用回调函数，其中对 `whisk.done()` 的调用指示激活已完成。

2. 运行以下命令来创建并调用操作：

  ```
  wsk action create asyncAction asyncAction.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result asyncAction
  ```
  {: pre}
  ```
  {
      "done": true
  }
  ```
  {: screen}

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
  {: screen}


  ```
  wsk activation get b066ca51e68c4d3382df2d8033265db0
  ```
  {: pre}
 ```
  {
      "start": 1455881628103,
      "end":   1455881648126,
      ...
  }
  ```
  {: screen}

  通过比较激活记录中的 `start` 和 `end` 时间戳记，可以看出完成此激活所用时间略微超过 20 秒。


### 使用操作来调用外部 API
{: #openwhisk_apicall_action}

到目前为止，示例都是自包含 JavaScript 函数。您还可以创建调用外部 API 的操作。

以下示例调用 Yahoo Weather 服务来获取特定位置的当前天气状况。 

1. 将以下内容保存在名为 `weather.js` 的文件中。
```
    var request = require('request');
    
    function main(msg) {
        var location = msg.location || 'Vermont';
        var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';
    
        request.get(url, function(error, response, body) {
            var condition = JSON.parse(body).query.results.channel.item.condition;
            var text = condition.text;
            var temperature = condition.temp;
            var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
            whisk.done({msg: output});
        });
    
        return whisk.async();
    }
  ```
  {: codeblock}

  请注意，示例中的操作使用 JavaScript `request` 库向 Yahoo Weather API 发起 HTTP 请求，然后从 JSON 结果中抽取字段。[参考](./openwhisk_reference.html#runtime_ref_runtime_environment)详细描述了可以在操作中使用的 Node.js 包。
  
  此示例还显示了需要异步操作。此操作返回 `whisk.async()`，指示函数返回时此操作的结果尚不可用。相反，结果会在 HTTP 调用完成后在 `request` 回调中提供，并且会作为自变量传递给 `whisk.done()` 函数。

2. 运行以下命令来创建并调用操作：
```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location 'Brooklyn, NY'
  ```
  {: pre}
  ```
  {
      "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
  }
  ```
  {: screen}

### 创建操作序列
{: #openwhisk_create_action_sequence}

可以创建用于将一序列操作链接在一起的操作。

在名为 `/whisk.system/util` 的包中提供了多个实用程序操作，可用于创建第一个序列。您可以在[包](./openwhisk_packages.html)部分中了解有关包的更多信息。

1. 显示 `/whisk.system/util` 包中的操作。
  
  ```
  wsk package get --summary /whisk.system/util
  ```
  {: pre}
  ```
  package /whisk.system/util
   action /whisk.system/util/cat: Concatenate array of strings, and split lines into an array
   action /whisk.system/util/head: Filter first K array elements and discard rest
   action /whisk.system/util/date: Get current date and time
   action /whisk.system/util/sort: Sort array
  ```
  {: screen}

  您将使用此示例中的 `cat` 和 `sort` 操作。

2. 创建操作序列，使一个操作的结果作为自变量传递给下一个操作。
  
  ```
  wsk action create myAction --sequence /whisk.system/util/cat,/whisk.system/util/sort
  ```
  {: pre}

  此操作序列会将一些文本行转换为数组，然后对这些行排序。

3. 调用操作序列之前，请创建名为“haiku.txt”的文本文件，其中包含以下几行文本：

  ```
  Over-ripe sushi,
  The Master
  Is full of regret.
  ```
  {: codeblock}

4. 调用操作：
  
  ```
  wsk action invoke --blocking --result myAction --param payload "$(cat haiku.txt)"
  ```
  {: pre}
  ```
  {
      "length": 3,
      "lines": [
          "Is full of regret.",
          "Over-ripe sushi,",
          "The Master"
      ]
  }
  ```
  {: screen}

  在结果中，您会看到这些行已排序。

**注**：有关使用多个指定参数来调用操作序列的更多信息，请参阅[设置缺省参数](./openwhisk_actions.html##openwhisk_binding_actions)

## 创建 Swift 操作
{: #openwhisk_actions_swift}

创建 Swift 操作的过程与创建 JavaScript 操作的过程类似。以下各部分将指导您创建并调用单个 Swift 操作，然后向该操作添加参数。

您还可以使用在线 [Swift Sandbox](https://swiftlang.ng.bluemix.net) 来测试 Swift 代码，而不必在您的计算机上安装 Xcode。

### 创建并调用操作
{: #openwhisk_actions_invoke_swift}

操作仅仅是顶级 Swift 函数。例如，创建名为 `hello.swift` 的文件并包含以下内容：

```
  func main(args: [String:Any]) -> [String:Any] {
      if let name = args["name"] as? String {
          return [ "greeting" : "Hello \(name)!" ]
      } else {
return [ "greeting" : "Hello stranger!" ]
      }
  }
```
{: codeblock}

请注意，正如 JavaScript 操作一样，Swift 操作始终会使用一个字典并生成一个字典。

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

```
  {
      "greeting": "Hello World!"
  }
```
{: screen}

**注意：**Swift 操作在 Linux 环境中运行。Swift on Linux 仍在开发中；{{site.data.keyword.openwhisk_short}} 通常会使用最新可用发行版，但此版本不一定稳定。此外，用于 {{site.data.keyword.openwhisk_short}} 的 Swift 版本可能与 Mac OS 上 Xcode 的稳定发行版中的 Swift 版本不一致。

## 创建 Docker 操作
{: #openwhisk_actions_docker}

通过 {{site.data.keyword.openwhisk_short}} Docker 操作，可以使用任何语言编写操作。

您的代码会编译为可执行二进制文件，并嵌入到 Docker 映像中。二进制程序通过采用来自 `stdin` 的输入并通过 `stdout` 进行回复，从而与系统进行交互。

作为先决条件，您必须拥有 Docker Hub 帐户。要设置免费 Docker 标识和帐户，请转至 [Docker Hub](https://hub.docker.com){: new_window}。

对于后续指示信息，假定用户标识为“janesmith”，密码为“janes_password”。假定已设置 CLI，必须执行三个步骤来设置定制二进制文件以供 {{site.data.keyword.openwhisk_short}} 使用。在此之后，上传的 Docker 映像即可用作操作。

1. 下载 Docker 框架。可以使用 CLI 进行下载，如下所示：

  ```
  wsk sdk install docker
  ```
  {: pre}
  ```
  现在，Docker 框架已安装在当前目录中。
```
  {: screen}

  ```
  ls dockerSkeleton/
  ```
  {: pre}
  ```
  Dockerfile      README.md       buildAndPush.sh client          server
  ```
  {: screen}

  框架是一种 Docker 容器模板，可以在其中以定制二进制文件的形式插入代码。

2. 在 Docker 框架中设置定制二进制文件。该框架已经包含可以使用的 C 程序。

  ```
  cat ./dockerSkeleton/client/example.c
  ```
  {: pre}
  {: pre}
  ```
  #include <stdio.h>
  
  int main(int argc, char *argv[]) {
      printf("Hello %s from arbitrary C program!\n",
             (argc == 1) ? "anonymous" : argv[1]);
  }
  ```
  {: screen}

  可以根据需要修改此文件。

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

  请注意，在 Docker 映像构建过程中，会对 example.c 文件中的部分内容进行编译，所以无需在您的计算机上对 C 程序进行编译。

4. 要通过 Docker 映像而不是通过提供的 JavaScript 文件来创建操作，请添加 `--docker`，并将 JavaScript 文件名替换为 Docker 映像名称。

  ```
  wsk action create --docker example janesmith/blackboxdemo
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result example --param payload Rey
  ```
  {: pre}
  ```
  {
      "msg": "Hello Rey from arbitrary C program!\n"
  }
  ```
  {: screen}


您可以在[参考](./openwhisk_reference.html#openwhisk_ref_docker)部分中找到有关创建 Docker 操作的更多信息。


## 监视操作输出
{: #openwhisk_actions_polling}

{{site.data.keyword.openwhisk_short}} 操作可能会由其他用户调用，以响应各种事件或作为操作序列的组成部分。在此类情况下，监视调用会非常有用。

可以使用 {{site.data.keyword.openwhisk_short}} CLI 在调用操作时监视其输出。

1. 在 shell 中发出以下命令：```
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
  {: screen}

3. 观察轮询窗口中的激活日志：

  ```
  Activation: helloWorld (7331f9b9e2044d85afd219b12c0f1491)
    2016-02-11T16:46:56.842065025Z stdout: hello bob!
  ```
  {: screen}

  与此类似，每当运行轮询实用程序时，都会实时看到 {{site.data.keyword.openwhisk_short}} 中代表您运行的任何操作的日志。

## 删除操作
{: #openwhisk_delete_action}

可以通过删除不想使用的操作来进行清理。

1. 运行以下命令来删除操作：```
  wsk action delete hello
  ```
  {: pre}
  ```
  ok: deleted hello
  ```
  {: screen}

2. 验证该操作是否不再出现在操作列表中。```
  wsk action list
  ```
  {: pre}
  ```
  actions
  ```
  {: screen}
